# Development Setup Guide — Unreal Engine 5.8

Practical steps for getting the full development environment running from scratch.

---

## 1. Unreal Engine 5.8

Download and install via Epic Games Launcher inside the `ue5dev` container:

- Inside `toolbox enter ue5dev`
- Visit epicgames.com/download
- Download Epic Games Launcher (Linux version)
- Sign in with Epic account (create one if needed)
- Navigate to Unreal Engine tab
- Select Version 5.8.x (latest stable 5.8 release)
- Click "Install"
- Select installation location (recommend SSD, ~60–90 GB)
- Select target platform: **Linux only** (this project compiles for Linux exclusively)
- Install completes in approximately 20–40 minutes depending on internet and disk speed

The Unreal Engine 5.8 binary is the authoritative engine for this project. Do not use engine versions before 5.8 or any other version.

---

## 2. C++ Compiler & Build Tools

**Linux (Bluefin Atomic Desktop — Primary Development Platform):**

Bluefin uses an immutable root filesystem, so development tools are installed in a mutable container via `toolbox`.

```bash
# Create a development container (one-time setup)
toolbox create -c ue5dev -i quay.io/fedora/fedora:40

# Enter the development container
toolbox enter ue5dev

# Inside the container: Install build essentials
sudo dnf groupinstall "Development Tools" "Development Libraries"

# Install clang/LLVM (UE5.8 primary Linux compiler)
sudo dnf install clang llvm-devel

# Install required graphics and X11 libraries
sudo dnf install libX11-devel libXrandr-devel libxcb-devel mesa-libGL-devel libXinerama-devel libXcursor-devel

# Install additional UE5 dependencies
sudo dnf install openssl-devel libicu-devel libuuid-devel tbb-devel

# Verify installation (inside container)
clang --version
clang++ --version
```

**Exiting and re-entering the container:**
```bash
# Exit container (return to host)
exit

# Re-enter the development container
toolbox enter ue5dev
```

**Note**: All UE5.8 development, compilation, and the editor run inside the `ue5dev` container. The immutable root filesystem on Bluefin prevents direct installation of large development tools like UE5.8, so containerization is the standard approach.


---

## 3. Blender 4.x (3D Asset Creation)

Download from blender.org:

- Download Blender 4.x LTS release
- Install per platform instructions
- (Optional) Install Blender-to-Unreal Export plugin for direct asset pipeline
- Verify: Launch Blender, check version in Help → About Blender

Models created in Blender export to FBX or use the bridge plugin for direct import into UE5.

---

## 4. Substance Painter (PBR Texturing)

Download from substance3d.com:

- Create Substance account (free tier available with basic features)
- Download Substance 3D Painter
- Install per platform
- (Optional) Subscribe to Substance Plus for additional materials and plugins

Textures created in Substance Painter export as PBR material packages (albedo, normal, roughness, metallic, AO) for import into UE5 materials.

---

## 5. Quixel/Megascans (Material Library — Free with UE License)

Access via Epic Games account:

- Log into Epic Games account
- Navigate to Megascans.com
- Authorize with Epic account
- Browse material library (3D scans of real materials: brick, stone, wood, metal, concrete)
- Download materials directly or via Quixel Bridge (integrates with UE editor)
- Import into UE5 project (browser-based or Bridge integration)

Megascans is free with your UE5 license. Use extensively for Frederick's historic architecture textures (period brick, weathered stone, aged wood).

---

## 6. Stable Diffusion (Concept Art & Reference)

Setup for local generation (AUTOMATIC1111 webui):

```bash
# Clone AUTOMATIC1111 repository
git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui
cd stable-diffusion-webui

# Download model (DreamShaper XL recommended, ~6 GB)
# Place .safetensors in: models/Stable-diffusion/

# Install ControlNet extension for pose-guided generation
git clone https://github.com/Mikubill/sd-webui-controlnet extensions/sd-webui-controlnet

# Download ControlNet OpenPose model
# Place in: extensions/sd-webui-controlnet/models/

# Launch webui
./webui.sh  # Linux

# Access at http://127.0.0.1:7860
```

Stable Diffusion is used for mood boards, character concept art, and environment reference — not for final assets. Output images inform art direction; actual assets are created in Blender and textured in Substance Painter.

---

## 7. Audio Generation Tools

**Music (Suno.ai):**
- Create account at suno.ai (free tier available)
- Generate 30–60 second tracks with text prompts
- Download as MP3
- Convert to WAV: `ffmpeg -i track.mp3 track.wav`
- Import into UE5 as Sound Wave assets
- Store in Content/Audio/Music/

