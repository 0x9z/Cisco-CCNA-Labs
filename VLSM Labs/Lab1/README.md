# VLSM Multi-LAN Enterprise Network

## Scenario
Design and configure a network with 4 LANs of varying sizes, connected through 2 routers via a point-to-point link. Subnet the 192.168.5.0/24 network using VLSM to efficiently address each LAN, assign the first usable IP to each PC and the last usable IP to each router interface, then configure static routing so all PCs can reach each other.

**Requirements:**
- LAN1: 45 hosts | LAN2: 64 hosts | LAN3: 14 hosts | LAN4: 9 hosts
- Point-to-point link between R1 and R2
- Static routes on both routers

## VLSM Addressing Table

| Network | Hosts Needed | Subnet | Range | Broadcast |
|---|---|---|---|---|
| LAN2 | 64 | 192.168.5.0/25 | .1 - .126 | .127 |
| LAN1 | 45 | 192.168.5.128/26 | .129 - .190 | .191 |
| LAN3 | 14 | 192.168.5.192/27 | .193 - .222 | .223 |
| LAN4 | 9 | 192.168.5.224/28 | .225 - .238 | .239 |
| R1-R2 Link | 2 | 192.168.5.240/30 | .241 - .242 | .243 |

## Static Routes

**R1:**
```
ip route 192.168.5.192 255.255.255.224 192.168.5.242
ip route 192.168.5.224 255.255.255.240 192.168.5.242
```

**R2:**
```
ip route 192.168.5.0 255.255.255.128 192.168.5.241
ip route 192.168.5.128 255.255.255.192 192.168.5.241
```


## What I Learned
The hardest part wasn't the subnetting math — it was avoiding overlap between the point-to-point link subnet and the LAN subnets. My first attempt used a /29 for the link instead of /30, which ate into address space that LAN3 and LAN4 needed, breaking connectivity between the two router sides. Once I traced each subnet's exact start and end address, the overlap became obvious — and the fix was just recalculating the link as a proper /30 starting right where the last LAN subnet ended.

## Result
Full connectivity confirmed — PCs on both sides of the network (behind R1 and behind R2) successfully ping across the point-to-point link.

## Tools
Cisco Packet Tracer 8.x

##Download the lab [here](https://github.com/0x9z/Cisco-CCNA-Labs/raw/refs/heads/main/lab4/Lab4-VLSM.pkt)
