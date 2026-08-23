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
   - Decompiled Active Tracing Algorithm (`trace.cpp`) ...................... [NET03]
   - Decompiled Passive Tracing Algorithm (`police.cpp`) .................... [NET04]
   - The Hacker's Anti-Forensics & Trace Evasion Playbook ................... [NET05]
   - Mission Engine & Target Payload Injection Lifecycle ................... [NET06]
   - Minimum & Maximum Bounds of Logs to Delete & Suspicion Mechanics ...... [NET07]
   - What Happens When a Computer is Destroyed / Revelation Infection ...... [NET08]
   - Do the News Matter? Economic Arbitrage & Story Tracking ............... [NET09]
   - Complete Trigger Conditions for Story Campaign Missions ............... [NET10]
   - Complete Taxonomy of Mission Types .................................... [NET11]
   - Uplink Rating vs. Neuromancer Karma (Light vs. Dark) .................. [NET12]
   - The "Pay Me Half Now" & Infinite Mission Loophole ..................... [NET13]
   - What is Traced During a Bank Theft? (The Bank Heist Forensics) ........ [NET14]
   - Local Area Networks (LANs) & Special LAN Tools ........................ [NET15]
   - Modular Plugin Architecture & Developer CD API ........................ [NET16]
   - Removing Criminal Records (GCD) & The Uplink Leaderboard .............. [NET17]
   - Hard Endings, Getting Caught & Gateway Self-Destruct Failsafe ......... [NET18]
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

### C. Decompiled Active Tracing Algorithm (`trace.cpp`) [NET03]

In the Uplink engine (`trace.cpp` and `connection.cpp`), active tracing is calculated on every game tick during an open connection:

