# EIGRP Multi-Router Network with FTP & NTP

![Topology](topology.)

## 📌 Overview

A large-scale enterprise network built in Cisco Packet Tracer using
**EIGRP** as the dynamic routing protocol, with **FTP file distribution**,
**NTP time synchronization**, and **CDP neighbor discovery**.

The topology spans **9 routers** + **4 serial hub routers (Router-PT)**,
6 FTP servers, an NTP server, and 4 PCs across **6 LANs** and
**11 point-to-point WAN links** — including redundant paths between
the serial hub routers.

## 🎯 Objective

- Configure EIGRP AS 1 across all 13 routers with `no auto-summary`
- Provide FTP file distribution across two database rooms
- Synchronize all routers with a central NTP server (`192.168.3.17`)
- Verify full connectivity using `ping`, `tracert`, `show ip route`
- Map the topology with CDP neighbor discovery
- Demonstrate redundant path selection with EIGRP metrics

## 📊 Topology

![Topology](topology.)

### LANs

| LAN | Network | Purpose |
|-----|---------|---------|
| LAN1 | 192.168.1.0/24 | PC1 · R1 gateway |
| LAN2 | 192.168.2.0/24 | FTP Database Room 1 (3 servers) |
| LAN3 | 192.168.3.0/24 | PC2 · NTP Server (192.168.3.17) |
| LAN4 | 192.168.4.0/24 | PC3 · R5 gateway |
| LAN5 | 192.168.5.0/24 | FTP Database Room 2 (3 servers) |
| LAN9 | 192.168.9.0/24 | PC4 · R6 gateway |

### WAN Links (all /30)

| Link | Network |
|------|---------|
| R1 ↔ R2 | 10.0.0.0/30 |
| R2 ↔ S-R1 | 20.0.0.0/30 |
| S-R1 ↔ S-R2 | 88.200.15.0/30 |
| S-R1 ↔ S-R3 | 144.250.12.0/30 |
| S-R2 ↔ S-R4 | 17.147.145.0/30 |
| S-R3 ↔ S-R4 | 180.16.1.0/30 |
| S-R2 ↔ R4 | 50.0.0.0/30 |
| S-R3 ↔ R3 | 30.0.0.0/30 |
| S-R4 ↔ R5 | 40.0.0.0/30 |
| R4 ↔ R6 | 60.0.0.0/30 |
| R4 ↔ R7 | 70.0.0.0/30 |

### Devices Used

- **9×** Cisco 2911 routers (R1–R7 + 2 shown in diagram)
- **4×** PT1000 serial routers (S-R1, S-R2, S-R3, S-R4)
- **6×** Server-PT (FTP1–FTP6)
- **1×** Server-PT (NTP Server, 192.168.3.17)
- **4×** PC-PT (PC1–PC4)
- **4×** Cisco 2960 switches

## 📋 IP Addressing Table

### Router Interfaces

| Router | Interface | IP | Mask |
|--------|-----------|-----|------|
| R1 | Gig0/0 | 192.168.1.1 | /24 |
| R1 | Gig0/1 | 10.0.0.1 | /30 |
| R2 | Gig0/0 | 10.0.0.2 | /30 |
| R2 | Gig0/1 | 20.0.0.1 | /30 |
| R3 | Gig0/0 | 30.0.0.1 | /30 |
| R3 | Gig0/1 | 192.168.3.1 | /24 |
| R4 | Gig0/0 | 50.0.0.2 | /30 |
| R4 | Gig0/1 | 60.0.0.1 | /30 |
| R4 | Gig0/2 | 70.0.0.1 | /30 |
| R5 | Gig0/0 | 40.0.0.2 | /30 |
| R5 | Gig0/1 | 192.168.4.1 | /24 |
| R6 | Gig0/0 | 60.0.0.2 | /30 |
| R6 | Gig0/1 | 192.168.9.1 | /24 |
| R7 | Gig0/0 | 70.0.0.2 | /30 |
| R7 | Gig0/1 | 192.168.5.1 | /24 |
| S-R1 | Se2/0 | 144.250.12.1 | /30 |
| S-R1 | Se3/0 | 88.200.15.1 | /30 |
| S-R1 | Gig6/0 | 20.0.0.2 | /30 |
| S-R2 | Se2/0 | 17.147.145.1 | /30 |
| S-R2 | Se3/0 | 88.200.15.2 | /30 |
| S-R2 | Gig6/0 | 50.0.0.1 | /30 |
| S-R3 | Se2/0 | 144.250.12.2 | /30 |
| S-R3 | Se3/0 | 180.16.1.2 | /30 |
| S-R3 | Gig6/0 | 30.0.0.2 | /30 |
| S-R4 | Se2/0 | 17.147.145.2 | /30 |
| S-R4 | Se3/0 | 180.16.1.1 | /30 |
| S-R4 | Gig6/0 | 40.0.0.1 | /30 |

