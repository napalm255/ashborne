# Ashborne — Crafting & Gear System
### Design Document

---

## Overview

Maddox Grey is not a soldier. He's a guy who understands systems — how they work, how they fail, and how to make them do things they weren't designed to do. The crafting system reflects this. There are no magic forges or enchanting tables. Maddox finds parts, understands what they can do, and builds something useful at his workbench. Later, when the world stops making sense, he figures out how to make his gear work in that world too.

**Core loop:** Explore → Find components → Return to workbench → Build → Deploy.

Crafting is never the obstacle. The obstacle is finding what you need and knowing what to build.

---

## Crafting Locations

**Primary:** Maddox's Workshop (INT-01, Room 1B) — full access to all recipes and build tiers. Houses two printers: an FDM printer (Bambu Lab X1C) for structural parts, enclosures, mounts, and mechanical components, and a resin printer (Elegoo Saturn) for fine-detail work — precision housings, small gears, optical mounts, and reproduced period hardware. Both printers run off a dedicated print server Maddox manages from his workstation. Print jobs queue automatically when a recipe calls for printed parts; the fabrication time is abstracted (parts are ready on next visit or after a rest).

**Secondary:** Mercer's Auto & Cycle (INT-04) — full access. Sal's tools supplement Maddox's for certain builds. Sal also has a consumer FDM printer in the back office he uses for fabricating obsolete automotive brackets — lower resolution than Maddox's, but functional for Tier 1 structural parts in a pinch.

**Field:** Maddox's go-bag contains a compact kit for Tier 1 field repairs and simple Tier 2 assembly. Tier 3 items cannot be built or modified in the field — they require the workbench and printers.

---

## Component Categories

All craftable items are built from components. Components are found through exploration, purchased from vendors, or salvaged from the environment.

