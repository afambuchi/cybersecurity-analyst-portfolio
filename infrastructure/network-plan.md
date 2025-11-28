# Network Plan

This document describes the network layout used in the SOC lab and the reasoning behind its design.

## External Network (Home LAN)
- **Subnet:** 192.168.1.0/24
- **Purpose:** Provides WAN access for Proxmox and the firewall
- **Gateway:** Home router
- **Proxmox Bridge:** vmbr0
- **DHCP:** Provided by home router

## Internal SOC Network
- **Subnet:** 10.0.10.0/24
- **Purpose:** Main lab subnet for all SOC components
- **Gateway:** 10.0.10.1 (Ubuntu firewall)
- **Proxmox Bridge:** vmbr1
- **DHCP:** Provided by the firewall
- **DNS:** 10.0.10.1 internally, with fallback to public resolvers

### Current IP Assignments
| Device                 | IP Address     | Role                      |
|------------------------|----------------|---------------------------|
| Firewall (LAN)         | 10.0.10.1      | Gateway, NAT, DHCP        |
| Analyst VM             | 10.0.10.20     | Testing & analysis        |
| Future AD Server       | 10.0.10.5      | Domain controller         |
| Future Wazuh Server    | 10.0.10.50     | SIEM                      |
| Future FleetDM Server  | 10.0.10.60     | Endpoint management       |

---

## Future Network Segmentation

The current single-LAN structure will expand into multiple VLANs during Phase 3–4:

- **Infrastructure VLAN** — Domain controllers, core services  
- **Workstation VLAN** — Windows endpoints  
- **Security Tools VLAN** — Wazuh, FleetDM, log pipeline  
- **DMZ VLAN** — Controlled external-facing services (optional)  
- **Attack VLAN** — Kali and red-team tools  

These segments will eventually be routed through the Ubuntu firewall using additional virtual NICs or VLAN tagging.
