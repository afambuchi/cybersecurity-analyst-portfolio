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
