# CCNA Cisco Multi-Site Network Project 🌐

(CCNA-Cisco-Multi-Site-Network-Project
/topology.png)

## 📖 About The Project

This project is a comprehensive network simulation designed to validate core **CCNA (Cisco Certified Network Associate)** routing and switching concepts. It simulates a realistic multi-site enterprise network connecting a **Headquarters (HQ)** and a remote **Branch Office** via a WAN link, with secure edge connectivity to an **ISP**.

The topology demonstrates the integration of **Layer 2 switching**, **Layer 3 Inter-VLAN routing**, **dynamic routing (OSPF)**, and **network security (ACLs & NAT)**.

## 🛠️ Technologies & Features

This lab covers topics from CCNA 1 (ITN), CCNA 2 (SRWE), and CCNA 3 (ENSA):

*   **VLANs & Trunks:** Segmentation of Sales, Engineering, and Management traffic (802.1Q).
    
*   **Inter-VLAN Routing:**
    
    *   **HQ:** Layer 3 Switching using SVIs.
        
    *   **Branch:** Router-on-a-Stick (ROAS) utilizing subinterfaces.
        
*   **Dynamic Routing:** Single-Area **OSPFv2** with `default-information originate` for internet route propagation.
    
*   **Network Services:**
    
    *   **DHCPv4:** Dynamic IP allocation for end devices.
        
    *   **NAT/PAT:** Overloading a single public IP for internal private subnets.
        
*   **Security:**
    
    *   **Extended ACLs:** Strict traffic filtering (e.g., blocking Engineering VLAN from Management).
        
    *   **SSH:** Secure remote management for network devices.
        
*   **WAN Connectivity:** Serial DCE/DTE simulation between sites.
    

## 🧩 Topology Overview

| Device | Role | Key Configurations |
| --- | --- | --- |
| HQ-R1 | Edge Router | NAT/PAT, OSPF, ACLs, Default Route to ISP. |
| HQ-Core-SW | L3 Core Switch | SVIs (VLAN 10, 20), DHCP Server, OSPF. |
| BR-R1 | Branch Router | ROAS, OSPF, DHCP Server. |
| BR-SW1 | L2 Access Switch | VLANs, Trunking, SSH Management. |
| ISP | Service Provider | Simulated Public Internet & DNS (8.8.8.10). |

## 🚀 Getting Started

### Prerequisites

*   **Cisco Packet Tracer** (Version 8.0 or newer recommended) OR
    
*   **GNS3 / EVE-NG** (with appropriate IOS images).
    

### Installation

1.  Clone this repository:
    

    git clone [https://github.com/yourusername/ccna-master-lab.git](https://github.com/yourusername/ccna-master-lab.git)
    

2.  Open the topology file (e.g., `.pkt`) in your simulator.
    
3.  If starting from scratch, copy the configurations from the `configs/` folder into the CLI of each respective device.
    

## 🧪 Verification & Testing

To verify the network is fully functional, perform the following checks:

### 1\. Connectivity (Ping)

*   **Internal:** PC-Sales (HQ) should be able to ping PC-Branch (Branch).
    
*   **External:** All PCs should be able to ping the ISP Server at `8.8.8.10`.
    

### 2\. Routing (OSPF)

Check the routing table on the HQ Core Switch:

    HQ-Core-SW# show ip route
    > O*E2 0.0.0.0/0 [110/1] via 10.1.1.1
    

### 3\. Security (ACLs)

*   **Permit:** VLAN 10 (Sales) -> VLAN 99 (Mgmt) = **SUCCESS**
    
*   **Deny:** VLAN 20 (Engineering) -> VLAN 99 (Mgmt) = **FAIL**
    

### 4\. NAT

Run a ping to the internet and check translations on the Edge Router:

    HQ-R1# show ip nat translations
    > Pro Inside global      Inside local       Outside local      Outside global
    > icmp 209.165.200.226:1 192.168.10.10:1    8.8.8.10:1         8.8.8.10:1
    

## 💡 Key Learnings

*   **ACL Sequencing:** Learned that `permit` statements for routing protocols (OSPF) and ICMP must be carefully placed before specific `deny` statements to prevent accidental isolation.
    
*   **NAT Troubleshooting:** Resolved "Destination Host Unreachable" errors by ensuring the Edge Router had a static default route pointing to the ISP, which was then propagated via OSPF.
    
*   **Layer 3 Switching:** Configured `ip routing` on the Core switch to offload inter-VLAN traffic from the router.
    

## 👤 Author

**Stuart**

*   [LinkedIn](https://www.google.com/search?q=https://www.linkedin.com/in/stuartcybersecurity "null")
    

_This project was created for educational purposes to demonstrate CCNA networking proficiency._
