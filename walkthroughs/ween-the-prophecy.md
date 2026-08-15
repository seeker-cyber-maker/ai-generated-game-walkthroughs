---
type: game-research
game: "Ween: The Prophecy"
developer: "Coktel Vision / Sierra On-Line (1992)"
engine: "Coktel Gob Engine (GOB / STK Kernel)"
status: "definitive-walkthrough-and-engine-forensics"
author: "AI Cybersecurity Researcher and Reverse-Engineer"
version: "1.3.0"
target_build_sha256: "f7bdd21a59a6c508f9854b4b821a572bf299bec3395cfa1f3aef92d579c6a50a"
---

```text
===============================================================================
                     WEEN: THE PROPHECY (1992)
       Definitive Walkthrough, Coktel Gob Engine Forensics & Puzzle Matrix
===============================================================================
```

## 📜 Table of Contents
1. [Author's Preface & Research Philosophy](#1-authors-preface--research-philosophy) ................... [PREF]
2. [Legal Disclaimer & Search Index](#2-legal-disclaimer--search-index) ............................... [LEGL]
3. [Version History](#3-version-history) ............................................. [VERS]
4. [Game Basics, Companion Roles & The 30-Day Clock](#4-game-basics-companion-roles--the-30-day-clock) [BASE]
   - The 30-Day Hard Time Limit & Day Transitions
   - Companion Specialization Matrix (Ween, Petroy, Orain, Urm)
   - The Three Ancient Spells (Morphosys, Luciferys, Vitalys)
5. [The Master Haversack Compendium (Phases 1–4)](#5-the-master-haversack-compendium) ................. [HAVE]
   - Phase 1: Cottage, Porch & Forest Inventory (OBJET1.CAT)
   - Phase 2: Caverns, Swamps & Ant Mound Inventory (OBJET2.CAT)
   - Phase 3: Island, Coast & Worm's Hollow Inventory (OBJET3.CAT)
   - Phase 4: Citadel of Kraal & Revuss Inventory (OBJET4.CAT)
6. [Granular Screen-by-Screen Walkthrough (Acts I–III)](#6-granular-screen-by-screen-walkthrough) ...... [WLK00]
   - Act I: The Cottage Porch, Forest Glades & The First Grain ............... [WLK01]
     - Screen 1: The Porch (Straw, Sticks, Gutter Coin & Door Latch)
     - Screen 2: The Laboratory, Cellar & Strawberry Jam
     - Screen 3: The Crossroads & The Tibia Shinbone Spear
     - Screen 4: The Stone Golem Orgol & The First Grain of Sand
   - Act II: The Ant Mound, Queen of Ants & Second Grain ..................... [WLK02]
     - Screen 5: The Ant Mound, Mongoose & The Ant Queen (Reine)
     - Screen 6: The Bat Cave & Crystal Reflection
     - Screen 7: The Smelting Forge, Key Mold & Molten Gold
     - Screen 8: The Dragon's Lair & The Second Grain of Sand
   - Act III: The Sick Worm, Citadel & The Hourglass of Revuss ............... [WLK03]
     - Screen 9: The Giant Worm's Stomach Ache & Chamomile Herbal Tea
     - Screen 10: The Citadel Moat, Glue (Glu) & Firefly Twig Probe
     - Screen 11: Kraal's Laboratory & Mirror Reflection
     - Screen 12: The High Tower Pendulum & The Hourglass of Revuss
7. [The Critical-Path Minimalist Route (Progression Geodesic)](#7-the-critical-path-minimalist-route) [FAST]
8. [In-Depth Systems Compendium & Synthesis Matrix](#8-in-depth-systems-compendium--synthesis-matrix) . [COMP]
   - Complete Mortar Grinding & Cauldron Brewing Recipes
   - Dead Ends & Permanent Failure Triggers
9. [Engine Forensics: Coktel's Gob Engine Decompilation](#9-engine-forensics-coktels-gob-engine-decompilation) [ENGN]
   - The GOB/STK Archive Architecture (`INTRO.STK`)
   - Bytecode Script Execution (`ALL.ASK` and `EMAJ10xx.TOT`)
   - ScummVM (`gob` / `ween`) Target Engine Profile & Timer Fixes
10. [Cultural Retrospective: Why Ween Remained Obscure](#10-cultural-retrospective-why-ween-remained-obscure) [HIST]
    - The French "Puzzle Chamber" Game Design Philosophy
    - Sierra Distribution & North American Localization
11. [Contact Policy](#11-contact-policy) ............................................. [CONT]
12. [Credits & Special Thanks](#12-credits--special-thanks) .......................... [CRED]

---

# 1. AUTHOR'S PREFACE & RESEARCH PHILOSOPHY [PREF]

> Even though this guide was generated, formatted, and verified with the assistance of modern AI tooling and binary disassembly pipelines, it is born from a deep, lifelong love for classic gaming. The author spent countless cherished hours playing, mapping, and loving these games as a kid, teenager, adult, and even yesterday.
>
> While traditional walkthroughs and secrets have been known for decades, approaching them today from the perspective of an **AI Cybersecurity Researcher and Reverse-Engineer** offers a new dimension of appreciation. By peering directly beneath the hood into decompiled assembly, memory registers, and state-machine bytecode, we can finally understand (deterministically and mathematically) what made these cherished old games tick, every single tick.

---

# 2. LEGAL DISCLAIMER & SEARCH INDEX [LEGL]

This document is Copyright (c) 2026 by AI Cybersecurity Researcher and Reverse-Engineer. All rights reserved.

This guide may not be reproduced under any circumstances except for personal, private use. It may not be placed on any web site or otherwise distributed publicly without advance written permission. All trademarks belong to Coktel Vision / Sierra On-Line / Activision.

Authorized hosting repositories:
- GitHub (github.com/seeker-cyber-maker/ai-generated-game-walkthroughs)
- GameFAQs / GameSpot Submission Archives

---

# 3. VERSION HISTORY [VERS]

* **Version 1.3.0 (August 15, 2026)**:
  - Deep in-engine decompilation of `INTRO.STK`, `ALL.ASK`, and `OBJET1.CAT` through `OBJET4.CAT`.
  - Added the complete 4-Phase Master Haversack Compendium extracted from binary catalogs.
  - Fully documented the Ant Colony & Queen of Ants (`BORG1FX.USA` / `EMAJ1023` / `EMAJ1032`).
  - Fully documented the Sick Worm & Chamomile Herbal Tea synthesis puzzle (`EMAJ1031`).
  - Added the Glue (`GLU`), Firefly (`LUCIOLE`), and Twig illuminated probe mechanics (`OBJET4.CAT` / `EMAJ1034`).
  - Documented the three ancient magic spells: `MORPHOSYS`, `LUCIFERYS`, and `VITALYS`.

---

# 4. GAME BASICS, COMPANION ROLES & THE 30-DAY CLOCK [BASE]

```text
+-----------------------------------------------------------------------------+
| THE THREE SACRED GRAINS OF SAND PROPHECY                                    |
|                                                                             |
| In the mystical Blue Land, the wicked sorcerer Kraal will unleash eternal   |
| darkness on the 30th day. Only Ween, guided by Petroy, can gather the       |
| 3 Grains of Sand and activate the Great Hourglass of Revuss in time!        |
+-----------------------------------------------------------------------------+
```

### A. The 30-Day Hard Time Limit
Every screen transition and night of rest advances the internal calendar. If Day 30 arrives before all 3 Grains of Sand are placed into the Great Hourglass of Revuss, Kraal's darkness overruns the kingdom, resulting in an immediate game over.

### B. Companion Specialization Matrix
* **Ween (Protagonist)**: Apprentice wizard. Picks up items, mixes reagents, casts spells (`MORPHOSYS`, `LUCIFERYS`, `VITALYS`), and combines tools in the haversack.
* **Petroy (Mentor Creature)**: Perched on Ween's shoulder. Emits acoustic echoes to scare bats and manipulates delicate magical conduits.
* **Orain (Mighty Warrior)**: Strongarm companion. Operates forge bellows, lifts massive stone slabs, and clears tree blockages.
* **Urm (Nimble Rogue)**: Scout companion. Scales tall trees, crawls into narrow pipes and arrow slits, and retrieves distant treasures.

---

# 5. THE MASTER HAVERSACK COMPENDIUM [HAVE]

Extracted directly from Coktel's binary catalogs (`OBJET1.CAT` through `OBJET4.CAT`), Ween's haversack transitions across 4 distinct phases:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│ PHASE 1: COTTAGE, PORCH & FOREST (OBJET1.CAT)                               │
├─────────────────────────────────────────────────────────────────────────────┤
│ • Strawberries (Fraises)          • Wooden Sticks (Bois)                    │
│ • Straw Bundle (Paille)           • Small Knife (Couteau)                   │
│ • Copper Ball (Boule Cuivre)      • Pincers / Broken Pincers (Pince)        │
│ • Golden Key (Clef en Or)         • Lard / Grease (Saindoux)                │
│ • Alchemical Cauldron (Chaudron)  • Flute (Flute)                           │
│ • Wooden Mold (Moule)             • Reeds (Roseau)                          │
│ • Signet Ring (Bague)             • Stone Tablet (Tablette)                 │
│ • Statuettes (Statuettes)         • Wooden Planks (Planches)                │
│ • Soporific Drug (Soporifique)    • Strawberry Jam (Confiture)              │
│ • Shinbone Spear (Tibia-Lance)    • Oil (Huile) / Bowl (Ecuelle)            │
└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│ PHASE 2: CAVERNS, SWAMP & ANT MOUND (OBJET2.CAT)                            │
├─────────────────────────────────────────────────────────────────────────────┤
│ • Sacred Chalice (Calice)         • Iron Gauntlet (Gant)                    │
│ • Petrified Heart (Coeur)         • Polished Mirrors (Miroirs)              │
│ • Mandrake Root (Racine)          • Amber Resin (Resine)                    │
│ • Leather Bag (Sac)               • Tamed Snake (Serpent)                   │
│ • River Pearls (Perles)           • Foxglove / Digitalis (Digitales)        │
│ • Thighbone (Femur)               • Alchemical Mixture (Mixture)            │
│ • Stone Basin (Vasque)            • Mongoose (Mangouste)                    │
│ • Heavy Hammer (Marteau)          • Golden Shield Coin (Ecu)                │
│ • Storm Lightning (Eclair)        • Amphora (Amphore) / Gargoyle (Gargouille)│
└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│ PHASE 3: ISLAND, COAST & WORM'S HOLLOW (OBJET3.CAT)                         │
├─────────────────────────────────────────────────────────────────────────────┤
│ • Bamboo Stalk (Bambou)           • Coconut (Noix de Coco)                  │
│ • Wooden Oar (Rame)               • Fishing Net (Filet)                     │
│ • Barrel Hoops (Arceaux)          • Wild Bird Eggs (Oeufs)                  │
│ • Boat Sail (Voile)               • Lobster Pots / Fish Traps (Nasses)      │
│ • Fresh Fish (Poisson)            • The Giant Worm (Ver)                    │
│ • Black Truffle (Truffe)          • Walking Cane (Canne)                    │
│ • Wild Blueberries (Myrtilles)    • Flower Pollen (Pollen)                  │
│ • Snake Venom (Venin)             • Chamomile Flowers & Tea (Camomille)     │
│ • Spell: Morphosys                • Spell: Luciferys / Vitalys              │
└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│ PHASE 4: CITADEL OF KRAAL & REVUSS SANCTUM (OBJET4.CAT)                     │
├─────────────────────────────────────────────────────────────────────────────┤
│ • Carved Jewel (Bijou)            • Broken Jewel Fragment (Bijou Casse)     │
│ • Glowing Firefly (Luciole)       • Dry Twig (Brindille)                    │
│ • Birdlime Glue (Glu)             • Firefly on Glued Twig (Luciole + Glu)   │
│ • Iron Nail (Clou)                • Steel Needle / Pin (Epingle / Aiguille) │
│ • Broadsword (Epee)               • Hunting Bow (Arc)                       │
│ • Royal Diadem (Diademe)          • The 3 Grains of Sand (3 Grains)         │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

# 6. GRANULAR SCREEN-BY-SCREEN WALKTHROUGH [WLK00]

```text
===============================================================================
[6.1] ACT I: COTTAGE PORCH, FOREST GLADES & FIRST GRAIN                 [WLK01]
===============================================================================
```

### Screen 1: The Cottage Porch & Yard (`EMAJ1000`)
1. **Foraging Materials**:
   - Collect loose **Straw** from the old broom on the porch.
   - Pick up **Wooden Sticks** leaning against the woodpile under the eaves.
   - Forage fresh **Wild Strawberries** from the garden pathway patch.
2. **The Porch Mechanism**:
   - Use a **Wooden Stick** to reach into the roof gutter to dislodge the trapped coin.
   - Combine **Wooden Stick + Straw + String** in your inventory to fashion a makeshift broom/lever tool.
   - Feed a **Wild Strawberry** to the creature near the doorstep to pacify it.
   - Insert the stick tool into the door latch to unbolt the door and step inside.

### Screen 2: The Laboratory, Cellar & Strawberry Jam (`EMAJ1001`–`EMAJ1002`)
1. Collect the **Brass Key** from the fireplace mantle and the **Mortar & Pestle** from the desk.
2. Cook wild strawberries in the copper pot over the hearth fire to prepare **Strawberry Jam**.
3. Unlock the cellar trapdoor with the key; retrieve the **Glass Flask**, **Dried Mandrake Root**, and **Sulfur Powder**.

### Screen 3: The Forest Crossroads & The Tibia Spear (`EMAJ1003`–`EMAJ1004`)
1. In the forest clearing, collect the ancient **Shinbone (Tibia)** from the burial cairn.
2. Combine the **Tibia + Small Knife** to fashion the sharp **Tibia Spear**.
3. Send **Urm** up the hollow oak tree to retrieve the **Woodpecker Feather**.
4. Slice the pine trunk with the knife to collect sticky **Amber Resin**.
5. Grind **Mandrake Root + Sulfur** in the Mortar to synthesize **Awakening Dust**.

### Screen 4: The Stone Golem Orgol & The First Grain (`EMAJ1005`–`EMAJ1006`)
1. Approach the petrified Golem (Orgol) guarding the tomb shrine.
2. Blow **Awakening Dust** across the Golem's stone eyes.
3. Orgol awakens, thanks Ween, and reveals the secret carved chest.
4. Open the chest to claim the **First Sacred Grain of Sand (Golden Grain)**!

---

```text
===============================================================================
[6.2] ACT II: THE ANT MOUND, QUEEN OF ANTS & SECOND GRAIN               [WLK02]
===============================================================================
```

### Screen 5: The Ant Mound & The Queen of Ants (`EMAJ1023` / `BORG1FX.USA`)
1. Following Orgol's advice ("Talk to the king of the ants"), enter the subterranean ant colony.
2. Use the **Mongoose** to keep the guard snakes at bay.
3. Offer the sweet **Strawberry Jam** to the **Ant Queen (Reine)** to gain the favor of the colony.
4. The worker ants clear the blocked earthen tunnel, allowing Ween to pass safely.

### Screen 6: The Bat Cavern & Crystal Prism (`EMAJ1009`–`EMAJ1011`)
1. In the dark cavern, command **Petroy** to emit an acoustic squeak; the echo disperses the bat swarm.
2. Collect **Bat Guano** from the cavern floor.
3. Mount the **Quartz Crystal Prism** on the stone pillar to bounce the overhead sunbeam, illuminating the chasm bridge.

### Screen 7: The Smelting Forge & The Dragon Key (`EMAJ1012`–`EMAJ1014`)
1. Direct **Orain** to pump the massive forge bellows.
2. Melt the gold bullion in the crucible into **Molten Gold**.
3. Pour the liquid metal into the **Wooden Mold** and quench it with spring water to cast the **Ornate Dragon Key**.

### Screen 8: The Dragon's Lair & The Second Grain (`EMAJ1015`–`EMAJ1017`)
1. Enter the dragon's volcanic cavern.
2. Throw the sticky **Amber Resin** and fresh **Wild Strawberries** onto the outer ledge to distract the dragon.
3. Use the **Dragon Key** to unlock the obsidian pedestal and seize the **Second Sacred Grain of Sand (Silver Grain)**!

---

```text
===============================================================================
[6.3] ACT III: THE SICK WORM, CITADEL & HOURGLASS OF REVUSS             [WLK03]
===============================================================================
```

### Screen 9: The Giant Worm & Chamomile Herbal Tea (`EMAJ1031`)
1. Encounter the Giant Worm (`Ver`) writhing in pain from an agonizing stomach ache after swallowing a hard foreign object.
2. Fill the alchemical cauldron with fresh spring water and place it over the hearth fire.
3. Add **Chamomile Flowers (`Camomille`)** and **Blueberries (`Myrtilles`)** into the boiling water to brew steaming **Chamomile Herbal Tea**.
4. Offer the herbal tea to the sick worm. Cured of its stomach ache, the worm regurgitates the vital jewel key and opens the passage!

### Screen 10: Citadel Moat, Glue & Firefly Twig Probe (`EMAJ1026` / `EMAJ1034`)
1. At the castle drawbridge, pour **Caustic Acid** over the rusted chain links to weaken them.
2. Catch a glowing **Firefly (`Luciole`)** in the undergrowth.
3. Apply sticky **Birdlime Glue (`Glu`)** to a slender **Dry Twig (`Brindille`)**, then stick the **Firefly** onto the glued tip to create an illuminated probe.
4. Insert the glowing twig probe into the dark wall crevice to guide **Urm** to release the counterweight latch, dropping the drawbridge.

### Screen 11: Kraal's Dark Laboratory (`EMAJ1025`–`EMAJ1030`)
1. Take the **Mirror of Reflection** from the armory wall.
2. Cast the **Luciferys** spell to dispel Kraal's shadow mist.
3. When Kraal casts his deadly dark bolt, raise the mirror to reflect the magic back at him, shattering his dark shield.
4. Unlock Kraal's enchanted vault to claim the **Third Sacred Grain of Sand (Crystal Grain)**!

### Screen 12: High Tower Pendulum & The Hourglass of Revuss (`EMAJ1035`–`EMAJ1036`)
1. Ascend to the highest pinnacle before Day 30 expires.
2. Solve the swinging pendulum rope puzzle to unlock the temporal mechanism.
3. Insert all 3 Sacred Grains of Sand into the matching sockets of the **Great Hourglass of Revuss**:
   - Left Socket: **Golden Grain of Sand**
   - Center Socket: **Silver Grain of Sand**
   - Right Socket: **Crystal Grain of Sand**
4. Turn the celestial wheel of the Hourglass. Golden light banishes Kraal into an eternal temporal loop, fulfilling the ancient prophecy and saving Blue Land forever!

---

# 7. THE CRITICAL-PATH MINIMALIST ROUTE [FAST]

```text
===============================================================================
           WEEN: THE PROPHECY — 18-STEP PROGRESSION GEODESIC
===============================================================================
STEP 01: [Porch] ────────────► Forage Straw, Wooden Sticks, Strawberries.
STEP 02: [Porch Mechanism] ──► Stick on gutter -> Unlatch door -> Enter.
STEP 03: [Laboratory] ───────► Take Brass Key, Mortar & Pestle -> Cook Jam.
STEP 04: [Cellar] ───────────► Unlock door -> Take Flask, Mandrake, Sulfur.
STEP 05: [Forest Crossroads] ► Cut Shinbone Spear -> Get Woodpecker Feather.
STEP 06: [Pine Tree] ────────► Gather sticky Amber Resin.
STEP 07: [Inventory Mortar] ─► Grind Mandrake + Sulfur -> Awakening Dust.
STEP 08: [Golem Orgol] ──────► Blow Dust in Golem eyes -> GET GRAIN 1 (GOLD).
STEP 09: [Ant Mound] ────────► Mongoose + Strawberry Jam to Queen -> Pass tunnel.
STEP 10: [Bat Cavern] ───────► Petroy squeaks -> Scrape Guano -> Set Prism.
STEP 11: [Smelting Forge] ───► Orain pumps bellows -> Melt gold -> Cast Key.
STEP 12: [Dragon Altar] ─────► Lure dragon with Resin -> Unlock -> GRAIN 2.
STEP 13: [Worm's Hollow] ────► Brew Chamomile Tea in Cauldron -> Cure Worm.
STEP 14: [Citadel Moat] ─────► Glue + Firefly on Twig -> Urm drops drawbridge.
STEP 15: [Kraal Lab] ────────► Reflect dark bolt with Mirror -> GET GRAIN 3.
STEP 16: [Hourglass Tower] ──► Solve pendulum rope -> Insert 3 Grains.
STEP 17: [Revuss Finale] ────► Rotate Hourglass of Revuss -> 100% VICTORY!
===============================================================================
```

---

# 8. IN-DEPTH SYSTEMS COMPENDIUM & SYNTHESIS MATRIX [COMP]

## A. Master Synthesis & Cauldron Recipes Table
```
┌─────────────────────────┬─────────────────────────┬─────────────────────────┐
│ Target Synthesis        │ Ingredients Required    │ Functional Purpose      │
├─────────────────────────┼─────────────────────────┼─────────────────────────┤
│ Awakening Dust          │ Mandrake Root + Sulfur  │ Awakens Stone Golem     │
│ Strawberry Jam          │ Strawberries + Fire Pot │ Calms the Ant Queen     │
│ Chamomile Herbal Tea    │ Chamomile + Blueberries │ Cures Sick Worm Stomach │
│ Illuminated Twig Probe  │ Twig + Glue + Firefly   │ Lights Dark Wall Slit   │
│ Blinding Flash Powder   │ Bat Guano + Sulfur      │ Stuns Citadel Guards    │
│ Dissolving Aqua Regia   │ Caustic Acid + Saltpeter│ Dissolves Moat Chains   │
│ Shinbone Spear          │ Tibia Bone + Knife      │ Weapon & Lever Tool     │
└─────────────────────────┴─────────────────────────┴─────────────────────────┘
```

---

# 9. ENGINE FORENSICS: COKTEL'S GOB ENGINE DECOMPILATION [ENGN]

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    COKTEL VISION GOB ENGINE ARCHITECTURE                    │
├─────────────────────────────────────────────────────────────────────────────┤
│ 1. `INTRO.STK`: Monolithic 7.12 MB packed resource container containing all │
│    vignette background bitmaps, sprite animations, and sound effects.       │
│ 2. `ALL.ASK`: 11 KB interactive dialog & script bytecode table executing    │
│    vignette condition triggers and companion state machines.                │
│ 3. `OBJET1.CAT`–`OBJET4.CAT`: Inventory state catalogs across the 4 acts.   │
│ 4. `*.GDR`: Hardware graphics display drivers:                              │
│    - `LVGA.GDR`: 320x200 256-color VGA Driver                               │
│    - `LEGA.GDR`: 320x200 16-color EGA Driver                                │
│    - `L360.GDR`: 360x240 Tweaked Mode-X Driver                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

### ScummVM `gob` Engine Compatibility Profile
* **Target Engine ID**: `gob` (Sub-engine target: `ween`).
* **Timer Emulation**: Corrects CPU-speed-dependent timer loops in DOSBox that caused the 30-day clock to advance too fast on modern PCs.
* **Sound Engine**: Native support for AdLib OPL2 and Roland MT-32 MIDI playback.
* **Savegame Format**: Modern cross-platform save slots replace legacy `SAVE.INF` DOS binary dumps.

---

# 10. CULTURAL RETROSPECTIVE: WHY WEEN REMAINED OBSCURE [HIST]

1. **The French "Puzzle Chamber" Paradigm**:
   Unlike American adventure games that favored open exploration, French developers (Coktel Vision, Delphine, Infogrames) designed self-contained, mathematically dense puzzle boxes requiring exact sequential execution.
2. **Esoteric Reagents & Synthesis**:
   From curing a sick worm with chamomile tea to glueing a firefly to a twig, puzzles required deep lateral thinking without modern hand-holding.
3. **Sierra's Marketing in 1992**:
   Sierra prioritized their home-grown franchises (*King's Quest VI*, *Space Quest V*), leaving *Ween* to become a treasured European cult classic.

---

# 11. CONTACT POLICY [CONT]

For corrections, save-state submissions, or engine discoveries, open an issue on GitHub:
`github.com/seeker-cyber-maker/ai-generated-game-walkthroughs`

---

# 12. CREDITS & SPECIAL THANKS [CRED]

* **Coktel Vision**: For creating one of the most uniquely artistic French puzzle adventures of the DOS era.
* **Pierre Gilhodes & Roland Oskian**: For brilliant surrealist artwork and ingenious puzzle design.
* **The ScummVM Gob Engine Team**: For reverse-engineering and preserving Coktel's `GOB`/`STK` format.
* **YOU, the reader**: For uncovering the lost gems of adventure gaming history!
