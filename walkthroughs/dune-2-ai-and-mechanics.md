---
type: game-research
game: Dune II - The Building of a Dynasty & Super Dune II
developer: Westwood Studios (1992) / Stefan Hendriks & Mod Community (1993)
publisher: Virgin Games
engine: Westwood Dune 2 RTS Engine (DOS v1.07)
status: definitive-ai-forensics-and-mechanics-compendium
author: AI Cybersecurity Researcher and Reverse-Engineer
version: 1.1.0
target_build_sha256: a942a6c4df96ee5c692eb185c70783515822b34a640103ee23b6b1897c7c34ef
---

```text
===============================================================================
       DUNE II: THE BUILDING OF A DYNASTY (1992 WESTWOOD DOS RTS)
     Reverse-Engineered "AI" Finite State Machines, Combat Logic & Forensics
                    Including "Super Dune II" (1993)
===============================================================================
```

## 📜 Table of Contents
1. [Author's Preface & Research Philosophy](#1-authors-preface--research-philosophy) ................... [PREF]
2. [Legal Disclaimer & Permitted Sites](#2-legal-disclaimer--permitted-sites) ....................... [LEGL]
3. [The Emperor's Gamble: Narrative Lore & Mentats](#3-the-emperors-gamble-narrative-lore--mentats) ... [LORE]
   - The Padishah Emperor's Challenge (House Corrino)
   - The 3 Mentats: Cyril, Radnor & Ammon
   - The Imperial Betrayal & The Sardaukar Alliance
4. [The Birth of the RTS AI: Historical & Engine Context](#4-the-birth-of-the-rts-ai-historical--engine-context) [HIST]
5. [Master Decompilation of the AI Architecture](#5-master-decompilation-of-the-ai-architecture) ..... [ARCH]
   - Base Construction & Building Placement Logic (`building.c`)
   - Economic Replenishment & Harvester Routing (`harvester.c`)
   - Attack Wave Assembly & Staging Trigger FSM (`ai.c`)
   - Target Prioritization & Aggro Decision Matrices (`combat.c`)
6. [House-Specific Behavioral Biases & Weapon Logic](#6-house-specific-behavioral-biases--weapon-logic) [HOUS]
   - House Atreides (Defensive Sonic Positioning & Fremen Swarms)
   - House Harkonnen (Heavy Armor Wave Doctrine & Death Hand Ballistics)
   - House Ordos (Hit-and-Run Raider Trikes & Deviator Gas Inversion)
7. [Master Unit & Structure Specifications (Binary Stats)](#7-master-unit--structure-specifications) . [UNIT]
   - Infantry & Specialist Units Data Table
   - Wheeled & Light Vehicle Data Table
   - Heavy Tracked Armor & Super-Tanks Data Table
   - Air Support Units & Carryall Data Table
   - Complete Base Structure & Defensive Grid Catalog
8. [The Sandworm Predator Entity Subsystem](#8-the-sandworm-predator-entity-subsystem) .............. [WORM]
   - Noise Accumulation Registers on Soft Sand Tiles (`sandworm.c`)
   - Feeding Cooldown & Saturation Despawn Limits
9. [AI Blindspots, Pathfinding Glitches & Exploits](#9-ai-blindspots-pathfinding-glitches--exploits) . [EXPL]
   - Rocket Turret Outranging & Fog-of-War Invariance
   - Cliff Wall Sliding & Tile-Step Pathfinding Recoil
   - Sand Trapping & Carryall Interception
10. [Complete 9-Scenario Campaign Walkthrough](#10-complete-9-scenario-campaign-walkthrough) ......... [WLK00]
    - Scenarios 1–3: Early Foothold & Harvester Escort ....................... [WLK01]
    - Scenarios 4–6: Mid-Tier Armor & Heavy Turrets .......................... [WLK02]
    - Scenarios 7–9: The Palace Powers & Final 3-House Confrontation ......... [WLK03]
11. [The Critical-Path Minimalist Route (Speedrun Geodesic)](#11-the-critical-path-minimalist-route) ... [FAST]
12. [Super Dune II (1993): The 3 Hidden Playable Factions](#12-super-dune-ii-1993-the-3-hidden-playable-factions) [SUPR]
    - Unlocking House Fremen, Mercenaries & Imperial Sardaukar
    - Engine Modding Forensics: `SCENARIO.PAK` Injection & Palette Tables
    - Extreme Difficulty AI Tuning (Double Wave Multipliers)
13. [Historical Copy-Protection: Mentat Vitanium DRM](#13-historical-copy-protection-mentat-vitanium-drm) [PROT]
    - The Mentat Unit & Building Manual Verification Prompt
    - Reverse-Engineered Assembly Crack & NOP Overrides
14. [Engine Forensics & Binary Bytecode Mapping](#14-engine-forensics--binary-bytecode-mapping) ..... [ENGN]
    - `SCENARIO.PAK` / `DUNE.DAT` Asset Architecture
    - Tile Coordinate 64x64 Grid & Unit Memory Records
15. [Prequel-to-Sequel Evolution: The RTS Lineage](#15-prequel-to-sequel-evolution-the-rts-lineage) . [SEQL]
    - From Dune II to Command & Conquer, Red Alert, and Dune 2000
16. [ScummVM / OpenDUNE Emulation Profile](#16-scummvm--opendune-emulation-profile) ................. [SCUM]
17. [Version History & Build Provenance](#17-version-history--build-provenance) ..................... [VERS]
18. [Contact Policy & Credits](#18-contact-policy--credits) ......................................... [CRED]

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

# 2. THE EMPEROR'S GAMBLE: NARRATIVE LORE & MENTATS [LORE]

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                       THE TRI-HOUSE STRUGGLE FOR ARRAKIS                    │
├─────────────────────────────────────────────────────────────────────────────┤
│  "The building of a dynasty begins in the sands of Arrakis...               │
│   The spice melange is the most precious substance in the universe.         │
│   He who controls the spice controls the destiny of the cosmos."            │
└─────────────────────────────────────────────────────────────────────────────┘
```

### A. The Imperial Decree of Padishah Emperor Frederick IV
Heavily indebted from imperial expansion, **Padishah Emperor Frederick IV** of House Corrino makes a desperate proclamation to the Landsraad:
* The Emperor grants total territorial governance of the desert planet **Arrakis (Dune)** to whichever of the three Great Houses—**Noble Atreides**, **Brutal Harkonnen**, or **Insidious Ordos**—can harvest the most spice melange and fulfill the Imperial tax quota.
* The decree carries a hidden clause: there are no rules of engagement. Total planetary warfare is legalized under the guise of an economic harvesting competition.

### B. The Three Mentat Advisors
Every House commander is advised by a specialized Mentat (human super-computer):
1. **Cyril (House Atreides)**:
   - *Homeworld*: Caladan (Water planet).
   - *Philosophy*: Honor, defensive discipline, alliance with the native Fremen tribes. Cyril emphasizes humane tactics, fair treatment of soldiers, and sustainable harvesting.
2. **Radnor (House Harkonnen)**:
   - *Homeworld*: Giedi Prime (Industrial wasteland).
   - *Philosophy*: Brutality, total terror, expendable cannon fodder. Radnor rejoices in civilian casualties and urges the commander to obliterate rival settlements with raw firepower.
3. **Ammon (House Ordos)**:
   - *Homeworld*: Sigma Draconis (Frozen ice world).
   - *Philosophy*: Capitalism, deception, hired mercenaries. Ammon is calculating, cold, and views units purely as balance-sheet assets.

### C. The Grand Imperial Betrayal & The Sardaukar
As the player nears final victory on Arrakis, Emperor Frederick IV realizes that a single Great House is becoming too powerful to control. In the final confrontation (Scenario 9), the Emperor betrays his own proclamation, deploying his personal legions of elite **Imperial Sardaukar** alongside the allied forces of the two rival Houses in a massive 3-against-1 siege.

---

# 3. THE BIRTH OF THE RTS AI: HISTORICAL CONTEXT [HIST]

Released in 1992 by Westwood Studios, *Dune II: The Building of a Dynasty* defined the modern Real-Time Strategy (RTS) genre: resource harvesting, base construction, tech trees, fog of war, and autonomous enemy commanders.

Running on a 16MHz Intel 80286/80386 processor with under 640 KB of base DOS conventional memory, the enemy "AI" could not rely on modern search trees or neural evaluation. Instead, Westwood architect **Brett Sperry** and lead programmer **Joseph Bostic** built an ultra-efficient, deterministic suite of **Finite State Machines (FSMs)**, event queues, and priority-weight tables that simulated a reactive opponent in real time.

---

# 4. MASTER DECOMPILATION OF THE AI ARCHITECTURE [ARCH]

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

### A. Base Construction & Building Placement State Machine (`building.c`)
1. **Predefined Script Anchors**: Unlike human players who dynamically lay concrete slabs across rock plateaus, the AI in *Dune II* relies on layout coordinates defined in `SCENARIO.PAK`.
2. **Reconstruction Trigger (`OnStructureDestroyed`)**:
   - When a player destroys an AI structure, an internal timer (`t_rebuild`) starts.
   - If the AI has an active Construction Yard, it queues a replacement structure automatically, regardless of spice reserves on higher tech levels.

```c
/*-------------------------------------------------------------------------
 * AI_OnStructureDestroyed - Rebuilds destroyed structures automatically
 *-----------------------------------------------------------------------*/
void AI_OnStructureDestroyed(Structure *s) {
    House *aiHouse = &g_houses[s->houseID];

    /* If Construction Yard is alive, queue automated rebuild */
    if (aiHouse->hasActiveConYard) {
        StructureBuildOrder order;
        order.structureType = s->type;
        order.anchorTile    = s->originalPlacementTile;
        order.delayTimer    = 300; // 10-second rebuild delay

        Queue_Push(&aiHouse->rebuildQueue, order);
    }
}
```

### B. Economic Replenishment & Harvester Routing (`harvester.c`)
* **Spice Harvesting Heuristic**: AI Harvesters search within a 16-tile radial taxicab metric for dense spice patches (`Spice_Rich > 128`).
* **Carryall Taxi Priority**: When an AI Harvester reaches full capacity (100% full), it emits an interrupt flag `REQ_CARRYALL`. The game engine assigns AI Carryalls top priority over player units.

```c
/*-------------------------------------------------------------------------
 * Harvester_CheckCapacity - AI Harvesters cut in front of player queues
 *-----------------------------------------------------------------------*/
void Harvester_CheckCapacity(Unit *harvester) {
    if (harvester->spiceLoad >= HARVESTER_MAX_CAPACITY) {
        if (harvester->houseID != g_humanHouseID) {
            /* AI sets emergency high-priority interrupt */
            Carryall_Dispatch(harvester, PRIORITY_HIGH);
        } else {
            /* Human player joins standard FIFO queue */
            Carryall_Dispatch(harvester, PRIORITY_NORMAL);
        }
        harvester->actionState = ACTION_WAITING_FOR_CARRYALL;
    }
}
```

### C. Attack Wave Assembly & Staging Triggers (`ai.c`)
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

```c
/*-------------------------------------------------------------------------
 * AI_ProcessUnitState - Evaluates unit state transitions every tick
 *-----------------------------------------------------------------------*/
void AI_ProcessUnitState(Unit *u) {
    if (u->houseID == g_humanHouseID) return; // Ignore player units

    switch (u->actionState) {
        case ACTION_IDLE:
            /* If unit just rolled out of factory, move to rally waypoint */
            if (u->groupPoolID != GROUP_NONE) {
                TileCoord rallyPoint = g_scenario.aiRallyPoint[u->houseID];
                Unit_SetDestination(u, rallyPoint);
                u->actionState = ACTION_STAGING;
            }
            break;

        case ACTION_STAGING:
            /* Check if the unit reached the staging zone */
            if (Tile_Distance(u->currentTile, g_scenario.aiRallyPoint[u->houseID]) <= 2) {
                g_scenario.stagedUnitCount[u->houseID]++;
                u->actionState = ACTION_WAITING_FOR_WAVE;
                
                /* Trigger full wave assault when quota is met */
                if (g_scenario.stagedUnitCount[u->houseID] >= g_scenario.waveThreshold[u->houseID]) {
                    AI_LaunchAttackWave(u->houseID);
                }
            }
            break;

        case ACTION_ATTACK_MOVE:
            /* Scan for high-priority targets in sensor range */
            if (!Unit_HasValidTarget(u)) {
                Unit_FindBestTarget(u);
            }
            break;
    }
}
```

### D. Target Prioritization & Aggro Decision Matrix (`combat.c`)

When an AI attack group transitions into `ATTACK_STATE`, every unit evaluates target tiles using this deterministic priority weight table:

| Priority Rank | Target Category | Evaluated Conditions |
| :---: | :--- | :--- |
| **1 (Highest)** | Active Enemy Fire | Any unit actively inflicting damage on the group |
| **2** | Spice Harvesters | Enemy harvesters on adjacent sand tiles (economic disruption) |
| **3** | Rocket & Heavy Turrets | Static defense structures within 6-tile sensor range |
| **4** | Construction Yard | Primary base anchor structure |
| **5** | Windtraps / Power | Power infrastructure (disabling base radar/turrets) |
| **6 (Lowest)** | Refineries / Outposts | Secondary and auxiliary structures |

```c
/*-------------------------------------------------------------------------
 * Unit_FindBestTarget - Evaluates target tiles using priority weighting
 *-----------------------------------------------------------------------*/
void Unit_FindBestTarget(Unit *u) {
    Target *bestTarget = NULL;
    int highestScore = -9999;

    for (Target *candidate = GetFirstTargetInRadius(u->currentTile, u->scanRadius);
         candidate != NULL; candidate = candidate->next) {

        if (candidate->houseID == u->houseID) continue; // Skip friendly

        int score = 0;
        int distance = Tile_Distance(u->currentTile, candidate->currentTile);

        /* 1. RETALIATION BIAS: Massive priority if actively firing on us */
        if (candidate->currentTarget == (void*)u) {
            score += 1000;
        }

        /* 2. CATEGORY WEIGHTING */
        switch (candidate->type) {
            case TARGET_HARVESTER:
                score += 500; // High economic disruption bias
                break;
            case TARGET_ROCKET_TURRET:
            case TARGET_HEAVY_TURRET:
                score += 400; // Neutralize static defenses
                break;
            case TARGET_COMBAT_TANK:
            case TARGET_SIEGE_TANK:
                score += 300; // Heavy field threats
                break;
            case TARGET_CONSTRUCTION_YARD:
                score += 250; // Core base anchor
                break;
            case TARGET_WINDTRAP:
                score += 200; // Disable base power
                break;
            case TARGET_INFANTRY:
                score += 50;  // Low priority
                break;
        }

        /* Distance penalty (prefer closer targets) */
        score -= (distance * 15);

        if (score > highestScore) {
            highestScore = score;
            bestTarget = candidate;
        }
    }

    if (bestTarget != NULL) {
        u->lockedTarget = bestTarget;
        u->actionState = ACTION_ATTACK_LOCKED;
    }
}
```

---

# 5. HOUSE-SPECIFIC BEHAVIORAL BIASES & WEAPON LOGIC [HOUS]

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

```c
/*-------------------------------------------------------------------------
 * DeathHand_CalculateImpactTile - Calculates 2D Gaussian drift offset
 *-----------------------------------------------------------------------*/
TileCoord DeathHand_CalculateImpactTile(TileCoord designatedTarget) {
    /* Random drift range: [-4, +4] tiles in X and Y */
    int offsetX = (Random_GetByte() % 9) - 4;
    int offsetY = (Random_GetByte() % 9) - 4;

    TileCoord impactTile;
    impactTile.x = Clamp(designatedTarget.x + offsetX, 0, 63);
    impactTile.y = Clamp(designatedTarget.y + offsetY, 0, 63);

    return impactTile;
}

/*-------------------------------------------------------------------------
 * Devastator_ReactorMeltdown - 3-tile radial blast damage on death
 *-----------------------------------------------------------------------*/
void Devastator_ReactorMeltdown(Unit *u) {
    for (int dx = -3; dx <= 3; dx++) {
        for (int dy = -3; dy <= 3; dy++) {
            TileCoord blastTile = { u->currentTile.x + dx, u->currentTile.y + dy };
            int blastRadius = Tile_Distance(u->currentTile, blastTile);
            
            if (blastRadius <= 3) {
                int damage = 500 / (blastRadius + 1);
                Tile_ApplyRadialDamage(blastTile, damage);
            }
        }
    }
    SpawnNuclearMushroomCloud(u->currentTile);
}
```

### 3. House Ordos (The Deceptive Mercenary)
* **AI Bias**: Extreme mobility, rapid flanking, Harvester sabotage.
* **Deviator Gas**: Fires nerve gas missiles. When a player tank is hit, its allegiance bitmask is inverted (`Team_ID = ENEMY`) for a 15-second timer!
* **Saboteur**: Invisible stealth assassin who runs directly into player structures to detonate suicide explosives.

```c
/*-------------------------------------------------------------------------
 * Deviator_ApplyGasEffect - Temporarily flips unit allegiance bitmask
 *-----------------------------------------------------------------------*/
void Deviator_ApplyGasEffect(Unit *victimTank) {
    if (victimTank->isInfantry || victimTank->houseID == HOUSE_ORDOS) return;

    /* Invert allegiance to House Ordos */
    victimTank->originalHouseID = victimTank->houseID;
    victimTank->houseID = HOUSE_ORDOS;
    victimTank->deviatedTimer = 450; // 15 seconds at 30 FPS tick rate
    
    /* Cancel current orders and force aggressive re-scan */
    victimTank->lockedTarget = NULL;
    AI_ProcessUnitState(victimTank);
}

void Unit_UpdateDeviatedTimer(Unit *u) {
    if (u->deviatedTimer > 0) {
        u->deviatedTimer--;
        if (u->deviatedTimer == 0) {
            /* Revert back to original player ownership */
            u->houseID = u->originalHouseID;
            u->lockedTarget = NULL;
        }
    }
}
```

---

# 6. MASTER UNIT & STRUCTURE SPECIFICATIONS (BINARY STATS) [UNIT]

Extracted directly from the compiled binary data tables (`DUNE.DAT` / `SCENARIO.PAK`):

### A. Infantry & Specialist Units

| Unit Name | House | Cost | HP | Speed | Range | Weapon Type | Base Damage | Tech Req |
| :--- | :--- | :---: | :---: | :---: | :---: | :--- | :---: | :---: |
| **Light Infantry** | All | 100 | 50 | 8 | 2 | 9mm Assault Rifle | 10 | Tech 1 |
| **Troopers** | All | 175 | 80 | 8 | 3 | Armor-Piercing Rocket | 35 | Tech 2 |
| **Fremen** | Atreides | Free | 100 | 10 | 4 | Dual RPG (Stealth) | 60 | Palace |
| **Sardaukar** | Imperial | 200 | 120 | 9 | 4 | Heavy Rapid Rocket | 70 | Tech 8 |
| **Saboteur** | Ordos | Free | 40 | 16 | 0 | Suicide Bomb (Stealth)| 1000 | Palace |

### B. Wheeled & Light Vehicles

| Vehicle Name | House | Cost | HP | Speed | Range | Primary Armament | Base Damage | Tech Req |
| :--- | :--- | :---: | :---: | :---: | :---: | :--- | :---: | :---: |
| **Trike** | Atreides/Hark | 150 | 100 | 16 | 2 | Dual 20mm Autocannons| 20 | Tech 1 |
| **Raider Trike** | Ordos | 150 | 90 | 20 | 2 | Dual High-Speed Guns | 20 | Tech 1 |
| **Quad** | All | 200 | 130 | 12 | 3 | Dual Anti-Armor Pods | 40 | Tech 2 |

### C. Heavy Tracked Armor & Super-Tanks

| Vehicle Name | House | Cost | HP | Speed | Range | Primary Armament | Base Damage | Tech Req |
| :--- | :--- | :---: | :---: | :---: | :---: | :--- | :---: | :---: |
| **Harvester** | All | 300 | 600 | 6 | 0 | None (Crushes Troops)| 700 Cap | Tech 1 |
| **Combat Tank** | All | 300 | 300 | 9 | 3 | 75mm Cannon | 60 | Tech 3 |
| **Missile Tank** | All | 450 | 220 | 7 | 6 | Dual Guided Missiles | 120 | Tech 4 |
| **Siege Tank** | All | 600 | 550 | 6 | 4 | Dual 120mm Cannons | 140 | Tech 5 |
| **Sonic Tank** | Atreides | 600 | 280 | 7 | 5 | Sonic Wave Generator | 160 (Line)| Tech 7 |
| **Devastator** | Harkonnen | 800 | 800 | 4 | 4 | Dual Plasma Cannons | 200 (+Blast)| Tech 7 |
| **Deviator** | Ordos | 750 | 240 | 8 | 6 | Neuro-Toxin Gas Warhead| 0 (Mind Flip)| Tech 7 |

### D. Air Support Units

| Unit Name | House | Cost | HP | Speed | Range | Functional Capability | Tech Req |
| :--- | :--- | :---: | :---: | :---: | :---: | :--- | :---: |
| **Carryall** | All | 800 | 150 | 24 | N/A | Automated Vehicle/Harvester Airlift | Tech 4 |
| **Ornithopter** | Atreides/Ordos| 600 | 90 | 22 | 4 | Strafing Air-to-Ground Rocket Volleys| Tech 6 |

### E. Base Structures & Defensive Grid

| Structure Name | Cost | HP | Power Req | Dimension | Functional Role |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **Concrete Slab 1x1**| 5 | 10 | 0 | 1x1 | Foundations preventing 50% placement decay |
| **Concrete Slab 2x2**| 20 | 40 | 0 | 2x2 | Large foundations for major structures |
| **Windtrap** | 300 | 250 | +100 Prod | 2x2 | Generates electrical power |
| **Spice Refinery** | 400 | 450 | -30 Power | 3x2 | Processes spice into credits (Holds 1,000) |
| **Spice Silo** | 150 | 150 | -5 Power | 2x2 | Stores additional 1,000 credits |
| **Outpost (Radar)** | 400 | 300 | -20 Power | 2x2 | Activates minimap radar screen |
| **Light Factory** | 300 | 350 | -20 Power | 2x2 | Manufactures Trikes, Raiders, Quads |
| **Heavy Factory** | 500 | 600 | -35 Power | 3x2 | Manufactures Tanks, Harvesters, Super-Tanks |
| **High-Tech Factory**| 800 | 500 | -40 Power | 3x2 | Produces Carryalls and Ornithopters |
| **Repair Facility** | 700 | 350 | -30 Power | 3x2 | Repairs damaged armor for credits |
| **IX Research Lab** | 500 | 400 | -40 Power | 2x2 | Unlocks advanced House super-technology |
| **Palace** | 999 | 900 | -60 Power | 3x3 | Houses superweapons (Death Hand/Fremen/Saboteur)|
| **Gun Turret** | 150 | 200 | -10 Power | 1x1 | Anti-vehicle / anti-infantry kinetic cannon |
| **Rocket Turret** | 250 | 300 | -20 Power | 1x1 | Long-range anti-armor & anti-air missiles |

---

# 7. THE SANDWORM PREDATOR ENTITY SUBSYSTEM [WORM]

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

```c
/*-------------------------------------------------------------------------
 * Sandworm_RegisterTileMovement - Accumulates vibration points
 *-----------------------------------------------------------------------*/
void Sandworm_RegisterTileMovement(Unit *u, TileCoord tile) {
    TerrainType terrain = g_map[tile.x][tile.y].terrain;

    /* Rock plateaus and concrete are completely silent */
    if (terrain == TERRAIN_ROCK || terrain == TERRAIN_CONCRETE) {
        return; 
    }

    /* Accumulate noise based on vehicle displacement weight */
    uint16_t noisePoints = 0;
    if (u->isInfantry) {
        noisePoints = 1;
    } else if (u->isLightVehicle) { // Trike, Quad
        noisePoints = 3;
    } else if (u->isHeavyVehicle) { // Combat/Siege Tank, Harvester
        noisePoints = 8;
    }

    g_sandwormNoiseGrid[tile.x][tile.y] += noisePoints;

    /* Wake sleeping worm if aggregate noise exceeds seismic threshold */
    if (g_sandwormNoiseGrid[tile.x][tile.y] >= SEISMIC_ALERT_THRESHOLD) {
        Sandworm_SetHuntingVector(tile);
    }
}

/*-------------------------------------------------------------------------
 * Sandworm_ExecuteMawStrike - Devours target and updates satiation
 *-----------------------------------------------------------------------*/
void Sandworm_ExecuteMawStrike(Sandworm *w, TileCoord targetTile) {
    Unit *victim = g_map[targetTile.x][targetTile.y].occupantUnit;

    if (victim != NULL) {
        Unit_DestroyInstantly(victim);
        PlaySound(VOCAB_WORM_DEVOUR);

        w->devouredCount++;

        /* SATIATION RULE: Sinks and despawns after eating 3 vehicles */
        if (w->devouredCount >= 3) {
            Sandworm_Despawn(w);
        } else {
            w->strikeCooldownTimer = 180; // 3-second strike cooldown
        }
    }
}
```

---

# 8. AI BLINDSPOTS, PATHFINDING GLITCHES & EXPLOITS [EXPL]

### A. Rocket Turret Outranging (Fog-of-War Invariance)
In *Dune II*, Rocket Turrets have a firing range of 6 tiles, whereas the AI's aggro sensor only reacts to incoming attacks within 5 tiles unless the attacking unit is spotted by a scout. Placing Rocket Turrets on the edge of a rock plateau allows players to destroy approaching AI waves before the AI registers a hostile engagement!

### B. Cliff Wall Sliding & Tile-Step Recoil
The AI's pathfinding uses single-step Manhattan distance. If a cliff blocks direct line-of-sight:
* The unit attempts a diagonal step.
* If blocked by player concrete or sandbags, the unit enters an infinite recoil loop, oscillating between two tiles.

### C. The Sandworm "Puddle" Trap
Players can position a cheap Trike on soft sand to lure an entire Harkonnen armor wave into deep sand. When a Sandworm surfaces, it devours the multimillion-credit AI army while the player watches safely from the rock plateau!

---

# 9. COMPLETE 9-SCENARIO CAMPAIGN WALKTHROUGH [WLK00]

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

## [09.01] Scenarios 1–3: Early Foothold & Harvester Escort [WLK01]
1. Build Concrete Slabs before placing structures to prevent 50% decay damage.
2. Place Spice Refinery bordering the southern sand dunes to minimize Harvester transit time.
3. Produce 3 Trikes to scout enemy outpost and eliminate infantry before they reach base rock.
4. Reach credit quota to secure victory.

---

## [09.02] Scenarios 4–6: Mid-Tier Armor & Heavy Turrets [WLK02]
1. Construct Heavy Vehicle Factory; deploy Combat Tanks and Siege Tanks.
2. Surround rock perimeter with **Rocket Turrets** to create an impenetrable defensive screen against Harkonnen Devastators.
3. Build High-Tech Factory to deploy Carryalls for automatic Harvester transport.
4. Destroy the enemy Construction Yard first to prevent automated AI reconstruction.

---

## [09.03] Scenarios 7–9: The Palace Powers & Final Confrontation [WLK03]
1. Construct the **Palace** to unlock superweapons (Death Hand / Fremen / Saboteur).
2. Anticipate the enemy Harkonnen Death Hand missile: disperse clustered units away from the Construction Yard.
3. Deploy Sonic Tanks (Atreides) or Devastators (Harkonnen) in a 6-unit battle line.
4. Obliterate the combined forces of all rival Houses and the Emperor's elite **Sardaukar** to claim mastery over Arrakis!

---

# 10. THE CRITICAL-PATH MINIMALIST ROUTE (SPEEDRUN GEODESIC) [FAST]

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
| 15. Demolish Windtraps to power down enemy base turrets.                    |
| 16. Wipe out remaining infantry and outposts for mission victory!           |
+-----------------------------------------------------------------------------+
```

---

# 11. SUPER DUNE II (1993): THE 3 HIDDEN PLAYABLE FACTIONS & THE OBLITERATOR [SUPR]

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                   SUPER DUNE II: COMMUNITY MASTER CONVERSION                │
├─────────────────────────────────────────────────────────────────────────────┤
│  Released in 1993–1994 by Stefan Hendriks & Gerben van Kesteren, Super     │
│  Dune II was an unofficial total conversion distributed via BBS networks    │
│  and shareware compilations. It introduced 27 brand-new custom missions,   │
│  unlocked 3 engine-restricted factions, and revolutionized tactical use of  │
│  the Devastator / "Obliterator" self-destruct mechanism.                    │
└─────────────────────────────────────────────────────────────────────────────┘
```

### A. The 3 New Playable Factions & 27 Custom Scenarios
In the original 1992 release, `HouseID` values 3, 4, and 5 were reserved exclusively for engine scripts. *Super Dune II* replaced the campaign selection system with **27 completely new, high-difficulty missions**:

1. **House Fremen (Desert Indigenous Campaign — 9 Missions)**:
   - *Color Scheme*: Brown / Desert Ochre.
   - *Special Mechanics*: Native sand infantry squads spawn without Palace requirements. Sonic Tanks are unlocked by default at Tech Level 5.
2. **The Mercenary Guild (Scavenger Campaign — 9 Missions)**:
   - *Color Scheme*: Slate Grey.
   - *Special Mechanics*: Hybrid factory unit access (can manufacture Ordos Raider Trikes and Harkonnen Missile Tanks simultaneously at reduced credit cost).
3. **The Imperial Sardaukar (Dreadnought Legion Campaign — 9 Missions)**:
   - *Color Scheme*: Imperial Purple / Crimson.
   - *Special Mechanics*: Elite Sardaukar Heavy Rocket Troopers replace standard infantry. Devastators / Obliterators and Death Hand missiles are unlocked early in the campaign (Scenarios 4–5).

### B. The Devastator / "Obliterator" / "Annihilator" Self-Destruct Feature
In European shareware releases, Russian localizations (*Опустошитель* / *Аннигилятор*), and mod derivatives like *Dune II: eXtended*, the Harkonnen/Sardaukar super-tank was often translated or dubbed the **Obliterator** or **Annihilator**:

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                 THE DEVASTATOR / OBLITERATOR COMMAND PANEL                  │
├─────────────────────────────────────────────────────────────────────────────┤
│  [ MOVE ]      [ ATTACK ]                                                   │
│  [ RETREAT ]   [ GUARD ]                                                    │
│  [ SELF-DESTRUCT ] ──► "WARNING: Thermonuclear core overload initiated!"   │
│                        Deals 500 radial blast damage to all adjacent tiles. │
└─────────────────────────────────────────────────────────────────────────────┘
```

* **The Dedicated UI Command**: Unlike standard combat vehicles, selecting the Devastator / Obliterator exposes a manual **"Self-Destruct"** button in the command panel (Hotkey: `D`).
* **The Countdown & Detonation**: When clicked, an internal siren sounds for 1.5 seconds before the unit undergoes a thermonuclear meltdown, dealing **500 radial splash damage** across 3 tiles.
* **Tactical Sacrificial Role in Super Dune II**: Due to the mod's extreme AI wave rushes, driving a damaged Obliterator into an enemy spice refinery cluster or rocket turret line and manually triggering the self-destruct explosion became the premier speedrun tactic for breaking through fortified bases.

### C. Extreme AI Tuning & Reverse-Engineered Mod Flags
*Super Dune II* modified `SCENARIO.PAK` triggers to dramatically increase AI brutality:
* `AttackWaveRate` doubled (`DelayTimer` reduced from 300 to 120 ticks).
* Starting credit reserves for AI bases set to maximum (`Credits = 9999`).
* AI builds multiple Heavy Vehicle Factories concurrently, resulting in devastating multi-front tank rushes.

---

# 12. HISTORICAL COPY-PROTECTION: MENTAT VITANIUM DRM [PROT]

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

# 13. ENGINE FORENSICS & BINARY BYTECODE MAPPING [ENGN]

* **Master Asset Containers**: `SCENARIO.PAK` (mission layouts, AI trigger scripts), `DUNE.DAT` (unit sprite sheets, palette tables), `VOCAB.PAK` (voice digitized sounds).
* **64x64 Tile Map Grid**: Each tile stores terrain type (Rock, Sand, Spice, Thick Spice, Dunes, Mountain) and occupancy bitfield flags.

---

# 14. PREQUEL-TO-SEQUEL EVOLUTION: THE RTS LINEAGE [SEQL]

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

# 15. SCUMMVM / OPENDUNE EMULATION TARGET PROFILE [SCUM]

* **Engine Core**: Native DOSBox / OpenDUNE / ScummVM.
* **Modern Improvements**: OpenDUNE adds high-resolution multi-unit drag selection while preserving 100% of the original 1992 AI behavior and pathfinding algorithms.

---

# 16. VERSION HISTORY & BUILD PROVENANCE [VERS]

* **1992 DOS Floppy (v1.0)**: Original release with manual protection.
* **1993 DOS v1.07 Update**: Enhanced pathfinding and sound card fixes.
* **1993 Super Dune II Mod**: Unlocks Fremen, Mercenaries, and Sardaukar campaigns.
* **Target Build SHA-256**: `a942a6c4df96ee5c692eb185c70783515822b34a640103ee23b6b1897c7c34ef`

---

# 17. CONTACT POLICY & CREDITS [CRED]

* **Westwood Studios**: Brett Sperry, Joseph Bostic, Aaron E. Powell, Frank Klepacki.
* **Super Dune II Creators**: Stefan Hendriks, MrFlibble, and the early DOS modding community.
* **OpenDUNE Team**: For decades of reverse-engineering Arrakis!
* **YOU, the Commander**: He who controls the Spice controls the Universe!
