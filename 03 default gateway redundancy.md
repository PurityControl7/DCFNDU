# Describing Layer 3 First-Hop Redundancy

*First Hop Redundancy Protocol (FHRP) is a general term for a networking protocol that protects the default gateway. It allows two or more routers or Layer 3 switches to provide a backup for that address. If one first-hop router fails, the backup router will, within a few seconds, by default take over the address.*

*You will learn about the challenges of first-hop redundancy and the solution using Hot Standby Router Protocol (HSRP), Virtual Router Redundancy Protocol (VRRP), and Gateway Load Balancing Protocol (GLBP) as Layer 3 redundancy protocols.*

## Default Gateway Redundancy

*Hosts in the network support one default gateway and a single path to that gateway. A device, usually a switch, is located between the host and the router, which supports multiple connections. The switch can connect over various paths to multiple routes that are in the same group. The first-hop redundancy protocol ensures that the default gateway address is the only address and that an active path to a router is available. You will learn about the challenges of default gateways in a redundant network and how default gateway redundancy operates.*

*In a network, each client receives only one default gateway. No means exist to configure a secondary gateway, even if a second route exists to carry packets off the local segment. The following two examples describe how redundant paths provide redundancy in networks.*

*For example, Router A is the primary default gateway for hosts in Subnet A, and for hosts in Subnet B the primary default gateway is Router B. If Router A becomes unavailable, the routing protocols can quickly and dynamically converge and determine that Router B can transfer packets that would otherwise have gone through Router A. Most workstations, servers, and printers, however, do not receive this dynamic routing information.*

![Default Gateway](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/default_gateway.png)

*End devices are typically configured with a single default gateway IP address that does not change when the network topology changes. If the router whose IP address is configured as the default gateway fails, the local device is unable to send packets off the local network segment. This situation effectively disconnects the router from the rest of the network. Even if a redundant router exists that could serve as a default gateway for that segment, these devices have no dynamic method by which to determine the address of a new default gateway.*

*Even though the example is explained on routers, in modern networks, these routers would be Layer 3 switches. These high-performance devices for routing (in contrast to routers) have many interfaces.*

## Default Gateway Redundancy Operation

*With the type of router redundancy that displays in the figure, a set of routers works together to present the illusion of a single router to the hosts on the LAN. By sharing an IP (Layer 3) address and a MAC (Layer 2) address, two or more routers can act as a single “virtual” router.*

![Virtual Router](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/virtual_router.png)

*The IP address of the virtual router is configured as the default gateway for the workstations on a particular IP segment. When frames transmit from the workstation to the default gateway, the workstation uses Address Resolution Protocol (ARP) to resolve the MAC address that associates with the IP address of the default gateway. The ARP resolution returns the MAC address of the virtual router. An active router or standby router that is part of that virtual router group can physically process frames that transmit to the MAC address of the virtual router.*

*Several redundancy protocols identify two or more routers as the devices that are responsible for processing frames that transmit to the MAC or IP address of the virtual router. Host devices send traffic to the address of the virtual router. The physical router that forwards this traffic is transparent to the end stations.*

![Virtual Router 2](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/virtual_router2.png)

*The redundancy protocol provides the mechanism for determining which router should take the active role in forwarding traffic and determining when a standby router must assume that role. The transition from one forwarding router to another forwarding router is transparent to end devices.*

*The following steps occur when a router fails:*

1. *The standby router stops seeing hello messages from the forwarding router.*

2. *The standby router assumes the role of the forwarding router.*

3. *Because the new forwarding router assumes the IP address and the MAC address of the virtual router, the end stations see no disruption in service.*

##  Hot Standby Router Protocol

*HSRP defines a standby group of routers, with one router designated as the active router. HSRP provides gateway redundancy by sharing IP and MAC addresses between redundant gateways. The protocol consists of virtual MAC and IP addresses that are shared between two routers that belong to the same HSRP group. You will learn how HSRP operates with active and standby routers and how HSRP improves network performance with interface tracking and load balancing.*

![HSRP](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/hsrp.png)

*The main characteristics of HSRP are the following:*

- *HSRP defines a group of routers: one active and one standby, as shown in the figure.*

- *Virtual IP and MAC addresses are shared between the two routers.*

