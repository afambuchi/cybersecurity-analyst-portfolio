# Installation Notes – Windows Server (DC01)

This document outlines the installation and preparation of Windows Server 2022 inside the SOC Home Lab.

---

## 1. VM Creation (Proxmox)

Settings used during VM creation:

- **Name:** DC01
- **OS ISO:** Windows Server 2022
- **BIOS:** UEFI (OVMF)
- **Machine Type:** q35
- **CPU:** 2–4 cores
- **Memory:** 4–8 GB
- **Disk:** 80 GiB (SATA for compatibility)
- **Network Model:** Intel E1000
- **Bridge:** vmbr1 (SOC internal network)

---

## 2. Installation Process

1. Booted from Windows Server ISO  
2. Selected **Windows Server 2022 Standard – Desktop Experience**  
3. Chose SATA disk (no additional drivers required)  
4. Completed installation and initial admin setup  
5. Verified network connectivity:
   - `ping 10.0.10.1` (firewall)
   - `ping 8.8.8.8` (internet)
6. Enabled RDP (optional)

---

## 3. Pre-AD Configuration

Configured a temporary static IP:

- **IP:** 10.0.10.50  
- **Subnet:** 255.255.255.0  
- **Gateway:** 10.0.10.1  
- **DNS:** 1.1.1.1 (temporary, replaced after promotion)

All checks passed and system was prepared for domain controller deployment.

---
