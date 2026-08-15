# GameFAQs Formatted Text Guide Specification & Style Standard

**Standard Version**: 1.0.0 (CJayC / SBAllen Contributor Compliance)  
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
  [09.00] CONTACT POLICY .............................................. [CONT]
  [10.00] CREDITS & SPECIAL THANKS .................................... [CRED]
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

## 📦 4. Checklist & Callout Boxes (Final Fantasy Style)

Item checklists and danger warnings must use ASCII box borders (`+`, `-`, `|`) with a total width of **exactly 79 characters**:

```text
+-----------------------------------------------------------------------------+
| AREA ITEM & CHEST CHECKLIST: GLADSTONE & FORESTS                            |
|                                                                             |
| [ ] Gladstone Signet Ring ... (X:02, Y:01) [NPC: King Richard]             |
| [ ] Timothy (Companion) ..... (X:15, Y:01) [NPC: Hallway Soldier]          |
| [ ] [SECRET] Fine Broadsword  (X:08, Y:02) [Hidden Alcove: Torch Switch]    |
| [ ] [SECRET] Leather Cuirass. (X:08, Y:02) [Hidden Alcove: Torch Switch]    |
| [ ] Aloe Leaf (x3) .......... (X:08, Y:02) [Hidden Alcove: Torch Switch]    |
| [ ] [MISSABLE] Elven Longbow. (X:14, Y:08) [Northlands: 3-Click Oak Knot]  |
| [ ] Lightning Quiver (x20) .. (X:14, Y:08) [Northlands: 3-Click Oak Knot]  |
| [ ] [PERMANENT BUFF] Blue Well(X:04, Y:12) [Roland Manor: +5 Max Mana]      |
+-----------------------------------------------------------------------------+
```

---

## 🤖 5. Automated Python Verification Snippet

Run this script to verify that your plain text guide passes all GameFAQs submission rules:

```python
import sys

def validate_gamefaqs_txt(file_path):
    with open(file_path, "r", encoding="utf-8") as f:
        lines = f.readlines()
    
    errors = []
    for i, line in enumerate(lines, 1):
        clean_line = line.rstrip("\r\n")
        if "\t" in clean_line:
            errors.append(f"Line {i}: Contains TAB character (use spaces only).")
        if len(clean_line) > 79:
            errors.append(f"Line {i}: Exceeds 79 characters ({len(clean_line)} chars): '{clean_line[:40]}...'")
            
    if errors:
        print(f"FAILED: Found {len(errors)} formatting violations:")
        for err in errors[:10]:
            print("  ", err)
        return False
    else:
        print(f"PASSED: {file_path} is 100% compliant with GameFAQs 79-column standards ({len(lines)} lines).")
        return True

if __name__ == "__main__":
    validate_gamefaqs_txt(sys.argv[1])
```
