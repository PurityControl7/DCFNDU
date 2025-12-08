# Describing Port Channels and vPCs

*A port channel is a technology that enables packets to transmit over several physical interfaces as if the interfaces were a single interface. Port channel technology logically bonds several physical connections into one logical connection. The process offers redundancy and load balancing while maintaining the combined throughput of physical devices.*

*You can establish port channels over several physical links, such as Ethernet. The data plane of the receiving Cisco Nexus device treats packets that travel through physical links as coming through several links. The management plane treats the packets as a single data flow.*

## LAN Port Channels

*You can create LAN port channels between two devices that are connected by a physical Ethernet topology. It uses the same speed and feasible distance of the physical links that are logically bonded.*

*The figure shows a physical view and a logical view of the same system using the port channel configuration.*

![Port Channels](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/port_channels.png)

*To add resiliency against link failures and increase the available bandwidth between two devices, multiple physical links can be provisioned between the devices. However, without port channel technology, most control plane protocols, such as Layer 2 Spanning Tree Protocol (STP) or Layer 3 routing protocols, treat the multiple links as individual links. With STP, the result is blocked ports. Although the extra links add resiliency, the available bandwidth between the two devices does not increase.*

*A port channel bundles individual links into a channel group to create a single logical link (called a port channel) that provides the aggregate bandwidth of several physical links. Each link can be in only one port channel. All the links in a port channel must be compatible: they must use the same speed and operate in full-duplex mode.*

*You can use static port channels, with no associated control protocol, for a simplified configuration. For a more efficient use of the port channel, you can use the Link Aggregation Control Protocol (LACP), which is defined in IEEE 802.1ax and 802.1aq. With LACP, you can control link aggregation (for example, the maximum number of bundled ports that is allowed). LACP is also superior to static port channels with failover detection.*

*Note: Cisco Nexus Operating System (NX-OS) does not support Port Aggregation Protocol (PAgP) for port channels.*

## LAN Port Channel Modes

*Several port channel modes are available that you must configure to correspond between devices. Some combinations of port modes are supported; other combinations are not supported.*

![Port Channels 2](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/port_channels2.png)

*The following table lists the channel modes.*

![Port Channel Modes](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/port_channels3.png)

*The passive and active modes allow LACP to negotiate between ports to determine if the ports can form a port channel. The criteria are based on the port speed and the trunking state. Passive mode is useful when you do not know if the remote system (or partner) supports LACP.*

*Note: You must enable the LACP feature before you can configure and use LACP functions.*

## Port Channel Mode Compatibility

*Ports can form an LACP port channel when the ports are in differing but compatible LACP modes, as shown in the table.*

![Port Channel Compatibility](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/port_channels4.png)

*Port channel configurations that are invalid do not result in the creation of a port channel. The ports in a port channel are operational when the port status is channeling.*

## Port Channel Load Balancing

*Because a port channel uses several links to transport packets through physical infrastructure, the packets must be distributed between the physical links through load balancing.*

*Cisco Nexus Series Switches support the bundling of up to 16 ports into a port channel.*

*The Cisco Nexus Series Switch load-balances all traffic that is switched or routed to a port channel interface across all operational individual physical links. It hashes the various header fields in a frame into a numerical value that chooses one of the links in the channel. Load balancing is performed in the hardware and is enabled by default. You can apply the load-balancing method to all port channels on a specified module. If you configure a per-module load-balancing method, this configuration has precedence over the switchwide setting.*

*You can configure the switch to use one of the following load-balancing methods:*

- *Destination MAC address*

- *Source MAC address*

- *Source and destination MAC addresses*

- *Destination IP address*

- *Source IP address*

- *Source and destination IP addresses*

- *Source TCP or UDP port number*

- *Destination TCP or UDP port number*

- *Source and destination TCP or UDP port numbers*

*Note: One goal of load balancing is to use all available links. The other is to ensure that packets with the same header are forwarded on the same physical link to prevent packet reordering.*

## Port Channel Layer 2 and Layer 3 Interfaces

*A port channel configuration can run on Open Systems Interconnection (OSI) Layer 2 or Layer 3. The administrator can choose the interface classification.*

*The figure shows you the difference between a Layer 2 and Layer 3 port channel configuration.*

![Port Channel Differences](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/port_channels5.png)

*You can classify port channel interfaces as Layer 2 or Layer 3 interfaces. You can also configure Layer 2 port channels in access mode or trunk mode. Layer 3 port channel interfaces have routed ports as channel members and may have subinterfaces.*

*You can configure a Layer 3 port channel with a static MAC address. If you do not configure this value, the Layer 3 port channel uses the router MAC of the first channel member to become active.*

## Virtual Port Channels

*The biggest limitation of classic port channel technology is that the port channel operates only between two devices. In large networks, the support of multiple devices in combination is often necessary to provide some form of hardware failure alternate path. This alternate path is often connected in a way that would cause a loop, limiting the benefits that are gained with port channel technology to a single path.*

*To address this limitation, Cisco NX-OS provides a technology that is called virtual port channel (vPC). A pair of switches acting as a vPC peer endpoint appears as a single logical entity to the port channel-attached devices. However, the two devices that act as one logical port channel endpoint are still two distinct devices.*

