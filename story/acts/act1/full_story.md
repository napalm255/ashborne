# Act 1: The Intrusion — Full Story
## Complete Narrative of April 7–19, 2025

---

## Scene 1: The Contract
**Tuesday, April 8, 2025 — Morning**

Maddox's apartment was quiet the way apartments are quiet at 8 AM when you've been awake for two hours already and the rest of the city is still sleeping. His coffee maker hissed. Three monitors glowed. Dexter's snoring formed a bass line under everything.

The Signal notification on his MagSafe-mounted phone was from a contact labeled FCC-Vendor. A DocuSign link. Maddox opened it on his laptop — the contract was for a penetration assessment of Frederick's municipal network infrastructure, including wireless survey of City Hall and surrounding civic buildings. Server room access review. External-facing web services. Scope: three weeks. Rate: acceptable.

He signed at 8:47 AM.

Dexter appeared at his elbow, having decided that if Maddox was awake then morning had officially begun. Maddox told him they had a city job. Dexter sat down. He approved of steady income. They had done this dance a hundred times.

---

## Scene 2: City Hall Discovery
**Wednesday & Thursday, April 9–10 — City Hall, Basement Server Room**

The server room was cold. 65 degrees Fahrenheit, maintained mechanically, and Maddox noticed immediately that the temperature should have been higher given the heat load from running equipment. He made a note.

Thomas Hale — the city IT director, 51, the kind of competent that doesn't draw attention — showed him the racks. Standard equipment. Dell and HPE servers, Cisco switching, UPS battery backup. Nothing unusual. Nothing that shouldn't be there.

Until Maddox ran his Nmap scan on the network segment marked as "decommissioned." A server that predated the 2004 infrastructure rebuild was active and responding. He mentioned this to Hale. Hale's face did something brief and tired.

"That's been there forever," Hale said. "Legacy junk. We've had contractors look at it twice. It's air-gapped, isolated, not worth the audit paperwork to properly retire."

Maddox had his HackRF One in the go-bag. He set it running, scanning the RF spectrum. Standard stuff. WiFi. Cellular. And then something that shouldn't be there — a signal originating from inside the server room, on a frequency that had no business having active transmission.

He zoomed in. The signal wasn't constant. It was modulated. And the modulation pattern was old. Pre-digital architecture. Something like Vigenère cipher but adapted, evolved. He'd never seen anything like it.

He flagged it to Hale. "You have an RF emission from that legacy partition. Something's broadcasting."

Hale looked at the data on Maddox's analyzer screen. His expression didn't change. "Probably electromagnetic bleed-through from the power supplies. Old equipment radiates. I'll have the electrician check the shielding."

But Hale didn't have the electrician check anything. Maddox would learn this later, after Hale was already dead.

---

## Scene 3: The Death
**Saturday, April 12, 2025 — Frederick Memorial Hospital**

Nora texted Maddox while she was in the middle of her shift: *code blue came in from city hall, server room area, you still doing work there?*

He called her back. She couldn't say much — patient privacy — but by evening it was public: Thomas Hale, cardiac event, found unresponsive in the City Hall server room. Age 51. No prior cardiac history.

Maddox's first instinct was correct: this wasn't a coincidence. His second instinct was correct too: he shouldn't have this thought, it was paranoid and conspiratorial and he was reaching.

He pulled the Verkada security feed before city IT locked him out of contractor access (which happened at midnight). He watched Hale working at his personal station. Normal activity. And then 47 seconds of corrupted footage — not deleted, not looped. *Rewritten.* Like someone had gone into the video file and changed what happened. The metadata was corrupted too, in a pattern Maddox had never encountered.

He downloaded everything before his access expired.

---

## Scene 4: The Decision
**Sunday, April 12 — Apartment, Late Night**

Maddox had everything he'd downloaded. He had no legal standing to continue investigating. He continued anyway.

