# Portable SOC Lab Environment

This repository documents the portable SOC lab I am building for demonstrations, advanced practice, and research. The environment is designed to run on a single mini-PC (KAMRUI AK1 Plus with Proxmox) and supports realistic security operations workflows in a compact footprint.

I use this lab to:
- Validate and deepen the topics I teach in cybersecurity courses
- Prototype detection logic and incident response workflows
- Demonstrate modern network segmentation, access control, and monitoring

---

## High-Level Architecture

**Platform**

- Proxmox VE running on a mini-PC (Intel N95, 16 GB RAM)
- Internal and external networks implemented with Proxmox bridges
- Remote access using Tailscale for secure management from any location

**Core Components**

- **Ubuntu Firewall VM**
  - Acts as the primary router and firewall for the lab
  - Two interfaces:
    - `ens18` (WAN) → home network (192.168.1.0/24)
    - `ens19` (LAN) → lab network (10.0.10.0/24)
  - Uses `nftables` for firewalling and NAT
  - Provides DHCP for the 10.0.10.0/24 network

- **Analyst Workstation (Linux)**
  - Lives on the 10.0.10.0/24 network
  - Used for analysis, testing, and management
  - Will also host Python tooling and automation experiments

- **Planned VMs**
  - Windows Server with Active Directory
  - Windows 11 endpoint
  - Wazuh SIEM stack
  - FleetDM for endpoint management
  - Kali Linux for controlled offensive testing

A more detailed architecture and network description is in [`docs/01-architecture.md`](docs/01-architecture.md) and [`docs/02-networking-firewall.md`](docs/02-networking-firewall.md).

---

## Network Design

Current lab networks:

- **Home / WAN:** `192.168.1.0/24`
  - Default gateway provided by the home router
  - Proxmox host and firewall WAN interface live here

- **SOC Lab LAN:** `10.0.10.0/24`
  - Default gateway: `10.0.10.1` (Ubuntu firewall)
  - DHCP range: `10.0.10.100 – 10.0.10.200`
  - Analyst workstation and future SOC components live here

### Architecture Diagram
See the Phase 1 network topology here:
[architecture/phase1-network-diagram.png](architecture/phase1-network-diagram.png)

Planned expansion:
- Additional VLAN-backed subnets for:
  - Domain controllers and core infrastructure
  - Workstations / clients
  - Security tooling (Wazuh, FleetDM, etc.)
  - Red team / testing

---

## Firewall Implementation (Ubuntu + nftables)

The firewall VM replaces traditional firewall appliances and is built to be transparent and customizable.

Key configuration files (sanitized for public sharing):

- [`firewall/nftables.conf`](firewall/nftables.conf)  
  - Defines input, forward, and output chains
  - Enables LAN → WAN forwarding and NAT
  - Restricts direct access to the firewall itself

- [`firewall/netplan-firewall.yaml`](firewall/netplan-firewall.yaml)  
  - Configures:
    - `ens18` with DHCP on the WAN side
    - `ens19` with static `10.0.10.1/24` on LAN

- [`firewall/dhcpd.conf`](firewall/dhcpd.conf)  
  - Implements DHCP for `10.0.10.0/24`

The build process and troubleshooting notes are in [`firewall/notes-firewall-build.md`](firewall/notes-firewall-build.md).

---

## Proxmox Layout

The Proxmox configuration uses:

- `vmbr0` as the external bridge connected to the physical NIC
- `vmbr1` as an internal-only bridge for the SOC LAN

Each VM in the lab is attached to one of these bridges depending on its role. The firewall VM has one NIC on each bridge and routes traffic between them.

More detail can be found in [`docs/03-proxmox-layout.md`](docs/03-proxmox-layout.md).

---

## Lab Usage and Scenarios

As this environment evolves, I will add:

- Detection and investigation scenarios in [`detection-lab/`](detection-lab/)
- Example logs, alerts, and queries based on Wazuh and other tools
- Python-based automation for enrichment, triage, or containment workflows

The intent is for this repository to function both as:
- A professional portfolio of my SOC lab design and implementation, and
- A reference that students and peers can use to build similar environments.

---

## Roadmap

Planned next steps:

- [ ] Finalize Windows Server AD and Windows 11 endpoint
- [ ] Deploy Wazuh and integrate with endpoints
- [ ] Add FleetDM for endpoint visibility
- [ ] Introduce VLAN segmentation for separate security zones
- [ ] Publish example detection and response playbooks
- [ ] Add Python tooling for automation and incident response examples

---

## Notes

All configuration files in this repository are sanitized for public sharing. No real secrets, keys, or confidential data are included. IP addresses and hostnames are either generic or specific to the lab environment only.
