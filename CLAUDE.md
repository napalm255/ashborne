# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

---

## Project Overview

**Ashborne: A Maddox Grey Mystery** is a narrative-driven indie game currently in the design documentation phase. It's a mystery/detective experience set in Frederick, Maryland, blending real-world hacking and electronics with supernatural elements.

**Current State**: Pre-production. Design documentation is complete and expanded: full story synopsis, 14 character/NPC profiles, Act 1 full narrative with walkthrough, location maps, crafting system, and gameplay mechanics. No game code implemented yet.

**Platform**: Linux (Bluefin Atomic Desktop, Fedora-based). Engine: **Unreal Engine 5.8** (C++ + Blueprint). Viewpoint: fixed isometric (~45° angle, Diablo-style). Art direction: Gabriel Knight aesthetic (atmospheric, painted quality). Setting: Frederick, Maryland, April–June 2025.

---

## Development Environment Setup

**Bluefin Linux (Primary Platform)**

See `story/systems/development_setup.md` for complete setup guide. Development uses containerized workflow via `toolbox`:

```bash
# One-time setup: create development container
toolbox create -c ue5dev -i quay.io/fedora/fedora:40

# Each session: enter development container
toolbox enter ue5dev
```

**Inside the container:**
- **Unreal Engine 5.8** — Download via Epic Games Launcher; 60–90 GB install
- **clang/LLVM** — C++ compilation on Linux (installed via dnf inside container)
- **Blender 4.x** — 3D asset creation and PBR material texturing; exports to FBX for UE5
- **Quixel/Megascans** — Material library (free with UE license); historic architecture textures
- **Stable Diffusion (AUTOMATIC1111)** — Concept art and mood boards (not final assets)
- **Suno.ai or AudioCraft** — Music generation
- **ffmpeg** — Audio format conversion (MP3 → WAV for UE5)

All UE5.8 development, compilation, and editor work occurs inside the `ue5dev` container. The Bluefin immutable root filesystem is never modified.

---

## Design Documentation Structure

See `story/INDEX.md` for full navigation. All design files organized by type:

**World & Setting** (`story/world/`):
- `overview.md` — Frederick 2025, atmosphere, tone, themes
- `history.md` — Civil War/Ironveil backstory, sealing ritual, the Ashborne
- `locations_exterior.md` — Zones, fast travel routes, geography
- `locations_interior.md` — Interior maps, room-by-room layouts

**Characters** (`story/characters/`):
- Protagonist: `maddox_grey.md`, `wren_calloway.md`, `dexter.md`, `scout_and_finn.md`
- NPCs: 6 individual files in `npcs/` (Nora, Sal, Vivienne, Okafor, Hale, Keeper)

**Story & Acts** (`story/acts/`):
- `synopsis.md` — Three-act structure, themes, logline
- `act1/full_story.md` — Complete prose narrative (14 scenes, April 7–19)
- `act1/walkthrough.md` — Player-facing progression guide
- `act2/overview.md`, `act3/overview.md` — Story beats for later acts

**Gameplay Systems** (`story/systems/`):
- `gameplay_overview.md` — UE5.8 features, isometric camera, Gabriel Knight aesthetic
- `dexter_mechanics.md` — Companion AI, commands, sensor integration
- `crafting_and_gear.md` — Tier 1–3 gear, components, recipes
- `development_setup.md` — UE5.8 environment setup

**Note**: All design documents assume UE5.8 implementation (C++ + Blueprints). Isometric 3D with fixed camera at ~45° pitch.

---

## Toolchain & Development Standards

**All tools must be 100% free** — no trials, subscriptions, or proprietary licenses. Free software includes open source (GPLv3, MIT, Apache 2.0) and free-tier community products.

**Free tool choices**:
- **Blender 4.x** (texture painting, baking, FBX export) — replaces Substance Painter
- **Material Maker** (procedural PBR generation) — open source alternative
- **Unreal Header Tool** (UHT) — built into UE5, validates reflection system
- **clang-format**, **clang-tidy**, **cppcheck** — C++ linting and static analysis
- **UE5 Automation Framework** — built-in, free testing system
- **GitHub Actions** — free CI/CD (self-hosted runner required due to disk space)
- **unreal-mcp** — open source Python MCP server for Claude Code integration

