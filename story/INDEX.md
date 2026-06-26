# Ashborne: Design Documentation Index

**Master navigation for all story, character, and system design files.**

---

## Quick Navigation

### Start Here
- **[synopsis.md](acts/synopsis.md)** — Logline, three-act structure, themes, character overview

### World & Setting
- **[overview.md](world/overview.md)** — Frederick 2025, atmosphere, tone, themes
- **[history.md](world/history.md)** — Civil War backstory, Ironveil founding, sealing ritual
- **[locations_exterior.md](world/locations_exterior.md)** — Zones, fast travel, geography
- **[locations_interior.md](world/locations_interior.md)** — Interior maps, room-by-room design

### Characters
**Protagonist & Companions**:
- **[maddox_grey.md](characters/maddox_grey.md)** — Maddox profile, skills, 2025 toolkit
- **[wren_calloway.md](characters/wren_calloway.md)** — Love interest, historian, co-investigator
- **[dexter.md](characters/dexter.md)** — Companion dog, supernatural sensor, Phoenix patch
- **[scout_and_finn.md](characters/scout_and_finn.md)** — Wren's dogs, mechanics, investigation support

**NPCs**:
- **[npcs/nora_grey.md](characters/npcs/nora_grey.md)** — Sister, ER nurse, personal stakes
- **[npcs/sal_mercer.md](characters/npcs/sal_mercer.md)** — Best friend, mechanic, logistics
- **[npcs/vivienne_colt.md](characters/npcs/vivienne_colt.md)** — Antiquarian, Ironveil knowledge, archive access
- **[npcs/det_ray_okafor.md](characters/npcs/det_ray_okafor.md)** — Detective, institutional pressure, ally
- **[npcs/thomas_hale.md](characters/npcs/thomas_hale.md)** — IT director (deceased), inciting death, documentation
- **[npcs/the_keeper.md](characters/npcs/the_keeper.md)** — Antagonist (Act II reveal), seal dismantler

### Story & Narrative
**Act I**:
- **[act1/overview.md](acts/act1/overview.md)** — Story beats, mechanics, character arcs (Apr 7–19)
- **[act1/full_story.md](acts/act1/full_story.md)** — Complete prose narrative, 14 scenes
- **[act1/walkthrough.md](acts/act1/walkthrough.md)** — Player guide, puzzles, progression

**Act II & III**:
- **[act2/overview.md](acts/act2/overview.md)** — Story beats, key locations, themes (May–June)
- **[act3/overview.md](acts/act3/overview.md)** — Story beats, final confrontation (late June)

### Gameplay Systems
- **[gameplay_overview.md](systems/gameplay_overview.md)** — UE5.8, isometric camera, Gabriel Knight aesthetic
- **[dexter_mechanics.md](systems/dexter_mechanics.md)** — Companion AI, commands, sensor vest, spontaneous contributions
- **[crafting_and_gear.md](systems/crafting_and_gear.md)** — Crafting system, recipes, Tier 1–3 gear, components
- **[development_setup.md](systems/development_setup.md)** — UE5.8 environment, tools, quick-start checklist

---

## File Organization

```
story/
├── INDEX.md (this file)
├── world/
│   ├── overview.md
│   ├── history.md
│   ├── locations_exterior.md
│   └── locations_interior.md
├── characters/
│   ├── maddox_grey.md
│   ├── wren_calloway.md
│   ├── dexter.md
│   ├── scout_and_finn.md
│   └── npcs/
│       ├── nora_grey.md
│       ├── sal_mercer.md
│       ├── vivienne_colt.md
│       ├── det_ray_okafor.md
│       ├── thomas_hale.md
│       └── the_keeper.md
├── acts/
│   ├── synopsis.md
│   ├── act1/
│   │   ├── overview.md
│   │   ├── full_story.md
│   │   └── walkthrough.md
│   ├── act2/
│   │   └── overview.md
│   └── act3/
│       └── overview.md
└── systems/
    ├── gameplay_overview.md
    ├── dexter_mechanics.md
    ├── crafting_and_gear.md
    └── development_setup.md
```

---

## By Role

### For Designers
- World & setting: [overview.md](world/overview.md), [locations_exterior.md](world/locations_exterior.md), [locations_interior.md](world/locations_interior.md)
- Narrative: [synopsis.md](acts/synopsis.md), [act1/overview.md](acts/act1/overview.md), [act2/overview.md](acts/act2/overview.md), [act3/overview.md](acts/act3/overview.md)
- Gameplay: [gameplay_overview.md](systems/gameplay_overview.md), [crafting_and_gear.md](systems/crafting_and_gear.md)

### For Writers
- Characters: all in [characters/](characters/)
- Story beats: [act1/full_story.md](acts/act1/full_story.md), act 2/3 overviews
- Dialogue notes: see individual character files

### For Programmers
- Gameplay systems: [gameplay_overview.md](systems/gameplay_overview.md), [dexter_mechanics.md](systems/dexter_mechanics.md), [crafting_and_gear.md](systems/crafting_and_gear.md)
- Dev setup: [development_setup.md](systems/development_setup.md)
- Architecture: [gameplay_overview.md](systems/gameplay_overview.md) — UE5.8 features, data structures

### For QA/Testing
- Act 1 walkthrough: [act1/walkthrough.md](acts/act1/walkthrough.md) — progression, puzzles, collectibles
- All story files for context

---

## Key Concepts

**The Ashborne**: Entity sealed in Frederick's digital/physical infrastructure in 1864. Fed on Battle of Monocacy carnage. Seal is 161 years old and failing. Main antagonist force (not a single enemy, but an environmental hazard).

**The Ironveil**: Secret order formed 1864 to seal the Ashborne. Descendants still maintain knowledge. Includes soldiers, clergy, and telegraph operator Clara Marsh. Maps, documents, and ritual knowledge scattered across Frederick.

**The Keeper**: Human antagonist. Deliberately dismantling the seal to release the Ashborne. Believes it can be controlled. Identity revealed Act II.

**The Partition**: Anomalous encrypted section of Frederick's municipal network. Physical housing of the Ashborne's current manifestation. Signal is a self-replicating cipher.

**Phenomenon Intensity**: Global value (0.0–1.0) that escalates across game. Affects lighting, audio, equipment disruption, NPC behavior, Dexter's reactions.

---

## Design Philosophy

- **Investigation-first**: Exploration and puzzle-solving dominate. Action sequences are rare and story-driven.
- **Atmosphere over action**: Gabriel Knight (1993) aesthetic — literary, dense, occasionally unsettling.
- **Dexter as reliable tool**: When electronic systems fail (due to phenomenon), Dexter's senses and behavior are the player's most trustworthy instruments.
- **Tech and history collide**: Modern 2025 infrastructure contains ancient supernatural threat. The contrast drives the story.
- **No player death**: Reloading from last save; consequence is narrative, not mechanical.
- **Containment over victory**: The Ashborne cannot be destroyed. It must be held. The ending is maintenance, not triumph.

---

## Quick Reference: What Goes Where

| Type | Location | Example |
|------|----------|---------|
| Story beats | `acts/` | Act 1 overview, full story, walkthrough |
| Character profiles | `characters/` | Maddox, Wren, Dexter, all NPCs |
| World building | `world/` | Locations, zones, history, atmosphere |
| Gameplay systems | `systems/` | Crafting, Dexter AI, controls, UE5.8 setup |
| Three-act structure | `acts/synopsis.md` | Logline, arcs, themes |

---

**Last updated**: June 26, 2025
**Engine**: Unreal Engine 5.8
**Setting year**: April–June 2025
**Status**: Pre-production design complete; Act 1 detailed

