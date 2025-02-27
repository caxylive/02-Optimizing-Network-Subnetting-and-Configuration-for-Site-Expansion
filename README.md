# Project_02: Optimizing Network Subnetting and Configuration for Site Expansion
Author: [Carl Xymon Verdejo](https://hardworking-lion-z4sd3b.mystrikingly.com/) </br>
Contact: [carl.xymon.verdejo@gmail.com](carl.xymon.verdejo@gmail.com)

# Project Overview
## Background
In this project, we aim to design and configure a small-scale network with multiple subnets and internet connectivity using Cisco Packet Tracer. Building upon the previous project (Project_01), we will extend and conserve IP addresses for network expansion in Project_02.

## Network Topology (Pre-Subnetting / After Project_01)
The initial network topology in Project_01 consisted of two primary sites, Site 1 and Site 2, connected to an intermediary router (IntRouter) for internet access. Subnetting was performed on the ```192.168.1.0 /24``` network to allocate IP addresses efficiently for various network segments.
![Figure 1: Network Topology](/screenshot/project_02-network-topology-initial.png)

## Objectives
1. Break up the ```192.168.1.64 /26``` subnet to support as many subnets as possible with at least 8 hosts each.
2. Allocate the first new subnet to Site 3 and manually configure all devices in this subnet.
3. Subnet the last new subnet obtained from ```192.168.1.64/26``` with ```/30``` masks for serial links.
4. Verify network connectivity and internet access for all PCs.

# Network Design: Subnetting Calculations

![Table 1: Subnetting Table](/screenshot/project_02-subnetting-table.png)

# Network Design: Network Topology (After Subnetting)
After subnetting, the network was expanded to include Site 3. The new topology consists of three primary sites, each connected to the IntRouter, with subnets allocated for efficient IP address management. Below is a screenshot of the network topology populated with IP Addresses:
![Figure 2: Network Topology](/screenshot/project02-network-topology.png)

## Site 3 (Subnet: 192.168.1.64/28)
| **Device**    | **IP Address**| CIDR |
|---------------|---------------|------|
| **Router R4** | 192.168.1.78  | /28  |
| **Switch S3** | 192.168.1.77  | /28  |
| **PC6**       | 192.168.1.65  | /28  |
| **PC7**       | 192.168.1.66  | /28  |
| **PC8**       | 192.168.1.67  | /28  |

## Serial Links (Subnet: 192.168.1.112/30 - 192.168.1.120/30)
| **Link**             |   **IP Address**       | **IP Address IntRouter** |
|----------------------|------------------------|--------------------------|
| **R4 ↔ IntRouter**   | 192.168.1.117 /30      | 192.168.1.118 /30        |
| **R2 ↔ IntRouter**   | 192.168.1.121 /30      | 192.168.1.122 /30        |
| **R1 ↔ IntRouter**   | 192.168.1.112 /30      | 192.168.1.113 /30        |

## Device Configuration
### Router (R1) Serial Configuration Example:
- Assign ```192.168.1.113``` ```255.255.255.252``` to R1 Serial 0/1/0 interface
- Bring up the interface: ```no shutdown```
- Check Serial 0/1/0 is up: ```show ip interface brief```
- copy vRAM into nvRAM: ```copy running-config startup-config```
![Figure 3: R1 Config - Serial 0/1/0](/screenshot/R1-config-serial.png)

### Router (R2) Serial Configuration Example:
- Assign ```192.168.1.121``` ```255.255.255.252``` to R2 Serial 0/1/0 interface
- Bring up the interface: ```no shutdown```
- Check Serial 0/1/0 is up: ```show ip interface brief```
- copy vRAM into nvRAM: ```copy running-config startup-config```
![Figure 4: R2 Config - Serial 0/1/0](/screenshot/R2-config-serial.png)

### Router (R4) Serial Configuration Example:
- Assign ```192.168.1.117``` ```255.255.255.252``` to R4 Serial 0/1/0 interface
- Bring up the interface: ```no shutdown```
- Check Serial 0/1/0 is up: ```show ip interface brief```
- copy vRAM into nvRAM: ```copy running-config startup-config```
![Figure 5: R4 Config - Serial 0/1/0](/screenshot/R4-config-serial.png)

### IntRouter ↔ R1 Serial Configuration Example:
- Assign ```192.168.1.114``` ```255.255.255.252``` to R1 Serial 0/1/0 interface
- Bring up the interface: ```no shutdown```
- Check Serial 0/1/0 is up: ```show ip interface brief```
- copy vRAM into nvRAM: ```copy running-config startup-config```
![Figure 6: IntRouter-R1 - Serial 0/1/0](/screenshot/IntRouter-config-serial-r1.png)

### IntRouter ↔ R2 Serial Configuration Example:
- Assign ```192.168.1.122``` ```255.255.255.252``` to R1 Serial 0/1/1 interface
- Bring up the interface: ```no shutdown```
- Check Serial 0/1/1 is up: ```show ip interface brief```
- copy vRAM into nvRAM: ```copy running-config startup-config```
![Figure 7: IntRouter-R2 - Serial 0/1/1](/screenshot/IntRouter-config-serial-r2.png)

### IntRouter ↔ R4 Serial Configuration Example:
- Assign ```192.168.1.118``` ```255.255.255.252``` to R1 Serial 0/2/0 interface
- Bring up the interface: ```no shutdown```
- Check Serial 0/2/0 is up: ```show ip interface brief```
- copy vRAM into nvRAM: ```copy running-config startup-config```
![Figure 8: IntRouter-R4 Config - Serial 0/2/0](/screenshot/IntRouter-config-serial-r4.png)

### R4 ↔ S3 GigabitEthernet Configuration Example:
- Assign ```192.168.1.78``` ```255.255.255.240``` to R4 GigabitEthernet 0/0/0 interface
- Bring up the interface: ```no shutdown```
- Check GigabitEthernet 0/0/0 is up: ```show ip interface brief```
- copy vRAM into nvRAM: ```copy running-config startup-config```
![Figure 9: R4↔S3 Config - GigabitEthernet 0/0/0](/screenshot/R4-config-r4-s3.png)

### S3 Vlan1 Configuration Example:
- Assign ```192.168.1.77``` ```255.255.255.240``` to S3 Vlan1 interface
- Bring up the interface: ```no shutdown```
- Check Vlan1 is up: ```show ip interface brief```
- copy vRAM into nvRAM: ```copy running-config startup-config```
![Figure 10: S3 Config - Vlan1](/screenshot/S3-config-vlan1.png)

### Manually Configuring IPs for PCs
| PC       | IP Address     | Subnet Mask     | Default Gateway |
|----------|----------------|-----------------|-----------------|
| **PC6**  | 192.168.1.65   | 255.255.255.240 | 192.168.1.78    |
| **PC7**  | 192.168.1.66   | 255.255.255.240 | 192.168.1.78    |
| **PC8**  | 192.168.1.67   | 255.255.255.240 | 192.168.1.78    |

## Verification and Testing
To verify the network configuration, we conducted several tests:

### Ping Tests:
- PCs were able to ping their default gateways and other devices within their subnet.
- PCs successfully pinged external IP addresses (e.g., Google DNS [8.8.8.8], facebook.com, cisco.com).
![Figure 11: Pinging External Sites](/screenshot/PC6-ipconfig-ping.png)
- Pinging Internal Devices from Site_01 and Site_02 </br>
![Figure 12: Pinging Internal Devices](/screenshot/PC6-ping.png)

### Browser Tests:
- PCs accessed websites like [cisco.com](cisco.com)
![Figure 13: Visiting Cisco's Website](/screenshot/PC6-cisco.png)
- And [facebook.com](facebook.com) to confirm internet connectivity.
![Figure 14: Visiting Facebook's Website](/screenshot/PC6-facebook.png)

## Results
The ```192.168.1.64 /26``` subnet was successfully divided into smaller subnets, maximizing the number of subnets with at least 8 hosts each. This approach allowed for efficient IP address allocation and accommodated additional devices within the network.

The first new subnet ```192.168.1.64 /28``` was allocated to Site 3. All devices in Site 3, including Router R4, Switch S3, and PCs (PC6, PC7, and PC8), were manually configured with appropriate IP addresses. This ensured that Site 3 was fully integrated into the network.

The last new subnet from ```192.168.1.64 /26``` was further divided into ```/30``` subnets for serial links. This provided efficient IP address allocation for the serial links connecting R4, R2, and R1 to the IntRouter. Each serial link was configured with the correct IP addresses, ensuring seamless connectivity.

Extensive verification and testing were conducted to ensure network connectivity and internet access for all PCs. Ping tests confirmed that PCs could communicate with their default gateways and other devices within their subnets. Browser tests verified that PCs could access external websites like [cisco.com](cisco.com) and [facebook.com](facebook.com), demonstrating successful internet connectivity.

The project successfully met all the objectives, demonstrating the effectiveness of subnetting and IP address management. The network's scalability and manageability were enhanced, providing a solid foundation for future expansion and optimization.

## Limitations of Project
### 1. Simulation Tool Constraints
Cisco Packet Tracer is a simulation tool and does not fully replicate real-world network behavior in terms of performance, latency, and security threats.

### 2. Lack of Redundancy
The current setup lacks redundancy mechanisms such as HSRP, VRRP, or load balancing, which are crucial for enterprise-level reliability.

### 3. Minimal Security Measures
Security configurations like firewall rules and access control lists (ACLs) were not implemented in this project.

## Future Improvements and Optimization
### 1. Implementing Redundancy and Failover Mechanisms
Introduce protocols like **HSRP** or **VRRP** to ensure failover if a router goes down. Use **EtherChannel** or **Link Aggregation** (**LACP**) to create redundant links.

### 2. Optimizing Network Performance
Implement **Quality of Service** (**QoS**) to prioritize critical traffic. Introduce **traffic shaping** and **rate limiting** to prevent congestion.

### 3. Enhancing Security Measures
Apply **ACLs** on routers to restrict unauthorized traffic. Implement **firewall rules** and **802.1X authentication** for device access control. Enable **IDS/IPS** for network monitoring.

### 4. Expanding the Network with VLANs and Subnetting
Introduce **VLAN segmentation** to improve security and reduce broadcast traffic. Use **Inter-VLAN Routing** to enable communication between different VLANs.

### 5. Real-World Deployment and Testing
Conduct **physical implementation** using real routers, switches, and servers to test **real-world performance**. Use tools like **GNS3** or **EVE-NG** for more accurate network simulations. Perform **penetration testing** to evaluate network security.

## Conclusion
The project successfully demonstrated the implementation of a structured enterprise-level network using subnetting, routing, switching, and DHCP services. By dividing the ```192.168.1.0/24``` network into smaller subnets, IP address management was optimized, and logical segmentation was achieved. The configuration of routers, switches, and DHCP servers ensured efficient network communication between local and remote hosts. This topology serves as a foundational model for small-to-medium business networks, providing scalability and efficiency while maintaining security and performance. Future improvements could include VLAN segmentation, load balancing, and redundancy mechanisms to improve fault tolerance. Overall, the project achieved its goals and laid the groundwork for a robust and scalable network infrastructure.

