# Project_02: Optimizing Network Subnetting and Configuration for Site Expansion
Author: Carl Xymon Verdejo
Contact: carl.xymon.verdejo@gmail.com

# Project Overview
## Background
In this project, we aim to design and configure a small-scale network with multiple subnets and internet connectivity using Cisco Packet Tracer. Building upon the previous project (Project_01), we will extend and conserve IP addresses for network expansion in Project_02.

## Network Topology (Pre-Subnetting / After Project_01)
The initial network topology in Project_01 consisted of two primary sites, Site 1 and Site 2, connected to an intermediary router (IntRouter) for internet access. Subnetting was performed on the 192.168.1.0/24 network to allocate IP addresses efficiently for various network segments.

## Objectives
Break up the 192.168.1.64/26 subnet to support as many subnets as possible with at least 8 hosts each.

Allocate the first new subnet to Site 3 and manually configure all devices in this subnet.

Subnet the last new subnet obtained from 192.168.1.64/26 with /30 masks for serial links.

Verify network connectivity and internet access for all PCs.

# Network Design: Subnetting Calculations
Subnetting Details: Insert your subnetting Excel tables here to provide detailed calculations for the subnetting process. Ensure to include columns for IP Address, CIDR, Subnet Mask, Interface, Interface Port, Device Name, Remarks, and Configured status.

# Network Design: Network Topology (After Subnetting)
After subnetting, the network was expanded to include Site 3. The new topology consists of three primary sites, each connected to the IntRouter, with subnets allocated for efficient IP address management.

## Site 3 (Subnet 1: 192.168.1.64/28)
Router R4: 192.168.1.78
Switch S3: 192.168.1.77
PCs: Manually assigned IPs from 192.168.1.65 to 192.168.1.76

## Serial Links (Subnet 2: 192.168.1.240/28)
R4 ↔ IntRouter: 192.168.1.241, 192.168.1.242
R2 ↔ IntRouter: 192.168.1.245, 192.168.1.246
R1 ↔ IntRouter: 192.168.1.249, 192.168.1.250

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

### Manually Configuring IPs for PCs
PC6:
- IP Address: 192.168.1.65
- Subnet Mask: 255.255.255.240
- Default Gateway: 192.168.1.78

PC7:
- IP Address: 192.168.1.66
- Subnet Mask: 255.255.255.240
- Default Gateway: 192.168.1.78

PC8:
- IP Address: 192.168.1.67
- Subnet Mask: 255.255.255.240
- Default Gateway: 192.168.1.78

## Verification and Testing
To verify the network configuration, we conducted several tests:

### Ping Tests:
- PCs were able to ping their default gateways and other devices within their subnet.
- PCs successfully pinged external IP addresses (e.g., 8.8.8.8).

Browser Tests:
- PCs accessed websites like cisco.comand facebook.comto confirm internet connectivity.

## Results
The network was successfully expanded and configured according to the objectives. All devices communicated effectively within their subnets and accessed the internet.

## Limitations of Project
### Simulation Tool Constraints
Cisco Packet Tracer is a simulation tool and does not fully replicate real-world network behavior in terms of performance, latency, and security threats.

### Lack of Redundancy
The current setup lacks redundancy mechanisms such as HSRP, VRRP, or load balancing, which are crucial for enterprise-level reliability.

### Minimal Security Measures
Security configurations like firewall rules and access control lists (ACLs) were not implemented in this project.

## Future Improvements and Optimization
### Implementing Redundancy and Failover Mechanisms
Introduce protocols like HSRP or VRRP to ensure failover if a router goes down. Use EtherChannel or Link Aggregation (LACP) to create redundant links.

### Optimizing Network Performance
Implement Quality of Service (QoS) to prioritize critical traffic. Introduce traffic shaping and rate limiting to prevent congestion.

### Enhancing Security Measures
Apply ACLs on routers to restrict unauthorized traffic. Implement firewall rules and 802.1X authentication for device access control. Enable IDS/IPS for network monitoring.

### Expanding the Network with VLANs and Subnetting
Introduce VLAN segmentation to improve security and reduce broadcast traffic. Use Inter-VLAN Routing to enable communication between different VLANs.

### Real-World Deployment and Testing
Conduct physical implementation using real routers, switches, and servers to test real-world performance. Use tools like GNS3 or EVE-NG for more accurate network simulations. Perform penetration testing to evaluate network security.

## Conclusion
The project successfully demonstrated the implementation of a structured enterprise-level network using subnetting, routing, switching, and DHCP services. By dividing the 192.168.1.0/24 network into smaller subnets, IP address management was optimized, and logical segmentation was achieved. The configuration of routers, switches, and DHCP servers ensured efficient network communication between local and remote hosts. This topology serves as a foundational model for small-to-medium business networks, providing scalability and efficiency while maintaining security and performance. Future improvements could include VLAN segmentation, load balancing, and redundancy mechanisms to improve fault tolerance. Overall, the project

