# Analyst VM Build Notes

The analyst VM was created early in the lab build to validate networking, firewall rules, and segmentation.

## Initial Challenges
- VM originally attached to vmbr0, receiving a 192.168.1.x IP
- Failed to reach the firewall or internal network
- Netplan changes initially rejected due to YAML indentation issues

## Resolutions
- Moved NIC to vmbr1
- Assigned static 10.0.10.20/24 IP
- Adjusted YAML formatting and file permissions
- Confirmed outbound internet access through firewall NAT

## Role in the SOC Lab
This VM acts as the primary validation endpoint.  
It will later be used for:
- Running investigations
- Querying Wazuh dashboards
- Testing FleetDM visibility
- Writing automation scripts
- Observing normal and malicious behavior inside the lab

## Future Enhancements
- Install Python tooling
- Configure Wazuh agent
- Add security utilities
- Integrate with AD after Windows Server deployment
