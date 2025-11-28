# Proxmox Network Bridges

This document explains the bridge configuration that creates both the external and internal networks.

## vmbr0 (External Network)
- Connected to: Physical NIC on the mini-PC  
- Network: 192.168.1.0/24 (home LAN)  
- Purpose: Provides WAN access to the firewall  
- Used by: Ubuntu Firewall (ens18), Proxmox host  

vmbr0 behaves like a virtual switch connected directly to your home router.

## vmbr1 (Internal SOC Network)
- No physical connection  
- Network: 10.0.10.0/24 (via firewall)  
- Purpose: SOC lab internal LAN  
- Used by: Firewall LAN interface (ens19), Analyst VM, future SOC VMs  

vmbr1 is isolated until routed and NATed through the firewall.

## Interface Mapping
Matching NICs inside VMs to these bridges required MAC validation:

- VM NIC attached to vmbr0 → becomes `ens18` in firewall  
- VM NIC attached to vmbr1 → becomes `ens19` in firewall  

This mapping is documented because Proxmox NIC order may vary between VMs.
