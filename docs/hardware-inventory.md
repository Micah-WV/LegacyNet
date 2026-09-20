# Hardware Inventory & Specifications

This document tracks the physical hardware deployed within the LegacyNet infrastructure, detailing compute platforms, interface controllers, and storage arrays.

## 1. Perimeter Edge Gateway (Firewall)
* **Model:** Fanless Industrial Mini-PC
* **Processor:** Intel Celeron N5105 (4-Core / 4-Thread, up to 2.9GHz, AES-NI hardware crypto enabled)
* **Memory:** 8GB Crucial DDR4-2666 MT/s SODIMM
* **Storage:** 128GB Patriot P300 M.2 PCIe Gen 3 x4 NVMe SSD
* **Network Interfaces:** 4x Intel i226-V 2.5GbE RJ45 Controllers
  * `Port 1`: WAN (Coax Modem / ISP)
  * `Port 2`: LAN (Core 2.5Gbps Switch Trunk)
  * `Port 3`: OPT1 (Isolated Surveillance VLAN / PoE Switch)
  * `Port 4`: Reserved / DMZ / Out-of-Band

## 2. Hypervisor & SIEM Compute Node
* **Motherboard:** ASUS TUF Gaming B650-PLUS WiFi (Onboard Wi-Fi/Bluetooth disabled in UEFI and antennas disconnected)
* **Platform:** AMD Ryzen AM5 architecture
* **Memory:** 32GB (2x16GB) G.SKILL Ripjaws S5 DDR5-6000 CL36
* **Storage Array:**
  * *Boot / OS:* 512GB NVMe SSD (Proxmox VE hypervisor host)
  * *Analytics Pool (Target):* High-endurance 2TB NVMe PCIe 4.0 SSD (SIEM logs, PCAP capture buffer, container volumes)
* **Form Factor:** Open-air thermal management chassis

## 3. Switching & Physical Infrastructure
* **Core Distribution Switch:** Unmanaged 2.5Gbps Multi-Gigabit Switch
* **Surveillance Switch:** Dedicated 1Gbps PoE 802.3af/at Switch
* **Cabling:** Solid-copper Cat6/Cat6a S/FTP horizontal trunk (Garage to Office distribution closet)
* **Wireless Subsystem:** Amazon Eero Mesh nodes (Locked in **Bridge Mode**; strictly functioning as unprivileged Wi-Fi access points)
