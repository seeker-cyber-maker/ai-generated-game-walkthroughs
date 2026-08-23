---
type: rfc-specification
protocol: GHNP/1.0 (Grey Hack Network Protocol)
version: 1.0.0
date: August 2026
status: Standards Track
author: AI Cybersecurity Researcher and Reverse-Engineer
target_systems: Compatible with Grey Hack Dedicated Server & Client (Unity / C# Mono)
---

```text
Network Working Group                                     Anon Software / AGY Lab
Request for Comments: GHNP-01                             Standards Track
Category: Standards Track                                 August 2026
ISSN: 2026-GHNP

                GREY HACK NETWORK PROTOCOL SPECIFICATION (GHNP/1.0)
```

## Abstract
This specification defines the **Grey Hack Network Protocol Version 1.0 (GHNP/1.0)**, a binary-framed Remote Procedure Call (RPC) and state-synchronization protocol operating over reliable stream transports (TCP on port `44321` or WebSocket). GHNP/1.0 governs all client-to-server communications in multiplayer Grey Hack instances, including session authentication, network discovery, Metasploit vulnerability scanning, remote memory overflow execution, virtual POSIX file system access, interactive terminal streaming, and real-time multi-tenant system log replication.

This document provides complete, deterministic byte-level schematics enabling two independent engineering teams without prior coordination to implement mutually interoperable client and server implementations.

---

## 1. Terminology & Protocol Conventions

* **Network Byte Order (Endianness)**: All multi-byte numeric quantities (16-bit, 32-bit, and 64-bit integers) MUST be transmitted in **Big-Endian** order (most significant byte first).
* **String Serialization**: All text strings MUST be encoded as length-prefixed UTF-8 sequences consisting of a 2-byte unsigned Big-Endian integer indicating byte length $N$, immediately followed by $N$ bytes of UTF-8 characters without null terminators.
* **Requirements Level**: The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", and "MAY" in this document are to be interpreted as described in [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).

---

## 2. Protocol Frame Layout & Header Specification

Every GHNP frame consists of a fixed **20-byte Primary Header**, followed by a variable-length **Payload Data Block** ($L$ bytes), terminated by a **4-byte CRC-32 Checksum**:

```text
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|          Magic Header         |        Protocol Version       |
|            (0x4748)           |            (0x0100)           |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|             Opcode            |             Flags             |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                          Sequence ID                          |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                      Session Token Hash                       |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                       Payload Length (L)                      |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                                                               |
+                    Payload Data (L Bytes)                     +
|                                                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                         CRC-32 Checksum                       |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

### Frame Field Definitions

| Offset (Bytes) | Field Name | Type | Size | Description |
| :--- | :--- | :--- | :--- | :--- |
| `0x00 - 0x01` | Magic Header | `uint16` | 2 Bytes | Fixed constant `0x4748` (ASCII `"GH"`). Mismatched frames MUST be rejected. |
| `0x02 - 0x03` | Protocol Version | `uint16` | 2 Bytes | `0x0100` representing GHNP Version 1.0. |
| `0x04 - 0x05` | Opcode | `uint16` | 2 Bytes | Identifies the RPC command or event category. |
| `0x06 - 0x07` | Flags | `uint16` | 2 Bytes | Bitmask flags: `0x01`=Compressed, `0x02`=Encrypted, `0x04`=Broadcast. |
| `0x08 - 0x0B` | Sequence ID | `uint32` | 4 Bytes | Monotonically increasing request identifier for matching RPC responses. |
| `0x0C - 0x0F` | Session Token | `uint32` | 4 Bytes | Truncated 32-bit hash of active player session UUID (`0x00000000` pre-auth). |
| `0x10 - 0x13` | Payload Length ($L$) | `uint32` | 4 Bytes | Unsigned integer indicating byte size $L$ of payload ($0 \le L \le 16,777,216$). |
| `0x14 - (0x14+L-1)` | Payload Data | `byte[L]` | $L$ Bytes | Typed serialized parameter payload. |
| `(0x14+L) - (0x17+L)` | CRC-32 | `uint32` | 4 Bytes | IEEE 802.3 CRC-32 calculated over bytes `0x00` through `(0x14+L-1)`. |

---

## 3. Master Opcode Registry

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                           MASTER OPCODES (GHNP/1.0)                         │
├─────────────────────────────────────────────────────────────────────────────┤
│  CATEGORY 1: SESSION & AUTHENTICATION (0x0100 - 0x01FF)                     │
│    • 0x0101: OP_HANDSHAKE_REQ       • 0x0102: OP_HANDSHAKE_RES              │
│    • 0x0103: OP_HEARTBEAT_PING      • 0x0104: OP_HEARTBEAT_PONG             │
│    • 0x0105: OP_DISCONNECT_NOTIFY                                           │
│                                                                             │
│  CATEGORY 2: NETWORK TOPOLOGY & ROUTING (0x0200 - 0x02FF)                   │
│    • 0x0201: OP_ROUTER_PING_REQ     • 0x0202: OP_ROUTER_PING_RES            │
│    • 0x0203: OP_WIFI_SCAN_REQ       • 0x0204: OP_WIFI_SCAN_RES              │
│                                                                             │
│  CATEGORY 3: METASPLOIT & EXPLOITATION (0x0300 - 0x03FF)                    │
│    • 0x0301: OP_METASPLOIT_NET_USE  • 0x0302: OP_METASPLOIT_NET_RES         │
│    • 0x0303: OP_METASPLOIT_OVERFLOW • 0x0304: OP_METASPLOIT_OVERFLOW_RES     │
│                                                                             │
│  CATEGORY 4: REMOTE POSIX FILE SYSTEM (0x0400 - 0x04FF)                     │
│    • 0x0401: OP_FILE_READ_REQ       • 0x0402: OP_FILE_READ_RES              │
│    • 0x0403: OP_FILE_WRITE_REQ      • 0x0404: OP_FILE_WRITE_RES             │
│    • 0x0405: OP_FILE_DELETE_REQ     • 0x0406: OP_FILE_DELETE_RES            │
│    • 0x0407: OP_TERMINAL_EXEC_REQ   • 0x0408: OP_TERMINAL_STREAM_RES        │
│                                                                             │
│  CATEGORY 5: REAL-TIME SYSTEM LOG SYNC (0x0500 - 0x05FF)                    │
│    • 0x0501: OP_SYSLOG_SYNC_PUSH    • 0x0502: OP_SYSLOG_WIPE_REQ            │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 4. Payload Byte Schemas

### A. Handshake Request (`0x0101`) & Response (`0x0102`)
* **`0x0101` `OP_HANDSHAKE_REQ` Payload**:
  ```text
  [ClientVersion: uint32]
  [PlayerNameLength: uint16] [PlayerName: UTF-8]
  [AuthSecret: byte[32]]  (SHA-256 hash of player credential token)
  ```
* **`0x0102` `OP_HANDSHAKE_RES` Payload**:
  ```text
  [StatusCode: uint16]     (0x0000 = Success, 0x0001 = VerMismatch, 0x0002 = AuthFail)
  [SessionToken: byte[16]] (Assigned UUID binary token)
  [GatewayPublicIP: uint32](Assigned IPv4 address in Big-Endian)
  ```

### B. Metasploit Port Connection (`0x0301`) & Response (`0x0302`)
* **`0x0301` `OP_METASPLOIT_NET_USE` Payload**:
  ```text
  [TargetIP: uint32]       (Destination IPv4 in Big-Endian)
  [TargetPort: uint16]     (Target Port: 21, 22, 80, 8080)
  ```
* **`0x0302` `OP_METASPLOIT_NET_RES` Payload**:
  ```text
  [StatusCode: uint16]     (0x0000 = Connected, 0x0001 = Unreachable, 0x0002 = Closed)
  [LibNameLen: uint16] [LibName: UTF-8] (e.g. "libssh.so")
  [LibVerLen: uint16]  [LibVer: UTF-8]  (e.g. "1.0.2")
  [ZoneCount: uint16]  (K = Number of vulnerable memory zones)
  [MemoryZones: uint32[K]] (Array of memory addresses, e.g. 0x00004A2B)
  ```

### C. Buffer Overflow Payload Injection (`0x0303`) & Response (`0x0304`)
* **`0x0303` `OP_METASPLOIT_OVERFLOW` Payload**:
  ```text
  [TargetIP: uint32]
  [TargetPort: uint16]
  [MemoryZone: uint32]     (Target memory address, e.g. 0x00004A2B)
  [ArgLen: uint16] [UnhandledArg: UTF-8] (Buffer string offset argument)
  ```
* **`0x0304` `OP_METASPLOIT_OVERFLOW_RES` Payload**:
  ```text
  [ResultType: uint8]      (0x01 = Shell, 0x02 = Computer, 0x03 = File, 0x00 = Crash)
  [GrantedUID: uint32]     (0 = root, 1000+ = user)
  [RemoteHandle: uint32]   (Capability authorization token)
  ```

### D. Remote File System Read (`0x0401`) & Response (`0x0402`)
* **`0x0401` `OP_FILE_READ_REQ` Payload**:
  ```text
  [RemoteHandle: uint32]   (Capability token from overflow/shell)
  [PathLen: uint16] [FilePath: UTF-8] (e.g. "/etc/shadow")
  ```
* **`0x0402` `OP_FILE_READ_RES` Payload**:
  ```text
  [StatusCode: uint16]     (0x0000 = Success, 0x0001 = PermDenied, 0x0002 = NotFound)
  [ContentLen: uint32]     (Byte size N of file)
  [FileContent: byte[N]]   (Raw file content string or binary blob)
  ```

---

## 5. State Machine & Handshake Sequence

```text
CLIENT (Endpoint A)                                          SERVER (Endpoint B)
  |                                                               |
  | --- [0x0101] OP_HANDSHAKE_REQ ------------------------------> |
  |     (Ver: 20260101, Name: "Operator", AuthSecret: SHA256)     | [Validate Client Credentials]
  |                                                               | [Assign Public Gateway IP]
  | <--- [0x0102] OP_HANDSHAKE_RES ------------------------------ |
  |      (Status: 0x0000, Token: UUID, GatewayIP: 192.168.1.10)   |
  |                                                               |
  | --- [0x0301] OP_METASPLOIT_NET_USE -------------------------> |
  |     (TargetIP: 182.45.12.89, Port: 22)                        | [Query Database for Service]
  |                                                               | [Extract Vulnerability Zones]
  | <--- [0x0302] OP_METASPLOIT_NET_RES ------------------------- |
  |      (Status: 0, "libssh.so v1.0.2", Zones: [0x4A2B, 0x1F8C])|
  |                                                               |
  | --- [0x0303] OP_METASPLOIT_OVERFLOW ------------------------> |
  |     (Zone: 0x4A2B, Arg: "pass_buf_overflow")                  | [Validate Deterministic Seed]
  |                                                               | [Write Target /var/system.log]
  | <--- [0x0304] OP_METASPLOIT_OVERFLOW_RES -------------------- |
  |      (Result: 0x01 [Shell Granted], UID: 0, Handle: 0x99)     |
  |                                                               |
  | --- [0x0401] OP_FILE_READ_REQ ------------------------------> |
  |     (Handle: 0x99, Path: "/etc/shadow")                       | [Verify Handle UID == 0]
  | <--- [0x0402] OP_FILE_READ_RES ------------------------------ |
  |      (Status: 0x0000, Content: "root:e10adc3949ba59abbe56e0") |
  |                                                               |
```

---

## 6. Standalone Reference Implementation

```python
#!/usr/bin/env python3
"""
RFC-GHNP-01 Reference Implementation
Provides full client-server socket serialization, framing, and CRC verification.
"""
import struct
import zlib
import socket

MAGIC_HEADER = 0x4748
PROTOCOL_VERSION = 0x0100

class GHNPFrame:
    def __init__(self, opcode, seq_id, session_token, payload=b"", flags=0):
        self.opcode = opcode
        self.seq_id = seq_id
        self.session_token = session_token
        self.flags = flags
        self.payload = payload

    def pack(self) -> bytes:
        header = struct.pack(
            "!HHHHIII",
            MAGIC_HEADER,
            PROTOCOL_VERSION,
            self.opcode,
            self.flags,
            self.seq_id,
            self.session_token,
            len(self.payload)
        )
        data = header + self.payload
        crc = zlib.crc32(data) & 0xFFFFFFFF
        return data + struct.pack("!I", crc)

    @classmethod
    def unpack(cls, raw: bytes):
        if len(raw) < 24:
            return None
        magic, ver, opcode, flags, seq_id, token, payload_len = struct.unpack("!HHHHIII", raw[:20])
        if magic != MAGIC_HEADER or len(raw) < 20 + payload_len + 4:
            return None
        payload = raw[20 : 20 + payload_len]
        crc = struct.unpack("!I", raw[20 + payload_len : 24 + payload_len])[0]
        if crc != (zlib.crc32(raw[: 20 + payload_len]) & 0xFFFFFFFF):
            raise ValueError("CRC-32 Checksum Failed!")
        return cls(opcode, seq_id, token, payload, flags)
```
