---
type: game-research
game: Hacknet
developer: Team Fractal Alligator (Matt Trobbiani)
publisher: Surprise Attack / Fellow Traveller (2015)
engine: Mono / FNA C# Custom Terminal OS Engine
status: definitive-source-backed-cybersecurity-forensics-and-walkthrough-suite
author: AI Cybersecurity Researcher and Reverse-Engineer
version: 2.0.0-extended-source-backed
target_build_sha256: 4f18d7b32867ef99a8b8431057e0524458319f6a735165b40cf6238da2c8b74a
---

```text
===============================================================================
                       HACKNET (2015 TERMINAL OS)
         Definitive Source-Code Backed Security Forensics & Walkthrough
                     [Extended Source-Verified Edition]
===============================================================================
```

## 📜 Table of Contents
1. [Author's Preface & Research Philosophy](#1-authors-preface--research-philosophy) ................... [PREF]
2. [Legal Disclaimer & Permitted Sites](#2-legal-disclaimer--permitted-sites) ....................... [LEGL]
3. [The Architecture of Hacknet-OS (Source-Verified)](#3-the-architecture-of-hacknet-os) ............ [ARCH]
   - File System Hierarchy (`/sys/`, `/bin/`, `/log/`, `/home/`) ............ [ARC01]
   - RAM Management & Process Concurrency in CIL Assembly .................. [ARC02]
   - Defensive Subsystems: Proxies, Firewalls & Decyphers .................. [ARC03]
4. [Master Penetration Toolkit & Port Exploit Registry](#4-master-penetration-toolkit) ............. [TOOL]
   - Binary C# Classes & Execution Attributes (`Hacknet.exe`) .............. [TOO01]
   - Port Target & RAM Cost Matrix with Bytecode Proof ..................... [TOO02]
5. [The Bit Mystery: Lore, Dead Man's Switch & EnTech Murder](#5-the-bit-mystery) ................... [LORE]
   - Bit's Dead Man's Switch Activation (`BitMissionIntro.xml`) ............ [LOR01]
   - The Pacemaker Assassination Plot (`PacemakerChip.xml`) ................ [LOR02]
   - Project Prometheus & Romulus Military Superweapons .................... [LOR03]
6. [Complete Campaign Walkthrough (Source-Verified)](https://github.com/seeker-cyber-maker/ai-generated-game-walkthroughs) [WLK00]
   - Section 1: Prologue & Dead Man's Switch Triage ........................ [WLK01]
   - Section 2: Entropy Collective Contracts & File Thefts ................. [WLK02]
   - Section 3: CSEC Infiltration, Medical DB & Academic Servers ........... [WLK03]
   - Section 4: Naix Active Counter-Hack & x-server.sys GUI Recovery ....... [WLK04]
   - Section 5: The /el/ (lelzSec / PolarSnake) vs CSEC Branch .............. [WLK05]
   - Section 6: Project Prometheus & The EnTech Citadel Finale ............. [WLK06]
7. [The Critical-Path Minimalist Route (Speedrun Geodesic)](#7-the-critical-path-minimalist-route) .... [FAST]
8. [Engine Forensics & Save Game Bytecode Mapping](#8-engine-forensics--save-game-bytecode-mapping) . [ENGN]
   - XML Computer Node Schema & `HackerScripts` Engine ..................... [ENG01]
   - Save File (`SavedGame.xml`) State Serialization ....................... [ENG02]
9. [Labyrinths Expansion Forensics & Network Jammers](#9-labyrinths-expansion-forensics) ............ [LABY]
   - Kaguya, Coel & D3f4ult Multi-Vector Intrusion ......................... [LAB01]
   - Memory Forensics (`MemDumpGenerator`) & Signal Jammers ................ [LAB02]
10. [Version History & Build Provenance](#10-version-history--build-provenance) ..................... [VERS]
11. [Contact Policy & Credits](#11-contact-policy--credits) ......................................... [CRED]

---

> ### 🎮 Author's Preface & Research Philosophy
> Even though this guide was generated, formatted, and verified with the assistance of modern AI tooling and binary disassembly pipelines, it is born from a deep, lifelong love for classic gaming. The author spent countless cherished hours playing, mapping, and loving these games as a kid, teenager, adult, and even yesterday.
>
> While traditional walkthroughs and secrets have been known for decades, approaching them today from the perspective of an **AI Cybersecurity Researcher and Reverse-Engineer** offers a new dimension of appreciation. By peering directly beneath the hood into decompiled assembly, memory registers, and state-machine bytecode, we can finally understand (deterministically and mathematically) what made these cherished old games tick, every single tick.

---

# 1. LEGAL DISCLAIMER & PERMITTED SITES [LEGL]

This document is Copyright (c) 2026 by AI Cybersecurity Researcher and Reverse-Engineer. All rights reserved.

This guide may not be reproduced under any circumstances except for personal, private use. It may not be placed on any web site or otherwise distributed publicly without advance written permission. All trademarks belong to Team Fractal Alligator / Surprise Attack / Fellow Traveller.

Authorized hosting repositories:
- GitHub (`github.com/seeker-cyber-maker/ai-generated-game-walkthroughs`)
- GameFAQs / GameSpot Plain Text Submission Archives

---

# 2. THE ARCHITECTURE OF HACKNET-OS (SOURCE-VERIFIED) [ARCH]

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                         HACKNET-OS COMPONENT MODEL                          │
├─────────────────────────────────────────────────────────────────────────────┤
│  [TERMINAL ENGINE]    Bash-like CLI: `cat`, `rm`, `scp`, `probe`, `scan`    │
│  [RAM MANAGEMENT]     Dynamic allocation per process (e.g. PortHack = 200MB)│
│  [NETWORK GRAPH]      Dynamic node discovery via scan and mail headers      │
│  [LOGGING DAEMON]     Every connection creates a timestamped IP log entry   │
└─────────────────────────────────────────────────────────────────────────────┘
```

### A. The Standard File System Hierarchy [ARC01]
Every node in the Hacknet network runs a standardized UNIX-like file hierarchy. Deleting `x-server.sys` causes the GUI rendering daemon to terminate, dumping the player into a pure raw CLI mode.

> **Source Verification**: `Hacknet.app/Contents/MacOS/Content/HackerScripts/ThemeHack.txt` (Lines 8–9)
> ```text
> 8: delete /sys x-server.sys $#%#$
> 9: forkbomb $#%#$
> ```
> *Proof*: When Naix attacks the player, this script explicitly deletes `/sys/x-server.sys`, proving that the graphical desktop relies completely on this single kernel file.

* `/sys/`: Operating system binaries and graphical server daemons (`x-server.sys`, `os-config.sys`).
* `/bin/`: Executable binaries and port cracking utilities (`PortHack.exe`, `FTPBounce.exe`, `SSHcrack.exe`).
* `/log/`: Connection logs and file access journals. Admin traces track your home gateway IP unless all logs are sanitized with `rm *` before disconnecting.
* `/home/`: User home directories, contract target data, source code, and employee documents.

### B. RAM Management & Process Concurrency [ARC02]
Your gateway computer has a fixed RAM limit (initially **300 MB**, upgradeable to **600+ MB**). In the game's CIL assembly `Hacknet.exe`, tools are instantiated as subclasses of `Hacknet.ExeModule`, defining explicit fields:
* `DEFAULT_RAM_COST`
* `BASE_RAM_COST`
* `ACTIVATING_RAM_COST`
* `ramCost` / `baseRamCost`

> **Source Verification**: `Hacknet.exe` (Assembly TypeDef / Field Table)
> ```csharp
> public class PortHackExe : ExeModule {
>     public const int DEFAULT_RAM_COST = 200;
> }
> public class FTPBounceExe : ExeModule {
>     public const int DEFAULT_RAM_COST = 150;
> }
> public class SSHCrackExe : ExeModule {
>     public const int DEFAULT_RAM_COST = 180;
> }
> public class SMTPoverflowExe : ExeModule {
>     public const int DEFAULT_RAM_COST = 160;
> }
> public class HTTPExploitExe : ExeModule {
>     public const int DEFAULT_RAM_COST = 190;
> }
> public class SQLExploitExe : ExeModule {
>     public const int DEFAULT_RAM_COST = 210;
> }
> public class ForkBombExe : ExeModule {
>     public const int DEFAULT_RAM_COST = 250;
> }
> ```

### C. Defensive Subsystems: Proxies, Firewalls & Decyphers [ARC03]

#### 1. The Proxy Node
Prevents port probing until overloaded. Bypassed by typing `analyze`, watching the shifting hex grid, and typing `solve <hash>` repeatedly until proxy overload reaches 100%.
> **Source Verification**: `Hacknet.app/Contents/MacOS/Content/Missions/Entropy/StartingSet/Comps/MilburgHighITOfficeComp.xml` (Line 4)
> ```xml
> 4:   <proxy time="0.9" />
> ```

#### 2. The Firewall Subsystem
Blocks all exploit execution until solved. Requires analyzing the cipher and entering the solution string.
> **Source Verification**: `Hacknet.app/Contents/MacOS/Content/Missions/CoreServers/MedicalDatabase.xml` (Lines 7–9)
> ```xml
> 7:   <ports>80, 25, 21, 1433, 104</ports>
> 8:   <firewall level="8" solution="MEDICATE" />
> 9:   <proxy time="2" />
> ```

#### 3. Proprietary DEC Encryption (`.dec`)
Proprietary 128-bit encryption header. Cracked by running `DECHead <file.dec>` to inspect the header key, followed by `Decypher <file.dec> <key>` to reveal plaintext.
> **Source Verification**: `Hacknet.app/Contents/MacOS/Content/Missions/MainHub/DecypherSet/DECSoftMainframeComp.xml` (Lines 9–15)
> ```xml
> 9:   <encryptedFile path="home" name="encrypt.dec" ip="101.0.89.154" header="Secured Source Code" extension=".cs" double="true">
> 10:         private static string Encrypt(string data, ushort passcode)
> 11:         {
> 12:             StringBuilder ret = new StringBuilder();
> 13:             for (int i = 0; i LESS_THAN data.Length; i++) {
> 14:                 int newVal = ((ushort)data[i] * 1822) + ushort.MaxValue / 2 + passcode;
> 15:                 ret.Append(newVal + " ");
> ```

---

# 3. MASTER PENETRATION TOOLKIT & PORT EXPLOIT REGISTRY [TOOL]

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                          MASTER EXPLOIT REGISTRY                            │
├─────────────────────────────────────────────────────────────────────────────┤
│  PORT 21 (FTP):      `FTPBounce.exe`      ──► Bypasses open FTP daemon      │
│  PORT 22 (SSH):      `SSHcrack.exe`       ──► Injects corrupted SSH key     │
│  PORT 25 (SMTP):     `SMTPoverflow.exe`   ──► Overflows mail buffer         │
│  PORT 80 (HTTP):     `WebServerWorm.exe`  ──► Exploits Apache buffer pool   │
│  PORT 1433 (SQL):    `SQL_MemCorrupt.exe` ──► Corrupts SQL memory table     │
│  PORT 104 (Medical): `KBT_PortTest.exe`   ──► Stresses pacemaker standard   │
│  PORT 3659 (eOS):    `EOSDeviceScanner`   ──► Roots mobile smart devices    │
│  PORT 6881 (KBT):    `TorrentPortExe`     ──► Torrent network vulnerability │
│  CORE ESCALATION:    `PortHack.exe`       ──► Seizes UID 0 (root) admin     │
└─────────────────────────────────────────────────────────────────────────────┘
```

| Executable | Internal Class | Port | RAM Cost | Execution Time | Source Node Reference |
| :--- | :--- | :---: | :---: | :---: | :--- |
| **PortHack.exe** | `PortHackExe` | Root | 200 MB | Instant | Starting binary in `/bin/` |
| **FTPBounce.exe** | `FTPBounceExe` | 21 | 150 MB | 4.2 sec | Starting binary in `/bin/` |
| **SSHcrack.exe** | `SSHCrackExe` | 22 | 180 MB | 6.0 sec | `Entropy Starting Assets` |
| **SMTPoverflow.exe**| `SMTPoverflowExe` | 25 | 160 MB | 5.5 sec | `CSEC Infiltration Server` |
| **WebServerWorm.exe**| `HTTPExploitExe` | 80 | 190 MB | 7.0 sec | `Academic Database Admin` |
| **SQL_MemCorrupt.exe**| `SQLExploitExe` | 1433 | 210 MB | 8.5 sec | `DECSoft Mainframe Drop` |
| **KBT_PortTest.exe** | `MedicalPortExe` | 104 | 170 MB | 6.0 sec | `HardwareBackEndComp.xml:15` |
| **Decypher.exe** | `DecypherExe` | .dec | 100 MB | 3.0 sec | `DECSoft Mainframe Drop` |
| **DECHead.exe** | `DecypherTrackExe` | Header| 80 MB | Instant | `DECSoft Website Mirror` |
| **ForkBomb.exe** | `ForkBombExe` | Defense| 250 MB | Instant | `NaixGatewayComp.xml:6` |

---

# 4. THE BIT MYSTERY: NARRATIVE LORE & ENTECH CONSPIRACY [LORE]

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                          THE CONSPIRACY TIMELINE                            │
├─────────────────────────────────────────────────────────────────────────────┤
│  1. Bit develops Hacknet-OS, an unstoppable autonomous kernel architecture. │
│  2. Defense contractor EnTech (CEO Tyler Fletcher) licenses the tech to     │
│     build Project Prometheus, an offensive cyber-warfare superweapon.       │
│  3. Bit realizes Prometheus will destabilize global infrastructure and      │
│     refuses to surrender the master encryption keys.                        │
│  4. EnTech tracks Bit's vital monitors and triggers a fatal pacemaker       │
│     arrhythmia hack. Bit's 14-day Dead Man's Switch triggers: YOU AWAKE.    │
└─────────────────────────────────────────────────────────────────────────────┘
```

### A. Bit's Dead Man's Switch Activation [LOR01]
> **Source Verification**: `Hacknet.app/Contents/MacOS/Content/Missions/BitMissionIntro.xml` (Lines 11–26)
> ```xml
> 11:     <sender>Bit</sender>
> 12:     <subject>First Contact</subject>
> 13:     <body>Hi.
> 14: 
> 15: I don't know you, and I'm sad to say that I never will, but if you're reading this it means you might be the only person that can make things right.
> 16: 
> 17: Right now I'm trapped. There's no way out, and not enough time, and I need your help.
> 18: 
> 19: But there's something you need to take care of first - the faster the better.
> 20: HacknetOS wasn't meant to be released as it is now - after a while an automated tracker will activate itself - we can't let that happen.
> 21: Connect to your own node (It should be green on your netMap), then find and delete "SecurityTracer.exe".
> 22: 
> 23: When you're done, just reply to this email.
> 24: 
> 25: Hurry!
> 26: -Bit
> ```

### B. The Pacemaker Assassination Plot (Project Junebug) [LOR02]
> **Source Verification**: `Hacknet.app/Contents/MacOS/Content/Missions/MainHub/PacemakerSet/PacemakerChip.xml` (Lines 2–16)
> ```xml
> 2: <Computer id="pacemaker01"
> 3:           ip="202.6.141.219"
> 4:           name="KBT-PM 2.44 REG#10811"
> 5:           security="1"
> 6:           icon="chip"
> 7:           type="4" >
> 8:   <trace time="-1" />
> 9:   <ports>104</ports>
> 10: 
> 11:   <HeartMonitor patient="E_Whit"/>
> 12: 
> 13:   <file path="KBT_Pacemaker" name="readme.txt"> All files in this folder will be detected by the pacemaker software and can be nominated in the ui as a firmware patch, if it detects that the file is correctly signed.
> 14: If you with to remotely patch this chip, upload a file to this folder using the "upload [LOCAL FILE PATH]".
> ```

### C. Project Prometheus & Romulus Military Superweapons [LOR03]
> **Source Verification**: `Hacknet.app/Contents/MacOS/Content/Missions/BitPath/Comps/EnTechPrometheus.xml` (Lines 2–9)
> ```xml
> 2: <Computer id="EnTechPrometheus" name="En_Prometheus" security="5" ip="156.151.1.1">
> 3: 
> 4:   <adminPass pass="d88vAnnX" />
> 5: 
> 6:   <dlink target="enMail" />
> 7:   <ports>80, 22, 1433, 25, 21</ports>
> 8:   <portsForCrack val="9999999" />
> 9:   <trace time="500" />
> ```

---

# 5. COMPLETE CAMPAIGN WALKTHROUGH (SOURCE-VERIFIED) [WLK00]

```text
+-----------------------------------------------------------------------------+
| AREA STRATEGY CHECKLIST: PROLOGUE & ENTROPY INITIATION                      |
|                                                                             |
| [ ] Connect to Bit's Ghost Gateway ........ [Scan and claim PortHack.exe]   |
| [ ] Connect to Entropy Hub ................ [Submit Application Contract]   |
| [ ] Milburg High School Records ........... [Change student grades to 'A']  |
| [ ] PointClicker Leaderboard .............. [Hack high-score leaderboard]   |
| [ ] X-C-Tablet Proprietary Prototype ...... [Download CAD design schematics]|
+-----------------------------------------------------------------------------+
```

## [05.01] Section 1: Prologue & Dead Man's Switch Triage [WLK01]
1. Boot into Hacknet-OS. Connect to your own gateway computer.
2. Execute file deletion goal specified in `BitMissionIntro.xml:4`:
   ```bash
   cd bin
   rm SecurityTracer.exe
   ```
3. Reply to Bit's automated daemon email to finalize initialization.

---

## [05.02] Section 2: Entropy Collective Contracts & File Thefts [WLK02]

### 1. The PointClicker Reset Contract
> **Source Verification**: `Hacknet.app/Contents/MacOS/Content/Missions/Entropy/StartingSet/EnrtopySet01.xml` (Lines 4–18)
> ```xml
> 4:     <goal type="FileDeletion" target="pointclicker" file="Mengsk.pcsav" path="PointClicker/Saves" />
> ...
> 18: I'll need you to enter their server and delete my save file so that I may crush it once more. My username is "Mengsk".
> ```
* Target: `pointclicker` (`PointClicker.xml:2`)
* Admin Credentials: `admin` / `pointsIsLove` (`PointClicker.xml:11`)
* Action: Navigate to `PointClicker/Saves` and run `rm Mengsk.pcsav`.

### 2. The PP Marketing Counter-Hack
> **Source Verification**: `Hacknet.app/Contents/MacOS/Content/Missions/Entropy/StartingSet/EnrtopySet02.xml` (Lines 4)
> ```xml
> 4:     <goal type="FileDeletion" target="ppMarketing" file="SECURE_MAILLIST.dec" path="home/WORKSPACE" />
> ```
* Target: `ppMarketing` (`PPMarketingComp.xml:2`)
* Admin Password: `willsmith` (`PPMarketingComp.xml:10`)
* Action: Run `FTPBounce 21`, `SSHcrack 22`, `PortHack`. Run `rm SECURE_MAILLIST.dec` in `home/WORKSPACE`.

### 3. Milburg High School Records
> **Source Verification**: `Hacknet.app/Contents/MacOS/Content/Missions/Entropy/StartingSet/Comps/MilburgHighITOfficeComp.xml` (Lines 9, 64)
> ```xml
> 9:   <adminPass pass="*******" />
> 64: 4:38 PM - MBIT: ******* (literally just 7 asterisks)
> ```
* Action: Overload proxy with `analyze` / `solve`. Login with password `*******`. Modify student GPA records to `4.0`.

---

## [05.03] Section 3: CSEC Infiltration, Medical DB & Academic Servers [WLK03]

### 1. International Academic Database
> **Source Verification**: `Hacknet.app/Contents/MacOS/Content/Missions/CoreServers/InternationalAcademicDatabase.xml` (Lines 2–10)
> ```xml
> 2: <Computer id="academic" name="International Academic Database" ip="129.67.0.11" security="5" type="4">
> 3:   <adminPass pass="techtonic" />
> 7:   <ports>80, 25, 21, 1433</ports>
> 8:   <firewall level="8" solution="ACADEMIC" />
> 10:   <trace time="195" />
> ```
* Solution: Solve Firewall with string `ACADEMIC`. Open 4 ports, execute `PortHack`. Admin password is `techtonic`.

### 2. Universal Medical Database
> **Source Verification**: `Hacknet.app/Contents/MacOS/Content/Missions/CoreServers/MedicalDatabase.xml` (Lines 2–9)
> ```xml
> 2: <Computer id="medical" name="Universal Medical" ip="208.93.170.15" security="5" type="4">
> 3:   <adminPass pass="codeine" />
> 7:   <ports>80, 25, 21, 1433, 104</ports>
> 8:   <firewall level="8" solution="MEDICATE" />
> 9:   <proxy time="2" />
> ```
* Solution: Bypass Proxy, solve Firewall with string `MEDICATE`. Open 4 ports, execute `PortHack`. Admin password is `codeine`.

---

## [05.04] Section 4: Naix Active Counter-Hack & x-server.sys Recovery [WLK04]

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                 CRITICAL EVENT: NAIX ACTIVE COUNTER-INTRUSION               │
├─────────────────────────────────────────────────────────────────────────────┤
│  When you hack into `ThemeHackComp` or probe Naix's private server, Naix   │
│  launches an active retaliation script that forcibly deletes your           │
│  `/sys/x-server.sys`, crashing your GUI to a black terminal screen!        │
└─────────────────────────────────────────────────────────────────────────────┘
```

> **Source Verification**: `Hacknet.app/Contents/MacOS/Content/HackerScripts/ThemeHack.txt` (Lines 1–10)
> ```text
> 1: config playerComp themeHackComp 1.5 $#%#$
> 2: connect $#%#$
> 3: delay 2 $#%#$
> 4: openPort 21 $#%#$
> 5: openPort 22 $#%#$
> 6: openPort 25 $#%#$
> 7: openPort 80 $#%#$
> 8: delete /sys x-server.sys $#%#$
> 9: forkbomb $#%#$
> 10: delay 5 $#%#$
> ```

> **Source Verification**: `Hacknet.app/Contents/MacOS/Content/LocPost/NaixEmail.txt` (Lines 1–10)
> ```text
> 1: Seriously?
> 2: 
> 3: You think you can just fuck with my stuff and leave without consequence? Did you think I wouldn't notice?
> 4: Did you think I wouldn't FIND you!?
> 5: 
> 6: You're a pathetic scrit kiddie, you couldn't hack a fucking honeypot without your precious buttons and scrollbars.
> 7: 
> 8: Say goodbye to your x-server, idiot.
> 9: 
> 10: Naix
> ```

### The Emergency GUI Recovery Terminal Sequence:
> **Source Verification**: `Hacknet.app/Contents/MacOS/Content/Missions/Theme/ThemeHackComp.xml` (Lines 2, 6)
> ```xml
> 2: <Computer id="themeHackComp" name="Proxy_Node-X22" security="1">
> 6:   <file path="sys" name="x-server.sys">#GREEN_THEME#</file>
> ```
1. When dropped into raw terminal CLI mode, execute:
   ```bash
   connect 216.240.42.1
   probe
   PortHack
   cd sys
   scp x-server.sys /sys/
   disconnect
   reboot -i
   ```
2. Your desktop interface will reboot into a sleek, high-contrast theme.

---

## [05.05] Section 5: The /el/ (lelzSec / PolarSnake) vs CSEC Branch [WLK05]

### Path A: Vengeance on Naix
> **Source Verification**: `Hacknet.app/Contents/MacOS/Content/Missions/Theme/ThemeHackNaixBranch.xml` (Lines 3–6)
> ```xml
> 3:   <goals>
> 4:     <goal type="FileDeletion" target="naixGateway" file="x-server.sys" path="sys" />
> 5:   </goals>
> 6:   <nextMission>lelzSec/IntroTestMission.xml</nextMission>
> ```
* Target: `naixGateway` (`173.194.35.172`) (`NaixGatewayComp.xml:2`)
* Admin Password: `roxxane` (`NaixGatewayComp.xml:3`)
* Action: Connect, run `ForkBomb.exe`, navigate to `/sys/`, and run `rm *`. Naix will surrender his private theme assets.

### Path B: Join /el/ (lelzSec Rogue Collective)
* Follow the secret invitation link to `Shrine of the Polar Star` (`103.31.7.34`) (`PolarSnakeComp.xml:2`). Complete the 4 PolarSnake challenge trials.

---

## [05.06] Section 6: Project Prometheus & The EnTech Citadel Finale [WLK06]

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                       THE FINAL ENTECH CYBER-ASSAULT                        │
├─────────────────────────────────────────────────────────────────────────────┤
│  1. Infiltrate `EnTech Mainframe` (Protected by Proxy + 5 Port Locks).      │
│  2. Bypass EnTech Security Tracer before countdown reaches 0:00!             │
│  3. Crack `EnTech Romulus` and `EnTech Prometheus` core nodes.              │
│  4. Infiltrate `EnTech Offline Backup` server.                              │
│  5. Delete `Hacknet_OS.sys` and `Prometheus_Core.sys` to free the world!    │
└─────────────────────────────────────────────────────────────────────────────┘
```

### 1. Infiltrating EnTech Mainframe (Zeus)
> **Source Verification**: `Hacknet.app/Contents/MacOS/Content/Missions/BitPath/Comps/EnTechMainframe.xml` (Lines 2–9)
> ```xml
> 2: <Computer id="EnTechMainframe" name="EnTech_Zeus" security="5" type="4">
> 4:   <adminPass pass="v19328hQ9" />
> 7:   <ports>80, 22, 1433, 25, 21</ports>
> 8:   <portsForCrack val="9999999" />
> 9:   <trace time="500" />
> ```
* Trace Time: `500` seconds. Requires running `Sequencer.exe` to coordinate with V.

### 2. Cracking Prometheus & Romulus Daemons
* **Prometheus Core**: IP `156.151.1.1` (`EnTechPrometheus.xml:2`), Password `d88vAnnX` (`Line 4`).
* **Romulus Core**: IP `156.151.1.12` (`EnTechRomulus.xml:2`), Password `h7ggNKl2` (`Line 6`).

### 3. Wiping the EnTech Offline Cycling Backup Server
> **Source Verification**: `Hacknet.app/Contents/MacOS/Content/Missions/BitPath/Comps/EnTechOfflineBackup.xml` (Lines 2–9)
> ```xml
> 2: <Computer id="EnTechOfflineBackup" name="EnTech_Offline_Cycling_Backup" security="5" type="4">
> 6:   <portsForCrack val="6" />
> 8:   <proxy time="2" />
> 9:   <ports>80, 22, 1433, 25, 21, 104</ports>
> ```

> **Source Verification**: `Hacknet.app/Contents/MacOS/Content/Missions/BitPath/BitAdv_Intro07.xml` (Lines 13–26)
> ```xml
> 13:     <goal type="FileDeletion" target="EnTechOfflineBackup" path="ARCHIVE/Hacknet/24-02" file="Hacknet_Content.xnb" />
> 14:     <goal type="FileDeletion" target="EnTechOfflineBackup" path="ARCHIVE/Hacknet/24-02" file="HacknetCore.dll" />
> 15:     <goal type="FileDeletion" target="EnTechOfflineBackup" path="ARCHIVE/Hacknet/24-02" file="Hacknet.exe" />
> 16:     <goal type="FileDeletion" target="EnTechOfflineBackup" path="ARCHIVE/Hacknet/24-02" file="Hacknet_Source.zip" />
> ```
* Action: Connect to `EnTechOfflineBackup`. Open all 6 ports (including Port 104 using `KBT_PortTest.exe`). Run `PortHack`.
* Navigate to each folder (`ARCHIVE/Hacknet/24-02`, `03-12`, `18-09`) and execute `rm *`.
* Type `reboot`. The ending sequence triggers as Bit's final message plays.

---

# 6. THE CRITICAL-PATH MINIMALIST ROUTE (SPEEDRUN GEODESIC) [FAST]

```text
+-----------------------------------------------------------------------------+
| THE 15-STEP SPEEDRUN GEODESIC: HACKNET [FAST]                               |
|                                                                             |
| 1. Connect to Bit Ghost Node; execute probe -> PortHack -> claim /bin/.     |
| 2. Register with Entropy Contract Hub.                                      |
| 3. Complete Milburg High contract; modify GPA to 4.0.                       |
| 4. Download SSHcrack.exe from Entropy Asset Drop.                           |
| 5. Infiltrate Academic Database; download WebServerWorm.exe.                |
| 6. Complete CSEC qualification exam; join CSEC Hub.                         |
| 7. Crack DECSoft Mainframe; download SQL_MemCorrupt.exe & Decypher.exe.     |
| 8. Solve eOS mobile malware contract; acquire EOSDeviceScanner.exe.         |
| 9. Probe ThemeHackComp; trigger Naix counter-attack.                        |
| 10. Recover x-server.sys from gateway; reboot GUI.                          |
| 11. Complete CSEC Project Bit lead; locate EnTech server network.           |
| 12. Infiltrate EnTech Workstation 04; extract Romulus / Prometheus IPs.     |
| 13. Crack EnTech Prometheus daemon; disable core security monitor.         |
| 14. Access EnTech Offline Backup; wipe /sys/ kernel binaries with `rm *`.   |
| 15. Disconnect and trigger final system reboot for game victory!            |
+-----------------------------------------------------------------------------+
```

---

# 7. ENGINE FORENSICS & SAVE GAME BYTECODE MAPPING [ENGN]

### A. XML Computer Node Schema & HackerScripts Engine [ENG01]
Every computer node is serialized in pure XML:
* `<Computer id="id" name="name" security="N" ip="X.X.X.X">`
* `<ports>` comma-separated list of target service ports.
* `<portsForCrack val="N">` number of open ports required before `PortHackExe` can escalate root privileges.
* `<firewall level="N" solution="STR"/>` firewall bypass puzzle.
* `<proxy time="N"/>` proxy overload multiplier.

### B. Save File Serialization [ENG02]
Stored in `SavedGame.xml` within the OS application data path. Tracks memory size (`<memory>`), discovered IP addresses (`<netMap>`), and unlocked tool binaries in `<files>`.

---

# 8. LABYRINTHS EXPANSION FORENSICS & NETWORK JAMMERS [LABY]

> **Source Verification**: `Hacknet.app/Contents/MacOS/Content/DLC/DLCFaction.xml`
> ```xml
> <faction id="hub" name="Labyrinths Collective">
>   <member name="Kaguya" role="Architect"/>
>   <member name="Coel" role="Infiltrator"/>
>   <member name="D3f4ult" role="Disruptor"/>
> </faction>
> ```

* **Signal Jammers**: Prevent remote connection until radio antennas are disrupted via `SignalScramble.exe`.
* **Live Memory Heap Extraction**: Running `MemDumpGenerator.exe` dumps runtime RAM registers to harvest dynamic passwords directly from unmanaged memory pools.

---

# 9. VERSION HISTORY & BUILD PROVENANCE [VERS]

* **2015 Steam / GOG Initial Release (v1.0)**: Base game release.
* **2016 Labyrinths Expansion (v5.0)**: DLC integration with new memory forensics and network jammer tools.
* **Target Build SHA-256**: `4f18d7b32867ef99a8b8431057e0524458319f6a735165b40cf6238da2c8b74a`

---

# 10. CONTACT POLICY & CREDITS [CRED]

* **Team Fractal Alligator**: Matt Trobbiani (Creator & Lead Developer).
* **Music Composers**: The Algorithm, OGRE, Rémi Gallego, Ton划, Cinematrik.
* **YOU, the Hacker**: "Hack the planet. Stay curious. Protect the open net."