### End Devices

| Device | IP | Gateway |
|--------|-----|---------|
| PC1 | 192.168.1.54 | 192.168.1.1 |
| PC2 | 192.168.3.x | 192.168.3.1 |
| PC3 | 192.168.4.82 | 192.168.4.1 |
| PC4 | 192.168.9.155 | 192.168.9.1 |
| FTP1 | 192.168.2.120 | 192.168.2.1 |
| FTP2 | 192.168.2.36 | 192.168.2.1 |
| FTP3 | 192.168.2.8 | 192.168.2.1 |
| FTP4 | 192.168.5.6 | 192.168.5.1 |
| FTP5 | 192.168.5.9 | 192.168.5.1 |
| FTP6 | 192.168.5.7 | 192.168.5.1 |
| NTP Server | 192.168.3.17 | 192.168.3.1 |

## ⚙️ EIGRP Configuration

Applied on **all 13 routers**:

```
router eigrp 1
 no auto-summary
 network <classful-network>
 exit
```

| Router | Network Statements |
|--------|--------------------|
| R1 | `192.168.1.0` · `10.0.0.0` |
| R2 | `10.0.0.0` · `20.0.0.0` |
| R3 | `30.0.0.0` · `192.168.3.0` |
| R4 | `50.0.0.0` · `60.0.0.0` · `70.0.0.0` |
| R5 | `40.0.0.0` · `192.168.4.0` |
| R6 | `60.0.0.0` · `192.168.9.0` |
| R7 | `70.0.0.0` · `192.168.5.0` |
| S-R1 | `88.200.15.0` · `144.250.12.0` · `20.0.0.0` |
| S-R2 | `88.200.15.0` · `17.147.145.0` · `50.0.0.0` |
| S-R3 | `144.250.12.0` · `180.16.1.0` · `30.0.0.0` |
| S-R4 | `17.147.145.0` · `180.16.1.0` · `40.0.0.0` |

### ⚠️ Key Notes

- **EIGRP AS number must match** on all routers (AS 1 used here).
- `no auto-summary` is required for discontiguous subnets.
- Classful `network` statements — no masks, no wildcards.
- Serial **DCE interfaces require `clock rate 64000`**.
- Neighbor adjacencies appear automatically as `%DUAL-5-NBRCHANGE`.
- EIGRP supports **equal-cost load balancing** across redundant paths.

## 🕐 NTP Configuration

Central NTP server: **192.168.3.17** (Server-PT, stratum 1)

On every router:

```
ntp server 192.168.3.17
```

Verify:

```
show ntp status
show ntp association
```

Expected:

```
Clock is synchronized, stratum 2, reference is 192.168.3.17
```

## 📁 FTP Configuration

### FTP Database Room 1 (192.168.2.0/24)
- **FTP1** — 192.168.2.120 · username `zeroftp1`
- **FTP2** — 192.168.2.36
- **FTP3** — 192.168.2.8

### FTP Database Room 2 (192.168.5.0/24)
- **FTP4** — 192.168.5.6
- **FTP5** — 192.168.5.9
- **FTP6** — 192.168.5.7 · username `zeroftp6`

