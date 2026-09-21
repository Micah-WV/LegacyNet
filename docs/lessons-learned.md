# Engineering Lessons Learned & Architectural Pivots

This document records key decisions, trade-offs, and design pivots made during the evolution of LegacyNet, serving as an engineering reference for risk management and system design.

## 1. Decoupling Perimeter Routing from the Virtualization Hypervisor
* **Initial Concept:** Early designs evaluated an all-in-one virtualized architecture; running OPNsense as a VM inside a Proxmox hypervisor alongside heavy analytics tools like Security Onion.
* **The Failure Mode Identified:** In a single-node setup, any hypervisor kernel update, storage bottleneck from log indexing, or experimental configuration error immediately takes down core family internet access (violation of operational resilience and the "Wife Acceptance Factor").
* **The Pivot:** We shifted to a dedicated bare-metal edge firewall (Intel N5105 mini-PC) for zero-downtime perimeter control, leaving the heavy compute node (ASUS TUF AM5 platform) entirely free for hypervisor experimentation, SIEM testing, and containerized workloads.

## 2. Navigating Silicon Pricing & Component Sourcing
* **The Challenge:** Rapidly shifting component markets (driven by enterprise AI data center demand) created severe price distortions for standalone RAM and NVMe drives, making individual barebones component sourcing financially inefficient for certain tiers.
* **The Solution:** We deliberately targeted DDR4-based industrial mini-PCs rather than cutting-edge DDR5 platforms for the firewall tier. This allowed us to leverage mature, lower-cost memory standards specifically for routing duties while reserving expensive DDR5 investments strictly for the high-performance compute node where memory bandwidth is genuinely required.

## 3. Hardware Supply-Chain Realism
* **Threat Modeling:** Rather than chasing impossible hardware purity against opaque global silicon fabrication, the architecture embraces a zero-trust boundary model. We assume consumer endpoints and standard processors contain complex management engines.
* **Mitigation:** Control is enforced entirely at the software and network layers via strict default-deny egress rules, hardware-isolated surveillance VLANs, and encrypted DNS transport; ensuring that even if underlying hardware attempts telemetry, it is comprehensively blocked at the perimeter.

## 4. UEFI Bootstrapping & Firmware Quirks (ASUS Platforms)
* **The Challenge:** Modern ASUS UEFI firmware exhibits strict validation hurdles when booting custom hypervisor media, frequently failing silently or throwing parsing errors.
* **Key Discoveries & Mitigations:**
  * **Secure Boot:** Standard disable toggles are insufficient on certain UEFI versions. Clearing all Secure Boot keys (PK, KEK, DB, DBX to "no keys") and disabling Fast Boot are mandatory to allow unsigned or hybrid bootloaders to execute.
  * **Flashing Tool Selection:** BalenaEtcher and Ventoy can encounter parsing bottlenecks or "invalid magic number / need to load the kernel first" errors with ISOHybrid Debian/Proxmox structures. **Rufus in DD image mode** provides a reliable raw block-level write once firmware security restrictions are neutralized.
  * **Architecture Validation:** Always verify target hardware architecture (`x86_64` vs. `arm64`) prior to flashing to prevent fundamental instruction-set mismatches.

## 5. Air-Gapped Deployment Under Zero-Trust
* **The Threat Model:** When operating under the assumption that an existing legacy home network is potentially compromised by external adversaries, connecting unhardened infrastructure introduces unnecessary risk.
* **The Strategy:** 
  * Execute hypervisor and operating system installations **completely air-gapped** using local physical media, a dedicated monitor, and a keyboard.
  * Utilize placeholder static configurations (e.g., isolated subnet allocations) to satisfy installer requirements without touching external networks.
  * Defer network integration until the sovereign edge firewall (LegacyNet perimeter) is physically installed, configured, and verified.
