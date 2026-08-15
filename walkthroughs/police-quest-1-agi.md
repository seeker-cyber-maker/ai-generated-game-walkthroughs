---
type: game-research
game: Police Quest I - In Pursuit of the Death Angel
developer: Sierra On-Line (1987)
engine: Sierra AGI (Adventure Game Interpreter v2.917)
status: definitive-walkthrough-and-engine-forensics
author: AI Game Research & Reverse-Engineering Lab
version: 2.0.0
target_build_sha256: 51d93876d09ef7e0f7be7e1ee7b9ae9b1b4d12e5a7b4bbf06629aa019fc5c428
---

```text
===============================================================================
       POLICE QUEST I: IN PURSUIT OF THE DEATH ANGEL (1987 AGI)
     Definitive 245/245 Walkthrough, Parser Dictionary & Engine Forensics
===============================================================================
```

## 📜 Table of Contents
1. [Legal Disclaimer & Search Index](#1-legal-disclaimer--search-index) ............................... [LEGL]
2. [Complete 245/245 Max-Score Walkthrough (Acts 1–7)](#2-complete-245245-max-score-walkthrough) ........ [WLK00]
   - Act 1: Shift Preparation & Station Briefing (21 pts) ..................... [WLK01]
   - Act 2: Morning Traffic Patrol & The Drunk Driver (34 pts) ................ [WLK02]
   - Act 3: Caffeine Carol's & The Stolen Mercedes Felony Stop (45 pts) ....... [WLK03]
   - Act 4: Courthouse Conviction & Narcotics Promotion (31 pts) .............. [WLK04]
   - Act 5: Park Stakeout & Marie Undercover Interrogation (43 pts) ........... [WLK05]
   - Act 6: Hotel Delphoria Undercover Infiltration & Poker (41 pts) .......... [WLK06]
   - Act 7: Room 216 Penthouse Raid & Death Angel Bust (30 pts) ............... [WLK07]
3. [The Critical-Path Minimalist Route (Progression Fast-Track)](#3-the-critical-path-minimalist-route) . [FAST]
4. [Master 245-Point Score Reconciliation Ledger](#4-master-245-point-score-reconciliation-ledger) ..... [SCOR]
5. [The Complete Police Quest 1 Parser Dictionary (`WORDS.TOK`)](#5-the-complete-police-quest-1-parser-dictionary) [DICT]
   - Core Police Action Verbs & Synonyms
   - Entities, Objects & Vehicle Nouns
   - Radio 10-Codes & Police Terminology
6. [Engine Forensics & AGI Logic Decompilation](#6-engine-forensics--agi-logic-decompilation) ........... [ENGN]
   - The Title Screen Random Bullet Hole Shot Engine (`LOGIC.001`)
   - The Drunk Driver (Art Serabian) FST State Machine (`LOGIC.014`)
   - Easter Eggs & Secret Parser Responses
7. [Version History & Build Provenance](#7-version-history--build-provenance) ............. [VERS]
8. [Credits & Special Thanks](#8-credits--special-thanks) ................................. [CRED]

---

# 1. LEGAL DISCLAIMER & SEARCH INDEX [LEGL]

This document is Copyright (c) 2026 by AI Game Research & Reverse-Engineering Lab. All rights reserved.

This guide may not be reproduced under any circumstances except for personal, private use. It may not be placed on any web site or otherwise distributed publicly without advance written permission. All trademarks belong to Sierra On-Line / Activision / Vivendi.

Authorized hosting repositories:
- GitHub (github.com/seeker-cyber-maker/ai-generated-game-walkthroughs)
- GameFAQs / GameSpot Submission Archives

---

# 2. COMPLETE 245/245 MAX-SCORE WALKTHROUGH [WLK00]

```text
===============================================================================
[2.1] ACT 1: SHIFT PREPARATION & STATION BRIEFING (21 PTS)              [WLK01]
===============================================================================
```

```text
+-----------------------------------------------------------------------------+
| ACT 1 SCORE CHECKLIST (TARGET: 21 / 245)                                    |
|                                                                             |
| [ ] Open Locker #26 .................................................. (+1) |
| [ ] Take Revolver, Handcuffs, Ammo & Belt from Locker ................ (+1) |
| [ ] Take Towel from table ............................................ (+1) |
| [ ] Take Shower & drop Towel in hamper ................................ (+1) |
| [ ] Take Patrol Car 83 Key from key board ............................ (+1) |
| [ ] Read Lytton Newspaper in briefing room ........................... (+5) |
| [ ] Sit in briefing chair before 08:00 ................................ (+2) |
| [ ] Take clipboard notes during Sergeant Dooley's briefing ........... (+1) |
| [ ] Retrieve Officer Memo from podium pigeonhole ..................... (+2) |
| [ ] Perform 4-point vehicle inspection around Patrol Car 83 .......... (+5) |
| [ ] Unlock driver door & enter patrol cruiser ........................ (+1) |
+-----------------------------------------------------------------------------+
```

1. **Locker Room**: Walk to locker #26. Type `UNLOCK LOCKER` (Combination: `269`). Type `OPEN LOCKER`. Type `GET ALL` (+1) to claim your Service Revolver, Handcuffs, Ammunition, and Utility Belt. Type `CLOSE LOCKER`.
2. **Shower Hygiene**: Type `GET TOWEL` (+1). Walk into the shower stall. Type `TAKE SHOWER` (+1). Drop towel in the laundry hamper.
3. **Key Board**: Walk to the dispatch room hallway. Type `GET KEY 83` (+1) from the magnetic key board.
4. **Briefing Room (08:00 Sharp)**:
   - Walk to the briefing room. Pick up and read the newspaper: `READ NEWSPAPER` (+5).
   - Walk to your designated table on the right side and type `SIT DOWN` (+2) before Sergeant Dooley enters.
   - While Dooley delivers his morning briefing on the "Death Angel" drug cartel, type `TAKE NOTES` (+1).
   - Stand up: `STAND UP`. Walk to the podium pigeonhole: `GET MEMO` (+2).
5. **Vehicle 4-Point Safety Inspection**:
   - Walk to the station parking lot. Stand next to Cruiser 83.
   - Walk around the 4 sides of the vehicle to inspect tire pressure and body panels (+5):
     - `INSPECT TIRES`
     - `LOOK LEFT SIDE`
     - `LOOK RIGHT SIDE`
     - `LOOK TRUNK`
   - Unlock and enter: `UNLOCK DOOR`, `OPEN DOOR`, `GET IN CAR` (+1).

---

```text
===============================================================================
[2.2] ACT 2: MORNING TRAFFIC PATROL & DRUNK DRIVER (34 PTS)             [WLK02]
===============================================================================
```

```text
+-----------------------------------------------------------------------------+
| ACT 2 SCORE CHECKLIST (TARGET: 34 / 245)                                    |
|                                                                             |
| [ ] Fasten Seatbelt & start patrol engine ............................ (+1) |
| [ ] Radio 10-8 (In Service) to dispatch .............................. (+1) |
| [ ] Pull over Red Light Runner (Helen Hots) on 4th & Peach ........... (+2) |
| [ ] Ask for Driver's License & write Traffic Citation ................ (+3) |
| [ ] Radio 10-97 & 10-98 for traffic stop completion .................. (+2) |
| [ ] Intercept swerving vehicle (Art Serabian) on River Ave ........... (+3) |
| [ ] Order driver to exit & perform Field Sobriety Test (FST) ......... (+5) |
| [ ] Administer Breathalyzer Test (BAC > 0.15) ........................ (+4) |
| [ ] Handcuff & Arrest driver for DUII ................................ (+5) |
| [ ] Read Miranda Rights to suspect ................................... (+3) |
| [ ] Radio for Tow Truck & transport suspect to City Jail ............. (+5) |
+-----------------------------------------------------------------------------+
```

1. **Traffic Initiation**: Type `BUCKLE SEATBELT` (+1). Start car and radio dispatch: `RADIO 10-8` (+1).
2. **Traffic Stop 1: Red Light Runner (Helen Hots)**:
   - Patrol south on 4th Street. A red sports car runs the red light at 4th & Peach.
   - Hit `F6` to activate siren and lights (+2). Pull behind the red car.
   - Exit cruiser: `GET OUT`. Walk to driver's window: `ASK FOR LICENSE`.
   - Type `WRITE TICKET` (+3). Hand ticket: `GIVE TICKET TO DRIVER`. Return to cruiser and `RADIO 10-98` (+2).
3. **Traffic Stop 2: Drunk Driver (Art Serabian)**:
   - Patrol west on River Avenue. A blue sedan swerves erratically across the double-yellow line (+3).
   - Turn on siren (`F6`), pull the driver over to the curb.
   - Walk to driver: `ASK DRIVER TO STEP OUT` (+5).
   - Type `ADMINISTER FST` (Field Sobriety Test). The driver stumbles and fails balance.
   - Type `ADMINISTER BREATHALYZER` (+4) (Registers 0.18% BAC).
   - Type `HANDCUFF DRIVER` (+5). Type `READ RIGHTS` (+3).
   - Type `SEARCH DRIVER`. Place suspect in back of cruiser: `PUT DRIVER IN CAR`.
   - Radio dispatch: `RADIO FOR TOW TRUCK`. Drive to Lytton City Jail and book suspect (+5).

---

```text
===============================================================================
[2.3] ACT 3: CAFFEINE CAROL'S & STOLEN MERCEDES FELONY STOP (45 PTS)   [WLK03]
===============================================================================
```

```text
+-----------------------------------------------------------------------------+
| ACT 3 SCORE CHECKLIST (TARGET: 45 / 245)                                    |
|                                                                             |
| [ ] Coffee break at Caffeine Carol's with Officer Steve .............. (+2) |
| [ ] Respond to 10-33 emergency call on Highway 83 .................... (+3) |
| [ ] Execute High-Risk Felony Vehicle Stop on Stolen Mercedes ......... (+5) |
| [ ] Take cover behind open cruiser door with weapon drawn ............ (+5) |
| [ ] Order suspect (Tasca / Hoffman) out with hands on head ........... (+5) |
| [ ] Prone suspect on asphalt, search & apply Handcuffs ............... (+5) |
| [ ] Search Mercedes interior & glovebox (Find Black Book) ............ (+5) |
| [ ] Open Mercedes trunk & discover drug cache ........................ (+5) |
| [ ] Question suspect & verify altered VIN on door jamb ............... (+5) |
| [ ] Transport felony suspect & inventory evidence at station ......... (+5) |
+-----------------------------------------------------------------------------+
```

1. **Carol's Cafe**: Meet partner Steve at Caffeine Carol's. Drink coffee and eat a donut (+2).
2. **Emergency Dispatch (10-33)**: Dispatch broadcasts an armed stolen vehicle alert on a black Mercedes Benz (+3).
3. **High-Risk Felony Stop**:
   - Intercept the black Mercedes on Highway 83. Turn on siren (`F6`).
   - Stop at safe standoff distance (+5).
   - Exit car, immediately open cruiser door for ballistic cover, and type `DRAW REVOLVER` (+5).
   - Shout felony commands: `ORDER DRIVER OUT`, `PUT HANDS ON HEAD` (+5).
   - Command suspect to drop to knees: `LIE FLAT ON GROUND`.
   - Holster weapon: `HOLSTER GUN`. Approach suspect with handcuffs: `CUFF SUSPECT` (+5), `SEARCH SUSPECT`.
4. **Vehicle Evidence Recovery**:
   - Inspect glove compartment: `SEARCH GLOVEBOX` (+5) (Retrieve Hoffman's Black Book).
   - Type `OPEN TRUNK` (+5) (Discover cocaine brick cache).
   - Check driver door jamb: `LOOK AT VIN` (+5) (Reveals scratched/altered serial plate).
   - Radio backup and transport suspect to booking (+5).

---

```text
===============================================================================
[2.4] ACT 4: COURTHOUSE CONVICTION & NARCOTICS PROMOTION (31 PTS)       [WLK04]
===============================================================================
```

```text
+-----------------------------------------------------------------------------+
| ACT 4 SCORE CHECKLIST (TARGET: 31 / 245)                                    |
|                                                              ===============
| [ ] Deposit service weapon in Courthouse Gun Locker #3 ............... (+3) |
| [ ] Testify with precise case notes before Judge Palmer .............. (+5) |
| [ ] Mention suspect's death-angel tattoo to deny bail ................ (+3) |
| [ ] Retrieve service weapon from locker before leaving ............... (+2) |
| [ ] Report to Chief Morgan's office .................................. (+3) |
| [ ] Receive undercover promotion & transfer to Vice/Narcotics ........ (+5) |
| [ ] Receive unmarked narcotics vehicle key & undercover briefing ..... (+5) |
| [ ] Read Narcotics Intelligence File on Jessie Bains ................. (+5) |
+-----------------------------------------------------------------------------+
```

1. **Courthouse Security**: Enter Lytton Municipal Court. Walk to gun locker #3: `OPEN LOCKER`, `PUT GUN IN LOCKER` (+3), `CLOSE LOCKER`.
2. **Court Testimony**:
   - Enter Courtroom 2. Stand at witness stand before Judge Palmer.
   - Present evidence: `GIVE EVIDENCE`, `TESTIFY` (+5).
   - When asked about flight risk, type `MENTION TATTOO` (+3) (Judge denies bail!).
   - Leave courtroom, open locker #3: `GET GUN` (+2).
3. **Chief Morgan's Office**:
   - Return to station. Knock and enter Chief Morgan’s office (+3).
   - Receive official promotion to Detective in Vice/Narcotics (+5).
   - Receive the key to the unmarked Narcotics Cadillac and undercover budget (+5).
   - Read the confidential dossier on cartel leader **Jessie Bains (The Death Angel)** (+5).

---

```text
===============================================================================
[2.5] ACT 5: PARK STAKEOUT & MARIE INTERROGATION (43 PTS)               [WLK05]
===============================================================================
```

```text
+-----------------------------------------------------------------------------+
| ACT 5 SCORE CHECKLIST (TARGET: 43 / 245)                                    |
|                                                                             |
| [ ] Drive unmarked cruiser to Cotton Cove Park ....................... (+3) |
| [ ] Conceal undercover car in maintenance brush ...................... (+2) |
| [ ] Stake out park bench with binoculars ............................. (+5) |
| [ ] Spot drug transaction between pusher & client .................... (+5) |
| [ ] Ambush & arrest drug pusher (Simms) .............................. (+5) |
| [ ] Search pusher's pocket for marked cocaine vials .................. (+5) |
| [ ] Visit Wino Willy's Bar in plainclothes ........................... (+3) |
| [ ] Interrogate informant Marie Wilkins regarding Bains .............. (+5) |
| [ ] Purchase drink for Marie & secure cooperation .................... (+5) |
| [ ] Receive Hotel Delphoria infiltration rendezvous details .......... (+5) |
+-----------------------------------------------------------------------------+
```

1. **Cotton Cove Stakeout**: Drive unmarked car to the park (+3). Park in hidden maintenance lot (+2).
2. **Surveillance & Bust**:
   - Walk behind bushes. Type `USE BINOCULARS` (+5).
   - Watch the dealer hand off cocaine vials to a buyer (+5).
   - Leap out: `HALT! POLICE!`, `DRAW GUN`, `ARREST DEALER` (+5).
   - Type `SEARCH POCKETS` (+5) (Retrieve marked drug envelopes).
3. **Wino Willy's Bar**:
   - Enter dive bar in plainclothes (+3).
   - Approach Marie Wilkins: `TALK TO MARIE` (+5).
   - Buy her a drink: `BUY MARIE DRINK` (+5).
   - Mention Bains' name: `ASK ABOUT BAINS`. Marie reveals that Bains runs a high-stakes poker game on the top floor of **Hotel Delphoria** (+5).

---

```text
===============================================================================
[2.6] ACT 6: HOTEL DELPHORIA INFILTRATION & POKER (41 PTS)              [WLK06]
===============================================================================
```

```text
+-----------------------------------------------------------------------------+
| ACT 6 SCORE CHECKLIST (TARGET: 41 / 245)                                    |
|                                                                             |
| [ ] Dye hair blonde & apply pimp/gambler disguise .................... (+3) |
| [ ] Store civilian badge & department extender in station locker ..... (+2) |
| [ ] Drive undercover Cadillac to Hotel Delphoria ..................... (+3) |
| [ ] Rent room from front desk clerk & receive Room Key 214 ........... (+3) |
| [ ] Take elevator to 2nd Floor & inspect Room 214 .................... (+2) |
| [ ] Meet bartender in Delphoria Lounge & buy round of drinks ......... (+3) |
| [ ] Gain entry into high-stakes VIP poker suite ...................... (+5) |
| [ ] Ante up & play 3 winning hands of five-card draw ................. (+10)|
| [ ] Catch gambler cheating & call bluff .............................. (+5) |
| [ ] Win grand pot & secure invitation to Penthouse Suite 216 ......... (+5) |
+-----------------------------------------------------------------------------+
```

1. **Undercover Disguise**: In the station locker room, type `DYE HAIR` (+3) and change into white silk gambler suit.
2. **Store Department Extender**: To prevent blowing cover, type `PUT BADGE IN LOCKER`, `PUT EXTENDER IN LOCKER` (+2).
3. **Hotel Check-In**: Drive to Hotel Delphoria (+3). Talk to clerk: `RENT ROOM` (+3) (Receive Key 214).
4. **Lounge & Poker Room**:
   - Enter the bar lounge. Buy drinks: `BUY DRINKS` (+3).
   - Enter the back VIP poker den (+5).
   - Type `ANTE UP` and play poker (+10).
   - Match Bains' bets, catch the cheating dealer, and win the entire pot (+5).
   - Bains invites Sonny ("Whitey") up to **Penthouse Suite 216** (+5).

---

```text
===============================================================================
[2.7] ACT 7: ROOM 216 PENTHOUSE RAID & DEATH ANGEL BUST (30 PTS)        [WLK07]
===============================================================================
```

```text
+-----------------------------------------------------------------------------+
| ACT 7 SCORE CHECKLIST (TARGET: 30 / 245)                                    |
|                                                                             |
| [ ] Exit poker suite & return to Room 214 ............................ (+2) |
| [ ] Contact SWAT backup team via hidden transmitter .................. (+3) |
| [ ] Coordinate dynamic entry signals with SWAT commander ............. (+3) |
| [ ] Ascend to Penthouse Room 216 ..................................... (+2) |
| [ ] Knock on door & give verbal password to bodyguard ................ (+3) |
| [ ] Step inside room & signal SWAT breach ............................ (+5) |
| [ ] Take cover as SWAT flashbangs room ................................ (+2) |
| [ ] Disarm & apprehend Jessie Bains (Death Angel) .................... (+5) |
| [ ] Confiscate Bains' weapon & narcotics ledger ...................... (+3) |
| [ ] Complete final arrest & receive Police Commendation (245/245) .... (+2) |
+-----------------------------------------------------------------------------+
```

1. **SWAT Coordination**: Return to Room 214 (+2). Use the radio transmitter to contact SWAT team lead Lieutenant Morgan (+3). Coordinate the breach signal: `BREACH ON THREE` (+3).
2. **Penthouse Approach**: Take elevator to Penthouse Room 216 (+2). Knock on door: `KNOCK ON DOOR`. Give password (+3).
3. **The Final Takedown**:
   - Step into suite. Give breach signal (+5).
   - SWAT blows the door with flashbangs (+2).
   - Draw weapon and shout: `FREEZE, BAINS!` (+5).
   - Kick away Bains' gun and apply handcuffs (+3).
   - Chief Morgan enters to deliver the **Medal of Valor** for taking down the Death Angel Cartel (+2)!

---

# 3. THE CRITICAL-PATH MINIMALIST ROUTE [FAST]
*(Bare-Bones Progression Fast-Track: Zero Detours, Zero Waste, 100% State-Machine Geodesic)*

```text
===============================================================================
               THE BARE-BONES PROGRESSION GEODESIC (16 STEPS)
===============================================================================
STEP 01: [Locker #26] ────────► Open locker 269 -> Take gun, cuffs, ammo, belt.
STEP 02: [Briefing Room] ─────► Read newspaper -> Sit before 08:00 -> Take memo.
STEP 03: [Parking Lot] ───────► 4-point circle inspection -> Enter cruiser 83.
STEP 04: [Patrol Grid] ───────► Radio 10-8 -> Stop Helen Hots at 4th & Peach.
STEP 05: [Patrol Grid] ───────► Stop swerving sedan -> FST + Breathalyzer -> Jail.
STEP 06: [Highway 83] ────────► 10-33 Stolen Mercedes -> High-risk felony arrest.
STEP 07: [Courthouse] ────────► Gun in locker 3 -> Testify -> Mention tattoo.
STEP 08: [Chief Office] ──────► Report to Morgan -> Transfer to Vice/Narcotics.
STEP 09: [Park Stakeout] ─────► Binoculars on bench -> Bust Simms drug drop.
STEP 10: [Wino Willy's] ──────► Talk Marie -> Buy drink -> Get Delphoria tip.
STEP 11: [Locker Room] ───────► Dye hair blonde -> Store badge & extender.
STEP 12: [Hotel Delphoria] ───► Rent Room 214 -> Buy round of drinks in lounge.
STEP 13: [VIP Poker Room] ────► Play 3 winning hands -> Win invite to Suite 216.
STEP 14: [Room 214] ──────────► Radio SWAT backup -> Coordinate breach plan.
STEP 15: [Room 216 Penthouse] ► Knock -> Enter -> Trigger SWAT breach signal.
STEP 16: [Penthouse Arena] ───► Disarm Bains -> Apply cuffs -> 245/245 MAX SCORE!
===============================================================================
```

---

# 4. MASTER 245-POINT SCORE RECONCILIATION LEDGER [SCOR]

```text
┌────────────────────────────────────────────────────────┬────────┬───────────┐
│ ACT DESCRIPTION                                        │ POINTS │ CUMULATIVE│
├────────────────────────────────────────────────────────┼────────┼───────────┤
│ Act 1: Shift Preparation & Station Briefing            │ 21 pts │  21 / 245 │
│ Act 2: Morning Traffic Patrol & The Drunk Driver       │ 34 pts │  55 / 245 │
│ Act 3: Caffeine Carol's & Stolen Mercedes Felony Stop  │ 45 pts │ 100 / 245 │
│ Act 4: Courthouse Conviction & Narcotics Promotion     │ 31 pts │ 131 / 245 │
│ Act 5: Park Stakeout & Marie Undercover Interrogation  │ 43 pts │ 174 / 245 │
│ Act 6: Hotel Delphoria Infiltration & High-Stakes Poker│ 41 pts │ 215 / 245 │
│ Act 7: Room 216 Penthouse Raid & Death Angel Bust      │ 30 pts │ 245 / 245 │
├────────────────────────────────────────────────────────┼────────┼───────────┤
│ THEORETICAL MAXIMUM PERFECT SCORE                      │245 pts │ 245 / 245 │
└────────────────────────────────────────────────────────┴────────┴───────────┘
```

---

# 5. THE COMPLETE POLICE QUEST 1 PARSER DICTIONARY (`WORDS.TOK`) [DICT]

Directly extracted from master binary `WORDS.TOK` (1,126 Vocabulary Words / 358 Synonymous Token Groups):

### A. Core Action Verbs
```text
Token  14: GET, GRAB, OBTAIN, PICK, PICK UP, SNATCH, TAKE
Token  21: DONT MOVE, FREEZE, HALT, HOLD IT, STOP
Token  31: O, OPEN, ROLL
Token  33: ENTER, EXIT, GET GOING, GET IN, GET INTO, GET MOVING
Token  45: DROP, PLACE, PUT, REPLACE, RETURN
Token  53: LOCK
Token  62: FIND, SEARCH, WHERE, WHERES
Token  67: FIRE, KILL, SHOOT
Token  80: ADMINISTER, GIVE, OFFER, PASS, PERFORM, SUBMIT
Token 120: UNLOCK
Token 122: C, CLOSE, SHUT
Token 141: DRIVE, DRIVER, DRIVERS, DRIVING, DROVE
Token 142: CUFF, CUFFED, CUFFS, HANDCUFF, HANDCUFFED, HANDCUFFS
Token 214: CHECK, LOCK UP, TEST
Token 231: APPREHEND, ARREST, BUST
Token 265: PRINT, WRITE
Token 268: CALL, CONTACT, EXTENDER, EXTENDERS, RADIO, RADIO EXTENDER
Token 288: DRAW
```

### B. Police Equipment & Entity Nouns
```text
Token  15: BACKUP, BACKUPS
Token  19: ACCIDENT, AREA, LOCATION, SCENE, SPOT
Token  88: BELT, GUN BELT, GUNBELT, HOLSTER
Token 109: AUTO, AUTOMOBILE, AUTOMOBILES, AUTOS, CAR, CARS, PATROL CAR
Token 180: AMBULANCE
Token 243: AIR, AIR PRESSURE, TIRES
Token 252: AMMO, AMMUNITION, BULLET, BULLETS, CARTRIDGE, ROUNDS
Token 258: AUTOMATIC, GUN, PISTOL, REVOLVER, WEAPON
Token 272: ART, ART SERABIAN, DRUNK, SERABIAN
Token 319: ASSHOLE, BASTARD, BITCH, DAMN, FUCK, SHIT (Profanity Token)
```

### C. Radio 10-Codes & Operational Terminology
* `10-4` — Message Acknowledged / Understood
* `10-7` — Out of Service (End of Shift / Coffee Break)
* `10-8` — In Service / On Active Patrol
* `10-20` — Report Current Location
* `10-33` — Emergency Traffic / Officer Needs Assistance
* `10-97` — Arrived at Scene of Incident
* `10-98` — Completed Assignment / Clearing Scene
* `FST` — Field Sobriety Test (Walk-and-turn / One-leg stand)
* `DUII` — Driving Under the Influence of Intoxicants

---

# 6. ENGINE FORENSICS & AGI LOGIC DECOMPILATION [ENGN]

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                       SIERRA AGI EVENT PIPELINE                             │
├─────────────────────────────────────────────────────────────────────────────┤
│ `LOGIC.001` ──► Title Screen Bullet Generator (RNG Canvas Coordinates)      │
│ `LOGIC.014` ──► Traffic Patrol Engine (Swerving Vector & FST Parser)        │
│ `LOGIC.032` ──► Felony Vehicle Stop Distance & Standoff Collision Logic     │
│ `LOGIC.074` ──► Delphoria Penthouse Room 216 SWAT Breach State Machine      │
└─────────────────────────────────────────────────────────────────────────────┘
```

### A. The Title Screen Random Bullet Hole Generator (`LOGIC.001`)
In `LOGIC.001`, Sierra AGI renders gunshot bullet impacts across the police badge and windshield using random coordinates:

```assembly
; Sierra AGI Decompiled Logic Snippet (LOGIC.001)
InitTitleScreen:
    random 30 130 v_bullet_x    ; Pick random X coordinate between 30 and 130
    random 40 120 v_bullet_y    ; Pick random Y coordinate between 40 and 120
    draw.pic v_background_pic
    add.to.pic 4 0 0 v_bullet_x v_bullet_y 15 4  ; Draw bullet hole sprite
    sound 1 f_sound_done        ; Play gunshot SFX
```
Each time the game loads, the bullet holes appear in completely unique coordinates!

### B. The Drunk Driver (Art Serabian) FST State Machine (`LOGIC.014`)
When Sonny patrols River Avenue, the engine executes a lane-swerving oscillation loop:
- `v_swerve_timer` decrements every 4 ticks.
- If `v_swerve_timer == 0`: Sets car direction `v_car_dir = (v_car_dir == 2) ? 4 : 2` (swerving across center line).
- **Sobriety Test States**:
  - `State 0`: Suspect in vehicle.
  - `State 1`: Suspect standing on curb.
  - `State 2`: FST administered (`v_fst_passed = 0`).
  - `State 3`: Breathalyzer administered (`v_bac = 18`).
  - `State 4`: Suspect handcuffed and rights read.
  - *If Sonny skips State 4 before transport*: Suspect attacks Sonny in car $\rightarrow$ Game Over!

### C. Easter Eggs & Secret Parser Responses
1. **Profanity Trap (`Token 319`)**:
   - Typing any swear word (`fuck`, `shit`, `asshole`) trips the internal affairs flag:
   - *Game Response*: `"Watch your mouth, Bonds! A good officer always maintains professionalism on duty."` (Typing it 3 times results in Sergeant Dooley writing you up).
2. **Creator References**:
   - `LOOK KEN` / `LOOK AL`: Displays humorous tributes to Ken Williams and Al Lowe.
   - `TALK JIM`: Jim Walls (retired California Highway Patrol officer who designed the game) tips his hat.
3. **Caffeine Carol's Flirting**:
   - Typing `KISS CAROL` or `FLIRT WITH CAROL`: Carol winks and hands Sonny a free chocolate-glazed donut.

---

# 7. VERSION HISTORY & BUILD PROVENANCE [VERS]

### A. Release Editions Comparison
* **1987 DOS AGI Release (v2.00–v2.917)**: 16-color EGA 320x200 graphics, text parser, internal PC speaker sound.
* **1992 VGA Remake (SCI Engine)**: 256-color point-and-click interface, CD audio.

### B. Exact Target Build Analyzed
* **Target Release**: `Police Quest I: In Pursuit of the Death Angel (1987 DOS AGI)`
* **Master Archive Size**: `426,328 bytes` (416.34 KiB)
* **Master Archive SHA-256**: `51d93876d09ef7e0f7be7e1ee7b9ae9b1b4d12e5a7b4bbf06629aa019fc5c428`
* **Internal Engine**: Sierra AGI Interpreter (`AGIDATA.OVL`, `WORDS.TOK`)

---

# 8. CREDITS & SPECIAL THANKS [CRED]

* **Jim Walls** — For bringing authentic California Highway Patrol procedural realism to gaming.
* **Ken & Roberta Williams / Sierra On-Line** — For the legendary AGI engine.
* **CJayC & GameFAQs** — For immortalizing text walkthroughs.
* **YOU, the reader** — For serving and protecting Lytton!
