# Multi-Site EIGRP Network with Wireless DHCP Relay

## 📌 Overview

A large-scale enterprise network built in Cisco Packet Tracer, connecting a main site, a wireless branch, and a remote office across an **11-router serial EIGRP chain**. The main site hosts centralized DHCP, NTP, and FTP servers; a wireless LAN (phones, laptops, tablets) connects through an Access Point at the far end of the chain and relies on **DHCP relay** across all 11 hops to reach the central DHCP server. A separate remote branch (IP phone + local server) connects through a different point in the chain.

This lab stress-tests EIGRP convergence, DHCP relay, and end-to-end connectivity across a long serial topology — deliberately longer than any real-world design would use, to see how far these mechanisms actually scale.

## 🎯 Objective

- Build and converge EIGRP across an 11-router serial chain
- Extend DHCP relay across the full chain so wireless clients reach a centralized DHCP server
- Connect a remote branch (IP phone + local server) into the same EIGRP domain
- Verify end-to-end connectivity, routing paths, and FTP transfer across the full topology

## 📊 Topology

```
[Main Site]                                                          [Wireless Branch]
192.168.1.0/24                                                       192.168.200.0/24
DHCP / NTP / FTP servers                                             Laptops, Smartphones, Tablet
      │                                                                      │
     R1 ── 10.0.0.0/30 ── SR1 ── 20.0.0.0/30 ── SR2 ── 30.0.0.0/30 ── SR3 ── ... ── SR11 ── AP
                                                                                      (11 serial hops total)

                                        ┌─ SR4 ── 60.0.0.0/30 ── 192.168.60.0/24 [Remote Branch: IP Phone, Local Server]
```

- **Main Site LAN:** 192.168.1.0/24 — DHCP-SERVER, NTP-Server, FTP-Server
- **Serial chain:** Serial-Router-1 through Serial-Router-11, linked by point-to-point /30 links (10.0.0.0/30 through 110.0.0.0/30)
- **Remote Branch:** 192.168.60.0/24, branching off Serial-Router-4, with a Cisco 7960 IP Phone and a local server
- **Wireless Branch:** 192.168.200.0/24, at the far end (Serial-Router-11), served by an Access Point (not a home router)

## Devices Used

- 12× Cisco routers (R1 + Serial-Router-1 through Serial-Router-11)
- 1× Access Point (Linksys-WPC300N wireless module used on client devices)
- 3× Server-PT (DHCP, NTP, FTP)
- 1× Server-PT (remote branch local server)
- 1× Cisco 7960 IP Phone
- Wireless clients: laptops, smartphones, tablet, printer

## ⚙️ Key Configuration

### R1 (main site) — EIGRP + LAN

```
interface Gig0/0
 ip address 192.168.1.1 255.255.255.0
 no shutdown

interface Gig0/1
 ip address 10.0.0.1 255.255.255.252
 no shutdown

router eigrp 1
 no auto-summary
 network 192.168.1.0
 network 10.0.0.0
```

### Each Serial-Router (pattern repeated 11 times)

```
interface Serial2/0
 ip address <local> <mask>
 clock rate 64000   ! only on the DCE side of each link
 no shutdown

interface Serial3/0
 ip address <local> <mask>
 no shutdown

router eigrp 1
 no auto-summary
 network <upstream-link>
 network <downstream-link>
```

### Serial-Router-11 (final hop) — DHCP Relay for the wireless branch

```
interface Gig6/0
 ip address 192.168.200.1 255.255.255.0
 ip helper-address 192.168.1.10
 no shutdown
```

This is the only router in the chain that needs `ip helper-address` — it's the last hop before the actual DHCP broadcast domain (the AP's LAN), exactly like the single-hop DHCP relay lab, just at the end of a much longer chain.

## 🐛 Troubleshooting Notes

- Several typos along the way (`no shutdwon`, `clock-rate` without space, `int serial3` incomplete) — all caught immediately from the `% Invalid input` error and corrected in the same line.
- Early in the build, briefly tried `ip helper-address` on the wrong router (a mid-chain serial router) — realized helper-address only makes sense on the router directly facing the broadcast domain, not on transit routers.
- Wireless clients initially failed to reach the main site until the AP (not a home router) was used and DHCP relay was placed correctly on the final hop — see the companion DHCP Relay Lab for the earlier failed attempt with a home router that caused double-NAT isolation.

## 🔍 Verification

**Wireless client (Laptop1) IP config:**
```
Wireless0 Connection:
IPv4 Address....................: 192.168.200.31
Subnet Mask.....................: 255.255.255.0
Default Gateway.................: 192.168.200.1
```

**Ping + tracert from Laptop1 to the DHCP server (192.168.1.10) — 13 hops across the full chain:**
```
Reply from 192.168.1.10: bytes=32 time=250ms TTL=116
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)

Tracing route to 192.168.1.10:
 1  192.168.200.1   2  110.0.0.1   3  100.0.0.1   4  90.0.0.1
 5  80.0.0.1        6  70.0.0.1    7  60.0.0.1    8  50.0.0.1
 9  40.0.0.1       10  30.0.0.1   11  20.0.0.1   12  10.0.0.1
13  192.168.1.10
Trace complete.
```

**FTP transfer from Laptop1 to the FTP server (192.168.1.12) — full TCP session, not just ICMP:**
```
ftp> put file.txt
[Transfer complete - 3 bytes]
```

**Remote branch (PC2) reaching the same FTP server via a shorter, different path:**
```
Tracing route to 192.168.1.12:
 1  192.168.60.1   2  40.0.0.1   3  30.0.0.1   4  20.0.0.1   5  10.0.0.1   6  192.168.1.12
Trace complete.
```

This confirms EIGRP computes the best path independently for each site — the wireless branch takes 13 hops, while the remote branch (entering the chain further along) takes only 6.

## 🧠 What I Learned

- **DHCP relay scales across long chains** — `ip helper-address` only needs to sit on the last router before the client's broadcast domain, regardless of how many transit hops exist upstream.
- **EIGRP picks the best path per source**, not one fixed path for the whole network — two different sites reaching the same server took completely different hop counts.
- **Round-trip time compounds with hop count** — 200-250ms across 11-13 hops is a clear, measurable illustration of why real-world designs use hierarchical (core/distribution/access) topologies instead of long serial chains. This design is a deliberate stress test, not a real-world recommendation.
- **A working ping doesn't prove TCP works** — confirming the FTP session (control + data channel, login, file transfer) end-to-end was a stronger verification than ICMP alone.
- **Access Point vs. home router matters**: an AP bridges wireless clients into the existing LAN; a home router NATs them into an isolated subnet — a mistake from an earlier lab that this design deliberately avoided.

## ⚠️ Design Note

This 11-router serial chain is an intentional stress test of EIGRP and DHCP relay over a long path — not a real-world topology recommendation. A production network with this many sites would use a hierarchical design (core/distribution/access, or hub-and-spoke) to avoid the latency and single-point-of-failure risks of a long linear chain.

## 🛠️ Tools

- Cisco Packet Tracer 8.x
- 12× Cisco routers, 1× Access Point, 3× centralized servers, 1× IP Phone

## 👤 Author

Zero — Linux & IT Infrastructure Specialist
- 🌐 zero.ma · blog.zero.ma
- 🐙 GitHub @0x9z

## 📄 License

MIT — free to use for learning.