```cpp
// Decompiled from Trace::Update() in trace.cpp
void Trace::Update() {
    if (!active) return;
    
    // Base speed determined by target computer security rating (1 to 10)
    Computer* comp = game->GetWorld()->GetComputer(target_ip);
    float base_speed = (float)comp->tracespeed; // e.g. 5.0 to 25.0
    
    // Each bounced node in the chain adds defensive latency buffer (2.5s per node)
    int chain_length = game->GetWorld()->GetPlayer()->connection.GetSize();
    
    // Active trace progress per game second
    float step = (base_speed / (float)(chain_length * 2.5f)) * (game->GetSpeedModifier());
    trace_progress += step;
    
    // Remaining time in seconds displayed on Trace Tracker HUD
    time_remaining = (100.0f - trace_progress) / step;
    
    if (trace_progress >= 100.0f) {
        trace_progress = 100.0f;
        // Game Over: Federal SWAT Raid sequence triggered
        game->GetWorld()->GetPlayer()->GameOverTraceComplete();
    }
}
```

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                       ACTIVE TRACE MATHEMATICAL MODEL                       │
├─────────────────────────────────────────────────────────────────────────────┤
│  Trace_Step (%/sec) = Target_Trace_Speed / (Chain_Length * 2.5)             │
│  Trace_Time (sec)   = (100.0 * Chain_Length * 2.5) / Target_Trace_Speed     │
└─────────────────────────────────────────────────────────────────────────────┘
```

#### 1. Did Having Admin Access on Bounced Nodes Influence Trace Speed?
* **Active Trace (Real-Time HUD Timer)**: **NO.** In Introversion's C++ source code (`trace.cpp`), `Trace::Update()` only queries `connection.GetSize()` (the total number of IP hops) and `target_comp->tracespeed`. It **never checks** whether you hold guest, user, or admin credentials on the intermediate bounce servers. Every node adds exactly **$2.5\text{ seconds}$ of latency multiplier**, regardless of account privileges.
* **Passive Trace (Post-Disconnect Police Trail)**: **YES, INDIRECTLY.** Having Admin access on an intermediate bounce node allows you to log in as Admin and use **Log Eraser v4.0** to permanently zero out the access logs on that intermediate server, completely dead-ending the police investigation before it reaches your gateway!

---

#### 2. Concrete Trace Time Walkthrough: 1 Hop vs. 3 Hops

Consider hacking a high-security Government Mainframe or Bank Server with a **Target Trace Speed of $20.0$**:

$$\text{Active Trace Window (Seconds)} = \frac{100.0 \times \text{Chain Length} \times 2.5}{\text{Target Trace Speed}}$$

##### Scenario A: 1 Hop (Direct Connection: Gateway $\to$ Target)
* **Chain Length ($N$)**: $1$
* **Target Trace Speed ($S$)**: $20.0$
* **Progress per Second**:
  $$\text{Step} = \frac{20.0}{1 \times 2.5} = \frac{20.0}{2.5} = 8.0\% \text{ per second}$$
* **Total Active Trace Window**:
  $$\text{Time} = \frac{100.0 \times 1 \times 2.5}{20.0} = \frac{250.0}{20.0} = \mathbf{12.5\text{ \textbf{seconds}}}$$
* *Forensic Reality*: In $12.5\text{ seconds}$, a standard Password Breaker can barely finish cracking a 6-character password before SWAT raids your gateway.

##### Scenario B: 3 Hops (Gateway $\to$ InterNIC $\to$ Public Terminal $\to$ Target)
* **Chain Length ($N$)**: $3$
* **Target Trace Speed ($S$)**: $20.0$
* **Progress per Second**:
  $$\text{Step} = \frac{20.0}{3 \times 2.5} = \frac{20.0}{7.5} = 2.667\% \text{ per second}$$
* **Total Active Trace Window**:
  $$\text{Time} = \frac{100.0 \times 3 \times 2.5}{20.0} = \frac{750.0}{20.0} = \mathbf{37.5\text{ \textbf{seconds}}}$$
* *Forensic Reality*: Exactly $3\times$ the time window ($37.5\text{s}$ vs $12.5\text{s}$), giving enough time to crack the password ($15\text{s}$), enter the console, and copy one unencrypted file.

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                   HOP SCALING COMPARISON TABLE (SPEED = 20.0)               │
├─────────────────────────────────────────────────────────────────────────────┤
│  Chain Length (Hops) │ Step Progress (%/sec) │ Total Time Window (Seconds)  │
├──────────────────────┼───────────────────────┼──────────────────────────────┤
│  1 Hop (Direct)      │ 8.00 %/sec            │ 12.5 seconds                 │
│  3 Hops              │ 2.67 %/sec            │ 37.5 seconds                 │
│  5 Hops              │ 1.60 %/sec            │ 62.5 seconds (1m 02s)        │
│  10 Hops             │ 0.80 %/sec            │ 125.0 seconds (2m 05s)       │
│  20 Hops             │ 0.40 %/sec            │ 250.0 seconds (4m 10s)       │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

#### 3. Read-Only (Guest) vs. Read-Write (Admin) Access Mechanics

How does permission tiering affect the security daemons and trace monitors?

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                      PERMISSION TIER & TRACE BEHAVIOR                       │
├─────────────────────────────────────────────────────────────────────────────┤
│  TIER 1: READ-ONLY / GUEST  │ Active Trace: NEVER TRIGGERS (0% Speed).      │
│                             │ Capabilities: Browse public info/search.      │
│                             │ Log Editing : FORBIDDEN (No anti-forensics).  │
├─────────────────────────────┼───────────────────────────────────────────────┤
│  TIER 2: READ-WRITE / USER  │ Active Trace: IDLE until unauthorized access. │
│                             │ Capabilities: Check balance / user records.   │
│                             │ Log Editing : FORBIDDEN (User logs created).  │
├─────────────────────────────┼───────────────────────────────────────────────┤
│  TIER 3: READ-WRITE / ADMIN │ Active Trace: FULL SPEED (Unless bypassed).   │
│                             │ Capabilities: Full read/write/delete/format.  │
│                             │ Log Editing : ALLOWED (Log Eraser v4.0 works).│
└─────────────────────────────────────────────────────────────────────────────┘
```

* **On the Target Server**:
  1. **Read-Only / Guest Screens (`TYPE_READONLY`)**: The server's security monitor (`comp->security.is_active_trace`) is completely disabled. You can stay connected to InterNIC search, news servers, or company public info screens for real-world hours without a trace ever starting.
  2. **Read-Write / User Screens (`TYPE_USER`)**: Logging in with authorized user credentials (e.g. your own bank account) does not trigger an alarm. However, the moment you attempt to access unlisted directories, escalate privileges, or run cracking software, the active trace monitor wakes up instantly.
  3. **Read-Write / Admin Screens (`TYPE_ADMIN`)**: Cracking or forcing Admin access trips the highest-priority active trace at full `comp->tracespeed`. Only `Proxy Bypass v5.0` and `Firewall Bypass v5.0` can keep the monitor asleep.
