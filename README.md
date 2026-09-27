# Cisco CCNA Labs

![CCNA](https://img.shields.io/badge/CCNA-200--301-blue)
![Packet Tracer](https://img.shields.io/badge/Packet%20Tracer-8.x-orange)
![Labs](https://img.shields.io/badge/Labs-success)
![License](https://img.shields.io/badge/License-MIT-yellow)

# Cisco CCNA Labs

Hands-on Cisco networking labs built in Packet Tracer — routing, switching, DHCP, and enterprise topologies. Each lab includes a topology diagram, configuration files, and verification.

---

## Labs

| # | Lab | Topic | Folder | Status |
|---|-----|-------|--------|--------|
| 01 | Console & VTY Security | Router security, passwords, encryption | `Basic-Router-Security/Lab-3` | Done |
| 02 | Static Routing Lab 1 | 4 routers, 2 PCs, static routes | `Static Routing Labs/Static Routing Lab1` | Done |
| 03 | VLSM Lab 1 | 4 LANs, VLSM subnetting, /30 WAN | `VLSM Labs/VLSM-Lab1` | Done |
| 04 | RIPv2 Multi-Site Enterprise | 4 routers, 3 LANs, 24 PCs, 9 servers | `RIPv2-Labs/RIPv2-Multi-Site-Enterprise` | Done |
| 05 | RIPv2 Multi-Site Redundant | 4 LANs, 8 routers, redundant ring, FTP | `RIPv2-Labs/RIPv2-Multi-Site-Redundant` | Done |
| 06 | EIGRP Multi-Router + FTP + NTP | 13 routers, 6 LANs, FTP, NTP, CDP | `EIGRP-Labs/EIGRP-Multi-Router-FTP-NTP` | Done |
| 07 | EIGRP Multi-Site Redundant | EIGRP version of RIPv2 redundant ring | `EIGRP-Labs/EIGRP-Multi-Site-Redundant` | Done |
| 08 | BGP Basic Peering | 2 routers, eBGP, 2 ASes | `BGP Labs/BGP-Basic-Peering` | Done |
| 09 | BGP Multi-AS Chain | 5 routers, 5 ASes, AS path | `BGP Labs/BGP-Multi-AS-Chain` | Done |
| 10 | DHCP Relay Multi-LAN | Centralized DHCP server, ip helper-address | `DHCP-Labs/DHCP-Multi-LAN-Enterprise-Network` | Done |
| 11 | DHCP Hub-and-Spoke EIGRP | 4 LANs, 5 routers, DHCP per LAN | `DHCP-Labs/DHCP-Hub-Spoke-EIGRP` | Done |
| 12 | EIGRP 12-Router WAN | 12 routers, 11 serial links, DHCP relay, wireless | `EIGRP-Labs/EIGRP-12-Router-WAN-DHCP-Relay` | Done |
| 13 | OSPF Single-Area | Single-area OSPF with multi-router topology | `OSPF-Labs/` | Planned |
| 14 | VLANs + Trunking | VLAN segmentation, 802.1Q trunking | `VLAN-Labs/` | Planned |
| 15 | Inter-VLAN Routing | Router-on-a-stick, L3 switching | `VLAN-Labs/` | Planned |
| 16 | ACLs | Standard, extended, named ACLs | `ACL-Labs/` | Planned |
| 17 | NAT / PAT | Static, dynamic, overload | `NAT-Labs/` | Planned |
| 18 | IPv6 | Addressing, static, OSPFv3 | `IPv6-Labs/` | Planned |

---

## Skills Covered

- IPv4 addressing and subnetting
- VLSM design
- Static routing
- RIPv2, EIGRP, BGP (eBGP)
- DHCP (router-based and relay)
- FTP, NTP, CDP
- Serial WAN links (DCE/DTE, clock rate)
- Wireless integration
- Router security (console, VTY, SSH)
- Multi-router and multi-LAN topologies
- Network troubleshooting and verification

---

## Tools

- Cisco Packet Tracer 8.x
- Cisco 2911 and PT1000 routers
- Cisco 2960 switches

---

## How to Use

1. Clone the repo:
   ```bash
   git clone https://github.com/0x9z/Cisco-CCNA-Labs.git
   ```
2. Open any `.pkt` file in Cisco Packet Tracer
3. Read the lab's `README.md` for objectives and configuration
4. Verify with `ping`, `tracert`, and `show` commands

---

## Author

**Zero** — Linux & IT Infrastructure Specialist

- Website: [zero.ma](https://zero.ma)
- GitHub: [@0x9z](https://github.com/0x9z)
- LinkedIn: [linkedin.com/in/0x9z](https://linkedin.com/in/0x9z)

---

## License

MIT — free to use for learning.
