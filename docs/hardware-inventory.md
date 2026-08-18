# LegacyNet: Hardware Inventory

*Status: Planning phase. Not yet installed.*

---

## Current Hardware

| Device            | Manufacturer | Model     | Role                    |
|-------------------|--------------|-----------|-------------------------|
| Modem             | Frontier     | (check)   | ISP entry point         |
| Eero              | Amazon       | (check)   | Wi-Fi access point      |
| UPS               | APC          | (check)   | Power protection        |

## Planned Hardware

| Device | Manufacturer | Model               | Est. Price | Purpose                     |
|--------|--------------|---------------------|------------|-----------------------------|
| Router | Ubiquiti     | EdgeRouter X        | $60-$80    | Firewall / routing / VLANs  |
| Switch | Ubiquiti     | EdgeSwitch 8-PoE    | $100-$150  | Switching, PoE, mirroring   |
| Host 1 | Dell         | OptiPlex 7060 SFF   | $200-$300  | SOC node (Security Onion)   |
| Host 2 | Dell         | OptiPlex 7060 SFF   | $200-$300  | sysadmin-host (Proxmox / VMs / mining)|
| NIC    | Intel        | I350-T2 (2-port)    | $40-$60    | Second NIC for SOC node     |
| SSD    | Samsung/Intel| 500GB-1TB NVMe      | $30-$70    | Logs / storage              |
| Cameras| LongPlus     | 4K PoE kit (4pc)    | $400       | Surveillance                |
| Cabinet| Navepoint    | 8U wall mount       | $80-$120   | Physical organization       |

---

## Notes

- All hardware is being sourced used/refurbished where possible (eBay/Amazon)
- Power draw estimated: ~250W total for full stack
- Will upgrade to solar/battery power in the future
