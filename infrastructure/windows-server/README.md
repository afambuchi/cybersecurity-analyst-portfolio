# Windows Server (DC01) – SOC Home Lab

This directory contains the deployment details for **DC01**, the Windows Server that will serve as the primary Domain Controller, DNS server, and identity provider within the SOC environment.

DC01 provides the foundation for authentication, domain management, security policies, and enterprise-style identity workflows across the lab.

---

## System Overview

- **Hostname:** DC01
- **Operating System:** Windows Server 2022 Standard (Desktop Experience)
- **Role:** Domain Controller (after promotion)
- **Network Location:** Internal SOC VLAN (10.0.10.0/24)
- **Static IP:** 10.0.10.50
- **Gateway:** 10.0.10.1 (Firewall VM)
- **DNS (post-promotion):** 10.0.10.50

---

## Included Files

| File | Description |
|------|-------------|
| `installation-notes.md` | Documented process of installing Windows Server |
| `vm-configuration.md` | VM hardware settings used in Proxmox |
| `post-install-checklist.md` | Verification steps after installation |
| `images/` | Screenshots and visuals from installation (optional) |

---

## Role in the SOC Lab

DC01 supports:

- Active Directory (AD DS)
- Domain-integrated DNS
- Group Policy Objects (GPOs)
- Centralized authentication and access control
- Logging and monitoring for identity-based attacks
- Integration with SIEM, Wazuh, FleetDM, and other SOC tools

AD is a critical component used for incident response training, detection engineering, and SOC workflow demonstrations.

---

## Next Steps

The next phase includes:

1. Promoting DC01 to a Domain Controller  
2. Creating the internal domain: **soc.lab**  
3. Configuring DNS  
4. Provisioning users and organizational units  
5. Joining Windows and Linux hosts to the domain  
6. Enabling event forwarding and advanced logging  

This folder will continue to grow as the environment expands.
