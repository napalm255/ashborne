# CI/CD, Testing, and Distribution — Ashborne Project

Comprehensive guide to automated testing, continuous integration/deployment, and release management for Ashborne on Linux (primary), Windows (secondary), and Android (optional).

---

## Testing Strategy

The Ashborne project uses **UE5 Automation Framework** (built-in, free) for unit, functional, and smoke testing. Tests are part of the codebase and run on every commit via GitHub Actions.

### What We Test

| System | Type | Method | When |
|--------|------|--------|------|
| Crafting recipe math | Unit | `IMPLEMENT_SIMPLE_AUTOMATION_TEST` | Every commit |
| Data asset validation | Unit | Asset referential checks | Every commit |
| Inventory add/remove | Unit | Inventory subsystem tests | Every commit |
| Cipher decryption logic | Unit | Cipher/parser unit tests | Every commit |
| Phenomenon intensity clamping | Unit | Float math bounds checks | Every commit |
| Dexter command dispatch | Functional | `AFunctionalTest` in level | Every commit |
| Player → workbench interaction | Functional | `AFunctionalTest` in level | Every commit |
| Project compilation | Smoke | Headless build | Every commit |

### What We Don't Test

- **Art direction and atmosphere** — visual and emotional intent cannot be automated; requires human eye
- **Narrative quality** — dialogue, pacing, emotional beats require human judgment
- **Camera feel** — player experience of camera responsiveness and lag
- **Audio atmosphere** — emotional weight and immersion of soundscape
- **Performance targets** — profiling is manual; UE Insights is the authoritative tool

### Unit Tests

Written in C++ with the UE5 Automation Framework macro `IMPLEMENT_SIMPLE_AUTOMATION_TEST`.

**Location**: `Source/AshborneProject/Tests/`

**Naming convention**: `Ashborne.<System>.<TestName>`

**Examples**:
- `Ashborne.Crafting.RecipeValidation_MissingComponentFails`
- `Ashborne.Inventory.AddItem_StacksCorrectly`
- `Ashborne.Phenomenon.IntensityClamp_ClampsToZeroOne`
- `Ashborne.Cipher.DecryptTelegraphCode_ValidSignatureDecodes`

**Structure**:
```cpp
IMPLEMENT_SIMPLE_AUTOMATION_TEST(FCraftingRecipeTest, "Ashborne.Crafting.RecipeValidation", EAutomationTestFlags::ApplicationContextMask | EAutomationTestFlags::ProductFilter)

bool FCraftingRecipeTest::RunTest(const FString& Parameters)
{
    // Arrange
    FEngineBuild RecipeBuild;
    RecipeBuild.RequiredComponent = EComponentType::RFAnalyzer;
    
    // Act
    bool bCanBuild = RecipeBuild.ValidateRequirements();
    
    // Assert
    TestTrue("Recipe should require RF Analyzer", bCanBuild);
    return true;
}
```

### Data Asset Validation Tests

All crafting and gear data assets (`DA_CraftingRecipe`, `DA_GearItem`, `DA_ComponentItem`) must have required fields populated. Tests run via `Ashborne.Data.*` test suite.

**Checks**:
- `DA_CraftingRecipe`: Display name, description, required components array not empty, printer selection (FDM or resin), output item reference populated
- `DA_GearItem`: Display name, description, tier level, weight, rarity
- `DA_ComponentItem`: Display name, description, rarity, weight, vendor/source

**Execution**: Automatic on asset load during test run; failures halt test suite and report which asset is missing required fields.

### Functional Tests

Using `AFunctionalTest` actors placed in dedicated test maps (`Maps/TEST_Crafting.umap`, `Maps/TEST_Dexter.umap`, etc.).

**Test flow**:
1. Spawn player character at known position
2. Interact with world objects (workbench, NPC, gear)
3. Execute gameplay flow (craft item, command Dexter, pick up component)
4. Assert expected state (inventory contains item, Dexter moved, etc.)

**Examples**:
- **Crafting Flow**: Player has components → accesses workbench → selects recipe → initiates print → returns on next visit → item in inventory
- **Dexter Commands**: Dexter at player position → send "Search" command → Dexter moves to search zone → sends alert or returns
- **Phenomenon Intensity**: Intensity set to 0.5 → enter high-phenomenon zone → Dexter agitates → RF analyzer static increases

