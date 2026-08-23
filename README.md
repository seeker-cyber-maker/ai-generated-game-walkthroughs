# AI-Generated Game Walkthroughs & Binary Reverse-Engineering Lab

![Are ya winning, son? Yes, Dad.](docs/assets/are-ya-winning-son.png)

> ### 🎮 Author's Preface & Research Philosophy
> Even though these guides are assembled, formatted, and mathematically validated with the assistance of modern AI tooling and binary disassembly pipelines, they are born from a deep, lifelong love for classic gaming. The author spent countless cherished hours playing, mapping, and loving these games as a kid, teenager, adult, and even yesterday.
>
> While traditional narrative walkthroughs have been known for decades and their secrets cataloged, revisiting them today from the perspective of an **AI Cybersecurity Researcher and Reverse-Engineer** offers a new dimension of appreciation. By peering directly beneath the hood into decompiled assembly, memory registers, and state-machine bytecode, we can finally understand (deterministically and mathematically) what made these cherished old games tick, every single tick.

---

## What Is Here

- Original, command-first walkthrough notes and zero-detour speedrun fast-tracks.
- Mathematical point reconciliations and decompiled state-machine blueprints.
- Complete parser vocabulary dictionaries extracted directly from master binaries (e.g., Sierra `WORDS.TOK`).
- Binary engine forensics on RNG seeds, tile bitmasks, and item respawn vectors.
- Cryptographic SHA-256 build verification targets.

## What Is Not Here

- Game executables, copyrighted resource archives, proprietary artwork, or music.
- Hallucinated or speculative web walkthrough prose.
- Unverifiable completion claims without attached disassembly or runtime traces.

---

## 📚 Current Guides Catalog

| Title | Release Year | Platform / Engine | Multi-Format Suite |
| :--- | :--- | :--- | :--- |
| **Police Quest I: In Pursuit of the Death Angel** | 1987 | Sierra AGI v2.917 | [Markdown](walkthroughs/police-quest-1-agi.md) • [79-Col Text](walkthroughs/police-quest-1-agi.txt) • [HTML App](walkthroughs/police-quest-1-agi.html) |
| **Lands of Lore: The Throne of Chaos** | 1993 | Westwood 2.5D DOS (Talkie CD) | [Markdown](walkthroughs/lands-of-lore-throne-of-chaos.md) • [79-Col Text](walkthroughs/lands-of-lore-throne-of-chaos.txt) • [HTML App](walkthroughs/lands-of-lore-throne-of-chaos.html) |
| **The Legend of Kyrandia: Book 1** | 1992 | Westwood Kyra 1 DOS (Talkie CD) | [Markdown](walkthroughs/legend-of-kyrandia-book-1.md) • [79-Col Text](walkthroughs/legend-of-kyrandia-book-1.txt) • [HTML App](walkthroughs/legend-of-kyrandia-book-1.html) |
| **The Legend of Kyrandia: Book 2 - Hand of Fate** | 1993 | Westwood Kyra 2 DOS (Talkie CD) | [Markdown](walkthroughs/legend-of-kyrandia-book-2-hand-of-fate.md) • [79-Col Text](walkthroughs/legend-of-kyrandia-book-2-hand-of-fate.txt) • [HTML App](walkthroughs/legend-of-kyrandia-book-2-hand-of-fate.html) |
| **The Legend of Kyrandia: Book 3 - Malcolm's Revenge** | 1994 | Westwood Kyra 3 DOS (Talkie CD) | [Markdown](walkthroughs/legend-of-kyrandia-book-3-malcolms-revenge.md) • [79-Col Text](walkthroughs/legend-of-kyrandia-book-3-malcolms-revenge.txt) • [HTML App](walkthroughs/legend-of-kyrandia-book-3-malcolms-revenge.html) |
| **Space Quest III: The Pirates of Pestulon** | 1989 | Sierra SCI0 (DOS EGA) | [Markdown](walkthroughs/space-quest-3-sci0.md) • [79-Col Text](walkthroughs/space-quest-3-sci0.txt) • [HTML App](walkthroughs/space-quest-3-sci0.html) |
| **Ween: The Prophecy** | 1992 | Coktel Vision Gob Engine DOS | [Markdown](walkthroughs/ween-the-prophecy.md) • [79-Col Text](walkthroughs/ween-the-prophecy.txt) • [HTML App](walkthroughs/ween-the-prophecy.html) |

---

## 📐 Formatting Standards & Verification

All monospaced text releases comply strictly with the [GameFAQs 79-Column Formatting Standard](templates/gamefaqs-formatting-standard.md) (0 lines exceeding 79 columns, 0 tab characters, dot-leader right-justified TOCs).

---

## License

The original explanatory text and reverse-engineering research notes in this repository are released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Game titles, character likenesses, and original binaries remain the property of their respective trademark and copyright holders.