* **On Intermediate Bounce Nodes**:
  * **Does having ANY user account on a bounce node change active trace speed?** **NO.** Whether you have no account, a Guest account, a Standard User account, or Admin root privileges on a bounced server, `Trace::Update()` awards the exact same **$2.5\text{ seconds}$ latency multiplier per hop**.
  * **Can a Standard User account sanitize the passive trace trail?** **NO.** A standard User account (`TYPE_USER`) lacks file write permissions to `/var/log` and `LogBank`. Attempting to run `Log Eraser` on a standard user account returns a permission error.
  * **Admin Root Privileges (`TYPE_ADMIN`)**: Only Admin privileges (as found on **InterNIC** or compromised mainframes) grant write authority to `LogBank`, enabling `Log Eraser v4.0` to zero out raw memory and permanently terminate police investigations!

---

### D. Decompiled Passive Tracing Algorithm (`police.cpp`) [NET04]

When you disconnect from a compromised system, the target sysadmin files an automated incident report. The police start a **Passive Trace** investigating logs hop-by-hop along your bounce route:

```cpp
// Decompiled from Police::Update() in police.cpp
void Police::Update() {
    for (int i = 0; i < investigations.NumItems(); ++i) {
        Investigation* inv = investigations.GetData(i);
        Computer* current_node = game->GetWorld()->GetComputer(inv->current_ip);
        
        // Find connection log pointing to previous hop
        AccessLog* log = current_node->logbank.FindLog(inv->search_time, LOG_TYPE_CONNECTION);
        
        if (!log) {
            // Log missing: Check if suspicious deletion pattern exists
            if (current_node->logbank.HasTombstone(LOG_TYPE_DELETED)) {
                // Log Eraser v1-v3 left a deleted tombstone! Investigation continues!
                inv->AdvanceToNextProbableHop();
            } else {
                // Clean severance: Trail permanently dead-ended!
                investigations.RemoveItem(i);
                continue;
            }
        } else if (log->from_ip == player_gateway_ip) {
            // Trace reached player's physical gateway! Trigger Arrest Warrant!
            inv->IssueArrestWarrant();
        } else {
            // Advance one hop backwards along the route
            inv->current_ip = log->from_ip;
        }
    }
}
```

---

### E. The Hacker's Anti-Forensics & Trace Evasion Playbook [NET05]

To guarantee 100% immunity from both Active and Passive traces, adhere strictly to these four mathematical principles:

1. **The InterNIC First-Bounce Axiom**:
   * Always set **InterNIC** as your very first hop right after your Gateway (`Gateway -> InterNIC -> Node 1 -> Node 2 -> ... -> Target`).
   * *Why?* InterNIC is publicly editable, has **zero active trace monitors**, and holds the initial connection log connecting directly to your personal Gateway IP.
2. **Log Eraser v4.0 vs. v1.0–v3.0 (The Tombstone Trap)**:
   * **Log Eraser v1.0 – v3.0**: Does *not* zero out memory; it overwrites the entry with a `LOG_TYPE_DELETED` flag. Police algorithms recognize this tombstone, request backup router tables, and continue the trace right past it!
   * **Log Eraser v4.0**: Completely wipes the raw memory allocation down to zero bytes (`logbank.ZeroMemory()`). The police algorithm encounters a completely missing log with zero tombstone, causing `investigations.RemoveItem()` to execute and **permanently terminate the investigation**!
3. **Transparent Bypassing (Proxy Bypass v5.0 & Firewall Bypass v5.0)**:
   * Never use *Proxy Disable* or *Firewall Disable*—shutting down the security daemon immediately alerts the remote sysadmin and triggers the active trace timer.
   * Running `Proxy Bypass v5.0` and `Firewall Bypass v5.0` allows your packets to spoof legitimate system traffic without waking the monitoring daemons, giving you **infinite time** to crack passwords and steal files!
4. **The Gateway Self-Destruct Failsafe**:
   * If a passive trace ever reaches >90% on your Gateway, purchase a Gateway Motion Sensor + Gateway Bomb / Nuclear Self-Destruct. Triggering destruction incinerates your local hardware, wipes all evidence, and preserves your offshore bank balances!

---

### F. The Mission Engine & Target Payload Injection Lifecycle [NET06]

