# Proxmox Troubleshooting Notes

This section captures issues encountered on the hypervisor and their solutions.

## NIC Mapping Confusion
**Issue:** Firewall NICs appeared as ens18 and ens19 but were not immediately clear which was WAN or LAN.  
**Solution:** Used `ip addr` inside the firewall VM to match MAC addresses with Proxmox NIC entries.

## Internal VM Connectivity Failure
**Issue:** Analyst VM received a 192.168.1.x IP and failed to communicate with firewall.  
**Root Cause:** VM was incorrectly attached to vmbr0.  
**Fix:** Reassigned to vmbr1 and configured a static IP.

## Copy/Paste Limitations
**Issue:** NoVNC console loses formatting on multi-line firewall configs.  
**Solution:** Typed nftables rules manually inside the VM.

## Tailscale Connectivity
Tailscale configuration works best after the firewall and analyst VMs have consistent networking.  
Proxmox host should be added after WAN connectivity is stable.

## ISO Upload Issues
Some firewall appliance ISOs were rejected or failed to extract.  
Ubuntu Server ISO is consistently reliable for custom firewall builds.

These troubleshooting notes help guide future rebuilds or expansions.
