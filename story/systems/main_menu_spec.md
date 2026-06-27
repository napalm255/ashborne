# Main Menu Design Specification

## Style: Atmospheric + Animated

### Background

- **Live UE5 level rendered behind the UI** — not a video or static image
- **Scene**: Frederick, MD at night; aerial fixed isometric view (matching gameplay camera angle), moonlit, April atmosphere (bare trees, cool blue-grey tone)
- **Slow environmental animation**: light wind in trees, distant moving car headlights, one flickering streetlight
- **Ashborne bleed-in effects** (subtle, not obvious on first viewing):
  - Occasional cold-breath fog wisps drifting through the frame
  - Barely perceptible red-shift creeping in from one corner of the screen
  - The flickering streetlight is the Ashborne itself — dims and brightens slightly out of rhythm, as if breathing

### Menu Options (in order)

1. **New Game** — always enabled
2. **Continue** — greyed/disabled if no save file exists
3. **Settings** — opens settings submenu overlay
4. **Quit** — exits to operating system

### Settings Submenu

- **Display**: resolution, fullscreen/windowed toggle, vsync on/off
- **Audio**: master volume, music volume, SFX volume (all sliders 0–100)
- **Controls**: placeholder for future keyboard remapping (deferred to Act 1 development)
- **Back**: returns to main menu via CommonUI back stack

### Transitions

- **Launch → Menu**: fade from black over ~1.5 seconds (cinematic entrance)
- **New Game**: fade to black → `OpenLevelBySoftObjectPtr` to `Maps/INT_Workshop.umap` → fade in to gameplay
- **Continue**: fade to black → restore last saved map from `UAshborneGameInstance` → fade in
- **Quit**: immediate exit via `UKismetSystemLibrary::QuitGame`

### Audio

- **Ambient track**: quiet Frederick night ambience (distant traffic hum, wind through streets, distant siren)
- **Music bed**: sparse, unsettling underscore that plays beneath the ambient
- **Ashborne undertone**: low sub-bass rumble (~0.3 Hz, 30 Hz fundamental), barely perceptible — creates unease without conscious awareness
- **No music sting on menu open** — atmosphere is already playing when screen fades in

### UMG Widget Layout

```
[Full-screen background: live UE5 scene rendering INT_Workshop exterior or similar]

   ASHBORNE                           ← game title, top-left, atmospheric serif font (large)
   A Maddox Grey Mystery              ← subtitle, smaller, lighter weight

                        [ New Game  ]
                        [ Continue  ]   ← greyed if no save exists
                        [ Settings  ]
                        [ Quit      ]
```

**Button style**: right-aligned cluster, light text (off-white) on semi-transparent dark background panel. No visible button borders.
**Hover state**: text brightens to pure white + subtle audio tick (UI confirmation sound).
**Focus management**: handled automatically by CommonUI; do not manage widget focus manually.

---

## UE5.8 Implementation Details

### Widget Classes

- **`WBP_MainMenu`**: extends `UCommonActivatableWidget` (not plain `UUserWidget`)
  - Overrides `NativeOnActivated()` to call `UAshborneGameInstance::HasSaveData()` and disable/grey Continue button
  - Manages button bindings via CommonUI's focus system
  
- **`WBP_MenuButton`**: extends `UCommonButtonBase` (not plain `UButton`)
  - Inherits focus navigation and back-button handling
  - Can be reused for Settings overlay buttons as well

### Widget Stack Management

- **Settings overlay** is pushed onto the CommonUI layer stack via `UCommonUIExtensions::PushContentToLayer_ForPlayer`
- Back button automatically pops the overlay (CommonUI default behavior)
- No manual back-button handling code needed

### Game Mode

- **`AAshborneMenuGameMode`**: no pawn, no player character, no gameplay logic
- UI only; input consumed by CommonUI widget system exclusively
- Disables default pawn spawning in constructor

### Save Detection

- **`UAshborneGameInstance::HasSaveData()`**: returns `bool`
  - Checks if `"AshborneSave_Slot0"` exists via `UGameplayStatics::DoesSaveGameExist`
  - Called on `WBP_MainMenu::NativeOnActivated()` to set Continue button enabled state

### Asset References

- **`UI_MainMenu.umap`** is referenced via `TSoftObjectPtr<UWorld>` in `UAshborneGameInstance`
- Loaded via `UGameplayStatics::OpenLevelBySoftObjectPtr` with automatic unloading of previous map
- No hard references; deferred loading

### Required Plugins

- **CommonUI** (shipped with UE5.8)
- **Enhanced Input** (shipped with UE5.8)

Both are enabled in `AshborneProject.uproject`.

---

## Design Notes

- **Atmosphere first**: The menu should feel like stepping into the game world, not stepping out of it. The "bleed-in" effects should be deniable — did the light flicker or did I imagine it?
- **No loading screen separate from menu**: The menu itself IS a loading transition. New Game fades to black, loads, fades back in.
- **Diegetic feel**: Buttons are interactive, but the experience is grounded — no floating UI, no sci-fi chrome. Keep it analog and tactile.
- **Accessibility**: Settings should always be reachable without starting a new game. Continue should reflect actual save state.