- *HSRP is proprietary to Cisco, and VRRP is a standard protocol.*

![HSRP 2](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/hsrp2.png)

*In an HSRP group, there are two types of routers:*

***Active router:***

- *Responds to default gateway ARP requests with the virtual router MAC address.*

- *Assumes active forwarding of packets for the virtual router.*

- *Sends hello messages.*

- *Knows the virtual router IP address.*

***Standby router:***

- *Listens for periodic hello messages.*

- *Assumes active forwarding of packets if it does not hear from the active router.*

## HSRP Interface Tracking

*Interface tracking lets you adjust the priority of a standby group router, based on the availability of the router interfaces. When a tracked interface becomes unavailable, the HSRP tracking feature ensures that a router with an unavailable key interface relinquishes the active router role.*

*The HSRP group tracks the uplink interfaces. If the uplink on the right switch fails, the router decrements the priority on that interface and sends hello messages with the decremented priority.*

![Tracked Interfaces](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/tracked_interfaces.png)

*In the example in the figure, assume that the router on the right is configured with a higher priority, so it is processing the traffic toward the core. When the tracked interface through the router on the right fails, the host cannot reach the core network. HSRP makes the router on the left the active router.*

## HSRP Load Balancing

*HSRP is often used to improve resiliency in networks, but this approach can cause a decrease in network efficiency.*

*When the hosts must send packets to the core network, they send them to the host default gateway or to the router that is active in the HSRP group. Because only one router is active, packets from the hosts to the servers traverse only one of the two available paths.*

*To use the two paths from the host network to the server network, you can configure the Multigroup Hot Standby Router Protocol (MHSRP) between two routers. In the figure, R1 is configured with two HSRP groups (for example, group 10 and group 20) and R2 is also configured with the same HSRP groups. For group 10, R1 is the active router and R2 is the standby router. For group 20, R2 is the active router and R1 is the standby router. You would next configure half of the host default gateways with the HSRP group 10 virtual IP address and configure the other half of the host default gateways with the HSRP group 20 virtual IP address.*

![MHSRP](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/MHSRP.png)

*This feature inherently provides some improvement in overall networking resilience by providing load-balancing and redundancy capabilities between subnets and VLANs.*

## HSRP Versions

![HSRP Versions](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/hsrp_versions.png)

*Cisco Nexus Operating System (NX-OS) supports HSRP version 1 by default. You can configure an interface to use HSRP version 2.*

*With HSRP version 2, you gain the following enhancements:*

- ***Expanded group number range:*** *HSRP version 1 supports group numbers from 0 to 255. HSRP version 2 supports group numbers from 0 to 4095.*

- ***Use of the new IP multicast address:*** *The new IP multicast address 224.0.0.102 can send hello packets instead of the multicast address of 224.0.0.2, which is used by HSRP version 1.*

- ***Use of the MAC address range:*** *The MAC address range of 0000.0C9F.F000 to 0000.0C9F.FFFF is available. HSRP version 1 uses the MAC address range of 0000.0C07.AC00 to 0000.0C07.ACFF.*

- ***MD5 authentication is supported:*** *Message Digest 5 (MD5) authentication protects against HSRP-spoofing software and uses the industry-standard MD5 algorithm for improved reliability and security.*

## HSRP Configuration

![HSRP Configuration](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/hsrp_configuration.png)

*The brief sequence of steps to configure the HSRP is as follows. First, you must globally enable the HSRP feature before you can configure HSRP groups. Next, you configure an HSRP group on an interface and configure the virtual IP address, virtual MAC address, and the version for the HSRP group. You can configure the HSRP priority on an interface. HSRP uses the priority to determine which HSRP group member acts as the active router.*

*Optionally, you can configure the HSRP group to adjust its priority based on the availability of an interface. The priority of a device can change dynamically if it was configured for object tracking and the object that is tracked goes down. The tracking process periodically polls the tracked objects and notes a value change. The value change triggers HSRP to recalculate the priority. The HSRP interface with the higher priority becomes the active router if you configure the HSRP interface for pre-emption.*

## Lab: Configure HSRP Between the Peer Cisco Nexus 9000 Series Switches N9K-C and N9K-D