**Execution**: `AFunctionalTest::ExecuteTest()` called by automation framework; results logged and reported.

### Smoke Tests

**Compilation Check**: Does the project compile without errors?

- Runs via `Build.sh` on Linux target in CI/CD
- Reports compile errors immediately; no need to run full test suite if compilation fails
- Fastest feedback loop for build-breaking changes

---

## Static Analysis & Linting

### clang-format

**Purpose**: Enforce consistent C++ code style across the project.

**Installation** (inside `ue5dev` container):
```bash
sudo dnf install clang-tools-extra
```

**Configuration**: Place `.clang-format` in project root (see example below).

**UE5 Style Profile**:
- Indentation: 4 spaces (no tabs)
- Opening braces: Allman style (opening brace on new line for functions/classes)
- Column limit: 120 characters
- Include sorting: alphabetical, then local includes
- Pointer alignment: left (int* ptr, not int *ptr)

**Example `.clang-format`**:
```yaml
BasedOnStyle: LLVM
IndentWidth: 4
ColumnLimit: 120
UseTab: Never
BreakBeforeBraces: Allman
BinPackParameters: false
PointerAlignment: Left
IncludeBlocks: Regroup
```

**Usage**:
```bash
# Format a single file
clang-format -i Source/AshborneProject/Core/Player/MaddoxCharacter.cpp

# Check all files without modifying
clang-format --dry-run Source/AshborneProject/**/*.cpp

# CI: Fail if formatting differs
clang-format Source/AshborneProject/**/*.cpp --output-replacements-xml | grep -q '<replacement ' && exit 1
```

### clang-tidy

**Purpose**: Detect bugs, style violations, and UE5-specific anti-patterns.

**Installation** (inside `ue5dev` container):
```bash
sudo dnf install clang-tools-extra
```

**Configuration**: Place `.clang-tidy` in project root (see example below).

**Checks**:
- `modernize-*` — Suggest modern C++ idioms (range-based for, nullptr instead of NULL)
- `readability-*` — Suspicious code patterns (implicit conversions, redundant declarations)
- `performance-*` — Performance anti-patterns (unnecessary copies, inefficient string operations)
- `bugprone-*` — Common mistakes (use of uninitialized variables, integer overflows)
- `cppcoreguidelines-*` — C++ Core Guidelines compliance (avoid raw pointers where unique_ptr fits)
- `portability-*` — Platform-specific issues (endianness assumptions)

**UE5-Specific Checks** (custom):
- Flag raw `new`/`delete` outside UPROPERTY management
- Flag missing `UCLASS()` macro on class definitions
- Flag missing `UPROPERTY()` on member variables that should be exposed

**Example `.clang-tidy`**:
```yaml
Checks: >
  -clang-diagnostic-*,
  -clang-analyzer-*,
  modernize-*,
  readability-*,
  performance-*,
  bugprone-*,
  cppcoreguidelines-avoid-c-arrays,
  cppcoreguidelines-avoid-magic-numbers,
  cppcoreguidelines-init-variables,
  cppcoreguidelines-no-malloc,
  cppcoreguidelines-pro-bounds-array-to-pointer-decay,
  cppcoreguidelines-pro-type-member-init,
  portability-*
WarningsAsErrors: '*'
HeaderFilterRegex: 'Source/AshborneProject/.*'
CheckOptions:
  - key: readability-identifier-naming.FunctionCase
    value: CamelCase
  - key: readability-identifier-naming.VariableCase
    value: CamelCase
  - key: readability-identifier-naming.ClassCase
    value: CamelCase
```

**Usage**:
```bash
# Run on single file
clang-tidy Source/AshborneProject/Core/Player/MaddoxCharacter.cpp

# Run on all files in directory
clang-tidy Source/AshborneProject/**/*.cpp

# CI: Generate report
clang-tidy Source/AshborneProject/**/*.cpp > /tmp/tidy-report.txt 2>&1
```

### cppcheck

**Purpose**: Supplemental static analysis for classic C++ bugs not caught by clang-tidy.

**Installation** (inside `ue5dev` container):
```bash
sudo dnf install cppcheck
```

**Configuration**: Command-line flags in CI/CD (no config file needed).

**Checks**:
- Memory leaks (objects allocated but never freed)
- Use of uninitialized variables
- Null pointer dereferences
- Buffer overflows
- Integer overflow
- Dead code

