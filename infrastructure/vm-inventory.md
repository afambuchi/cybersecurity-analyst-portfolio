# Virtual Machine Inventory

This file lists all active and planned virtual machines in the SOC lab, their roles, and their network assignments.

## Active Virtual Machines

### 1. Ubuntu Firewall VM
- **Role:** Primary router and firewall for SOC
- **Bridges:** 
  - ens18 → vmbr0 (WAN)
  - ens19 → vmbr1 (LAN)
- **IP Addresses:**
  - WAN: DHCP from home network (192.168.1.x)
  - LAN: 10.0.10.1/24
- **Notes:** Provides DHCP and NAT for internal network

### 2. Ubuntu Analyst VM
- **Role:** Analyst workstation for testing, validation, and SOC tooling
- **Bridge:** vmbr1
- **IP Address:** 10.0.10.20/24 (static)
- **Notes:** Will later include Python tools, packet captures, and SIEM dashboards

---

## Planned Virtual Machines (Phase 2+)

### 3. Windows Server (Active Directory)
- **Role:** Domain controller, DNS, Group Policy
- **Network:** vmbr1 (10.0.10.0/24)
- **Planned IP:** 10.0.10.5

### 4. Windows 11 Endpoint
- **Role:** Domain-joined workstation for endpoint logging and testing
- **Network:** vmbr1
- **Planned IP:** DHCP from firewall

### 5. Wazuh SIEM Server
- **Role:** Log collection, analysis, alerting
- **Network:** vmbr1
- **Planned IP:** 10.0.10.50

### 6. FleetDM Server
- **Role:** Endpoint visibility and management
- **Network:** vmbr1
- **Planned IP:** 10.0.10.60

### 7. Kali Linux
- **Role:** Offensive security testing
- **Network:** vmbr1
- **Planned IP:** DHCP or static

These VMs will be added as the SOC expands.
