# Development Phases: Ashborne

**Living document** — update status and checkboxes as work completes.

---

**Last updated**: 2026-06-26
**Current phase**: Phase 0 (not started)
**Overall status**: Pre-production complete; implementation not begun

---

## Status Key
- `[ ]` Not started
- `[~]` In progress
- `[x]` Complete
- `[-]` Skipped / deferred

---

## Why This Order

Game development works best vertically — get one thing fully working before starting the next. AI works best on well-defined, bounded tasks with a clear "done" state. Each phase should be fully testable in isolation.

**Never start Phase N+1 until Phase N passes its smoke test.** Incomplete dependencies create placeholder debt fast.

---

## [ ] Phase 0: Project Bootstrap

**Goal**: Empty UE5.8 project compiles, runs, opens to a black screen.
**Status**: Not started

### Tasks
- [ ] Create `AshborneProject.uproject` with C++ module
- [ ] Enable plugins: CommonUI, EnhancedInput, GameplayTags, GameplayMessageRuntime
- [ ] Stub `UAshborneGameInstance`, `AAshborneMenuGameMode` (empty bodies)
- [ ] Create `Maps/UI_MainMenu.umap` (empty level)
- [ ] Configure `DefaultEngine.ini` per `ue5_project_bootstrap.md`
- [ ] CI validates: project compiles headless without error

**Done when**: `UnrealEditor AshborneProject.uproject` opens without crashing.

---

## [ ] Phase 1: Main Menu

**Goal**: Game opens to an atmospheric main menu with working navigation.
**Status**: Not started
**Spec**: `main_menu_spec.md`

### Tasks
- [ ] Implement `WBP_MainMenu` extending `UCommonActivatableWidget`
- [ ] Button classes extend `UCommonButtonBase` (auto-focus, back-button handling)
- [ ] `UI_MainMenu.umap` background scene (Frederick night — placeholder assets fine)
- [ ] Settings submenu: display, audio, controls (placeholders) — push/pop via CommonUI widget stack
- [ ] `USaveSubsystem` stub with `HasSaveData()` method
- [ ] Fade from black on launch (~1.5 sec); fade to black on New Game
- [ ] Ambient audio placeholder (MetaSound source with sub-bass undertone)

**UE5.8**: CommonUI handles focus and back-button automatically. Do not manage widget focus manually.

**Done when**: Game launches → menu shows → New Game fades to black and loads test level.

---

## [ ] Phase 2: Core Movement

**Goal**: Maddox moves in the world with the isometric camera locked.
**Status**: Not started

### Tasks
- [ ] `AMaddoxCharacter` with capsule collision + placeholder mesh (no animation yet)
- [ ] `AAshbornePlayerController` with Enhanced Input (`IMC_Default`)
- [ ] Isometric camera: `USpringArmComponent` at -50° pitch, `bInvertPitch = false`, locked rotation, no camera lag
- [ ] `INT_Workshop.umap` as first gameplay test level
- [ ] Navigation Mesh baked on workshop floor (needed for Dexter AI Phase 9)
- [ ] Character slides around freely — placeholder animation or T-pose is fine

**UE5.8**: Use `UEnhancedInputLocalPlayerSubsystem::AddMappingContext` on controller possess. Do not use legacy `BindAxis`.

**Done when**: New Game → Maddox slides around workshop, isometric camera is correct angle.

---

## [ ] Phase 3: Save / Load

**Goal**: Game state persists across sessions.
**Status**: Not started

### Tasks
- [ ] `UAshborneSaveGame` class: `FName LastMapName`, `FVector LastPosition`, `int32 ActProgress`, `float PhenomenonIntensity`, `int32 SaveVersion`
- [ ] `USaveSubsystem` implementation: async save on map transition, async load on game start
- [ ] Continue on main menu restores last map + position correctly
- [ ] Save slot: `"AshborneSave_Slot0"` (single slot; multi-slot deferred)

**UE5.8**: Always `AsyncSaveGameToSlot` with callback. Never block game thread on synchronous save.

**Done when**: Move Maddox → quit to menu → Continue → Maddox is at correct saved position.

---

## [ ] Phase 4: Map Transitions & Level Loading

**Goal**: Multiple maps load and unload with clean transitions.
**Status**: Not started

### Tasks
- [ ] `EXT_Frederick_01.umap` created (World Partition enabled, empty terrain)
- [ ] Door trigger volumes on workshop exterior wall
- [ ] Transitions via `UGameplayStatics::OpenLevelBySoftObjectPtr` (soft reference)
- [ ] Fade-to-black before each transition; save fires before loading new map
- [ ] `AAshborneGameMode` handles gameplay map setup (spawn points, game rules)