**Usage**:
```bash
# Analyze project
cppcheck --enable=all --suppress=missingIncludeSystem \
  --project=AshborneProject.uproject \
  Source/AshborneProject/

# Output to file for review
cppcheck --enable=all --xml --output-file=cppcheck-report.xml Source/AshborneProject/
```

### Unreal Header Tool (UHT)

**Purpose**: Enforces Unreal's reflection system constraints (UCLASS, UPROPERTY, UFUNCTION macros).

**Built-in**: UHT runs automatically during project build.

**What it catches**:
- Missing or malformed `UCLASS()` macros on Actor/Component subclasses
- Missing `UPROPERTY()` on members that need reflection
- Invalid function signatures for `UFUNCTION()`
- Circular header includes that break reflection

**Output**: Build fails if UHT reports errors; no special setup required.

---

## GitHub Actions CI/CD

### Runner Setup

**Requirement**: Self-hosted runner (GitHub-hosted runners have ~14 GB disk; UE5 requires 60–90 GB).

**Setup** (one-time):
```bash
# On dev machine, inside ue5dev container:
cd /path/to/actions-runner
./config.sh --url https://github.com/your-org/zgame --token YOUR_REGISTRATION_TOKEN

# Start runner (as systemd service or in tmux)
./run.sh
```

**Registration token**: Found in repo Settings → Actions → Runners → New self-hosted runner.

### Workflow Files

All workflows live in `.github/workflows/`.

#### `main.yml` — Lint, Build, Test (on every push to `main` and PRs)

```yaml
name: CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  lint:
    runs-on: [self-hosted, linux, ue5]
    steps:
      - uses: actions/checkout@v4
      
      - name: clang-format check
        run: |
          clang-format --dry-run Source/AshborneProject/**/*.cpp | grep -q '<replacement' && exit 1 || exit 0
      
      - name: clang-tidy
        run: clang-tidy Source/AshborneProject/**/*.cpp -- -I${{ env.UE5_INCLUDE_PATHS }}
      
      - name: cppcheck
        run: cppcheck --enable=all --suppress=missingIncludeSystem Source/AshborneProject/

  build-linux:
    runs-on: [self-hosted, linux, ue5]
    needs: lint
    steps:
      - uses: actions/checkout@v4
      
      - name: Build (Development)
        run: |
          ${{ env.UE5_PATH }}/Engine/Build/BatchFiles/Linux/Build.sh \
            AshborneProject Linux Development \
            -Project="${{ github.workspace }}/AshborneProject.uproject"

  test:
    runs-on: [self-hosted, linux, ue5]
    needs: build-linux
    steps:
      - uses: actions/checkout@v4
      
      - name: Run Automation Tests
        run: |
          ${{ env.UE5_PATH }}/Engine/Binaries/Linux/UE4Editor \
            AshborneProject.uproject \
            -ExecCmds="Automation RunTests Ashborne" \
            -nullrhi \
            -unattended \
            -nopause

  package-linux:
    runs-on: [self-hosted, linux, ue5]
    needs: test
    if: startsWith(github.ref, 'refs/tags/v')
    steps:
      - uses: actions/checkout@v4
      
      - name: Cook and Package (Shipping)
        run: |
          ${{ env.UE5_PATH }}/Engine/Build/BatchFiles/Linux/RunUAT.sh BuildCookRun \
            -project="${{ github.workspace }}/AshborneProject.uproject" \
            -platform=Linux \
            -clientconfig=Shipping \
            -cook -build -stage -archive \
            -archivedirectory="${{ github.workspace }}/builds"
      
      - name: Create Release and Upload
        uses: softprops/action-gh-release@v1
        with:
          files: builds/AshborneProject-Linux-Shipping.tar.gz
        env:
          GITHUB_TOKEN: ${{ secrets.GH_TOKEN }}
```

#### `build-windows.yml` — Windows build (optional, manual dispatch or tag)

