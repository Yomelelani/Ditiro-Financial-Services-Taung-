# Ditiro-Financial-Services-Taung-

This project is an enterprise network designed and implemented in Cisco Packet Tracer.
The goal of the project was to build a segmented and secure network for different departments while providing controlled communication between departments and a dedicated server network.
The network includes:

VLAN segmentation
Inter-VLAN routing
Layer 3 switching
802.1Q trunking
Access Control Lists (ACLs)
SSH remote management
Dedicated management VLAN
Switch hardening
Static routing
The network consists of:

1 Cisco Catalyst 3560 Layer 3 core switch
3 Cisco Catalyst 2960 access switches
1 router
2Administration PCs
2Finance PCs
2HR PCs
2IT PCs
2Guest PCs
1 server
VLAN and IP Addressing Plan
VLAN 10 — Administration
Network: 192.168.15.0/27
Default Gateway: 192.168.15.1
Purpose: Administration department
VLAN 20 — Finance
Network: 192.168.15.32/27
Default Gateway: 192.168.15.33
Purpose: Finance department
VLAN 30 — HR
Network: 192.168.15.64/27
Default Gateway: 192.168.15.65
Purpose: Human Resources department
VLAN 40 — IT
Network: 192.168.15.96/27
Default Gateway: 192.168.15.97
Purpose: IT department
VLAN 50 — Guest
Network: 192.168.15.128/27
Default Gateway: 192.168.15.129
Purpose: Guest users and restricted access
VLAN 60 — Server
Network: 192.168.15.160/27
Default Gateway: 192.168.15.161
Server IP: 192.168.15.162
Purpose: Dedicated server network
VLAN 70 — Management
Network: 192.168.15.192/27
Default Gateway: 192.168.15.193
Purpose: Network device management
Router-to-Core Transit Network
Network: 192.168.15.224/30
Core 3560 Fa0/4: 192.168.15.225
Router Gi0/0/0: 192.168.15.226
Purpose: Routed connection between the core switch and router
Device Management

A dedicated management VLAN was created for network devices.

Core 3560: 192.168.15.193
SW1: 192.168.15.194
SW2: 192.168.15.195
SW3: 192.168.15.196
Network Configuration
VLAN Configuration

The network was divided into separate VLANs to isolate different departments.

VLAN 10 - Administration
VLAN 20 - Finance
VLAN 30 - HR
VLAN 40 - IT
VLAN 50 - Guest
VLAN 60 - Server
VLAN 70 - Management
Inter-VLAN Routing

The Cisco Catalyst 3560 was configured as a Layer 3 switch.

IP routing was enabled and SVIs were configured for each VLAN.

interface vlan 10
 ip address 192.168.15.1 255.255.255.224

interface vlan 20
 ip address 192.168.15.33 255.255.255.224

interface vlan 30
 ip address 192.168.15.65 255.255.255.224
 Security Configuration
Guest Network Isolation

The Guest VLAN was restricted from accessing the internal 192.168.15.0/24 network.

ACL:

GUEST_RESTRICTION

The ACL was applied inbound on VLAN 50.

This prevents Guest devices from reaching internal departmental and server networks while allowing other traffic according to the configured policy.

Server Protection

The server uses:

192.168.15.162

Access to the server was permitted from:

Administration
Finance
HR
IT

Other sources were denied.

ACL:

SERVER_PROTECTION

The ACL was applied outbound to VLAN 60.

Switch Hardening

Unused switch ports were:

Moved to VLAN 999
Administratively shut down
interface range fastethernet 0/8 - 24
 switchport mode access
 switchport access vlan 999
 shutdown

SSH was used instead of Telnet for remote management.

A login banner was also configured on the switches.

Routing

The 3560 core switch uses a default route toward the router:

0.0.0.0/0 → 192.168.15.226

The router contains static routes back to all internal VLAN networks through:

192.168.15.225
Testing and Verification

The configuration was tested using Cisco IOS verification commands and end-device connectivity tests.

Successful Tests
Administration PCs reached VLAN 10 gateway
Finance PCs reached VLAN 20 gateway
HR PCs reached VLAN 30 gateway
IT PCs reached VLAN 40 gateway
Guest PCs reached VLAN 50 gateway
Administration reached the server
Finance reached the server
HR reached the server
IT reached the server
Core reached the router
SSH access to SW1
SSH access to SW2
SSH access to SW3
Security Tests

Guest traffic to internal networks was blocked by GUEST_RESTRICTION.

Unauthorized access to the server was blocked by SERVER_PROTECTION.

ACL counters were checked using:

show ip access-lists
Verification Commands

The following commands were used to verify the network:

show vlan brief
show interfaces status
show interfaces trunk
show ip interface brief
show ip route
show ip access-lists
show spanning-tree
show cdp neighbors
show ip ssh
copy running-config startup-config
Technologies Used
Cisco Packet Tracer
Cisco IOS
VLANs
802.1Q trunking
Layer 3 switching
Inter-VLAN routing
ACLs
SSH
Spanning Tree Protocol
Static routing
Network segmentation
Project Files
milestone_onepkt/

screenshots/
    topology.png
    vlan-configuration.png
    routing.png
    acl-security.png
    ssh-management.png
What I Learned

This project improved my practical understanding of:

Designing a segmented enterprise network
Configuring Cisco switches
Creating and assigning VLANs
Configuring Layer 3 SVIs
Troubleshooting trunk and native VLAN issues
Using Spanning Tree Protocol
Implementing ACL-based security
Configuring secure SSH management
Verifying network connectivity using Cisco IOS commands
Troubleshooting network connectivity systematically
Author
YOMELELANI DAMANE
GitHub:https://github.com/Yomelelani/Ditiro-Financial-Services-Taung-