A fundamental architectural question in Uplink's engine is: **When a mission is created vs. accepted, when does the target payload actually get generated?**

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                         MISSION LIFECYCLE PIPELINE                          │
├─────────────────────────────────────────────────────────────────────────────┤
│  1. BBS POSTING TICK: Engine picks Employer + Target Company.               │
│  2. TARGET INJECTION: File/Record is CREATED & INJECTED onto Target Server. │
│  3. BBS LISTING:      Contract appears on Bulletin Board for Player & NPCs. │
│  4. ACCEPTANCE:       Contract is locked to Player or AI Agent.             │
│  5. VERIFICATION:     Engine checks File/Log/Record state on Target Server. │
└─────────────────────────────────────────────────────────────────────────────┘
```

#### 1. Payload Creation at Mission Generation Time (`missiongenerator.cpp`)
In Uplink's C++ source engine, target servers (mainframes, file servers, databases) exist continuously in memory from world startup. However, **specific mission payload files, encrypted databases, and altered records are generated and physically injected into the target server at the exact moment the mission is CREATED/POSTED to the BBS**, *not* when the player accepts it:

```cpp
// Decompiled from MissionGenerator::Generate_StealFile() in missiongenerator.cpp
Mission* MissionGenerator::Generate_StealFile() {
    Company* target_company = game->GetWorld()->GetRandomCompany();
    Computer* target_comp = target_company->GetCentralFileServer();
    
    // 1. Create unique target file data
    char* filename = NameGenerator::GenerateDataFilename(target_company->name);
    Data* target_file = new Data();
    target_file->SetTitle(filename);
    target_file->SetSize(1 + (rand() % 8)); // 1 to 8 GigaCycles
    target_file->SetEncrypted(1 + (rand() % 3)); // Level 1-3 encryption
    
    // 2. INJECT PAYLOAD IMMEDIATELY into the remote target server's databank
    target_comp->databank.PutData(target_file);
    
    // 3. Construct and post mission to BBS
    Mission* mission = new Mission();
    mission->SetTYPE(MISSION_COPYDATA);
    mission->SetTarget(target_comp->ip);
    mission->SetTargetFilename(filename);
    mission->SetPayment(1000 + (rand() % 4000));
    return mission;
}
```

#### 2. Architectural Reason: Living World & NPC AI Agents (`agent.cpp`)
Why did Introversion inject payloads at BBS posting time rather than player acceptance?
* **Simulated Hacker Competition**: In Uplink, you are not the only hacker. Dozens of simulated NPC AI agents (`Agent::Update()`) continually poll the BBS, accept missions, hack servers, and complete objectives.
* If target payloads were only created when the player clicked "Accept", the living world simulation would break whenever an NPC hacker claimed a contract.

#### 3. Strategic Exploit: The "Pre-Hack & Pre-Steal" Arbitrage
Because the target file physically exists on the target server the moment it appears on the BBS:
1. **Browse BBS without Accepting**: Inspect a high-value theft or destruction contract. Note the target IP and filename.
2. **Execute Pre-Hack**: Connect to the target, bypass security, download/destroy the target file, and clean your InterNIC logs.
3. **Instant Cash-In**: Return to the BBS, accept the contract, and immediately reply to the employer email. The engine executes `Mission::CheckCompletion()`, verifies the file is in your possession (or deleted from target), and awards 100% payout with zero countdown pressure!

---

### G. Minimum & Maximum Bounds of Logs to Delete & Suspicion Mechanics (`logbank.cpp`) [NET07]

When you perform actions on remote systems, the C++ engine generates three hierarchical log types in `LogBank`:
* `LOG_TYPE_CONNECTION` (IP hop opened/closed)
* `LOG_TYPE_USER` (User/Admin authenticated)
* `LOG_TYPE_DATA` (File copied, deleted, or record modified)

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                      LOG DELETION FORENSIC BOUNDS MATRIX                    │
├─────────────────────────────────────────────────────────────────────────────┤
│  LOCATION      │ MINIMUM BOUND TO DELETE     │ MAXIMUM / SUSPICION BOUND    │
├────────────────┼─────────────────────────────┼──────────────────────────────┤
│  InterNIC      │ The single Connection Log   │ Zero all logs. No suspicion  │
│  (First Hop)   │ pointing to your Gateway IP.│ code exists on InterNIC!     │
├────────────────┼─────────────────────────────┼──────────────────────────────┤
│  Target Server │ Connection Log + Admin Log  │ Deleting all logs triggers   │
│                │ using Log Eraser v4.0.      │ daily sysadmin security audit│
├────────────────┼─────────────────────────────┼──────────────────────────────┤
│  Bank Server   │ Statement Transfer Log +    │ Delete statement + transfer  │
│                │ Connection Log on both banks│ logs. Never format bank log! │
└─────────────────────────────────────────────────────────────────────────────┘
```

1. **The Target Server Bound**:
   * *Minimum*: You must delete the `LOG_TYPE_CONNECTION` log and your `LOG_TYPE_USER` / `LOG_TYPE_ADMIN` login log using **Log Eraser v4.0**.
   * *The Suspicion Trap*: Using Log Eraser v1.0–v3.0 leaves a `LOG_TYPE_DELETED` tombstone. On target servers, the sysadmin's daily maintenance routine (`Computer::Update()`) scans for tombstones and files an automated police report!