```yaml
name: Build Windows

on:
  workflow_dispatch:
  push:
    tags: ['v*']

jobs:
  build-windows:
    runs-on: [self-hosted, windows, ue5]
    steps:
      - uses: actions/checkout@v4
      
      - name: Build (Development)
        run: |
          & "${{ env.UE5_PATH }}\Engine\Build\BatchFiles\Windows\Build.bat" `
            AshborneProject Win64 Development `
            -Project="${{ github.workspace }}\AshborneProject.uproject"

  package-windows:
    runs-on: [self-hosted, windows, ue5]
    needs: build-windows
    if: startsWith(github.ref, 'refs/tags/v')
    steps:
      - uses: actions/checkout@v4
      
      - name: Cook and Package (Shipping)
        run: |
          & "${{ env.UE5_PATH }}\Engine\Build\BatchFiles\Windows\RunUAT.bat" BuildCookRun `
            -project="${{ github.workspace }}\AshborneProject.uproject" `
            -platform=Win64 `
            -clientconfig=Shipping `
            -cook -build -stage -archive `
            -archivedirectory="${{ github.workspace }}\builds"
      
      - name: Upload to Release
        uses: softprops/action-gh-release@v1
        with:
          files: builds/AshborneProject-Win64-Shipping.zip
        env:
          GITHUB_TOKEN: ${{ secrets.GH_TOKEN }}
```

#### `build-android.yml` — Android build (optional, manual or `[android]` commit tag)

```yaml
name: Build Android

on:
  workflow_dispatch:
  push:
    branches: [main]
    tags: ['v*']

jobs:
  build-android:
    runs-on: [self-hosted, linux, ue5, android]
    if: contains(github.event.head_commit.message, '[android]') || startsWith(github.ref, 'refs/tags/v')
    steps:
      - uses: actions/checkout@v4
      
      - name: Build (Development)
        run: |
          ${{ env.UE5_PATH }}/Engine/Build/BatchFiles/Linux/Build.sh \
            AshborneProject Android Development \
            -Project="${{ github.workspace }}/AshborneProject.uproject"

  package-android:
    runs-on: [self-hosted, linux, ue5, android]
    needs: build-android
    if: startsWith(github.ref, 'refs/tags/v')
    steps:
      - uses: actions/checkout@v4
      
      - name: Cook and Package (Shipping, ARM64)
        run: |
          ${{ env.UE5_PATH }}/Engine/Build/BatchFiles/Linux/RunUAT.sh BuildCookRun \
            -project="${{ github.workspace }}/AshborneProject.uproject" \
            -platform=Android \
            -clientconfig=Shipping \
            -cook -build -stage -archive \
            -archivedirectory="${{ github.workspace }}/builds"
      
      - name: Upload to Release
        uses: softprops/action-gh-release@v1
        with:
          files: builds/AshborneProject-Android-Shipping.apk
        env:
          GITHUB_TOKEN: ${{ secrets.GH_TOKEN }}
```

### Environment Variables (GitHub Secrets)

Configure in repo Settings → Secrets and Variables → Actions:

| Secret | Value | Purpose |
|--------|-------|---------|
| `GH_TOKEN` | GitHub personal access token (repo + releases scopes) | Create releases and upload artifacts |
| `UE5_PATH` | `/path/to/UnrealEngine/5.8` on self-hosted runner | Path to UE5 installation |
| `RUNNER_TOKEN` | GitHub-issued runner registration token | Register self-hosted runner |

---

## Commit Message Convention

**Standard**: Conventional Commits (https://www.conventionalcommits.org/)

**Format**: `<type>(<scope>): <subject>`

**Constraints**:
- Subject under 72 characters
- Imperative mood ("add", not "added" or "adds")
- No period at end
- Scope optional but encouraged

**Types**:
- `feat` — New feature (new gear recipe, new NPC interaction, etc.)
- `fix` — Bug fix (crafting logic error, Dexter AI issue, etc.)
- `docs` — Documentation only (update story files, README, etc.)
- `test` — Add or update tests; no code change
- `ci` — CI/CD configuration, workflows, linting config
- `chore` — Build, dependencies, non-functional cleanup
- `refactor` — Restructure code without changing behavior
- `perf` — Performance improvement (optimize queries, reduce memory)
- `style` — Code style (formatting, variable naming consistency)

**Scopes** (optional but encouraged):
- `crafting` — Crafting system, recipes, components
- `dexter` — Dexter companion AI, commands, behavior
- `phenomenon` — Ashborne presence, phenomenon intensity, effects
- `ui` — User interface, HUD, menus, widgets
- `tools` — Gear/equipment systems (RF analyzer, thermal imager, etc.)
- `ci` — CI/CD, testing, tooling
- `docs` — Documentation
- `assets` — 3D models, materials, audio, art direction

**Examples**:
```
feat(crafting): unlock Tier 3 recipes after Ironveil discovery
fix(dexter): fix command dispatch not respecting cooldown
docs: update crafting system overview in story/systems/
test(phenomenon): validate intensity clamp to [0.0, 1.0]
ci: add Android build workflow with manual dispatch
chore: update LLVM to clang-18 for better UE5.8 support
refactor(inventory): extract component deduplication logic
perf(ui): memoize crafting recipe lookups
```

### Enforcement (commitlint)

**Installation** (project root):
```bash
npm install --save-dev @commitlint/config-conventional @commitlint/cli
```

**Configuration** (`commitlint.config.js`):
```javascript
module.exports = {
  extends: ['@commitlint/config-conventional'],
  rules: {
    'type-enum': [2, 'always', ['feat', 'fix', 'docs', 'test', 'ci', 'chore', 'refactor', 'perf', 'style']],
    'scope-enum': [2, 'always', ['crafting', 'dexter', 'phenomenon', 'ui', 'tools', 'ci', 'docs', 'assets']],
    'subject-max-length': [2, 'always', 72],
  },
};
```

**GitHub Actions Check** (in CI workflow):
```yaml
- name: Commitlint
  run: npx commitlint --from HEAD~1 --to HEAD
