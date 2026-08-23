# GameFAQs Formatted Text Guide Specification & Style Standard

**Standard Version**: 1.2.0 (CJayC / SBAllen Contributor Compliance & Modern Emulation Addendum)  
**Target Platform**: GameFAQs / GameSpot Plain Text Submission Queue  
**File Extension**: `.txt` (ASCII / UTF-8 Plain Text)

---

## 📏 1. Fundamental Geometry & Invariants

```text
Column 1                                                              Column 79
v                                                                             v
+-----------------------------------------------------------------------------+
| 1. Hard Maximum Line Width : 79 Characters (Never 80+)                      |
| 2. Tab Characters (\t)     : STRICTLY FORBIDDEN (Use 2 or 4 spaces only)    |
| 3. Em-Dashes (— / \u2014)  : STRICTLY FORBIDDEN (Use colons, commas, parens)|
| 4. Line Endings            : Unix (\n) or DOS (\r\n)                        |
| 5. Encoding                : Plain ASCII or standard UTF-8                  |
| 6. Trailing Whitespace     : Stripped                                       |
+-----------------------------------------------------------------------------+
```

### Why 79 Columns Instead of 80?
On classic 80-column monospaced CRT terminals, DOS editors, and the GameFAQs text viewer, writing exactly 80 characters followed by a newline (`\n`) triggers an automatic terminal line-wrap, creating an unwanted blank line after every sentence. A strict **79-column hard limit** guarantees pixel-perfect rendering across every screen and operating system.

### Why No Em-Dashes (—) or AI Prose Tropes?
Em-dashes are not native ASCII (0x2014) and frequently corrupt into Mojibake (`â€”` or `?`) in classic DOS viewers, terminal pagers, and GameFAQs submission parsers. Furthermore, overuse of em-dashes is an obvious AI prose trope. Standard hyphens (`-`), colons (`:`), commas (`,`), or parentheses `()` must be used instead.

---

## 📑 2. Table of Contents & Dot-Leader Right-Justification

The Table of Contents must use **Dot-Leaders (`....`)** extending to right-justify bracketed search codes on columns 73–79:

```text
-------------------------------------------------------------------------------
TABLE OF CONTENTS ..................................................... [00.00]
-------------------------------------------------------------------------------
  [01.00] AUTHOR'S PREFACE & RESEARCH PHILOSOPHY ....................... [PREF]
  [02.00] LEGAL DISCLAIMER & PERMITTED SITES .......................... [LEGL]
  [03.00] VERSION HISTORY ............................................. [VERS]
  [04.00] GAME BASICS & COMBAT MECHANICS .............................. [BASE]
  [05.00] COMPLETE WALKTHROUGH ........................................ [WLK00]
          - [05.01] Act I: Gladstone Keep & The Great Forests ......... [WLK01]
          - [05.02] Act II: Gorkha Swamp & Shaman's Trial ............. [WLK02]
          - [05.03] Act III: Mines of Apparitions & Draracle .......... [WLK03]
          - [05.04] Act IV: The White Tower & Gladstone Siege ......... [WLK04]
          - [05.05] Act V: City of Yvel & The Sewers .................. [WLK05]
          - [04.06] Act VI: Castle Cimmeria & Nether Mask ............. [WLK06]
  [05.00] THE CRITICAL-PATH MINIMALIST ROUTE .......................... [FAST]
  [06.00] WEAPONS, ARMOR & SPELLS COMPENDIUM .......................... [COMP]
  [07.00] SECRETS & PERMANENT MISSABLES ............................... [SECR]
  [08.00] ENGINE FORENSICS & REVERSE-ENGINEERING ...................... [ENGN]
  [09.00] SCUMMVM & MODERN EMULATION TARGET PROFILE .................. [SCUM]
  [10.00] CONTACT POLICY .............................................. [CONT]
  [11.00] CREDITS & SPECIAL THANKS .................................... [CRED]
```

---

## 🧱 3. Header & Section Dividers

