# Challenges and Troubleshooting

This section documents the problems encountered during the build and the solutions applied.

## Firewall Installation Issues
**Issue:** pfSense, OPNsense, and IPFire produced installation errors, freezes, or image extraction failures.  
**Root Cause:** Compatibility issues between installer formats and Proxmox’s virtual hardware.  
**Solution:** Replaced appliance-style firewalls with a custom Ubuntu-based firewall to retain full control and reliability.

## Networking Confusion
**Issue:** Analyst VM received a 192.168.1.x address instead of a 10.0.10.x address.  
**Root Cause:** It was attached to `vmbr0` rather than the internal `vmbr1` bridge.  
**Solution:** Created vmbr1, moved the analyst VM to it, and assigned a static internal IP to validate routing.

## nftables Configuration
**Issue:** Copying config into Proxmox console caused syntax errors.  
**Root Cause:** NoVNC console cannot safely handle multiline paste.  
**Solution:** Config was typed manually inside the firewall VM and tested before enabling the nftables service.

## DHCP Failures
**Issue:** Analyst VM showed “Activation of network connection failed.”  
**Root Cause:** Internal LAN had no DHCP server yet.  
**Solution:** Temporarily assigned a static IP, then configured DHCP on the firewall.

These issues reflect normal, real-world challenges in networking and system deployment and reinforce the importance of methodical troubleshooting.
