# Ashborne: Gameplay Overview
## Engine, Perspective, and Design Principles

---

## Engine & Platform

**Engine**: Unreal Engine 5.8 (C++ + Blueprints)

**Target Platform**: Linux (Fedora/Bluefin Atomic Desktop) — development, testing, and shipping exclusively on Linux

**Other Platforms**: Out of scope for initial release. Architecture may support future porting but is not a design constraint.

---

## Viewpoint: Fixed Isometric Camera

The game uses a **fixed isometric camera** at approximately -50° pitch (looking down-and-forward into the scene). This is the Diablo/Path of Exile convention: the player sees Maddox in three-dimensional space from a consistent, fixed angle. The camera does not rotate; the player cannot change the viewpoint.

**Camera behavior:**
- Follows Maddox as he moves (slight lag for cinematic quality, spring arm follow)
- Spring arm distance: approximately 1500 UE units
- Pitch: -50 degrees (fixed)
- Yaw: locked at 0 (no rotation)
- Roll: 0 (always level)
- Post-process vignette: 0.5 intensity (frames the action, emphasizes focus)

**Cinematic moments:**
During story sequences, the camera can temporarily shift angle or pull back for dramatic emphasis (camera cuts in sequencer, not player-controlled).

---

## Art Direction: Gabriel Knight Atmosphere in 3D

**Aesthetic Goal**: The painted, atmospheric quality of Gabriel Knight (1993) translated into three-dimensional isometric space.

**Implementation in UE5.8:**
- **Lumen** (dynamic global illumination) provides realistic light bounce and atmospheric depth
- **Nanite** (virtualized geometry) allows rich architectural detail without runtime LOD cost — every brick, every stone, every weathered surface is visible and tactile
- **Post-process materials** push the image toward a painterly quality: warm amber tones for safe/domestic spaces, desaturated cool tones for phenomenon-active zones
- **Color grading per zone**: Each major location has a LUT that reinforces its emotional tone
- **Vignette + film grain**: Subtle edge darkening and grain texture enhance the painted aesthetic
- **Lighting design**: Drama over realism. Shadows are heavy. Highlights are warm. Atmosphere is thick.

**Reference aesthetic:**
- Gabriel Knight 1 hand-painted VGA backgrounds (color palette, composition density)
- Disco Elysium isometric lighting and atmosphere
- Planescape: Torment environmental density and visual weight
- Baldur's Gate 3 isometric camera and staging

Frederick's historic interiors should feel lived-in, aged, and heavy with history. The server rooms should feel cold and sterile. Phenomenon zones should feel wrong — colors off, light broken, space distorted.

---

## Movement & Interaction

**Movement**: Click-to-move (point-and-click) as primary control scheme, WASD as secondary.
- Click a location on the ground → pathfinding calculates route → Maddox walks there
- Controller support: Right stick to move, face buttons to interact
- Dexter follows automatically at a short distance, with his own behavior tree running in parallel

**Interaction Model**: Point-and-click object interaction.
- Interactable objects highlight at configurable proximity radius (~100 units)
- Click or press E to interact
- Contextual verb menus appear (Examine, Take, Use, Talk)
- No minigames; interaction is automatic or dialogue-gated

**Dexter as autonomous entity**:
- Dexter has his own pathfinding and behavior tree
- When Maddox commands him (Search, Guard, Track, Stand Down), his behavior tree updates
- Dexter can diverge from following (fixation on a wall, refusal to enter zone) — this creates visible gameplay signals
- Player learns to read Dexter's posture, ear position, and movement as mechanical feedback

---

## UI/UX Philosophy

**Diegetic first**: Interfaces are rendered in-world when possible.
- Workshop terminal: UMG widget rendered to a screen mesh in INT-01
- Phone/laptop: inventory and case files accessed through Maddox's devices
- Map: accessed via a phone app Maddox built
- Field notebook: physical object in the world, opens as a detailed texture display

**Hotkey-driven**: 
- I for inventory
- M for map/case files
- N for field notebook
- C for crafting (when at workbench)
- Q radial menu for Dexter commands

**No HUD clutter**: Health bars, ammo counters, and objective markers are absent. The game trusts the player to understand state through environment and dialogue.

---

## Tone & Pacing

**Tone**: Gritty, grounded, occasionally funny in the way that exhausted people are funny. Dry wit surfaces at the worst possible moments. Atmosphere is Gabriel Knight — literary, dense, occasionally unsettling.

