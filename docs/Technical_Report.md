# Technical Report: Hybrid Cloud Connectivity Implementation

**Student:** Oscar Castro  
**Program:** IT Systems Management and Security (NSCC)  
**Project:** Site-to-Site VPN (VMware to Azure)

## 1. Executive Summary
The objective of this project was to establish a secure and encrypted connection between a local virtual environment (VMware Workstation) and a Microsoft Azure Virtual Network (VNet).

## 2. Network Topology and Architecture
| Resource | Interface / Network | IP Address | Purpose |
| :--- | :--- | :--- | :--- |
| **VM 1 (Local Server)** | WAN (NAT) | 192.168.58.128 | Internet Access / VPN Endpoint |
| **VM 1 (Local Server)** | LAN (VMnet2) | 192.168.10.1 | Gateway for Local Clients |
| **VM 2 (Local Client)** | LAN (VMnet2) | 192.168.10.10 | User Workstation |
| **Azure VNet** | vnet-canada-prod | 172.16.0.0/16 | Cloud Network Space |
| **Azure VM** | vm-project | 172.16.0.x | Workload (Private IP) |
| **VPN Gateway** | vng-canada-hybrid | 20.150.110.150 | Azure VPN Entry Point |

## 3. System Operation
The environment operates through a three-layer routing process involving Gateway Routing, IPsec Encapsulation (IKEv2), and Cloud Firewall (NSG) inspection.

## 4. Connectivity Evidence
Validation was confirmed by accessing the Azure VM using its private IP address via RDP and successful Ping tests after firewall adjustments.

## 5. Professional Development
As part of this project, I completed the Azure Administrator learning path on Microsoft Learn to master identity, storage, and network management.

## 6. Troubleshooting
Key challenges included resolving ICMP blocks via Windows Defender Firewall and managing public IP changes during resource recreation in Azure.

## 7. Conclusion
This project demonstrates a functional Hybrid Cloud architecture, validating security, routing, and cost management skills.
