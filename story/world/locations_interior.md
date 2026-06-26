# Ashborne — Interior Zone Maps
### Room-by-Room Layout Design Document

---

## Design Principles

**Atmosphere first.** Every interior should feel like a place that existed before Maddox arrived and will exist after he leaves. Rooms have lived-in detail, environmental storytelling, and a sense that something is slightly wrong even before anything happens.

**Environmental hazards over combat.** Danger comes from unstable structures, compromised electrical systems, toxic atmospheres, occult phenomena, trapped mechanisms, and the occasional direct threat. When enemies appear, their presence is meaningful — not filler.

**Dexter as sensor.** In every interior, Dexter's behavior provides atmospheric cues. He sniffs specific objects, avoids specific corners, fixates on walls or floors where things are hidden. His reactions are gameplay signals, not decorative.

**Fixed layouts, randomized respawns.** Room geometry and key interactables are always in the same place. Enemy placement, loot containers, and ambient hazard intensity vary between visits.

**Lighting matters.** Every room has a default lighting state and a compromised lighting state. Power can be cut, bulbs can fail, and Maddox's equipment can be disrupted. Each room description notes natural light sources and artificial ones.

**Scale note:** All dimensions are approximate interior measurements (wall to wall). Ceiling heights noted where relevant.

---

---

# ZONE 1 — DOWNTOWN FREDERICK

---

## INT-01 | Maddox's Apartment & Workshop
**Building:** Second floor above Anchor Print Co., side street off Market Street
**Total Footprint:** ~1,400 sq ft across two connected spaces
**Access:** Private exterior staircase (rear alley) + locked interior door from print shop hallway

### Room 1A — Main Living Area
**Dimensions:** 28ft x 22ft | Ceiling: 10ft (exposed brick, original tin ceiling partially intact)
**Lighting:** Four south-facing windows (natural), two overhead industrial pendants, multiple monitor glow

The largest room. Open-plan with a kitchen alcove at the north end and a defined seating area at the south. The division between "living space" and "work space" is theoretical — a folding table near the east wall holds three monitors, a network rack, and a soldering station. Bookshelves line the west wall, heavy with technical manuals, regional history texts, and a notable absence of fiction.

**Key Interactables:**
- **Main workstation** — Inventory management, active case files, network access, crafting schematics. The hub interface.
- **Network rack** — Houses Maddox's custom server. Contains the original copy of the anomalous partition data. Can be queried for analysis tasks.
- **Bookshelf (east section)** — Three books are flagged as interactive: a dog-eared Frederick County history, a technical manual with handwritten margin notes, and one book spine that doesn't match any title (Ironveil-related, discovered Act II).
- **Dexter's bed** — 40"x52" orthopedic platform in the southeast corner. Dexter goes here when he's unsettled. If he refuses to leave it, the apartment has been compromised in some way.
- **Kitchen alcove** — Coffee maker always on. One cabinet contains a false back (discovered via Dexter investigation) holding a small emergency cache: burner phone, cash, USB drive.

**Hazard State:** None baseline. In Act III, the Ashborne can intrude through the network — monitors flicker, the rack throws errors, ambient temperature drops. Working at the station during intrusion events carries a sanity/disruption penalty.

---

### Room 1B — Workshop
**Dimensions:** 20ft x 18ft | Ceiling: 9ft
**Lighting:** One north-facing window (frosted), four overhead shop lights on a separate breaker, under-cabinet task lighting at the bench

Connected to the main living area through a wide doorway with a heavy curtain (no door — Maddox removed it). The workshop smells like solder flux and machine oil. Pegboard covers the east wall, tools organized with the specific deliberateness of someone who was messy once and learned from it. A heavy steel workbench runs the south wall.

**Key Interactables:**
- **Main workbench** — Device crafting station. Components combine here. Has a built-in vice, oscilloscope, and a drawered cabinet of components organized by type.
- **Parts cabinet (west wall)** — Randomized component loot between visits. Core crafting materials always stocked (wire, resistors, common ICs). Specialty components must be sourced.
- **Pegboard** — Tools have silhouettes painted behind them. Missing tools are immediately obvious — relevant when something has been taken.
- **Locked steel cabinet (floor, north wall)** — 36"x24". Contains Maddox's sensitive equipment: RF analyzer, signal jammer, a compact EMP device he built "for emergencies." Opens with a 6-digit code. Code changes if Maddox suspects the apartment has been accessed.
- **Scan printer/plotter** — Used to print physical maps, decoded documents, circuit diagrams. Physical output can be pinned to the corkboard in 1A.

**Hazard State:** None baseline. A gas line runs along the north wall — in a late-game scenario, this becomes relevant.

---

### Room 1C — Bedroom
**Dimensions:** 14ft x 12ft | Ceiling: 9ft
**Lighting:** One west-facing window, bedside lamp, no overhead

Spare. Bed, nightstand, a clothes rack that functions as a closet. The only room without screens. A framed photograph on the nightstand (Maddox and Dexter, somewhere outdoors — date and location visible if examined). Under the bed: a go-bag, always packed.

**Key Interactables:**
- **Go-bag** — Contains the starting inventory loadout. Can be restocked here. Examining it early game reveals Maddox has always been prepared for something, even if he didn't know what.
- **Nightstand drawer** — Field notebook. Physical record of clues, sketches, observations. Readable as in-game artifact. Updates as the story progresses.
- **Window** — Faces the alley. Can be used as an alternate exit. In Act II, Maddox notices the same car parked in the alley across three different nights. Interacting with the window flags this.

---

### Room 1D — Bathroom
**Dimensions:** 8ft x 7ft
**Lighting:** Overhead fluorescent (flickers slightly — always has, always will)

