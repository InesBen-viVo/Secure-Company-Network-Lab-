# 🔍 Reconnaissance — Algérie Télécom Network Lab

**Lab:** Design and Implementation of a Secure Company Network System  
**Author:** Bendib Ines  
**Institution:** Mediterranean Institute of Management (INSIM)  
**Supervisor:** Mr. Bouzoubia Ramzi  
**Academic Year:** 2024 – 2025  

---

## 1. Target Organization Overview

**Algérie Télécom Group** is an Algerian public economic enterprise operating in the telecommunications sector. Its primary objective is the implementation, coordination, and supervision of major telecommunications projects across Algeria.

- **Founded:** November 9, 2017 (formally structured)  
- **Type:** Joint-stock public enterprise  
- **Sector:** Telecommunications (fixed, mobile, satellite, fiber optics)  

### 1.1 Subsidiaries
| Subsidiary | Role |
|---|---|
| Algérie Télécom (AT) | Fixed telephony, broadband, wireless |
| Algérie Télécom Mobile (Mobilis) | Mobile and wireless high-speed internet |
| Algérie Télécom Satellite (ATS) | Satellite telecommunications |
| Algérie Télécom Europe (ATE) | Manages submarine cable ORVAL/ARVAL (DZ–Europe) |
| COMINTAL | Dark fiber optic raw solutions |
| SATICOM | Modern IT communication solutions for enterprises |

---

## 2. Network Infrastructure Reconnaissance

### 2.1 External Network

Algeria Telecom's external network covers all physical and logical interconnections between Algeria and the global telecommunications infrastructure.

**Key capabilities:**
- Global internet access for Algerian users
- Traffic redundancy and resilience (link failover)
- International transit of governmental, commercial, and personal data
- Integration into global DNS, exchange points, and cloud infrastructure

#### Submarine Fiber Optic Cables

| Cable | Landing (DZ) | Main Link | Capacity | Status |
|---|---|---|---|---|
| SEA-ME-WE-4 | Annaba | France – Asia – Middle East – Africa | >1.28 Tbps | Active (since 2005) |
| Medex | Algiers | Marseille, France | Multi-Tb | Active (2022) |
| Orval/Alval | Oran / Algiers | Valence, Spain | 20 Tbps | Active (2021) |
| SMW-5 (planned) | Algiers / Skikda | Europe – Asia – Africa | >36 Tbps | Under study |

**Technical characteristics of submarine links:**
- Latency < 50 ms to Europe
- Path redundancy via multiple entry/exit points
- Scalable bandwidth using DWDM
- Automatic traffic rerouting on cable cuts

### 2.2 Internal Network Architecture

Algeria Telecom's internal infrastructure follows a **three-tier hierarchical architecture**:

```
┌─────────────────────────────────────────────────────┐
│              National Backbone (Core)               │
│         Ultra high-speed fiber > 100 Gbps           │
│    Connects wilayas, cities, regional data centers  │
└───────────────────┬─────────────────────────────────┘
                    │
┌───────────────────▼─────────────────────────────────┐
│           Aggregation Network Layer                  │
│     DSLAM, OLT links to subscriber areas            │
└───────────────────┬─────────────────────────────────┘
                    │
┌───────────────────▼─────────────────────────────────┐
│         Access Network (Last Mile)                   │
│  ADSL, VDSL, FTTH, 4G LTE, GPON/EPON               │
└─────────────────────────────────────────────────────┘
```

#### Transmission Technologies

| Technology | Use | Throughput |
|---|---|---|
| SDH/SONET | Legacy base networks | Up to 10 Gbps |
| DWDM | Optical multiplexing in backbone | > 400 Gbps/cable |
| MPLS | Multiprotocol IP transport | QoS + prioritization |
| Metro Ethernet | Regional aggregation | 1 to 100 Gbps |

#### Customer Access Technologies

| Technology | Type | Area Served | Throughput |
|---|---|---|---|
| ADSL/VDSL | Copper | Urban/dense areas | 10 – 50 Mbps |
| FTTH | Fiber | Urban areas | > 100 Mbps |
| LTE 4G Fixed | Wireless (SIM) | Rural areas | 10 – 40 Mbps |
| WiMAX (legacy) | Point-to-multipoint radio | Remote sites | 1 – 5 Mbps |

### 2.3 Data Centers & NOC

| Site | Role |
|---|---|
| Algiers (Bir Mourad Raïs) | Primary national DC, cloud services |
| Oran | Regional DC |
| Constantine | Regional DC |

- **Monitoring:** National NOC (Network Operations Center), SNMP, NetFlow
- **Security Stack:** Arbor, Fortinet, Cisco Secure, SIEM + IDS/IPS

---

## 3. Security Threat Landscape (Recon Phase)

### 3.1 External Threat Vectors Identified

- DDoS attacks from international sources
- Optical wiretapping on submarine cables
- BGP hijacking attacks
- Malicious/accidental submarine cable cuts

### 3.2 Internal Threat Vectors Identified

- Unauthorized access to network equipment
- Internal attacks / insider threats
- Traffic capture and analysis (Wireshark, tcpdump-based)
- Misconfigured services and default configurations

### 3.3 Security Countermeasures in Place

- Anti-DDoS protection at network edge
- L2/L3/L7 encryption for sensitive flows (government traffic)
- Continuous monitoring from Security Operations Center (SOC)
- SIEM + IDS/IPS integration
- Tools: Arbor, Fortinet, Cisco Secure

---

## 4. Lab Objectives

The goal of this practical lab is to:

1. Design a **secure, hierarchical network** for Algérie Télécom
2. Implement **VLAN segmentation** for traffic isolation
3. Configure **Cisco ASA firewalls** with strict DMZ policies
4. Deploy **OSPF dynamic routing** and **HSRP high availability**
5. Secure remote access via **SSH + ACLs**
6. Enable **VoIP** and **WLC** wireless infrastructure
7. Build a **Site-to-Site IPsec VPN** for secure inter-site communication

---

*Next Phase → [Enumeration.md](./Enumeration.md)*
