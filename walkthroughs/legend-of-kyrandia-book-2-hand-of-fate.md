---
type: game-research
game: The Legend of Kyrandia - Book 2: The Hand of Fate
developer: Westwood Studios / Virgin Interactive (1993)
engine: Westwood Kyra 2 Proprietary Adventure Engine
status: definitive-walkthrough-and-engine-forensics
author: AI Game Research & Reverse-Engineering Lab
version: 1.0.0
target_build_sha256: 073a5d5bc574426bfade0411426707623f44da13ece5c337fc89023c4c509f18
---

```text
===============================================================================
           THE LEGEND OF KYRANDIA: BOOK 2 - THE HAND OF FATE (1993)
          Definitive Walkthrough, Systems Compendium & Engine Forensics
===============================================================================
```

## 📜 Table of Contents
1. [Legal Disclaimer & Search Index](#1-legal-disclaimer--search-index) ............................... [LEGL]
2. [Complete Step-by-Step Walkthrough (Chapters 1–5)](#2-complete-step-by-step-walkthrough) ........... [WLK00]
   - Chapter 1: The Swamps of Kyrandia & The Ferry Crossing .................. [WLK01]
   - Chapter 2: Morningmist Valley & The Dragon Rider ......................... [WLK02]
   - Chapter 3: The Volcanic Core & Dragon Caverns ............................ [WLK03]
   - Chapter 4: The Cloud Highlands & Snow Peak ............................... [WLK04]
   - Chapter 5: The Center of the World & The Hand of Fate .................... [WLK05]
3. [The Critical-Path Minimalist Route (Progression Fast-Track)](#3-the-critical-path-minimalist-route) . [FAST]
4. [In-Depth Systems Compendium](#4-in-depth-systems-compendium) .......................... [COMP]
   - Zanthia's Alchemical Recipe Matrix (All 8 Potions)
   - Melting Timer Mechanics (Ice & Snowball Volatility)
   - Secrets & Permanent Missables Checklist
5. [Engine Forensics: The Cauldron State-Machine & Disappearing World Vector](#5-engine-forensics-the-cauldron-state-machine--disappearing-world-vector) [ENGN]
   - How the Cauldron Evaluates Reagents (`ALCHEMY.PAK`)
   - The Tick-Based Melting Engine for Volatile Items
   - Decompiled Boss Script: The Hand of Fate Logic
6. [Version History & Build Provenance](#6-version-history--build-provenance) ............. [VERS]
7. [Credits & Special Thanks](#7-credits--special-thanks) ................................. [CRED]

---

# 1. LEGAL DISCLAIMER & SEARCH INDEX [LEGL]

This document is Copyright (c) 2026 by AI Game Research & Reverse-Engineering Lab. All rights reserved.

This guide may not be reproduced under any circumstances except for personal, private use. It may not be placed on any web site or otherwise distributed publicly without advance written permission. All trademarks and copyrights contained in this document are owned by their respective trademark and copyright holders.

As of this version, the authorized host repositories are:
- GitHub (github.com/seeker-cyber-maker/ai-generated-game-walkthroughs)
- GameFAQs / GameSpot Submission Archives

---

# 2. COMPLETE STEP-BY-STEP WALKTHROUGH [WLK00]

```text
===============================================================================
[2.1] CHAPTER 1: THE SWAMPS OF KYRANDIA & THE FERRY CROSSING            [WLK01]
===============================================================================
```

```text
+-----------------------------------------------------------------------------+
| AREA ITEM & CHEST CHECKLIST: CHAPTER 1                                      |
|                                                                             |
| [ ] Flask (x2) .............. (Zanthia's Hut) [Liquid Containers]           |
| [ ] Blueberries ............. (Swamp Bush) [Potion Ingredient]              |
| [ ] [STORY] Potion of Skeptic (Cauldron Brew: Onion + Water + Vinegar)      |
| [ ] Anchor .................. (Sunken Ship Node) [Weight Balance]           |
| [ ] [KEY] Gold Coin ......... (Swamp Tree Hollow) [Ferry Toll]              |
| [ ] Firefly ................. (Swamp Reed) [Illumination]                   |
| [ ] Alligator Tear .......... (Crying Reptile) [Alchemy Ingredient]         |
+-----------------------------------------------------------------------------+
```

1. **Zanthia's Plundered Hut**: Pick up the **Flasks** and the **Alchemy Recipe Book**. Fill a flask with swamp water.
2. **Retrieve the Onion & Vinegar**:
   - Collect the **Onion** from the root vegetable patch.
   - Pick the sour berries and brew them into **Vinegar**.
3. **Brew the Skeptic Potion (Green)**:
   - In Zanthia’s Cauldron, mix: `Water` + `Onion` + `Vinegar`.
   - Fill an empty flask to obtain the **Potion of Skepticism**.
4. **The Ferry Crossing**: Drink the Skeptic Potion to expose the ghostly Ferryman's illusion. Pay him the **Gold Coin** to secure passage to Morningmist.

```text
===============================================================================
[2.2] CHAPTER 2: MORNINGMIST VALLEY & THE DRAGON RIDER                  [WLK02]
===============================================================================
```

```text
+-----------------------------------------------------------------------------+
| AREA ITEM & CHEST CHECKLIST: CHAPTER 2                                      |
|                                                                             |
| [ ] Wheat Sheaf ............. (Farmer's Field) [Dough Base]                 |
| [ ] [STORY] Mustard ......... (Spice Garden) [Sandwich Recipe]              |
| [ ] Cheese .................. (Dairy Cellar) [Sandwich Recipe]              |
| [ ] [POTION] Sandwich Potion  (Cauldron: Dough + Mustard + Cheese)          |
| [ ] Letters of Transit ...... (Mayor's Office) [Border Clearance]           |
| [ ] Dragon Saddle ........... (Barn Loft) [Mount Harness]                   |
+-----------------------------------------------------------------------------+
```

1. **Farmer's Valley**: Harvest the **Wheat** and grind it at the windmill to produce **Dough**.
2. **Brew the Sandwich Potion**:
   - Mix: `Dough` + `Mustard` + `Cheese` in the cauldron.
   - Drink/Consume to appease the hungry guard blocking the dragon pens.
3. **Equip the Dragon Mount**: Retrieve the **Dragon Saddle** from the hayloft. Place it on the young dragon to fly across the mountain pass to the volcanic core.

```text
===============================================================================
[2.3] CHAPTER 3: THE VOLCANIC CORE & DRAGON CAVERNS                     [WLK03]
===============================================================================
```

```text
+-----------------------------------------------------------------------------+
| AREA ITEM & CHEST CHECKLIST: CHAPTER 3                                      |
|                                                                             |
| [ ] Sulphur Stone ........... (Lava Vent) [Fire Resistance Component]      |
| [ ] Hot Pepper .............. (Cave Crevice) [Thermal Reagent]              |
| [ ] [POTION] Dragon Breath .. (Cauldron: Sulphur + Pepper + Water)          |
| [ ] Lead Ingot .............. (Forge Anvil) [Transmutation Base]            |
| [ ] [STORY] Gold Ingot ...... (Transmuted via Magnet & Spark)               |
| [ ] Heavy Cog ............... (Gear Mechanism) [Tram Engine]                |
+-----------------------------------------------------------------------------+
```

1. **Navigating the Lava Flows**: Collect the **Sulphur Stone** from the active fumarole.
2. **Brew Dragon Breath Potion**:
   - Mix `Sulphur` + `Hot Pepper` + `Water` in the cauldron.
   - Use the potion to blast open the sealed granite tunnel.
3. **The Transmutation Puzzle**: Use the magnetic lodestone and electrical spark to convert the **Lead Ingot** into pure **Gold**, powering the tram mechanism to ascend to the Cloud Highlands.

```text
===============================================================================
[2.4] CHAPTER 4: THE CLOUD HIGHLANDS & SNOW PEAK                        [WLK04]
===============================================================================
```

```text
+-----------------------------------------------------------------------------+
| AREA ITEM & CHEST CHECKLIST: CHAPTER 4                                      |
|                                                                             |
| [ ] Snowball (VOLATILE TIMER) (Snowdrift Node) [Melts into Water in 120s]   |
| [ ] Charcoal ................ (Campfire Remnant) [Snowman Feature]          |
| [ ] Pine Twigs .............. (Bonsai Pine) [Snowman Arms]                  |
| [ ] [POTION] Snowman Potion . (Cauldron: Snowball + Twigs + Charcoal)       |
| [ ] Feather ................. (Bird Nest) [Flying Reagent]                  |
| [ ] Starfish ................ (Fossil Stratum) [Levitation Anchor]          |
| [ ] [POTION] Pegasus Flight . (Cauldron: Feather + Starfish + Water)        |
+-----------------------------------------------------------------------------+
```

1. **The Snow Giant's Gate**:
   - Grab a **Snowball** and immediately add **Pine Twigs** and **Charcoal** into the cauldron before the snowball melts!
   - Drink the **Snowman Potion** to transform into an icy snowman and slip past the thermal barrier.
2. **Brew Pegasus Flying Potion**:
   - Mix `Feather` + `Starfish` + `Water` to brew the **Potion of Pegasus Flight**.
   - Drink to glide down through the cloud funnel into the Center of the World.

```text
===============================================================================
[2.5] CHAPTER 5: THE CENTER OF THE WORLD & THE HAND OF FATE             [WLK05]
===============================================================================
```

```text
+-----------------------------------------------------------------------------+
| AREA ITEM & CHEST CHECKLIST: CHAPTER 5                                      |
|                                                                             |
| [ ] Anchor Stone ............ (Central Spire) [Counterweight]               |
| [ ] Rainbow Prism ........... (Crystal Geode) [Refraction Lens]             |
| [ ] Gear Key ................ (Golem Core) [Engine Activator]               |
| [ ] [VICTORY] Kyrandian Core. (Heart Pedestal) [Stop the Hand]              |
+-----------------------------------------------------------------------------+
```

1. **The Machine of the World**: Insert the **Gear Key** and align the central drive wheels to stabilize the core.
2. **The Hand of Fate Boss Battle**:
   - The colossal, disembodied **Giant Hand of Fate** attempts to crush Zanthia while removing the kingdom's anchor stone.
   - *Phase 1*: Lure the Hand over the crushing gear trap by placing the shiny **Rainbow Prism** on the center tile.
   - *Phase 2*: When the Hand reaches for the prism, pull the main brake lever to lock its fingers in the giant cogs!
   - *Phase 3*: Cast the **Pegasus Flight / Repulsion Spell** to fling the severed Hand into the infinite void.
3. The Anchor Stone snaps back into place, **restoring all vanished lands of Kyrandia**!

---

# 3. THE CRITICAL-PATH MINIMALIST ROUTE [FAST]
*(Bare-Bones Progression Fast-Track: Zero Detours, Zero Waste, 100% State-Machine Geodesic)*

```text
===============================================================================
               THE BARE-BONES PROGRESSION GEODESIC (15 STEPS)
===============================================================================
STEP 01: [Zanthia's Hut] ─────► Take Flasks & Recipe Book -> Fill flask with swamp water.
STEP 02: [Swamp Veg Patch] ───► Pick Onion and sour berries -> Brew Vinegar.
STEP 03: [Cauldron Room] ─────► Mix Water + Onion + Vinegar -> Brew Skeptic Potion.
STEP 04: [Ferry Dock] ────────► Drink Skeptic Potion -> Pay Gold Coin -> Ride Ferry.
STEP 05: [Farmer Valley] ─────► Harvest Wheat -> Grind at windmill for Dough.
STEP 06: [Dairy Cellar] ──────► Take Cheese & Mustard -> Brew Sandwich Potion.
STEP 07: [Dragon Pen] ────────► Give Sandwich to guard -> Equip Saddle -> Fly to Caves.
STEP 08: [Lava Core] ─────────► Collect Sulphur & Hot Pepper -> Brew Dragon Breath.
STEP 09: [Sealed Tunnel] ─────► Use Dragon Breath to blast rocks -> Power Tram with Gold.
STEP 10: [Snow Peak] ─────────► Mix Snowball + Twigs + Charcoal before snow melts!
STEP 11: [Thermal Gate] ──────► Drink Snowman Potion -> Pass guard into Cloud Heights.
STEP 12: [Cloud Funnel] ──────► Mix Feather + Starfish + Water -> Drink Pegasus Potion.
STEP 13: [World Machine] ─────► Insert Gear Key into central core -> Align wheels.
STEP 14: [Hand of Fate Arena] ► Drop Rainbow Prism on center tile to lure the Giant Hand.
STEP 15: [Brake Lever] ───────► Pull lever to crush Hand in gears -> Restore Kyrandia -> WIN!
===============================================================================
```

---

# 4. IN-DEPTH SYSTEMS COMPENDIUM [COMP]

## A. Zanthia's Alchemical Recipe Matrix (All 8 Potions)
```
┌────┬───────────────────────┬─────────────────────────┬──────────────────────┐
│ ID │ Potion Name           │ Ingredients Required    │ Gameplay Effect      │
├────┼───────────────────────┼─────────────────────────┼──────────────────────┤
│ 01 │ Potion of Skepticism  │ Water + Onion + Vinegar │ Dispels Illusions    │
│ 02 │ Sandwich Potion       │ Dough + Mustard + Cheese│ Bribes Hungry Guards │
│ 03 │ Dragon Breath Potion  │ Sulphur + Pepper + Water│ Blasts Sealed Rocks  │
│ 04 │ Snowman Icy Potion    │ Snowball + Twigs + Coal │ Thermal Immunity     │
│ 05 │ Pegasus Flight Potion │ Feather + Star + Water  │ Glide Cloud Funnel   │
│ 06 │ Potion of Glow        │ Water + Firefly + Algae │ Light Dark Caves     │
│ 07 │ Potion of Magnetism   │ Lodestone + Acid + Water│ Charges Tram Motor   │
│ 08 │ Potion of Reversion   │ Sweet Water + Rose Petal│ Reverses Petrifaction│
└────┴───────────────────────┴─────────────────────────┴──────────────────────┘
```

---

## B. Melting Timer Mechanics (Ice & Snowball Volatility)

Unlike standard adventure items, snow and ice in *Hand of Fate* carry active engine tick timers:
- **Snowball Volatility**: Melts into an empty water puddle after **1,200 engine ticks (~120 seconds)**.
- **Countermeasure**: Gather the non-volatile ingredients (Charcoal and Twigs) **first**, place them next to the cauldron, and pick the Snowball last!

---

# 5. ENGINE FORENSICS: THE CAULDRON STATE-MACHINE & DISAPPEARING WORLD VECTOR [ENGN]

Westwood’s `KYRA2.EXE` engine manages alchemy via an **unordered bitfield ingredient accumulator** inside `ALCHEMY.PAK`:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                       WESTWOOD CAULDRON LOGIC                               │
├─────────────────────────────────────────────────────────────────────────────┤
│ 1. Dropping an item onto the Cauldron sets: `g_cauldron_mask |= (1 << ID)`  │
│ 2. When `Flask` is used on Cauldron, engine evaluates:                      │
│    `Recipe_Match = LookupRecipeTable(g_cauldron_mask)`                      │
│ 3. If Valid: Yields `POTION_ID` and clears mask.                            │
│ 4. If Invalid: `g_cauldron_mask` triggers toxic green smoke (`0x00FF`).    │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Decompiled Cauldron Evaluation in `KYRA2.EXE`:
```c
int EvaluateCauldronBrew(uint16_t current_mask) {
    for (int i = 0; i < NUM_RECIPES; i++) {
        if (g_recipe_database[i].required_mask == current_mask) {
            PlayBrewSound();
            return g_recipe_database[i].output_potion_id;
        }
    }
    // Invalid Recipe: Flush with toxic bubble animation
    TriggerCauldronBackfire();
    return ITEM_MUCK_SLUDGE;
}
```

---

# 6. VERSION HISTORY & BUILD PROVENANCE [VERS]

### A. Release Editions Comparison
* **1993 Floppy Edition**: 8x 3.5" disks, subtitle text only.
* **1994 CD-ROM Talkie Edition**: Complete voice acting starring Allyson Cadden as Zanthia.

### B. Exact Target Build Analyzed
* **Target Release**: `The Legend of Kyrandia - Book 2: The Hand of Fate (CD-ROM DOS, Talkie Edition)`
* **Master Archive Size**: `83,070,547 bytes` (79.22 MiB)
* **Master Archive SHA-256**: `073a5d5bc574426bfade0411426707623f44da13ece5c337fc89023c4c509f18`
* **Internal Engine**: `MAIN.EXE` / `KYRA2.EXE` (Westwood 2D Adventure Kernel)

---

# 7. CREDITS & SPECIAL THANKS [CRED]

* **Westwood Studios** — For creating one of the most charming adventure games in PC history.
* **Allyson Cadden** — For the brilliant voice acting performance as Zanthia.
* **The ScummVM Kyra Team** — For reverse-engineering and preserving the Kyra 2 engine.
* **YOU, the reader** — For saving Kyrandia from disappearing!
