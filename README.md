# Inter-VLAN Routing - Cisco Packet Tracer Lab

### Overview

This project demonstrates **Inter-VLAN Routing** using Cisco Packet Tracer. The lab is designed to showcase how to configure VLANs on switches and routers to enable communication between devices across different VLANs. The goal is to familiarize users with VLAN configuration, router-on-a-stick setup, and effective communication between VLANs.
<img src= "https://github.com/ro-drick/Inter-VLAN-Routing/blob/main/inter-vlan-routing.PNG">

### Lab Details

- **File:** `inter-vlan-routing.pkt`
- **Tool:** Cisco Packet Tracer
- **Concepts Covered:**
  - VLAN creation and management on switches
  - Router-on-a-stick configuration
  - Subnetting for different VLANs
  - Inter-VLAN communication via routing

### Prerequisites

Before starting with this lab, ensure you have the following:

- Cisco Packet Tracer installed on your system.
- Basic knowledge of VLANs, subnetting, and Cisco commands.
- Familiarity with configuring switches and routers.

### Step-by-Step Configuration Process

#### 1. **Configure VLANs on the Switch**

   a. **Access the switch CLI:**  
```bash
      Switch> enable
      Switch# configure terminal
```

   b. **Create VLANs:**  
      For each VLAN (e.g., VLAN 10 and VLAN 20), use the following commands:
      
```bash
      Switch(config)# vlan 10
      Switch(config-vlan)# name STUDENTS
      Switch(config-vlan)# exit
      Switch(config)# vlan 20
      Switch(config-vlan)# name FACULTY
      Switch(config-vlan)# exit
```

   c. **Assign VLANs to Switch Ports:**  
      Assign the appropriate switch ports to the VLANs:
```bash
      Switch(config)# interface fastethernet 0/1
      Switch(config-if)# switchport mode access
      Switch(config-if)# switchport access vlan 10
      Switch(config-if)# exit
      Switch(config)# interface fastethernet 0/2
      Switch(config-if)# switchport mode access
      Switch(config-if)# switchport access vlan 20
      Switch(config-if)# exit
```

#### 2. **Configure Trunk Port on the Switch**

   a. **Set the Trunk Port:**  
      This is necessary for communication between the switch and the router. Configure the port connecting to the router as a trunk:
```bash
      Switch(config)# interface fastethernet 0/24
      Switch(config-if)# switchport mode trunk
      Switch(config-if)# exit
```

#### 3. **Configure the Router (Router-on-a-stick)**

   a. **Access the router CLI:**
```bash
      Router> enable
      Router# configure terminal
```

   b. **Create Sub-Interfaces for Each VLAN:**  
      For each VLAN, create a sub-interface on the router's interface connected to the switch. For example, if `FastEthernet 0/0` is connected:
```bash
      Router(config)# interface fastethernet 0/0.10
      Router(config-subif)# encapsulation dot1Q 10
      Router(config-subif)# ip address 192.168.10.1 255.255.255.0
      Router(config-subif)# exit

      Router(config)# interface fastethernet 0/0.20
      Router(config-subif)# encapsulation dot1Q 20
      Router(config-subif)# ip address 192.168.20.1 255.255.255.0
      Router(config-subif)# exit
```

   c. **Activate the Physical Interface:**  
      Enable the physical interface on the router:
```bash
      Router(config)# interface fastethernet 0/0
      Router(config-if)# no shutdown
      Router(config-if)# exit
```

#### 4. **Assign IP Addresses to End Devices**

   - **PC1 (VLAN 10):**
     - IP address: `192.168.10.x`
     - Subnet mask: `255.255.255.0`
     - Default gateway: `192.168.10.1`
   
   - **PC2 (VLAN 20):**
     - IP address: `192.168.20.x`
     - Subnet mask: `255.255.255.0`
     - Default gateway: `192.168.20.1`

#### 5. **Test Inter-VLAN Communication**

   a. **Ping from one VLAN to another:**
      - Test the connectivity by pinging from a PC in VLAN 10 to a PC in VLAN 20.
      - If configuration is correct, the devices will be able to communicate through the router.

---

### Subnetting Details

The lab uses **Variable Length Subnet Masking (VLSM)** to efficiently allocate IP addresses to each VLAN. Ensure you understand the subnetting scheme and the IP ranges assigned to each VLAN.

### Learning Outcomes

By completing this lab, you will be able to:
- Configure VLANs on Cisco switches.
- Implement Inter-VLAN routing using a single router interface (Router-on-a-stick).
- Apply subnetting techniques using VLSM.
- Troubleshoot VLAN and inter-VLAN communication issues.
