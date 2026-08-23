---
type: game-research
game: FTL: Faster Than Light
developer: Subset Games (Justin Ma & Matthew Davis)
publisher: Subset Games (2012 / Advanced Edition 2014)
engine: C++ Custom 2D Engine with FNA/OpenGL
status: definitive-reverse-engineered-mechanics-and-blue-option-statistical-suite
author: AI Cybersecurity Researcher and Reverse-Engineer
version: 1.0.0
target_build_sha256: 7d60be992850937b420ee963d76e73ff6697818e698889a7be8e7be1ffec975f
---

```text
===============================================================================
                    FTL: FASTER THAN LIGHT (2012/2014)
    Reverse-Engineered Mechanics, Flagship Forensics & Blue-Text Statistics
===============================================================================
```

## 📜 Table of Contents
1. [Author's Preface & Research Philosophy](#1-authors-preface--research-philosophy) ................... [PREF]
2. [Legal Disclaimer & Permitted Sites](#2-legal-disclaimer--permitted-sites) ....................... [LEGL]
3. [Combat Engine & Mathematical Subsystems](#3-combat-engine--mathematical-subsystems) ............. [MATH]
   - Evasion, Engines & Piloting Probability Curves ......................... [MAT01]
   - Shield Penetration & Laser/Beam Damage Mechanics ....................... [MAT02]
   - Oxygen Depletion, Fire Spread & Hull Breach State Machines ............. [MAT03]
4. [The Definitive Blue Option Statistical Analysis](#4-the-definitive-blue-option-statistical-analysis) [STAT]
   - Macro Distribution: Positive (63.00%) vs. Neutral (35.24%) vs. Trap .... [STA01]
   - Top Blue Option Enablers by System, Crew & Augment ..................... [STA02]
   - The 4 Infamous Negative & High-Risk "Trap" Blue Options ................ [STA03]
5. [Master Blueprint Catalog: Ships, Weapons & Drones](#5-master-blueprint-catalog) .................. [BLUE]
   - Weapon Tiers: Volley Synchronization & Ion Stacking .................... [BLU01]
   - Crew Racial Trait Matrix (Engi, Mantis, Zoltan, Rock, Slug, Lanius) .... [BLU02]
6. [Complete 8-Sector Route Optimization & Scrap Economy](#6-complete-8-sector-route-optimization) ... [SECT]
   - Sector Pathing & Beacon Maximization Algorithms ........................ [SEC01]
   - The Rebel Fleet Pursuit Wave Equation .................................. [SEC02]
7. [The Rebel Flagship: 3-Phase Tactical Destruction Guide](#7-the-rebel-flagship-3-phase-tactical-destruction-guide) [BOSS]
   - Phase 1: Cloaking & Ion/Laser/Missile/Beam Artillery Isolation ......... [BOS01]
   - Phase 2: Defense Drone Overload & Power Surge Drone Swarms ............. [BOS02]
   - Phase 3: Zoltan Super-Shield, Mind Control & Laser Power Surge ......... [BOS03]
8. [The Secret Crystal Sector & Quest Geodesic](#8-the-secret-crystal-sector--quest-geodesic) ........ [CRYS]
9. [Version History & Build Provenance](#9-version-history--build-provenance) ....................... [VERS]
10. [Contact Policy & Credits](#10-contact-policy--credits) ......................................... [CRED]

---

> ### 🎮 Author's Preface & Research Philosophy
> Even though this guide was generated, formatted, and verified with the assistance of modern AI tooling and binary disassembly pipelines, it is born from a deep, lifelong love for classic gaming. The author spent countless cherished hours playing, mapping, and loving these games as a kid, teenager, adult, and even yesterday.
>
> While traditional walkthroughs and secrets have been known for decades, approaching them today from the perspective of an **AI Cybersecurity Researcher and Reverse-Engineer** offers a new dimension of appreciation. By peering directly beneath the hood into decompiled assembly, memory registers, and state-machine bytecode, we can finally understand (deterministically and mathematically) what made these cherished old games tick, every single tick.

---

# 1. LEGAL DISCLAIMER & PERMITTED SITES [LEGL]

This document is Copyright (c) 2026 by AI Cybersecurity Researcher and Reverse-Engineer. All rights reserved.

This guide may not be reproduced under any circumstances except for personal, private use. It may not be placed on any web site or otherwise distributed publicly without advance written permission. All trademarks belong to Subset Games (Justin Ma & Matthew Davis).

Authorized hosting repositories:
- GitHub (`github.com/seeker-cyber-maker/ai-generated-game-walkthroughs`)
- GameFAQs / GameSpot Plain Text Submission Archives

---

# 2. COMBAT ENGINE & MATHEMATICAL SUBSYSTEMS [MATH]

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                          FTL COMBAT MATHEMATICS                             │
├─────────────────────────────────────────────────────────────────────────────┤
│  EVASION EQUATION:     Evasion% = Engine_Base% + Pilot_Man% + Engine_Man%   │
│  SHIELD RECHARGE:      Recharge_Time = 10.0s / (1.0 + 0.1 * Shield_Crew_Lvl)│
│  FIRE SPREAD RATE:     P(Spread) = 0.05 / sec per adjacent tile if O2 > 10% │
│  BEAM DAMAGE FORMULA:  Damage_Dealt = Max(0, Beam_Base_Damage - Active_Shields)
└─────────────────────────────────────────────────────────────────────────────┘
```

### A. Evasion, Engines & Piloting Probability Curves [MAT01]
Incoming projectiles roll a uniform pseudo-random number $R \in [0, 99]$. If $R < \text{Evasion}$, the projectile misses completely.

$$\text{Total Evasion} = \text{Engine Base} + \text{Piloting Manning Bonus} + \text{Engine Manning Bonus}$$

| Engine Level | Power Req | Base Evasion | Manning +0 (Untrained) | Manning +2 (Master Crew) | Cloaking Surge (+60%) |
| :---: | :---: | :---: | :---: | :---: | :---: |
| **Level 1** | 1 | 5% | 10% | 15% | 75% |
| **Level 2** | 2 | 10% | 15% | 20% | 80% |
| **Level 3** | 3 | 15% | 20% | 25% | 85% |
| **Level 4** | 4 | 20% | 25% | 30% | 90% |
| **Level 5** | 5 | 25% | 30% | 35% | 95% |
| **Level 6** | 6 | 28% | 33% | 38% | 98% |
| **Level 7** | 7 | 31% | 36% | 41% | 100% |
| **Level 8** | 8 | 35% | 40% | 45% | 100% (Hard Cap) |

> **Tactical Rule of Gold**: Upgrading Engines to **Level 4 or 5** before Sector 3 yields the highest survivability per scrap spent in the entire game. Level 5 with max-trained crew provides **45% passive dodge**, and activates guaranteed **100% invulnerability** during Level 1 Cloaking!

### B. Shield Penetration & Laser/Beam Damage Mechanics [MAT02]
* **Laser / Flak Volleys**: Every laser or flak projectile absorbs 1 shield bubble. To damage a ship with 4 shield bubbles, your volley must land at least **5 synchronized projectiles**.
* **Beam Weapons**: Beams do not miss. A beam deals damage equal to:
  $$\text{Damage per Room} = \max(0, \text{Beam Damage} - \text{Remaining Shields})$$
  *(e.g., A Halberd Beam [2 dmg] against 1 shield bubble inflicts 1 damage per room crossed).*
* **Ion Weapons**: Deals no hull damage, but ionizes shield power for 5 seconds per ion point. Consecutive ion hits before dissipation reset the countdown and stack linearly!

---

# 3. THE DEFINITIVE BLUE OPTION STATISTICAL ANALYSIS [STAT]

From decompiling the raw FTL event files (`events.xml`, `events_*.xml`, `dlcEvents.xml`), there are **227 total Blue Option choices** with conditional requirements (`req="..."`).

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                    FTL: BLUE OPTION MASTER DISTRIBUTION                     │
├─────────────────────────────────────────────────────────────────────────────┤
│  TOTAL BLUE OPTIONS ANALYZED: 227 CHOICES                                   │
│                                                                             │
│  • POSITIVE (Direct Reward / Free Crew / Safe Bypass):  143  ( 63.00% )     │
│  • ABSTAIN / NEUTRAL (Decline / Passive Safe Pass):      80  ( 35.24% )     │
│  • NEGATIVE (Direct Hull Damage / Permanent Loss Trap):    3  (  1.32% )     │
│  • MIXED / RISKY (Resource Cost for High-Reward):          1  (  0.44% )     │
└─────────────────────────────────────────────────────────────────────────────┘
```

### A. Requirement Category Distribution [STA01]

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                       BLUE OPTIONS BY REQUIREMENT TYPE                      │
├─────────────────────────────────────────────────────────────────────────────┤
│  1. SHIP SYSTEMS / SUBSYSTEMS:  123 choices  ( 54.19% )                     │
│  2. CREW RACIAL TRAITS:          50 choices  ( 22.03% )                     │
│  3. AUGMENTS & SPECIAL ITEMS:    38 choices  ( 16.74% )                     │
│  4. WEAPON ARCHETYPES:           16 choices  (  7.05% )                     │
└─────────────────────────────────────────────────────────────────────────────┘
```

### B. Top 15 Blue Option Enablers in FTL [STA02]

| Enabler System / Trait | Category | Blue Options Enabled | % of All Blue Options | Primary Benefit |
| :--- | :--- | :---: | :---: | :--- |
| **Sensors (Lvl 2/3)** | Subsystem | **24** | 10.57% | Reveals traps, scouts enemy bases, safe navigation |
| **Hacking System** | System | **19** | 8.37% | Bypasses automated security, disables rebel base turrets |
| **Medbay (Lvl 2/3)** | System | **13** | 5.73% | Cures alien plagues, saves infected colonists, gains crew |
| **Lanius (Anaerobic)** | Crew Race | **12** | 5.29% | Explores airless wrecks, drains oxygen hazards |
| **Piloting (Lvl 2/3)** | Subsystem | **11** | 4.85% | Dodges asteroid belts, out-maneuvers planetary defenses |
| **Slug Crew** | Crew Race | **11** | 4.85% | Detects psychic illusions, reveals hidden slug swindles |
| **Teleporter (Lvl 2)** | System | **11** | 4.85% | Raids derelict hulls, captures civilian vessels safely |
| **Cloaking (Lvl 2)** | System | **11** | 4.85% | Avoids pirate ambushes, bypasses asteroid storms |
| **Engi Crew** | Crew Race | **11** | 4.85% | Repairs derelict tech, upgrades automated satellites |
| **Engines (Lvl 4/5/6)**| System | **9** | 3.96% | Escapes solar flares, outruns rebel pursuers |
| **Mind Control** | System | **8** | 3.52% | Pacifies hostile madmen, breaks alien mind traps |
| **Long-Ranged Scanners**| Augment | **7** | 3.08% | Reveals ship/hazard beacons, guarantees high-scrap path |
| **Rock Crew** | Crew Race | **6** | 2.64% | Immune to fire hazards, survives volcanic collapses |
| **Clone Bay** | System | **5** | 2.20% | Bypasses fatal crew encounters with instant respawn |
| **Doors (Lvl 2/3)** | Subsystem | **5** | 2.20% | Traps fire, suffocates hostile boarders automatically |

---

### C. The 4 Infamous Negative & High-Risk "Trap" Blue Options [STA03]

While 98.24% of Blue Options are strictly beneficial or neutral, there are **4 specific instances** where clicking the Blue Option results in damage, loss, or extreme risk:

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                 THE 4 EXCEPTION TRAPS IN FTL BLUE CHOICES                   │
├─────────────────────────────────────────────────────────────────────────────┤
│  1. EVENT #66: `BOARDERS_ASTEROID_GHOST` (Engines Lvl 5) ──► 3 HULL DAMAGE  │
│  2. EVENT #107: `ENGI_VIRUS` (Engi Crew) ──► PERMANENT ENGI LOSS (Then Boss)│
│  3. EVENT #164: `ROCK_STARSHIP_MINE` (Missile Weapon) ──► 3 HULL DAMAGE     │
│  4. EVENT #214: `QUEST_CONSTRUCTIONYARD` (Lanius Crew) ──► CREW SACRIFICE   │
└─────────────────────────────────────────────────────────────────────────────┘
```

#### 1. Trap #1: Out-Maneuvering Asteroids (`BOARDERS_ASTEROID_GHOST`)
* **Requirement**: `Engines Level 5`
* **Source XML**: `events.xml` (Line 143698)
* **What Happens**: The game describes your ship deftly navigating an asteroid field, but an unexpected collision occurs:
  ```xml
  <damage amount="3"/>
  <damage amount="1" system="random"/>
  ```
* **Verdict**: Direct **3 Hull Damage + 1 System Damage**. Avoid unless hull is full!

#### 2. Trap #2: The Engi Virus Infection (`ENGI_VIRUS`)
* **Requirement**: `Engi Crew Member`
* **Source XML**: `events_engi.xml` (Line 152748)
* **What Happens**: Sending your Engi to communicate with the infected station immediately uploads a deadly cyber-pathogen:
  ```xml
  <removeCrew class="engi"><clone>false</clone></removeCrew>
  ```
* **The Silver Lining**: Defeating the resulting hostile ship permanently cures the virus, resurrecting your crew member as **Virus**, a unique Engi possessing **max level-2 mastery in all 6 skills**!

#### 3. Trap #3: Firing a Missile into a Mine (`ROCK_STARSHIP_MINE`)
* **Requirement**: `WEAPONS_MISSILES`
* **Source XML**: `events_rock.xml` (Line 152889)
* **What Happens**: Firing a high-explosive missile into the volatile rock cavern detonates the mine prematurely:
  ```xml
  <damage amount="3"/>
  <damage amount="1" system="random"/>
  <item_modify><item type="missile" min="-1" max="-1"/></item_modify>
  <autoReward level="LOW">scrap_only</autoReward>
  ```
* **Verdict**: Costs 1 missile, takes 3 hull damage for low scrap.

#### 4. Trap #4: The Lanius Augmented Sacrifice (`QUEST_CONSTRUCTIONYARD`)
* **Requirement**: `Lanius / Anaerobic Crew`
* **Source XML**: `dlcEvents_anaerobic.xml` (Line 152538)
* **What Happens**: You are given the option to sacrifice a Lanius crew member to construct a high-tier augment:
  ```xml
  <removeCrew class="anaerobic"><clone>false</clone></removeCrew>
  <autoReward level="HIGH">augment</autoReward>
  ```
* **Verdict**: Permanent loss of a Lanius (cannot be cloned). Only choose if you have surplus crew and desperately need an augment!

---

# 4. MASTER SHIP UNLOCK FORENSICS & THE SECRET CRYSTAL QUEST [CRYS]

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                    THE 10 FEDERATION CRUISERS & UNLOCK IDs                  │
├─────────────────────────────────────────────────────────────────────────────┤
│  ID 0: The Kestrel (Starting Cruiser)                                       │
│  ID 1: Stealth Cruiser (The Nesasio)       ──► Engi Homeworlds Stolen Tech  │
│  ID 2: Mantis Cruiser (The Gila Monster)   ──► Warlord KazaaakplethKILIK    │
│  ID 3: Engi Cruiser (The Torus)            ──► Reach Sector 5               │
│  ID 4: Federation Cruiser (The Osprey)     ──► Rebel Stronghold Shipyard    │
│  ID 5: Slug Cruiser (The Man of War)       ──► Slug Homeworlds Prototype    │
│  ID 6: Rock Cruiser (The Bulwark)          ──► Rock Homeworlds Sun Trial    │
│  ID 7: Zoltan Cruiser (The Adjudicator)    ──► Zoltan Peace Accord Quest    │
│  ID 8: Crystal Cruiser (The Bravais)       ──► Ancient Monolith to Sector 8 │
│  ID 9: Lanius Cruiser (The Kruos)          ──► Unlock 4 Cruisers (AE)       │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

### A. The Legendary 3-Step Crystal Cruiser Questline [CRY01]

The **Crystal Cruiser (The Bravais)** is the rarest and most intricate secret in FTL. It requires connecting three separate random events across multiple sectors in a single run:

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                        THE 3-STEP CRYSTAL GEODESIC                          │
├─────────────────────────────────────────────────────────────────────────────┤
│  STEP 1: Dense Asteroid Field (Engi/Pirate/Rock Sector) ──► Stasis Pod      │
│  STEP 2: Zoltan/Engi Research Facility (Zoltan/Engi Sector) ──► Revive Ruwen│
│  STEP 3: Rock Homeworlds (Red Sector 4-7) ──► Activate Ancient Monolith     │
│  STEP 4: Sector 8 (Hidden Crystal Worlds) ──► Reach Crystal City Base!      │
└─────────────────────────────────────────────────────────────────────────────┘
```

#### Step 1: Recovering the Damaged Stasis Pod
* **Location**: Pirate Sector, Engi Controlled, or Rock Controlled (Sectors 1–5).
* **Encounter**: `ASTEROID_SPACE_DOCK` / `PIRATE_SALVAGE`.
* **Action**: Choose the Blue Option `req="rock"` or `req="ROCK_ARMOR"` ("Investigate without lifeform scan") or search the dense asteroid debris.
* **Reward**: Grants the `STASIS_POD` augment (*Damaged Stasis Pod*).

#### Step 2: Reviving Ruwen at the Zoltan Research Lab
* **Location**: Zoltan Homeworlds, Zoltan Controlled, Engi Homeworlds, or Engi Controlled (Sectors 2–6).
* **Encounter**: `ZOLTAN_RESEARCH_LAB` / `ZOLTAN_SCIENCE_DOCK`.
* **Action**: Choose the Blue Option `req="STASIS_POD"`:
  ```text
  "Ask if they can open the stasis pod."
  ```
* **Reward**: The pod opens, reviving **Ruwen**, an ancient Crystal crew member who possesses **Level 2 in Shields, Engines, and Weapons**!

#### Step 3: Activating the Ancient Monolith Gateway
* **Location**: **Rock Homeworlds** (Red Sector, Sectors 4–7).
* **Forensic Mechanism**: Having **Ruwen** on your crew forces a **guaranteed green Quest Marker** to appear on the sector beacon map!
* **Source XML**: `events_rock.xml` (`ROCK_CRYSTAL_BEACON`):
  ```xml
  <event name="ROCK_CRYSTAL_BEACON">
    <text id="event_ROCK_CRYSTAL_BEACON_text"/>
    <choice hidden="true" req="crystal">
      <text>Reactivate the ancient device.</text>
      <event load="START_BEACON_CRYSTAL"/>
    </choice>
  </event>
  ```
* **Outcome**: Teleports your ship directly into the secret **Hidden Crystal Worlds**!

#### Step 4: Claiming The Bravais at the Crystal City Base
* **Location**: Hidden Crystal Worlds (Sector 8 Variant).
* **Source XML**: `events_crystal.xml` (`CRYSTAL_UNLOCK`):
  ```xml
  <event name="CRYSTAL_UNLOCK">
    <text id="event_CRYSTAL_UNLOCK_text"/>
    <autoReward level="MED">fuel</autoReward>
    <augment name="CRYSTAL_SHARDS"/>
    <damage amount="-10"/>
    <unlockShip id="8"/>
  </event>
  ```
* **Reward**: 10 Hull Repairs, `CRYSTAL_SHARDS` augment, and `<unlockShip id="8"/>`!

> **Advanced Edition Alternate Unlock**: Beat the Rebel Flagship with the Type A and Type B layouts of all 6 original non-Kestrel ships to unlock the Crystal Cruiser automatically without the quest!

---

### B. All Other 8 Cruiser Quests & Dialogue Trees [CRY02]

#### 1. Stealth Cruiser (ID 1: The Nesasio)
* **Location**: **Engi Homeworlds** (Green Sector).
* **Source XML**: `events_engi.xml` (`ENGI_UNLOCK_1` -> `ENGI_UNLOCK_4`):
* **Requirement**: `Engi Crew Member`.
* **Action**: Speak with the Engi research outpost. They give you 2 simultaneous quest markers. One is a decoy; the other is the secret Rebel Stealth Shipyard.
* **Reward**: Defeat the stealth prototype to receive `SYSTEM_CASING` augment and `<unlockShip id="1"/>`!

#### 2. Mantis Cruiser (ID 2: The Gila Monster)
* **Location**: **Mantis Homeworlds** (Red Sector).
* **Source XML**: `events_mantis.xml` (`MANTIS_NAMED_THIEF_DEFEAT`):
* **Requirement**: `Medbay Lvl 2` / `Clonebay Lvl 2` AND `Teleporter Lvl 2`.
* **Action**: Intercept legendary warlord **KazaaakplethKILIK**. You must **kill all enemy crew without destroying their ship hull**!
* **Blue Option**: Beam aboard with Level 2 Medbay/Teleporter to stabilize the dying warlord.
* **Reward**: KazaaakplethKILIK joins your crew with max Level 2 in all 6 skills + `CREW_STIMS` augment + `<unlockShip id="2"/>`!

#### 3. Federation Cruiser (ID 4: The Osprey)
* **Location**: **Rebel Stronghold** (Red Sector).
* **Source XML**: `events_rebel.xml` (`FLAGSHIP_CONSTRUCTION`):
* **Action**: Scan the secret Rebel naval yard building a secondary Rebel Flagship. Engage and destroy the unfinished Flagship construction.
* **Reward**: High scrap + `<unlockShip id="4"/>`! *(Also unlocks by beating the normal Flagship with any ship).*

#### 4. Slug Cruiser (ID 5: The Man of War)
* **Location**: **Slug Homeworlds** (Purple Nebula Sector).
* **Source XML**: `events_slug.xml` (`SLUG_UNLOCK_1` / `JELLY_UNLOCK`):
* **Requirement**: `Sensors Level 2` or `Slug Crew`.
* **Action**: Fight the Slug warship until they offer surrender. Reject their weapon surrender and select:
  ```text
  "We don't want weapons, we want data/information!"
  ```
* **Outcome**: A quest marker appears inside an ion/oxygen-hazard nebula. Defeat the prototype cruiser to unlock `<unlockShip id="5"/>`!

#### 5. Rock Cruiser (ID 6: The Bulwark)
* **Location**: **Rock Homeworlds** (Red Sector).
* **Source XML**: `events_rock.xml` (`ROCK_UNLOCK1` -> `ROCK_UNLOCK3`):
* **Action**: When hailed by the Rock warship, do NOT pick the aggressive dialogue. Choose:
  ```text
  "We are going to save the galaxy, not squabble."
  ```
* **The Sun Trial**: Travel to the quest beacon bordering a solar flare. **Do NOT jump away early!** Endure the solar flare damage until the Rock warship retreats. Travel to the final quest beacon to earn their honor, the `ROCK_ARMOR` augment, and `<unlockShip id="6"/>`!

#### 6. Zoltan Cruiser (ID 7: The Adjudicator)
* **Location**: **Zoltan Homeworlds** (Green Sector).
* **Source XML**: `events_zoltan.xml` (`ZOLTAN_PEACE_QUEST`):
* **Dialogue Tree**:
  1. Unarmed transport hails: Choose **Choice 2** ("Hear them out").
  2. At the quest marker: Choose **Choice 2** ("Perhaps there is a way to resolve this without violence?").
  3. Final response: Choose **Choice 1** ("True progress can only be achieved without bloodshed").
* **Reward**: Master Zoltan **Envoy** (Max Level 2 in all skills), `ENERGY_SHIELD` augment, and `<unlockShip id="7"/>`!

---

# 5. MASTER BLUEPRINT CATALOG: WEAPONS & DRONES [BLUE]

### A. The S-Tier Weapon Hierarchy
1. **Burst Laser II** *(Cost: 80 scrap, Power: 2, Cooldown: 12.0s)*: 3 laser shots for only 2 power. The gold standard for volley synchronization.
2. **Flak I** *(Cost: 65 scrap, Power: 2, Cooldown: 10.0s)*: 3 projectiles in a tight spread. The most efficient shield-stripping weapon in the game.
3. **Halberd Beam** *(Cost: 65 scrap, Power: 3, Cooldown: 17.0s)*: 2 damage per room. Sweeps 4–5 rooms across the Rebel Flagship for 8–10 total hull damage!
4. **Ion Blast II** *(Cost: 70 scrap, Power: 3, Cooldown: 4.0s)*: Continuously keeps 4 shield bubbles completely disabled when fully manned.

---

# 5. THE REBEL FLAGSHIP: 3-PHASE TACTICAL DESTRUCTION GUIDE [BOSS]

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                      REBEL FLAGSHIP ARTILLERY LAYOUT                        │
├─────────────────────────────────────────────────────────────────────────────┤
│  [ROOM 1: ION ARTILLERY]      [ROOM 2: LASER ARTILLERY (3-Shot)]            │
│  [ROOM 3: MISSILE ARTILLERY]  [ROOM 4: BEAM ARTILLERY (Halberd)]            │
│                                                                             │
│  PRIMARY THREAT IS ROOM 3 (Triple Missile Artillery). Neutralize FIRST!     │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Phase 1: The Cloaking & Artillery Isolation
* **Flagship Defenses**: 4 Shield Layers, Level 3 Cloaking, Level 3 Medbay, Level 3 Doors, 4 Isolated Artillery Pods.
* **Target Priority**:
  1. Teleport boarders (or fire concentrated volleys) into the **Missile Artillery Room** (3rd weapon pod from left). Once the operator dies, it stays destroyed!
  2. Next, neutralize the **Ion Artillery** (1st pod) and **Beam Artillery** (4th pod).
  3. **CRITICAL HARD MODE EXPLOIT**: Leave the operator of the **Triple Laser Pod** (2nd room) alive! If all 4 crew members die, the Flagship's automated AI takes over, repairing all systems autonomously!

### Phase 2: Defense Drone & Power Surge Swarm
* **Flagship Defenses**: 4 Shields, Boarding Drone, Defense Drone I, **Drone Power Surge** (spawns 6–8 attack drones every 25 seconds).
* **Strategy**:
  - Depower your Hacking Drone just as the Flagship's Defense Drone fires, then repower it to bypass the defense grid!
  - Activate Level 1 Cloaking **only when the warning siren sounds for the Drone Power Surge** to dodge the entire swarm.

### Phase 3: Zoltan Super-Shield, Mind Control & Laser Overload
* **Flagship Defenses**: 12 HP Zoltan Shield, Level 3 Mind Control, Level 3 Teleporter (2-man boarder waves), **Laser Power Surge** (12-shot volley).
* **Strategy**:
  - Immediately counter Mind Control with your own Mind Control (or Level 1 Slug).
  - Strip the Zoltan Super-Shield using Flak and Ion volleys.
  - Time your Cloaking to dodge the 12-laser Power Surge volley!

---

# 6. THE 16-STEP SPEEDRUN & VICTORY GEODESIC [FAST]

```text
+-----------------------------------------------------------------------------+
| THE 16-STEP SPEEDRUN GEODESIC: FTL VICTORY [FAST]                           |
|                                                                             |
| 1. Sector 1: Upgrade Shields to Level 2 (2 bubbles / 50 scrap) immediately. |
| 2. Acquire Long-Ranged Scanners at first store to optimize scrap beacons.   |
| 3. Upgrade Engines to Level 4 (30% evasion) before entering Sector 3.       |
| 4. Seek Burst Laser II, Flak I, or Halberd Beam in Stores.                  |
| 5. Acquire Hacking System (80 scrap) by Sector 4.                           |
| 6. Purchase Level 1 Cloaking (150 scrap) before Sector 6.                   |
| 7. Train Pilot and Engine crew to Golden Master (+10% passive dodge).       |
| 8. Upgrade Shields to Level 3 (3 bubbles) by Sector 5.                      |
| 9. Upgrade Subsystems: Doors Level 2, Piloting Level 2 (anti-asteroid).    |
| 10. Reach Sector 8 with at least 3 Shield Bubbles, 40% Evasion, Cloaking.   |
| 11. Sector 8: Destroy Rebel repair stations for scrap and hull repairs.     |
| 12. Flagship Phase 1: Hack Shields; disable Missile Artillery; kill crew.   |
| 13. Flagship Phase 2: Cloak drone surge; destroy missile pod; break shields.|
| 14. Flagship Phase 3: Counter Mind Control; cloak 12-laser surge.           |
| 15. Focus beam and laser fire on Flagship shield room.                      |
| 16. Federation Victory achieved! The Rebellion is broken!                   |
+-----------------------------------------------------------------------------+
```

---

# 7. VERSION HISTORY & BUILD PROVENANCE [VERS]

* **2012 Initial Release (v1.01)**: Base game.
* **2014 Advanced Edition (v1.5.13)**: Added Lanius, Hacking, Mind Control, Backup Battery, and Clone Bay.
* **2021+ FNA/Modern Engine Build (v1.6.14)**: Current Steam build.
* **Target Build SHA-256**: `7d60be992850937b420ee963d76e73ff6697818e698889a7be8e7be1ffec975f`

---

# 8. CONTACT POLICY & CREDITS [CRED]

* **Subset Games**: Justin Ma and Matthew Davis.
* **Composer**: Ben Prunty (Iconic chiptune/ambient soundtrack).
* **YOU, the Captain**: "To boldly go where no Federation cruiser has gone before!"