## vPC Topology Implementations

![vPC Implementations](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vpc.png)

*The vPC solution combines the benefits of hardware redundancy with the benefits of port channel loop management. As you can see from the figure, the three main use cases for vPC technology are as follows:*

***Dual-uplink Layer 2 access (A):*** *In this scenario, an access switch such as a Cisco Nexus 9000 Series switch is dual-homed to a pair of distribution switches, such as Cisco Nexus 9500 Series switches.*

***Server dual-homing (B):*** *In this case, a server is connected via two interfaces to two access switches.*

*You can use vPC in several topologies that allow for various redundancy and data transit options.*

## Cisco UCS Fabric Interconnects with vPC Topologies

*In Cisco Unified Computing System (Cisco UCS), vPCs are not supported on the fabric interconnects themselves. Fabric interconnects do not share a data or control plane. However, the upstream LAN switches to which the fabric interconnects connect can be a vPC, as shown in the figure. When a vPC is available upstream, you can use the fabric interconnect end-host mode (EHM) or fabric interconnect switching mode.*

![UCS Fabric Interconnects](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/ucs_fabrics_vpc.png)

## STP with and Without vPC

*vPC and STP can provide loop-prevention mechanisms. STP allows only a single path to a destination; vPC can use redundant connections. Failed links are also resolved much faster with vPC.*

*In early Layer 2 Ethernet network environments, it was necessary to develop protocol and control mechanisms that limited the disastrous effects of a topology loop in the network. STP was the primary solution to this problem because it provided loop detection and loop management for Layer 2 Ethernet networks.*

*This protocol underwent several enhancements and extensions. While STP scales to very large network environments, it still has one suboptimal principle: To break the loops in a network, only one active path is allowed from one device to another. This principle is true regardless of how many connections might exist in the network.*

*The figure shows you how vPC resolves loops in an environment.*

![vPC Loops](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vpc_loops.png)

*An environment without a vPC has the following characteristics:*

- *STP blocks redundant uplinks.*

- *Load balancing is virtual LAN (VLAN)–based.*

- *Loop resolution relies on STP.*

- *Protocol failure can cause a complete network failure.*

*An environment with a vPC has the following characteristics:*

- *No blocked uplinks*

- *Lower oversubscription*

- *Hash-based EtherChannel load balancing*

- *Loop-free topology*

*The other main benefit of migration to an entirely port channel–based loop-management mechanism is that link recovery is potentially much faster. STP can recover from a link failure in approximately 6 seconds, while an entirely port channel–based solution has the potential for failure recovery in less than 1 second.*

## vPC Components and Architecture

*The vPC topology can accommodate several types of infrastructures and uses particular technologies and naming conventions for its parts.*

*You can see the various components of a vPC topology in the figure.*

![vPC Components](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vpc_components.png)

*A pair of Cisco Nexus switches that use a vPC appear to other network devices as a single logical Layer 2 switch. However, the two switches remain two separately managed switches with independent management and control planes. The vPC architecture includes modifications to the data plane of the switches to ensure optimal packet forwarding. The vPC architecture also includes control plane components to exchange state information between the switches. It allows the two switches to appear as a single logical Layer 2 switch to the downstream devices.*

*The vPC architecture consists of the following components:*

- ***vPC peers:*** *The core of the vPC architecture is a pair of Cisco Nexus switches. This pair of switches acts as a single logical switch, which allows other devices to connect to the two switches.*

- ***vPC peer link:*** *The vPC peer link is the most important connectivity element in the vPC system. This link creates the illusion of a single control plane by forwarding bridge protocol data units (BPDU)s and LACP packets to the primary vPC switch from the secondary vPC switch. The peer link is also used to synchronize MAC address tables between the vPC peers and to synchronize IGMP entries for IGMP snooping. The peer link provides the necessary transport for multicast traffic and for the traffic of orphaned ports. If a vPC device is also a Layer 3 switch, the peer link also carries Hot Standby Router Protocol (HSRP) packets.*

- ***Cisco Fabric Services:*** *The Cisco Fabric Services (CFS in the figure) protocol is a reliable messaging protocol that supports rapid stateful configuration message passing and synchronization. The vPC peers use Cisco Fabric Services to synchronize data plane information and implement the necessary configuration checks. vPC peers must synchronize the Layer 2 Forwarding table between the vPC peers. Thus, if one vPC peer learns a new MAC address, that MAC address is also programmed on the Layer 2 Forwarding table of the other peer device.*

*Cisco Fabric Services travels on the peer link and does not require a user configuration. To help ensure that the peer link communication for Cisco Fabric Services is available, the spanning tree is modified to keep the peer-link ports continually forwarding. Cisco Fabric Services also performs compatibility checks for these purposes:*

- *Validate the compatibility of vPC member ports to form the channel.*

- *Synchronize the IGMP snooping status.*

- *Monitor the status of the vPC member ports.*

- *Synchronize the ARP table.*

**Additional Notes:** IGMP (Internet Group Management Protocol) snooping is a network switch feature that listens to IGMP traffic between hosts and routers. It helps manage multicast traffic by ensuring that multicast packets are only sent to ports that have requested them. This reduces unnecessary bandwidth usage and improves network efficiency.

