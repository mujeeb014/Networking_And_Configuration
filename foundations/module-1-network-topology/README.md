# Module 1 — Network Topology Portfolio

## 🧠 Objective

Design a basic network topology demonstrating understanding of the **Core, Distribution, and Access layers** using Cisco Packet Tracer.

## 📄 Files in this folder

- `M1_Topology_Labeled_Portfolio.pkt` — Packet Tracer file of the complete topology
- `screenshots/` — Topology diagram, device labels, and command output
- This file — full description of design, device roles, and configuration status

## ⚙️ Tools used

- Cisco Packet Tracer v8.x
- Markdown for documentation

## 🏗️ Topology overview

The network is organized into the three-layer hierarchical model:

- **Core layer** — `R1_Core` (1x router). Routes and manages traffic between the two distribution-layer networks. Connects to `S1_Dist` via `G0/0` and to `S2_Dist` via `G0/1`.
- **Distribution layer** — `S1_Dist` and `S2_Dist` (2x switches). Aggregate their respective access-layer segments and sit between the access layer and the core, enforcing network policy and providing the boundary between the two halves of the network.
- **Access layer** — Two access-layer segments, one under each distribution switch:
  - **Under `S1_Dist`:** PC0, PC1, PC2 (wired, F0/1–F0/3), Access Point0 + Laptop0 (wireless, F0/4)
  - **Under `S2_Dist`:** PC3, PC4, PC5 (wired, F0/1–F0/3), Access Point1 + Laptop1 (wireless, F0/4)

This gives a symmetric two-branch topology: each branch has its own distribution switch and access-layer segment, both converging on the single core router.

## 🔢 IP addressing & device configuration status

This module focused on **physical and logical topology design** — placing devices, assigning them to the correct hierarchical layer, and cabling them correctly — rather than IP addressing or device configuration.
No interfaces have IP addressing configured yet, and all are administratively down. IP addressing, VLAN segmentation, and interface activation (`no shutdown`) are planned for the next module, where the addressing scheme and device hardening will be added on top of this topology.

## ⚙️ Configuration steps completed in this module

1. Placed and labeled devices by hierarchical role: `R1_Core` (Core), `S1_Dist` / `S2_Dist` (Distribution), end devices (Access)
2. Cabled the core router to both distribution switches (`G0/0` → `S1_Dist`, `G0/1` → `S2_Dist`)
3. Cabled each distribution switch to its access-layer segment (PCs, laptops, and a wireless access point per branch)
4. Verified interface status via `show ip interface` to confirm baseline state before configuration begins

**Not yet done (planned for next module):** hostname/banner configuration, enable secret and line passwords, interface IP assignment + `no shutdown`, VLAN creation, and verification via `show ip interface brief` / `show vlan brief`.

## 🔍 Summary — what this demonstrates

This topology demonstrates the ability to:
- Categorize devices into Core, Distribution, and Access layers and explain *why* each device sits where it does
- Design a symmetric, scalable topology where each access-layer segment funnels up through its own distribution switch to a shared core
- Build and verify physical/logical connectivity using Packet Tracer before any addressing or hardening is applied — i.e., get the skeleton right before adding configuration on top

## 🎯 Attacker/defender notes

Even at this early, unconfigured stage, the topology itself raises real security questions worth thinking through:

- **Right now, every device is wide open.** `R1_Core`'s interfaces have no IP addressing and Internet protocol processing is disabled — there's no enable secret, no line passwords, nothing configured. In a real deployment, this is the exact window (between physical install and hardening) where a device is most vulnerable if anyone gets local/console access.
- **Symmetric design = symmetric risk.** Because `S1_Dist` and `S2_Dist` are mirror images of each other, whatever misconfiguration or vulnerability exists on one branch likely exists on the other too — a pentester (or attacker) who compromises one access-layer segment should be assumed to have a roadmap to the other.
- **Two branches converging on one Core is a single point of failure *and* a single point of control.** From a defensive view, this is good — all inter-branch traffic must pass through `R1_Core`, making it the natural place for ACLs, logging, and monitoring once configuration begins. From an attacker's view, it's the highest-value target in the whole topology.
- **Next module's job (IP + hardening) is where real attack surface appears.** Once VLANs, IPs, and passwords are added, this becomes a meaningfully analyzable target — default credentials, unencrypted management access (Telnet vs SSH), and VLAN misconfiguration will all become relevant questions to revisit then.

## 📚 Author

**Mujeeb Ur Rahman**