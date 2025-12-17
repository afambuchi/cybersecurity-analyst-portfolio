# Changelog

All notable changes to this project are documented in this file.

This project follows an iterative lab-build approach. Entries reflect architectural decisions, rebuilds, and lessons learned as the environment evolved.

---

## [2.2.0] – Lab Reset and Firewall Rebuild

### Added
- pfSense CE 2.8.1 successfully installed and configured in Proxmox
- WAN/LAN interface assignment and LAN gateway configuration
- HTTPS WebConfigurator enabled and verified

### Changed
- Lab architecture rebuilt from a clean Proxmox environment
- Firewall approach changed from custom Ubuntu firewall to pfSense
- VM build order restructured to prioritize DNS and AD stability

### Lessons Learned
- Firewall placement and DNS order are critical in SOC environments
- Incremental verification prevents cascading failures

---

## [Phase 2] Reset and Structured Rebuild 12/2025

### Added
- Reset and rebuild decision documentation
- Clean rebuild strategy with defined order of operations
- Updated documentation structure to reflect intentional phases
- Improved clarity around DNS, Active Directory, and Linux integration

### Changed
- Rebuilt all virtual machines from a clean state
- Enforced static IP and DNS configuration before AD deployment
- Adjusted Linux DNS handling to rely exclusively on domain DNS
- Improved validation steps between infrastructure phases

### Fixed
- DNS resolution failures between Linux and Windows systems
- Active Directory authentication issues on Linux clients
- Domain join failures caused by misordered configuration steps
- Hidden configuration drift introduced during early experimentation

---

## [Phase 1] Initial Build and Exploration 11/2025

### Added
- Proxmox host configuration and networking setup
- Initial network diagrams and architecture planning
- Windows Server installation and Active Directory deployment
- Linux analyst workstation build
- Early troubleshooting notes and build logs

### Known Issues
- DNS configuration drift during early stages
- Domain dependency ordering not strictly enforced
- Incomplete validation between build phases

These issues informed the Phase 2 reset and rebuild.

---

## Notes

This changelog intentionally documents resets and architectural pivots.  
Rebuilds are treated as design decisions, not failures.

The goal of this project is not perfection on the first attempt, but mastery through iteration.