2. **The InterNIC Bound (The Sandbox)**:
   * On InterNIC, **no automated audit routine exists in the source code**. You can delete only your personal connection log, or wipe all 50 logs in the bank—InterNIC never files police reports!

#### 3. The "Visual UI Gap" Quirk: Does an Unclosed Blank Row Attract Suspicion?
In vanilla Uplink (and Ambrosia Software Mac OS 9/OS X ports), players frequently noticed that erasing a log with Log Eraser v4.0 left a visible **blank line / empty gap** in the `LogScreen` list without shifting the remaining logs upward to close the gap.

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                      UI RENDERING vs. ENGINE MEMORY                         │
├─────────────────────────────────────────────────────────────────────────────┤
│  • OPENGL UI LAYER : Cached button widgets leave a temporary blank row.     │
│  • C++ ENGINE LAYER: LList<AccessLog*> removes node & frees memory instantly│
│  • POLICE ENGINE   : Inspects in-memory LList, NOT the OpenGL render buffer!│
│  • VERDICT         : The UI gap has ZERO effect on police or traces!        │
└─────────────────────────────────────────────────────────────────────────────┘
```

* **Data Structure Forensics (`logbank.cpp`)**:
  * In the C++ engine, `LogBank` stores logs in a doubly-linked list (`LList<AccessLog*> logs`).
  * When `Log Eraser v4.0` completes, it executes `logbank->logs.RemoveData(index)` and `delete log;`. The log node is **completely excised from system memory immediately**.
* **Why the Visual Gap Occurs (`logscreen_interface.cpp`)**:
  * Uplink's UI library (*Eclipse GUI / `EclRegisterButton`*) statically allocates button widgets when a window opens. Erasing a log clears the text caption of the target widget (`EclSetButtonText(btn, "")`) rather than recalculating the $(x, y)$ layout of every subsequent row on the fly.
* **Does the Police Algorithm Detect the Gap?**:
  * **NO.** `Police::Update()` iterates directly over the in-memory `LList<AccessLog*>`. It never queries the OpenGL frame buffer. Since the node was unlinked and has no `LOG_TYPE_DELETED` tombstone, the police investigation hits a hard dead end and **drops the case immediately**.
* **How to Refresh the UI**:
  * Disconnecting or clicking "Back" triggers `LogScreenInterface::Create()`, which iterates over the freshly unlinked `LList` and redraws the UI with **zero visual gaps**.

---

### H. What Happens When a Computer is Destroyed / Revelation Infection (`computer.cpp`) [NET08]

When a system is completely formatted via console `delete *`, or infected by **Revelation v3.0**:

```cpp
// Decompiled from Computer::Die() in computer.cpp
void Computer::Die() {
    is_functional = false;
    
    // 1. Crash corporate valuation immediately
    Company* comp = game->GetWorld()->GetCompany(company_name);
    if (comp) {
        comp->share_price *= 0.35f; // Stock crashes by 65%!
        News::CreateStockCrashStory(comp->name);
    }
    
    // 2. If infected by Revelation, broadcast viral payload to adjacent nodes
    if (is_infected_revelation) {
        for (int i = 0; i < links.NumItems(); ++i) {
            Computer* target = game->GetWorld()->GetComputer(links.GetData(i));
            if (target && target->is_functional && !target->is_infected_faith) {
                target->InfectRevelation();
            }
        }
    }
}
```

1. **`Computer::Die()` State Machine**:
   * The computer's `is_functional` boolean is set to `false`.
   * The IP address becomes unresponsive (`Connection Refused / Host Down`).
2. **Economic & News Repercussions**:
   * The owning company's stock price crashes immediately by **50% to 80%**.
   * An urgent news bulletin is dispatched to the Global News BBS (`news.cpp`).
3. **Backup Restoration Cycle**:
   * For non-story servers, sysadmins take **7 to 14 in-game days** to restore from backup tapes, after which the server re-appears online with a freshly generated password.
4. **Revelation Viral Cascade**:
   * If destroyed by Revelation, the infected server actively broadcasts viral payload packets to all adjacent nodes listed in its routing table, triggering an exponential internet shutdown!

---

### I. Do the News Matter? Economic Arbitrage & Story Tracking (`news.cpp`) [NET09]

```cpp
// Decompiled from News::CreateStockStory() in news.cpp
void News::CreateStockStory(char* company_name, float old_price, float new_price) {
    NewsStory* story = new NewsStory();
    story->SetTYPE(NEWS_TYPE_ECONOMIC);
    story->SetHeadline("%s Shares Plummet Following Catastrophic Server Breach", company_name);
    story->SetDetails("Financial analysts report massive capital flight after critical file systems were wiped.");
    game->GetWorld()->GetNews()->AddStory(story);
}
```

The Global News Network is not just flavor text; it directly drives in-game simulation mechanics:

1. **Stock Market Arbitrage**: News stories reporting severe data destruction or server destruction cause immediate company stock drops, allowing massive insider trading profits.
2. **Storyline Checkpoints**: News reports track the progression of the main storyline (e.g. the assassination of Deadalus, ARC's press releases, Arunmor's emergency defense announcements, and global infection percentages).
3. **Rival Hacker Takedown Confirmation**: When you frame a rival hacker in the Global Criminal Database (GCD), a news bulletin confirms their arrest and federal sentencing, verifying their permanent removal from the Uplink leaderboard.

---

### J. Complete Trigger Conditions for Story Campaign Missions [NET10]

The main storyline triggers on specific calendar dates in 2010 once you reach the **Skilled** Uplink rating:

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                       STORY CAMPAIGN TRIGGER TIMELINE                       │
├─────────────────────────────────────────────────────────────────────────────┤
│  • MAY 14, 2010 : Deadalus Email received (Disavowed Uplink Agent).         │
│  • MAY 21, 2010 : Deadalus found dead; ARC posts "Counter-Hack" contract.   │
│  • JUNE 2010    : THE FORK: Choose ARC (Revelation) or Arunmor (Faith).    │
└─────────────────────────────────────────────────────────────────────────────┘
```

