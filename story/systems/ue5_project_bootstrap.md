# UE5 Project Bootstrap Specification

Foundational C++ class names, map names, subsystem structure, and naming conventions. These definitions anchor all future implementation phases.

---

## Project Identity

- **Project name**: `AshborneProject`
- **Module name**: `AshborneProject`
- **Copyright header**: `// Copyright 2025 Ashborne Project. All Rights Reserved.`
- **Required plugins**: CommonUI, EnhancedInput, GameplayTags, GameplayMessageRuntime
  - All shipped with UE5.8; no third-party plugins needed for Phase 0–2

---

## Core C++ Classes

| Class | Parent | Pattern | Purpose |
|-------|--------|---------|---------|
| `UAshborneGameInstance` | `UGameInstance` | Standard | Persistent across map loads: save slot pointer, act progress, global flags, phenomenon intensity |
| `AAshborneMenuGameMode` | `AGameModeBase` | Standard | Main menu map — no pawn, UI input only |
| `AAshborneGameMode` | `AGameModeBase` | Standard | Base game mode for all gameplay maps (extends with spawn logic later) |
| `AAshbornePlayerController` | `APlayerController` | Standard | Maddox's controller; input routing, camera setup, CommonUI activation |
| `AMaddoxCharacter` | `ACharacter` | Standard | Maddox's pawn; movement, interaction radius, equipment slots |

---

## Subsystems (UE5.8 pattern — replaces singletons and manager actors)

| Class | Parent | Scope | Purpose |
|-------|--------|-------|---------|
| `USaveSubsystem` | `UGameInstanceSubsystem` | Game Instance | Save/load async wrapper, slot management, auto-save logic |
| `UPhenomenonSubsystem` | `UGameInstanceSubsystem` | Game Instance | Global phenomenon intensity (0.0–1.0), zone registry, broadcasts intensity changes |
| `UCraftingSubsystem` | `UGameInstanceSubsystem` | Game Instance | Recipe state, unlock flags, print queue, component tracking |
| `UDialogueSubsystem` | `UWorldSubsystem` | World | Active dialogue state, per-NPC conversation flags (world-scoped for clean resets) |
| `UInventorySubsystem` | `UWorldSubsystem` | World | Maddox's inventory; world-scoped so it resets cleanly on map load |

### Why Subsystems?

- **UE5 manages lifecycle** — no manual registration, no null checks
- **Automatic Blueprint access** — all subsystems exposed to Blueprints automatically
- **Scope guarantees** — Game Instance subsystems persist, World subsystems reset per level
- **Message routing** — use `UGameplayMessageSubsystem` for decoupled event broadcasting

---

## Maps

| Map File | Purpose | Streaming | Partitions |
|----------|---------|-----------|-----------|
| `Maps/UI_MainMenu.umap` | Main menu background scene | Standard persistent | N/A |
| `Maps/EXT_Frederick_01.umap` | First exterior zone (Act 1) | **World Partition** | Cell size: 12800 (128m) |
| `Maps/INT_Workshop.umap` | Maddox's workshop (home base) | Standard persistent | N/A |
| `Maps/TEST_Sandbox.umap` | Dev/test sandbox — not shipped | Standard persistent | N/A |

- All `EXT_*` maps use **World Partition** for automatic spatial streaming and memory management
- All `INT_*` maps use standard persistent levels (small enough to load entirely)
- **Default map** (Project Settings → Maps & Modes → Game Default Map): `UI_MainMenu`

---

## Save System

- **Class**: `UAshborneSaveGame` (extends `USaveGame`)
- **Slot name**: `"AshborneSave_Slot0"` (single slot; multi-slot deferred to future phase)
- **Save version field**: `int32 SaveVersion = 1` — increment on breaking schema changes
- **Phase 1 fields**:
  - `FName LastMapName` — which map player was in
  - `FVector LastPosition` — player's world position
  - `int32 ActProgress` — story act (1, 2, or 3)
  - `float PhenomenonIntensity` — global Ashborne intensity (0.0–1.0)
- **Always async**: `USaveSubsystem` wraps `AsyncSaveGameToSlot` / `AsyncLoadGameFromSlot`; never call synchronous save on game thread

---

## Gameplay Tags

Define in `Config/DefaultGameplayTags.ini` (auto-generated once project boots).

**Phase 1 tags**:

```ini
[/Script/GameplayTags.GameplayTagsSettings]
+GameplayTagList=(Tag="Ashborne.Act.Act1",DevComment="Story progression — Act 1")
+GameplayTagList=(Tag="Ashborne.Act.Act2",DevComment="Story progression — Act 2")
+GameplayTagList=(Tag="Ashborne.Act.Act3",DevComment="Story progression — Act 3")
+GameplayTagList=(Tag="Ashborne.Story.ThomasHaleDead",DevComment="Thomas Hale death discovered")
+GameplayTagList=(Tag="Ashborne.Gear.Tier1.Unlocked",DevComment="Tier 1 gear recipes available")
+GameplayTagList=(Tag="Ashborne.Gear.Tier2.Unlocked",DevComment="Tier 2 gear recipes available")
+GameplayTagList=(Tag="Ashborne.Phenomenon.Active",DevComment="Ashborne presence detected")
+GameplayTagList=(Tag="Ashborne.Dialogue.Sal.MetMaddox",DevComment="Talked to Sal about Maddox")
```

