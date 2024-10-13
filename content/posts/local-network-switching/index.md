---
title: "Local Network Switching - Final Project"
draft: false
date: 2024-05-25
description: "A packet tracer project that puts the following concepts into practice: VLANs, EtherChannel, redundancy, subnetting, STP and PVST."
summary: "This was my final project of the local network switching class, it is a document about the implementation of all the topics seen during the semester."
---

## Topology

### In packet tracer 

{{< figure
    src="resources/topology-PT.svg"
    alt="Image of the topology in packet tracer"
    nozoom=true
>}}

### In a real enviorment

{{< figure
    src="resources/topology-real.svg"
    alt="Image of the topology in a real-world example"
    nozoom=true
>}}

## 1. Network redundancy

In the proposed topology each outgoing switch of each department has two outputs, the main switch and the backup switch so we would have an STP with the root on the main switch and the secondary root on the backup switch, so if it fails they could simply send their packets through the secondary without any problem.

| Department     | Number of LAN switch ports    |
|--------------- | ----------------------------- |
| Sales         | 12                            |
| Engineering 2.1 | 48                            |
| Engineering 2.2 | 12                            |
| Administration | 24                            |
| Marketing      | 48                            |

## 2. Configuration of each LAN switch

| Switch | Configuration                                    |
|--------|--------------------------------------------------|
| 1      | - vlan 10                                        |
|        | - name sales                                    |
|        | - (Inside each interface towards a computer)     |
|        |   - switchport mode access                       |
|        |   - switchport access vlan 10                    |
| 2.1    | - vlan 20                                        |
|        | - name engineering                                |
|        | - (Inside each interface towards a computer)     |
|        |   - switchport mode access                       |
|        |   - switchport access vlan 20                    |
| 2.2    | - vlan 20                                        |
|        | - name engineering                                |
|        | - (Inside each interface towards a computer)     |
|        |   - switchport mode access                       |
|        |   - switchport access vlan 20                    |
| 3      | - vlan 30                                        |
|        | - name administration                            |
|        | - (Inside each interface towards a computer)     |
|        |   - switchport mode access                       |
|        |   - switchport access vlan 30                    |
| 4      | - vlan 40                                        |
|        | - name marketing                                 |
|        | - (Inside each interface towards a computer)     |
|        |   - switchport mode access                       |
|        |   - switchport access vlan 40                    |

## 3. Router to the Internet

{{< figure
    src="resources/router-internet.svg"
    alt="Image of the topology in a real-world example"
    nozoom=true
    class="mx-auto"
>}}

In this case we have the “Main” and “Backup” switches so they will do the inter-VLAN routing so we don't need to have something like a Router-On-A-Stick to do the VLAN routing.

## 4. EtherChannel

It is possible to add an EtherChannel in any of the switches, a practical example would be in the case that for example, engineering grows and now needs much more bandwidth or something like that, here is a generic example of the configuration to make an EtherChannel between two switches:

_In the switch1_
```
interface range GigabitEthernet1/0/1 - 2
  description Link_to_switch2_Switch
  switchport mode trunk  
  channel-group 1 mode active
  channel-protocol lacp
```

_In the switch2_
```
interface range GigabitEthernet1/0/1 - 2
  description Link_to_switch1_Switch
  switchport mode trunk  
  channel-group 1 mode active
  channel-protocol lacp
```

Once configured, EtherChannel will group the selected ports on both switches into a single logical “channel”.
This means that the combined bandwidth of the physical links will be used to carry traffic between switch1 and switch2. If one of the physical links fails, traffic is automatically rerouted over the other link without manual intervention, maintaining connectivity and performance.

Implementing EtherChannel will significantly improve network performance between these two critical departments and help to efficiently handle large volumes of traffic, while also ensuring higher availability and redundancy.

## 5. IP addressing scheme

There will be 4 VLANS:
  - Sales: 10 users
  - Administration: 20 users 
  - Marketing: 35 users
  - Engineering: 50 users


| Department     | Range of useful IPs                | VLAN number |
| -------------- | ---------------------------------- | ----------- |
| Sales         | 192.168.10.0 - 192.168.10.30       | 10          |
| Engineering     | 192.168.10.128 - 192.168.10.190    | 20          |
| Administration | 192.168.10.32 - 192.168.10.62      | 30          |
| Marketing      | 192.168.10.64 - 192.168.10.126     | 40          |

## 6. Gateway and PC masks for each department 


| Department     |  Gateway      | Mask           |
| -------------- | ------------- | ----------------- |
| Sales         | 192.168.10.1  | 255.255.255.224   |
| Engineering     | 192.168.10.129| 255.255.255.192   |
| Administration | 192.168.10.33 | 255.255.255.224   |
| Marketing      | 192.168.10.65 | 255.255.255.192   |

## 7. LAN switches main switch

The idea in this topology is that the main switch is the one called “Main”, the command used to see if the switch is the main switch or not is:

```
# show spanning-tree
```

Once this command is executed it will give you an output like this:

```
Switch#show spanning-tree
VLAN0001
  Spanning tree enabled protocol ieee
  Root ID    Priority    32769
             Address     0002.1770.0A10
             This bridge is the root
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32769  (priority 32768 sys-id-ext 1)
             Address     0002.1770.0A10
             Hello Time  2 sec  Max Age 20 sec  Forward Delay 15 sec
             Aging Time  20

Interface   Role Sts Cost      Prio.Nbr Type
----------- ---- --- --------- -------- ----
Fa0/2       Desg FWD 19        128.2    P2p
Fa0/5       Desg FWD 19        128.5    P2p
Fa0/1       Desg FWD 19        128.1    P2p
```

Where you can see in the third line of the “Root ID” section that this is the “Bridge root” or the main root switch.

## 8. LAN switches secondary switch

In this case, as the name indicates, the idea is that the router called “Backup” acts as the secondary. 

The command that would be used would be the same way the show spanning-tree and in the legend that says in the previous image “This bridge is the root” will say that it is the secondary. 

## 9. Separate STP by VLAN

Given the size of the network and the separation into several departments with different connectivity requirements, it would be possible to implement PVST+. Implementing it could improve operational efficiency by allowing different root paths for different VLANs, plus it is likely that it could increase overall network stability by pinpointing potential STP problems to individual VLANs, preventing a problem in one VLAN from affecting the entire network.

Implementing PVST+ can maximize the use of all available links and provide a better user experience by optimizing network traffic based on the specific needs of each department.

## 10. Recommended commands for STP security

_Inside each interface connected to a PC_

- **spanning-tree portfast**: this is not for security but it is highly recommended to use it on interfaces going to end devices like PCs.

- **spanning-tree bpduguard enable**: this command makes sure that if an interface put in portfast mode for a PC for example and then connects a device capable of sending BPDU packets such as a switch this BPDU packet does not break the spanning-tree, turning off the interface to achieve this. 
