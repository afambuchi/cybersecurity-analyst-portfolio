# Build Log

This file captures the sequence of major steps and decisions made while constructing the SOC lab.

## Hardware and Platform Setup
- Selected a KAMRUI AK1 Plus mini-PC for portability and low power usage.
- Installed Proxmox VE as the hypervisor.
- Removed the factory Windows installation to dedicate the system fully to virtualization.
- Created two Proxmox network bridges:
  - `vmbr0` for external (home network)
  - `vmbr1` for internal SOC networking

## Firewall Deployment
- Attempted multiple firewall platforms (pfSense, OPNsense, IPFire).
- Encountered issues including image compatibility, installer lockups, and performance instability.
- Pivoted to building a custom firewall using Ubuntu Server.
- Configured:
  - `ens18` as WAN (DHCP from home router)
  - `ens19` as LAN (10.0.10.1/24)
  - Persistent IP forwarding
  - nftables for filtering and NAT
  - DHCP service for the internal network

## Analyst Workstation
- Reconfigured the analyst VM to use `vmbr1` after validating LAN isolation.
- Assigned a static IP (10.0.10.20/24) for initial connectivity testing.
- Validated routing to the firewall and external network through NAT.

## Current State
- Core networking is functional.
- Internal LAN traffic flows through the firewall.
- Analyst VM can test, inspect, and administer the environment.
- Ready for Phase 2: Windows infrastructure and SIEM deployment.
 