Dexter was asleep on his bed. When Maddox opened the corrupted video file for the fifteenth time, Dexter's eyes opened. He didn't move. He just looked at Maddox from across the room with that specific dog attention that meant he was monitoring the situation.

Maddox said: "Don't start. I know."

Dexter closed his eyes again. He wasn't judging. He was just bearing witness.

Maddox made coffee at 2 AM and didn't sleep.

---

## Scene 5: Carroll Creek Recon
**Monday, April 13 — Dawn**

Walking the Carroll Creek waterfront with Dexter at 6 AM. The city was quiet. Maddox was thinking. There had to be a pattern. The partition couldn't be isolated. If it was propagating through the network, there had to be entry points.

He spotted a city maintenance access panel on one of the creek bridge supports — a telemetry node for the city's infrastructure monitoring. His HackRF found a signal on it. Frequency didn't match city spec. Signal pattern matched the partition's signature exactly.

The partition wasn't in City Hall. It was everywhere.

Dexter was calm. That was the part that convinced Maddox he wasn't imagining this. Dexter recognized something wrong, and Dexter didn't do paranoia. Dexter did threat assessment.

---

## Scene 6: Colt & Compass
**Monday, April 13 — Afternoon**

Vivienne Colt's antique shop smelled like old paper and cedar oil. Dexter pulled toward it as if magnetized — unusual for Dexter, who was normally confident and didn't need direction. Maddox had been here before, bought some signal equipment from Vivienne years back. He went in.

He had printed the cipher pattern from his notes on paper. No screen. He showed it to Vivienne.

She took the paper. She looked at it for three seconds. Then: "Where did you find this?"

"Frederick's municipal network. Legacy server, supposed to be decommissioned."

Vivienne turned and walked to the back of the shop. She opened the archive door with a key. Maddox followed. Inside, she pulled a box from a shelf — labeled "Civil War, Monocacy, August 1864" — and extracted a field document, hand-written, on paper that was genuinely old.

The cipher pattern was identical.

She said: "What you found has been in Frederick for one hundred and sixty-one years."

---

## Scene 7: Monocacy Battlefield — Night
**Tuesday, April 14 — Evening**

Maddox rode the motorcycle to Monocacy after dark. Trespassing. Not caring. The HackRF went into distortion near the Monocacy River ford — readings that shouldn't be possible. Dexter was tense but didn't break. He was mapping signal intensity when a light appeared on the path.

Wren Calloway. 34, competent, currently doing evening monitoring rounds after recent vandalism reports at the site. She found Maddox with RF equipment in a restricted area. She was professional and firm. He was charming in a way that didn't hide what he was doing.

She was about to report him. Scout — her Belgian Malinois mix — went alert on the same spot Dexter was fixed on. Both dogs, same response, different handlers. Wren let Maddox go with a warning and the unsettled feeling of having just seen something she couldn't dismiss.

He rode home. She stayed another hour writing in her field notebook.

---

## Scene 8: Detective Okafor
**Wednesday, April 15 — Afternoon**

Ray Okafor at the apartment door. Detective, homicide division. He'd been assigned to investigate the suspicious death. His opening line was crisp: "You were contracted to assess city IT infrastructure starting April 14. Thomas Hale died approximately 36 hours into that assessment. Help me understand the connection."

Maddox was trapped. He told Okafor what was safe to say. Hale was concerned about network anomalies. Maddox was assessing them. No connection he was aware of to Hale's death. Okafor knew Maddox was holding back. He didn't push too hard. Yet.

"If you become aware of anything relevant to the death," Okafor said before leaving, "you have an obligation to report it."

---

## Scene 9: Vivienne's Archive — Deeper
**Thursday, April 16 — Colt & Compass Archive**

Second visit. Vivienne opened the archive more completely. She showed him documents from the Ironveil — a secret order formed after the Battle of Monocacy. Soldiers. Two clergymen. A telegraph operator. They witnessed something on the battlefield. They spent their remaining lives containing it.

