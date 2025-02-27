# Project_02: Optimizing Network Subnetting and Configuration for Site Expansion
Author: [Carl Xymon Verdejo]() </br>
Contact: [carl.xymon.verdejo@gmail.com](carl.xymon.verdejo@gmail.com)

# Project Overview
## Background
In this project, we aim to design and configure a small-scale network with multiple subnets and internet connectivity using Cisco Packet Tracer. Building upon the previous project (Project_01), we will extend and conserve IP addresses for network expansion in Project_02.

## Network Topology (Pre-Subnetting / After Project_01)
The initial network topology in Project_01 consisted of two primary sites, Site 1 and Site 2, connected to an intermediary router (IntRouter) for internet access. Subnetting was performed on the ```192.168.1.0 /24``` network to allocate IP addresses efficiently for various network segments.
![]()

## Objectives
1. Break up the ```192.168.1.64 /26``` subnet to support as many subnets as possible with at least 8 hosts each.
2. Allocate the first new subnet to Site 3 and manually configure all devices in this subnet.
3. Subnet the last new subnet obtained from ```192.168.1.64/26``` with ```/30``` masks for serial links.
4. Verify network connectivity and internet access for all PCs.

# Network Design: Subnetting Calculations

![]()

# Network Design: Network Topology (After Subnetting)
After subnetting, the network was expanded to include Site 3. The new topology consists of three primary sites, each connected to the IntRouter, with subnets allocated for efficient IP address management.

## Site 3 (Subnet 1: ```192.168.1.64/28```)
- Router R4: ```192.168.1.78/28```
- Switch S3: ```192.168.1.77/28```
- PCs: Manually assigned IPs from ```192.168.1.65/28``` to ```192.168.1.76/28```

## Serial Links (Subnet 2: 192.168.1.112/28
- R4 ↔ IntRouter : ```192.168.1.117/30```↔ ```192.168.1.118/30```
- R2 ↔ IntRouter : ```192.168.1.121/30```↔ ```192.168.1.122/30```
- R1 ↔ IntRouter : ```192.168.1.112/30```↔ ```192.168.1.113/30```

## Device Configuration
### Router (R1) Configuration Example:
``` plaintext
Router>enable
Router#configure terminal
Router(config)#hostname R1
Router(config)#interface GigabitEthernet 0/0/0
Router(config-if)#no shutdown
Router(config-if)#ip address 192.168.1.62 255.255.255.192
Router(config-if)#exit
Router(config)#end
Router#copy running-config startup-config
Router#ping 192.168.1.62
```
![]()

### Switch (S1) Configuration Example:
``` plaintext
Switch>enable
Switch#configure terminal
Switch(config)#hostname S1
S1(config)#ip default-gateway 192.168.1.62
S1(config)#interface vlan 1
S1(config-if)#no shutdown
S1(config-if)#ip address 192.168.1.61 255.255.255.192
S1(config-if)#exit
S1(config)#end
S1#copy running-config startup-config
S1#ping 192.168.1.62
```
![]()

### Manually Configuring IPs for PCs
| PC   | IP Address     | Subnet Mask        | Default Gateway |
|------|----------------|--------------------|-----------------|
| PC6  | 192.168.1.65   | 255.255.255.240    | 192.168.1.78    |
| PC7  | 192.168.1.66   | 255.255.255.240    | 192.168.1.78    |
| PC8  | 192.168.1.67   | 255.255.255.240    | 192.168.1.78    |

## Verification and Testing
To verify the network configuration, we conducted several tests:

### Ping Tests:
- PCs were able to ping their default gateways and other devices within their subnet.
- PCs successfully pinged external IP addresses (e.g., 8.8.8.8).

### Browser Tests:
- PCs accessed websites like [cisco.com](cisco.com) and [facebook.com](facebook.com) to confirm internet connectivity.

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

