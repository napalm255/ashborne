# Dexter: Gameplay Mechanics
## Companion System & Supernatural Detection

---

## Overview

Dexter functions as Maddox's autonomous companion and primary supernatural detection system. Unlike traditional pet mechanics, Dexter is not an equipment slot or resource bar — he is a presence with his own agency, behavior, and reliability as a tool.

**Core principle**: Dexter's behavior is the player's most trustworthy instrument when electronic systems are failing.

---

## Behavior Tree System

Dexter operates via a behavior tree with four primary modes:

### Mode 1: Companion (Default)
- Follows Maddox at short distance (approximately 100 UE units behind)
- Responds to player movement, jumping/vaulting with Maddox
- Baseline alert state: ears forward, posture relaxed, occasionally sniffs environment
- Transitions to other modes based on environmental triggers and player commands

### Mode 2: Alert
- Something detected — unusual scent, temperature variance, phenomenon presence
- Visual cues: ears sharpen, posture stiffens, body turns toward stimulus
- Audio cue: subtle growl or alert bark (situational)
- Player prompt: "Dexter has detected something" flag added to case files
- Can be followed by Search command (mode shift) or dismissed (return to Companion)

### Mode 3: Fixation
- Dexter locks attention on specific location or object
- Refuses to move until player intervenes
- Visual cue: stiff posture, ears locked forward, nose pointing at target
- Common triggers: hidden doors (Dexter hears movement behind), concealed items, phenomenon concentration zones
- Player can approach and interact with the fixated object, or issue Stand Down command

### Mode 4: Refusal
- Hard block — Dexter will not enter an area
- Sits down at zone boundary, body language signals fear/warning
- Visual cue: ears back, posture low, whine/distress vocalization
- Triggers: active supernatural hazard, hostile NPC with weapon drawn, extreme environmental danger
- Requires player preparation (Tier 3 gear, NPC talk-down, environmental change) to override
- When override succeeds, Dexter enters zone reluctantly but reliably

---

## Player Commands

Activated via radial menu (Q key) or hotkeys. Dexter responds within ~0.5 seconds.

### Search
- Dexter leaves Maddox's immediate area and surveys surroundings
- Systematic sweep (radius adjusts by location — ~30 units indoors, ~100 units outdoors)
- Returns and alerts if anything anomalous is found
- Used to: locate hidden objects, confirm zone safety, find scent trails

**Input**: Q → Search (or hotkey S)
**Cooldown**: 10 seconds (Dexter needs recovery time between intense searches)
**Range**: Adjusts by environment (constrained indoors, wider outdoors)

### Guard
- Dexter holds position and monitors surroundings
- Will alert and posture-warn if threat approaches (NPC, animal, phenomenon spike)
- Useful for: securing a location during investigation, warning of NPC arrival, monitoring phenomenon intensity
- Dexter remains in Guard mode until Stand Down is issued or player moves >200 units away

**Input**: Q → Guard (or hotkey G)
**Duration**: Indefinite (until Stand Down or player distance-breaks)
**Alert radius**: ~150 units

### Track
- Dexter follows a scent trail to its source
- Unlocked in Act II (once player has encountered enough scent-based puzzles)
- Maddox must indicate starting point; Dexter follows scent from there
- Useful for: locating NPCs, following creatures, finding hidden paths

**Input**: Q → Track (requires proximity to scent source)
**Cooldown**: 30 seconds
**Distance**: Trail fades if older than ~2 hours in-game time
**Success rate**: 100% if trail is current, unreliable if aged

### Stand Down
- Dexter disengages from Alert/Guard/Track modes, returns to Companion mode
- Useful for: diplomatic situations (approaching friendly NPCs), ending Guard duty, resetting behavior

**Input**: Q → Stand Down (or hotkey D)
**Cooldown**: None (immediate)

---

## Behavioral Signals (Passive Information)

Even without commands, Dexter's baseline behavior communicates information:

| Behavior | Meaning | Action |
|---|---|---|
| Sniffing floor, nose working | Hidden object or recent passage below | Investigate floor, use Search command |
| Sitting, staring at wall | Hollow space, hidden door, or inscription behind | Move closer, examine wall, use RF analyzer |
| Ears back, moving slowly | Caution; something wrong but not immediate threat | Move carefully, increase alertness |
| Pressing against Maddox's leg | Maddox in danger he hasn't recognized | Reassess surroundings, watch for threats |
| Sitting calmly in tense space | Space is safe; trust the assessment | Relax, continue investigation |
| Hackles raised, stationary | Immediate threat nearby (NPC or supernatural) | Combat ready or flee |
| Tail between legs, whining | Fear; retreat recommended | Leave zone or prepare for major hazard |

---

## The Phoenix Patch: Phenomenon Immunity

Dexter's white chest patch carries special properties tied to the Ashborne mythology.

**In-game effect**: 
- Dexter is immune to disruption effects that disable other electronic systems
- When Maddox's RF analyzer is failing, Dexter's senses remain reliable
- In maximum-phenomenon zones (Act III), Dexter's white patch glows faintly (emissive material driven by phenomenon intensity float)
- The glow serves as a subtle light source when other lights fail

**Narrative implication**: 
- The patch is the same marking as a dog in an 1923 Ironveil photograph
- Whether this is coincidence, reincarnation, or Ashborne-specific immunity is left deliberately ambiguous
- It matters mechanically; narrative explanation is optional

