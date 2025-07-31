# Small-Home-Office-Network
Design, implement, and configure a functional small office/home office (SOHO) network using Cisco Packet Tracer

## Phase 1: Network Design and IP Addressing Scheme
### LAN Segment 1 Office Network 192.168.1.0/24
- Gateway 192.168.1.1
- DHCP Pool: 192.168.1.100 - 192.168.1.200
### LAN Segment 2 Server Network: 192.168.2.0/24
- Gateway: 192.168.2.1
- DHCP Pool: 192.168.2.100 - 192.168.2.200
### WAN Link (ISP Simulation): 10.0.0.0/30
- Router Interface: 10.0.0.1
- ISP Router Interface: 10.0.0.2

  
![image alt](https://github.com/Salayne/Small-Home-Office-Network/blob/main/1.png)


## Phase 2: Initial Device Placement and Cabling
- 1 2911 router (Edge Router)
- 2 2960 switches
- 2 PCS
- 1 server
- 1 2901 router (ISP router)

![image alt](https://github.com/Salayne/Small-Home-Office-Network/blob/main/cableConnections.png)

**Cable Connections:**
- Router to Switches: Use Copper Straight-Through cables.
- Router GigabitEthernet0/0/0 to Switch 1 FastEthernet0/1
- Router GigabitEthernet0/0/1 to Switch 2 FastEthernet0/1
- Switches to PCs/Server: Use Copper Straight-Through cables.
- Switch 1 FastEthernet0/2 to PC1 FastEthernet0
- Switch 2 FastEthernet0/2 to PC2 FastEthernet0
- Switch 2 FastEthernet0/3 to Server FastEthernet0
- Router GigabitEthernet0/0/2 to ISP Router GigabitEthernet0/0


## Phase 3: Router Configuration (Edge Router)

- Access CLI: Click on the Cisco 2911 Router and go to the "CLI" tab.
- Enable Mode: ***Type*** enable
- Global Configuration Mode: ***Type*** configure terminal
- Configure Hostname: hostname Edge_Router
- 

  **Configure Interface for LAN Segment 1:**
- interface GigabitEthernet0/0
- ip address 192.168.1.1 255.255.255.0
- no shutdown
- description Link to Office_LAN
- exit


**Configure Interface for LAN Segment 2:**
- interface GigabitEthernet0/1
- ip address 192.168.2.1 255.255.255.0
- no shutdown
- description Link to Server_LAN
- exit


**Configure Interface for WAN Link:**
- interface GigabitEthernet0/2
- ip address 10.0.0.1 255.255.255.252
- no shutdown
- description Link to ISP
- exit

  
![image alt](https://github.com/Salayne/Small-Home-Office-Network/blob/main/routerConfig1.png)


**Configure DHCP Server for LAN Segment 1:**
- ip dhcp pool OFFICE_POOL
- network 192.168.1.0 255.255.255.0
- default-router 192.168.1.1
- dns-server 192.168.2.10 (We will configure the server with this IP later)
- exit
- ip dhcp excluded-address 192.168.1.1 192.168.1.99


**Configure Default Route (to ISP):**
- ip route 0.0.0.0 0.0.0.0 10.0.0.2


**Save Configuration:**
- copy running-config startup-config



![image alt](https://github.com/Salayne/Small-Home-Office-Network/blob/main/routerConfig2.png)



## Phase 4: ISP Router Configuration (Simulation)

- Access CLI: Click on the Generic Router (simulating ISP) and go to the "CLI" tab.
- Enable Mode: **Type** enable
- Global Configuration Mode: Type configure terminal
- Configure Hostname: hostname ISP_Router

**Configure Interface for WAN Link:**
- interface GigabitEthernet0/0
- ip address 10.0.0.2 255.255.255.252
- no shutdown
- description Link to Edge_Router
- exit

**Configure Static Route back to your network:**
- ip route 192.168.1.0 255.255.255.0 10.0.0.1
- ip route 192.168.2.0 255.255.255.0 10.0.0.1

**Save Configuration:**
copy running-config startup-config

![image alt](https://github.com/Salayne/Small-Home-Office-Network/blob/main/ISPConfig1.png)








## Phase 5: Server Configuration (DHCP/DNS on LAN Segment 2)
## Phase 6: Client PC Configuration and Verification
## Phase 7: Connectivity Testing and Verification
