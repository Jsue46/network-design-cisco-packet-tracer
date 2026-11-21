# Network Infrastructure Design — Cisco Packet Tracer

Academic project developed for the **Computer Networks 2** course at the Universidad de San Carlos de Guatemala (Second Semester 2026).

This repository contains the network simulation files, technical documentation, and configuration evidence for two lab practices. All topologies were designed and validated in **Cisco Packet Tracer**. The project was developed collaboratively as a group assignment.

---

## Overview

The practices cover advanced network design and configuration, including Layer 2 segmentation, redundancy protocols, dynamic routing, wireless integration, and network services — applied to realistic enterprise-scale scenarios.

---

## Practice 1 — Monte Alto School Network

Design and configuration of a multi-building campus network.

**Topics covered:**
- VLAN segmentation by academic level (Primary, Middle, High School)
- VLAN Trunking Protocol (VTP) in Server/Client mode
- Spanning Tree Protocol: PVST vs. Rapid PVST comparison
- Port Security with MAC address restrictions and shutdown policies
- Dynamic routing with EIGRP, RIP, and OSPF with route redistribution

---

## Practice 2 — Restaurant Multi-Floor Network

Design and configuration of a multi-floor enterprise network.

**Topics covered:**
- VLAN design: ADMIN (17), COCINA (27), WEB\_SERVERS (37), DHCP\_SERVERS (47)
- VLSM/FLSM subnetting for users, servers, and routing links
- Trunk links between multilayer and access switches
- LACP/EtherChannel link aggregation
- HSRP for gateway redundancy
- EIGRP dynamic routing
- DHCP for wired VLANs and wireless networks
- Wireless: SSID, WPA2, /25 addressing
- DNS and HTTP services

---

## Repository Structure

```
network-design-cisco-packet-tracer/
├── Practica1/
│   ├── Practica1_G25.pkt     # Cisco Packet Tracer simulation
│   ├── README.md             # Technical documentation
│   ├── assets/images/
│   └── docs/
└── Practica2/
    ├── Practica2_G25.pkt     # Cisco Packet Tracer simulation
    ├── README.md             # Technical documentation
    ├── assets/evidence/
    └── docs/
```

---

## Technologies

- Cisco Packet Tracer
- Protocols: VTP, STP/RSTP, PVST, EIGRP, OSPF, RIP, HSRP, LACP
- Services: DHCP, DNS, HTTP, WPA2

---

## Academic Context

| Field       | Detail                                         |
|-------------|------------------------------------------------|
| Course      | Computer Networks 2 (REDES2)                   |
| Institution | Universidad de San Carlos de Guatemala         |
| Semester    | Second Semester 2026                           |
| Type        | Group project                                  |
