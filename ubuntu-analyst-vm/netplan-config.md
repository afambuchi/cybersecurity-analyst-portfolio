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

# Analyst VM Tooling and Setup

The analyst VM serves multiple purposes:
- Connectivity validation
- Firewall testing
- Packet capture and traffic inspection
- Python-based automation
- SOC scenario development
- Log analysis and future SIEM dashboards

## Base Tools Installed

### Networking and Diagnostics
net-tools
nmap
curl
wget
tcpdump
traceroute


### Python Environment (future)
The VM will host:
- Python 3.x
- Virtual environments
- SOC automation scripts
- API test tools

### Security and Analysis Tools (future)
- Syslog viewer
- Packet capture tools
- Log parsers
- Wazuh agent (Phase 3)

These tools will evolve as the SOC lab expands.

# Connectivity Testing and Validation

This VM is used to test both sides of the firewall:
- Internal LAN communication
- Routed traffic to the external network
- NAT and filtering rules

## Internal Connectivity Tests

### Ping the firewall
ping -c 3 10.0.10.1

### Check ARP resolution
ip neigh

### Check routing table
ip route

## External Connectivity Tests

### Ping external IP
ping -c 3 8.8.8.8

### Test DNS resolution
ping -c 3 google.com

### Check outbound port availability
nc -zv google.com 80
nc -zv google.com 443

## When Tests Fail
- Incorrect Netplan configuration
- DHCP issues on internal network
- Firewall NAT rules not applied
- Wrong bridge assignment inside Proxmox