### FTP Test (PC1 → FTP1)

```
C:\>ftp 192.168.2.120
Username: zeroftp1
Password: ****
ftp> dir
ftp> put key.txt
ftp> put secret.txt
ftp> quit
```

### FTP Test (PC2 → FTP1 → FTP6)

```
C:\>ftp 192.168.2.120
ftp> get key.txt
ftp> get secret.txt
ftp> quit

C:\>ftp 192.168.5.7
ftp> put key.txt
ftp> put secret.txt
ftp> quit
```

**Result:** Files transferred end-to-end across the entire EIGRP-routed topology. ✅

## 🔍 Verification

### Ping across network (PC1 → FTP4)

```
C:\>ping 192.168.5.6
Reply from 192.168.5.6: bytes=32 time=58ms TTL=122
Sent = 4, Received = 4, Lost = 0 (0% loss)
```

### Tracert to FTP1

```
C:\>tracert 192.168.2.120
  1   0 ms      192.168.1.1        (R1)
  2   0 ms      10.0.0.2           (R2)
  3   0 ms      20.0.0.2           (S-R1)
  4   34 ms     88.200.15.2        (S-R2)
  5   43 ms     50.0.0.2           (R4)
  6   47 ms     70.0.0.2           (R7)
  7   24 ms     192.168.5.6        (FTP4)
Trace complete.
```

### CDP Neighbor Discovery (S-R1)

```
S-R1#show cdp neighbor

Device ID    Local Intrfce   Holdtme    Capability   Platform    Port ID
R2           Gig 6/0          132            R       C2900       Gig 0/2
S-R3         Ser 2/0          135            R       PT1000      Ser 2/0
S-R2         Ser 3/0          129            R       PT1000      Ser 3/0
```

### EIGRP Route Table (S-R1)

```
S-R1#show ip route

D    10.0.0.0/8      [90/3072]      via 20.0.0.1, Gig6/0
D    17.0.0.0/8      [90/21024000]  via 88.200.15.2, Serial3/0
D    30.0.0.0/8      [90/20512256]  via 144.250.12.2, Serial2/0
D    40.0.0.0/8      [90/21024256]  via 144.250.12.2, Serial2/0
                     [90/21024256]  via 88.200.15.2, Serial3/0
D    192.168.5.0/24 [90/20515072]  via 88.200.15.2, Serial3/0
```

**Notice:** Route to `40.0.0.0/8` has **two equal-cost paths** — EIGRP load balancing in action. ✅

## 🧠 What I Learned

- **EIGRP configuration** — AS number, `no auto-summary`, classful networks
- **DCE/DTE** — clock rate on DCE side of serial links
- **NTP synchronization** — central time source across all routers
- **FTP file distribution** — client/server file transfer over routed networks
- **CDP discovery** — mapping topology without a diagram
- **Redundant path selection** — EIGRP picks best route, load balances on equal cost
- **Self-debugging** — caught NTP IP typo, missing clock rate
- **Convergence** — adjacencies form fast (`%DUAL-5-NBRCHANGE`)

## 🛠️ Tools

- Cisco Packet Tracer 8.x
- 9× Cisco 2911 routers + 4× PT1000 serial routers
- 6× FTP servers + 1× NTP server

## 📸 Screenshots

| Topology | EIGRP Routes | NTP Status | FTP Session |
|----------|--------------|------------|-------------|
| `topology.png` | `show-ip-route.png` | `show-ntp-status.png` | `ftp-session.png` |

## 👤 Author

**Zero** — Linux & IT Infrastructure Specialist

- 🌐 [zero.ma](https://zero.ma) · [cybernetwork.technology](https://cybernetwork.technology)
- 🐙 [GitHub @0x9z](https://github.com/0x9z)
- 💼 [LinkedIn](https://linkedin.com/in/0x9z)

## 📄 License

MIT — free to use for learning.