**UE5.8**: `TSoftObjectPtr<UWorld>` for all map references. World Partition cell size 12800 (128m cells) on `EXT_*` maps.

**Done when**: Exit workshop door → exterior loads → re-enter → workshop reloads correctly.

---

## [ ] Phase 5: Interaction System

**Goal**: Maddox can examine objects and trigger context actions.
**Status**: Not started

### Tasks
- [ ] `IInteractable` interface: `Interact(AAshbornePlayerController*)`, `GetInteractionLabel() → FText`
- [ ] Sphere overlap on `AAshbornePlayerController` to find nearby interactables
- [ ] Closest interactable gets on-screen prompt (diegetic: phone notification style, CommonUI widget)
- [ ] `IA_Interact` input action fires `Interact()` on closest valid target
- [ ] First real interactable: workshop workbench

**UE5.8**: Use `UGameplayMessageSubsystem::BroadcastMessage` to notify UI of new interactable — avoids direct coupling between controller and HUD widget.

**Done when**: Approach workbench → prompt appears → E pressed → detail view opens.

---

## [ ] Phase 6: Dialogue System

**Goal**: NPCs speak to Maddox with branching dialogue options.
**Status**: Not started

### Tasks
- [ ] `UDialogueComponent` on NPC actors
- [ ] Dialogue trees stored as `UPrimaryDataAsset` subclass (`DA_Dialogue_*`)
- [ ] Dialogue state tracked via **Gameplay Tags** in `UDialogueSubsystem` (not booleans)
- [ ] UI: diegetic phone SMS-style overlay (`UCommonActivatableWidget`)
- [ ] First NPC dialogue: Sal Mercer in workshop

**Done when**: Talk to Sal → dialogue plays → select choice → Gameplay Tag updates.

---

## [ ] Phase 7: Inventory System

**Goal**: Maddox picks up, holds, and inspects items.
**Status**: Not started

### Tasks
- [ ] Item data: `DA_Item_*` (`UPrimaryDataAsset` subclass) — name, description, tier, `TSoftObjectPtr<UTexture2D>` icon
- [ ] `UInventorySubsystem` (world-scoped): add/remove/query items
- [ ] Diegetic inventory: `WBP_Phone` screen as item list and detail view
- [ ] Pick up via `IInteractable` → broadcasts `Ashborne.Event.ItemPickedUp` via `UGameplayMessageSubsystem`
- [ ] Inspect: push detail widget to phone UI layer

**Done when**: Pick up lock picks → see in phone inventory → inspect shows description.

---

## [ ] Phase 8: Crafting System

**Goal**: Maddox crafts gear at the workshop.
**Status**: Not started

### Tasks
- [ ] Recipe data: `DA_Recipe_*` (`UPrimaryDataAsset`) — required component tags, output item, unlock tag
- [ ] `UCraftingSubsystem`: recipe unlock on **Gameplay Tag**, not recipe item
- [ ] 3D printer abstraction: queued items available on next workshop visit (no simulation of print time)
- [ ] Workshop terminal interactable opens `WBP_CraftingUI` (CommonUI widget)

**Done when**: Have components → interact terminal → Tier 1 item appears in inventory on next workshop visit.

---

## [ ] Phase 9: Dexter Companion AI

**Goal**: Dexter follows Maddox, responds to commands, reacts to phenomenon.
**Status**: Not started

### Tasks
- [ ] `ADexterCharacter` with behavior tree (`BT_Dexter`) + blackboard
- [ ] Autonomous follow using Navigation Mesh (path already baked in Phase 2)
- [ ] Commands dispatch via `UGameplayMessageSubsystem` (no direct controller calls)
- [ ] Phenomenon intensity read from blackboard; alert behavior triggers at intensity > 0.3
- [ ] Equipment socket for sensor vest attachment

**Done when**: Dexter follows Maddox, sit command works, alerts near a phenomenon zone.

---

## [ ] Phase 10: Phenomenon System

**Goal**: Ashborne environmental presence escalates and disrupts electronics.
**Status**: Not started

### Tasks
- [ ] `UPhenomenonSubsystem` (game instance scope): global intensity float (0.0–1.0)
- [ ] Intensity updated via story triggers; broadcasts `Ashborne.Event.IntensityChanged`
- [ ] High-intensity zones: Lumen lighting shift, audio distortion (MetaSound parameter), UI glitch material
- [ ] `APhenomenonZone` actor: local intensity multiplier placed in levels
- [ ] Dexter behavior tree reads intensity from blackboard (updated by subsystem)

