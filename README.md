# 🛡️ Secure-Company-Network-Lab

> **Bachelor Thesis Lab** — Design and Implementation of a Secure Network Infrastructure for Algérie Télécom  
> **Author:** Bendib Ines | **Institution:** INSIM | **Year:** 2024–2025  

---

## 📁 Repository Structure

```
Secure-Company-Network-Lab/
├── README.md              ← You are here
├── Recon.md               ← Organization & infrastructure reconnaissance
├── Enumeration.md         ← Network analysis, protocols & threat enumeration
├── Exploitation.md        ← Full device configuration & implementation
├── Screenshots/           ← Topology diagrams & configuration proof
└── Final_Report.md        ← Full thesis findings, conclusions & references
```

---

## 🎯 Lab Objectives

| # | Objective |
|---|---|
| 1 | Design a hierarchical secure network for a telecom enterprise |
| 2 | Segment traffic using VLANs (Management, LAN, WLAN, VoIP, DMZ) |
| 3 | Configure Cisco ASA dual-firewall with DMZ zone architecture |
| 4 | Implement OSPF dynamic routing across all devices |
| 5 | Deploy HSRP for high-availability gateway redundancy |
| 6 | Secure all remote access with SSH v2 + ACLs |
| 7 | Build a Site-to-Site IPsec VPN between two sites |
| 8 | Enable VoIP communication over VLAN 70 |
| 9 | Harden all devices against common Layer 2 and Layer 3 attacks |

---

## 🗺️ Network Topology

```
                         Internet
                             │
               ┌─────────────▼──────────────┐
               │     ASA Firewall 1 (FWL1)  │
               │  Outside(0)| DMZ(70)|Inside(100)│
               └─────────────┬──────────────┘
                             │
           ┌─────────────────▼──────────────────┐
           │         Core Switching Layer        │
           │  CORE-SW ←──LACP EtherChannel──→ CORE-SW1│
           │    HSRP Active (Pri:110)  Standby   │
           └──────┬──────────────────────┬───────┘
                  │                      │
        ┌─────────▼────┐       ┌─────────▼────┐
        │   MK-SW      │       │  Server-SW   │
        │ (Access SW)  │       │ (VLAN 90)    │
        └──────────────┘       └──────────────┘
               │
     ┌─────────▼──────────┐
     │   ASA Firewall 2   │  ←── IPsec VPN Tunnel ──→  Remote Site
     │       (FWL2)       │
     └────────────────────┘
```

---

## 📌 IP Addressing Summary

| Segment | VLAN | Network | Gateway |
|---|---|---|---|
| Management | 10 | 192.168.20.0/24 | 192.168.20.1 |
| LAN | 20 | 172.16.0.0/16 | 172.16.0.1 |
| WLAN | 50 | 10.20.0.0/16 | 10.20.0.1 |
| VoIP | 70 | 172.30.0.0/16 | 172.30.0.1 |
| DMZ | — | 10.11.11.0/27 | 10.11.11.1 |
| Inside Servers | 90 | 10.11.11.32/27 | 10.11.11.33 |

---

## 🔐 Security Features

- ✅ SSH v2 + VTY ACL (management subnet only)
- ✅ Service password-encryption + enable secret
- ✅ STP PortFast + BPDUGuard (edge ports)
- ✅ VLAN 199 Blackhole (unused ports isolated)
- ✅ Dual Cisco ASA Firewalls with DMZ zone
- ✅ Extended ACLs (ICMP, HTTP, DNS filtering)
- ✅ Dynamic NAT on all inside interfaces
- ✅ Site-to-Site IPsec VPN (3DES + SHA / IKEv1)
- ✅ OSPF with Area 0 backbone routing
- ✅ HSRP failover (< 10s recovery)
- ✅ EtherChannel LACP (link redundancy + bandwidth)

---

## 📖 Navigation

| File | Description |
|---|---|
| [Recon.md](./Recon.md) | Organization background, infrastructure mapping, threat landscape |
| [Enumeration.md](./Enumeration.md) | VLAN enumeration, IP table, protocol inventory, attack analysis |
| [Exploitation.md](./Exploitation.md) | Step-by-step Cisco configurations with commands |
| [Screenshots/](./Screenshots/) | Lab screenshots and topology evidence |
| [Final_Report.md](./Final_Report.md) | Full report with validation results, lessons learned, and references |

---

## 🛠️ Tools Used

| Tool | Purpose |
|---|---|
| Cisco Packet Tracer | Network simulation and configuration |
| Cisco IOS CLI | Router, switch, and firewall configuration |
| Cisco ASA | Perimeter security, NAT, VPN, ACLs |
| Cisco CME | VoIP call manager for IP phones |
| OSPF | Dynamic routing protocol |
| IKEv1 / IPsec | VPN encryption |

---

## 📚 Academic Context

This lab was developed as a **Bachelor's thesis project** at INSIM (Mediterranean Institute of Management), Constantine, Algeria. It demonstrates the application of enterprise network security principles to a real-world telecommunications operator context.

---

*Made with dedication by Bendib Ines 💙*
