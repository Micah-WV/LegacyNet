# Project Roadmap & TODOs

## Phase 1: Perimeter & Physical Infrastructure (Current Focus)
- [x] Procure and pull horizontal Cat6/Cat6a S/FTP structured cabling (Garage to Office).
- [x] Source and purchase bare-metal firewall appliance (Intel N5105 / 4x 2.5GbE).
- [ ] Assemble firewall internals (Crucial 8GB DDR4 RAM + Patriot 128GB NVMe SSD).
- [ ] Flash and provision bare-metal OPNsense.
- [ ] Configure WAN, LAN, and isolated Surveillance firewall interfaces.
- [ ] Transition Eero mesh infrastructure to transparent Bridge Mode.
- [ ] Hardwire primary workstations directly to the 2.5Gb core switch.

## Phase 2: Compute & Analytics Node
- [ ] Provision Proxmox VE hypervisor on the ASUS TUF B650 AM5 open-air platform.
- [ ] Procure and install secondary high-TBW 2TB NVMe SSD for SIEM indices and VM storage.
- [ ] Deploy local NVR container/VM for isolated IP camera ingestion.

## Phase 3: Advanced Telemetry & Hardening
- [ ] Upgrade core distribution switch to an 802.1Q managed 2.5GbE unit.
- [ ] Configure hardware Port Mirroring (SPAN) for passive packet capture.
- [ ] Deploy Security Onion and tune Suricata IDS rulesets for local network monitoring.
