# Firewall Build Notes

This file documents the reasoning, decisions, and troubleshooting that led to the final firewall configuration.

## Overview

The original plan was to deploy pfSense, OPNsense, or IPFire as the primary firewall.  
Multiple issues occurred during installation:

- pfSense and OPNsense had image extraction and boot compatibility problems on macOS tools
- IPFire froze during setup inside Proxmox
- Several ISO and IMG formats required additional steps that were not reliable in this environment

Given these issues, the decision was made to build a firewall directly on Ubuntu Server.  
This provided full control over networking, routing, NAT, and firewalling through standard Linux tools.

## Interface Layout

The firewall uses two NICs:

- `ens18` – WAN  
  - Attached to `vmbr0` in Proxmox  
  - Receives a 192.168.1.x address from the home router

- `ens19` – LAN  
  - Attached to `vmbr1` in Proxmox  
  - Assigned static 10.0.10.1/24

This creates a clean separation between external and internal networks.

## Routing and IP Forwarding

IP forwarding was enabled via:

sudo nano /etc/sysctl.conf
net.ipv4.ip_forward=1

Then applied with:


## nftables

The firewall uses nftables to control:
- Input filtering  
- Forwarding  
- NAT  
- ICMP access  
- SSH access from the internal network  

Pasting configs in Proxmox caused formatting issues, so the working config was typed manually directly into the VM.

## DHCP

`isc-dhcp-server` was configured to provide addresses in the 10.0.10.0/24 range:

- Gateway: 10.0.10.1  
- DNS: Firewall + public resolvers  
- Pool: 10.0.10.100–200  

## Key Lessons Learned

- Virtual NIC mapping must be validated using MAC addresses inside the VM.
- Internal bridges in Proxmox must be created manually (vmbr1).
- Copy-paste into NoVNC should be avoided for multiline firewall configs.
- Building the firewall by hand provides far greater flexibility and visibility into the network.

This firewall now forms the foundation of the SOC lab and will support all future segmentation and security tooling.