**Pacing**: Investigation-first, action-rare.
- Acts I–II are exploration, puzzle-solving, and dialogue
- Action sequences (confrontations) are brief, high-stakes, and story-driven
- The game rewards slow, careful observation
- Rushing has consequences (Dexter's alerts go unheeded, clues are missed)

**Tension building**: Phenomenon intensity increases across the game. Act I is subtle (Dexter's reactions, equipment glitches). Act II is building (cold zones, audio anomalies). Act III is intense (direct Ashborne manifestation, world-state changes).

---

## UE5.8 Feature Integration

### Lumen (Real-Time Global Illumination)
Essential for dynamic lighting across phenomenon zones. As the Ashborne's influence intensifies, Lumen adapts: cold zones invert light values, phenomenon zones create visual distortion.

### Nanite (Virtualized Geometry)
Frederick's historic interiors are architecture-heavy. Nanite handles this without performance cost. The Best Farm cellar has precisely modeled stone walls. City Hall has detailed period fixtures. Every interior is richly detailed.

### World Partition (Spatial Streaming)
Each zone (Downtown Frederick, Monocacy Battlefield, Walkersville, etc.) is a World Partition cell. Fast travel manages cell loading. This prevents the open world from requiring simultaneous full load.

### MetaSounds (Procedural Audio)
The Ashborne's presence alters ambient audio. MetaSounds procedural graph handles this:
- Normal audio state: city ambience, interior hum
- Phenomenon audio state: sub-bass drone, signal interference, cold void acoustics
- Gradual transitions based on phenomenon intensity float

### Enhanced Input (Click-to-Move)
Point-and-click interaction uses UE's Enhanced Input System for flexible input mapping. Supports keyboard, mouse, gamepad, and touch (if ported to platforms supporting it).

### Chaos Physics (Environmental Hazards)
Libertytown farmstead ceiling can collapse. Heavy objects can be moved. Environmental storytelling through destruction and persistence.

---

## Crafting System (UE5.8 Implementation)

**Data-driven approach**: Recipes, components, and gear are Data Assets (UE native). Each item is a DA_GearItem subclass. Components are DA_ComponentItem. Recipes are DA_CraftingRecipe with required component arrays.

**Crafting Manager Subsystem**: Handles recipe discovery, component tracking, and printer queue management.

**3D Printer Integration**: 
- Bambu Lab X1C and Elegoo Saturn 4 Ultra are in-world objects (static meshes in the workshop)
- Print queue is managed by subsystem
- Fabrication time is abstracted (parts ready on next workshop visit)
- Visual feedback: printer status on Maddox's monitors, print indicator on UI

---

## Phenomenon System

**Phenomenon Intensity (0.0–1.0 float):**
Global value that escalates across the game. Environmental effects reference this value:
- Lighting shifts (blue-tinted shadows at high intensity)
- Audio shifts (MetaSounds procedural audio intensity)
- Dexter's baseline agitation (posture changes, vocalizations)
- Equipment disruption (RF analyzer static, monitors flicker)
- NPC behavior changes (speech patterns, movement uncertainty)

**Phase State**: Act 1, Act 2, Act 3 flag gates progression and unlocks. Phenomenon intensity and phase state together determine gameplay difficulty and narrative pacing.

**Cold Zones**: Specific locations with concentrated Ashborne presence. These zones:
- Disrupt electronic equipment (harder, faster degradation)
- Lower Dexter's confidence (he'll alert but may refuse entry without player override)
- Create visual distortion (inverted colors, light interference)
- Require protective measures (Null Field Generator in Act III) for extended exposure

---

## Death & Consequence

**No permadeath**: If Maddox is killed, the game reloads from the last save/rest point.

**Consequence through story**: Deaths have narrative weight. An NPC death cascades through dialogue and story beats. A failed investigation allows the Ashborne to progress unchecked (visible in world state and NPC reactions).

**Resets and save points**: 
- Saving happens automatically at workshop (home base) and at Sal's shop (secondary location)
- Rest (sleep/downtime) saves progress and advances day/night cycles
- No manual save (encourages commitment to choices)
- No quicksave/quickload (maintains tension)

---

## Accessibility

**Colorblind modes**: Post-process shader variations for deuteranopia, protanopia, tritanopia.

**Text scaling**: UI text size adjustable in settings (affects UMG widgets).

**Subtitle support**: All dialogue has subtitles (essential for story delivery).

**Input remapping**: Enhanced Input System allows complete rebinding of all controls.

**No timed sequences**: Investigation puzzles never require real-time precision. Confrontation sequences are player-paced (not action game reflexes required).

---

## Testing & Performance Targets

**Resolution & framerate**: 
- Target: 1440p at 60 FPS on mid-range hardware (RTX 3070, Ryzen 5 5600X equivalent)
- Minimum: 1080p at 30 FPS on lower-end hardware
- Ultra: 4K at 60 FPS on high-end hardware

**Memory targets**: 
- Loaded zone footprint: ~8–12 GB VRAM (accounting for Nanite/Lumen overhead)
- Total install size: ~80–150 GB (depends on audio/texture quality assets)

**Profiling**: Use UE Insights for frame time analysis. Stat unit for per-frame breakdown. Stat memory for allocation tracking.