**Done when**: Set intensity to 0.8 → enter zone → lights flicker, phone UI glitches, Dexter alerts.

---

## [ ] Phase 11: Investigation Tools

**Goal**: Each gear item functions as a gameplay system.
**Status**: Not started

Implement one tool per sub-phase (11a, 11b, etc.):

### 11a: RF Analyzer
- [ ] Signal map overlay (post-process material + `APhenomenonZone` radius visualization)

### 11b: Thermal Imager
- [ ] Heat vision (post-process material + specialized camera mode)

### 11c: Lock Pick Kit
- [ ] Interaction minigame or simplified `IInteractable` unlock mechanic

### 11d: Fiber Optic Scope
- [ ] Secondary camera view (render target texture on screen mesh)

### 11e: Network Intrusion Kit
- [ ] Terminal minigame (CommonUI widget with hacking puzzle)

### 11f: Null Field Generator
- [ ] Suppresses `UPhenomenonSubsystem` intensity in a local radius

### 11g: Tier 3 Occult-Tech
- [ ] Ashborne Compass, Sealing Transmitter, Faraday Shell (gameplay mechanics per `crafting_and_gear.md`)

---

## [ ] Phase 12: Act 1 Content

**Goal**: Full Act 1 playable end-to-end per `act1/full_story.md`.
**Status**: Not started

### Tasks
- [ ] All 14 scenes from prose narrative implemented
- [ ] All NPCs with full dialogue trees
- [ ] All locations (interior, exterior, tunnels) accessible via map transitions
- [ ] Cipher fragments collectable throughout Act 1; decryption puzzle functional
- [ ] Act 1 ending triggers (`Ashborne.Act.Act1.Complete` Gameplay Tag)

---

## [ ] Phase 13: Audio & Visual Polish

**Goal**: Atmosphere is complete.
**Status**: Not started

### Tasks
- [ ] MetaSound graphs for all ambient tracks, music, and SFX
- [ ] Full Lumen/Nanite configuration, film grain, vignette post-process effects
- [ ] Niagara particle systems: cold breath, phenomenon wisps, Ashborne manifestation
- [ ] Character and NPC animation sets
- [ ] CommonUI widget animation polish (fade-in, transitions, hover effects)

---

## [ ] Phase 14: QA, Testing & Shipping

**Goal**: Releasable Linux build.
**Status**: Not started

### Tasks
- [ ] Automation test coverage for all subsystems (naming: `Ashborne.<System>.<TestName>`)
- [ ] Performance profiling (Unreal Insights)
- [ ] Linux Shipping build via CI pipeline
- [ ] GitHub Release artifact upload (`.tar.gz`)

---

## Implementation Rules (AI)

**Mandatory**:
- **One phase at a time.** Never start Phase N+1 until Phase N has a passing smoke test.
- **Subsystems, not singletons.** All game systems live in `UGameInstanceSubsystem` or `UWorldSubsystem`.
- **Gameplay Tags for state.** No `bool` flags for dialogue, story gates, gear unlocks — use `FGameplayTag`.
- **CommonUI for all interactive UI.** Always `UCommonActivatableWidget`, never plain `UUserWidget`.
- **Soft references for assets.** No hard pointers in data assets — use `TSoftObjectPtr`, loaded on demand.
- **Async save/load.** `USaveSubsystem` wraps async operations; never block game thread.
- **No gold-plating per phase.** Placeholder mesh, audio, animation — all fine. Ship the phase.
- **Names are permanent.** Use class/map names from `ue5_project_bootstrap.md`. Renaming C++ in UE5 is painful.

---

## Checkpoint Summary

| Phase | Deliverable | Testable Outcome |
|-------|-------------|------------------|
| 0 | Project structure | Editor opens |
| 1 | Main menu | New Game loads test level |
| 2 | Movement | Maddox walks, camera correct |
| 3 | Save/Load | Position persists |
| 4 | Map transitions | Multiple maps load cleanly |
| 5 | Interaction | Can examine workbench |
| 6 | Dialogue | Can talk to Sal, flags update |
| 7 | Inventory | Can pick up items, inspect |
| 8 | Crafting | Can craft Tier 1 gear |
| 9 | Dexter AI | Dexter follows, responds to commands |
| 10 | Phenomenon | Intensity affects world state |
| 11 | Tools | RF Analyzer, Thermal Imager, etc. functional |
| 12 | Act 1 | Story playable end-to-end |
| 13 | Polish | Atmosphere complete |
| 14 | Release | Linux build shipped |