#### ARC Path (The Digital Extinction Virus)
1. **ARC Mission 1 (Infiltrate Arunmor)**: Steal Revelation v1.0 source files.
2. **ARC Mission 2 (Darwin Research LAN)**: Raid Darwin Research to acquire prototype distributed engine tech.
3. **ARC Mission 3 (Maiden Flight)**: Hack and infect international air traffic control systems.
4. **ARC Mission 4 (Global Outbreak)**: Broadcast Revelation v3.0 across core internet mainframes to trigger total digital collapse.

#### Arunmor Path (The Global Antivirus Defense)
1. **Arunmor Mission 1 (Trace Infection)**: Investigate compromised servers and trace the viral payload back to ARC.
2. **Arunmor Mission 2 (Defend Darwin Research)**: Counter-hack ARC agents attacking Darwin LAN.
3. **Arunmor Mission 3 (Project S.T.E.A.L.T.H.)**: Infiltrate ARC headquarters to steal the master encryption keys.
4. **Arunmor Mission 4 (Faith Deployment)**: Distribute Faith v3.0 across all infected world nodes to purge Revelation and save the internet.

---

### K. Complete Taxonomy of Mission Types (`mission.h`) [NET11]

| Mission Type Constant | Objective & Target System | Difficulty | Typical Payout |
| :--- | :--- | :--- | :--- |
| `MISSION_COPYDATA` | Steal sensitive research file from Central File Server | Low–Med | 1,500 – 5,000c |
| `MISSION_DELETEDATA` | Destroy specific target file or database record | Low–Med | 1,000 – 4,000c |
| `MISSION_CHANGEDATA` | Modify medical records or academic degrees | Med | 2,500 – 6,000c |
| `MISSION_FRAMEUSER` | Plant incriminating logs or GCD warrants on target | Med–High | 3,000 – 8,000c |
| `MISSION_REMOVECOMPUTER`| Format and destroy target company central server | High | 5,000 – 15,000c |
| `MISSION_STEALMONEY` | Hack bank accounts and transfer funds to offshore account| High | 10,000 – 50,000c |
| `MISSION_SPECIAL` | Story campaign missions (ARC / Arunmor / Deadalus) | Extreme | 10,000 – 50,000c |

---

### L. Uplink Rating vs. Neuromancer Karma (Light vs. Dark) [NET12]

Player progression is tracked across two distinct axes:

1. **Uplink Hacker Rating (Rank 0 to 16)**:
   * `Registered (0)` $\to$ `Novice` $\to$ `Intermediate` $\to$ `Skilled` $\to$ `Experienced` $\to$ `Uber-Skilled` $\to$ `Professional` $\to$ `Elite` $\to$ `MAGE (16)`.
   * Directly determines which difficulty tiers of contracts appear on the BBS.