High availability in a data center always comes at a price: more links, more devices… and more ways for packets to get confused. End hosts only know a *single* default gateway, and that address never updates dynamically, even when the topology shifts. So when the physical device behind that gateway dies, your hosts basically sit there like abandoned ships in the fog.

HSRP solves this by giving you a **virtual default gateway**—an IP that never dies because multiple switches/routers stand behind it, taking turns as “active.”

In this lab, N9K-C and N9K-D will act as redundant Layer 3 gateways for VLAN 200 using HSRP group 10.

1. Prepare VLAN 200 on All Switches:

Enable VLAN 200 and assign it to interfaces Eth1/1–1/6 on all four Nexus switches.

```
N9K-A# configure
Enter configuration commands, one per line. End with CNTL/Z.
N9K-A(config)# vlan 200
N9K-A(config-vlan)# exit
N9K-A(config)# int eth 1/1-6
N9K-A(config-if-range)# switchport mode access
N9K-A(config-if-range)# switchport access vlan 200
N9K-A(config-if-range)# end
```

Repeat for N9K-B, N9K-C, N9K-D.

2. Create SVI for VLAN 200:

Enable the SVI feature and assign each switch its SVI IP (based on the provided job aid).

```
N9K-A# configure
Enter configuration commands, one per line. End with CNTL/Z.
N9K-A(config)# feature interface-vlan
N9K-A(config)# interface vlan 200
N9K-A(config-if)# ip address 172.16.200.21/24
N9K-A(config-if)# no shutdown
N9K-A(config-if)# end
```

Repeat for the other three switches with their respective IPs. Use ```show ip interface brief``` to confirm SVI state = up/up.

3. Verify Reachability:

From N9K-A and N9K-B, ping the VLAN 200 SVIs of N9K-C and N9K-D (172.16.200.11 and .12). First ping may fail due to ARP—normal behavior.

4. Enable the HSRP Feature (C & D Only):

```
N9K-C# configure
Enter configuration commands, one per line. End with CNTL/Z.
N9K-C(config)# feature hsrp
N9K-C(config)# end
```

Repeat on N9K-D.

5. Configure HSRP Group 10:

Virtual IP = 172.16.200.100

N9K-C should *preempt* (take back active role after it recovers).

```
N9K-C# configure
Enter configuration commands, one per line. End with CNTL/Z.
N9K-C(config)# interface vlan 200
N9K-C(config-if)# hsrp 10
N9K-C(config-if-hsrp)# ip 172.16.200.100
N9K-C(config-if-hsrp)# preempt
```

and...

```
N9K-D# configure
Enter configuration commands, one per line. End with CNTL/Z.
N9K-D(config)# interface vlan 200
N9K-D(config-if)# hsrp 10
N9K-D(config-if-hsrp)# ip 172.16.200.100
```

*Note:* ```preempt delay minimum <sec>``` exists if you want a graceful takeover. Default delay = 10 seconds.

6. Initial HSRP State Check:

Use:

```
show hsrp brief
```

Expected initial behavior:

- N9K-C → Active

- N9K-D → Standby

Why? Their priorities are equal (default 100), so the switch with the *higher SVI IP* wins. My materials confirm this exact behavior.

7. Assign a Manual Priority to Control Roles:

Give N9K-D a higher priority (example: 120):

```
N9K-D(config)# interface vlan 200
N9K-D(config-if)# hsrp 10
N9K-D(config-if-hsrp)# priority 120
```

Result: Active will NOT change yet. HSRP does *not* switch active routers automatically based on priority unless **preempt** is enabled.

8. Enable Preemption on N9K-D:

This allows N9K-D to take over if it has the higher priority.

```
N9K-D(config-if-hsrp)# preempt
```

Wait ~10 seconds and run:

```
show hsrp brief
```

Now N9K-D becomes *Active*, C becomes *Standby*.

9. Verify Virtual Gateway Reachability:

From N9K-A and N9K-B:

```
ping 172.16.200.100
```

The VIP should respond regardless of which switch is active.

10. Test Failover:

Shut VLAN 200 on N9K-D (currently active):

```
N9K-D(config)# interface vlan 200
N9K-D(config-if)# shutdown
```

Check:

```
show hsrp brief
```

N9K-C should take over as *Active*.

Bring VLAN 200 back up:

