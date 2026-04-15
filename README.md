# Hybrid Cloud Connectivity: VMware to Azure Site-to-Site VPN Lab

## 📌 Project Overview
This repository documents the implementation of a secure **Hybrid Cloud Infrastructure**. The project establishes an encrypted **Site-to-Site IPsec VPN tunnel** connecting an on-premises virtualized environment (VMware Workstation) with a Microsoft Azure Virtual Network (VNet).

## 🏗️ Architecture & Topology
The environment bridges two distinct sites using the **IKEv2 protocol** to ensure secure data transmission across the public internet.

| Component | Specifications |
| :--- | :--- |
| **On-Premises (VMware)** | Windows Server 2022 (RRAS/Gateway) & Windows 10 Client |
| **Cloud (Azure)** | Canada Central VNet, Virtual Network Gateway, Windows Server 2022 VM |
| **Connectivity** | Site-to-Site VPN (IPsec/IKEv2) |
| **Authentication** | Pre-Shared Key (PSK) |

### Network Addressing Table
| Network Segment | Subnet | IP Range |
| :--- | :--- | :--- |
| **On-Premises LAN** | VMnet2 (Internal) | `192.168.10.0/24` |
| **Azure VNet** | `vnet-canada-prod` | `172.16.0.0/16` |
| **Azure Gateway Subnet** | `GatewaySubnet` | `172.16.255.0/24` |

---

## 🛠️ Key Features & Implementation
* **Routing & NAT:** Configured Windows Server RRAS to manage internal LAN traffic and provide internet access via NAT.
* **Security Groups (NSG):** Implemented strict "Least Privilege" inbound rules, allowing RDP and ICMP traffic only from the designated on-premises subnet.
* **Infrastructure as Code (IaC):** Exported the environment as an **ARM Template** for modular redeployment.
* **Traffic Tunneling:** Forced all traffic destined for the `172.16.0.0/16` range through the encrypted tunnel using static routes.

---

## 🧪 Validation & Testing
To verify the hybrid link, the following tests were conducted:
1.  **Status Check:** Confirmed "Connected" state in both Azure Portal and RRAS Console.
2.  **ICMP Connectivity:** Successful `ping` from local client to Azure private IP after adjusting Windows Defender Firewall rules.
3.  **Encrypted Management:** Established a **Remote Desktop (RDP)** session over the private tunnel, bypassing the need for a Public IP on the cloud VM.

---

## 🧠 Lessons Learned & Troubleshooting
### The "$10 FinOps Lesson"
A critical takeaway from this project was the importance of **Cloud Cost Management**. During the early stages, I neglected to decommission the high-cost VPN Gateway after a test run, leading to an unexpected $10 charge. This experience led me to adopt **FinOps best practices**, such as implementing a "deploy-on-demand" workflow to preserve credits.

### Technical Hurdles
* **Firewall Hardening:** Encountered "Request Timed Out" errors due to default ICMP blocks. Resolved by creating specific Inbound Rules for Echo Requests in the Windows Advanced Firewall.
* **Dynamic Endpoint Updates:** Managed a Public IP change during resource recreation by dynamically updating the local Demand-Dial interface settings.

---

## 🎓 Professional Development
In preparation for this lab, I successfully completed the **Microsoft Azure Administrator (AZ-104) Learning Path**. This project serves as a practical application of those skills, focusing on hybrid networking, compute management, and security.

---

## 🚀 Future Outlook
While my current focus is expanding into broader IT specializations, this project solidifies my foundation in cloud administration. I plan to continue exploring **Infrastructure as Code (Terraform)** and **Automated Security Patching** in hybrid environments.