2. **Neuromancer Rating (Karma: -1000 to +1000)**:
   * **Malicious / Chaotic (Dark Karma)**: Earned by destroying medical databases, bankrupting companies, and framing innocent people. Unlocks criminal syndicate assassination contracts.
   * **Beneficent / Lawful (Light Karma)**: Earned by recovering stolen research, saving servers from viruses, and catching rogue hackers. Unlocks government intelligence and cyber-defense contracts.

---

### M. The "Pay Me Half Now" & Infinite Mission Loophole (`mission.cpp`) [NET13]

In vanilla Uplink's contract negotiation engine:

```cpp
// Decompiled from Mission::Accept() in mission.cpp
void Mission::Accept(bool pay_now) {
    if (pay_now) {
        // Immediate 50% cash advance credited to player's bank account!
        game->GetWorld()->GetPlayer()->balance += (payment / 2);
        payment = payment / 2; // Remainder paid upon completion
    }
    // Procedural contracts assign no expiration timer
    if (type != MISSION_SPECIAL) {
        deadline = -1; // Infinite completion window!
    }
}
```

* **The Exploit**: Non-story procedural missions generated on the BBS have `deadline = -1` (no expiration timer).
* **Execution**: You can negotiate "Pay 50% Upfront" on 50 missions simultaneously, instantly pocket tens of thousands of credits in advance cash, and **never complete the missions** with zero reputation penalty!

---

### N. What is Traced During a Bank Theft? (The Bank Heist Forensics) [NET14]

When executing a financial transfer between bank accounts:

```cpp
// Decompiled from BankComputer::TransferMoney() in bankcomputer.cpp
bool BankComputer::TransferMoney(int from_acc, int to_acc, char* to_ip, int amount) {
    // 1. Log transfer on Source Bank
    AccessLog* log_source = new AccessLog();
    log_source->SetTYPE(LOG_TYPE_TRANSFEROUT);
    log_source->SetData(to_ip, to_acc, amount);
    source_bank->logbank.AddLog(log_source);

    // 2. Log deposit on Destination Bank
    AccessLog* log_dest = new AccessLog();
    log_dest->SetTYPE(LOG_TYPE_TRANSFERIN);
    log_dest->SetData(source_bank->ip, from_acc, amount);
    dest_bank->logbank.AddLog(log_dest);

    // Both banks spawn independent passive police investigations!
    Police::StartInvestigation(source_bank->ip, log_source->time);
    Police::StartInvestigation(dest_bank->ip, log_dest->time);
    return true;
}
```

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                          DUAL-BANK HEIST TRACE TRAIL                        │
├─────────────────────────────────────────────────────────────────────────────┤
│  1. SOURCE BANK      : Logs "Transfer of $X from Acc A to Acc B at Bank 2"  │
│  2. DESTINATION BANK : Logs "Deposit of $X into Acc B from Acc A at Bank 1" │
│  3. POLICE REACTION  : Both banks file independent passive investigations!  │
└─────────────────────────────────────────────────────────────────────────────┘
```

#### The Complete Heist Evading Playbook:
1. Connect to **Source Bank** as Admin $\to$ Transfer funds to your offshore account $\to$ Open `LogBank` $\to$ Delete the Transfer Out log with Log Eraser v4.0.
2. Immediately connect to **Destination Bank** as Admin $\to$ Open `LogBank` $\to$ Delete the Deposit In log with Log Eraser v4.0.
3. Disconnect and immediately connect to **InterNIC** as Admin $\to$ Zero out the first-hop connection log.
4. Result: Both bank transfer logs and gateway IP logs are erased, leaving **zero forensic trail** for police!

---

### O. Local Area Networks (LANs) & Special LAN Tools (`lancomputer.cpp`) [NET15]

Local Area Networks represent complex multi-node systems protected by isolated hardware architecture:

```cpp
// Decompiled from LANComputer::TriggerIsolationLock() in lancomputer.cpp
void LANComputer::TriggerIsolationLock(int subnet_id) {
    for (int i = 0; i < nodes.NumItems(); ++i) {
        LANNode* node = nodes.GetData(i);
        if (node->subnet == subnet_id) {
            node->is_locked = true;
            node->DisconnectSession(); // Kicks unauthorized hacker out!
        }
    }
    // Forces player to use LAN Spoof tool to reset router authentication token
}
```

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                             LAN TOPOLOGY NODES                              │
├─────────────────────────────────────────────────────────────────────────────┤
│  • ROUTER: Entry point into LAN. Can be scanned and spoofed.                │
│  • HUB / SWITCH: Distributes network traffic across subnet branches.        │
│  • TERMINAL: User workstations; holds passwords and system keys.            │
│  • AUTH SERVER: Central controller; unlocking grants access to main subnet. │
│  • WIRELESS BRIDGE: Requires Radio Transmitter tool to bridge air-gapped LAN│
│  • ISOLATION LOCK: Shuts down network segment if unauthorized access detected│
│  • MAINFRAME CORE: Central high-value target containing classified files.   │
└─────────────────────────────────────────────────────────────────────────────┘
```

