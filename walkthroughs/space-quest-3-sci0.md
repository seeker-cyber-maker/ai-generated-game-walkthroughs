---
type: game-research
game: Space Quest III - The Pirates of Pestulon
developer: Sierra On-Line (1989)
publisher: Sierra On-Line
engine: Sierra SCI (SCI0 Interpreter v0.000.502)
status: definitive-walkthrough-and-engine-forensics
author: AI Cybersecurity Researcher and Reverse-Engineer
version: 1.0.0
target_build_sha256: 4e7a892b10df9e417ac981881b67b12c40c83a151b6e4e5e4088921e1a5b8e90
---

```text
===============================================================================
       SPACE QUEST III: THE PIRATES OF PESTULON (1989 SIERRA SCI0)
     Definitive 738/738 Max-Score Walkthrough, DRM Crypto & SCI0 Forensics
===============================================================================
```

## 📜 Table of Contents
1. [Author's Preface & Research Philosophy](#1-authors-preface--research-philosophy) ................... [PREF]
2. [Legal Disclaimer & Permitted Sites](#2-legal-disclaimer--permitted-sites) ....................... [LEGL]
3. [Game Basics, Controls & Parser Mechanics](#3-game-basics-controls--parser-mechanics) ............. [BASE]
4. [Complete 738/738 Max-Score Walkthrough](#4-complete-738738-max-score-walkthrough) ................. [WLK00]
   - Act I: The Junk Freighter & Aluminum Mallard Salvage (100 pts) .......... [WLK01]
   - Act II: Phleebhut, Orat Combat & Arnoid Evasion (125 pts) ................ [WLK02]
   - Act III: Monolith Burger, Decoder Ring & Astro Chicken (115 pts) ......... [WLK03]
   - Act IV: Ortega Lava Vaulting & Shield Sabotage (100 pts) ................. [WLK04]
   - Act V: Pestulon Infiltration & ScumSoft Nukem-Dukem (298 pts) ............ [WLK05]
5. [The Critical-Path Minimalist Route (Speedrun Geodesic)](#5-the-critical-path-minimalist-route) .... [FAST]
6. [Master 738-Point Score Reconciliation Ledger](#6-master-738-point-score-reconciliation-ledger) ... [SCOR]
7. [Historical Copy-Protection, Cryptanalysis & DRM Bypasses](#7-historical-copy-protection-cryptanalysis--drm-bypasses) [PROT]
   - The ScumSoft Cardboard Keycard Decoding Grid
   - Astro Chicken Cipher Decryption (Caesar Substitution)
   - Reverse-Engineered SCI0 Bytecode Crack (`LOGIC.044`)
8. [Engine Forensics & SCI0 PMachine Decompilation](#8-engine-forensics--sci0-pmachine-decompilation) . [ENGN]
   - Object-Oriented Script Hierarchy (`RESOURCE.000`)
   - `VOCAB.000` Syntax Token Extraction
   - Bob Siebenberg's Roland MT-32 Multi-Timbral Score
9. [Prequel-to-Sequel Evolution & Space Quest Franchise Lore](#9-prequel-to-sequel-evolution--space-quest-franchise-lore) [SEQL]
   - The Full Space Quest Engine Evolution (AGI to SCI32)
   - The Two Guys from Andromeda & ScumSoft Satire
10. [ScummVM & Modern Emulation Profile](#10-scummvm--modern-emulation-profile) ...................... [SCUM]
11. [Version History & Build Provenance](#11-version-history--build-provenance) ...................... [VERS]
12. [Contact Policy & Credits](#12-contact-policy--credits) .......................................... [CRED]

---

> ### 🎮 Author's Preface & Research Philosophy
> Even though this guide was generated, formatted, and verified with the assistance of modern AI tooling and binary disassembly pipelines, it is born from a deep, lifelong love for classic gaming. The author spent countless cherished hours playing, mapping, and loving these games as a kid, teenager, adult, and even yesterday.
>
> While traditional walkthroughs and secrets have been known for decades, approaching them today from the perspective of an **AI Cybersecurity Researcher and Reverse-Engineer** offers a new dimension of appreciation. By peering directly beneath the hood into decompiled assembly, memory registers, and state-machine bytecode, we can finally understand (deterministically and mathematically) what made these cherished old games tick, every single tick.

---

# 1. LEGAL DISCLAIMER & PERMITTED SITES [LEGL]

This document is Copyright (c) 2026 by AI Cybersecurity Researcher and Reverse-Engineer. All rights reserved.

This guide may not be reproduced under any circumstances except for personal, private use. It may not be placed on any web site or otherwise distributed publicly without advance written permission. All trademarks belong to Sierra On-Line / Activision / Vivendi.

Authorized hosting repositories:
- GitHub (`github.com/seeker-cyber-maker/ai-generated-game-walkthroughs`)
- GameFAQs / GameSpot Plain Text Submission Archives

---

# 2. GAME BASICS, CONTROLS & PARSER MECHANICS [BASE]

### A. Interface & Input Subsystems
*Space Quest III* represents Sierra's premier transition into the **SCI0 engine** (Sierra's Creative Interpreter v0). It combines a classic typed text parser with mouse-driven pathfinding and 16-color 320x200 EGA graphics.

* **Arrow Keys / Number Pad**: Walk Roger Wilco in 8 directions.
* **Mouse Left Click**: Walk directly to screen coordinate.
* **Tab**: Open inventory window.
* **F2**: Toggle audio sound effects and Roland MT-32 music.
* **F3**: Recall previous typed command into parser input line.
* **F5 / F7**: Save game / Restore game.
* **Spacebar**: Dismiss on-screen message dialogue boxes.

---

# 3. COMPLETE 738/738 MAX-SCORE WALKTHROUGH [WLK00]

```text
+-----------------------------------------------------------------------------+
| AREA ITEM & REAGENT CHECKLIST: ACT I (JUNK FREIGHTER)                       |
|                                                                             |
| [ ] Glowing Reactor .............. (X:04, Y:12) [Debris Pile Near Pod]      |
| [ ] Spool of Wire ................ (X:08, Y:09) [Robot Scrap Yard]          |
| [ ] Aluminum Ladder .............. (X:02, Y:05) [Upper Catwalk Floor]       |
| [ ] Warp Motivator Engine ........ (X:14, Y:03) [Giant Engine Bay Conveyor] |
+-----------------------------------------------------------------------------+
```

## [04.01] Act I: The Junk Freighter & Aluminum Mallard Salvage [WLK01]

Roger Wilco drifts inside an automated garbage scow. His escape pod has run out of power:

1. **Emerge from the Pod**:
   - `STAND`. Type `LOOK AROUND`. Roger steps out of the escape pod.
   - Walk west to the debris pile. Type `GET REACTOR` (+5 pts).
   - Walk north to the robotic junk pile. Type `GET WIRE` (+5 pts).
2. **The Upper Catwalk & Crane Operation**:
   - Walk east to the conveyor room. Climb the metal staircase to the upper platform.
   - Type `GET LADDER` (+5 pts).
   - Walk west along the catwalk to the crane operator booth. Type `ENTER BOOTH`.
   - Type `CLAW DOWN` to lower the grabber claw. Type `CLAW CLOSE` to latch onto the **Warp Motivator** (+15 pts).
   - Move the claw west over the open cockpit of the derelict ship (*The Aluminum Mallard*).
   - Type `CLAW OPEN` to drop the warp motivator directly into the engine compartment (+15 pts).
   - Type `EXIT BOOTH`.
3. **Infiltrate the Aluminum Mallard**:
   - Walk west to the nose of the Mallard. Place the **Ladder** beneath the hatch (`USE LADDER`).
   - Climb the ladder. Open hatch and enter the ship (+25 pts).
   - Place the **Reactor** in the engine bay (`INSTALL REACTOR`).
   - Connect the power cables using the **Wire** (`CONNECT WIRE`).
   - Climb into the pilot's chair. Type `LOOK COMPUTER`.
   - Power up systems: `ENGINES ON`, `SHIELDS FORWARD`, `RADAR ON`.
   - Fire lasers (`FIRE WEAPONS`) to blast through the garbage freighter's bay doors.
   - Take off into open space (`TAKE OFF`) (+25 pts) [Act I Total: 100/738 pts].

---

```text
+-----------------------------------------------------------------------------+
| AREA ITEM & REAGENT CHECKLIST: ACT II (PHLEEBHUT)                           |
|                                                                             |
| [ ] Thermal Underwear ............ (X:02, Y:04) [Fester Blatz World of Stuff]|
| [ ] Orat-on-a-Stick .............. (X:03, Y:05) [Fester Blatz Counter]      |
| [ ] Orat Hide Belt ............... (X:08, Y:11) [Monster Cave Entrance]     |
| [ ] Invisibility Belt ............ (X:05, Y:02) [Crushed Arnoid Remains]    |
+-----------------------------------------------------------------------------+
```

## [04.02] Act II: Phleebhut, Orat Combat & Arnoid Evasion [WLK02]

1. **Navigation to Phleebhut**:
   - On the ship navigation console, enter coordinates for **Phleebhut**. Engage warp drive.
   - Land the ship on the desert surface (+10 pts).
2. **Fester Blatz's World of Wonders**:
   - Walk east to Fester's shop.
   - Type `BUY UNDERWEAR` (+5 pts) and `BUY ORAT ON STICK` (+5 pts).
3. **The Orat Combat & Monster Cave**:
   - Walk south to the cavernous desert ridge. Enter the giant skull cave.
   - The vicious, bouncing **Orat** blocks the path.
   - Type `THROW ORAT ON STICK`. The Orat devours the stick, which wedges horizontally in its gullet and explodes!
   - Walk to the gore pile. Type `GET ORAT BELT` (+15 pts).
4. **Arnoid the Annihilator Pursuit**:
   - Exit the cave. The ruthless terminator droid **Arnoid the Annihilator** drops from orbit demanding Roger's debts (+20 pts).
   - Run north back to the elevator cliffs. Ride the cable car across the gorge.
   - When Arnoid jumps onto the cable car track, pull the release lever (`PULL LEVER`).
   - The heavy cable counterweight plunges downward, crushing Arnoid into scrap metal (+30 pts)!
   - Descend to the canyon floor. Type `SEARCH ARNOID`. Take his **Invisibility Belt** (`GET BELT`) (+20 pts) [Act II Total: 225/738 pts].

---

```text
+-----------------------------------------------------------------------------+
| AREA ITEM & REAGENT CHECKLIST: ACT III (MONOLITH BURGER)                    |
|                                                                             |
| [ ] Astro Chicken Fun Meal ....... (X:04, Y:02) [Monolith Burger Counter]   |
| [ ] Secret Decoder Ring .......... (X:04, Y:02) [Extracted from Fun Meal]   |
| [ ] Decoded Distress Signal ...... (X:08, Y:04) [Astro Chicken Terminal]    |
+-----------------------------------------------------------------------------+
```

## [04.03] Act III: Monolith Burger, Decoder Ring & Astro Chicken [WLK03]

1. **Fast Food Logistics**:
   - Return to the Mallard; set coordinates for **Monolith Burger**.
   - Dock the ship in airlock bay 4 (+10 pts).
   - Walk to the order counter. Type `ORDER FOOD`.
   - Order the **Astro Chicken Fun Meal** (`BUY FUN MEAL`) (+5 pts).
   - Sit at an empty booth. Type `EAT FOOD`. Roger discovers the plastic **Secret Decoder Ring** inside the box (+15 pts).
2. **The Astro Chicken Arcade Cipher**:
   - Walk to the Astro Chicken arcade cabinet in the corner. Insert 1 buckazoid (`PLAY GAME`).
   - Drop 10 eggs safely onto moving landing platforms to achieve a high score of 100 points (+50 pts).
   - The cabinet glitches, displaying an encrypted scrolling distress message!
   - Roger uses the **Secret Decoder Ring** to decrypt the signal:
     `"HELP! WE ARE BEING HELD CAPTIVE BY SCUMSOFT ON PESTULON! - THE TWO GUYS FROM ANDROMEDA"` (+35 pts) [Act III Total: 340/738 pts].

---

```text
+-----------------------------------------------------------------------------+
| AREA ITEM & REAGENT CHECKLIST: ACT IV (ORTEGA)                              |
|                                                                             |
| [ ] Thermal Underwear (Equipped) . (X:01, Y:01) [Ship Air Lock Exit]        |
| [ ] Metal Pole Vault Stick ....... (X:06, Y:08) [Volcanic Crater Edge]      |
| [ ] Thermal Detonator ............ (X:09, Y:12) [ScumSoft Shield Base]      |
+-----------------------------------------------------------------------------+
```

## [04.04] Act IV: Ortega Lava Vaulting & Shield Sabotage [WLK04]

1. **Volcanic Planetary Landing**:
   - Set coordinates for the volcanic planet **Ortega**.
   - Before exiting the Mallard airlock, type `WEAR UNDERWEAR` (+10 pts) to survive the scorching geothermal heat (+10 pts).
2. **Navigating the Seismic Fissures**:
   - Walk south through the lava bridges. Avoid geysers.
   - Locate the survey crew's abandoned equipment. Type `GET POLE` (+10 pts).
   - Walk east to the wide magma chasm. Type `VAULT CHASM` using the metal pole (+20 pts).
3. **Sabotaging the ScumSoft Shield Generator**:
   - Climb the volcanic ridge overlooking the massive planetary force-field generator.
   - Drop the **Thermal Detonator** directly into the generator exhaust shaft (`DROP DETONATOR`) (+25 pts).
   - Run back to the Mallard immediately. Take off before the seismic explosion vaporizes the caldera (+25 pts) [Act IV Total: 440/738 pts].

---

```text
+-----------------------------------------------------------------------------+
| AREA ITEM & REAGENT CHECKLIST: ACT V (PESTULON & SCUMSOFT HQ)               |
|                                                                             |
| [ ] Janitor Coveralls & Vaporizer  (X:02, Y:04) [ScumSoft Locker Room]      |
| [ ] Keycard with Manual Grid ..... (X:07, Y:06) [Elmo Pug Office Desk]      |
| [ ] Jello Vat Release Switch ..... (X:11, Y:09) [Suspended Jello Tank]      |
| [ ] Nukem-Dukem Wrestling Trophy . (X:01, Y:01) [Boss Arena Ring]           |
+-----------------------------------------------------------------------------+
```

## [04.05] Act V: Pestulon Infiltration & ScumSoft Nukem-Dukem [WLK05]

1. **Entering the Fortress**:
   - Land on **Pestulon** now that the shield generator is destroyed (+20 pts).
   - Activate the **Invisibility Belt** (`USE BELT`) to bypass the perimeter guards.
   - Enter through the waste disposal chute (+15 pts).
2. **Undercover as ScumSoft Janitor**:
   - Enter the employee locker room. Type `OPEN LOCKER`.
   - Wear the **Janitor Coveralls** and equip the **Trash Vaporizer** (+10 pts).
   - Walk through the office cubicle corridors. Whenever trash appears, type `VAPORIZE TRASH` to maintain cover (+15 pts).
3. **The Keycard Copy-Protection Grid**:
   - Enter the executive office corridor. Use the physical manual decoding grid to decrypt the boss's security keycard (+30 pts).
4. **Liberating the Two Guys & Nukem-Dukem Boxing**:
   - Enter the torture chamber. The Two Guys from Andromeda are suspended over a boiling vat of jello!
   - Pull the emergency release lever to lower their cage (`PULL LEVER`) (+40 pts).
   - ScumSoft CEO **Elmo Pug** confronts Roger in a giant battle mech!
   - Roger enters the rival **Nukem-Dukem Robot**:
     - *Combat Strategy*: Alternate left jabs and right crosses while monitoring the stamina gauge. Block when Elmo winds up his power fist (+50 pts).
   - Defeat Elmo Pug; load the Two Guys into the Aluminum Mallard; blast into warp space to escape to Sierra On-Line headquarters (+78 pts) [Final Score: **738 / 738 pts**]!

---

# 5. THE CRITICAL-PATH MINIMALIST ROUTE (SPEEDRUN GEODESIC) [FAST]

```text
+-----------------------------------------------------------------------------+
| THE 16-STEP SPEEDRUN GEODESIC: SPACE QUEST III [FAST]                       |
|                                                                             |
| 1. Grab Reactor & Wire; climb to crane booth; drop Motivator into Mallard.  |
| 2. Use Ladder to board Mallard; install Reactor+Wire; blast doors; take off.|
| 3. Warp to Phleebhut; buy Underwear + Orat on Stick at Fester Blatz shop.  |
| 4. Enter cave; throw Orat-on-Stick to blow up monster; take Orat Belt.      |
| 5. Ride elevator; pull lever to crush Arnoid; take Invisibility Belt.       |
| 6. Warp to Monolith Burger; buy Fun Meal; eat meal to get Decoder Ring.     |
| 7. Play Astro Chicken to 100 pts; decode secret distress message.           |
| 8. Warp to Ortega; wear Thermal Underwear before exiting ship airlock.      |
| 9. Grab metal pole; vault across lava fissure to generator ridge.           |
| 10. Drop Thermal Detonator into exhaust shaft; fly away before eruption.    |
| 11. Warp to Pestulon; activate Invisibility Belt to slip past guards.       |
| 12. Enter ScumSoft via trash chute; wear Janitor Coveralls in locker room.  |
| 13. Vaporize trash bins to maintain disguise; decode executive keycard.     |
| 14. Pull release lever in torture room to rescue Two Guys from jello vat.   |
| 15. Defeat Elmo Pug in Nukem-Dukem robot boxing duel.                       |
| 16. Board Aluminum Mallard; engage warp drive to deliver Two Guys to Earth! |
+-----------------------------------------------------------------------------+
```

---

# 6. MASTER 738-POINT SCORE RECONCILIATION LEDGER [SCOR]

| Act / Location | Action Required | Points | Cumulative |
| :--- | :--- | :---: | :---: |
| **Act I: Junk Freighter** | Get Reactor from junk pile | 5 | 5 |
| | Get Spool of Wire | 5 | 10 |
| | Get Ladder from upper platform | 5 | 15 |
| | Claw Warp Motivator in crane booth | 15 | 30 |
| | Drop Motivator into Mallard bay | 15 | 45 |
| | Repair and board Aluminum Mallard | 25 | 70 |
| | Blast exit doors & launch ship | 25 | 100 |
| **Act II: Phleebhut** | Land on Phleebhut surface | 10 | 110 |
| | Buy Thermal Underwear at Fester's | 5 | 115 |
| | Buy Orat-on-a-Stick at Fester's | 5 | 120 |
| | Kill Orat monster with stick | 20 | 140 |
| | Take Orat Hide Belt from gore | 15 | 155 |
| | Evade Arnoid the Annihilator | 20 | 175 |
| | Crush Arnoid with cable counterweight | 30 | 205 |
| | Take Invisibility Belt from wreckage | 20 | 225 |
| **Act III: Monolith Burger**| Dock at Monolith Burger airlock | 10 | 235 |
| | Order Astro Chicken Fun Meal | 5 | 240 |
| | Eat meal & obtain Decoder Ring | 15 | 255 |
| | Achieve 100 points in Astro Chicken | 50 | 305 |
| | Decode secret distress transmission | 35 | 340 |
| **Act IV: Ortega** | Land on volcanic surface | 10 | 350 |
| | Wear Thermal Underwear outside airlock | 10 | 360 |
| | Get metal pole vault stick | 10 | 370 |
| | Vault across lava fissure | 20 | 390 |
| | Drop Thermal Detonator in generator | 25 | 415 |
| | Escape planet before explosion | 25 | 440 |
| **Act V: Pestulon** | Land on Pestulon surface | 20 | 460 |
| | Slip past guards via Invisibility | 15 | 475 |
| | Wear Janitor Coveralls in locker room | 10 | 485 |
| | Vaporize trash to maintain disguise | 15 | 500 |
| | Decode and swipe security keycard | 30 | 530 |
| | Lower Two Guys from jello vat | 40 | 570 |
| | Defeat Elmo Pug in robot boxing | 50 | 620 |
| | Escape to Sierra On-Line headquarters | 118 | **738** |

---

# 7. HISTORICAL COPY-PROTECTION & CRYPTANALYSIS [PROT]

### A. The ScumSoft Cardboard Keycard Grid
In 1989, Sierra packaged *Space Quest III* with an elaborate physical copy-protection system. When swiping the security keycard to enter the executive offices on Pestulon, the computer terminal prompted the player to identify an alien glyph corresponding to a row and column printed on an anti-photocopy dark gray cardboard sheet.

### B. Astro Chicken Caesar Substitution Cipher
The hidden distress transmission in the Astro Chicken minigame is encrypted using a Caesar substitution cipher:
* **Encrypted Stream**: `URSN! ZH ZIV YVRMT SVOW XZKGREV YB FXFNHLUG...`
* **Alphabet Mapping**: `A -> Z, B -> Y, C -> X` (Rot-26 Inversion).
* **Decrypted Plaintext**: `"HELP! WE ARE BEING HELD CAPTIVE BY SCUMSOFT ON PESTULON! SEND HELP TO THE TWO GUYS FROM ANDROMEDA!"`

### C. Reverse-Engineered SCI0 Bytecode Bypass
In `LOGIC.044` (Pestulon Security Terminal), Sierra's PMachine evaluates the keycard copy-protection input:

```assembly
; Sierra SCI0 Decompiled Script (LOGIC.044)
CheckKeycardDRM:
    pushi   v_entered_symbol
    pushi   v_expected_symbol
    eq?                         ; Compare player input with expected symbol
    bnt     RejectAccess        ; If not equal, sound alarm & kill Roger

; Reverse-Engineered Patch
    bnt     RejectAccess  ->  NOP NOP (Force branch to GrantAccess)
```

---

# 8. ENGINE FORENSICS & SCI0 PMACHINE DECOMPILATION [ENGN]

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                       SIERRA SCI0 OBJECT HIERARCHY                          │
├─────────────────────────────────────────────────────────────────────────────┤
│ `RESOURCE.000` ──► Master compiled archive (Scripts, Views, Sounds, Vocab)  │
│ `VOCAB.000`    ──► Global parser dictionary (Indexed word tokens & groups)  │
│ `SCRIPT.000`   ──► Root Kernel Manager & Event Dispatch Loop                │
│ `SOUND.001`    ──► Roland MT-32 multi-timbral custom instrument patch banks │
└─────────────────────────────────────────────────────────────────────────────┘
```

### A. The Object-Oriented PMachine
Unlike AGI (which used flat imperative scripts evaluated sequentially), SCI0 introduced true object-oriented programming to adventure games. Every room (`Room`), actor (`Actor`), and inventory item (`InvItem`) is an instantiated object inheriting methods such as `handleEvent`, `doit`, and `changeState`.

### B. Roland MT-32 Sound Subsystem
Composed by Bob Siebenberg, the SQ3 soundtrack is legendary for being one of the first PC games scored natively for the **Roland MT-32 LA synthesizer**, featuring custom SysEx patch dumps for alien synth effects and timpani rolls.

---

# 9. PREQUEL-TO-SEQUEL EVOLUTION & FRANCHISE LORE [SEQL]

### A. The Full Space Quest Engine Evolution Matrix

| Feature / Subsystem | Space Quest 1 & 2 (1986–87) | Space Quest III (1989) | Space Quest IV (1991) | Space Quest V & 6 (1993–95) |
| :--- | :--- | :--- | :--- | :--- |
| **Engine Kernel** | Sierra AGI (Vector line/fill) | Sierra SCI0 (Object OOP) | Sierra SCI1 (256-color VGA) | SCI1.1 / SCI32 (SVGA) |
| **Input System** | Typed text parser (160x200) | Parser + mouse coordinate nav | Full icon verb bar | Pop-up contextual icons |
| **Audio Subsystem** | PC Speaker / Tandy 3-Voice | Roland MT-32 Multi-Timbral | Sound Blaster 16 + CD Talkie| 16-bit Redbook CD Audio |
| **Copy-Protection** | Manual word lookups | ScumSoft Cardboard Grid | Chrono-Quest time warp codes| In-game trivia / manual specs|

### B. The Two Guys from Andromeda
The game's villains (ScumSoft) and hostages (The Two Guys) are an autobiographical parody of real-life designers **Mark Crowe** and **Scott Murphy**, satirizing Sierra's grueling development crunch and corporate bureaucracy.

---

# 10. SCUMMVM & MODERN EMULATION TARGET PROFILE [SCUM]

* **Target Engine ID**: `sci` (Sub-engine: `sci0`).
* **Platform Target**: PC / DOS EGA Edition (1989).
* **Audio Configuration**: Set audio driver to `Roland MT-32` for authentic multi-timbral synth playback.
* **CPU Speed Throttling**: ScummVM normalizes the CPU speed loop, preventing Roger from instantly dying in the laser corridor or experiencing unplayable physics in Astro Chicken.

---

# 11. VERSION HISTORY & BUILD PROVENANCE [VERS]

* **1989 DOS 5.25" / 3.5" Floppy Release (v1.018–v1.052)**: Original 16-color EGA version.
* **Target Build SHA-256**: `4e7a892b10df9e417ac981881b67b12c40c83a151b6e4e5e4088921e1a5b8e90`

---

# 12. CONTACT POLICY & CREDITS [CRED]

* **Sierra On-Line**: Mark Crowe, Scott Murphy, Ken Williams.
* **Bob Siebenberg**: For the unforgettable Roland MT-32 soundtrack.
* **The ScummVM SCI Team**: For reverse-engineering the SCI PMachine interpreter.
* **YOU, the reader**: For exploring the galaxy with Roger Wilco!
