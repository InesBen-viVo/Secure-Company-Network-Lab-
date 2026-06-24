# 📋 Enumeration — Network Analysis & Security Assessment

*Phase 2 of the Algérie Télécom Secure Network Lab*

---

## 1. Network Types Identified

| Network Type | Scope | Notes |
|---|---|---|
| PAN (Personal Area Network) | ~10 m | Bluetooth/USB peripherals |
| LAN (Local Area Network) | Building / campus | Core enterprise network |
| MAN (Metropolitan Area Network) | City-scale | Inter-site in same city |
| GAN (Global Area Network) | Worldwide | Internet / WAN backbone |
| VPN (Virtual Private Network) | Logical overlay | Secure tunnel over public IP |

---

## 2. Network Topologies in Use

| Topology | Description | Used In This Lab |
|---|---|---|
| Star | All nodes connect to a central switch | ✅ Access layer |
| Hierarchical (Tree) | Core → Distribution → Access | ✅ Overall design |
| Mesh | Redundant full connections | ✅ WAN/Core layer |
| Bus | Linear single cable | ❌ Legacy, not used |
| Ring | Circular data path | ❌ Legacy |
| Hybrid | Combination of topologies | ✅ Implied |

---

## 3. OSI Model Layer Analysis

| Layer | Name | Key Protocols / Devices |
|---|---|---|
| 7 | Application | HTTP, FTP, DNS, SSH, SNMP |
| 6 | Presentation | TLS/SSL, encoding |
| 5 | Session | NetBIOS, RPC |
| 4 | Transport | TCP, UDP |
| 3 | Network | IP, OSPF, BGP, HSRP, ACLs |
| 2 | Data Link | Ethernet, VLAN (802.1Q), STP, EtherChannel |
| 1 | Physical | Fiber, copper, wireless (802.11) |

---

## 4. VLAN Enumeration

VLANs configured in the lab topology for traffic segmentation:

| VLAN ID | Name | Purpose | Network Address |
|---|---|---|---|
| 10 | Management | Device management (SSH/Telnet) | 192.168.20.0/24 |
| 20 | LAN | General user data traffic | 172.16.0.0/16 |
| 50 | WLAN | Wireless user traffic | 10.20.0.0/16 |
| 70 | VoIP | Voice over IP telephony | 172.30.0.0/16 |
| 90 | INSIDE-SERVERS | Internal server farm | 10.11.11.32/27 |
| 199 | Blackhole | All unused/disabled ports | N/A (isolated) |

### 4.1 Key VLAN Design Decisions

- **Trunk Ports** (fa0/1, fa0/2): Carry all VLAN tags between switches using 802.1Q
- **Access Ports**: Assigned to a single VLAN per device role
- **VLAN 199 (Blackhole)**: Unused ports are placed here to prevent rogue device connectivity
- **VLAN 90 (INSIDE-SERVERS)**: Replaced VLAN 199 on Server-SW; ports fa0/3–fa0/5 assigned

---

## 5. IP Addressing / Subnetting Enumeration

| Segment | Network Address | Mask | Gateway | Broadcast |
|---|---|---|---|---|
| Management | 192.168.20.0 | /24 | 192.168.20.1 | 192.168.20.255 |
| WLAN | 10.20.0.0 | /16 | 10.20.0.1 | 10.20.255.255 |
| LAN | 172.16.0.0 | /16 | 172.16.0.1 | 172.16.255.255 |
| VoIP | 172.30.0.0 | /16 | 172.30.0.1 | 172.30.255.255 |
| DMZ | 10.11.11.0 | /27 | 10.11.11.1 | 10.11.11.31 |
| Inside Servers | 10.11.11.32 | /27 | 10.11.11.33 | 10.11.11.63 |

---

## 6. Protocol Enumeration

### 6.1 Routing Protocols

| Protocol | Role | Location |
|---|---|---|
| OSPF | Dynamic routing between routers, switches, and ASA firewall | Entire topology |
| HSRP | High-availability gateway redundancy between routers | Core / Distribution layer |
| Static Routes | Fixed paths for DMZ and server farm | ASA Firewall |

### 6.2 Security Protocols

| Protocol | Purpose |
|---|---|
| SSH v2 | Encrypted remote management (replaces Telnet) |
| ACL (Extended) | Restrict VTY access to trusted subnet 192.168.10.0/24 |
| STP + PortFast + BPDUGuard | Loop prevention on switches; protects edge ports |
| EtherChannel (LACP) | Link aggregation for bandwidth + redundancy between CORE-SW and CORE-SW1 |
| IPsec IKEv1 | Site-to-Site VPN tunnel encryption |