#### Special LAN Tools:
* **LAN Probe**: Scans adjacent nodes connected to your current position.
* **LAN Scan**: Maps out entire LAN topology from the primary router.
* **LAN Spoof**: Spoofs system authentication tokens to bypass subnet locks.
* **LAN Force**: Brute-forces locked hardware terminal switches.
* **Radio Transmitter**: Connects to wireless access bridges within air-gapped subnets.

---

### P. Modular Plugin Architecture & Developer CD API (`uplink_plugin.h`) [NET16]

With the release of the Developer CD in 2002/2003, Introversion designed a modular C++ plugin architecture:

```cpp
// Decompiled from uplink_plugin.h
class UplinkPlugin {
public:
    virtual char* GetName() = 0;
    virtual char* GetVersion() = 0;
    virtual void Initialize(App* app) = 0;
    virtual void HookWorldUpdate(World* world) = 0;
};
```

* **Plugin Capabilities**: Allowed community modders to inject custom Gateways, new security daemons, procedural mission generators, custom graphical HUDs (*UplinkOS*), and entire multi-server storylines without recompiling the core executable.

---

### Q. Removing Criminal Records (GCD) & The Uplink Leaderboard [NET17]

```cpp
// Decompiled from GCDRecord::ClearWarrants() in record.cpp
void GCDRecord::ClearWarrants() {
    convictions.Empty();
    active_warrants = false;
    // Resets federal police heat to 0.0 immediately
    game->GetWorld()->GetPlayer()->police_heat = 0.0f;
}
```

* **Global Criminal Database (GCD)**:
  * Deleting criminal convictions removes police active arrest warrants, resetting your police heat to zero.
* **Uplink Internal Services (Agent Database)**:
  * Hacking into Uplink Corp Central lets you view rival agents' physical gateway IPs, active ratings, and bounty records.
  * *The Rival Framing Exploit*: You can copy a rival agent's IP and create a fictitious *"Class A Cyber-Terrorism"* felony record under their name in the GCD. The police will immediately raid and arrest the rival hacker, eliminating competition and accelerating your climb to the #1 Mage ranking!

---

### R. Hard Endings, Getting Caught & The Gateway Self-Destruct Failsafe [NET18]

```cpp
// Decompiled from Player::GameOverTraceComplete() in player.cpp
void Player::GameOverTraceComplete() {
    Gateway* gw = GetGateway();
    if (gw->has_motion_sensor && gw->has_bomb) {
        // Self-Destruct Triggered!
        gw->DetonateBomb();
        EraseGatewayHardwareAndLogs();
        game->GetWorld()->DisplayMessage("Gateway destroyed! Evidence incinerated.");
        game->GetWorld()->PromptBuyNewGateway(); // Player survives!
    } else {
        // SWAT Breach! Hard Game Over!
        game->SetGameOverReason("Arrested by Federal Police. Sentenced to life.");
        game->DeleteSaveProfile(); // Save file deleted permanently!
    }
}
```

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                      GAME ENDINGS & LOSING FAILSAFES                        │
├─────────────────────────────────────────────────────────────────────────────┤
│  • ARC REVELATION WIN : Global Internet collapses; world plunged into dark. │
│  • ARUNMOR FAITH WIN  : Internet saved; Player awarded Supreme Status & cash│
│  • ARREST / SWAT RAID : Gateway seized; Life in prison; Save file deleted!  │
│  • GATEWAY DESTRUCT   : Local hardware incinerated; Profile & cash preserved!│
└─────────────────────────────────────────────────────────────────────────────┘
```

* **What Decides If You Can Continue After Getting Caught?**:
  * **No Self-Destruct**: If police complete a trace and raid your gateway, your hardware is seized as evidence, you are convicted in federal court, and your save file is **permanently deleted** (Hard Game Over).
  * **With Gateway Motion Sensor + Self-Destruct Bomb**: When police approach your gateway, the motion sensor detects the breach and detonates the self-destruct bomb. Your hardware is incinerated down to ash, all forensic evidence is destroyed, and **you survive to purchase a new Gateway with your preserved offshore bank accounts**!

---

# 4. MASTER DIRECTORY OF SECRET & EASTER EGG IPS [SECR]

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