Benefits of IGMP Snooping:

- Bandwidth Conservation: By filtering multicast traffic, IGMP snooping prevents flooding of unnecessary data to all ports in a VLAN.

- Improved Performance: It enhances multicast performance by reducing false flooding, which can occur if IGMP snooping is disabled.

- Dynamic Membership Management: It tracks which ports are connected to multicast-capable routers, allowing for efficient multicast forwarding.

*(...continuation of vPC architecture...)*

- ***vPC peer keepalive link:*** *The peer keepalive link is a logical link that often runs over an out-of-band (OOB) network. The peer keepalive link provides a Layer 3 communications path that is used as a secondary test to determine if the remote peer is operating properly. No data or synchronization traffic transmits over the vPC peer keepalive link. Only IP packets transmit to indicate that the originating switch is operating and running a vPC. The peer keepalive status determines the status of the vPC peer when the vPC peer link goes down. In this scenario, the status helps the vPC switch to determine if the peer link itself failed or if the vPC peer failed entirely.*

- ***vPC:*** *A vPC is a Multichassis EtherChannel (MEC), which is a Layer 2 port channel that spans the two vPC peer switches. The downstream device that connects on the vPC sees the vPC peer switches as a single logical switch. The downstream device does not need to support the vPC itself. The downstream device uses a regular port channel to connect to the vPC peer switches, which you can statically configure or negotiate through LACP.*

- ***vPC domain:*** *The vPC domain includes the two vPC peer devices, vPC peer keepalive link, vPC peer link, and all port channels in the vPC domain that connect to the downstream devices. A numerical vPC domain ID identifies the vPC. You can have only one vPC domain ID on each device.*

- ***vPC member port:*** *The vPC member port is a port on one of the vPC peers that is a member of one of the vPCs configured on the vPC peers.*

- ***Orphan device:*** *An orphan device connects to a vPC domain using regular links instead of connecting through a vPC.*

- ***Orphan port:*** *An orphan port is a switch port that connects to an orphan device. The term is also used for vPC port members that connect to a single vPC peer. This situation can occur if a device that connects to a vPC loses all its connections to one of the vPC peers.*

## vPC Control Plane

*A vPC uses the Cisco Fabric Services protocol in the control plane to construct a vPC between peers and allow communication between the primary and secondary vPC devices.*

*The figure shows a primary device, a secondary device, and the Cisco Fabric Services protocol functionality. The two devices act as a single entity toward their client.*

![vPC Control Plane](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vpc_control_plane.png)

*Cisco Fabric Services (CFS in the figure) acts as the primary control plane protocol for vPC and performs several functions:*

- *vPC peers must synchronize the Layer 2 MAC address table between the vPC peers. If one vPC peer learns a new MAC address on a vPC, that MAC address is also programmed on the Layer 2 Forwarding table of the other peer device for that same vPC. This MAC address learning mechanism replaces the regular switch MAC address learning mechanism and prevents traffic from forwarding across the vPC peer link unnecessarily.*

- *Cisco Fabric Services performs the synchronization of Internet Group Management Protocol (IGMP) snooping information. Layer 2 Forwarding of multicast traffic with the vPC is based on modified IGMP snooping behavior that synchronizes the IGMP entries between the vPC peers. In a vPC implementation, IGMP traffic entering a vPC peer switch through a vPC triggers hardware programming for the multicast entry on the two vPC member devices.*

- *Cisco Fabric Services communicates essential configuration information to ensure configuration consistency between peer switches. Similar to regular port channels, vPCs are subject to consistency checks and compatibility checks. During a compatibility check, one vPC peer conveys configuration information to the other vPC peer to verify that vPC member ports can form a port channel. In addition to compatibility checks for the individual vPCs, Cisco Fabric Services also performs consistency checks for switchwide parameters that you must configure consistently on the two peer switches.*

- *Cisco Fabric Services can track vPC status on the peer. When all vPC member ports on one of the vPC peer switches go down, Cisco Fabric Services notifies the vPC peer switch that its ports are now orphan ports. Traffic that is received on the peer link for that vPC should now forward to the vPC.*

- *You may configure Layer 3 vPC peers to synchronize their respective ARP tables. This feature is disabled by default, and you can enable it by using the ```ip arp synchronize``` command. If enabled, this feature helps ensure faster convergence time on a vPC switch reload. When two switches reconnect after a failure, they use Cisco Fabric Services to perform bulk synchronization of the ARP table.*

*An election is held between the pair of vPC peer switches to determine a primary vPC device and secondary vPC device. This election is not preemptive. The vPC primary or secondary role is primarily a control plane role. It determines which of the two switches will primarily be responsible for the generation and processing of spanning-tree Bridge Protocol Data Units (BPDUs) for the vPCs.*

*Note: The vPC peer-switch option allows the primary and secondary devices to generate BPDUs for vPCs independently. The two switches use the same spanning-tree bridge ID to ensure that connected devices on a vPC still see the vPC peers as a single logical switch.*