### 6.3 Service Protocols

| Protocol | Purpose |
|---|---|
| DHCP | Dynamic IP addressing for LAN/WLAN/VoIP clients |
| VoIP (SCCP/SIP) | IP telephone connectivity via VLAN 70 |
| NAT | Address translation at ASA firewall |
| OSPF on ASA | Dynamic routing integration with firewall |

---

## 7. Device Inventory

| Device Type | Role | Configuration Highlights |
|---|---|---|
| CORE-SW / CORE-SW1 | Layer 3 Core Switches | EtherChannel (LACP), Inter-VLAN routing, OSPF |
| MK-SW | Access Switch | VLAN access ports, STP PortFast, BPDUGuard, VoIP ports |
| Server-SW | Server Farm Switch | VLAN 90 (INSIDE-SERVERS), port isolation |
| Router 4 | WAN/Edge Router | OSPF, HSRP, site-to-site VPN, DHCP relay |
| Cisco ASA Firewall | Perimeter Security | DMZ zones, NAT rules, OSPF, Inspection Policies |
| WLC | Wireless LAN Controller | WLAN management (VLAN 50) |
| IP Phones | VoIP endpoints | VLAN 70, Directory Numbers via CME |

---

## 8. Cybersecurity Threat Enumeration

### 8.1 Security Concepts (X.800 Standard)

| Mechanism | Description |
|---|---|
| Authentication | Verifying the identity of communicating entities |
| Access Control | Limiting access to resources based on roles |
| Confidentiality | Protecting data from unauthorized disclosure |
| Data Integrity | Ensuring data has not been altered |
| Non-repudiation | Preventing denial of sent/received messages |
| Traffic Padding | Inserting random data to prevent traffic analysis |
| Routing Control | Selecting secure physical routes; adapting on breach |
| Notarization | Trusted third-party validation of data properties |
| Security Audit | Logging and verification of security-related events |

### 8.2 Threat Types

| Category | Description |
|---|---|
| Accidental | System failures, bugs, operational errors |
| Intentional – Passive | Surveillance, traffic capture, no system modification |
| Intentional – Active | Data alteration, session hijacking, injection attacks |

### 8.3 Attack Techniques Identified

#### Network Layer Attacks

| Attack | Description |
|---|---|
| IP Spoofing | Forging source IP to hide identity or impersonate a device |
| DNS Spoofing | Returning false IP for domain queries → redirects users |
| DNS Cache Poisoning | Corrupting DNS server cache to affect all downstream users |
| ARP Spoofing | Redirecting traffic at Layer 2 to intercept communications |
| TCP Session Hijacking | Taking over an active TCP session post-authentication |
| Port Scanning | Enumerating open ports to identify vulnerabilities |

#### Application Layer Attacks

| Attack | Description |
|---|---|
| SQL Injection | Injecting SQL code through unvalidated input fields |
| Script Attacks | Exploiting dynamic server-side scripts with malformed input |
| Configuration Exploits | Targeting insecure default configurations |
| Man-in-the-Middle (MitM) | Intercepting traffic between two communicating parties |
| DoS / DDoS | Flooding resources to deny legitimate user access |

#### Wireless-Specific Attacks

| Attack | Description |
|---|---|
| War-Driving | Detecting and cracking WEP-protected wireless networks |
| Social Engineering | Manipulating insiders to reveal credentials or access |

### 8.4 SSH vs Telnet Comparison

| Feature | SSH | Telnet |
|---|---|---|
| Encryption | ✅ Yes (AES, RSA) | ❌ No (plaintext) |
| Authentication | ✅ Public key / password | ⚠️ Password only |
| Port | 22 | 23 |
| Recommended | ✅ Always preferred | ❌ Never in production |

---

## 9. Firewall Zone Enumeration

| Zone | Trust Level | Scope |
|---|---|---|
| Inside (LAN) | High | Internal corporate network |
| DMZ | Medium | Public-facing servers (Web, DNS, Email) |
| Outside | Low | Internet / untrusted networks |

### 9.1 DMZ Topologies Considered

- **Single-Firewall with DMZ**: One ASA separating Inside, DMZ, and Outside — simpler but single point of failure
- **Dual-Firewall with DMZ**: Two ASAs sandwiching the DMZ — higher security, more resilience ✅ *Selected approach*

---

*Next Phase → [Exploitation.md](./Exploitation.md)*
