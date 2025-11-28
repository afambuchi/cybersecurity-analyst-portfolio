# Ubuntu Firewall VM

This folder contains the configuration files and build notes for the custom Ubuntu-based firewall used in the SOC lab.  
The firewall acts as the router, NAT device, and access control point between the external home network and the internal SOC network.

The decision to use Ubuntu instead of pfSense or OPNsense was based on installation issues and the need for full transparency and customization.  
This approach gives complete control over routing, firewall rules, and logging.

Contents:
- `nftables.conf` – Layer 3 and 4 filtering rules and NAT configuration
- `netplan-firewall.yaml` – Network interface configuration for LAN and WAN
- `dhcpd.conf` – DHCP configuration for the 10.0.10.0/24 network
- `notes-firewall-build.md` – Build log, reasoning, and troubleshooting notes