```

---

## GitHub Packages & Releases

### Publish Builds to GitHub Releases

**Trigger**: Tagged commit (`v1.0.0`, `v1.0.0-beta.1`, etc.)

**Assets**:
- `AshborneProject-Linux-Shipping.tar.gz` — Linux build
- `AshborneProject-Win64-Shipping.zip` — Windows build (if built)
- `AshborneProject-Android-Shipping.apk` — Android APK (if built)
- `CHANGELOG.md` — Release notes (manual, before tagging)

**Creation**:
```bash
# Tag a commit
git tag -a v0.1.0 -m "Pre-alpha: Act I complete, crafting system functional"
git push origin v0.1.0

# CI/CD automatically builds, packages, and publishes to GitHub Releases
# Access at: https://github.com/user/zgame/releases/tag/v0.1.0
```

### Publish to GitHub Container Registry (Optional)

Containerized delivery via `ghcr.io`:

**Dockerfile**:
```dockerfile
FROM ubuntu:22.04

# Install runtime dependencies
RUN apt-get update && apt-get install -y libssl3 libicu70 libuuid1

# Copy packaged build
COPY AshborneProject-Linux-Shipping /app/ashborne

ENV LD_LIBRARY_PATH="/app/ashborne/lib:$LD_LIBRARY_PATH"
ENTRYPOINT ["/app/ashborne/bin/AshborneProject"]
```

**Build and Push** (in CI workflow):
```yaml
- name: Build and Push OCI Image
  run: |
    docker build -t ghcr.io/user/zgame:${{ github.ref_name }} .
    echo "${{ secrets.GITHUB_TOKEN }}" | docker login ghcr.io -u ${{ github.actor }} --password-stdin
    docker push ghcr.io/user/zgame:${{ github.ref_name }}
```

---

## Android Support

### Prerequisites

**NDK Setup** (inside `ue5dev` container):
```bash
sudo dnf install android-tools

# Install Android SDK/NDK via sdkmanager
sdkmanager "ndk;25.2.9519653"
sdkmanager "platforms;android-26"
sdkmanager "build-tools;35.0.0"
sdkmanager "cmdline-tools;latest"
```

**Environment Variables**:
```bash
export ANDROID_HOME=$HOME/Android/Sdk
export ANDROID_SDK_ROOT=$ANDROID_HOME
export ANDROID_NDK=$ANDROID_HOME/ndk/25.2.9519653
export PATH=$ANDROID_HOME/cmdline-tools/latest/bin:$PATH
```

### UE5 Android Configuration

In `AshborneProject.uproject`:
```json
{
  "Platforms": [
    "Linux",
    "Win64",
    "Android"
  ],
  "TargetPlatforms": ["Linux", "Win64", "Android"]
}
```

In `Project Settings → Platforms → Android`:
- **Package name**: `com.napalm255.ashborne`
- **Minimum API level**: 26 (Android 8.0)
- **Target API level**: 34
- **Architecture**: arm64-v8a (64-bit ARM)
- **Enable Vulkan**: Yes (primary graphics API)

### Building for Android

```bash
# Inside ue5dev container
$UE5_PATH/Engine/Build/BatchFiles/Linux/Build.sh \
  AshborneProject Android Development \
  -Project="/path/to/AshborneProject.uproject"