The entity: the Ashborne. A name from fragmented documents. Something that fed on the carnage of July 9, 1864. Not killed. Sealed. Because sealed things could hold. Killed things didn't.

She explained, in measured language, what had to be true: the partition in Frederick's network was the Ashborne's current housing. It had adapted from one substrate to another over 161 years. And the seal was failing.

Dexter sat beside Vivienne's chair. She scratched behind his ear. She understood something about the dog that Maddox couldn't name.

---

## Scene 10: Historical Society
**Saturday, April 17–18 — Frederick County Historical Society**

Margaret Howell, archivist for 28 years. Maddox built rapport by being genuinely interested in Frederick's history. He got access to the restricted archive. Found the photograph: July 11, 1864, soldiers in front of a Frederick building. Three of them had the same symbol on their lapels. He photographed it.

Then he texted Wren: *found something. you have battlefield records?*

She texted back: *found the same symbol. different location. we need to talk.*

---

## Scene 11: The Pub
**Friday, April 17 — Evening**

The Monocacy Pub. Dexter in the sidecar outside. Scout alert on a short lead beside Finn, Wren's golden retriever, who was asleep against Scout's side. Maddox and Wren were guarded for twenty minutes. Then one of them showed the other something they'd been keeping back.

By closing time, they had cross-referenced their independent data. Her field observations. His RF measurements. His network analysis. Her historical context. The patterns aligned perfectly.

Something real was happening. Something neither of them had been crazy for recognizing. Something that was getting worse.

---

## Scene 12: Hale's Workstation
**Saturday, April 18 — City Hall, After Hours**

Maddox cracked Hale's workstation password (simple: Hale's daughter's name, Hale's birth year, standard pattern). Inside was a TrueCrypt container labeled cryptically: "weird_notes."

Inside that: fourteen months of anomaly logs. Hale's personal shorthand. Power draw spikes. Firmware integrity checks failing. Permissions escalations from the partition. All documented. All dated. The earliest entry was fourteen months before the game's start.

The partition had been active, spreading through the network, for over a year. No one knew. Just Hale. Just Vivienne, who'd noticed other things. Just Dexter, who'd been alert the whole time.

---

## Scene 13: The Ghost Access
**Sunday, April 19 — Morning**

Maddox's monitoring terminal flagged an active session on the partition. From Terminal 7 in the server room. Unoccupied. No one was there.

He had his own camera tap on the server room. He pulled the feed. Terminal 7: empty. The session was active. Authenticated. Accessing Hale's anomaly folder (which Maddox had left in place deliberately). Reading. Closing.

Eleven minutes of someone — something — operating a keyboard no one was touching.

He called Wren. No preamble: "Something accessed the server room remotely this morning. No user. Active authenticated session."

Pause. "I'll be there at 7."

---

## Scene 14: The Commitment
**Sunday, April 19 — Midnight**

Apartment. Workstation. Three windows open: the tap data, Hale's anomaly logs, the waveform from the corrupted video. He ran the waveform against the signal captured at Carroll Creek. They matched. The same signal. In the network partition. In the soil by the river.

He opened his physical field notebook to a fresh page. Wrote the date: Tuesday, April 22, 2025.

Then: *The partition is a seal. Something is inside it. And I just told it I can hear it.*

He closed the notebook. Dexter, who had been asleep, opened his eyes and looked at Maddox. He didn't move. Just looked.

Maddox said: "Don't start. I know."

Dexter closed his eyes again.

Maddox made coffee and didn't sleep.

---

## Act 1 Ends

The investigation is real. The seal is cracking. Maddox has committed to staying in it.

Wren is incoming. They have no idea what they're walking into, but they're walking into it anyway.

Dexter knows. He's known the whole time.

And something, somewhere in Frederick's digital and physical infrastructure, is aware that it's being noticed.