*The two switches actively participate in traffic-forwarding for the vPCs. However, the primary and secondary roles are also important in certain failure scenarios, most notably in a peer-link failure. When the vPC peer link fails but the vPC peer switches determine through the peer keepalive mechanism that the peer switch is still operational, the operational secondary switch suspends all vPC member ports. The secondary role also shuts down all switch virtual interfaces (SVIs) associated with VLANs that you configure as allowed VLANs for the vPC peer link.*

*For LACP and STP, the two vPC peer switches appear as a single logical switch to devices connected on a vPC. For LACP, this result is accomplished by generating the LACP system ID from a reserved pool of MAC addresses, which combine with the vPC domain ID. For STP, the behavior depends on the use of the peer-switch option.*

*If you do not use the peer-switch option, the vPC primary is responsible for generating and processing BPDUs and uses its own bridge ID for the BPDUs. The secondary role relays BPDU messages but does not generate BPDUs itself for the vPCs. When you use the peer-switch option, the primary and secondary switches send and process BPDUs. However, they use the same bridge ID to appear as a single switch to devices connected on a vPC.*

## vPC Peer-Link Restrictions

*Although a vPC allows for a loop-free topology, usually you must follow certain restrictions to traffic passing the peer link. The most important forwarding rule for a vPC is that a frame that enters the vPC peer switch from the peer link cannot exit the switch from a vPC member port.*

*The figure shows the allowed and disallowed traffic options.*

![vPC Peer-Link Restrictions](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vpc_link_restrictions.png)

*As you see in the figure, Switch3 and Switch4 connect to 9k01 and 9k02 with vPC port channels Po51 and Po52. If one of the hosts that is connected to Switch4 sends an unknown unicast or a broadcast, this traffic may get hashed to port eth2/2 on Po52. 9k02 receives the broadcast and must forward it to the peer link for the potential orphan ports on 9k01 to receive it.*

*Upon receiving the broadcast, 9k01 in the figure detects that this frame is coming from the vPC peer link. Therefore, it does not forward it to port 2/9 or 2/10; if it did, a duplicate frame on Switch3 or Switch4, respectively, would be created.*

*If a host on Switch4 sends a broadcast, 9k02 will correctly forward it to Po51 on port 2/9 and place it on the peer link. 9k01 will prevent this broadcast frame from exiting to port 2/9 or 2/10 because this frame entered 9k01 from a vPC peer link. If eth2/2 on Switch3 goes down, port 2/9 on 9k01 would become an orphan port, and as a result, will receive traffic that traverses the peer link. Therefore, the vPC peer link should consist of at least two dedicated 10 Gigabit Ethernet links. Cisco also recommends avoiding the use of orphan devices with a vPC, if possible. Traffic from orphan ports may need to be forwarded across the peer link and must be considered when scaling peer-link capacity. Also, orphan devices may experience traffic disruption in certain vPC failure scenarios.*

## vPC Data Plane Traffic Flow

*When communicating with external networks, the vPC domain prioritizes forwarding through local ports, except in certain situations when using the peer link between the vPC peers.*

*The figure shows a regular traffic path when communicating with external systems through a vPC domain.*

![vPC Data Plane Traffic Flow](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vpc_data_flow.png)

*Whenever a vPC peer switch must forward inbound traffic for a vPC, it forwards it to a local vPC port if possible. However, if the vPC peer switch has no active vPC member ports for the vPC, it forwards the traffic across the vPC peer link to the other vPC peer switch.*

*Aggregation switches using vPCs commonly use a First Hop Redundancy Protocol (FHRP) such as HSRP, Gateway Load Balancing Protocol (GLBP), or Virtual Router Redundancy Protocol (VRRP) for default gateway redundancy. The normal forwarding behavior of these protocols is enhanced with the peer-gateway feature to allow them to interoperate with vPCs.*

*Normally, only active FHRP routers forward traffic for the virtual default gateway MAC address. For vPCs, the forwarding rules are enhanced to allow a nonactive FHRP router to forward frames that are destined for the FHRP virtual MAC address. However, the primary FHRP device is still responsible for responding to ARP requests, even though the secondary FHRP device forwards the data traffic.*

## vPC Guidelines

*Consider these guidelines and limitations when deploying vPCs:*

- *You can deploy a vPC on a pair of Cisco Nexus 9200 Series switches or Cisco Nexus 9300 Series platform switches, but not on a combination of the two types of switches. A Cisco Nexus switch must pair with the same type of switch.*

- *A vPC peer link must consist of Ethernet ports with an interface speed of 10 Gbps or higher. Cisco recommends using at least two 10 Gigabit Ethernet ports in dedicated mode.*

- *A vPC keepalive must not run across a vPC peer link.*

- *You can configure only one vPC domain ID on a single switch. It is impossible for a switch to participate in more than one vPC domain.*

- *A vPC is a Layer 2 port channel. A vPC does not support the configuration of Layer 3 port channels. Beginning with Cisco NX-OS Release 7.0(3)I5(1), Layer 3 over vPC is supported on Cisco Nexus 9000 Series switches for Layer 3 unicast communication only.*

- *A vPC has support for static routing to FHRP addresses. The FHRP enhancements for vPCs enable routing to a virtual FHRP address across a vPC.*

- *You can use a vPC as a Layer 2 link to establish a routing adjacency between two external routers. The routing restrictions for vPCs apply only to routing adjacencies between the vPC peer switches and routers that connect on a vPC.*