Functional. Nothing notable except the medicine cabinet mirror, which in Act III shows a reflection that is one second delayed. Maddox can choose to ignore it or investigate. Investigating it triggers a lore fragment.

---

## INT-02 | Frederick City Hall — IT Infrastructure Room
**Building:** Frederick City Hall, 101 N Court St. Basement level.
**Total Footprint:** ~2,100 sq ft across three areas
**Access:** Public entrance to main building. Basement requires keycard (story) or access panel bypass (skill).

### Room 2A — Main Lobby / Reception
**Dimensions:** 40ft x 30ft | Ceiling: 14ft (vaulted, historic)
**Lighting:** Large south-facing windows, overhead chandeliers (converted to LED), motion-sensor sconces in corridors

The public face of city government. Marble floors, bulletin boards, a security desk staffed during business hours. Maddox has legitimate access here during the contract. NPCs include a receptionist, a security guard (schedule varies on respawn), and rotating civilian foot traffic.

**Key Interactables:**
- **Security desk** — Guard has a schedule. Shift change at 8am, 4pm, midnight. Desk drawer contains a building map (obtainable via distraction or after-hours access).
- **Bulletin board** — Contains public notices. One notice, easily missed, references a "system maintenance window" that coincides exactly with Thomas Hale's time of death.
- **Elevator** — Access to floors 2-4 (administrative). Basement requires a separate keycard not on the elevator panel — there's a slot below the standard buttons, partially concealed.

---

### Room 2B — Server Room Anteroom
**Dimensions:** 18ft x 14ft | Ceiling: 8ft
**Lighting:** Overhead fluorescent, no windows

A staging area between the basement stairwell and the main server room. Houses an access panel, a monitoring terminal (locked), and a defibrillator mounted on the wall — which Maddox notes is an unusual placement for a server anteroom.

**Key Interactables:**
- **Access panel** — Bypass puzzle. Requires wire tools and electronics skill. Time-limited if security is active.
- **Monitoring terminal** — Shows server room environmental data (temperature, humidity, power draw). The power draw log has anomalies on specific dates going back 14 months. Downloadable.
- **Defibrillator cabinet** — Behind it, scratched into the drywall: a symbol Maddox doesn't recognize yet. Dexter sniffs the wall here and does not stop until Maddox photographs it.

---

### Room 2C — Main Server Room
**Dimensions:** 45ft x 35ft | Ceiling: 10ft (raised floor, cable management overhead)
**Lighting:** Overhead LED strips, indicator lights from racks, emergency lighting strips at floor level
**Temperature:** Maintained at 65°F — noticeably cold on entry

The heart of the city's digital infrastructure. Rows of server racks on a raised floor. The hum is constant and slightly too regular — Maddox notices it doesn't fluctuate the way active server noise should.

**Key Interactables:**
- **Rack Row C, Unit 7** — The anomalous partition's physical host. Visually unremarkable. When Maddox's RF analyzer is active nearby, it throws readings that shouldn't be possible for the hardware spec.
- **Cable junction (northeast corner, under raised floor)** — Access panel in the raised floor. Below it: standard cable routing, and one cable that doesn't connect to any rack on either end. It runs into the concrete wall. The wall is solid. The cable is active.
- **Environmental control panel** — The temperature in the southeast quadrant of the room is 4 degrees colder than the rest of the room. The panel shows no reason for this. Dexter will not enter the southeast quadrant.
- **Hale's workstation (southwest corner)** — Thomas Hale's personal station. Password protected. Crackable. Contains his hidden documentation — 14 months of anomaly logs, written in a personal shorthand Maddox has to decode.

**Hazard State:** In Act II, the room becomes hostile during off-hours visits. The cold quadrant expands. Electronic equipment fails intermittently. The cable in the wall transmits something audible only through Maddox's signal analyzer — a pattern that matches the Battle of Monocacy's date in Morse.

---

## INT-03 | Colt & Compass Antiquities
**Building:** Patrick Street, Frederick. Narrow three-story brick rowhouse, converted to retail.
**Total Footprint:** ~1,800 sq ft across four levels including cellar
**Access:** Public during business hours (Tue–Sat, 10am–6pm). After-hours requires Vivienne's key (obtainable Act I) or rear window entry (available but Vivienne will know).

### Room 3A — Main Shop Floor
**Dimensions:** 22ft x 38ft | Ceiling: 11ft
**Lighting:** Front display windows (south), pendant lights over display cases, multiple floor lamps creating overlapping warm pools

A controlled chaos of antiques. Display cases line the walls and create two irregular aisles through the center. The organization system is Vivienne's alone — she can locate any object in under 30 seconds. Maddox cannot find anything without asking or spending significant time searching.

**Key Interactables:**
- **Front display case** — Contains items related to Frederick County history. One piece — a tarnished brass compass — reacts to Maddox's RF equipment in Act II.
- **Civil War artifact shelf (east wall)** — Military items, documents, insignia. Two items on this shelf are Ironveil-adjacent. Vivienne will discuss them freely. She won't discuss where she acquired them.
- **The back corner** — A wingback chair, a side table, a reading lamp. This is Vivienne's chair. Sitting in it is not an option. Dexter has been invited to sit beside it exactly once, and accepted.
- **Sales counter** — Vivienne's domain. Transaction interface, dialogue hub, and where she decides whether to show Maddox the back rooms.

---

### Room 3B — Storage and Sorting Room
**Dimensions:** 16ft x 14ft | Ceiling: 9ft
**Lighting:** One overhead fluorescent, one work lamp on a gooseneck
**Access:** Through a curtained doorway behind the counter. Requires Vivienne's permission or Act II story unlock.