# Cook and package for shipping
$UE5_PATH/Engine/Build/BatchFiles/Linux/RunUAT.sh BuildCookRun \
  -project="/path/to/AshborneProject.uproject" \
  -platform=Android \
  -clientconfig=Shipping \
  -cook -build -stage -archive \
  -archivedirectory="/path/to/builds"
```

Output: `AshborneProject-Android-Shipping.apk`

### Distribution

- Upload to GitHub Releases (tagged builds in CI)
- Optional: Google Play Store (requires developer account; out of scope for pre-alpha)
- Direct APK distribution for testing

---

## UE5.8 MCP Integration

### Overview

**MCP Server**: `unreal-mcp` (Python-based, community-maintained, open source)

**Bridge**: Connects Claude Code to running UE5 editor for live scripting and testing.

**Use cases**:
- Run Automation Tests from Claude Code without leaving editor
- Execute editor utility scripts (asset validation, batch operations)
- Inspect data asset fields and fix missing properties
- Trigger cook/build from within a coding session
- Query project state (actor count, memory usage, etc.)

### Setup

**Inside `ue5dev` container**:
```bash
# Install unreal-mcp package
pip install unreal-mcp

# Verify installation
pip show unreal-mcp
```

**Configure in Claude Code** (`~/.claude/settings.json`):
```json
{
  "mcpServers": {
    "ollama": { /* existing Ollama config */ },
    "unreal": {
      "command": "python3",
      "args": ["-m", "unreal_mcp"],
      "env": {
        "UE_PROJECT": "/path/to/AshborneProject.uproject",
        "EDITOR_PORT": "6776"
      }
    }
  }
}
```

### Example Usage in Claude Code

**Run a test suite**:
```
/unreal run-tests Ashborne.Crafting.*
```

**Validate all data assets**:
```
/unreal validate-assets DA_*
```

**Query actor count**:
```
/unreal exec "print GetWorldActorCount()"
```

**Batch fix missing properties**:
```
/unreal python << 'EOF'
import unreal
recipes = unreal.AssetRegistry.get_assets_by_class(unreal.CraftingRecipe)
for recipe in recipes:
    if not recipe.get_editor_property('display_name'):
        print(f"Missing display_name in {recipe.get_full_name()}")
EOF
```

---

## Troubleshooting

### Build Fails on Self-Hosted Runner

**Check runner is up**:
```bash
# On runner machine
cd /path/to/actions-runner
./run.sh
```

**Check UE5 path**:
```bash
echo $UE5_PATH
ls $UE5_PATH/Engine/Build/BatchFiles/Linux/Build.sh
```

### Tests Don't Run

**Verify UHT worked**:
```bash
./UnrealEditor AshborneProject.uproject -ExecCmds="Automation List" -nullrhi -unattended
```

If tests don't show, check that test classes use `IMPLEMENT_SIMPLE_AUTOMATION_TEST` and proper module linkage.

### clang-tidy False Positives

UE5 macros sometimes confuse clang-tidy. Suppress false positives with `// NOLINT` inline or update `.clang-tidy` config to exclude them.

### cppcheck Reports Memory Leaks in UE5 Code

If cppcheck reports leaks in UE5 internals, suppress with:
```bash
cppcheck --enable=all --suppress=unusedFunction:*Unreal* --suppress=memleak:*Unreal* Source/AshborneProject/
```

---

## Reference

- **UE5 Automation Framework**: https://docs.unrealengine.com/5.0/en-US/automation-testing-in-unreal-engine/
- **clang-format**: https://clang.llvm.org/docs/ClangFormat/
- **clang-tidy**: https://clang.llvm.org/extra/clang-tidy/
- **cppcheck**: https://cppcheck.sourceforge.io/
- **Conventional Commits**: https://www.conventionalcommits.org/
- **GitHub Actions**: https://docs.github.com/en/actions
- **UE5 Android Setup**: https://docs.unrealengine.com/5.0/en-US/how-to-set-up-android-sdk-and-ndk-for-unreal-engine/