## Lab: Configure vPCs

*Port Channels vs vPC (quick mental model):*

- **Port channel (LAG)** = multiple physical links bundled into *one logical interface* on a *single device.* STP and routing see it as one link.

- **vPC** = lets a downstream device build *one port channel* that physically connects to *two separate Nexus switches*, which pretend to be one logical switch.

Think of it this way:

- Port channel = “many cables, one switch.”

- vPC = “many cables, two switches, one illusion.”

In a vPC pair, both switches share a *single logical identity* toward downstream devices. But traffic can arrive on either switch. If traffic lands on the “wrong” peer (for example, the one whose uplink failed), it must cross over to the other switch — *that’s what the vPC peer-link is for.*

No peer-link = black holes, MAC confusion, tears.

### Verify Interswitch Connections

Before touching vPC config, we verify:

- Layer 3 connectivity between all N9Ks (the default VRF of each device)

- Layer 2 topology and cabling symmetry

If this foundation is shaky, vPC will absolutely punish you later.

Use plain ```ping``` — default VRF is assumed.

```
ping 172.16.200.11
ping 172.16.200.12
ping 172.16.200.22
```

- First ping may fail (ARP resolution, control-plane warm-up)

- Subsequent replies succeed

Overall, if all devices respond, Layer 3 underlay is good.

Verify Layer 2 topology with CDP. Run on *both vPC peer candidates (N9K-C and N9K-D):*

```
show cdp neighbors
```

What you’re checking:

- All expected neighbors appear

- *Multiple links between N9K-C ↔ N9K-D* (these will become:

1. vPC peer-link

2. possibly keepalive paths later)

- Downstream devices (servers, access switches) are dual-homed correctly

- Port numbering matches the lab diagram (this matters a lot later)

If link counts or neighbors don’t match — stop and fix cabling now.

**Key Takeaways:**

- Port channels simplify the control plane: STP + routing see *one link*

- vPC extends that illusion across *two physical switches*

- The *peer-link* is non-negotiable — it keeps traffic sane during failures

- Always verify **L3 first, L2 second** before configuring vPC

- CDP is your truth oracle: trust it more than memory

### Configure the vPC Peer Keepalive

The vPC peer-keepalive is a *logical, Layer 3 heartbeat* between vPC peers that answers one critical question when things go sideways: *did my peer die, or did just the peer-link die?*

If the peer-link drops, the keepalive decides whether to enter *dual-active protection* or not. This link does *not* carry data traffic—only lightweight IP-based keepalive messages—and it must *never traverse the vPC peer-link itself,* otherwise it becomes meaningless.

By default on Nexus switches, the peer-keepalive uses the *management VRF over ```mgmt0```*, but best practice (especially in real designs) is to isolate it in a *dedicated VRF on a dedicated routed interface.*

![vPC Keepalive](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vpc_keepalive.png)

**Additional Notes and Clarifications:**

- OOB = Out-Of-Band

This means management traffic that is *logically and physically separate* from production data paths. The ```mgmt0``` interface lives in its own universe for exactly this reason.

“Layer 3 cloud” in diagrams: This simply means *any IP-routable path.* It could be:

- a direct routed link between the two switches

- an upstream core/aggregation network

- or even a management network

The only rule: it must stay *independent* of the vPC peer-link.

Collapsed core / direct L3 connection? Yes. You can directly connect the aggregation switches with a routed port for keepalive as long as:

- it’s a separate interface (preferably on a different I/O module),

- placed in a *dedicated VRF,*

- and not bundled into the peer-link.

EtherChannel for keepalive? Technically possible, practically pointless. Keepalives are tiny and infrequent—using a port-channel buys you nothing and wastes ports. Single routed link wins.

Straight-through vs crossover cable? Modern Nexus ports auto-MDI/MDIX, so cable type doesn’t matter electrically. The warning in the labs is *topological*, not physical: *don’t directly cable ```mgmt0``` ports back-to-back*, because a supervisor switchover can kill the keepalive.

**Configuration: vPC Peer-Keepalive**

Goal: isolate keepalive traffic in its own VRF and routed interface

N9K-C:

```
configure
vrf context VPC-KEEPALIVE
interface ethernet 1/1
 no switchport
 vrf member VPC-KEEPALIVE
 ip address 209.165.200.225/24
 no shutdown
exit
```

N9K-D:

```
configure
vrf context VPC-KEEPALIVE
interface ethernet 1/1
 no switchport
 vrf member VPC-KEEPALIVE
 ip address 209.165.200.226/24
 no shutdown
exit
```

Even though Nexus ports default to Layer 3, explicitly using ```no switchport``` makes intent crystal clear and avoids ambiguity.

*Confirm interface status and VRF placement:*

```
show ip interface brief vrf VPC-KEEPALIVE
```

Test keepalive connectivity from N9K-C:

```
ping 209.165.200.226 vrf VPC-KEEPALIVE
```

Again, the first ping may fail due to ARP resolution—this is normal.

*Bottom line:* The peer-keepalive is not about bandwidth, it’s about truth. One clean, boring routed link in its own VRF is vastly superior to clever designs that accidentally depend on the very failure they’re meant to detect.