Boxes, bubble wrap, a worktable, shelves of items awaiting cataloging. Less curated than the shop floor — things here are transitional, between states. Several items here will be relevant to Maddox before Vivienne has cataloged them, which creates a puzzle about accessing them without her knowing.

**Key Interactables:**
- **Uncataloged box (northeast shelf, third from top)** — Contains a document folio acquired at estate sale. Inside: letters referencing the Ironveil by a different name — "the Sutured Order." First instance of this alternate name.
- **Worktable** — Vivienne's cataloging notes. Her handwriting is precise. Her personal observations in the margins are sharp. She has suspected something was wrong in Frederick for years.
- **Locked flat file cabinet** — Four drawers, map/document size. The lock is good. Contains Vivienne's private acquisition records — who sold what, and when. The pattern of sellers is significant.

---

### Room 3C — Private Archive
**Dimensions:** 18ft x 12ft | Ceiling: 9ft (low, oppressive feeling)
**Lighting:** No windows. Wall-mounted sconces, one standing lamp. Dim by design.
**Access:** Locked door at rear of storage room. Vivienne's key only until story unlock.

The archive proper. Shelving on all four walls, floor to ceiling, accessible by a rolling library ladder on a track. Materials organized by era, then geography. The Frederick County section takes up the entire north wall. A reading table in the center has a magnifying lamp and white cotton gloves laid out — Vivienne's standing rule.

**Key Interactables:**
- **Frederick County section, 1860–1870 shelf** — The core research resource for Acts I and II. Multiple lore documents, period maps, and a sealed envelope that predates standard envelope adhesive — it's been sealed with wax bearing the Ironveil symbol.
- **The sealed envelope** — Cannot be opened without consequences. Opening it triggers a sequence. Not opening it is also a choice with consequences. Vivienne knows it's there. She has never opened it.
- **Hidden shelf section (behind the ladder, north wall)** — A section of shelving that doesn't align with the track. Pulling the ladder reveals a narrow gap and three items that are not cataloged and not supposed to be here: a field journal, a hand-drawn map of Frederick's underground, and a glass vial of something dark.
- **Reading table** — Where Maddox decodes documents. Functions as an in-world puzzle interface for cipher and document work.

---

### Room 3D — Cellar
**Dimensions:** 20ft x 16ft | Ceiling: 7ft (stone, original building foundation)
**Lighting:** One bare bulb on a pull chain. No windows. Damp.
**Access:** Cellar door in storage room floor. Vivienne does not go down here. She did once. She doesn't discuss it.

Stone walls, packed earth floor in sections, original brick in others. Shelves of overflow stock from before Vivienne stopped using this space. The air is ten degrees colder than upstairs and smells wrong in a way that isn't mold or water damage.

**Key Interactables:**
- **Northeast corner** — The earth floor here is slightly raised compared to the rest — a subtle convexity. Dexter will not approach it. Ground-penetrating analysis (mid-game tool) reveals a void below.
- **Old shelving unit (west wall)** — Shoved against the wall at an angle that doesn't match the room geometry. Moving it reveals a filled-in doorway. The fill is newer than the surrounding stone by about 80 years.
- **The bare bulb** — When pulled, it stays on. When the Ashborne's influence is strong, it swings without air movement. This is the first place in the game where this happens.

**Hazard State:** In Act II and beyond, the cellar has active occult phenomenon. The cold is extreme. The convex earth section shows stress fractures between visits. By Act III, something is pushing up from below.

---

## INT-04 | Mercer's Auto & Cycle
**Building:** South end of downtown Frederick. Converted commercial garage, single-story with mezzanine office.
**Total Footprint:** ~3,200 sq ft
**Access:** Always available to Maddox. Sal gives him a key in Act I.

### Room 4A — Main Garage Bay
**Dimensions:** 60ft x 40ft | Ceiling: 16ft (overhead door clearance)
**Lighting:** Skylights (north-facing, diffuse), four overhead shop light arrays, portable work lights

Two vehicle bays. Hydraulic lift on the left bay, floor jack setup on the right. Tool chests line the south wall. The smell is oil, metal, and coffee. Maddox's motorcycle has a dedicated corner of the right bay.

**Key Interactables:**
- **Maddox's motorcycle corner** — Upgrade and modification station for the bike and Dexter's sidecar. Maddox can install equipment here that affects travel or combat capability.
- **Main tool chest (south wall, center)** — Sal's primary tools. Borrowing without asking is technically fine but tracked — Sal notices. Contains specialty tools Maddox needs for specific device builds.
- **Parts washer (northeast corner)** — Industrial solvent basin. In Act II, Sal uses it to clean an artifact Maddox brings in. The solvent reacts badly. This is a clue.
- **Overhead hoist** — Functional 2-ton chain hoist on a beam track. Relevant in one specific late-game scenario involving moving something heavy Maddox shouldn't be able to move alone.
- **Vehicle being worked on** — Randomized between visits. Occasionally the vehicle belongs to an NPC with information. Sal may or may not mention this.

---

### Room 4B — Parts Room
**Dimensions:** 24ft x 18ft | Ceiling: 10ft
**Lighting:** Two overhead fluorescents, one always flickering (Sal has replaced it four times; it always starts flickering again within a week)

Shelving units packed with parts, organized by a system only Sal fully understands. Boxes are labeled in his handwriting, which is readable if you know him, cryptic if you don't.

**Key Interactables:**
- **Specialty parts shelf (back wall)** — Randomized loot for crafting. Higher-grade components than what Maddox stocks at home.
- **The flickering light** — By Act II, it flickers in a pattern. The pattern is not random. Sal hasn't noticed. Maddox has.
- **Hidden lockbox (top shelf, behind surplus filters)** — Sal's emergency supplies. He hasn't told Maddox it's there. Dexter finds it. Contains: cash, a handgun (Sal's, legally registered), and a photograph of Sal much younger in a uniform Maddox doesn't immediately recognize.

