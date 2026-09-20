# LegacyNet 🛡️
**Hardened On-Premises Network Infrastructure, Threat-Informed Perimeter, and Security Operations Lab**

[![Status: Active Development](https://img.shields.io/badge/Status-Active%20Deployment-success?style=flat-square)]()
[![Platform: Proxmox VE](https://img.shields.io/badge/Virtualization-Proxmox%20VE-orange?style=flat-square)]()
[![Firewall: OPNsense](https://img.shields.io/badge/Perimeter-OPNsense%20(Bare%20Metal)-blue?style=flat-square)]()
[![Telemetry: Security Onion Target](https://img.shields.io/badge/SIEM-Security%20Onion-red?style=flat-square)]()

---

## Executive Summary & Operational Philosophy

LegacyNet is an on-premises, defense-in-depth network security architecture engineered from bare metal to provide enterprise-grade access control, micro-segmentation, and passive threat detection. 

Rather than relying on closed-source, vendor-managed consumer appliances, this environment implements a verified **Zero-Trust Network Architecture (ZTNA)**. It is constructed to address real-world threat models: supply chain interdiction, untrusted IoT firmware, pervasive surveillance telemetry, and unauthorized egress. The network maintains high-availability operational standards—ensuring that hypervisor experimentation, packet capture, and security analytics remain completely non-disruptive to baseline household production services.

---

## Technical Competencies Demonstrated

* **Perimeter Defense & Routing:** Stateful inspection, L4/L7 policy construction, dynamic routing, NAT, and strict default-deny egress filtering.
* **Network Segmentation & Quarantine:** Layer 2/3 physical boundary isolation targeting untrusted IP camera telemetry and rogue local devices.
* **Security Operations & Telemetry:** Log aggregation, continuous monitoring pipelines, full-packet capture (PCAP), and intrusion detection using Suricata and Security Onion.
* **Systems Hardening & Infrastructure:** Linux systems administration (Debian), bare-metal hypervisor operations (Proxmox VE), physical structured cabling, and hardware supply-chain validation.

---

## System Components & Engineering Specifications

### 1. Perimeter Appliance (Edge Security Gateway)
* **Chassis / Compute:** Fanless Industrial Mini-PC (Aluminum heatsink chassis, passive cooling)
* **Processor:** Intel Celeron N5105 (4-Core / 4-Thread, up to 2.9GHz)
  * *Cryptographic Engine:* Hardware-accelerated AES-NI instruction set enabled for encrypted transport.
* **Memory:** 8GB Crucial DDR4-2666 MT/s SODIMM
* **Storage:** 128GB Patriot P300 M.2 PCIe Gen 3 x4 NVMe SSD
* **Physical Interfaces:** 4x Intel i226-V 2.5GbE RJ45 Controllers (Dedicated WAN, Core LAN, Isolated Surveillance, Out-of-Band/DMZ)
* **Platform:** OPNsense (Bare Metal, non-virtualized for maximum uptime and tamper isolation)

### 2. Hypervisor & Threat Analytics Host (Compute Node)
* **Motherboard:** ASUS TUF Gaming B650-PLUS WiFi
  * *Hardening Measure:* Onboard 802.11/Bluetooth silicon logically disabled in UEFI and physically disconnected from antennas to eliminate unmonitored wireless ingress/out-of-band management vulnerabilities.
* **Processor Platform:** AMD Ryzen AM5 architecture
* **System Memory:** 32GB (2x16GB) G.SKILL Ripjaws S5 DDR5-6000 CL36 (Optimized for heavy log-indexing and in-memory analytics)
* **Storage Array:**
  * *Boot/OS:* 512GB NVMe SSD (Proxmox VE root environment)
  * *Analytics Volume (Target):* High-endurance 2TB NVMe PCIe 4.0 (Dedicated high-write partitions for SIEM indices, PCAP pools, and container images)
* **Form Factor:** Open-air thermal management configuration
* **Platform:** Proxmox VE (Debian-based hypervisor engine)
* **Target Services:** Security Onion (Elasticsearch/Logstash/Kibana/Zeek/Suricata), local NVR ingestion, secure administrative bastion hosts.

### 3. Distribution, Switching, and Physical Layer
* **Core Distribution Switch:** Unmanaged 2.5Gbps multi-gigabit switch (Direct high-speed trunk between workstation, hypervisor, and firewall).
* **Surveillance Switch:** Dedicated 1Gbps PoE 802.3af/at switch.
* **Structured Cabling:** 4-cable horizontal bundle of solid-copper Cat6/Cat6a S/FTP (Shielded/Foiled Twisted Pair) pulled directly from garage staging through wall cavities into the central distribution closet, terminated into shielded keystones.
* **Wireless Subsystem:** Amazon Eero Mesh infrastructure locked to **Bridge Mode**. Stripped of DHCP, routing, NAT, and gateway services; functioning strictly as dumb wireless access points for unprivileged mobile devices.

---

## Defensive Engineering & Threat Mitigation Rules

### 1. Hardened Surveillance Micro-Segmentation
Unbranded and embedded IP camera platforms are assumed to contain unpatched CVEs, hardcoded vendor credentials, and untrusted cloud telemetry.
* **Physical Isolation:** Cameras communicate only via the 1Gb PoE switch connected directly to physical interface `Port 3` (OPT1) on the firewall.
* **Policy Hardening:** An explicit firewall rule blocks all traffic from `Surveillance_Subnet` destined to `WAN`.
* **Least Privilege Access:** Camera streams can only be accessed by the internal NVR server; the cameras cannot ping outside their immediate broadcast domain, resolving the threat of remote command-and-control (C2) or exfiltration.

### 2. Operational Separation of Concerns
To resolve the common homelab failure mode—where core family routing collapses during virtualization development:
* The firewall is deployed on bare-metal hardware completely detached from the virtualization hypervisor.
* Hypervisor kernel updates, container experimentation, and high-resource SIEM indexing jobs can be executed, restarted, or crashed on the Proxmox host without causing packet loss or network degradation across production systems.

### 3. Egress Hardening & DNS Privacy
* By default, internal hosts are prohibited from establishing arbitrary outbound sessions over unvetted ports.
* Local DNS resolution is captured and resolved locally through OPNsense Unbound DNS over TLS (DoT) upstream, neutralizing standard ISP cleartext logging, poisoning vectors, and middlebox snooping.

---

## Strategic Roadmap

- [x] Pull and terminate 4-run Cat6/Cat6a horizontal structured cabling from garage to core distribution point.
- [x] Procure multi-NIC Intel i226-V bare-metal appliance for dedicated firewall routing.
- [ ] Assemble firewall internals (8GB DDR4 / 128GB NVMe) and provision OPNsense.
- [ ] Configure core routing interfaces, VLAN segment definitions, and egress policies.
- [ ] Transition consumer mesh Wi-Fi to transparent Bridge Mode.
- [ ] Deploy and harden Proxmox VE hypervisor on the ASUS TUF AM5 compute platform.
- [ ] Install secondary high-TBW 2TB NVMe SSD for dedicated telemetry storage pools.
- [ ] Deploy an 802.1Q managed switch with dedicated Port Mirroring (SPAN) to send bidirectional traffic copies to the Proxmox analytics interface.
- [ ] Deploy Security Onion and tune Suricata IDS rulesets for local network monitoring.