Use standard double-line (`=`) dividers for major chapters and single-line (`-`) dividers for sub-sections. Every divider must span **exactly 79 characters**:

```text
===============================================================================
[04.01] ACT I: GLADSTONE KEEP & THE GREAT FORESTS                       [WLK01]
===============================================================================

-------------------------------------------------------------------------------
Gladstone Dungeons & Northlands Secret
-------------------------------------------------------------------------------
```

---

## 📦 4. Final Fantasy Style Item & Chest Checklist Boxes

---

## 🔬 4. Content Quality Invariants (The "Lands of Lore" Forensic Benchmark)

Every guide produced in this repository must meet the rigorous technical and forensic standard established in our *Lands of Lore: The Throne of Chaos* master suite. Superficial, hand-waving, or purely narrative walkthroughs are **STRICTLY PROHIBITED**. Every walkthrough must fulfill the following 7 Non-Negotiable Invariants:

```text
+-----------------------------------------------------------------------------+
| THE 7 NON-NEGOTIABLE FORENSIC CONTENT INVARIANTS                            |
+-----------------------------------------------------------------------------+
| 1. Binary Disassembly & Bytecode State Machine Mapping ([ENGN])             |
| 2. Historical Copy-Protection & Reverse-Engineered Patch Vectors            |
| 3. Hidden Spells, Easter Eggs & Deterministic PRNG Registers                |
| 4. Exhaustive Data Tables & Dynamic Item Catalogs (Zero Placeholders)       |
| 5. Dual Walkthrough Architecture (Granular Checklist + [FAST] Geodesic)     |
| 6. Historical Lineage, Design Philosophy & Cultural Retrospective ([HIST]) |
| 7. Modern Emulation Engine & ScummVM Profile ([SCUM])                       |
| 8. Prequel-to-Sequel Evolutionary Forensics & Historical Format Deltas [SEQL]|
+-----------------------------------------------------------------------------+
```

### Invariant 1: Binary Disassembly & Engine Bytecode Mapping (`[ENGN]`)
Walkthroughs must decompile the game's actual internal binary architecture:
* **Sierra AGI / SCI**: Disassemble logic scripts, object flags, and extract master vocabulary tables (`WORDS.TOK`).
* **Westwood Kyra / LoL**: Disassemble `.PAK` archives, item bitfield masks (`ALCHEMY.PAK`), and memory registers.
* **Coktel Gob**: Unpack `.STK` archives via LZSS 4096-byte ring-buffers and map the full directed state machine (`EMAJ1000.TOT`–`EMAJ1038.TOT`).