---

### Room 4C — Mezzanine Office
**Dimensions:** 18ft x 14ft | Ceiling: 8ft | Overlooks garage bay via window
**Lighting:** One window (south-facing, overlooking alley), overhead fluorescent, desk lamp

Sal's office, which functions primarily as a place to eat, do paperwork he hates, and occasionally sleep. Desk covered in invoices. A couch against the east wall has a pillow and blanket that are always slightly rumpled. A small TV on a wall mount is always on, volume low, usually news.

**Key Interactables:**
- **Desk** — Invoices, client records. One client name appears in Act II that matches a name from the Ironveil documents. Sal doesn't know who they are — they call in, pay cash on pickup, never come in person.
- **TV** — Background news provides ambient world-state information. In Act II, a news segment about "unusual animal behavior in Frederick County" runs on loop. Sal keeps changing the channel. It comes back.
- **Couch** — Maddox has slept here. The game acknowledges this without comment. Save point available here as an alternative to the apartment.

---

## INT-05 | Frederick County Historical Society
**Building:** West Patrick Street, Frederick. Three-story historic structure.
**Total Footprint:** ~4,800 sq ft across public and restricted areas
**Access:** Public hours (Mon–Sat, 9am–5pm). Restricted archive requires library card or archivist rapport.

### Room 5A — Public Reading Room
**Dimensions:** 50ft x 35ft | Ceiling: 14ft (coffered, original plaster)
**Lighting:** Four tall windows (south and west), overhead pendant array, individual reading lamps at tables

The public face of the institution. Long reading tables, reference shelves, a card catalog that has been digitized but the physical version remains because the archivist doesn't trust the software. Quiet. The kind of quiet that has weight to it.

**Key Interactables:**
- **Reference shelves (east wall)** — Frederick County histories, genealogical records, city directories going back to the 1800s. City directories for 1863–1866 have been checked out repeatedly by the same library card number. That number is no longer active.
- **Card catalog** — Physical version contains cross-references the digital system doesn't. One card, filed under "Monocacy — Anomalous Reports," has been partially torn. The remaining half lists four document call numbers.
- **Archivist's desk** — Margaret Howell, 61, has been here 28 years. Her rapport meter determines access to restricted areas. She responds to genuine historical curiosity, Frederick County knowledge, and anyone who treats the materials with respect. She does not respond to impatience.
- **The photograph wall** — Rotating exhibit of historical Frederick photographs. One photograph — dated July 11, 1864, two days after the battle — shows a group of soldiers in front of a Frederick building. Three of them have the same symbol on their coat lapels. It's small. Maddox has to use his phone camera to zoom in.

---

### Room 5B — Restricted Archive — Main Room
**Dimensions:** 30ft x 25ft | Ceiling: 10ft
**Lighting:** Controlled UV-filtered overhead lighting, individual archival lamps at work surfaces
**Access:** With Margaret's permission or after acquiring researcher credentials.

Climate-controlled. The air here is drier and stiller than the rest of the building. Flat files, archival boxes, map drawers. Everything is labeled in pencil on acid-free tags. The Civil War collection takes up an entire wall of labeled boxes.

**Key Interactables:**
- **Civil War collection, Box 34** — Contains Monocacy battlefield after-action reports, soldier correspondence, and one document filed under a nondescript label that is actually a partial Ironveil membership record. 14 names. 11 are legible.
- **Map drawer 7** — Period maps of Frederick, 1860–1870. One map has annotations in a different hand than the cartographer — additions showing tunnel routes beneath the historic district that don't appear on any other map.
- **Anomalous reports file** — The four documents from the torn card catalog card. Three are accounts of what soldiers reported seeing at Monocacy. The fourth is a report filed by a Frederick physician in August 1864 describing patients presenting with identical symptoms: cold to the touch, unresponsive to light, speaking in a language he couldn't identify. He saw seven patients. None of them survived.

---

### Room 5C — Sub-Basement Storage
**Dimensions:** 28ft x 22ft | Ceiling: 7ft (stone, below grade)
**Lighting:** Single overhead fluorescent on a pull-switch. No windows.
**Access:** Sub-basement door in restricted archive, behind a shelving unit. Margaret mentions it exists. She says it's just overflow storage. She doesn't volunteer the key.

The Historical Society was built on an older foundation. The sub-basement is original — stone walls, earthen floor in the center section, brick in the periphery. Overflow storage consists of uncataloged materials deemed too fragile or too significant to process with current resources.

