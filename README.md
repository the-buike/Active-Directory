# Home Lab

A self-built home lab modeling enterprise network and identity infrastructure: VLAN-segmented networking, a Proxmox hypervisor running isolated workloads, and a live Active Directory domain. Built as hands-on preparation for Network Engineer and Cloud Engineer roles, alongside CompTIA Network+ and Microsoft AZ-104.

---

## What's in this repo

| Doc | Covers |
|---|---|
| [`Network-infrastructure-kb.md`](https://github.com/the-buike/homelab-lab/blob/main/network-knowledge-base.md) | VLAN design, MikroTik router configuration, switching, the Proxmox host, and remote access |
| [`Active-directory-kb.md`](./active-directory-kb.md) | The Windows Server domain controller build: forest promotion, DNS, OU structure, and verification |
| [`fictional-company-project-kb.md`](./fictional-company-project-kb.md) | Planned expansion: a fictional company network combining public DNS, an internal file server, and AD-based access control |
| [`homelab-config.rsc`](https://github.com/the-buike/homelab-lab/blob/main/configs/homelab-config.rsc) | Exported MikroTik RouterOS configuration, the authoritative source for the router's actual running config |

---

## Quick architecture overview

```
Internet
   |
Xfinity XB8 Gateway
   |
MoCA (coax to Ethernet)
   |
MikroTik hEX Router — VLANs, firewall, DHCP, NAT
   |
TP-Link TL-SG108E Managed Switch
   |
HP EliteDesk Mini running Proxmox VE
   |
   +-- ubuntu-services (VLAN 20) — Docker host
   +-- windows-server-ad / DC01 (VLAN 10) — Active Directory domain controller for homelab.local
```

Full detail on each layer lives in the linked docs above.

---

## Current status

**Complete:**
- VLAN-segmented network with centralized firewall policy on a MikroTik router, configured via CLI
- Proxmox VE hypervisor running multiple isolated VMs
- A live Active Directory forest (`homelab.local`) with DNS, a custom OU structure, a test user, and a security group
- Remote administration via RDP and a Tailscale mesh VPN

**In progress / planned:**
- Domain-joining a Windows client VM and validating end-to-end authentication
- Group Policy Object deployment
- 802.1X network authentication tied to Active Directory via RADIUS/NPS
- Expansion into a fictional company project combining a public domain, an internal file server, and AD-based access control

---

## Why this project exists

Most job postings for Network Engineer and Cloud Engineer roles assume comfort with both networking fundamentals and Windows-based identity infrastructure, even when the rest of a candidate's background leans Linux or cloud-native. This lab was built to close that gap with real, verifiable, hands-on work rather than just exam material, and to serve as a concrete talking point in interviews: not just "I know what a domain controller is," but "here's one I built, here's why I made the decisions I did, and here's how I fixed it when it broke."
