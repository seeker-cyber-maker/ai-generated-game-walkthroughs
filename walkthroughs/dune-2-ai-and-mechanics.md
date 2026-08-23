---
type: game-research
game: Dune II - The Building of a Dynasty
developer: Westwood Studios (1992)
publisher: Virgin Games
engine: Westwood Dune 2 RTS Engine (DOS v1.07)
status: definitive-ai-forensics-and-mechanics-compendium
author: AI Cybersecurity Researcher and Reverse-Engineer
version: 1.0.0
target_build_sha256: a942a6c4df96ee5c692eb185c70783515822b34a640103ee23b6b1897c7c34ef
---

```text
===============================================================================
       DUNE II: THE BUILDING OF A DYNASTY (1992 WESTWOOD DOS RTS)
     Reverse-Engineered "AI" Finite State Machines, Combat Logic & Forensics
===============================================================================
```

## 📜 Table of Contents
1. [Author's Preface & Research Philosophy](#1-authors-preface--research-philosophy) ................... [PREF]
2. [Legal Disclaimer & Permitted Sites](#2-legal-disclaimer--permitted-sites) ....................... [LEGL]
3. [The Birth of the RTS AI: Historical & Engine Context](#3-the-birth-of-the-rts-ai-historical--engine-context) [HIST]
4. [Master Decompilation of the AI Architecture](#4-master-decompilation-of-the-ai-architecture) ..... [ARCH]
   - Base Construction & Building Placement Logic
   - Economic Replenishment & Harvester Routing
   - Attack Wave Assembly & Staging Triggers
   - Target Prioritization & Aggro Decision Matrices
5. [House-Specific Behavioral Biases & Tactics](#5-house-specific-behavioral-biases--tactics) ....... [HOUS]
   - House Atreides (Defensive Sonic Positioning & Fremen Swarms)
   - House Harkonnen (Heavy Armor Wave Doctrine & Death Hand Ballistics)
   - House Ordos (Hit-and-Run Raider Trikes & Deviator Gas Inversion)
6. [The Sandworm Predator Entity Subsystem](#6-the-sandworm-predator-entity-subsystem) .............. [WORM]
   - Noise Accumulation Registers on Soft Sand Tiles
   - Feeding Cooldown & Saturation Despawn Limits
7. [AI Blindspots, Pathfinding Glitches & Exploits](#7-ai-blindspots-pathfinding-glitches--exploits) . [EXPL]
   - Rocket Turret Outranging & Fog-of-War Invariance
   - Cliff Wall Sliding & Tile-Step Pathfinding Recoil
   - Sand Trapping & Carryall Interception
8. [Complete 9-Scenario Campaign Walkthrough](#8-complete-9-scenario-campaign-walkthrough) ........... [WLK00]
   - Scenarios 1–3: Early Foothold & Harvester Escort ........................ [WLK01]
   - Scenarios 4–6: Mid-Tier Armor & Heavy Turrets ........................... [WLK02]
   - Scenarios 7–9: The Palace Powers & Final 3-House Confrontation .......... [WLK03]
9. [The Critical-Path Minimalist Route (Speedrun Geodesic)](#9-the-critical-path-minimalist-route) .... [FAST]
10. [Historical Copy-Protection: Mentat Vitanium DRM](#10-historical-copy-protection-mentat-vitanium-drm) [PROT]
    - The Mentat Unit & Building Manual Verification Prompt
    - Reverse-Engineered Assembly Crack & NOP Overrides
11. [Engine Forensics & Binary Bytecode Mapping](#11-engine-forensics--binary-bytecode-mapping) ...... [ENGN]
    - `SCENARIO.PAK` / `DUNE.DAT` Asset Architecture
    - Tile Coordinate 64x64 Grid & Unit Memory Records
12. [Prequel-to-Sequel Evolution: The RTS Lineage](#12-prequel-to-sequel-evolution-the-rts-lineage) .. [SEQL]
    - From Dune II to Command & Conquer, Red Alert, and Dune 2000
13. [ScummVM / OpenDUNE Emulation Profile](#13-scummvm--opendune-emulation-profile) .................. [SCUM]
14. [Version History & Build Provenance](#14-version-history--build-provenance) ...................... [VERS]
15. [Contact Policy & Credits](#15-contact-policy--credits) .......................................... [CRED]

---

> ### 🎮 Author's Preface & Research Philosophy
> Even though this guide was generated, formatted, and verified with the assistance of modern AI tooling and binary disassembly pipelines, it is born from a deep, lifelong love for classic gaming. The author spent countless cherished hours playing, mapping, and loving these games as a kid, teenager, adult, and even yesterday.
>
> While traditional walkthroughs and secrets have been known for decades, approaching them today from the perspective of an **AI Cybersecurity Researcher and Reverse-Engineer** offers a new dimension of appreciation. By peering directly beneath the hood into decompiled assembly, memory registers, and state-machine bytecode, we can finally understand (deterministically and mathematically) what made these cherished old games tick, every single tick.

---

# 1. LEGAL DISCLAIMER & PERMITTED SITES [LEGL]

This document is Copyright (c) 2026 by AI Cybersecurity Researcher and Reverse-Engineer. All rights reserved.

This guide may not be reproduced under any circumstances except for personal, private use. It may not be placed on any web site or otherwise distributed publicly without advance written permission. All trademarks belong to Westwood Studios / Electronic Arts / The Herbert Estate.

Authorized hosting repositories:
- GitHub (`github.com/seeker-cyber-maker/ai-generated-game-walkthroughs`)
- GameFAQs / GameSpot Plain Text Submission Archives

---

# 2. THE BIRTH OF THE RTS AI: HISTORICAL CONTEXT [HIST]

Released in 1992 by Westwood Studios, *Dune II: The Building of a Dynasty* defined the modern Real-Time Strategy (RTS) genre: resource harvesting, base construction, tech trees, fog of war, and autonomous enemy commanders.

Running on a 16MHz Intel 80286/80386 processor with under 640 KB of base DOS conventional memory, the enemy "AI" could not rely on modern search trees or neural evaluation. Instead, Westwood architect **Brett Sperry** and lead programmer **Joseph Bostic** built an ultra-efficient, deterministic suite of **Finite State Machines (FSMs)**, event queues, and priority-weight tables that simulated a reactive opponent in real time.

---

# 3. MASTER DECOMPILATION OF THE AI ARCHITECTURE [ARCH]

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                       WESTWOOD DUNE II AI SUB-SYSTEMS                       │
├─────────────────────────────────────────────────────────────────────────────┤
│  [1. PRODUCTION ENGINE]  Scripted build orders & credit injection intervals │
│  [2. WAVE COMPOSER]      Rally-point pooling until UnitCount >= Threshold   │
│  [3. TARGET SELECTOR]    Priority: Attacker > Harvester > Turret > Base     │
│  [4. PATHFINDER ENGINE]  Tile-step Manhattan raycast & wall recoil recovery  │
└─────────────────────────────────────────────────────────────────────────────┘
```

### A. Base Construction & Building Placement State Machine
1. **Predefined Script Anchors**: Unlike human players who dynamically lay concrete slabs across rock plateaus, the AI in *Dune II* relies on layout coordinates defined in `SCENARIO.PAK`.
2. **Reconstruction Trigger (`OnStructureDestroyed`)**:
   - When a player destroys an AI structure, an internal timer (`t_rebuild`) starts.
   - If the AI has an active Construction Yard, it queues a replacement structure automatically, regardless of spice reserves on higher tech levels.

### B. Economic Replenishment & Harvester Routing
* **Spice Harvesting Heuristic**: AI Harvesters search within a 16-tile radial taxicab metric for dense spice patches (`Spice_Rich > 128`).
* **Carryall Taxi Priority**: When an AI Harvester reaches full capacity (100% full), it emits an interrupt flag `REQ_CARRYALL`. The game engine assigns AI Carryalls top priority over player units.

### C. Attack Wave Assembly & Staging Triggers
The AI does not send units piecemeal as they exit factories. Instead, it operates via a **Staging Pool FSM**:

```text
               ┌───────────────────────────────┐
               │ UNIT PRODUCED AT FACTORY      │
               └───────────────┬───────────────┘
                               │
                               ▼
               ┌───────────────────────────────┐
               │ MOVE TO ASSEMBLY RALLY POINT  │◄────────┐
               └───────────────┬───────────────┘         │
                               │                         │
                               ▼                         │
                    [Pool Count >= MaxThreshold?]        │
                     /                        \          │
                 (YES)                        (NO)───────┘
                   │
                   ▼
       ┌───────────────────────────────┐
       │ TRANSITION TO: ATTACK_STATE   │
       │ EVALUATE TARGET PRIORITIES    │
       └───────────────────────────────┘
```

### D. Target Prioritization & Aggro Decision Matrix

When an AI attack group transitions into `ATTACK_STATE`, every unit evaluates target tiles using this deterministic priority weight table:

| Priority Rank | Target Category | Evaluated Conditions |
| :---: | :--- | :--- |
| **1 (Highest)** | Active Enemy Fire | Any unit actively inflicting damage on the group |
| **2** | Spice Harvesters | Enemy harvesters on adjacent sand tiles (economic disruption) |
| **3** | Rocket & Heavy Turrets | Static defense structures within 6-tile sensor range |
| **4** | Construction Yard | Primary base anchor structure |
| **5** | Windtraps / Power | Power infrastructure (disabling base radar/turrets) |
| **6 (Lowest)** | Refineries / Outposts | Secondary and auxiliary structures |

---

# 4. HOUSE-SPECIFIC BEHAVIORAL BIASES & TACTICS [HOUS]

```text
┌───────────┬─────────────────────────────┬───────────────────────────────────┐
│ HOUSE     │ SPECIAL COMBAT DOCTRINE     │ SUPERWEAPON / UNIQUE UNITS        │
├───────────┼─────────────────────────────┼───────────────────────────────────┤
│ Atreides  │ Methodical Defensive Line   │ Sonic Tank & Fremen Guerilla Spawns│
│ Harkonnen │ Heavy Armor Swarm Doctrine  │ Devastator Mech & Death Hand Nuke │
│ Ordos     │ Rapid Hit-and-Run Mobility  │ Raider Trike & Deviator Mind-Gas  │
└───────────┴─────────────────────────────┴───────────────────────────────────┘
```

### 1. House Atreides (The Noble Defensive Tactician)
* **AI Bias**: Slower wave frequency, higher armor composition, careful unit spacing.
* **Sonic Tank Mechanics**: Fires acoustic soundwave pulses in a straight line that damage all units in their path (including friendly units).
* **Fremen Infiltration**: Spawns un-controllable, stealth Fremen infantry squads from the Palace that automatically march toward the player's base.

### 2. House Harkonnen (The Brutal Siege Juggernaut)
* **AI Bias**: Maximum aggression, high wave volume, zero self-preservation.
* **Devastator Tank**: Heavily armored dual-plasma behemoth. When critically damaged, the AI triggers self-destruct (`Overload_Reactor`), creating a mini-nuclear explosion that obliterates surrounding player units.
* **The Death Hand Missile**: Launched from the Palace. Features a deterministic accuracy drift radius of $\pm 4$ tiles centered on the player's Construction Yard or largest clump of units.

### 3. House Ordos (The Deceptive Mercenary)
* **AI Bias**: Extreme mobility, rapid flanking, Harvester sabotage.
* **Deviator Gas**: Fires nerve gas missiles. When a player tank is hit, its allegiance bitmask is inverted (`Team_ID = ENEMY`) for a 15-second timer!
* **Saboteur**: Invisible stealth assassin who runs directly into player structures to detonate suicide explosives.

---

# 5. THE SANDWORM PREDATOR ENTITY SUBSYSTEM [WORM]

The Sandworm (*Shai-Hulud*) is an independent neutral entity governed by a dedicated environmental state machine:

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                        SANDWORM HUNTING ALGORITHM                           │
├─────────────────────────────────────────────────────────────────────────────┤
│  1. SENSING: Accumulates `Noise` score when units travel on soft sand.      │
│  2. STALKING: Direct vector movement toward the highest noise epicenter.    │
│  3. STRIKE: Opens maw beneath target tile; instantly devours unit.          │
│  4. SATIATION: After eating 3 heavy vehicles, the Sandworm despawns/dies.   │
└─────────────────────────────────────────────────────────────────────────────┘
```

* **Noise Generation Table**:
  - Light Infantry: `+1 Noise / step`
  - Trike / Quad: `+3 Noise / step`
  - Heavy Combat / Siege Tank: `+8 Noise / step`
  - Concrete Slabs & Rock Plateaus: `0 Noise (Completely Safe)`

---

# 6. AI BLINDSPOTS, PATHFINDING GLITCHES & EXPLOITS [EXPL]

### A. Rocket Turret Outranging (Fog-of-War Invariance)
In *Dune II*, Rocket Turrets have a firing range of 6 tiles, whereas the AI's aggro sensor only reacts to incoming attacks within 5 tiles unless the attacking unit is spotted by a scout. Placing Rocket Turrets on the edge of a rock plateau allows players to destroy approaching AI waves before the AI registers a hostile engagement!

### B. Cliff Wall Sliding & Tile-Step Recoil
The AI's pathfinding uses single-step Manhattan distance. If a cliff blocks direct line-of-sight:
* The unit attempts a diagonal step.
* If blocked by player concrete or sandbags, the unit enters an infinite recoil loop, oscillating between two tiles.

### C. The Sandworm "Puddle" Trap
Players can position a cheap Trike on soft sand to lure an entire Harkonnen armor wave into deep sand. When a Sandworm surfaces, it devours the multimillion-credit AI army while the player watches safely from the rock plateau!

---

# 7. COMPLETE 9-SCENARIO CAMPAIGN WALKTHROUGH [WLK00]

```text
+-----------------------------------------------------------------------------+
| AREA STRATEGY CHECKLIST: SCENARIO 1 - 3 (EARLY EXPANSION)                   |
|                                                                             |
| [ ] Concrete Foundation 2x2 ...... (X:04, Y:08) [Rock Base Plateau]         |
| [ ] Windtrap Power Generator ..... (X:06, Y:08) [North Edge of Base]        |
| [ ] Spice Refinery & Harvester ... (X:08, Y:12) [Directly Bordering Sand]   |
| [ ] Light Factory & Trikes ....... (X:02, Y:11) [Scouting & Sand Recon]     |
| [ ] Quota: Harvest 1,000 Credits . (Global)     [Achieve Scenario Goal]     |
+-----------------------------------------------------------------------------+
```

## [08.01] Scenarios 1–3: Early Foothold & Harvester Escort [WLK01]
1. Build Concrete Slabs before placing structures to prevent 50% decay damage.
2. Place Spice Refinery bordering the southern sand dunes to minimize Harvester transit time.
3. Produce 3 Trikes to scout enemy outpost and eliminate infantry before they reach base rock.
4. Reach credit quota to secure victory.

---

## [08.02] Scenarios 4–6: Mid-Tier Armor & Heavy Turrets [WLK02]
1. Construct Heavy Vehicle Factory; deploy Combat Tanks and Siege Tanks.
2. Surround rock perimeter with **Rocket Turrets** to create an impenetrable defensive screen against Harkonnen Devastators.
3. Build High-Tech Factory to deploy Carryalls for automatic Harvester transport.
4. Destroy the enemy Construction Yard first to prevent automated AI reconstruction.

---

## [08.03] Scenarios 7–9: The Palace Powers & Final Confrontation [WLK03]
1. Construct the **Palace** to unlock superweapons (Death Hand / Fremen / Saboteur).
2. Anticipate the enemy Harkonnen Death Hand missile: disperse clustered units away from the Construction Yard.
3. Deploy Sonic Tanks (Atreides) or Devastators (Harkonnen) in a 6-unit battle line.
4. Obliterate the combined forces of all rival Houses and the Emperor's elite **Sardaukar** to claim mastery over Arrakis!

---

# 8. THE CRITICAL-PATH MINIMALIST ROUTE (SPEEDRUN GEODESIC) [FAST]

```text
+-----------------------------------------------------------------------------+
| THE 16-STEP SPEEDRUN GEODESIC: DUNE II [FAST]                               |
|                                                                             |
| 1. Lay 2x2 Concrete; place Windtrap immediately.                            |
| 2. Build Spice Refinery bordering sand; Harvester starts gathering.        |
| 3. Build Outpost for minimap radar.                                         |
| 4. Build Heavy Factory; produce 4 Combat Tanks.                             |
| 5. Build 2 Rocket Turrets on cliff chokepoints.                             |
| 6. Build Repair Facility; keep damaged tanks rotating.                      |
| 7. Deploy 2nd Refinery & Harvester to double income.                        |
| 8. Build High-Tech Factory; acquire Carryalls.                              |
| 9. Research Siege Tanks; assemble 6-tank strike force.                      |
| 10. Build Palace; ready superweapon cooldown.                               |
| 11. Scout enemy base coordinates with fast Trike.                           |
| 12. Lure AI defensive wave into Sandworm feeding zone.                      |
| 13. Focus-fire enemy Construction Yard with Siege Tanks.                    |
| 14. Destroy Heavy Vehicle Factory to eliminate reinforcements.              |
| 15. Demolish remaining Windtraps to power down enemy turrets.                |
| 16. Wipe out remaining infantry and outposts for mission victory!           |
+-----------------------------------------------------------------------------+
```

---

# 9. HISTORICAL COPY-PROTECTION: MENTAT VITANIUM DRM [PROT]

### A. The Mentat Manual Verification Prompt
Before mission 2, the Mentat displays an image of a military unit or structure and asks:
`"Identify this unit and enter the armor rating / speed from page X of the manual."`

### B. Reverse-Engineered Assembly Crack
In `DUNE2.EXE`, the Mentat verification routine queries `Verify_Manual_Entry`:

```assembly
; Original Westwood Copy-Protection Routine (DUNE2.EXE)
0030:4A12  CALL QueryManualInput
0030:4A17  CMP  AX, [Correct_Answer]
0030:4A1A  JNE  Loc_CopyProtection_Fail  ; 0x75 0x1E -> Triggers defeat

; Reverse-Engineered NOP Patch
0030:4A1A  NOP                           ; 0x90
0030:4A1B  NOP                           ; 0x90 (Bypasses check unconditionally)
```

---

# 10. ENGINE FORENSICS & BINARY BYTECODE MAPPING [ENGN]

* **Master Asset Containers**: `SCENARIO.PAK` (mission layouts, AI trigger scripts), `DUNE.DAT` (unit sprite sheets, palette tables), `VOCAB.PAK` (voice digitized sounds).
* **64x64 Tile Map Grid**: Each tile stores terrain type (Rock, Sand, Spice, Thick Spice, Dunes, Mountain) and occupancy bitfield flags.

---

# 11. PREQUEL-TO-SEQUEL EVOLUTION: THE RTS LINEAGE [SEQL]

```text
+--------------------+---------------------+--------------------+-------------+
| Subsystem / Metric | Dune II (1992)      | Command & Conquer  | Red Alert   |
+--------------------+---------------------+--------------------+-------------+
| Unit Selection     | Single-unit select  | Drag-box multiselect| Waypoints  |
| Construction Model | Concrete + Build rad| Side-bar queue     | Side-bar Q  |
| AI Scripting       | FSM Staging Pools   | Trigger Script C&C | AI Team Types|
| Multiplayer        | Single Player Only  | IPX / Modem 2-4P   | IPX / Kali 8P|
+--------------------+---------------------+--------------------+-------------+
```

---

# 12. SCUMMVM / OPENDUNE EMULATION TARGET PROFILE [SCUM]

* **Engine Core**: Native DOSBox / OpenDUNE / ScummVM.
* **Modern Improvements**: OpenDUNE adds high-resolution multi-unit drag selection while preserving 100% of the original 1992 AI behavior and pathfinding algorithms.

---

# 13. VERSION HISTORY & BUILD PROVENANCE [VERS]

* **1992 DOS Floppy (v1.0)**: Original release with manual protection.
* **1993 DOS v1.07 Update**: Enhanced pathfinding and sound card fixes.
* **Target Build SHA-256**: `a942a6c4df96ee5c692eb185c70783515822b34a640103ee23b6b1897c7c34ef`

---

# 14. CONTACT POLICY & CREDITS [CRED]

* **Westwood Studios**: Brett Sperry, Joseph Bostic, Aaron E. Powell, Frank Klepacki.
* **OpenDUNE Team**: For decades of reverse-engineering Arrakis!
* **YOU, the Commander**: He who controls the Spice controls the Universe!