### Invariant 2: Historical Copy-Protection, DRM & Build Provenance (`[PROT]` / `[VERS]`)
Every guide must thoroughly document the contemporary copy-protection schemes and release provenance:
* **Physical Box & Manual Artifacts**:
  - *Code Wheels*: Dial-A-Pirate (*Monkey Island 1*), Voodoo Code Wheel (*Monkey Island 2*), Sector Navigators.
  - *Cardboard & Lenses*: ScumSoft keycard decoding grid (*Space Quest III*), red cellophane decoder glasses, dark-printed manual tables.
  - *Manual Lookups*: Page/line/word lookups (*Police Quest 2*, *King's Quest IV*), spellbook glyphs (*Kyrandia 2*), potion recipes (*Kyrandia 1*).
* **Media-Level & Hardware Checks**:
  - Floppy bad-track / non-standard sector interleave schemes (Keypunch, Copylock).
  - CD-ROM optical subchannel Q-data verification and MSCDEX volume label matching (`INT 2Fh, AX=1500h`).
* **Reverse-Engineered Assembly Cracks & Bypass Vectors**:
  - Document the exact x86 / 68k disassembly offsets, conditional jump opcodes (e.g. `JZ` `0x74` -> `JMP` `0xEB` or NOPing `0x90 0x90`), and register overrides (`MOV AX, 0001h`).
  - Preserve the historical computing context of how early crackers defeated manual lookups.
* **Build Provenance & Binary Hashes**:
  - Exhaustive release history: Floppy 3.5"/5.25" vs CD-ROM Talkie, EGA vs VGA, regional language editions.
  - Master binary SHA-256 checksums and exact engine interpreter build numbers.

### Invariant 3: Hidden Spells, Secrets & Session PRNG Registers
* Document all hidden spells (e.g. Hand of Fate Level 4), unlisted developer easter eggs, and secret debug shortcuts.
* Dissect pseudo-random number generators (e.g. Borland LCG `Seed = (Seed * 1103515245 + 12345) % 2^31`), differentiating true session RNG from static graphs with reused background tiles.

### Invariant 4: Complete Exhaustive Data Tables (Zero Placeholders)
* Provide complete, un-truncated tables: full 4-tier inventory catalogs (`OBJET1.CAT`–`OBJET4.CAT`), potion synthesis matrices, point ledgers, or damage/defense statistics.

### Invariant 5: Dual Walkthrough Architecture
Every guide must contain BOTH:
1. **Granular Screen-by-Screen Walkthrough**: Step-by-step solutions paired with 79-column ASCII Area Item Checklists.
2. **The Critical-Path Minimalist Route (`[FAST]`)**: A 12–18 step linear geodesic stripping away all optional backtracking for pure speedruns.

### Invariant 6: Historical Lineage, Sequel Bridges & Character Evolution (`[HIST]` / `[LORE]` / `[SEQL]`)
Every guide must trace the narrative lineage, character evolution, and thematic connections that carry forward into subsequent sequels:
* **Franchise Sequel Bridges & Character Evolution**:
  - *Sierra Police Quest & SWAT Series*: Sonny Bonds & Marie Wilkerson evolving across *PQ1*, *PQ2: The Vengeance*, *PQ3: The Kindred*, *PQ: Open Season*, and Jim Walls' *Blue Force*.
  - *Westwood Lands of Lore Series*: King Richard, Scotia's curse passing to her son Luther in *Lands of Lore II: Guardians of Destiny*, Gladstone Keep's destruction in *Lands of Lore III*, and the cosmic role of the Draracle and Arrant Rrak.
  - *Westwood The Legend of Kyrandia Trilogy*: Brandon's coronation in *Book 1*, Zanthia's solo journey to save the sinking world in *Book 2: The Hand of Fate*, and Malcolm's petrification escape and innocence trial in *Book 3: Malcolm's Revenge*.
  - *Coktel Vision Coktelverse*: Character dynamic evolution from *Ween* and *Gobliiins 1–3* into *Woodruff and the Schnibble of Azimuth* and *Lost in Time*.
* **Developer Anagrams & Cryptograms**: Unpack creator wordplay and inside jokes across franchises (e.g. *Simart* = Tramis, *Urm* = Muriel, *Revuss* = Se Sauver, *Arrant Rrak/Prac*).
* **Binary String Forensics**: Search decompiled string tables (`.ASK`, `.USA`, `.FRA`, `WORDS.TOK`, `.PAK`) for cut dialogue, developer signatures, and shared-universe continuity links.
* **Design Philosophy Retrospective**: Contrast European surrealist "puzzle chamber" paradigms with American open-world adventure traditions.

### Invariant 7: Modern Emulation & ScummVM Profile (`[SCUM]`)
Document the specific ScummVM engine kernel ID, CPU-speed timer normalization, speech/subtitle desync fixes, palette cycling emulation, and cross-platform save formats.

### Invariant 8: Prequel-to-Sequel Evolutionary Forensics & Format Deltas (`[SEQL]` / `[EVOL]`)
For every title in a franchise or engine family, the guide must explicitly document the technical and design delta between the prequel and the current installment:
* **Engine Architecture Shift**: e.g., AGI (interpreted vector/polling) -> SCI0 (OOP script state machine) -> SCI1/SCI32 (VGA/32-bit streaming); SCUMM v1–v3 (15-verb grid) -> v4/v5 (9-verb/iMUSE) -> v6/v7 (contextual cursor); Kyra 1 (simple point & click) -> Kyra 2 (alchemical cauldron) -> Kyra 3 (mood meter & 3D pre-rendered sprites).
* **User Interface & Interaction Overhaul**: How item handling, inventory limits, action hotkeys, and dialogue systems were upgraded or streamlined.
* **Audio Subsystem Progression**: Evolution from PC Speaker / 3-Voice Tandy -> AdLib / Sound Blaster FM synthesis -> Roland MT-32 multi-timbral MIDI -> Redbook CD-DA / digitized Talkie speech.
* **Copy-Protection Metamorphosis**: Evolution from printed manual symbol lookups -> code wheels (Dial-A-Pirate) -> in-game trivia prompts -> optical disc physical checks.
* **Puzzle & Death Mechanics Philosophy**: Shifts from unforgiving Sierra-style instant death and dead-ends -> fair-play LucasArts/Westwood design where items cannot be permanently missed or wasted.

---

## 🗺️ 5. Area Item Checklists & Maze Topology

Every distinct region or act must open with a 79-column ASCII checklist box:

```text
+-----------------------------------------------------------------------------+
| AREA ITEM & CHEST CHECKLIST: GLADSTONE & FORESTS                            |
|                                                                             |
| [ ] King's Royal Commission Letter (X:02, Y:01) [Gladstone Keep: Throne]    |
| [ ] 50 Gold Sovereigns ........... (X:02, Y:01) [Gladstone Keep: Treasury]  |
| [ ] Iron Broadsword .............. (X:05, Y:12) [North Forest: Stump Chest] |
| [ ] [SECRET] Elven Bow ........... (X:14, Y:03) [South Forest: Hidden Nook] |
| [ ] [RELIC] Compass .............. (X:04, Y:12) [Roland Manor Floor]        |
| [ ] [PARTY] Recruit Baccata ...... (X:03, Y:11) [Southlands Campfire]       |
+-----------------------------------------------------------------------------+
```

When documenting mazes (e.g. *Kyrandia 1* Caverns of Twilight or *Fate of Atlantis* Knossos Labyrinth):
1. **Deconstruct the Topology**: Clarify whether the maze is a true procedural generator or a static directed graph utilizing modular art tile reuse.
2. **State Variable Tracking**: Document all runtime RNG registers (e.g. `v_berry_charge`, `gem_req_slot2`).
3. **Failure Bounds**: Explicitly document step-counter expiration, trap triggers, or soft locks.

---

## 🤖 6. Automated Python Verification Script

Run this script to certify that any `.txt` file complies 100% with the standard before submission:

```python
import sys, re

def verify_gamefaqs_txt(filepath):
    with open(filepath, "r", encoding="utf-8") as f:
        lines = f.readlines()
        content = "".join(lines)
    
    errors = []
    in_toc = False
    for i, line in enumerate(lines, 1):
        clean = line.rstrip("\r\n")
        if "\t" in clean:
            errors.append(f"Line {i}: Contains TAB character.")
        if "—" in clean:
            errors.append(f"Line {i}: Contains em-dash.")
        if len(clean) > 79:
            errors.append(f"Line {i}: Exceeds 79 cols ({len(clean)} chars): \"{clean[:40]}...\"")
        if "TABLE OF CONTENTS" in clean:
            in_toc = True
        elif in_toc and clean.startswith("==="):
            in_toc = False
        if in_toc and re.search(r"\.{3,}\s+\[[A-Z0-9]+\]$", clean):
            if len(clean) != 79:
                errors.append(f"Line {i}: TOC dot-leader not aligned to col 79 (length={len(clean)})")

    if "AI Cybersecurity Researcher and Reverse-Engineer" not in content:
        errors.append("Missing exact title in Author Preface")
    if errors:
        print(f"FAILED: Found {len(errors)} formatting violations in {filepath}:")
        for err in errors[:10]:
            print("  ", err)
        return False
    print(f"PASSED: {filepath} is 100% GameFAQs compliant! Total lines: {len(lines)}")
    return True

if __name__ == "__main__":
    verify_gamefaqs_txt(sys.argv[1])
```