### Configure the vPC Domain

A vPC domain defines a pair of switches that operate as a single logical endpoint for downstream devices. Each domain supports *exactly two switches*, identified by a shared *domain ID (1–1000)*, and that ID is used to derive a *vPC system MAC address* used internally for vPC-related control protocols (most notably LACP).

Even though the vPC system MAC is link-scoped, Cisco strongly recommends that *each Layer 2 domain uses a unique vPC domain ID* to avoid ambiguity and weirdness during migrations or failures. You can statically configure the MAC, but letting NX-OS auto-derive it is usually safer and cleaner.

![vPC Domain](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vpc_domain.png)

**Enabling vPC (Mandatory First Step):**

Attempting to configure a vPC domain before enabling the feature fails—because NX-OS is strict and unforgiving (as it should be).

```
feature vpc
```

This must be done on both N9K-C and N9K-D.

**Configuring vPC Domain ID 10:**

```
vpc domain 10
```

After this, checking the role immediately shows that *no role is established yet*, because the switches cannot negotiate until the *peer-link exists.*

Key observations from ```show vpc role``` at this stage:

- vPC role: *none established*

- vPC system MAC: *00:00:00:00:00:00*

- Peer system MAC: *unknown*

- This is *expected and correct*

*Current vPC State (Before Peer-Link):*

Running ```show vpc``` now tells a very honest story:

- Peer link: *not configured*

- Keepalive: *disabled*

- Consistency checks: *failed*

- vPC role: *none established*

This is not an error state — it’s simply *an incomplete system.*

**Binding the Peer-Keepalive to the vPC Domain:**

Now we glue the L3 keepalive you already built into the vPC control plane:

N9K-C:

```
vpc domain 10
 peer-keepalive destination 209.165.200.226 source 209.165.200.225 vrf VPC-KEEPALIVE
```

N9K-D:

```
vpc domain 10
 peer-keepalive destination 209.165.200.225 source 209.165.200.226 vrf VPC-KEEPALIVE
```

This explicitly tells vPC:

- *where* to send keepalives,

- *which VRF* to use,

- and *which interface* is implicitly responsible.

**Verifying Peer-Keepalive Health:**

```show vpc peer-keepalive``` now confirms:

- peer is alive

- packets are flowing both ways

- traffic is confined to ```Eth1/1``` in ```VPC-KEEPALIVE```

Timers (1s interval, 5s timeout) are deliberately aggressive—vPC wants fast truth, not politeness.

### Configure a Port Channel Between Cisco Nexus 9000 Series Switches and Configure It as the vPC Peer-Link

**vPC Peer-Link: Turning Two Switches into One Brain**

The *vPC peer-link* is the Layer-2 backbone that makes vPC real. This is where the *illusion of a single control plane* finally becomes truth.

![vPC Peer-Link](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vpc_peer_link.png)

What the peer-link does:

- Synchronizes *MAC tables*, STP state, and control-plane info

- Carries *orphan traffic* during failures (when one peer loses an uplink)

- Allows *stateful failover* without blackholing traffic

Because of this, the peer-link *must be fast, redundant, and boringly stable.* That’s why it’s always:

- A *port channel*

- Made of *multiple links*

- Ideally on *different I/O modules*

**Building the Peer-Link Port Channel:**

You create a *normal* port channel first, then *elevate* it to a vPC peer-link.

Example config:

```
N9K-C(config)# interface ethernet 1/3
N9K-C(config-if)# no switchport access vlan 200
N9K-C(config-if)# switchport mode trunk
N9K-C(config-if)# channel-group 1
N9K-C(config-if)# shutdown
N9K-C(config-if)# no shutdown
N9K-C(config-if)# interface ethernet 1/4
N9K-C(config-if)# no switchport access vlan 200
N9K-C(config-if)# switchport mode trunk
N9K-C(config-if)# channel-group 1
N9K-C(config-if)# shutdown
N9K-C(config-if)# no shutdown
N9K-C(config-if)#

N9K-D(config)# interface ethernet 1/3
N9K-D(config-if)# no switchport access vlan 200
N9K-D(config-if)# switchport mode trunk
N9K-D(config-if)# channel-group 1
N9K-D(config-if)# shutdown
N9K-D(config-if)# no shutdown
N9K-D(config-if)# interface ethernet1/4
N9K-D(config-if)# no switchport access vlan 200
N9K-D(config-if)# switchport mode trunk
N9K-D(config-if)# channel-group 1
N9K-D(config-if)# shutdown
N9K-D(config-if)# no shutdown
N9K-D(config-if)# 
```

Why ```no switchport access vlan 200``` first?

This line is used to *clean up any existing access config* on the interface. NX-OS is strict; if the port previously had an access VLAN, switching it straight to trunk can throw warnings or inconsistencies. Think of it as *scrubbing state before repurposing the port.* Not strictly required in greenfield configs, but very common in labs and real networks.

Key points of the config:

- Interfaces are *Layer 2 trunk ports*

- No LACP used here (```Protocol NONE```)

- ```Shutdown``` / ```no shutdown``` helps NX-OS reconcile membership cleanly

After configuration, ```show port-channel summary``` says everything you want:

