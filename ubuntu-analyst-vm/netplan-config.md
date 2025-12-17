# Netplan Configuration for Analyst VM

The analyst VM uses a static IP address on the internal SOC network (vmbr1).  
This configuration ensures reliable routing, consistent connectivity, and predictable behavior when testing firewall rules.

## Configuration File
Path: `/etc/netplan/01-analyst.yaml`

network:
version: 2
ethernets:
ens18:
dhcp4: no
addresses:
- 10.0.10.20/24
gateway4: 10.0.10.1
nameservers:
addresses:
- 8.8.8.8
- 1.1.1.1

## Key Details
- `ens18` is attached to vmbr1 inside Proxmox.
- Static IP: 10.0.10.20/24  
- Gateway: 10.0.10.1 (Ubuntu firewall)  
- DNS: Public resolvers (can later switch to AD DNS)

## Verification Commands
ip addr show ens18
ip route
ping -c 3 10.0.10.1
ping -c 3 8.8.8.8
ping -c 3 google.com

The VM must reach the firewall first, then external networks through NAT.
