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
| 3. Line Endings            : Unix (\n) or DOS (\r\n)                        |
| 4. Encoding                : Plain ASCII or standard UTF-8                  |
| 5. Trailing Whitespace     : Stripped                                       |
+-----------------------------------------------------------------------------+
```

### Why 79 Columns Instead of 80?
On classic 80-column monospaced CRT terminals, DOS editors, and the GameFAQs text viewer, writing exactly 80 characters followed by a newline (`\n`) triggers an automatic terminal line-wrap, creating an unwanted blank line after every sentence. A strict **79-column hard limit** guarantees pixel-perfect rendering across every screen and operating system.

---

## 📑 2. Table of Contents & Dot-Leader Right-Justification

The Table of Contents must use **Dot-Leaders (`....`)** extending to right-justify bracketed search codes on columns 73–79:

```text
-------------------------------------------------------------------------------
TABLE OF CONTENTS ..................................................... [00.00]
-------------------------------------------------------------------------------
  [01.00] LEGAL DISCLAIMER & PERMITTED SITES .......................... [LEGL]
  [02.00] VERSION HISTORY ............................................. [VERS]
  [03.00] GAME BASICS & COMBAT MECHANICS .............................. [BASE]
  [04.00] COMPLETE WALKTHROUGH ........................................ [WLK00]
          - [04.01] Act I: Gladstone Keep & The Great Forests ......... [WLK01]
          - [04.02] Act II: Gorkha Swamp & Shaman's Trial ............. [WLK02]
          - [04.03] Act III: Mines of Apparitions & Draracle .......... [WLK03]
          - [04.04] Act IV: The White Tower & Gladstone Siege ......... [WLK04]
          - [04.05] Act V: City of Yvel & The Sewers .................. [WLK05]
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

---

## 🔬 5. Maze Topology & Procedural Randomness Documentation

When documenting mazes, labyrinths, or random encounters (e.g. *Kyrandia 1* Caverns of Twilight or *Fate of Atlantis* Knossos Labyrinth):
1. **Deconstruct the Topology**: Clarify whether the maze is a true procedural generator or a static directed graph utilizing modular art tile reuse.
2. **State Variable Tracking**: Document all runtime RNG registers (e.g. `v_berry_charge`, `v_sun_alignment`, `gem_req_slot2`).
3. **Failure Bounds**: Explicitly warn the reader of step-counter expiration, trap triggers, or soft locks.

---

## 🕹️ 6. ScummVM & Modern Emulation Profile (`[SCUM]`)

Every retro guide must treat modern open-source engines (e.g., **ScummVM**, **DOSBox-Staging**, **PCem**) as first-class version targets:
1. **Target Engine ID**: Document the specific ScummVM engine kernel (e.g. `kyra1`, `kyra2`, `sci`, `agi`, `scumm`).
2. **Emulation Quirks & Bug Fixes**:
   - Document any audio/speech desynchronization fixes (speech vs subtitle timing).
   - Document collision detection or bounding-box clipping differences between pure DOS and modern interpreters.
   - Document palette cycling behavior (VGA DAC register cycling in dark rooms).
3. **Savegame Compatibility**: Document cross-platform save paths (`.s00`–`.s99`) versus native DOS binary snapshots.

---

## 🤖 7. Automated Python Verification Script

Run this script to certify that any `.txt` file complies 100% with the standard before submission:

```python
import sys

def verify_gamefaqs_txt(filepath):
    with open(filepath, "r", encoding="utf-8") as f:
        lines = f.readlines()
    
    errors = []
    for i, line in enumerate(lines, 1):
        clean = line.rstrip("\r\n")
        if "\t" in clean:
            errors.append(f"Line {i}: Contains TAB character.")
        if len(clean) > 79:
            errors.append(f"Line {i}: Exceeds 79 cols ({len(clean)} chars): \"{clean[:40]}...\"")
            
    if errors:
        print(f"FAILED: Found {len(errors)} formatting violations:")
        for err in errors[:10]:
            print("  ", err)
        return False
    print(f"PASSED: {filepath} is 100% GameFAQs compliant! Total lines: {len(lines)}")
    return True

if __name__ == "__main__":
    verify_gamefaqs_txt(sys.argv[1])
```