**Implementation**: 
- Boolean flag on Dexter's character: `bPhenomenonImmune = true`
- RF analyzer and equipment disruption checks exclude Dexter from penalty logic
- Patch material parameter driven by global phenomenon intensity float
- At intensity >0.7, patch emissive kicks in

---

## Three Spontaneous Contributions

Three unscripted events where Dexter brings Maddox a component from nowhere.

**Mechanics**:
- Trigger volume in specific locations + correct story phase
- When Maddox enters volume, Dexter leaves, returns with component
- Component automatically added to inventory
- No player interaction required; happens autonomously

**Locations & Components**:
1. **Late Act I** (Southern warehouse near waterfront): Maddox needs an RF amplifier. Dexter returns with it after a Search.
2. **Mid Act II** (Libertytown farmstead): Maddox needs a resonant material component. Dexter brings it (source unexplained).
3. **Late Act II** (Middletown bell tower): Maddox needs a copper winding. Dexter produces it (source unexplained).

**Narrative note**: The game never explains these contributions. Maddox doesn't question them. The player is left to theorize: Did Dexter find them? Did Dexter manifest them from the Ashborne's influence? Is Dexter smarter than Maddox realizes?

---

## Sensor Vest (T2-09 Gear Item)

When equipped, Dexter wears a modified tactical vest with integrated sensors. The vest provides Maddox real-time environmental data:

- **Temperature sensor**: Confirms cold zones before Maddox enters
- **EM field sensor**: Detects Ashborne activity (correlates with RF analyzer)
- **Air quality sensor**: Flags toxic/unusual atmospheres
- **Ultrasonic sensor**: Detects sub-audible sounds (Ashborne communication pattern, audible only through this sensor)

**Mechanics**:
- Vest equipped from inventory (Dexter puts it on autonomously when selected)
- Real-time HUD overlay shows sensor feeds from Dexter's perspective
- Ranges limited to ~150 feet line-of-sight
- In high-phenomenon zones, ultrasonic sensor picks up signature pattern (becomes plot element)

**Gameplay purpose**: Extends Maddox's sensory range using Dexter as mobile sensor platform.

---

## Relationship to Wren's Dogs

Scout and Finn (Wren Calloway's dogs) interact with Dexter:

**Scout (Belgian Malinois mix)**:
- Work-drive recognition — Scout understands Dexter is working, not playing
- Professional respect between them
- Both alert on same phenomenon zones independently (provides dual confirmation to player)
- Occasionally coordinate Search sweeps (Scout covers range, Dexter covers detail)

**Finn (Golden Retriever)**:
- Gentle, patient approach
- Dexter and Finn settle near each other in safe zones (visual comfort signal)
- In high-phenomenon areas, Finn's continued calmness contrasts with Scout/Dexter alertness (narrative clue: Fin perceives Ashborne differently)

**Gameplay impact**: When both Dexter and Scout refuse to enter a zone, it's an absolute hard block. When both are calm, it's a green light. Mixed signals require player judgment.

---

## Dexter's Limitations

Dexter is powerful but not omniscient:

- Cannot bypass locked doors (mechanical or electronic)
- Cannot solve puzzles requiring fine manipulation
- Cannot access elevated areas (tall shelves, upper floors)
- Search mode has cooldown (requires ~10 second recovery between searches)
- In extreme phenomenon zones (Act III maximum), Dexter's alerts become delayed by 2–3 seconds (effect of supernatural interference)
- Cannot directly attack hostiles (loyalty to Maddox means he won't leave Maddox's side to pursue)

These limitations keep Dexter as complement to Maddox, not replacement.

---

## AI Implementation Details

**Behavior tree structure** (pseudocode):
```
Root: DexterBehaviorTree
├── Check Mode (Enum: Companion, Alert, Fixation, Refusal)
├── If Companion:
│   ├── Follow Maddox (pathfinding)
│   ├── Monitor Environment (phenomenon intensity, NPC proximity)
│   └── Update Audio (vocalizations based on environmental state)
├── If Alert:
│   ├── Face Stimulus
│   └── Play Alert Animation/Audio
├── If Fixation:
│   ├── Lock Position
│   └── Play Fixation Animation (stare, sniff)
├── If Refusal:
│   ├── Sit at Boundary
│   └── Play Distress Animation/Audio
└── Damage/Health:
    └── If Health < 0: Dexter Dies (story trigger)
```

**Pathfinding**: Uses standard UE AI navigation mesh. Dexter respects same obstacles as Maddox.

**Animation states**: 
- Idle (relaxed vs. alert vs. focused)
- Walk (normal speed following Maddox)
- Run (when player sprints or danger is imminent)
- Sit/Lie (in Guard mode, rest states)
- Alert animations (ears up, hackles raise, stiff posture)
- Vocalization (tied to audio subsystem)

**Perception**: 
- Sight: forward-facing cone, 200+ unit range
- Smell: omnidirectional, triggered by scent volumes and specific actors
- Hearing: responds to loud sounds, NPC dialogue, supernatural audio events

---

## Notes on Player Relationship

The Dexter system rewards treating him as a genuine teammate rather than a tool:

- Resting at Maddox's apartment (where Dexter sleeps) provides comfort state bonus to Maddox's morale/investigation focus
- Talking to Dexter (can be done any time) provides narrative reinforcement and subtle hints about next steps
- Equipping the sensor vest or giving commands makes Dexter feel like a partner in the investigation, not a pet to be ordered around

The game design philosophy is that Dexter should feel like the most important relationship in Maddox's life — which he is.

