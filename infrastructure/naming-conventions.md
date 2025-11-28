# Naming Conventions

Consistent naming ensures clarity across VMs, configuration files, diagrams, and documentation.

## Host Naming

| System             | Proposed Hostname     |
|--------------------|------------------------|
| Proxmox host       | proxmox-node           |
| Firewall VM        | fw-ubuntu              |
| Analyst VM         | analyst-ubuntu         |
| AD Server          | ad-server              |
| Windows Client     | win11-client           |
| Wazuh Server       | wazuh-manager          |
| FleetDM Server     | fleet-server           |
| Kali               | kali-lab               |

## Directory Naming
Use lowercase with hyphens, no spaces:
firewall/
ubuntu-analyst-vm/
proxmox/
infrastructure/
architecture/
docs/

## File Naming
For configs, use hyphens and descriptive names:

nftables.conf
netplan-firewall.yaml
dhcpd.conf
01-build-log.md

This keeps the repo structured, readable, and scalable.
