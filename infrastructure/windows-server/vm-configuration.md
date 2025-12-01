# Proxmox VM Configuration – DC01

This file documents the Virtual Machine configuration used for the Windows Server (DC01) inside Proxmox.

---

## VM Hardware Overview

| Component | Configuration |
|----------|---------------|
| CPU | 2–4 cores |
| Memory | 4096–8192 MB |
| Disk | 80 GiB SATA |
| BIOS | UEFI (OVMF) |
| Machine | q35 |
| Network Model | Intel E1000 |
| Bridge | vmbr1 (internal SOC LAN) |
| Display | Default |

---

## Reasoning Behind Configuration Choices

- **SATA disk** avoids the need for VirtIO drivers during installation  
- **Intel E1000 NIC** ensures Windows detects networking immediately  
- **UEFI (OVMF)** enables modern firmware and secure boot configurations  
- **q35 machine type** provides best compatibility with Windows 2022  
- **vmbr1** places the VM behind the custom firewall for segmentation  

---

## Optional: Export VM Config

To record the exact VM configuration, run:

```bash
qm config <VMID>


---

# 📄 4. **post-install-checklist.md**

```markdown
# Post Installation Checklist – DC01

These steps validate that Windows Server is properly installed and ready for promotion to a Domain Controller.

---

## ✔ System Identity

- [ ] Rename server to **DC01**  
- [ ] Reboot successfully  

---

## ✔ Network Configuration

Permanent configuration:

- IP Address: 10.0.10.50  
- Subnet Mask: 255.255.255.0  
- Gateway: 10.0.10.1  
- DNS (after AD): 10.0.10.50  

Test connectivity:

- [ ] ping 10.0.10.1  
- [ ] ping 8.8.8.8  
- [ ] ping google.com  

---

## ✔ Prepare for Active Directory

- [ ] Install Windows Updates  
- [ ] Add role: **Active Directory Domain Services**  
- [ ] Promote server to Domain Controller  
- [ ] Create domain **soc.lab**  
- [ ] Configure domain-integrated DNS  

---

## ✔ Snapshot 

- [ ] Create Proxmox snapshot: `post-install`  

Server is now ready for Domain Services and SOC integration.

---