```
N9K-D(config-if)# no shutdown
```

Wait 10 seconds. Because N9K-D has higher priority *and* preempt enabled, it becomes Active again.

Final test: ping the VIP from A/B once more.

**Additional Notes:** Why HSRP sees Nexus switches as “routers”?

HSRP is a *Layer 3 first-hop redundancy protocol.* If a device has an SVI with an IP address, it is effectively performing L3 routing. Therefore: *HSRP = router mode*, even if the box is branded a switch.

To summarize:

- VIP never dies

- Whoever is Active = gateway

- Priority decides the boss

- Preempt decides if the boss wants its throne back

## Virtual Router Redundancy Protocol

*VRRP is an open protocol that defines a group of routers with a single virtual IP address and ensures first-hop redundancy. VRRP chooses one router as the primary router, and other routers in the group act as backup routers if the primary router fails. You will learn the VRRP operation, the similarities and differences compared to the Cisco proprietary HSRP, and how to configure and verify VRRP operation on Cisco Nexus switches.*

*The main benefits of VRRP are the following:*

- *Multiple routers that are configured as the default gateway ensure redundancy.*

- *Multiple VRRP groups enable load sharing.*

- *Pre-emption is enabled by default.*

- *The advertisement protocol uses a standard multicast address.*

- *The VRRP interface and object tracking ensure that the best VRRP router is the primary.*

- *VRRP supports virtual routing and forwarding (VRF).*

*In the figure, you see a network with routers and clients, where routers A, B, and C form a VRRP group. VRRP allows the routers to share the same virtual IP address, and the clients have the same statically defined default gateway. The virtual IP address of the virtual router is the same as the IP address that is defined on the Ethernet interface of Router A. Router A is the primary router of the VRRP group and forwards the traffic that transmits to the virtual IP address.*

![VRRP](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vrrp.png)

*Routers B and C act as backups if Router A becomes unavailable. The router with the highest priority becomes the primary router until Router A recovers and assumes the role as the primary router in the VRRP group. The primary router sends VRRP advertisements that contain its priority and state to other routers in the same VRRP group. By default, advertisements transmit every second to the standard multicast IP 224.0.0.18 for VRRP advertisements.*

## VRRP Load Balancing

*A single physical interface supports up to 255 VRRP groups (the number of groups may vary depending on the router processing and memory capabilities). This figure displays a network with two routers with two VRRP groups. Each router acts as the primary router for one VRRP group and as the backup for the other group. This configuration enables load sharing between two routers.*

![VRRP Load Balancing](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vrrp2.png)

*The VRRP group with the virtual IP 10.0.0.1 is the default gateway for Clients 1 and 2. The VRRP group with the virtual IP 10.0.0.2 is the default gateway for Clients 3 and 4. Load balancing is achieved through manual configuration. If Router A fails, Router B takes the role of the primary router and forwards the traffic from all the clients until Router A becomes available again.*

## VRRP Tracking and Priority

*VRRP tracks the state of an interface and of an object. Tracking determines the priority of the router in a VRRP group to choose the primary router of the VRRP group. The functions of the router in a VRRP group are defined with the priority. The priority of the primary router is 255, and the priorities of the backups are lower. In the figure, Router A is the primary router, and its priority is 255. When Router A fails, the backup router with the highest priority assumes the role of the active router. In the example, Routers B and C have the same default priority of 100. VRRP chooses Router C as the primary router because of the higher-configured IP address.*

![VRRP Tracking](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vrrp3.png)

*By default, pre-emption is enabled. When a failed router comes back online and has a higher priority than the current primary router, it assumes the role of the primary router. When you disable pre-emption, the change from the current primary router to the router with the higher priority that came back online happens only when the current primary router fails.*

## Comparison of VRRP and HSRP

*You will now examine the differences and similarities between VRRP and HSRP.*

![VRRP vs HSRP](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vrrp4.png)

## VRRP Configuration

*To configure VRRP, you must follow these steps. First, you must globally enable the VRRP feature before you can configure VRRP groups. Next, you configure a VRRP group on an interface and configure the virtual IP address. This address should be in the same subnet as the IPv4 address of the interface. You can configure the VRRP priority on an interface. VRRP uses the priority to determine which VRRP group member acts as the active router. The priority range for a virtual router is from 1 to 254 (1 is the lowest priority and 254 is the highest). The default is 100 for backups and 255 for a primary router that has an interface IP address equal to the virtual IP address. You can also configure simple text authentication for a VRRP group.*

