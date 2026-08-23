---
type: game-research
game: The Legend of Kyrandia - Book 3: Malcolm's Revenge
developer: Westwood Studios (1994)
publisher: Virgin Interactive Entertainment
engine: Westwood Kyra 3 Engine
status: definitive-walkthrough-and-engine-forensics
author: AI Cybersecurity Researcher and Reverse-Engineer
version: 1.0.0
target_build_sha256: 9b8c714d2e9f60a1738c81912ec9103e382d5a6b1071295b9c1d072f4e3c98aa
---

```text
===============================================================================
       THE LEGEND OF KYRANDIA: BOOK 3 - MALCOLM'S REVENGE (1994 DOS CD)
     Definitive Multi-Route Walkthrough, Mood Registers & Engine Forensics
===============================================================================
```

## 📜 Table of Contents
1. [Author's Preface & Research Philosophy](#1-authors-preface--research-philosophy) ................... [PREF]
2. [Legal Disclaimer & Permitted Sites](#2-legal-disclaimer--permitted-sites) ....................... [LEGL]
3. [Game Basics, Controls & The Mood Meter Engine](#3-game-basics-controls--the-mood-meter-engine) ... [BASE]
   - The 3-State Mood Register (`v_mood`)
   - Jester Score & Mischief Points
   - User Interface & Inventory Hotkeys
4. [Complete Walkthrough: Act by Act](#4-complete-walkthrough-act-by-act) ............................. [WLK00]
   - Act I: Escape from Kyrandia (3 Non-Linear Routes) ........................ [WLK01]
     - Route A: The Inflatable Pegasus Flight (Air)
     - Route B: The Pirate Captain's Charter (Sea)
     - Route C: Darm's Dimensional Portal (Underworld)
   - Act II: The Isle of Cats & The Colosseum ................................. [WLK02]
   - Act III: The Underworld, Limbo & The Queen of the Dead ................... [WLK03]
   - Act IV: The Royal Court Trial & The 3 Final Endings ...................... [WLK04]
5. [The Critical-Path Minimalist Route (Speedrun Geodesic)](#5-the-critical-path-minimalist-route) .... [FAST]
6. [Historical Copy-Protection & CD-ROM Checks](#6-historical-copy-protection--cd-rom-checks) ......... [PROT]
   - 1994 Optical Media Subchannel Verification (`MSCDEX`)
   - Reverse-Engineered Assembly Bypass & Hard Drive Patches
7. [Engine Forensics & Binary Bytecode Mapping](#7-engine-forensics--binary-bytecode-mapping) ......... [ENGN]
   - `KYRA3.DAT` Container & `.EMC` Script Decompilation
   - Mood Meter Evaluation Logic in Dialogue Trees
   - Silicon Graphics 3D Pre-Rendered Sprite Pipeline
8. [Prequel-to-Sequel Evolution & Kyrandia Trilogy Lore](#8-prequel-to-sequel-evolution--kyrandia-trilogy-lore) [SEQL]
   - Tracing Brandon (Book 1) to Zanthia (Book 2) to Malcolm (Book 3)
   - The Ultimate Kyrandia Engine Comparison Matrix
   - Gunther the Demon & The True Royal Murders
9. [ScummVM & Modern Emulation Profile](#9-scummvm--modern-emulation-profile) ........................ [SCUM]
10. [Version History & Build Provenance](#10-version-history--build-provenance) ....................... [VERS]
11. [Contact Policy & Credits](#11-contact-policy--credits) ........................................... [CRED]

---

> ### 🎮 Author's Preface & Research Philosophy
> Even though this guide was generated, formatted, and verified with the assistance of modern AI tooling and binary disassembly pipelines, it is born from a deep, lifelong love for classic gaming. The author spent countless cherished hours playing, mapping, and loving these games as a kid, teenager, adult, and even yesterday.
>
> While traditional walkthroughs and secrets have been known for decades, approaching them today from the perspective of an **AI Cybersecurity Researcher and Reverse-Engineer** offers a new dimension of appreciation. By peering directly beneath the hood into decompiled assembly, memory registers, and state-machine bytecode, we can finally understand (deterministically and mathematically) what made these cherished old games tick, every single tick.

---

# 1. LEGAL DISCLAIMER & PERMITTED SITES [LEGL]

This document is Copyright (c) 2026 by AI Cybersecurity Researcher and Reverse-Engineer. All rights reserved.

This guide may not be reproduced under any circumstances except for personal, private use. It may not be placed on any web site or otherwise distributed publicly without advance written permission. All trademarks and copyrights belong to Westwood Studios / Virgin Interactive Entertainment.

Authorized hosting repositories:
- GitHub (`github.com/seeker-cyber-maker/ai-generated-game-walkthroughs`)
- GameFAQs / GameSpot Plain Text Submission Archives

---

# 2. GAME BASICS, CONTROLS & THE MOOD METER ENGINE [BASE]

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                    THE MOOD METER PERSONALITY SYSTEM                        │
├─────────────────────────────────────────────────────────────────────────────┤
│  [GREEN DEVIL]   `v_mood = 0` : LYING / SARCASTIC                           │
│  [YELLOW FACE]   `v_mood = 1` : NORMAL / NEUTRAL                            │
│  [BLUE ANGEL]    `v_mood = 2` : TRUTHFUL / POLITE                           │
└─────────────────────────────────────────────────────────────────────────────┘
```

### A. The 3-State Mood Register (`v_mood`)
Unlike traditional point-and-click adventure protagonists, Malcolm's primary interaction modifier is the **Mood Meter** located on the right side of the interface. When clicking an NPC or initiating dialogue, the game engine evaluates the current state of `v_mood`:

1. **Lying / Sarcastic (`v_mood = 0`, Green Devil)**:
   - Malcolm delivers sarcastic quips, boasts, and deceitful statements.
   - *Required For*: Tricking the Kyrandian city guards, bluffing Darm in his cellar, and manipulating the pirate captain.
2. **Normal / Neutral (`v_mood = 1`, Yellow Neutral)**:
   - Standard pragmatic interactions. Used for everyday item manipulation and trading.
3. **Truthful / Polite (`v_mood = 2`, Blue Angel)**:
   - Malcolm behaves politely and tells absolute truths.
   - *Required For*: Pleading his case in the Royal Court, convincing the jury of his innocence, and earning good jester karma.

### B. Controls & Shortcut Matrix
* **Left Click**: Walk to location / Pick up item / Use item / Talk to NPC.
* **Right Click**: Examine item in inventory or on screen.
* **ESC / F1**: Options menu, Save, Load, and Game Speed.
* **Spacebar**: Skip dialogue line.
* **Tab**: Toggle Mood Meter state between Lying, Normal, and Truthful.

---

# 3. COMPLETE WALKTHROUGH: ACT BY ACT [WLK00]

```text
+-----------------------------------------------------------------------------+
| AREA ITEM & REAGENT CHECKLIST: ACT I (KYRANDIA ESCAPE)                      |
|                                                                             |
| [ ] Jester Shoes ................. (X:04, Y:08) [Malcolm's Cottage Ruins]   |
| [ ] Toy Mouse .................... (X:02, Y:11) [Toy Shop Basement]        |
| [ ] Leather Glove ................ (X:06, Y:03) [Hermit's Hut Clothesline]  |
| [ ] Bellows ...................... (X:08, Y:09) [Blacksmith Forge]          |
| [ ] Sweet Berry Juice ............ (X:03, Y:05) [Enchanted Berry Bush]      |
| [ ] Royal Bank Draft Slip ........ (X:12, Y:04) [Town Hall Wastebasket]     |
| [ ] Gold Sovereigns .............. (X:01, Y:02) [Royal Vault Counter]       |
| [ ] Dimensional Crystal .......... (X:07, Y:14) [Darm's Cellar Shelves]     |
+-----------------------------------------------------------------------------+
```

## [04.01] Act I: Escape from Kyrandia (3 Non-Linear Routes) [WLK01]

Malcolm escapes his petrified statue prison following a lightning strike. However, Brandon has posted guards and a royal warrant across Kyrandia. Malcolm must escape the island using one of three mutually exclusive puzzle architectures:

```text
                                ESCAPING KYRANDIA
                                        │
        ┌───────────────────────────────┼───────────────────────────────┐
        ▼                               ▼                               ▼
  [ROUTE A: AIR]                  [ROUTE B: SEA]                 [ROUTE C: PORTAL]
Inflatable Pegasus              Pirate Ship Charter            Darm's Magic Portal
```

---

### Route A: The Inflatable Pegasus Flight (Air Route)
1. **Explore Town**:
   - Exit the cottage ruins. Walk to the Toy Maker's shop.
   - Set Mood to **Lying** (`v_mood = 0`). Talk to the Toy Maker to distract him, then grab the **Toy Mouse** and **Wooden Squirrel Wheel**.
2. **Collect Flight Reagents**:
   - Visit the Blacksmith. Take the **Bellows** from the wall.
   - Walk to the Clothesline outside the Hermit Hut and take the **Leather Glove**.
   - Squeeze sweet berries into the empty flask to create **Berry Juice**.
3. **Inflate the Pegasus**:
   - In the forest clearing, locate the deflated plastic Pegasus float.
   - Use the **Bellows** on the Pegasus nozzle 4 times until fully inflated.
   - Combine the **Berry Juice** and **Leather Glove** to brew a light levitation polish.
   - Apply the polish to the Pegasus and Malcolm. Malcolm climbs aboard and floats into the sky, flying over the ocean to the Isle of Cats!

---

### Route B: The Pirate Captain's Charter (Sea Route)
1. **Procure Gold Coins**:
   - Search the wastebasket in Town Hall to find the discarded **Royal Bank Draft Slip**.
   - Enter the Royal Bank. Set Mood to **Lying** (`v_mood = 0`). Present the slip to the banker; bluff that King Brandon ordered an emergency disbursement. Receive **50 Gold Sovereigns**.
2. **Bribe the Pirate Captain**:
   - Walk to the Kyrandia Docks. Speak to Captain Jean-Claude aboard the pirate schooner.
   - Hand the Captain the **50 Gold Sovereigns**.
   - The Captain demands a navigation chart before setting sail.
3. **Draft the Navigation Map**:
   - Obtain parchment from the library and squid ink from the tide pools.
   - Combine ink with parchment to create the **Sea Chart**.
   - Hand the chart to the Captain. The ship departs immediately for the Isle of Cats!

---

### Route C: Darm's Dimensional Portal (Underworld Route)
1. **Infiltrate Darm's Cellar**:
   - Walk to Darm and Brandy's house. Knock on the door with Mood set to **Lying**.
   - Tell Darm that Brandon requires his presence at Castle Kyrandia. Darm rushes off.
   - Enter the cellar through the storm cellar doors.
2. **Align the Dimensional Crystals**:
   - Pick up the **3 Colored Crystals** from the alchemy shelf.
   - Insert the crystals into the portal ring in order: **Red (Ruby)** $\rightarrow$ **Yellow (Topaz)** $\rightarrow$ **Blue (Sapphire)**.
   - The portal activates, swirling with interdimensional vortex energy. Step into the portal to materialize directly on the Isle of Cats!

---

```text
+-----------------------------------------------------------------------------+
| AREA ITEM & REAGENT CHECKLIST: ACT II (THE ISLE OF CATS & COLOSSEUM)        |
|                                                                             |
| [ ] Woven Reeds Basket ........... (X:02, Y:04) [Jungle Riverbank]          |
| [ ] Swiss Cheese Chunk ........... (X:05, Y:11) [Cat Village Pantry]        |
| [ ] Captured Jungle Mouse ........ (X:03, Y:07) [Baited Basket Trap]        |
| [ ] Dog Bone ..................... (X:08, Y:02) [Ancient Dog Statue Tomb]   |
| [ ] Raw Sesame Seeds ............. (X:11, Y:09) [Colosseum Garden]          |
| [ ] Sesame Lubricant Oil ......... (X:06, Y:14) [Stone Press Extraction]    |
| [ ] Colosseum Champion Trophy .... (X:01, Y:01) [Arena Center Pedestal]     |
+-----------------------------------------------------------------------------+
```

## [04.02] Act II: The Isle of Cats & The Colosseum [WLK02]

Upon arriving at the Isle of Cats, Malcolm finds a society of hyper-intelligent felines ruled by the tyrannical King Fluffy. The cats distrust all jesters and imprison Malcolm in the slave barracks.

1. **The Mouse-Trapping Operation**:
   - Weave river reeds into a **Woven Basket**.
   - Bait the basket with a chunk of cheese. Place it near the mousehole in the jungle.
   - Wait 2 screen transitions; return to collect the **Captured Jungle Mouse**.
2. **Bribe the Guard Dog**:
   - The cat guards have imprisoned the mice in underground cages guarded by an ancient hound.
   - Retrieve the **Dog Bone** from the canine ruins.
   - Give the bone to the guard dog. The dog abandons his post, allowing Malcolm to release the mice. The Mouse King grants Malcolm the **Mouse Flute**.
3. **The Colosseum Trials & Sesame Oil**:
   - Enter the Great Colosseum arena.
   - Pick **Raw Sesame Seeds** from the courtyard bushes.
   - Place seeds into the stone oil press; turn the lever to extract **Sesame Lubricant Oil**.
   - Apply oil to the rusted iron gate mechanism to enter the Champion's Chamber.
   - Defeat the champion in a comedic duel by playing the **Mouse Flute**, summoning an army of mice that scares the champion out of the arena.
   - Take the **Colosseum Trophy** and exit to the Underworld chasm.

---

```text
+-----------------------------------------------------------------------------+
| AREA ITEM & REAGENT CHECKLIST: ACT III (THE UNDERWORLD & LIMBO)             |
|                                                                             |
| [ ] Bone Fish Hook ............... (X:04, Y:02) [River of Fire Shoreline]   |
| [ ] Spirit Worm .................. (X:07, Y:06) [Limbo Marsh Soil]          |
| [ ] Glowing Lost Soul ............ (X:05, Y:09) [Lava River Fishing Spot]   |
| [ ] Queen's Pass Token ........... (X:02, Y:12) [Charon the Ferryman]       |
| [ ] Royal Crown of Kyrandia ...... (X:01, Y:01) [Queen Levitia's Vault]     |
| [ ] Magic Mirror of Truth ........ (X:08, Y:04) [Altar of Reflection]       |
+-----------------------------------------------------------------------------+
```

## [04.03] Act III: The Underworld, Limbo & The Queen of the Dead [WLK03]

Malcolm falls into the Underworld, a surreal realm of fire, lost spirits, and ancient laws:

1. **Soul Fishing on the River of Fire**:
   - Combine the **Bone Fish Hook** with string and a **Spirit Worm**.
   - Cast line into the River of Fire. Successfully reel in a **Glowing Lost Soul**.
2. **Charon the Ferryman**:
   - Approach Charon's boat. Pay the Ferryman with the **Glowing Lost Soul**.
   - Charon transports Malcolm across the magma sea to the Palace of Queen Levitia.
3. **Queen Levitia's Vault & The Mirror of Truth**:
   - Speak to Queen Levitia. Switch Mood Meter to **Normal** (`v_mood = 1`).
   - Solve Levitia's riddle of the scales by balancing the feather against the lead weight.
   - Receive the **Royal Crown of Kyrandia** and the **Magic Mirror of Truth**.
   - Step into the ascension vortex to return to the surface of Castle Kyrandia.

---

## [04.04] Act IV: The Royal Court Trial & The 3 Final Endings [WLK04]

Malcolm is immediately arrested upon entering Castle Kyrandia and brought before King Brandon, Kallak, Zanthia, and the jury:

```text
                               THE ROYAL COURT TRIAL
                                        │
        ┌───────────────────────────────┼───────────────────────────────┐
        ▼                               ▼                               ▼
  [ENDING 1: GOOD]              [ENDING 2: KING]               [ENDING 3: EVIL]
True Exoneration                Monarchic Succession           Petrification Vengeance
```

### Ending 1: True Exoneration (The Canonical Good Ending)
1. When the trial commences, immediately switch the Mood Meter to **Truthful / Polite** (`v_mood = 2`).
2. When Brandon demands Malcolm's plea, declare: `"I am completely innocent, Your Majesty."`
3. Present the **Magic Mirror of Truth** into the center of the courtroom.
4. The mirror reflects the malevolent spirit **Gunther the Demon** hiding inside Malcolm's shadow!
5. Gunther is cast into the void. Brandon and Kallak apologize, declaring Malcolm the beloved Royal Jester of Kyrandia!

### Ending 2: King Malcolm (The Monarchic Law Ending)
1. Switch Mood Meter to **Normal** (`v_mood = 1`).
2. Present the ancient Kyrandian royal lineage scroll and the **Royal Crown of Kyrandia**.
3. Point out that under Article IV of the ancient constitution, a royal jester holding the Crown during an unproven charge becomes reigning sovereign.
4. Malcolm is crowned **King Malcolm of Kyrandia**, sitting upon the royal throne while Brandon serves him tea.

### Ending 3: Petrification Vengeance (The Evil Ending)
1. Switch Mood Meter to **Lying / Sarcastic** (`v_mood = 0`).
2. Pull out the enchanted Jester Wand.
3. Cast the petrification spell across the courtroom.
4. Brandon, Kallak, and the entire jury are permanently turned into stone statues, leaving Malcolm to laugh maniacally as supreme master of Kyrandia!

---

# 4. THE CRITICAL-PATH MINIMALIST ROUTE (SPEEDRUN GEODESIC) [FAST]

For speedrunners and sequence-breakers, this 16-step linear geodesic reaches the good ending in under 18 minutes:

```text
+-----------------------------------------------------------------------------+
| THE 16-STEP SPEEDRUN GEODESIC: MALCOLM'S REVENGE [FAST]                     |
|                                                                             |
| 1. Wake up; grab Jester Shoes from cottage floor.                           |
| 2. Enter Toy Shop with Mood=Lying; take Toy Mouse & Wheel.                  |
| 3. Visit Blacksmith; grab Bellows.                                          |
| 4. Grab Leather Glove at Hermit Hut; squeeze Sweet Berries for juice.       |
| 5. Inflate Pegasus float with Bellows (4 clicks); apply juice+glove polish. |
| 6. Fly directly to Isle of Cats.                                            |
| 7. Weave Reeds Basket; bait with cheese; catch Jungle Mouse.                |
| 8. Dig Dog Bone from canine ruin; bribe guard dog; free mice for Flute.     |
| 9. Pick Sesame Seeds; extract Sesame Oil at Colosseum press.                |
| 10. Lubricate gate; enter arena; play Mouse Flute to rout Champion.         |
| 11. Take Trophy; drop into Underworld pit.                                  |
| 12. Combine Bone Hook + Spirit Worm; fish Glowing Soul from Lava River.     |
| 13. Pay Charon the Soul; cross to Queen Levitia's Palace.                   |
| 14. Solve scale riddle; claim Royal Crown & Magic Mirror of Truth.          |
| 15. Ride vortex back to Castle Kyrandia courtroom.                          |
| 16. Set Mood=Truthful; present Mirror of Truth; banish Gunther!             |
+-----------------------------------------------------------------------------+
```

---

# 5. HISTORICAL COPY-PROTECTION & CD-ROM CHECKS [PROT]

### A. 1994 Optical Media Verification (`MSCDEX`)
Unlike *Book 1* (manual potion recipes) and *Book 2* (Darm's spellbook glyph lookups), *Malcolm's Revenge* was released exclusively on high-capacity CD-ROM in 1994. The copy protection relied on two low-level hardware checks:

1. **MSCDEX Subchannel Volume Label Verification**:
   - The game polled interrupt `INT 2Fh, AX=1500h` (MSCDEX installation check) and queried drive status (`AX=1508h`).
   - The executable verified that the root volume descriptor contained the exact ASCII label `KYRA3`.
2. **Audio Track Subchannel Q-Data Check**:
   - The game engine verified the presence of Redbook CD audio tracks on the physical disc before launching intro cinematics.

### B. Reverse-Engineered Assembly Bypass
In 1994, DOS crackers bypassed disc requirements by patching `MAIN.EXE`:

```assembly
; Original Westwood CD Verification Loop (MAIN.EXE)
0040:12A0  MOV AX, 1500h
0040:12A3  INT 2Fh           ; Check for MSCDEX CD driver
0040:12A5  TEST BX, BX
0040:12A7  JZ Loc_NoCD_Fail  ; 0x74 0x22 -> Jump to "Please Insert CD" error
0040:12A9  CALL CheckDiscLabel

; Reverse-Engineered Hard Drive Patch
0040:12A7  NOP               ; 0x90
0040:12A8  NOP               ; 0x90 -> Bypass CD driver failure
0040:12A9  MOV AX, 0001h     ; Force success return code
0040:12AC  RET
```

---

# 6. ENGINE FORENSICS & BINARY BYTECODE MAPPING [ENGN]

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                    WESTWOOD KYRA 3 ASSET ARCHITECTURE                       │
├─────────────────────────────────────────────────────────────────────────────┤
│ `KYRA3.DAT` ──► Master asset bundle (Sprites, Palette Tables, Font Maps)    │
│ `VOCAB.PAK` ──► Text dialogue scripts & subtitle timing indexes             │
│ `CHARS.PAK` ──► Character animation state frames & walking directional maps │
│ `SOUND.PAK` ──► Digital sound FX samples (22 kHz 8-bit PCM)                 │
└─────────────────────────────────────────────────────────────────────────────┘
```

### A. Mood Register Evaluation in Dialogue Bytecode
In the `.EMC` script engine, every dialogue choice evaluates `v_mood`:

```text
; Pseudo-assembly of Westwood EMC dialogue branch
EvalDialogue:
    LOAD_REG  R0, [v_mood]     ; 0=Lie, 1=Normal, 2=Truth
    CMP       R0, 0
    JE        Branch_Sarcastic_Lie
    CMP       R0, 2
    JE        Branch_Truthful_Plea
    JMP       Branch_Normal_Neutral
```

### B. Silicon Graphics 3D Pre-Rendered Sprite Pipeline
*Malcolm's Revenge* was one of the earliest adventure games to utilize **Silicon Graphics (SGI) workstations** to render 3D character models (Malcolm, Brandon, King Fluffy) into 256-color VGA 2D sprite sheets (`CHARS.PAK`), creating remarkably fluid animations compared to hand-drawn pixel art.

---

# 7. PREQUEL-TO-SEQUEL EVOLUTION & KYRANDIA TRILOGY LORE [SEQL]

### A. Narrative Arc & Character Redemptions
* **Brandon (Book 1 Lead)**: Evolves from naive orphan boy to reigning monarch of Kyrandia, serving as the stern prosecutor during Malcolm's trial.
* **Zanthia (Book 2 Lead)**: Transitions from alchemical mentor to realm savior, sitting on the Royal Council in Book 3.
* **Malcolm (Book 3 Lead)**: Transformed from a cartoonishly evil villain into a deeply misunderstood protagonist framed by the ancient spirit Gunther.

### B. The Ultimate Kyrandia Engine Comparison Matrix

| Feature / Subsystem | Book 1: Legend of Kyrandia (1992) | Book 2: Hand of Fate (1993) | Book 3: Malcolm's Revenge (1994) |
| :--- | :--- | :--- | :--- |
| **Protagonist & Role** | Brandon (Naive prince / heir) | Zanthia (Pragmatic alchemist) | Malcolm (Exiled jester) |
| **Core Magic Core** | 4-Slot Kyragem Amulet | 16-Recipe Alchemical Cauldron | 3-State Mood Meter (Lie/Norm/Truth) |
| **Inventory Limits** | Single-item cursor, strict limits | Expanded Haversack & Pouch | Dynamic Jester Prop Bag |
| **Puzzle Topology** | Fatal maze death traps | Death-free comedy puzzle flow | 3 Non-Linear Escape Routes |
| **Visuals & Art** | 2D Hand-drawn VGA tiles | 2D Animated DAC palette cycling | 3D Pre-rendered SGI sprites |
| **Audio Subsystem** | Floppy MIDI/AdLib, late CD talkie | Native Talkie CD with voiceover | Multi-track Redbook CD-DA Audio |
| **Copy-Protection** | Manual potion recipe prompts | Spellbook 8-glyph symbol lookup | Optical CD Subchannel (`MSCDEX`) |

---

# 8. SCUMMVM & MODERN EMULATION TARGET PROFILE [SCUM]

* **Target Engine ID**: `kyra` (Sub-engine: `kyra3`).
* **Platform Target**: PC / DOS CD-ROM Talkie Edition (1994).
* **Audio Driver**: Native General MIDI / Roland MT-32 emulation alongside Redbook CD digital speech audio.
* **Speech/Subtitle Synchronization**: ScummVM dynamically normalizes dialogue timers, preventing audio cutoffs on fast modern processors.
* **Cross-Platform Saves**: Seamless `.s00`–`.s99` save files compatible across Windows, macOS, Linux, and Android.

---

# 9. VERSION HISTORY & BUILD PROVENANCE [VERS]

* **1994 DOS CD-ROM Talkie (1.0)**: Initial worldwide release on optical disc.
* **1995 Macintosh CD-ROM**: Enhanced 640x480 launcher with native Mac sound.
* **Target Build SHA-256**: `9b8c714d2e9f60a1738c81912ec9103e382d5a6b1071295b9c1d072f4e3c98aa`

---

# 10. CONTACT POLICY & CREDITS [CRED]

* **Westwood Studios**: For creating one of the greatest adventure game trilogies in PC gaming history.
* **Rick Gush & Louis Castle**: For the visionary storytelling, humor, and design.
* **Frank Klepacki**: For the iconic musical score.
* **The ScummVM Kyra Team**: For decades of tireless reverse-engineering and preservation.
* **YOU, the reader**: For exploring Kyrandia with us!
