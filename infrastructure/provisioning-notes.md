# Provisioning Notes

These notes cover how VMs are provisioned, configured, and connected in Proxmox.

## VM Creation Process
1. Create a new VM in Proxmox.
2. Attach the VM to the appropriate bridge:
   - `vmbr0` for WAN or Proxmox-facing systems
   - `vmbr1` for internal SOC systems
3. Allocate CPU and RAM based on role:
   - Firewall: 2 cores, 2 GB RAM
   - Analyst VM: 2 cores, 2–4 GB RAM
   - Future Windows systems: 2–4 cores, 4–8 GB RAM

## Storage Layout
- Proxmox host uses internal SSD
- SOC VMs stored on local-lvm
- ISOs stored in `local` storage

## Networking Configuration
- Proxmox requires the firewall VM to be operational before internal VMs gain outbound access.
- NIC order and MAC matching must be validated inside the VM.
- vmbr1 is isolated until routed through the firewall.

## Observations and Lessons Learned
- Ubuntu firewall provides unmatched control and transparency compared to appliance firewalls.
- Proxmox’s internal bridges make segmentation straightforward.
- Creating a clean network plan early avoids reconfiguration later.
- Typing firewall configs manually inside the VM avoids formatting errors from copy-paste.