- ```Po1(SU)``` → switched + up

- Member ports show ```(P)``` → actively bundled

**Promoting the Port Channel to vPC Peer-Link:**

This is the magical incantation:

```
interface port-channel 1
 vpc peer-link
```

Once applied on *both switches,* the peer-link becomes:

- A protected vPC control path

- STP-special

- VLAN-restricted to vPC-related traffic

*Bridge Assurance (That Warning I Saw):*

vPC requires *Bridge Assurance* to prevent split-brain disasters. On Nexus, it’s usually already enabled globally, but if it isn’t:

```
spanning-tree port type network
```

This must be applied on the *peer-link port-channel* (both sides). Bridge Assurance ensures that if BPDUs stop, the link is *hard-blocked,* not trusted. This is one of those “silent guardians” features — invisible when correct, catastrophic when missing.

**Final Verification:**

At this point:

- ```show vpc``` → *peer adjacency formed ok*

- ```show vpc peer-link``` → *up*, VLANs listed

- ```show vpc role``` → *primary / secondary elected*

Now the *vPC system MAC exists,* and yes, your observation is sharp:

- The *last octet (0A)* comes directly from *vPC domain 10*

- Identity negotiation is complete

- One switch becomes primary — *but traffic still flows symmetrically*

Primary ≠ active/standby.

Primary = *extra responsibilities,* not monopoly on forwarding.

**Cookbook TL;DR**

- Peer-link = *L2 port channel + control-plane spine*

- Clean old access config before trunking (defensive hygiene)

- Always multi-link, fast, and boring

- Bridge Assurance is *mandatory*

- Once peer-link is up → system MAC appears → roles settle → vPC is alive

### Configure the vPC Member Interfaces

*What the vPC domain actually gives you (and what it does not):*

Creating a vPC domain *does not magically forward traffic.* At this stage, the two Nexus switches merely agree to *present a single logical identity* to downstream devices using a shared *vPC system MAC.* This makes downstream switches *believe* they are connected to one upstream device.

What vPC gives you at this point:

- Redundancy (no STP block on dual-homed links)

- The ability to load balance

- A shared control-plane identity

What it does *not* give you yet:

- Working data paths

- Active forwarding interfaces

- Any usable links

Traffic only starts flowing once *port-channels are built and explicitly attached to the vPC domain.*

![vPC Members](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vpc_member_interfaces.png)

*Load balancing in vPC (important nuance):*

Load balancing in a vPC setup means traffic can be forwarded *simultaneously through both physical switches,* instead of one being blocked by STP. Hashing decisions are made per-flow, not per-packet, so you’ll typically see “roughly half” the traffic per switch across many flows.

This behavior improves further when:

- Interfaces are bundled into *port-channels*

- Multiple physical links exist per channel

- LACP is used to manage consistency and failure detection

**The critical concept:**

Once the vPC domain is established, *you do not add physical interfaces directly to vPC.* Instead, the workflow is:

1. Build *local port-channels* on each physical switch

2. Then bind those port-channels together using ```vpc <ID>```

Think of it like this:

*Port-channel = local bundle*

*vPC ID = logical glue across switches*

Each vPC member switch has *its own* port-channel interface. The ```vpc <ID>``` command simply tells both switches: “These two *separate* port-channels belong to the *same logical upstream connection.”*

**vPC ID vs Port-Channel ID:**

- Port-channel numbers are *locally significant*

- vPC IDs are *globally significant across the vPC pair*

So:

- Port-channel ```10``` on N9K-A ≠ Port-channel ```10``` on N9K-B by default

- But once both are assigned ```vpc 10```, they represent *one logical port-channel* to downstream devices

Matching numbers are not required, but *absolutely recommended* unless you enjoy troubleshooting chaos at 3 AM.

**Step 1: Verify and enable LACP**

vPC strongly expects LACP. While static bundling exists, LACP provides:

- Mis-cabling detection

- Compatibility checks

- Faster failure detection

- Cleaner vPC consistency behavior

Check the current state:

```
N9K-A# configure
N9K-A(config)# show feature | include lacp
lacp                   1          disabled
```

and...

```
N9K-B# configure
N9K-B(config)# show feature | include lacp
lacp                   1          disabled
```

Enable LACP:

```
N9K-A(config)# feature lacp
N9K-B(config)# feature lacp
```

**Step 2: Build local port-channels on N9K-A and N9K-B**

Interfaces Ethernet1/2 and Ethernet1/6 are bundled into port-channel 10 using LACP active mode.

```
N9K-A(config-if)# interface ethernet1/2, ethernet1/6
N9K-A(config-if-range)# no switchport access vlan 200
N9K-A(config-if-range)# switchport mode trunk
N9K-A(config-if-range)# channel-group 10 mode active
N9K-A(config-if-range)# shutdown
N9K-A(config-if-range)# no shutdown
```

and...

```
N9K-B(config)# interface ethernet1/2, ethernet1/6
N9K-B(config-if-range)# no switchport access vlan 200
N9K-B(config-if-range)# switchport mode trunk
N9K-B(config-if-range)# channel-group 10 mode active
N9K-B(config-if-range)# shutdown
N9K-B(config-if-range)# no shutdown
```

