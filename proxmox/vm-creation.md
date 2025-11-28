# VM Creation Process

This file outlines how VMs are created and configured in Proxmox.

## General Steps
1. Upload ISO to `local` storage.
2. Create new VM with:
   - Name based on role (e.g., fw-ubuntu, analyst-ubuntu)
   - UEFI BIOS
   - VirtIO SCSI or SATA disk
   - VirtIO network adapters
3. Attach the VM to the correct bridge (vmbr0 or vmbr1).
4. Configure CPU and RAM allocation:
   - Firewall: 2 cores, 2 GB RAM
   - Analyst VM: 2 cores, 2–4 GB RAM
5. Install OS using uploaded ISO.
6. Apply static IPs or DHCP settings depending on role.
7. Snapshot after successful configuration.

## Bridge Assignment Rules

### Firewall VM
- NIC 1 → vmbr0 (WAN)
- NIC 2 → vmbr1 (LAN)

### Analyst VM
- NIC 1 → vmbr1 (LAN)

### Future Windows / SIEM / FleetDM VMs
- NIC 1 → vmbr1 (LAN)

## Storage
VM disks are stored in `local-lvm` for performance and snapshot support.
