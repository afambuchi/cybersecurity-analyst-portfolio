# Post-Installation Checklist – Windows Server (DC01)

This checklist verifies that Windows Server 2022 was installed correctly and is fully prepared for promotion to a Domain Controller. Completing these steps ensures the system is stable, reachable, and configured properly before Active Directory deployment.

---

## 1. Server Identity

- [ ] Rename server to **DC01**
- [ ] Reboot system successfully after rename
- [ ] Confirm hostname using:

hostname

---

## 2. Network Configuration

Configure the server with a static IP on the internal SOC network:

- **IP Address:** 10.0.10.50  
- **Subnet Mask:** 255.255.255.0  
- **Gateway:** 10.0.10.1  
- **DNS (Temporary):** 1.1.1.1  
*(Final DNS will be 10.0.10.50 after promotion)*

Verify connectivity:

- [ ] `ping 10.0.10.1` (firewall)
- [ ] `ping 8.8.8.8` (internet)
- [ ] `ping google.com` (DNS resolution)

---

## 3. System Preparation

- [ ] Install all Windows Updates
- [ ] Enable Remote Desktop (optional but recommended)
- [ ] Verify time synchronization (important for AD)
- [ ] Disable unnecessary network adapters (if any)

---

## 4. Active Directory Preparation

Before adding AD DS:

- [ ] Confirm static IP is set (no DHCP)
- [ ] Confirm DNS is reachable
- [ ] Ensure server can reach the firewall and internet
- [ ] Log into Server Manager with Administrator account

Roles to install next:

- [ ] Active Directory Domain Services (AD DS)
- [ ] DNS Server (installed automatically with AD DS)

---

## 5. Snapshot

Create a Proxmox snapshot labeled **post-install**, so you can revert if needed:

- [ ] `DC01-post-install` snapshot created
- [ ] VM shuts down and boots cleanly after snapshot

---

## 6. Ready for Domain Controller Promotion

After completing the checklist, the server is ready for:

1. Creating the domain **soc.lab**
2. Promoting DC01 to a Domain Controller
3. Configuring domain-integrated DNS
4. Setting up Organizational Units (OUs)
5. Creating user accounts and security groups
6. Joining Windows and Linux endpoints to the domain

---

System is now fully prepared for enterprise-style Active Directory deployment within the SOC lab.

