# LegacyNet

**A home-grown, industrial-grade network and cybersecurity lab.**

Built to learn hands-on skills in networking, security operations, and systems administration while also serving as a foundation for independent practice.

---

## Project Status: Planning / In Progress

Current phase: Hardware research & initial documentation.

---

## Why This Project Matters

This lab demonstrates practical skills in:

- Network design & segmentation (VLANs)
- Firewall & routing (EdgeRouter X)
- Managed switching & port mirroring (EdgeSwitch)
- Power over Ethernet (PoE) camera deployment
- Intrusion detection / SIEM (Security Onion / Wazuh)
- Virtualization (Proxmox)
- Linux administration
- Security documentation & change management

---

## Current Hardware

| Device            | Role                              | Status |
|-------------------|-----------------------------------|--------|
| Frontier Modem    | ISP internet entry point          | Active |
| Eero (bridge)     | Wi-Fi access point (IoT / dirty)  | Active |
| APC UPS           | Power protection for gateway      | Active |

## Planned Hardware

| Device                        | Role                          |
|-------------------------------|-------------------------------|
| EdgeRouter X                  | Router / firewall / VLANs     |
| EdgeSwitch 8-PoE (managed)    | Switching, PoE, port mirroring|
| OptiPlex 7060 SFF (Burgarii)  | Security Onion (IDS / SIEM)   |
| OptiPlex 7060 SFF (ghost)     | Proxmox host / VMs / mining   |
| PoE security cameras (4x)     | Surveillance                  |
| Wall-mount network cabinet    | Physical organization         |

---

## VLAN Scheme

| VLAN | Name        | Purpose                       |
|------|-------------|-------------------------------|
| 10   | Management  | Router, switch, Burgarii mgmt |
| 20   | Servers     | ghost, VMs, NVR               |
| 30   | Surveillance| PoE cameras                   |
| 40   | Dirty / IoT | EERO Wi-Fi (phones, TV)       |

**Security rule:** VLAN 40 cannot reach VLANs 10, 20, or 30.

---

## Planned Architecture Diagram

*(To be added once physical organization is locked, will be drawn on draw.io or Excalidraw)*

---

## Skills Being Developed

- [ ] Routing & subnetting
- [ ] VLAN segmentation
- [ ] Firewall rules & policy
- [ ] Security Onion deployment
- [ ] Suricata / Zeek / Kibana
- [ ] Linux hardening
- [ ] Proxmox virtualization
- [ ] Network documentation & change management

---

## Future Improvements

- Add second site / remote VPN access
- Integrate with solar/battery power infrastructure
- Automate configuration backups
- Set up Wazuh for host-level detection

---

## Lessons Learned

*(To be updated as the project progresses)*