*Note:* NX-OS trunks allow all VLANs by default. That’s why no ```switchport trunk allowed vlan``` statement is required here. This is acceptable in:

- Labs

- Core / aggregation interconnects

In real access-layer designs, you almost always want explicit VLAN lists to:

- Reduce attack surface

- Avoid accidental VLAN leaks

- Reduce vPC consistency failures

*About ```mode on``` vs ```mode active``` (short answer: don’t):*

Yes, ```mode on``` would technically work. No, you should not use it for vPC.

Reasons:

- No negotiation

- No mis-cabling detection

- Breaks vPC safety checks

- Can cause silent traffic blackholing

Rule of thumb: vPC + production = LACP active/passive only

*Additional Notes (from the lab):* When you add an interface to a channel group, the software checks certain interface attributes to ensure that the interface is compatible with the channel group. For example, you cannot add a Layer 3 interface to a Layer 2 channel group. The Cisco NX-OS Software also checks several operational attributes for an interface before allowing that interface to participate in the port-channel aggregation. Use the ```show port-channel compatibility-parameters``` command to see the complete list of compatibility checks that Cisco NX-OS Software uses.

**Step 3: Configure the logical port-channel interface**

```
N9K-A(config)# interface port-channel 10
N9K-A(config-if)# description PC connection to vPC domain 10
```

and...

```
N9K-B(config)# interface port-channel 10
N9K-B(config-if)# description PC connection to vPC domain 10
```

At this point:

- Port-channel exists

- LACP is configured

- But no traffic flows yet

**Step 4: Why the port-channel is suspended (important diagnostic insight)**

The output of ```show port-channel summary``` now shows:

```
Po10(SD) Eth LACP Eth1/2(s) Eth1/6(s)
```

Suspended (```s```) status means:

- LACP negotiation incomplete

- Remote side not yet configured

- vPC binding missing

This is expected. You have only built *half* the topology.

**Step 5: Build downstream port-channels (N9K-C and N9K-D)**

Because the downstream switches see the vPC pair as *one logical switch*, they must bundle *one interface to each upstream switch* into a single port-channel.

Port-channel 11 toward N9K-A:

```
N9K-C(config)# feature lacp
N9K-C(config)# interface ethernet1/2
N9K-C(config-if)# no switchport access vlan 200
N9K-C(config-if)# switchport mode trunk
N9K-C(config-if)# channel-group 11 mode active
N9K-C(config-if)# shutdown
N9K-C(config-if)# no shutdown
```

and...

```
N9K-D(config)# feature lacp
N9K-D(config)# interface ethernet1/6
N9K-D(config-if)# no switchport access vlan 200
N9K-D(config-if)# switchport mode trunk
N9K-D(config-if)# channel-group 11 mode active
N9K-D(config-if)# shutdown
N9K-D(config-if)# no shutdown
```

Port-channel 12 toward **N9K-B:** repeat using different interfaces and port-channel ID ```12```.

```
N9K-C(config-if)# interface ethernet 1/6
N9K-C(config-if-range)# no switchport access vlan 200
N9K-C(config-if-range)# switchport mode trunk
N9K-C(config-if-range)# channel-group 12 mode active
N9K-C(config-if-range)# shutdown
N9K-C(config-if-range)# no shutdown
N9K-C(config-if-range)#
```
and...

```
N9K-D(config-if)# interface ethernet1/2
N9K-D(config-if-range)# no switchport access vlan 200
N9K-D(config-if-range)# switchport mode trunk
N9K-D(config-if-range)# channel-group 12 mode active
N9K-D(config-if-range)# shutdown
N9K-D(config-if-range)# no shutdown
N9K-D(config-if-range)#
```

**Step 6: Bind downstream port-channels to vPC**

Until this is done, these are *ordinary port-channels*, not vPC members.

N9K-C config:

```
N9K-C(config)# interface port-channel 11
N9K-C(config-if)# switchport mode trunk
N9K-C(config-if)# vpc 11
```

and...

```
N9K-C(config)# interface port-channel 12
N9K-C(config-if)# switchport mode trunk
N9K-C(config-if)# vpc 12
```

N9K-D config:

```
N9K-D(config)# interface port-channel 11
N9K-D(config-if)# switchport mode trunk
N9K-D(config-if)# vpc 11
```

and...

```
N9K-D(config)# interface port-channel 12
N9K-D(config-if)# switchport mode trunk
N9K-D(config-if)# vpc 12
```

This is the moment the topology “clicks” into place.

**Step 7: Verification**

- ```show port-channel summary``` → ```SU``` status

- ```show interface port-channel <group-number> brief``` → provides a concise, per–port-channel view showing operational status, switchport mode (L2/L3), trunking state, protocol (LACP), and *the exact reason* a port-channel is up or down (for example, *No operational members*), making it ideal for quickly diagnosing why a port-channel is not forwarding traffic.

- ```show vpc brief``` → consistency ```success```

- No suspended members

- VLANs active across peer-link and vPCs

At this point:

- vPC is forwarding

- Load balancing is active

- No STP blocking

- Downstream devices see *one switch*

*Final mental model:* Port-channels move traffic. vPC only tells the switches which port-channels belong together.