**Key Interactables:**
- **Uncataloged crate (northwest corner)** — Stenciled "MONOCACY — DO NOT CATALOG — per Board directive 1987." Inside: a collection of personal effects recovered from the battlefield in the 1980s during a drainage project. The Board directive is signed by a name that matches one of the Ironveil descendants in Walkersville.
- **The earth section (center floor)** — The brickwork stops and the floor is bare earth for approximately a 10ft x 10ft section. The earth is cold. Dexter refuses to stand on it. Pressing an ear to the ground (Maddox's action, prompted by Dexter's reaction) produces a faint rhythmic sound.
- **Wall inscription (south wall, behind shelving)** — Partially visible behind a steel shelf unit. Moving the unit (requires strength item or Maddox's ingenuity) reveals a full inscription in Latin and in a second language that is neither Latin nor English. The Latin portion translates to: *"Here it passed through. Here we close the wound."*

**Hazard State:** Sub-basement becomes actively dangerous in Act II. The cold intensifies. The rhythmic sound becomes audible without pressing an ear down. The earth section develops the same convex stress fractures as the Colt & Compass cellar.

---

---

# ZONE 2 — MONOCACY NATIONAL BATTLEFIELD

---

## INT-06 | The Best Farm — Farmhouse
**Building:** Historic farmhouse on battlefield grounds. Two stories, original construction 1820s, modified 1850s.
**Total Footprint:** ~1,600 sq ft above grade, cellar below
**Access:** Ground floor is public exhibit (staffed during park hours). Upper floor is restricted. Cellar is not on any public map.

### Room 6A — Ground Floor Public Exhibit
**Dimensions:** 32ft x 28ft (open plan, period room dividers) | Ceiling: 9ft
**Lighting:** Period windows (low natural light), supplemented by exhibit lighting on dimmers

Restored to approximate 1864 condition. Interpretive panels, reproduction furniture, a few original artifacts behind glass. A park ranger cycles through every 90 minutes during hours. After hours, motion sensors (bypassable) and a single camera (also bypassable) are the only monitoring.

**Key Interactables:**
- **Original fireplace (north wall)** — Massive stone hearth, 6ft wide. The firebox has a back panel that is not original stonework — it's been filled in. The fill matches the material in the Colt & Compass cellar doorway.
- **Exhibit case (east wall)** — Contains recovered artifacts from the farmhouse during the battle. One item — a small tin box — is listed in the exhibit manifest but is not in the case. The manifest is interactive; the discrepancy is flagged if Maddox examines both.
- **Floorboards near back door** — Three boards in the southeast quadrant sound different when walked on. They are different — they're a hatch cover, disguised flush with the floor and painted to match. The latch mechanism is inside the firebox.

---

### Room 6B — Cellar
**Dimensions:** 24ft x 20ft | Ceiling: 6.5ft (original stone, very low)
**Lighting:** None original. Maddox's equipment only. No windows.
**Access:** Hatch from ground floor, triggered by firebox latch. Not on any public or staff map.

The cellar predates the farmhouse. The stonework is different — older, and the construction method doesn't match the region's period style. Someone built this specifically. The air is extremely cold regardless of season. The walls have markings — not graffiti, not damage. Deliberate.

**Key Interactables:**
- **Wall markings (all four walls)** — A continuous inscription running around the room at shoulder height. Not linear text — a repeating symbolic sequence. Photographed and analyzed, it matches the cipher embedded in Frederick's network. This is the physical origin point.
- **Stone plinth (center)** — A roughly hewn stone block, approximately 3ft x 2ft x 2ft, that serves no structural purpose. The top surface has a depression — hand-shaped, deliberate. Placing a specific artifact here (obtained in Act II) is part of the sealing ritual.
- **The northeast corner** — The coldest point in the room, several degrees below the rest. Even Maddox's breath doesn't fog here — the temperature is past that threshold. Dexter stands at the corner of the room and points his nose toward this spot, ears flat, not making a sound.
- **Ironveil marker (under plinth)** — Moving the plinth (requires equipment) reveals an etched plate. The plate is a list: names, dates, and a role designation for each. It is the founding document of the Ironveil. Two of the names are also on the photograph at the Historical Society.

**Hazard State:** The cellar is the most supernaturally active interior in the game from first visit. Equipment fails intermittently. Prolonged exposure causes Maddox's on-screen displays to distort. Dexter is the only reliable instrument — his reactions are consistent when everything else is failing.

---

---

# ZONE 3 — WALKERSVILLE

---

## INT-07 | The Harmon House
**Building:** Residential, east side of Walkersville. Two-story Victorian, 1880s construction.
**Total Footprint:** ~2,200 sq ft plus attic
**Access:** Front door requires Edna's invitation (rapport-gated) or alternate entry. Edna is present during daytime hours.

### Room 7A — Front Parlor
**Dimensions:** 18ft x 16ft | Ceiling: 10ft
**Lighting:** Two front windows (east-facing), overhead chandelier (dim), two floor lamps

Edna Harmon's formal receiving room, which is to say the room where she decides whether she trusts you. Furniture from at least three different decades. Photographs on every surface. A side table with a very good tea service that is not ornamental.

**Key Interactables:**
- **Photograph groupings** — Three generations of Harmon family photographs. Faces, names, dates. Cross-referencing with Ironveil member names (known from prior research) connects at least two Harmon ancestors directly.
- **The secretary desk (east wall)** — Closed. Edna's desk. Never open when she's present. Contains correspondence and a small locked box. If trust is established, she may open the desk. If not, it requires after-hours access.
- **Edna herself** — Primary NPC for this interior. Her dialogue tree is long, layered, and trust-gated. She will discuss family history freely. She will discuss the Ironveil only when she has decided Maddox isn't going to get someone killed. This may take more than one visit.

---

### Room 7B — Kitchen
**Dimensions:** 16ft x 14ft | Ceiling: 9ft
**Lighting:** Window over sink (west-facing), overhead fluorescent (new, incongruous), under-cabinet lighting

Functional, slightly dated. Edna cooks. The kitchen smells like it. A door at the back leads to a small mudroom and rear yard.

**Key Interactables:**
- **Mudroom door** — The path to the rear yard, which has a cellar entrance that Edna doesn't use anymore. She notices if Maddox looks at this door.
- **Refrigerator (side panel)** — A handwritten note stuck there, faded. A list of names and phone numbers. Three of the names are Ironveil descendants from the Historical Society documents.
- **Rear window** — View of the backyard and cellar entrance. Casing option if Maddox needs to plan an after-hours approach.

---

### Room 7C — Upstairs Hallway & Bedrooms
**Dimensions:** Hallway 24ft x 5ft | Two bedrooms (one locked)
**Lighting:** Hallway: one overhead fixture. Bedrooms: standard residential.

The open bedroom is a guest room, unused but maintained. The locked bedroom was her late husband's study and has not been opened in eleven years. Edna's key is on her person. A duplicate key is in the secretary desk.

**Key Interactables:**
- **Locked study** — The goal. Inside: floor-to-ceiling bookshelves, a heavy oak desk, and a safe set into the wall behind a painting. The painting is of Monocacy. The safe contains Harmon family Ironveil materials — the most complete single collection outside of the archive Maddox hasn't found yet.
- **Safe** — Combination unknown. Three clues scattered across the house resolve the combination. Alternatively, Maddox can crack it with sufficient electronics skill and time.
- **Desk in study** — Even before the safe is opened, the desk surface has a leather blotter with impressions from letters written on top of it. Rubbing with a pencil (low-tech, effective) reveals a partial address in Libertytown.

---

### Room 7D — Attic
**Dimensions:** 30ft x 22ft (usable) | Ceiling: 6ft at peak, slopes to 3ft at eaves
**Lighting:** Two small gable windows (dim), Maddox's equipment only in corners
**Access:** Pull-down stair in hallway ceiling.

The attic is the end goal of the Walkersville visit. Edna hasn't been up here in years. She knows something is up here. She hasn't said what.

**Key Interactables:**
- **Steamer trunk (center, under peak)** — Locked with a padlock. Key is in the study safe. Contains Ironveil ceremonial items: a ledger, a ritual kit wrapped in oilcloth, and a hand-drawn map of the tunnel system beneath Frederick — more complete than the annotated map at the Historical Society.
- **The rafter inscription** — On the underside of the roof peak, visible only with a light source and looking up: the same symbolic sequence from the Best Farm cellar, written in what appears to be charcoal. This one has an addition at the end — a sequence that doesn't appear anywhere else. It's the final component of the sealing cipher.
- **Box of photographs (near east gable)** — Family photographs that were never displayed. Several show Ironveil gatherings — members in partial ceremonial dress, at locations Maddox can identify from other research. Dates range from 1890 to 1962. The last photograph in the box is dated 1962 and shows a gathering of twelve people. Someone has drawn an X through eleven of the faces. The twelfth is unmarked.

---

---

# ZONE 4 — LIBERTYTOWN

---

## INT-08 | St. Paul's Lutheran Church
**Building:** Active rural church, original structure 1850s with 1920s additions.
**Total Footprint:** ~2,800 sq ft including sanctuary, fellowship hall, and attached rectory
**Access:** Sanctuary open during daylight. Rectory requires pastor's invitation.

### Room 8A — Sanctuary
**Dimensions:** 45ft x 30ft | Ceiling: 22ft (vaulted wood)
**Lighting:** Stained glass windows (east and west), overhead pendant array (dim), candle sconces

A genuinely beautiful space. Old wood, worn pews, afternoon light through colored glass. The pastor, Reverend Carl Weiss, is usually present during the day — third-generation Libertytown, seventh-generation Frederick County. He knows why Maddox is here. He's been half-expecting this visit for twenty years.

**Key Interactables:**
- **The altar** — Standard Lutheran appointment, but the altar cloth has an embroidered border that incorporates the Ironveil symbol as a repeating motif. It's been there for 80 years. Weiss knows what it means. He inherited the church, the cloth, and the knowledge together.
- **Pew 7, left side** — A specific pew that is worn differently than the others — the kneeler is worn to bare wood while the others retain padding. Someone has knelt here, repeatedly, for a very long time. Under the kneeler, carved into the wooden rail: coordinates. Not GPS — a reference system used in 19th-century survey notation. They resolve to a location in Frederick's underground.
- **The south window** — One pane of the stained glass, third from the left in the south array, depicts a scene that doesn't match the biblical narrative of the adjacent panes. It shows a river, a figure kneeling, and a structure being sealed. The figure's coat has the Ironveil symbol. Weiss will explain the window if trust is established.

---

### Room 8B — Rectory Office
**Dimensions:** 16ft x 14ft | Ceiling: 9ft
**Lighting:** Two windows, desk lamp, overhead

Weiss's working space. Books, a modest desk, church records. He offers coffee. It's good coffee for a small rural church, which Maddox notes.

**Key Interactables:**
- **Church ledger, 1864–1890** — Records of congregation members, deaths, donations. Several entries in 1864–1865 use coded language for Ironveil activity. Weiss will translate if asked. He's been translating them for years, alone.
- **Weiss's personal notebook** — On his desk, open. He doesn't hide it. Contains his own research into what his ancestors were part of. He has gotten close to the truth. He's missing two pieces. Maddox has one of them. This is the conversation that unlocks the Libertytown farmstead.

---

## INT-09 | Abandoned Farmstead — Cellar
**Building:** Off Route 26 East. Farmhouse structurally unsafe — exterior only. Cellar accessed via exterior entrance in rear yard.
**Total Footprint (cellar):** ~600 sq ft
**Access:** Exterior cellar door, padlocked. Lock is old. Maddox can handle it.

### Room 9A — Farmstead Cellar
**Dimensions:** 30ft x 20ft | Ceiling: 6ft (stone and timber, one timber cracked and sagging)
**Lighting:** None. Maddox's equipment only.
**Hazard:** Structural instability. Three zones of the ceiling are marked (in-game) with visual indicators — moving under the cracked timber triggers a timed sequence. Prolonged exposure without shoring it up risks a collapse event.

The Ironveil's primary working location during the original sealing. The walls are covered — not just inscribed, covered — in the symbolic sequence, layered over multiple applications spanning decades of maintenance. The sealing ritual was performed here before being moved to the Best Farm cellar for the final act.

**Key Interactables:**
- **The sealing apparatus (center)** — The remains of a device built from period materials: iron, copper, glass, and organic elements. Partially disassembled — deliberately. Someone took it apart. The missing components are distributed across locations Maddox has already visited (or will visit). Reassembly is an Act III objective.
- **Document cache (east wall, behind loose stones)** — Three stones in the east wall are not mortared. Behind them: a sealed tin containing the Ironveil's operational manual. It describes the sealing process, the materials required, and — critically — what happens if the seal is broken before the ritual is complete.
- **The floor drain (southwest corner)** — An iron drain cover, original to the structure. Below it: a narrow vertical shaft, approximately 18 inches wide, dropping 40 feet into the tunnel network. Too narrow for Maddox. Not too narrow for Dexter, if given a specific command. Dexter can be sent down with a camera harness (craftable) to map the shaft.

---

---

# ZONE 5 — MIDDLETOWN

---

## INT-10 | Old Lutheran Church — Main Street
**Building:** Active church, 1847 original construction. Stone exterior, wooden interior.
**Total Footprint:** ~3,200 sq ft including sanctuary, undercroft, and bell tower
**Access:** Sanctuary public. Undercroft via pastor. Bell tower locked.

### Room 10A — Sanctuary
**Dimensions:** 48ft x 32ft | Ceiling: 26ft (stone vaulted)
**Lighting:** Tall lancet windows, minimal artificial lighting — designed to rely on natural light

Older and heavier than St. Paul's in Libertytown. Stone walls, stone floors, the specific chill of a building that holds cold regardless of season. The pastor, Reverend James Tillman, has been here 31 years. His family has been in Middletown since before the church was built. He knows about the Ashborne. He calls it something else — an old German compound word his grandmother used. He's been waiting for someone to come asking. He's afraid it took this long.

**Key Interactables:**
- **The baptismal font (north apse)** — Original 1847 stone. The basin is deeper than standard — nearly 3 feet. The sides have inscription in German and in the Ironveil symbolic language. The water in the font is always cold. It has been cold since 1864, Tillman says. The heating system doesn't explain it.
- **Nave floor, center aisle** — Three floor stones are slightly different from the surrounding material — different quarry, different era. They form a triangle pattern. The triangle, plotted on a map, points toward the South Mountain tunnel entrance Maddox hasn't found yet.
- **The organ (west wall)** — A pipe organ, original to the church. One pipe, second from the left in the main bank, is sealed — plugged with a lead plug. Removing the plug (small, requires fine tool) reveals the pipe is hollow beyond the plug. Inside: a rolled document in oilcloth. The document is a second copy of the sealing apparatus schematic, with annotations the farmstead version doesn't have.

---

### Room 10B — Undercroft
**Dimensions:** 40ft x 28ft | Ceiling: 8ft (vaulted stone, below grade)
**Lighting:** Small windows at grade level (very dim), hanging fixtures on pull-chains
**Access:** Staircase behind altar, with Tillman's permission.

The functional undercroft — used for church events, storage, fellowship. Stone walls and floor. A kitchen area on the south wall. But against the north wall, behind stored folding tables: a section of stonework that has been, at some point, built up. The original wall behind it is different.

**Key Interactables:**
- **Built-up north wall** — The additional stonework is 1890s construction over something older. Behind it (ground-penetrating scan, mid-game tool) is a sealed chamber approximately 8ft x 8ft. Getting through the wall without collapsing it is a puzzle. What's inside: an Ironveil ritual kit far more intact than the farmstead remains, and a journal written in the hand of one of the original members. The journal's final entry is dated July 14, 1864 — five days after the battle.

---

### Room 10C — Bell Tower
**Dimensions:** 8ft x 8ft per level | Four levels | Ceiling per level: 10ft
**Lighting:** Open belfry at top provides light to upper levels; lower levels are dark
**Access:** Exterior locked door on north side of church. Key held by Tillman (obtainable) or lockpick.

Narrow wooden stairs, each landing progressively less stable. The bell at the top is original and was last rung in 1943. The mechanism is frozen. The view from the belfry takes in the entire Middletown Valley — and, on a clear day, the South Mountain ridge where the tunnel entrance is located.

**Key Interactables:**
- **Level 2 landing** — A carved mark on the floor joist. The same coordinate notation system as the pew in Libertytown. These coordinates complete the location fix for the South Mountain tunnel entrance.
- **The bell mechanism** — Frozen with age and deliberate interference: a small iron wedge was inserted into the mechanism at some point. Removing it and ringing the bell (activating the mechanism) triggers a response — something in the valley below reacts to the sound. This is both a puzzle solution and an atmospheric event.
- **Belfry view** — Interactive camera mode from the top. Maddox can scan the valley. At certain times of day, an anomalous heat signature is visible on the South Mountain ridge using his thermal equipment. It marks the tunnel entrance.

---

---

# ZONE 6 — HAGERSTOWN

---

## INT-11 | The Maryland Theatre — Backstage & Basement
**Building:** 21 S Potomac St, Hagerstown. Active performing arts venue.
**Total Footprint (restricted areas):** ~3,800 sq ft backstage and below grade
**Access:** Public entrance for performances. Backstage requires staff access (obtainable via social engineering or after-hours entry). Basement is not on the public map.

### Room 11A — Backstage
**Dimensions:** 55ft x 30ft (irregular, follows stage geometry) | Ceiling: 40ft (flies above)
**Lighting:** Work lighting (dim blue-white), caged bulbs at head height, stage light bleed from the wings

The working backstage of an active theater — ropes, counterweights, flats, costume racks. It smells like old fabric and paint and the specific electrical smell of stage lighting at temperature. It's loud when a show is running. Between shows, it's very quiet and very large.

**Key Interactables:**
- **Fly system (overhead)** — Rope lines and counterweights managing the rigging above the stage. Several lines are tied off in positions inconsistent with any standard theatrical use — they form a specific pattern when viewed from above. The pattern is recognizable by Act II. Someone has been using this space.
- **Prop storage (stage right)** — Racks of props from past productions. Among them, several items that are not props — real objects with significant age and material composition (identifiable with Maddox's scanner) mixed in deliberately.
- **The loading dock door (north wall)** — Large, heavy, alarmed. The alarm has been disabled on one circuit — not the main alarm, a secondary circuit that was added in the last 18 months. Someone has regular access to this space outside of performance hours.

---

### Room 11B — Sub-Basement
**Dimensions:** 48ft x 36ft | Ceiling: 8ft (concrete)
**Lighting:** Installed by someone recently — LED strips on a battery backup system not connected to the building's power. Very deliberate.
**Access:** Hidden staircase behind a false wall in the theater's lower storage level.

This space doesn't appear in any building plan on file with the city. It was excavated — the concrete is less than five years old. It's clean, climate-controlled (portable units), and organized. It looks like an operational planning space, not a storage room.

**Key Interactables:**
- **Map table (center)** — A large surface with a physical map of Frederick County, annotated extensively. The annotations match the cipher Maddox has been decoding. But here the cipher is applied to locations — marking a sequence of sites that correspond to the Ironveil's original sealing points. Each point has a status: some marked complete. The seal isn't cracking by itself. It's being methodically dismantled.
- **Equipment storage (north wall)** — Procurement records and specialized equipment. Cross-referencing with the Hagerstown antique row acquisitions reveals the full artifact list the Keeper has assembled. Several items are checked off. Some Maddox has already encountered.
- **The comms setup (southeast corner)** — A laptop and encrypted radio setup. The laptop is locked but the radio has an active frequency. Maddox can listen. What he hears is a voice he recognizes. This is the moment the Keeper's identity becomes clear.
- **Exit tunnel (north wall)** — A doorway into a narrow concrete-walled passage heading northeast. It connects, after approximately 200ft, to the warehouse district. It's the Keeper's operational exit route and becomes a chase sequence location in Act III.

---

## INT-12 | The Warehouse — Hagerstown District
**Building:** South Hagerstown warehouse district. Registered to Ashborne Holdings LLC (shell company — Maddox takes a moment with this name).
**Total Footprint:** ~8,000 sq ft single-story plus mezzanine
**Access:** Loading dock (padlocked), personnel door (electronic lock — good one, takes time), or tunnel entrance from the theater sub-basement.

### Room 12A — Main Floor
**Dimensions:** 100ft x 60ft | Ceiling: 24ft (industrial steel)
**Lighting:** High-bay industrials (half operational), large skylights (dirty, diffuse light)

Large, mostly empty. Pallet racking along the walls with limited contents — enough to look like a working warehouse at a glance. The center floor has been cleared. At its center is a structure approximately 12ft x 12ft constructed from materials Maddox recognizes from the Ironveil documents — the wrong materials, assembled incorrectly. Not a sealing. The opposite.

**Key Interactables:**
- **The counter-structure** — A deliberate inversion of the Ironveil's sealing apparatus. Where the original was designed to contain, this is designed to invite. Maddox can analyze it with his equipment. What he finds will require everything he's learned to understand. Dexter will not approach within 20 feet of it.
- **Mezzanine office** — Above the main floor, accessible via steel stair. Contains the Keeper's organizational records — the full scope of the operation, timeline, personnel (most of it coded). And one personal item that makes the Keeper human in a way that complicates everything.
- **Loading dock (north wall)** — Three dock doors. One is internally sealed — welded shut from inside. The other two are operational. One of the dock areas has equipment for transport, suggesting something was meant to leave this building. Or arrive.

**Hazard State:** The main floor is the game's most dangerous interior. The counter-structure radiates the Ashborne's influence at full intensity. Electronics fail fast. Dexter is visibly distressed. The ceiling fixtures arc. The temperature at the structure is below freezing. This is the final confrontation's staging ground.

---

---

# APPENDIX — UNIVERSAL INTERIOR RULES

## Dexter Behavior Reference
| Behavior | Meaning |
|---|---|
| Sniffing along floor | Something hidden below or recently passed through |
| Sitting and staring at a wall | Hollow space, hidden door, or occult inscription behind |
| Refusing to enter a zone | Active supernatural hazard — requires preparation before entry |
| Hackles raised, stationary | Immediate threat, human or supernatural, nearby |
| Pressing against Maddox's leg | Maddox is in danger he hasn't recognized yet |
| Sitting calmly in an otherwise tense space | The space is safer than it appears — trust it |

## Hazard State Escalation (All Interiors)
- **Act I:** Baseline. Anomalies subtle. Equipment mostly reliable.
- **Act II:** Escalating phenomenon. Cold zones expand. Electronics intermittent. Dexter reactions more frequent and intense.
- **Act III:** Active. Some areas become time-limited. Counter-structure influence radiates outward. Two interiors (City Hall server room, Warehouse main floor) require protective equipment to enter without penalty.

## Lighting Philosophy
Every interior has three lighting states:
1. **Normal** — As described above.
2. **Compromised** — Power failure, equipment disruption, or Ashborne interference. Relies on Maddox's carried light sources.
3. **Phenomenon** — Ashborne active. Light sources fail unpredictably. Dexter's white chest patch is luminescent in this state — a subtle navigation guide. (This is why the Phoenix marking matters.)
