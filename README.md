# Proxmox-Based SOC Lab (Active Build)

This repository documents the design, teardown, and rebuild of a Proxmox-based SOC lab focused on Active Directory, Linux domain integration, and security operations fundamentals.

This lab is intentionally documented end-to-end, including architectural decisions, misconfigurations, resets, and rebuilds. The goal is to reflect real-world SOC and infrastructure work rather than a “perfect” lab environment.

---

## Lab Overview

This SOC lab is built to simulate an enterprise-style environment with:

- Active Directory Domain Services
- Linux systems joined to Active Directory
- Centralized DNS and identity management
- Secure network segmentation
- Analyst workstation workflows

The lab is designed for hands-on learning, troubleshooting, and SOC analyst skill development.

---

## Reset and Rebuild Decision

During the initial build, multiple layered networking and DNS issues were encountered across virtual machines. Rather than continuing to patch a fragile environment, the decision was made to fully wipe all VMs and rebuild the lab cleanly.

This reset allowed for:

- Proper install order
- Clean DNS and AD configuration
- Correct network design from the start
- Stronger documentation and repeatability

This reflects a real-world skill: knowing when to stop, reset, and rebuild correctly.

---

## Current Architecture (Post-Rebuild)

**Infrastructure**
- Hypervisor: Proxmox
- Network Range: 10.0.10.0/24

**Virtual Machines**
- DC01 (Windows Server)
  - Active Directory Domain Services
  - DNS
  - Domain: soc.local
- Analyst01 (Ubuntu Linux)
  - Joined to Active Directory
  - SSSD + Kerberos authentication
  - Domain user login enabled

---

## Completed Milestones

- Windows Server installed and promoted to Domain Controller
- DNS configured and validated
- Linux analyst VM successfully joined to Active Directory
- Domain user authentication verified on Linux
- DNS resolution confirmed between systems

---

## In Progress

- Time synchronization with domain controller
- Additional Linux hardening
- Logging and monitoring planning
- SOC tooling integration

---

## Lessons Learned

- DNS must be correct before anything else will work
- Install order matters more than expected
- Restarting clean is often faster than troubleshooting deeply broken state
- Documentation during failure is just as valuable as documentation during success

---

## Roadmap

- Additional Linux clients
- Windows workstation
- Centralized logging
- Detection and alerting workflows
- SOC-style investigation scenarios

---

## Documentation

Detailed notes and configuration steps will continue to be added as the lab evolves.

This repository is a living project.
  