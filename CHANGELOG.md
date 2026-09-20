# Changelog

All notable changes, architectural pivots, and technical milestones for **LegacyNet** are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to strict versioned documentation of on-premises infrastructure.

---

## [Unreleased]

### Planned
- **Storage Subsystem:** Provisioning of secondary high-TBW 2TB NVMe SSD into ASUS TUF B650 node for VM runtime images and SIEM data pools.
- **Switching Infrastructure:** Transition core switching from unmanaged 2.5Gb switch to an 802.1Q managed switch to support native hardware Port Mirroring (SPAN).
- **Telemetry Engine:** Deployment of Security Onion (Zeek, Suricata, OpenSearch/Kibana) inside Proxmox VE to monitor core network egress.
- **NVR Deployment:** Implementation of an isolated, containerized NVR platform (Frigate/Shinobi) on Proxmox to manage local IP camera recordings.

---

## [0.2.0] - 2026-09-19

### Architectural Pivot & Strategic Refactor
- **Decoupled Hypervisor & Firewall (SPOF Elimination):** Abandoned previous model of virtualizing core routing inside the multi-purpose hypervisor. Implemented a dedicated bare-metal appliance model to ensure household uptime remains 100% resilient during security testing.
- **Demoted Consumer Routing:** Reconfigured Eero mesh hardware from full gateway mode down to transparent Bridge Mode. Stripped all NAT, DHCP, and stateful inspection authority from proprietary Amazon devices; concentrated perimeter control into open-source OPNsense.
- **Physical Boundary Isolation:** Established dedicated physical interface assignment on the firewall for surveillance hardware, eliminating reliance on soft isolation for untrusted IoT/camera devices.
- **Workstation Physical Security:** Severed primary Debian/Windows workstation from wireless infrastructure; migrated to hardwired multi-gigabit interface to eliminate wireless attack surface.
- ### Updated
- Comprehensive project documentation in `/docs/` including hardware inventory, network architecture, project roadmap (`todo.md`), procurement tracking (`budget.md`), and engineering lessons learned (`lessons-learned.md`).


### Added
- **Hardware - Perimeter Gateway:** Fanless Industrial Mini-PC powered by Intel Celeron N5105 (AES-NI hardware crypto support) and 4x Intel i226-V 2.5GbE NICs.
- **Hardware - Gateway Components:** Crucial 8GB DDR4-2666 MT/s SODIMM and Patriot P300 128GB M.2 PCIe Gen 3 x4 NVMe SSD for dedicated OPNsense host.
- **Hardware - Hypervisor Engine:** ASUS TUF Gaming B650-PLUS WiFi bare-metal open-air rack node running 32GB G.SKILL DDR5-6000 memory on the AMD AM5 architecture.
- **Hardware - Surveillance Subsystem:** 1Gbps PoE network switch powering an isolated bank of IP security cameras.
- **Physical Layer Infrastructure:** 4-cable horizontal Cat6/Cat6a S/FTP structured wire bundle pulled between garage staging area and central office distribution closet.

### Removed
- Deprecated dependency on surplus legacy desktop processors lacking dedicated AES-NI crypto acceleration.
- Removed legacy EdgeRouter architecture plans in favor of custom-audited OPNsense deployment.
- Decommissioned consumer Wi-Fi routing, internal DHCP servers, and vendor cloud telemetry interfaces.

---

## [0.1.0] - 2026-07-16

### Added
- Initial conceptual network topology design and repository initialization.
- Early feasibility assessment of legacy enterprise workstation surplus (Dell OptiPlex platforms) for consolidated virtualization.
- Baseline requirements gathering for private Monero (XMR) nodes, personal cloud services, and sovereign data containment.