**Music (Local — AudioCraft):**
```bash
pip install audiocraft
python3 -c "
from audiocraft.models import MusicGen
model = MusicGen.get_pretrained('facebook/musicgen-medium')
model.set_generation_params(duration=60)
wav = model.generate(['dark noir mystery, slow piano, atmospheric'])
from audiocraft.data.audio import audio_write
audio_write('ashborne_theme', wav[0].cpu(), model.sample_rate, strategy='loudness')
"
```

**SFX (Sound Effects):**
- Browse freesound.org with CC0 license filter
- Recommended format: WAV, 44100 Hz, 16-bit stereo
- Download and organize by category (ambience, UI, supernatural, etc.)
- Import into UE5 as Sound Wave assets
- Store in Content/Audio/SFX/

---

## 8. First Project Setup

**Create new project in UE5:**
1. Inside container: `./UnrealEditor` → Unreal Engine tab (or launcher if separate)
2. Click "Create Project"
3. Template: "Third Person" (starting point for isometric camera configuration)
4. Project settings:
   - Project name: "AshborneProject"
   - Engine version: 5.8.x
   - Target platform: Linux (build platform only)
5. Create project (initializes and opens editor)

**Initial configuration:**
- Enable Lumen: Project Settings → Engine → Rendering → Global Illumination → "Lumen"
- Enable Nanite: Project Settings → Engine → Rendering → Nanite
- Enable World Partition: Project Settings → Engine → World Partition → Enable
- Configure save directory: Project Settings → Project → Maps & Modes

**Isometric camera setup:**
In Player Character Blueprint or C++ class:
- Spring Arm component: Target Arm Length = 1500 units
- Camera rotation: Pitch = -50 degrees, Yaw = locked (0), Roll = 0
- Enable "Inherit Pitch/Yaw/Roll" all set to false (fixed camera)
- Camera post-process: vignette intensity 0.5, color grading enabled

---

## 9. Common UE5 Editor Commands (Linux/Bluefin)

All commands run inside the `toolbox enter ue5dev` container:

```bash
# Launch editor
./UnrealEditor AshborneProject.uproject

# Validate project (syntax check)
./UnrealEditor -headless -run=None AshborneProject.uproject

# Build from command line
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

## 10. Source Control Setup

Recommended: Git LFS (Large File Storage) for binary assets on Linux.

**Fedora:**
```bash
# Install Git LFS
sudo dnf install git-lfs

# Initialize repository
git init
git lfs install

# Track binary files
git lfs track "*.uasset"
git lfs track "*.umap"
git lfs track "*.blend"
git lfs track "*.jpg"
git lfs track "*.png"
git lfs track "*.wav"
git lfs track "*.ogg"

# Commit
git add .gitattributes
git commit -m "Initialize LFS tracking"
```

Alternative: Perforce (P4) — Epic's native source control for Unreal teams. Perforce has native Linux support and may perform better than Git LFS on large projects.

**Note for Linux teams**: Ensure all developers have Git LFS installed and that `.gitattributes` is committed before sharing the repo. Without proper LFS setup, binary files will bloat the repository.

---

## 11. Debugging & Performance

**Memory profiler:**
- Console command: `stat unit` (frame time breakdown)
- stat memory (memory allocation overview)
- Use Insights tool for detailed profiling (accessed via editor Tools → Insights)

**Visual debugging:**
- stat levels (draw call count, polygon count)
- wireframe mode: F1 (viewport)
- light complexity view: viewport lighting mode dropdown

---

## 12. GitHub Secrets (for CI/CD, Future)

When setting up automated Linux builds (GitHub Actions or similar), configure repository secrets:

| Secret | Value |
|--------|-------|
| UE5_LICENSE | Automation token from epic.dev (requires Epic account) |
| LINUX_BUILD_ARGS | Any additional Linux build flags (optional) |

---

## Verification Checklist (Bluefin Linux)

After setup is complete inside the `ue5dev` container:

- [ ] `toolbox enter ue5dev` successfully enters the development container
- [ ] Inside container: `clang --version` and `clang++ --version` report 17+
- [ ] UE5.8 Editor launches: `./UnrealEditor AshborneProject.uproject`
- [ ] Blender opens and exports FBX (installed on Bluefin host or in container)
- [ ] Substance Painter opens and can export PBR materials (host or container)
- [ ] Megascans Bridge integrates with UE (Materials library accessible in-editor)
- [ ] Stable Diffusion webui runs at http://127.0.0.1:7860 (host or container)
- [ ] ffmpeg installed (inside container): `ffmpeg -version`
- [ ] AshborneProject opens in editor with Lumen/Nanite/World Partition enabled
- [ ] Linux build succeeds: `./Engine/Build/BatchFiles/Linux/Build.sh AshborneProject Linux Development`

You're ready to begin development on Bluefin Linux.

