# 🛡️ ParkShield — Secure Campus Network Architecture  
**Multi-VLAN, DMZ-First Design with Centralized Services & Defense-in-Depth**

---

## Project Overview

ParkShield is a high-availability campus network architecture designed for a multi-department environment.  
The project modernizes a legacy flat network into a **secure, segmented, and scalable infrastructure** using a **Core–Access layer model**.

The design explicitly governs both **East–West** (internal lateral) and **North–South** (edge and remote) traffic flows, aligning with enterprise and hybrid-network security principles.


--

📚 **Extended Documentation & Artifacts**

- 📄 Full Technical Project Report (PDF)  
- 📊 Architecture Presentation Deck (PDF)  
- 🧪 Validation, testing notes, and design decisions  

👉 See the [Project Wiki](../../wiki)
.

---


## Network Topology

![ParkShield Network Topology](./topology.png)


*High-level logical topology illustrating the Core-Access design, VLAN segmentation, DMZ isolation, and remote access boundary.*

## Security Architecture (Defense in Depth)

Security is designed **into the foundation**, not added as an afterthought.

- **VLAN Isolation**  
  Multiple network segments are used to reduce the internal attack surface and limit lateral movement.

- **DMZ-First Strategy**  
  Critical shared services (DNS/DHCP) are isolated in a dedicated DMZ (VLAN 60) and exposed only through explicitly permitted flows.

- **Layer 2 Hardening**  
  Native VLAN **99 (Black_Hole)** is enforced on all trunk links to mitigate VLAN hopping and native-VLAN mismatch risks.

- **Least-Privilege Access Control**  
  Extended ACLs are applied **inbound on SVIs**, closest to the traffic source, with an explicit default deny policy.

---

## VLAN & Subnet Plan (Core Segments)

| VLAN | Department        | Subnet            | Gateway (SVI) |
|-----:|-------------------|-------------------|---------------|
| 10   | Management        | 192.168.10.0/24   | 192.168.10.1 |
| 30   | Production        | 192.168.30.0/24   | 192.168.30.1 |
| 60   | DMZ (Servers)     | 192.168.60.0/24   | 192.168.60.1 |
| 80   | Remote Access     | 10.10.10.0/24     | 10.10.10.1   |

These VLANs represent the **primary trust boundaries** of the network and are enforced through inter-VLAN routing and least-privilege access policies.

---

## Testing & Validation

The network was validated using a structured functional and security test plan.

### Functional Tests
- Clients in all VLANs successfully obtain IP configuration via DHCP  
- DNS name resolution works from authorized segments  
- Inter-VLAN routing operates only where explicitly permitted  
- DMZ services are reachable only on approved ports  

### Negative / Security Tests
- Unauthorized inter-VLAN communication is blocked  
- Remote access VLAN cannot reach internal management networks  
- Non-permitted services to the DMZ are denied  

### Performance KPI
- **Intra-VLAN latency:** < 1 ms  
- **Inter-VLAN latency:** < 2 ms (campus environment)

All security controls were verified using **pass/fail validation** and deny-by-default enforcement.

---

## Design Intent

ParkShield demonstrates how enterprise networks are designed as **business-critical services**, balancing:

- Security
- Operational resilience
- Scalability
- Governance

Although implemented in Cisco Packet Tracer, the architecture directly translates to **real-world on-prem, hybrid, and cloud networking environments**.

---

## Project Classification

- Enterprise Network Architecture  
- Security-Focused Infrastructure Design  
- On-Prem / Hybrid-Ready Reference Project
