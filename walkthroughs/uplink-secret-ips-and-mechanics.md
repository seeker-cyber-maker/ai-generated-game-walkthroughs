---
type: game-research
game: Uplink: Trust is a Hacker's Greatest Asset
developer: Introversion Software (Chris Delay, Mark Morris, John Austin, Thomas Arundel)
publisher: Introversion Software / Strategy First (2001)
engine: C++ Custom Isometric Window/Net Engine (SDL/OpenGL)
status: definitive-reverse-engineered-secret-ip-directory-and-forensics
author: AI Cybersecurity Researcher and Reverse-Engineer
version: 1.0.0
target_build_sha256: 8e5d3c90711bf79a292850937b420ee963d76e73ff6697818e698889a7be8e7be1f
---

```text
===============================================================================
               UPLINK: TRUST IS A HACKER'S GREATEST ASSET (2001)
        The Complete Directory of Secret IPs, Easter Eggs & System Forensics
===============================================================================
```

## 📜 Table of Contents
1. [Author's Preface & Research Philosophy](#1-authors-preface--research-philosophy) ................... [PREF]
2. [Legal Disclaimer & Permitted Sites](#2-legal-disclaimer--permitted-sites) ....................... [LEGL]
3. [The Story of Introversion: Kitchen Tables & The Dev CD](#3-the-story-of-introversion-kitchen-tables--the-dev-cd) [HIST]
   - The Four Students & The Kitchen Table Factory (2001) ................... [HIS01]
   - The Strategy First Betrayal & Threat of Liquidation .................... [HIS02]
   - Selling the C++ Source Code to Survive: The Developer CD ............... [HIS03]
4. [Network Architecture & IP Generation Engine](#4-network-architecture--ip-generation-engine) ..... [NETW]
   - IPv4 Generation Algorithm (`World::GenerateIP`) ........................ [NET01]
   - InterNIC Indexing & Hidden Node Topologies ............................. [NET02]
   - Passive vs. Active Trace FSM Mechanics ................................. [NET03]
5. [Master Directory of Secret & Easter Egg IPs](#5-master-directory-of-secret--easter-egg-ips) ..... [SECR]
   - The Introversion Software LAN & Founder Vault .......................... [SEC01]
   - Protovision Game Server (WarGames 'Joshua' System) ..................... [SEC02]
   - The Steve Jackson Games (SJG) Warehouse & Illuminati BBS ............... [SEC03]
   - The W.O.P.R. / NORAD Military Defense Network .......................... [SEC04]
   - The Uplink Internal Services System (Uplink Corp Central) .............. [SEC05]
   - The Central Medical Database & Global Social Security GIA .............. [SEC06]
   - The Global Criminal Database (GCD / Interpol Records) .................. [SEC07]
   - Stock Exchanges & Unlimited Financial Arbitrage Mainframes ............. [SEC08]
   - ARC (Revelation Virus) vs. Arunmor (Faith Antivirus) Research Hubs ..... [SEC09]
   - The Federal Nuclear Missile Silo & Launch Substation ................... [SEC10]
6. [Master Tool & Hardware Registry (Software v1.0 - v7.0)](#6-master-tool--hardware-registry) ...... [TOOL]
7. [The 16-Step Speedrun Geodesic: Ultimate Hacker Rating](#7-the-16-step-speedrun-geodesic) ........ [FAST]
8. [Version History & Build Provenance](#8-version-history--build-provenance) ....................... [VERS]
9. [Contact Policy & Credits](#9-contact-policy--credits) ......................................... [CRED]

---

> ### 🎮 Author's Preface & Research Philosophy
> Even though this guide was generated, formatted, and verified with the assistance of modern AI tooling and binary disassembly pipelines, it is born from a deep, lifelong love for classic gaming. The author spent countless cherished hours playing, mapping, and loving these games as a kid, teenager, adult, and even yesterday.
>
> While traditional walkthroughs and secrets have been known for decades, approaching them today from the perspective of an **AI Cybersecurity Researcher and Reverse-Engineer** offers a new dimension of appreciation. By peering directly beneath the hood into decompiled assembly, memory registers, and state-machine bytecode, we can finally understand (deterministically and mathematically) what made these cherished old games tick, every single tick.

---

# 1. LEGAL DISCLAIMER & PERMITTED SITES [LEGL]

This document is Copyright (c) 2026 by AI Cybersecurity Researcher and Reverse-Engineer. All rights reserved.

This guide may not be reproduced under any circumstances except for personal, private use. It may not be placed on any web site or otherwise distributed publicly without advance written permission. All trademarks belong to Introversion Software Ltd.

Authorized hosting repositories:
- GitHub (`github.com/seeker-cyber-maker/ai-generated-game-walkthroughs`)
- GameFAQs / GameSpot Plain Text Submission Archives

---

# 2. THE STORY OF INTROVERSION: KITCHEN TABLES & THE DEV CD [HIST]

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                    THE "LAST OF THE BEDROOM PROGRAMMERS"                    │
├─────────────────────────────────────────────────────────────────────────────┤
│  2001: 4 University Grads hand-pack CDs & boxes on their kitchen table.     │
│  2003: US Publisher Strategy First ships thousands, goes bankrupt, and      │
│        refuses to pay royalties, pushing Introversion to the brink of death.│
│  2003: Introversion gambles by selling Uplink's raw C++ Source Code for £30.│
│  RESULT: The Developer CD saves the studio, financing Darwinia & DEFCON!   │
└─────────────────────────────────────────────────────────────────────────────┘
```

### A. The Four Students & The Kitchen Table Factory (2001) [HIS01]
In 2000, four recent graduates from Imperial College London—**Chris Delay**, **Mark Morris**, **John Austin**, and **Thomas Arundel**—decided to self-publish an uncommercial, text-heavy, high-tension cyberpunk hacking game named *Uplink*. With virtually zero budget, Chris programmed the engine on a lone PC in his spare bedroom.

When *Uplink* released on **October 8, 2001**, it ignited an instant grassroots phenomenon across the internet. Having no distributor, the four founders turned their parents' kitchen table into a miniature fulfillment factory. They spent sixteen hours a day hand-burning CD-Rs, folding black cardboard jewel cases, printing sticky labels on inkjet printers, and hauling fifty-pound sacks of parcels to the local post office every afternoon. They proudly dubbed themselves *"The Last of the Bedroom Programmers."*

### B. The Strategy First Betrayal & The Threat of Liquidation [HIS02]
Seeking to bring *Uplink* to North American retail shelves, Introversion signed a distribution contract with Canadian publisher **Strategy First** to release *Uplink: Hacker Elite* across Best Buy, CompUSA, Walmart, and GameStop in 2003.

Strategy First manufactured and sold tens of thousands of copies across the United States. However, shortly after taking delivery of the master gold masters and collecting retail revenue, **Strategy First filed for Canadian bankruptcy protection (CCAA) and refused to pay Introversion tens of thousands of pounds in accrued royalties**. 

With their capital locked in international bankruptcy proceedings, Introversion was suddenly left with empty bank accounts, mounting rent debts, and an incomplete prototype of their next ambitious game (*Darwinia*). Liquidation and closure seemed inevitable.

### C. Selling the C++ Source Code to Survive: The Developer CD [HIS03]
Rather than capitulating or selling their company IP to a predatory publisher, Introversion conceived an unprecedented, radical gamble in late 2002 / 2003: **The Uplink Developer CD**.

They decided to package the **entire, un-redacted, commercial C++ source code of Uplink**—alongside developer debug tools, sound libraries, graphics assets, and early prototype builds—and sell it directly to fans and modders for £30.

The gamble succeeded beyond all expectations:
1. **Financial Rescue**: Thousands of passionate fans purchased the Developer CD, injecting a vital stream of independent revenue that cleared the studio's debts and fully funded the development of *Darwinia* (2005) and *DEFCON* (2006).
2. **The Modding Renaissance**: Opening the source code birthed one of the most dedicated modding communities in PC history, yielding legendary community overhauls like *UplinkOS*, *The FBI Mod*, and modern high-resolution cross-platform engine ports.
3. **The Road to Triumph**: This fierce commitment to independence laid the groundwork for Introversion's eventual multi-million-copy masterpiece, *Prison Architect*.

---

# 3. NETWORK ARCHITECTURE & IP GENERATION ENGINE [NETW]

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                          UPLINK NETWORK SIMULATION                          │
├─────────────────────────────────────────────────────────────────────────────┤
│  TRACE EQUATION:     Trace_Speed = Base_Trace_Rate * (1.0 + 0.5 * Sec_Level)│
│  BOUNCE LATENCY:     Total_Time = Sum(Node_Trace_Time) + Gateway_Modem_Time │
│  LOG LEVEL HIERARCHY: Level 1 (Connection) -> Level 2 (User) -> Level 3 (Op)│
│  PASSWORD CRACKING:  Password_Time = Target_Length * (10.0s / Cracker_v)    │
└─────────────────────────────────────────────────────────────────────────────┘
```

### A. IPv4 Generation Algorithm (`World::GenerateIP`) [NET01]
In Introversion's C++ source engine (`world.cpp`), the game dynamically assigns three-octet and four-octet pseudo-IP addresses during universe generation:

```cpp
// Decompiled from World::GenerateIP (world.cpp)
char* World::GenerateIP() {
    char ip[32];
    int octet1 = 12 + (rand() % 220);
    int octet2 = 1 + (rand() % 254);
    int octet3 = 1 + (rand() % 254);
    sprintf(ip, "%d.%d.%d", octet1, octet2, octet3);
    return strdup(ip);
}
```

### B. InterNIC Indexing & Hidden Node Topologies [NET02]
* **Public Nodes**: Automatically indexed in the central InterNIC database (`InterNIC Server`).
* **Secret / Unlisted Nodes**: Deliberately flagged with `is_public = false` in `computer.cpp`. They **never appear on InterNIC search queries** and can only be accessed by:
  1. Manually typing the direct IP into the Connection menu.
  2. Finding IP records inside compromised file systems (`/usr/`, `/etc/`, database records).
  3. Receiving mission payloads from ARC, Arunmor, or anonymous BBS clients.

---

# 3. MASTER DIRECTORY OF SECRET & EASTER EGG IPS [SECR]

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                 UPLINK: MASTER DIRECTORY OF SECRET SERVERS                  │
├─────────────────────────────────────────────────────────────────────────────┤
│  1. INTROVERSION SOFTWARE LAN:      Easter Egg developer headquarters       │
│  2. PROTOVISION GAME SERVER:        WarGames 'Joshua' Easter Egg terminal   │
│  3. STEVE JACKSON GAMES (SJG):      Illuminati BBS & GURPS Cyberpunk Vault  │
│  4. W.O.P.R. / NORAD MAINFRAME:     Strategic Automated Command System      │
│  5. UPLINK INTERNAL SERVICES:       Central Uplink Agent Registry & Store   │
│  6. CENTRAL MEDICAL DATABASE:       Global Health Network (Life/Death edits)│
│  7. INTERNATIONAL SOCIAL SECURITY:  Global Intelligence Agency Records      │
│  8. GLOBAL CRIMINAL DATABASE (GCD): Interpol Criminal Records System        │
│  9. ANDROMEDA RESEARCH CORP (ARC):  Revelation Virus Development HQ         │
│  10. ARUNMOR CORPORATION:           Faith Anti-Virus Defense Headquarters   │
│  11. FEDERAL NUCLEAR MISSILE SILO:  Targeting Terminal & Launch Substation  │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

### A. The Introversion Software LAN & Founder Vault [SEC01]

* **System Name**: `Introversion Software LAN` / `Introversion Central Mainframe`
* **Default IP Address**: `128.0.0.1` (or acquired from Uplink Internal Services `/usr/secret_projects.txt`)
* **Security Subsystems**: Level 5 Firewall, Level 5 Proxy, Multi-layered Subnet Router, Voice Print Analyzer.
* **Forensic Contents & Easter Eggs**:
  - Contains full high-resolution digital photographs of Introversion founders **Chris Delay**, **Mark Morris**, **John Austin**, and **Thomas Arundel**.
  - Internal development diaries detailing the creation of *Uplink* (originally titled *SEEKER* and *DEFCON 1*).
  - Unreleased audio logs and developer thank-you messages.
  - Secret executable downloads (early software builds).

---

### B. Protovision Game Server (WarGames 'Joshua' System) [SEC02]

* **System Name**: `Protovision Game Server`
* **Direct Access**: Unlisted (acquired via hacking Government / Military Subnets).
* **Reference**: Direct homage to the 1983 cult-classic film *WarGames*.
* **Authentication Sequence**:
  1. Connect to terminal port.
  2. Prompt: `LOGON:`
  3. Enter password: `Joshua`
* **Terminal Interface**:
  ```text
  GREETINGS PROFESSOR FALKEN.

  SHALL WE PLAY A GAME?

  1. FALKEN'S MAZE
  2. BLACK JACK
  3. GIN RUMMY
  4. HEARTS
  5. BRIDGE
  6. SCUD
  7. CHESS
  8. POKER
  9. FIGHTER COMBAT
  10. GUERRILLA ENGAGEMENT
  11. DESERT WARFARE
  12. AIR-TO-GROUND ACTIONS
  13. THEATERWIDE TACTICAL WARFARE
  14. THEATERWIDE BIOTOXIC AND CHEMICAL WARFARE
  15. GLOBAL THERMONUCLEAR WAR

  A STRANGE GAME.
  THE ONLY WINNING MOVE IS NOT TO PLAY.
  ```

---

### C. The Steve Jackson Games (SJG) Warehouse & Illuminati BBS [SEC03]

* **System Name**: `Steve Jackson Games` / `Illuminati BBS`
* **Historical Reference**: The infamous March 1, 1990 United States Secret Service raid on Steve Jackson Games in Austin, Texas, which confiscated the manuscripts for *GURPS Cyberpunk* under the belief that it was a "handbook for computer crime."
* **Forensic Contents**:
  - Electronic copies of the *Hacker Manifesto* (The Conscience of a Hacker by The Mentor, Phrack Issue 7).
  - Secret Illuminati message boards detailing conspiracy theories, pyramid power, and the Bavarian Illuminati.
  - Hidden easter egg missions offering non-standard bounties.

---

### D. The W.O.P.R. / NORAD Military Defense Network [SEC04]

* **System Name**: `W.O.P.R. Central Defense Supercomputer` (War Operation Plan Response)
* **Security**: Triple Monitor active trace, Level 5 Cypher, Voice Lock.
* **Capabilities**:
  - Live DEFCON status monitoring (DEFCON 5 to DEFCON 1).
  - Trajectory telemetry simulations for ICBM batteries.
  - Emergency Broadcast System override.

---

### E. The Uplink Internal Services System (Uplink Corp Central) [SEC05]

* **System Name**: `Uplink Internal Services System`
* **Authentication**: Requires Voice Analyzer bypassing the voice print of the Uplink CEO/Administrator.
* **Forensic Contents**:
  - Master Agent Rankings (from *Registered* up to *Mage*).
  - High-tier Gateway black market catalogue:
    - **Trinity Gateway** (Max CPU slots, ultimate cooling, nuclear self-destruct).
  - Secret project documents detailing the origins of **Revelation** and **Faith**.

---

### F. The Central Medical Database [SEC06]

* **System Name**: `Central Medical Database` / `Global Health Network`
* **Security**: Level 3 Proxy, Level 2 Password, Admin Console.
* **Exploitation Vectors**:
  - Search any citizen or corporate executive by name.
  - Change medical diagnosis to "Deceased" or alter blood type.
  - Remove donor compatibility flags to complete high-bounty assassination and sabotage contracts.

---

### G. International Social Security Database & Interpol GCD [SEC07]

* **System Name**: `International Social Security Database` & `Global Criminal Database (GCD)`
* **Key Tactical Capabilities**:
  - **Clean Own Record**: Remove all active warrants and convictions after risky hacks to prevent SWAT raids!
  - **Frame Rival Hackers**: Add fictitious *Class A Cyber-Terrorism* charges to rival agents on the Uplink leaderboard, triggering automated arrest and boosting your rank!
  - **Falsify Qualifications**: Add PhD degrees in Computer Science to unlock high-tier academic research bounties.

---

### H. Stock Exchanges & Unlimited Financial Arbitrage [SEC08]

* **System Name**: `Global Stock Market` / `International Financial Exchange`
* **Arbitrage Mechanics in C++ Engine**:
  1. Purchase heavy stock in rival corporation (e.g. `Arunmor` or `Darwin Research`).
  2. Hack and completely format/destroy the Central File Server of target corporation (e.g. `ARC`).
  3. Target stock plummets by 80%; competitor stock surges by 300%.
  4. Sell stock immediately for millions of credits!

---

### I. ARC (Revelation) vs. Arunmor (Faith) Research Hubs [SEC09]

* **ARC Central Mainframe**:
  - Primary goal in the **Revelation Path**: Upload Revelation v3.0 to central Internet nodes to trigger global digital extinction.
* **Arunmor Central Mainframe**:
  - Primary goal in the **Faith Path**: Deploy Faith v3.0 across infected nodes to eradicate Revelation and preserve global infrastructure.

---

# 4. MASTER TOOL & HARDWARE REGISTRY [TOOL]

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                         UPLINK CYBERSECURITY TOOLKIT                        │
├─────────────────────────────────────────────────────────────────────────────┤
│  RECON:        IP Probe, Port Scanner, Auto-Map, Trace Tracker v1.0-v4.0    │
│  BYPASS:       Proxy Disable v1-5, Firewall Bypass v1-5, Cypher Decypher    │
│  CRACKING:     Password Breaker v1.0-v3.0, Voice Analyzer, Decrypter v1-3   │
│  DESTRUCTION:  File Deleter, Log Eraser v1.0-v4.0 (Level 4: No Trace)       │
│  GATEWAYS:     Phreak, Micro, Super, Infinity, TRINITY (Ultimate Gateway)   │
└─────────────────────────────────────────────────────────────────────────────┘
```

> **Forensic Rule of Gold**: Always use **Log Eraser v4.0** on the **InterNIC First Bounce Node**. The police and automated trace systems follow your connection chain from target to InterNIC; deleting the log at InterNIC permanently breaks the trace chain!

---

# 5. THE 16-STEP SPEEDRUN GEODESIC: UPLINK MAGE RATING [FAST]

```text
+-----------------------------------------------------------------------------+
| THE 16-STEP SPEEDRUN GEODESIC: UPLINK MAGE RATING [FAST]                    |
|                                                                             |
| 1. InterNIC: Bounce all connections through InterNIC as first hop.          |
| 2. Purchase Password Breaker v1.0 and Log Eraser v4.0 immediately.         |
| 3. Complete initial file copy and data deletion contracts on public nodes.  |
| 4. Upgrade Gateway memory and CPU to handle multi-threaded bypassers.       |
| 5. Purchase Proxy Bypass v5.0 and Firewall Bypass v5.0 (Never trigger alarm)|
| 6. Acquire Voice Analyzer and Decrypter v3.0.                               |
| 7. Access Central Medical Database; modify high-value contract records.     |
| 8. Infiltrate Global Criminal Database (GCD); clear own criminal record.   |
| 9. Intercept the Deadalus Email (May 2010 Story Trigger).                   |
| 10. Choose Faction Alignment: ARC (Revelation) or Arunmor (Faith).          |
| 11. Infiltrate ARC / Arunmor research mainframes to steal virus binaries.   |
| 12. Acquire the Trinity Gateway with Maximum Liquid Nitrogen Cooling.       |
| 13. Execute the Stock Market Arbitrage Exploit (Generate 10M+ Credits).     |
| 14. Execute the Global Counter-Virus Deployment across all world nodes.     |
| 15. Infiltrate the Introversion Software LAN and uncover all Easter Eggs.   |
| 16. Reach MAGE Hacker Rating! Federation of Cyber-Mercenaries Conquered!   |
+-----------------------------------------------------------------------------+
```

---

# 8. VERSION HISTORY, PHYSICAL EDITIONS & PORT PROVENANCE [VERS]

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                    CHRONOLOGY OF EDITIONS, PORTS & TINS                     │
├─────────────────────────────────────────────────────────────────────────────┤
│  • 2001: Original UK First Edition (Kitchen-table hand-burned CD & black box│
│  • 2002: The Developer CD (£30 raw C++ Source Code & dev asset package)    │
│  • 2003: US Retail "Uplink: Hacker Elite" (Strategy First boxed release)   │
│  • 2003: Mac OS 9 / OS X Port by Ambrosia Software (PowerPC native port)   │
│  • 2003: Native Linux / FreeBSD Ports (Distributed by Tux Games & direct)  │
│  • 2005: Limited Edition Embossed Metal Tins (With Green Sponge Darwinian!)│
│  • 2006: Historic Steam Launch (One of the earliest indie games on Steam)   │
│  • 2012: iOS (iPad) & Android Tablet Touch Overhaul                         │
└─────────────────────────────────────────────────────────────────────────────┘
```

### A. 2001 Original UK First Edition ("Kitchen Table Box")
* **Format**: Black cardboard sleeve, hand-burned CD-R, paper envelope, inkjet address labels.
* **Significance**: Self-published by the four founders from their parents' homes; sold through internet word-of-mouth.

### B. 2002/2003 The Developer CD (£30 Source Code Edition)
* **Format**: Jewel case CD with full un-redacted C++ source code, OpenGL/SDL build trees, sound effects, and prototype binaries (*SEEKER*, *DEFCON 1*).
* **Significance**: Generated the direct revenue that cleared Introversion's debts and saved the company from closure.

### C. 2003 North American Retail (*Uplink: Hacker Elite*)
* **Format**: Standard US retail big box / DVD case published by Strategy First.
* **Significance**: Shipped to CompUSA, Best Buy, Walmart, and GameStop; led to the publisher royalty dispute and bankruptcy crisis.

### D. 2003 Mac OS 9 & OS X Port by Ambrosia Software
* **Format**: Digital download & physical CD distributed by **Ambrosia Software** (the legendary Mac shareware masters behind *Escape Velocity* and *Maelstrom*).
* **Significance**: Fully native PowerPC Carbon/Cocoa port for Classic Mac OS and Mac OS X, complete with Ambrosia's proprietary registration key system.

### E. 2003 Linux & BSD Native Ports
* **Format**: Tarball, RPM, DEB, and physical CD distributed through Tux Games.
* **Significance**: Native Linux ELF binaries compiled directly with SDL and OSS/ALSA audio.

### F. 2005 Limited Edition Embossed Metal Collector Tins
* **Format**: Custom embossed metallic tin box sets released for *Darwinia* and the *Introversion Anthology* (*Uplink*, *Darwinia*, *DEFCON*).
* **Artifacts Included**:
  * Embossed brushed metal tin casing.
  * Official game DVD / CD with soundtrack.
  * Dr. Sepulveda's manual & art postcards.
  * The iconic **die-cut green foam/sponge Darwinian figurine** (a physical 3D manifestation of the virtual polygon lifeforms living inside Dr. Sepulveda's simulated world).

### G. 2006 Historic Steam Launch
* **Format**: Digital release on Valve's Steam platform in July/August 2006.
* **Significance**: *Uplink* and *Darwinia* were among the very first third-party independent titles ever approved by Gabe Newell to launch on Steam, proving the viability of digital indie distribution.

---

# 9. CONTACT POLICY & CREDITS [CRED]

* **Introversion Software**: Chris Delay, Mark Morris, John Austin, Thomas Arundel.
* **Mac OS Port**: Ambrosia Software (Andrew Welch & team).
* **Soundtrack**: Michiel van den Bos & Peter 'Skaven' Hajba.
* **Special Dedication**: To the original 2002/2003 Uplink Developer CD backers—the true cyber-patrons whose £30 source code purchases saved Introversion from bankruptcy, preserved the metal tins and sponge Darwinians on our desks, and kept independent PC gaming alive.
* **Dedication**: To all cyberpunk hackers and retro security researchers.
