# LegacyNet: Lessons Learned

*This file is a living document. Updated after every milestone, mistake, and "aha!" moment.*

---

## 2026-08-17 (Planning Phase)

**Lesson 1:** Documentation comes first.
> Even before I bought hardware, writing down the network architecture and VLAN scheme forced me to think through the design. This saved me from buying the wrong equipment.

**Lesson 2:** The Eero will be demoted to bridge mode.
> I learned that consumer mesh routers like Eero are great for Wi-Fi coverage, but terrible for network segmentation. The EdgeRouter + managed switch hand back control.

**Lesson 3:** One spool of Cat6 does it all.
> Same cable carries data AND power (PoE). No need for separate runs. Just need a PoE-enabled switch.

**Lesson 4:** Keep it simple at first.
> For the first project, install Security Onion on bare metal instead of virtualizing with Proxmox. One less layer of complexity while learning.

---

## Next Update: After hardware arrives

- [ ] Record actual installation experience
- [ ] Note any mistakes during cabling
- [ ] Document VLAN configuration issues (if any)
