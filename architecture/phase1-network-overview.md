# Phase 1 SOC Lab Architecture  
## Overview

Phase 1 of the SOC lab focuses on creating a stable and functional core network that supports routing, segmentation, endpoint connectivity, and future expansion into SIEM and monitoring tools.

This phase includes:
- Proxmox as the virtualization platform
- A custom Ubuntu-based firewall
- A dedicated internal LAN network
- A Linux analyst workstation connected to the internal network

This architecture serves as the foundation for future SOC components such as Windows Server, Windows endpoints, Wazuh, FleetDM, and Kali Linux.

---

## Proxmox Host Layout

The mini-PC runs Proxmox VE with two virtual bridges:

- `vmbr0`  
  The external bridge connected to the physical NIC on the mini PC.  
  This provides access to the home network (192.168.1.0/24) and the internet.

- `vmbr1`  
  An internal-only virtual bridge created for the SOC LAN.  
  This network does not connect to the physical host and is isolated within Proxmox.

---

## Firewall VM (Ubuntu)

The firewall VM routes and filters traffic between the external home network and the internal SOC lab.

- **ens18 (WAN)**  
  Bridge: vmbr0  
  Address: via DHCP from home router (192.168.1.x)

- **ens19 (LAN)**  
  Bridge: vmbr1  
  Address: 10.0.10.1/24 (static)

The firewall uses:
- IP forwarding (enabled in `/etc/sysctl.conf`)
- nftables for firewall rules and NAT
- isc-dhcp-server to provide DHCP for the internal network

This replaces pfSense/OPNsense due to compatibility issues encountered during installation and allows for full control and customization.

---

## Analyst Workstation (Ubuntu)

The analyst VM is attached directly to the SOC LAN:

- Interface: ens18
- Bridge: vmbr1
- Static IP: 10.0.10.20/24
- Gateway: 10.0.10.1 (firewall)
- DNS: 8.8.8.8, 1.1.1.1

This VM is used for:
- Connectivity validation  
- Packet inspection and testing  
- Python development  
- SOC tooling and future investigations  

---

## Network Flow

Home Router
|
| (physical NIC on mini-PC)
v
Proxmox Host
|
vmbr0 <—> Firewall ens18 (WAN)
|
vmbr1 <—> Firewall ens19 (LAN)
|
+—> Analyst VM

---

## Goals for Phase 2

Future architecture expansions will include:
- VLAN-based segmentation
- Active Directory subnet
- Endpoint subnet
- Security tools subnet (Wazuh, FleetDM)
- Optional DMZ or honeynet segment
- Logging and monitoring pipeline

These additions will build on the stable foundation created in Phase 1.