### Common Components
Found throughout all zones. Respawn on a cycle at vendor locations.
- **Wire** (copper, insulated, coaxial)
- **Fasteners** (screws, bolts, cable ties, adhesives)
- **Power cells** (AA/AAA, 9V, lithium coin, rechargeable packs)
- **Basic electronics** (resistors, capacitors, LEDs, switches, breadboard sections)
- **Enclosures** (plastic project boxes, metal tins, repurposed casings)
- **Hand tools** (consumed on specific builds — picks, pry tools, driver bits)
- **Filament stock** (PLA, PETG, TPU spools — stocked at workshop, purchasable online or at Sal's)
- **Resin stock** (standard and engineering-grade resin cartridges — stocked at workshop, purchasable online)

### Uncommon Components
Found in specific locations or purchased from specialty vendors. Do not respawn freely.
- **Microcontrollers** (Arduino-type, Raspberry Pi-type, custom ICs)
- **RF components** (antennas, amplifiers, filters, SDR modules)
- **Optical components** (lenses, IR sensors, laser diodes, fiber strands)
- **Mechanical components** (motors, servos, solenoids, springs, gears — some sourced, some printed)
- **Chemical components** (solvents, adhesives, compounds, resin post-processing chemicals — sourced from Sal's shop or hardware stores)
- **Signal components** (oscillators, signal generators, frequency modules)
- **Specialty filament** (carbon fiber-reinforced, metal-fill, flexible TPU for specific structural needs — ordered online)

### Rare Components
Found in specific story locations or acquired through NPC relationships. Non-respawning.
- **Custom ICs** — Maddox's own fabricated chips. Built at the workbench from common + uncommon components. Required for advanced Tier 2 and all Tier 3 items.
- **Salvaged mil-spec hardware** — Found at Monocacy battlefield, Historical Society sub-basement. Hardened, precise, irreplaceable.
- **Period materials** — Iron, copper, and glass components with specific provenance. Sourced from Vivienne, the farmstead, Ironveil locations. Required for Tier 3 hybrid items.
- **Printed period reproductions** — High-fidelity resin prints of Ironveil hardware components, cast from scanned originals. Maddox scans period artifacts (with Vivienne's permission, or without it) and prints structural reproductions that can be combined with authentic materials when originals are unavailable. The resin printer's resolution is high enough that the geometric specifications hold — it's the material provenance of the metal and resonant components that matters, not the housing.
- **Resonant materials** — Materials that have been in proximity to the Ashborne long enough to carry a detectable charge. Identified with the RF analyzer. Found late Act II and Act III. Required for the most powerful Tier 3 items.

---

## Gear Tiers

---

### TIER 1 — Mundane Gear
**Description:** Practical, real-world tools. No special properties beyond their function. Maddox could buy most of these at a hardware store, but his versions are purpose-built and better.

**Build location:** Workshop or field kit.
**Components:** Common only (some Tier 1 items use one uncommon component).
**Durability:** Persistent. Mundane gear doesn't degrade. It's just stuff.

---

#### T1-01 | Slim Jim Set
**Function:** Mechanical bypass tool for standard pin tumbler locks.
**Built from:** 2x flat spring steel strips, 1x handle wrap (paracord)
**Carried:** Go-bag slot. Always available once built.
**Use:** Opens standard residential and commercial locks without damage. Leaves no electronic trace. Slower than Maddox's electronic bypass tools but works when power is cut.
**Dexter note:** Dexter has watched Maddox use this enough times that he sits and waits with the specific patience of a dog who knows exactly how long this takes.

---

#### T1-02 | Pry Bar (Modified)
**Function:** Structural access — forcing panels, lifting hatches, moving obstructions.
**Built from:** 1x steel bar stock (salvaged or purchased), 1x grip wrap
**Carried:** Motorcycle saddlebag. Not a go-bag item — too large.
**Use:** Physical force solution for stuck or sealed access points. Some locations require this before electronic tools are relevant.

---

#### T1-03 | Fiber Optic Scope
**Function:** Visual access under doors, through vents, into tight spaces.
**Built from:** 1x fiber optic bundle, 1x LED tip, 1x flexible housing (printed — resin, semi-rigid), 1x eyepiece or phone adapter (printed mount)
**Carried:** Go-bag slot.
**Use:** Pre-entry reconnaissance. Reveals room state, occupants, hazard conditions before Maddox commits to entry. Can also be sent down narrow shafts — pairs with the Libertytown farmstead shaft when Dexter isn't available or as a supplement. The printed housing is form-fitted to the fiber bundle — tighter tolerance than anything off the shelf.

---

#### T1-04 | Faraday Pouch (Set of 3)
**Function:** Signal isolation for sensitive components or confiscated electronics.
**Built from:** 3x metallic fabric pouches, conductive thread, 3x zipper closures
**Carried:** Go-bag slots (all 3).
**Use:** Stores electronics that might be remotely wiped or tracked. Also used to transport resonant components without interference. Essential before the Ashborne begins actively disrupting equipment.

---

#### T1-05 | Bolt Cutters (Compact)
**Function:** Cuts padlocks, chains, wire fencing.
**Built from:** Purchased base (Sal's shop or hardware store) + custom grip extensions for compact carry
**Carried:** Motorcycle saddlebag.
**Use:** Brute-force access solution. Less elegant than lock picks, faster than mechanical bypass. Some locations are padlocked specifically because electronic access is unavailable.

---

#### T1-06 | Field Notebook + Rubbing Kit
**Function:** Document capture and analysis.
**Built from:** Blank notebook (purchased), graphite pencils, tracing paper, magnifier card
**Carried:** Go-bag slot. Always present from game start.
**Use:** The notebook auto-populates as Maddox documents clues. The rubbing kit is a manual tool for capturing impressed writing, surface inscriptions, and coin/seal details. Used at the Harmon House study desk and several other locations. Low-tech beats high-tech when power is out.

---

#### T1-07 | Dexter's Camera Harness
**Function:** Mounts a small camera to Dexter's chest for remote visual feed.
**Built from:** 1x nylon harness (modified from a dog harness), 1x compact camera module, 1x wireless transmitter, 1x printed camera mount (FDM, rigid — fitted to Dexter's chest geometry after Maddox spent an unreasonable amount of time measuring a dog who would not stay still), power cell
**Carried:** Motorcycle saddlebag (Dexter wears it on command).
**Use:** Sends Dexter into spaces too small or too dangerous for Maddox. Feed displays on Maddox's phone or tablet. Used at the Libertytown farmstead shaft. Range limited to ~150ft. Dexter cooperates fully; he has done stranger things.

---

### TIER 2 — Tech Gear
**Description:** Maddox's real toolkit. Custom-built electronic devices that leverage his expertise in RF, signals, network intrusion, and surveillance. These are the tools that make him specifically dangerous rather than just capable.

**Build location:** Workshop primary. Some can be assembled at Mercer's.
**Components:** Common + uncommon. Some require custom ICs (fabricated first).
**Durability:** Persistent. Tier 2 gear does not degrade, but some items can be temporarily disrupted by the Ashborne's influence in high-phenomenon areas. Disruption is environmental, not permanent damage.

---

#### T2-01 | RF Signal Analyzer
**Function:** Detects, records, and analyzes radio frequency signals across a wide spectrum. Identifies anomalous signals including the Ashborne's network signature.
**Built from:** 1x SDR module, 1x wideband antenna, 1x microcontroller, 1x printed enclosure (resin — shielded interior cavity, precision-fit component trays), power cell, 1x custom IC (signal processing)
**Carried:** Go-bag slot. Core tool — built in Act I, carried for entire game.
**Use:** The primary investigation tool. Detects the anomalous partition signal, maps its geographic intensity, identifies RF anomalies at the Monocacy battlefield, and — late game — detects resonant materials. Displays as a waveform overlay on Maddox's phone screen in-game. The resin enclosure is cast with embedded copper shielding — printed in two halves with a copper tape layer between them before bonding.
**Phenomenon behavior:** In high-phenomenon areas, the analyzer picks up signals that don't correspond to any known transmission format. These signals, when recorded and analyzed at the workbench, contain lore fragments and cipher components.

---

#### T2-02 | Network Intrusion Kit
**Function:** Physical and wireless network penetration. Clones access credentials, injects bypass packets, extracts data from secured systems.
**Built from:** 1x compact single-board computer, 1x multi-protocol wireless module, 1x cable breakout board, custom firmware (Maddox's own), 1x enclosure
**Carried:** Go-bag slot.
**Use:** Electronic lock bypass, network terminal access, security camera manipulation, data extraction. Used at City Hall, the warehouse, and several intermediate locations. Maddox's bread and butter — he's used versions of this for years.
**Upgrade path:** Mid-game, Maddox can add a custom IC that extends wireless range and adds a passive monitoring mode. Passive mode flags network anomalies automatically while Maddox explores.

---

#### T2-03 | Electronic Lock Bypass Tool
**Function:** Interfaces with electronic access control panels to extract or spoof credentials.
**Built from:** 1x microcontroller, 1x RFID read/write module, 1x contact probe set, 1x enclosure, power cell
**Carried:** Go-bag slot.
**Use:** Opens RFID-keyed doors, card readers, keypad locks with network backends. Faster than the network intrusion kit for standalone locks but doesn't provide network access beyond the immediate lock. Used extensively from Act I onward.
**Limitation:** Purely electronic — does not work on mechanical locks or locks that have been disconnected from power. This is why the Slim Jim Set matters.

---

#### T2-04 | Surveillance Tap
**Function:** Passively intercepts and records camera feeds, audio monitoring systems, and network traffic from a planted position.
**Built from:** 1x wireless transmitter, 1x compact processor, 1x camera/audio tap interface, 1x magnetic mount, power cell
**Carried:** Go-bag (2 units). Additional units craftable.
**Use:** Plant on a camera housing or network junction to intercept feeds remotely. Maddox can review tap footage from his workstation. Range approximately 300ft to receiver (phone or laptop). Used for pre-entry recon on guarded locations and for monitoring locations after departure.
**Dexter note:** Maddox has on three occasions asked Dexter to carry a tap to a location and deposit it. Dexter did this correctly all three times. Maddox has not fully processed what this implies about Dexter's intelligence.

---

#### T2-05 | Ground Penetrating Scanner
**Function:** Detects voids, density variations, and anomalous materials below floor and within wall surfaces.
**Built from:** 1x GPR sensor array (salvaged or sourced from Sal's contacts), 1x signal processor, 1x display interface, 1x enclosure, power cell, 1x custom IC
**Carried:** Motorcycle saddlebag. Too large for go-bag.
**Use:** Reveals hidden spaces — the void beneath the Colt & Compass cellar, the sealed chamber in the Middletown undercroft, tunnel networks. Also detects the convex stress fractures in flooring before they become visible. Becomes critical mid-Act II.
**Phenomenon behavior:** In high-phenomenon areas, the scanner picks up density readings that don't correspond to any known material. These readings cluster around the Ashborne's historical intrusion points.

---

#### T2-06 | Signal Jammer (Directional)
**Function:** Disrupts electronic communications and triggers within a directed cone, approximately 30ft range.
**Built from:** 1x RF transmitter (high power), 1x directional antenna array, 1x frequency controller, 1x enclosure, power cell (large)
**Carried:** Go-bag slot (compact form factor, antenna folds).
**Use:** Disables wireless security systems, prevents remote-triggered devices from activating, and — late game — disrupts the Ashborne's ability to interface with networked systems within range. Has a power draw that limits continuous use to approximately 8 minutes per charge.
**Important:** The jammer affects Maddox's own equipment within its cone. Requires tactical deployment — point away from self.

---

#### T2-07 | Thermal Imaging Monocular
**Function:** Detects heat signatures through moderate obstructions (thin walls, smoke, darkness).
**Built from:** 1x thermal sensor array, 1x optical assembly, 1x display processor, 1x printed housing (resin — monocular form factor, ergonomic grip, eyecup), power cell
**Carried:** Go-bag slot.
**Use:** Identifies occupants through walls before entry, detects warm/cold anomalies in investigation locations, and locates the South Mountain tunnel entrance from the Middletown bell tower. Cold signatures (the Ashborne's influence) are visible as deep blue voids in the thermal display — inverted from normal heat signatures. The printed housing is one of Maddox's cleaner builds — it looks almost commercial. Sal asked where he bought it. Maddox said he made it. Sal did not believe him until he saw the print lines.
**Phenomenon behavior:** In high-phenomenon areas, the thermal imager shows cold voids that are orders of magnitude colder than possible. The Ashborne's direct manifestation, when it occurs, appears as an absolute-zero black in the display.

---

#### T2-08 | EMP Device (Compact)
**Function:** Delivers a localized electromagnetic pulse, disabling unshielded electronics within approximately 15ft.
**Built from:** 1x capacitor bank (large), 1x pulse coil, 1x trigger circuit, 1x enclosure (heavy), power cell (high-capacity)
**Carried:** Go-bag slot. Single-use per charge — recharges at workbench.
**Use:** Emergency electronic disable. Kills security systems, disables hostile electronic devices, and — late game — temporarily disrupts the Ashborne's ability to manifest through networked hardware. Affects Maddox's own equipment equally; must be shielded or powered down before use.
**Sal's note:** Sal has seen this device once. He looked at it for a long time and then said "I don't want to know" and went back to work. This is one of the reasons Maddox considers him an excellent friend.

---

#### T2-09 | Dexter's Sensor Vest
**Function:** Equips Dexter with environmental sensors that feed data to Maddox's phone — air quality, temperature, electromagnetic field, audio above and below human hearing range.
**Built from:** 1x modified tactical dog vest, 4x sensor modules (temp, EM, air quality, ultrasonic), 4x printed sensor mounts (FDM, PETG — flush-mounted to vest panels, curved to match vest contour), 1x compact transmitter, power cell (vest-integrated)
**Carried:** Motorcycle saddlebag (Dexter wears on command).
**Use:** Extends Maddox's sensor range using Dexter as a mobile platform. Temperature data confirms cold zones before Maddox enters. EM data detects Ashborne activity. The ultrasonic sensor picks up sounds Dexter reacts to that Maddox can't hear — late game, these sounds are identified as the Ashborne's sub-audible communication pattern. The printed mounts are low-profile enough that the vest moves naturally with Dexter.
**Dexter's reaction:** Dexter tolerates the vest with the dignity of a dog who knows the vest is important, even if it is indignity. He does not tolerate adjustments to the fit.

---

### TIER 3 — Occult-Tech Hybrid Gear
**Description:** Items that should not work. Maddox builds them anyway because the evidence demands it. These are devices that combine his electronic expertise with materials and principles from the Ironveil's documented work — copper and iron with specific provenance, resonant materials charged by proximity to the Ashborne, and geometric configurations that Maddox refuses to call what they are (circuits, he says. They're just circuits arranged in an unusual pattern).

Tier 3 items are the endgame toolkit. They are the only things that reliably function in maximum-phenomenon environments and the only things capable of directly affecting the Ashborne.

**Build location:** Workshop only. Workbench requires a specific modification (iron junction plate, sourced Act II) to handle resonant materials safely.
**Components:** Common + uncommon + rare (period materials and resonant materials both required).
**Availability:** Recipes are discovered — through Vivienne's archive, the Ironveil documents, Reverend Tillman's knowledge, and Maddox's own synthesis of everything he's learned.
**Durability:** Persistent. Tier 3 items are not affected by the Ashborne's electronic disruption — the resonant materials provide a form of interference immunity that Maddox can measure but not fully explain.

---

#### T3-01 | The Null Field Generator
**Function:** Projects a localized field that suppresses Ashborne phenomenon within approximately 20ft radius. Electronics function normally within the field. Cold zones warm slightly. Dexter relaxes.
**Built from:** 1x RF signal generator (modified), 1x copper coil wound to Ironveil geometric specification (wound on a printed resin former — the geometry is precise enough that Maddox printed the former from a digitized version of the Ironveil schematic rather than try to hand-form it), 3x period iron components (sourced from Vivienne), 2x resonant materials, 1x custom IC, power cell (high-capacity)
**Carried:** Deployed — sets up as a stationary device. Not carried active. Pack and carry between locations.
**Use:** Establishes a safe operating zone in high-phenomenon interiors. Required for extended work in the City Hall server room (Act III) and the warehouse main floor. Battery life approximately 45 minutes per charge. Recharges at workshop.
**Maddox's note (field notebook):** *"I've run the numbers four times. The suppression effect is real and measurable. The coil geometry is doing something the signal alone can't explain. I've stopped trying to explain it and started calling it a feature."*

---

#### T3-02 | The Ashborne Compass
**Function:** Detects and directionally locates concentrations of Ashborne influence. Functions as a supernatural GPS for the entity's presence and for Ironveil sealing sites.
**Built from:** 1x brass compass housing (period, sourced from Vivienne's front display case), 1x custom magnetometer, 1x resonant material (primary), 1x copper winding (Ironveil specification), 1x microcontroller (minimal)
**Carried:** Go-bag slot. Passive — always active once built.
**Use:** The compass needle points toward the nearest significant Ashborne concentration rather than magnetic north. Displays intensity via a secondary indicator Maddox adds — a simple LED array scaled to proximity. Used to locate hidden intrusion points, track the Keeper's movements (the Keeper carries a resonant artifact), and navigate the tunnel network beneath Frederick.
**Note:** The brass compass from Vivienne's display case — the one that reacted to Maddox's RF equipment in Act II — is the required housing. Vivienne gives it to him when the time is right. She's been saving it.

---

#### T3-03 | The Sealing Transmitter
**Function:** Broadcasts the Ironveil's sealing cipher as a modulated RF signal, reinforcing or reactivating the sealing network around the Ashborne's containment points.
**Built from:** 1x high-power RF transmitter, 1x custom antenna (wound to Ironveil specification from period copper, on a printed resin former), 2x resonant materials, 1x period iron housing (authentic — sourced from Ironveil locations; a printed reproduction was attempted but the resonant calibration failed, confirming that material provenance matters for Tier 3 in ways that can be measured), 1x microcontroller loaded with the complete cipher sequence (assembled from all discovered cipher components), power cell (high-capacity)
**Carried:** Motorcycle saddlebag. Large. Heavy for its size.
**Use:** The primary tool of the Act III resolution. Deployed at each of the Ashborne's sealing points to rebroadcast the cipher and close the breach the Keeper has created. Requires the complete cipher — built from components gathered across the entire game. Missing any component means the transmitter broadcasts an incomplete sequence. Incomplete is worse than nothing.
**Assembly requirement:** The cipher must be complete before the transmitter can be built. The final cipher component is in the Harmon House attic (the rafter inscription). The transmitter cannot be assembled until that component is documented.
**Maddox's note:** *"This is a radio that closes a door that has been open since 1864. I built it at my workbench next to my coffee maker. I'm choosing not to think about that too hard."*

---

#### T3-04 | The Faraday Shell (Wearable)
**Function:** Personal protection against the Ashborne's direct electronic intrusion — the entity's ability to disrupt Maddox's equipment and, in late Act III, to affect Maddox directly through his own devices.
**Built from:** 1x modified tactical vest (base from Sal's contacts), copper mesh lining (Ironveil specification), 4x resonant materials (distributed across vest panels), period iron clasps (sourced), 1x grounding circuit (active, powered by integrated cell)
**Carried:** Worn. Equippable from inventory. Replaces standard jacket for final act.
**Use:** Passive protection — worn, not deployed. Prevents the Ashborne from using Maddox's own devices against him in the warehouse confrontation. Without it, the Ashborne can turn Maddox's electronics into hazards. With it, his gear functions normally in maximum-phenomenon conditions.
**Dexter note:** Dexter sniffs the vest thoroughly when Maddox first puts it on and then appears to approve. This is noted in the field notebook with the observation: *"I have started using Dexter's reactions as a quality control benchmark. This seems reasonable."*

---

#### T3-05 | The Resonant Disruptor
**Function:** Direct-effect device against Ashborne manifestations. Delivers a modulated pulse combining the sealing cipher's frequency with resonant material amplification — the supernatural equivalent of a very targeted signal jammer.
**Built from:** 1x pulse coil (Ironveil geometric specification), 3x resonant materials, 1x period copper core, 1x custom IC (signal modulation), 1x trigger assembly, power cell
**Carried:** Go-bag slot. Single-use per charge. Recharges at workbench.
**Use:** The closest thing in the game to a direct weapon. Disrupts Ashborne manifestations, forces retreat from a location, and — at the warehouse — buys time during the final sequence. Does not destroy. Nothing in the game destroys the Ashborne. The goal is containment, not elimination. The disruptor supports that goal by keeping the entity from interfering while the Sealing Transmitter does its work.
**Build note:** Requires the Null Field Generator to be built first — the resonant calibration process uses the generator's output as a reference. Maddox figures this out himself, which he notes with the specific satisfaction of someone who enjoys elegant systems.

---

## Vendor & Acquisition Reference

| Component Type | Primary Source | Secondary Source |
|---|---|---|
| Common electronics | Maddox's workshop stock | Hardware stores (Frederick) |
| RF components | Online order (in-game delivery to workshop) | Gray-market contact (All Saints St.) |
| Microcontrollers | Online order | Historical Society gift shop (oddly) |
| Mechanical components | Sal's parts room | Printed at workshop (FDM) |
| Chemical components | Sal's shop | Hardware stores |
| Filament (PLA/PETG/TPU) | Workshop stock (restocked online) | Sal's shop (basic PLA only) |
| Resin (standard/engineering) | Workshop stock (restocked online) | N/A — specialty item |
| Specialty filament (CF, metal-fill) | Online order only | N/A |
| Custom ICs | Fabricated at workbench | N/A — Maddox only |
| Period materials | Vivienne Colt | Ironveil locations (non-respawning) |
| Printed period reproductions | Printed at workshop from scanned originals | N/A |
| Mil-spec salvage | Monocacy Battlefield | Historical Society sub-basement |
| Resonant materials | High-phenomenon interiors | The Keeper's warehouse (late game) |

---

## Crafting UI Notes

**Recipe discovery:** Recipes appear in Maddox's workstation interface when he has encountered the relevant need AND has enough component knowledge to conceive the build. Some recipes unlock through NPC dialogue (Vivienne describes a device; Maddox translates it into electronics). Some unlock through document research. None require a separate "recipe item" to be found — Maddox figures things out.

**Build interface:** Select recipe → component slots populate → confirm available components → build. No minigame. No failure state. Maddox either has what he needs or he doesn't.

**3D printing queue:** Recipes that include printed parts show a printer icon alongside standard component slots. If filament or resin stock is sufficient, the print job queues automatically on confirm. Printed parts are available on next workshop visit or after a rest event — the game abstracts print time rather than making the player wait in real time. The workstation displays an active print job indicator while parts are running. Maddox occasionally checks on prints mid-investigation via a workshop camera feed on his phone.

**Scanning artifacts:** Maddox can scan physical objects with his phone to generate print-ready models — used for reproducing Ironveil components, creating custom mounts for found hardware, and reverse-engineering period mechanisms. Scanning is a dedicated interaction in the relevant interior locations. Scanned models appear in the workshop's print library and can be scaled, mirrored, or combined before printing.

**Component scanner:** Maddox's phone has a component identification mode. Pointing it at found items identifies them and adds them to inventory. Unknown components (resonant materials, period items) show as "unidentified — analysis required" until brought to the workbench.

**Dexter's contribution:** On three occasions in the game, Dexter brings Maddox a component he needed and didn't know where to find. The game does not explain this. Maddox does not question it. He thanks Dexter and adds the component to inventory.