Use tags for story gates, dialogue conditions, and quest progression — not booleans.

---

## Asset Naming Conventions

| Prefix | Type | Example |
|--------|------|---------|
| `BP_` | Blueprint Actor | `BP_MaddoxCharacter` |
| `WBP_` | Widget Blueprint | `WBP_MainMenu`, `WBP_Phone` |
| `DA_` | Data Asset (PrimaryDataAsset) | `DA_Item_LockPicks`, `DA_Recipe_Tier1` |
| `DT_` | Data Table (simple structured data) | `DT_NPCDialogue` |
| `IMC_` | Input Mapping Context | `IMC_Default` |
| `IA_` | Input Action | `IA_MoveForward`, `IA_Interact` |
| `GT_` | Gameplay Tag Table | (reserved; tags go in DefaultGameplayTags.ini) |
| `UI_` | Menu/UI maps | `UI_MainMenu.umap` |
| `EXT_` | Exterior maps | `EXT_Frederick_01.umap` |
| `INT_` | Interior maps | `INT_Workshop.umap` |
| `TEST_` | Test/dev maps (not shipped) | `TEST_Sandbox.umap` |

---

## Project Settings (`DefaultEngine.ini`)

```ini
[/Script/EngineSettings.GameMapsSettings]
GameInstanceClass=/Script/AshborneProject.AshborneGameInstance
GlobalDefaultGameMode=/Script/AshborneProject.AshborneMenuGameMode
GameDefaultMap=/Game/Maps/UI_MainMenu

[/Script/CommonUI.CommonUISettings]
DefaultThemeClass=/Game/UI/DA_AshborneUITheme.DA_AshborneUITheme_C
```

---

## Input System (Enhanced Input — UE5 standard)

**Initial Input Actions** (all defined in `Content/Input/Actions/`):

- `IA_MoveForward` — W key, gamepad thumbstick Y
- `IA_MoveRight` — A/D keys, gamepad thumbstick X
- `IA_Interact` — E key
- `IA_Sprint` — Left Shift
- `IA_UINavigate` — arrow keys, gamepad D-pad, thumbstick
- `IA_UIConfirm` — Enter, gamepad A button
- `IA_UIBack` — Escape, gamepad B button

**Input Mapping Context**: `IMC_Default`
- Applied to player controller via `UEnhancedInputLocalPlayerSubsystem::AddMappingContext` on possess
- Do NOT use legacy `BindAxis`, `BindAction` — always use Enhanced Input

---

## C++ Code Organization

**Source tree**:

```
Source/
├── AshborneProject/
│   ├── Core/
│   │   ├── AshborneGameInstance.h/.cpp
│   │   ├── AshborneGameMode.h/.cpp
│   │   ├── AshborneMenuGameMode.h/.cpp
│   │   ├── AshbornePlayerController.h/.cpp
│   │   └── AshborneSaveGame.h/.cpp
│   ├── Character/
│   │   └── MaddoxCharacter.h/.cpp
│   ├── Subsystems/
│   │   ├── SaveSubsystem.h/.cpp
│   │   ├── PhenomenonSubsystem.h/.cpp
│   │   ├── CraftingSubsystem.h/.cpp
│   │   ├── DialogueSubsystem.h/.cpp
│   │   └── InventorySubsystem.h/.cpp
│   ├── Tools/
│   ├── Interaction/
│   ├── UI/
│   ├── Tests/
│   └── AshborneProject.cpp
└── AshborneProject.Build.cs
```

---

## UE5.8 Best Practices Enforced

| Practice | Implementation |
|----------|-----------------|
| **CommonUI for all interactive UI** | All menu/HUD widgets extend `UCommonActivatableWidget`, all buttons extend `UCommonButtonBase` |
| **Subsystems instead of singletons** | Every game system lives in a `UGameInstanceSubsystem` or `UWorldSubsystem`; no static `Get()` functions |
| **Enhanced Input (not legacy Input)** | All input via Enhanced Input system; no `BindAxis`, no legacy Input callbacks |
| **Gameplay Tags for state** | Dialogue flags, story gates, gear unlocks — use `FGameplayTag`, never `bool` |
| **Soft references** | All asset pointers in data assets use `TSoftObjectPtr`, loaded on demand |
| **Async save/load** | `USaveSubsystem` wraps async operations; never block game thread on save |
| **Gameplay Messages** | Decoupled event broadcasting via `UGameplayMessageSubsystem` |
| **World Partition on EXT_* maps** | Automatic spatial streaming, memory management |

---

## Critical Notes

- **Names are permanent.** Renaming C++ classes in UE5 is painful. Use the names above and don't deviate.
- **Do not add code before Phase 0.** Bootstrap phase only: stub implementations, empty headers, plugin setup.
- **Never use hard references to assets.** Always `TSoftObjectPtr` for maps, materials, audio.
- **Subsystems are always available.** Use `GetGameInstance()->GetSubsystem<USaveSubsystem>()` — no null checks needed (UE5 manages lifecycle).