![VRRP Configuration](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vrrp5.png)

*Optionally, you can configure a VRRP group to adjust its priority based on the availability of an interface. The priority of a device can change dynamically if you configured it for object tracking and the object that is being tracked goes down. The tracking process periodically polls the tracked objects and notes a value change. The value change triggers VRRP to recalculate the priority. The VRRP interface with the higher priority becomes the active router if you configure the VRRP interface for pre-emption.*

## Gateway Load Balancing Protocol

*GLBP provides gateway resiliency and simultaneously allows full use of resources on all devices in a group. You will now learn the characteristics of GLBP, how it works, and how it differs from HSRP and VRRP.*

*The main benefits of GLBP are the following:*

- *The main benefits of GLBP are the following:*

- *A single virtual IP address and multiple virtual MAC addresses are provided.*

- *Traffic routes to a single gateway distributed across routers.*

- *Automatic rerouting is provided if a failure occurs.*

*Although HSRP and VRRP provide gateway resiliency, for the standby members of the redundancy group, the upstream bandwidth is not used while the device is in standby mode.*

*Only the active router in HSRP and VRRP groups forwards traffic for the virtual MAC address. Resources that associate with the standby router are not fully used. You can accomplish some load balancing with these protocols by creating multiple groups and assigning multiple default gateways, but this configuration creates an administrative burden.*

*GLBP is a proprietary solution from Cisco that allows automatic choice and simultaneous use of multiple available gateways, in addition to automatic failover between those gateways. Multiple routers share the load of frames that, from a client perspective, transmit to a single default gateway address.*

*With GLBP, you can fully use resources without the administrative burden of configuring multiple groups and managing multiple default gateway configurations.*

![GLBP](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/glbp.png)

## GLBP Active Virtual Gateway

*Members of a GLBP group elect one gateway to be the active virtual gateway (AVG) for that group. Other group members provide backup for the AVG if that AVG becomes unavailable. The AVG assigns a virtual MAC address to each member of the GLBP group. Each gateway assumes responsibility for forwarding packets that transmit to the virtual MAC address assigned to it by the AVG. This type of gateway is known as an active virtual forwarder (AVF) for the virtual MAC address.*

*As you can see in the figure, the AVG is responsible for answering ARP requests for the virtual IP address. Load sharing is achieved by the AVG replying to the ARP requests with various virtual MAC addresses.*

![GLBP AVG](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/glbp2.png)

*In this scenario, R1 is the AVG for a GLBP group and is responsible for the virtual IP (VIP in the figure) address 10.88.1.10. R1 is also an AVF for the virtual MAC address 0000.0000.000.1. R2 is a member of the same GLBP group and is designated as the AVF for the virtual MAC address 0000.0000.0002. Client A has a default gateway IP address of 10.88.1.10 and a gateway MAC address of 0000.0000.0001. Client B shares the same default gateway IP address but receives the gateway MAC address 0000.0000.0002 because R2 is sharing the traffic load with R1.*

![GLBP AVG2](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/glbp3.png)

*If R1 becomes unavailable, Client A will not lose access. R2 will assume responsibility for forwarding packets that transmit to the virtual MAC address of R1 and for responding to packets sent to its own virtual MAC address. R2 will also assume the role of the AVG for the entire GLBP group. Communication for the GLBP members continues despite the failure of a router in the GLBP group.*

## GLBP Interface Tracking

*GLBP weighting determines if a router can act as a virtual forwarder. You can set initial weighting values and specify optional thresholds. You can track interface states and set a decrement value to reduce the weighting value if the interface goes down. When the GLBP router weighting drops to less than a specified value, the router will no longer be an AVF. When the weighting exceeds a specified value, the router can resume its role as an active virtual forwarder.*

![GLBP Weighting](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/glbp4.png)

*You can adjust the GLBP group weighting by tracking the state of an interface within the router. If a tracked interface goes down, the GLBP group weighting is reduced by a specified value. You can track various interfaces to decrement the GLBP weighting by varying amounts.*