---

## Key Game Systems (to implement)

These are the major systems described in the design docs that will need code:

### 1. **Crafting System** (Tier-based)
- **Tier 1**: Mundane gear (lock picks, pry bars, fiber optic scope, etc.)
- **Tier 2**: Tech gear (RF analyzer, network intrusion kit, surveillance tap, thermal imager, etc.)
- **Tier 3**: Occult-tech hybrid (Null Field Generator, Ashborne Compass, Sealing Transmitter, etc.)

Key mechanics:
- Components (common/uncommon/rare) found via exploration or purchased
- 3D printing integration (FDM and resin printers at workshop, partial field kit)
- Recipe discovery tied to story progression and NPC dialogue
- No build failures — player either has components or doesn't
- Abstracts print time (parts ready on next visit)

### 2. **Investigation & Puzzle Mechanics**
- Network intrusion mini-games (accessing locked systems, extracting data)
- Cipher decryption (Civil War telegraph codes, Ironveil symbols)
- Document analysis (rubbing kit, field notebook, photo reconstruction)
- RF signal analysis (anomaly detection, mapping phenomenon intensity)
- Environmental scanning (thermal imaging, ground penetrating radar)

### 3. **Dexter Companion System**
- Follows Maddox autonomously, responds to commands (Search, Guard, Track, Stand Down)
- Can carry/deploy equipment (camera harness, sensor vest, surveillance taps)
- Supernatural sensitivity — alerts to phenomena before Maddox has explanation for it
- Sidecar mechanics (rides Maddox's motorcycle)

### 4. **Phenomenon System**
- Environmental presence of the Ashborne entity (grows over Acts I–III)
- High-phenomenon zones disrupt electronics, cause cold voids, emit anomalous signals
- Tier 3 gear (Null Field Generator, Faraday Shell) provides protection/immunity
- RF analyzer and thermal imager visualize phenomenon in gameplay

### 5. **Narrative Progression**
- Acts I–III as described in `synopsis.md`
- NPC relationships unlocking story beats and gear recipes
- Document/cipher discoveries gating progression
- Multiple location types (exteriors, interiors, tunnels, decommissioned sites)

---

## Architecture Notes

### Game Structure
- **Single-player**: No multiplayer components
- **Scope**: Contained to Frederick, Maryland (prevents scope creep on assets)
- **Pacing**: Investigation/puzzle flow punctuated by action sequences (confrontations with Ashborne)
- **UI**: Minimalist — mostly diegetic (in-world) interfaces (workshop terminals, phone screens, field notebook)

### Asset Pipeline (Pre-production)
- **3D Models**: Generated via Stable Diffusion → rembg background removal → Blender refinement → FBX export → UE5 import
- **Materials**: Blender texture baking + Material Maker (free alternatives) → PBR maps (albedo, normal, roughness, metallic, AO) → UE5 material instances → applied to assets
- **Audio**: Music via Suno.ai or AudioCraft; SFX from freesound.org (CC0 filtered); all converted to WAV → UE5 MetaSounds
- **Storage**: Content/ directory in UE5 project (.uasset binary format); expect 50+ GB once all assets are generated and imported

### CI/CD & Distribution
- **Testing**: UE5 Automation Framework for unit, functional, and smoke tests. Tests run on every commit via GitHub Actions.
- **Linting**: clang-format, clang-tidy, cppcheck run automatically on commits and PRs.
- **Build Pipeline**: GitHub Actions with self-hosted runner (UE5 is 60–90 GB). Stages: lint → build (Linux Dev) → test → package (Linux Shipping).
- **Releases**: Tagged commits (v*) trigger full package → publish pipeline. Built artifacts uploaded to GitHub Releases as `.tar.gz` (Linux), `.zip` (Windows), `.apk` (Android).
- **Platforms**: Linux primary (development and shipping), Windows secondary (future), Android optional (if easy).

See `story/systems/ci_cd_testing.md` for complete CI/CD, testing, and distribution strategy.

### UE5.8-Specific Patterns
- **C++ Core**: Game logic in C++ classes; exposed properties/functions to Blueprint for iteration
- **Blueprint**: High-level game state, UI, and gameplay sequences in Blueprint; C++ handles performance-critical systems
- **World Partition**: Exterior zones use UE5 World Partition for automatic spatial streaming and memory management
- **Lumen/Nanite**: Dynamic lighting via Lumen; virtualized geometry via Nanite for dense, detailed environments
- **Isometric Camera**: Fixed camera at -50° pitch with no rotation; implemented via Spring Arm + locked camera component
- **Diegetic UI**: In-world interfaces (phone screens, workshop terminals, field notebook) rendered to Screen meshes in world space

---

## Crafting/Gear Implementation Notes

The crafting system is central to the game loop. Key design points:

- **No recipe items**: Recipes unlock procedurally based on story context and component availability. See `crafting_and_gear.md` for unlock triggers.
- **3D Printer abstraction**: Printing is "fire and forget" — parts queue automatically, available on next workshop visit. Don't simulate real print times.
- **Resonant materials**: Late-game components that require the RF analyzer for identification. Glow/emit in thermal imaging. Track separately in inventory.
- **Dexter's contributions**: Three instances where Dexter brings Maddox a needed component. Unexamined by the narrative — just happens. Implement as scripted events, not player-driven.
- **Tier 3 requirements**: Many depend on prior builds (e.g., Resonant Disruptor requires Null Field Generator built first for calibration).

See `crafting_and_gear.md` for full component/recipe inventory and vendor sources.

---

## Writing & Dialogue

- **Tone**: Gritty, grounded, dark humor. Protagonist responds to supernatural events with dry wit and tech jargon.
- **Dexter commentary**: Maddox talks to Dexter constantly — full sentences, running commentary. Dexter's reactions (ears, posture, direction) answer back.
- **NPC Voices**: See individual character files in `story/characters/npcs/`:
  - **Vivienne Colt** (sharp, knowledgeable antiquarian)
  - **Sal Mercer** (working-class pragmatist, best friend)
  - **Nora Grey** (concerned sister, ER nurse)
  - **Ray Okafor** (institutional pressure, detective pragmatism)
  - **The Keeper** (cult leader, seduction/control rhetoric)
- **Documents**: In-world text (cipher fragments, historical records, Ironveil writings, network logs) will be integrated into puzzles and lore delivery.

---

## Content Organization for Future Implementation

When game code begins, expect this UE5.8 project structure:

```
AshborneProject/
├── AshborneProject.uproject           # UE5 project config
├── Source/
│   ├── AshborneProject/
│   │   ├── AshborneProject.Build.cs
│   │   ├── Core/
│   │   │   ├── Player/                # Maddox character controller, movement
│   │   │   ├── Companion/             # Dexter AI, behavior tree, commands
│   │   │   └── Interaction/           # Object examination, dialogue, interactables
│   │   ├── Systems/
│   │   │   ├── Crafting/              # Recipe management, component tracking
│   │   │   ├── Inventory/             # Item storage, equipment slots
│   │   │   ├── Phenomenon/            # Ashborne intensity, effect zones, anomalies
│   │   │   └── Dialogue/              # NPC dialogue trees, relationship state
│   │   ├── Tools/                     # Gear implementations (RF Analyzer, Thermal Imager, etc.)
│   │   ├── UI/                        # Diegetic UI classes (phone, notebook, terminals)
│   │   └── Game/                      # Core game state, save/load, progression
│   └── AshborneProject.cpp
├── Content/
│   ├── Blueprints/
│   │   ├── Character/                 # Maddox, Dexter, NPC blueprints
│   │   ├── Locations/                 # Location-specific logic blueprints
│   │   ├── UI/                        # HUD, menu, crafting UI widgets
│   │   └── GameFlow/                  # Main game, pause, dialogue managers
│   ├── Maps/
│   │   ├── EXT_Frederick/             # Exterior zones (open world partitions)
│   │   ├── INT_Workshop/              # Maddox's workshop, home base
│   │   ├── INT_CityHall/              # City Hall interior with puzzle rooms
│   │   ├── INT_HistoricalSociety/     # Archive research location
│   │   └── [more locations]           # Interior and exterior zones per design
│   ├── Characters/
│   │   ├── Meshes/                    # Maddox, Dexter, NPC models (FBX from Blender)
│   │   └── Materials/                 # PBR materials (from Blender, Material Maker, Megascans)
│   ├── Audio/
│   │   ├── Music/                     # Generated tracks (WAV, converted to MetaSound)
│   │   └── SFX/                       # Sound effects (WAV, 44100Hz, 16-bit)
│   ├── UI/
│   │   ├── Fonts/                     # In-game UI typography
│   │   ├── Icons/                     # Gear, inventory, interaction icons
│   │   └── WidgetBP/                  # UMG widget blueprints
│   ├── Materials/                     # Material instances, post-process effects, cold void visualization
│   └── Data/
│       ├── DT_Characters.uasset       # Data table: NPC properties, dialogue keys
│       ├── DT_Locations.uasset        # Data table: zone metadata, fast travel points
│       ├── DT_Crafting.uasset         # Data table: recipe definitions, components
│       └── DT_CipherFragments.uasset  # Data table: story-gated cipher pieces
```

This is a **suggested structure** — adjust as implementation progresses. All art assets (3D models, textures, audio) are stored in `Content/` as .uasset files.

---

## Testing

All new code should have automated tests where reasonable. Tests use **UE5 Automation Framework** (built-in, free).

### Test Types & Locations

| Type | Location | Command | When |
|------|----------|---------|------|
| Unit tests | `Source/AshborneProject/Tests/` | Run in-editor via Automation window | Every commit (via CI) |
| Functional tests | `Source/AshborneProject/Tests/` + test maps in `Maps/TEST_*.umap` | Headless: `Automation RunTests Ashborne.Functional` | Every commit (via CI) |
| Smoke tests | CI pipeline (Build.sh) | `Build.sh AshborneProject Linux Development` | Every commit |

### Test Naming Convention

Tests follow Conventional Commits scoping: `Ashborne.<System>.<TestName>`

**Examples**:
- `Ashborne.Crafting.RecipeValidation_MissingComponentFails`
- `Ashborne.Inventory.AddItem_StacksCorrectly`
- `Ashborne.Dexter.CommandDispatch_SearchMovesDexter`
- `Ashborne.Phenomenon.IntensityClamp_ClampsToZeroOne`

### Running Tests

**In-editor**: Window → Automation → Select test(s) → Start Tests

**Headless (CI)**: 
```bash
./UnrealEditor AshborneProject.uproject \
  -ExecCmds="Automation RunTests Ashborne" \
  -nullrhi -unattended -nopause
```

**List available tests**:
```bash
./UnrealEditor AshborneProject.uproject \
  -ExecCmds="Automation List" \
  -nullrhi -unattended -nopause
```

See `story/systems/ci_cd_testing.md` for comprehensive testing strategy.

---

## Code Quality & Commit Standards

### Commit Message Convention (Conventional Commits)

Format: `<type>(<scope>): <subject>`

**Types**: `feat`, `fix`, `docs`, `test`, `ci`, `chore`, `refactor`, `perf`, `style`

**Scopes**: `crafting`, `dexter`, `phenomenon`, `ui`, `tools`, `ci`, `docs`, `assets`

**Examples**:
```
feat(crafting): unlock Tier 3 recipes after Ironveil discovery
fix(dexter): fix command dispatch not respecting cooldown
test(phenomenon): validate intensity clamp to [0.0, 1.0]
ci: add Android build workflow
docs: update crafting system architecture
```

See `story/systems/ci_cd_testing.md` for full specification and examples.

### Code Linting

All new C++ code is checked against **clang-format**, **clang-tidy**, and **cppcheck** before merge.

**Manual checks** (before commit):
```bash
# Format check
clang-format --dry-run Source/AshborneProject/**/*.cpp

# Lint check
clang-tidy Source/AshborneProject/**/*.cpp

# Static analysis
cppcheck --enable=all Source/AshborneProject/
```

**CI/CD**: Automatic in GitHub Actions on every push and PR.

---

## Common Commands (UE5.8 Implementation on Bluefin)

All commands run inside the `toolbox enter ue5dev` container.

```bash
# Launch editor
./UnrealEditor AshborneProject.uproject

# Validate project syntax
./UnrealEditor -headless -run=None AshborneProject.uproject

# Build project from command line
./Engine/Build/BatchFiles/Linux/Build.sh AshborneProject Linux Development \
  -Project="path/to/AshborneProject.uproject"

# Cook content for Linux shipping
./Engine/Build/BatchFiles/Linux/RunUAT.sh BuildCookRun \
  -project="path/to/AshborneProject.uproject" \
  -platform=Linux -clientconfig=Shipping -cook -build -stage -archive \
  -archivedirectory="path/to/builds"

# Run game standalone (development)
./Binaries/Linux/AshborneProject-Linux-Shipping -windowed -ResX=1920 -ResY=1080
```

---

## UE5 MCP (Claude Code Integration)

**unreal-mcp** bridges Claude Code to the running UE5 editor for live scripting and testing.

### Setup

Inside `ue5dev` container:
```bash
pip install unreal-mcp
```

Configure in `~/.claude/settings.json`:
```json
{
  "mcpServers": {
    "unreal": {
      "command": "python3",
      "args": ["-m", "unreal_mcp"],
      "env": {
        "UE_PROJECT": "/path/to/AshborneProject.uproject"
      }
    }
  }
}
```

### Usage in Claude Code

**Run tests**: `/unreal run-tests Ashborne.Crafting.*`

**Validate assets**: `/unreal validate-assets DA_*`

**Execute editor script**: `/unreal exec "print GetWorldActorCount()"`

**Query live data**: `/unreal python` + Python script to inspect actors, assets, or game state

See `story/systems/ci_cd_testing.md` for detailed examples.

---

## Story Touchstones

Key narrative milestones to track during implementation:

- **Act I**: Maddox discovers the anomalous partition, first death, Dexter's supernatural sensitivity emerges
- **Act II**: Ironveil history revealed, sealing ritual mechanics introduced, Vivienne becomes ally
- **Act III**: Ashborne directly influences people, final confrontation in sealed tunnels, sealing ritual attempted
- **Cipher**: Built from components scattered across all locations; incomplete cipher = failed sealing
- **Dexter**: Thread about the Phoenix marking and historical connection (left ambiguous — design intentionally)

---

## References

**Master Navigation**: Start at `story/INDEX.md` for all design documentation.

**Story & Character Design**:
- **Lore Bible**: `story/acts/synopsis.md` (three-act structure, themes, logline)
- **Act 1 Complete**: `story/acts/act1/full_story.md` (detailed prose narrative)
- **Act 1 Walkthrough**: `story/acts/act1/walkthrough.md` (player progression guide)
- **Protagonist**: `story/characters/maddox_grey.md` (skills, 2025 toolkit, personality)
- **Love Interest**: `story/characters/wren_calloway.md` (historian, co-investigator)
- **Companion Dog**: `story/characters/dexter.md` (abilities, supernatural sensitivity, narrative role)
- **NPCs**: `story/characters/npcs/` (6 individual files: Nora, Sal, Vivienne, Okafor, Hale, Keeper)

**World & Locations**:
- **Setting Overview**: `story/world/overview.md` (Frederick 2025, atmosphere, tone)
- **History & Lore**: `story/world/history.md` (Civil War backstory, Ironveil, sealing ritual)
- **Exterior Locations**: `story/world/locations_exterior.md` (zones, fast travel routes)
- **Interior Locations**: `story/world/locations_interior.md` (maps, room-by-room design)

**Gameplay Systems**:
- **Gameplay Overview**: `story/systems/gameplay_overview.md` (UE5.8, isometric camera, Gabriel Knight aesthetic)
- **Dexter AI System**: `story/systems/dexter_mechanics.md` (commands, behavior tree, sensor vest)
- **Crafting System**: `story/systems/crafting_and_gear.md` (Tier 1–3 gear, recipes, components)
- **Development Setup**: `story/systems/development_setup.md` (UE5.8 + Bluefin Linux environment)

