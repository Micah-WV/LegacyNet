# Network Architecture & Security Topology

LegacyNet is built on a strict defense-in-depth model, enforcing physical and logical isolation between the perimeter, the internal high-speed core, and untrusted IoT devices.

## Segmentation & Traffic Flow

1. **Perimeter & Routing Plane:**
   * All ingress/egress traffic terminates directly on the bare-metal OPNsense N5105 appliance.
   * Local DNS is resolved upstream via encrypted Unbound DNS over TLS (DoT), preventing middlebox telemetry capture.

2. **Core High-Speed Backbone (LegacyNet LAN):**
   * Connected via 2.5GbE switching.
   * Houses the Proxmox virtualization node, hardwired primary workstations, and local administrative interfaces.
   * Eero wireless access points operate transparently in Bridge Mode, leaving all routing and security inspection to the core firewall.

3. **Surveillance Quarantine Zone:**
   * IP cameras are physically isolated to a dedicated 1Gb PoE switch tied directly to `Port 3` (OPT1) on the firewall.
   * Strict firewall rules (`Camera_Net -> WAN = DROP`) completely sever internet access for camera hardware, preventing external telemetry or command-and-control (C2) callback while permitting local NVR ingestion on the Proxmox node.
