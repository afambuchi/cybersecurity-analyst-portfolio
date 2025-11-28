# Proxmox Configuration Overview

This document provides an overview of the key Proxmox settings and layout used to support the SOC lab.

## Hardware Platform
- Mini-PC: KAMRUI AK1 Plus
- CPU: Intel N95
- RAM: 16 GB
- Boot Drive: 512 GB SSD
- Additional Storage: Optional external SSDs

Proxmox takes full control of the system, replacing Windows.

## Proxmox Version
Proxmox VE 8.x (latest stable at time of installation).

## Network Interfaces
Proxmox uses one physical NIC on the mini-PC.  
Two network bridges were created:

- `vmbr0` (default):  
  - Connected to physical NIC  
  - Provides access to home network and internet  
  - Used by firewall WAN interface  

- `vmbr1` (internal):  
  - Virtual-only network  
  - No physical uplink  
  - Used by internal SOC lab VMs  
  - Routed to the internet only through the Ubuntu firewall VM

## Storage Layout
- `local` — ISO images and templates  
- `local-lvm` — VM disks  
- No external storage attached yet  

This layout will support future snapshots, backups, and disk expansion.
