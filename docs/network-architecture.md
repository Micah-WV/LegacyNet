# LegacyNet: Network Architecture

## Physical Data Flow

```
Coax from wall 
| 
▼ 
Frontier Modem (ISP) 
|
▼ 
EdgeRouter X (WAN) — firewall & routing 
|
▼ 
EdgeSwitch 8-PoE (managed switch) 
|
├── Port 1 → EERO (bridge mode) - Wi-Fi for IoT
├── Port 2 → SOC node (management NIC)
├── Port 3 → SOC node (monitor NIC) - port mirror (SPAN)
├── Port 4 → sysadmin-host (Proxmox host)
├── Port 5 → NVR (if separate)
├── Ports 6-9 → PoE Cameras (surveillance)
└── Ports 10-16 → Future servers
```
---

## Logical Segmentation (VLANs)

| VLAN | Name        | Subnet          | Allows                    |
|------|-------------|-----------------|---------------------------|
| 10   | Management  | 192.168.10.0/24 | VLANs 20, 30 (for admin)  |
| 20   | Servers     | 192.168.20.0/24 | VLAN 10, Internet         |
| 30   | Surveillance| 192.168.30.0/24 | VLAN 20 (NVR), VLAN 10    |
| 40   | Dirty / IoT | 192.168.40.0/24 | Internet only             |

### Firewall Rules (EdgeRouter)

- VLAN 40 **cannot** initiate to VLANs 10, 20, or 30.
- VLAN 30 **can** reach VLAN 20 (NVR) and VLAN 10 (management).
- VLAN 20 **can** reach VLAN 10 and the internet (updates, mining pool).
- VLAN 10 is the most trusted.

---

## Port Mirroring (SPAN)

- **Mirror source:** All ports (1-16) or specific VLANs (10, 20, 30, 40)
- **Mirror destination:** Port 3 → SOC node monitor NIC
- **Why:** SOC node sees all traffic for analysis without being in the data path.

---

## Key Design Decisions

| Decision | Why |
|----------|-----|
| Eero in bridge mode | Prevents double-NAT, enables VLAN control |
| PoE switch for cameras | Single cable per camera (power + data) |
| Security Onion on bare metal | Not competing for resources with other VMs |
| Isolated IoT VLAN | Stops compromised devices from pivoting |

---

## To Be Updated

- [ ] Add final architecture diagram (PNG)
- [ ] Document actual IP assignments
- [ ] Record port mirroring config on EdgeSwitch
