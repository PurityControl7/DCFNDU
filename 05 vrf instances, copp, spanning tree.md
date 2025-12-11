# Describing Switch Virtualization

*Cisco Nexus Series Switches support many virtualization options in which you can segment one physical device into several devices that function independently. This virtualization includes Layer 3 virtual routing and forwarding (VRF) instances. Cisco Nexus Series Switches also provide operational segmentation into functional planes to segment the functions of the switch into functional layers.*

*This segmentation enables features (such as Control Plane Policing [CoPP] and stateful error recovery) that prevent operational disruptions. All these functionalities allow you to establish a stable data center environment with high performance and easy management.*

## Cisco Nexus Switch Basic Components

*Cisco Nexus Series Switches are data center devices that are designed to provide high performance while maintaining fault tolerance. The internal design of the switch segments the functionalities of the device into segments or planes that perform specific functions.*

*Cisco Nexus Operating System (Cisco NX-OS) also allows process separation within the device, which recovers services that fail and prevents system overloading by policing traffic. You will learn how these systems work and how to configure them.*

### Cisco Nexus Switch Functional Planes

*The traffic within a Cisco Nexus Series switch has three functional components or planes:*

- ***Data plane:*** *This plane manages all the end-to-end user data traffic (packet and frame forwarding).*

- ***Control plane:*** *This plane manages all Layer 2 and Layer 3 protocol control traffic. These control plane packets are destined to the device Layer 2 (MAC) and Layer 3 (IP) addresses.*

- ***Management plane:*** *This plane manages the device and is used for device configuration and monitoring.*

*The figure illustrates the Cisco Nexus 93400LD-H1 internal architecture.*

![Internal Arhitecture](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/internal_arhitecture.png)

*The CPU connects with PCI Express (PCIe) connections to the LS6400H1 switch on chip (SOC).*

*The console and 10, 100, and 1000BASE-T Ethernet management port are used to access the management plane to configure the device. For example, you would configure the device hostname, change interface status, and configure Open Shortest Path First (OSPF) routing protocol parameters.*

*The second very important functionality of the management plane is monitoring. It is necessary to ensure continuous operability and health of the device and its services.*

*Some protocols that are associated with the management plane are Secure Shell (SSH), Telnet, Network Configuration Protocol (NETCONF), and Simple Network Management Protocol (SNMP).*

*On the control plane side, the Cisco Nexus 93400LD-H1 switch runs Cisco NX-OS Software on a CPU.*

*The control plane is responsible for communicating with Layer 2 protocols that are needed for routing:*

- ***STP:*** *Spanning Tree Protocol*

- ***CDP:*** *Cisco Discovery Protocol*

- ***ARP:*** *Address Resolution Protocol*

- ***DHCP:*** *Dynamic Host Configuration Protocol*

*The control plane is also responsible for communicating with Layer 3 protocols that are needed for routing:*

- ***RIP:*** *Routing Information Protocol*

- ***OSPF:*** *Open Shortest Path First*

- ***BGP:*** *Border Gateway Protocol*

*The control plane manages route exchange, neighbor establishment with other routers, and populating of the IP routing table. It calculates the routing table with the Routing Information Base (RIB) and the forwarding table with the Forwarding Information Base (FIB) for data plane operation.*

*The main component of the data plane on the Cisco Nexus 93400LD-H1 consists of a single LS6400H1 application-specific integrated circuit (ASIC). This ASIC is connected via a shared on-die packet buffer of 40 MB. It has MACsec capability to 48 front-panel Small Form-Factor Pluggable (SFP) SFP56 ports and four Quad Small Form-Factor Pluggable–Double Density (QSFP-DD) ports. It uses a shared hash table known as the Unified Forwarding Table (UFT) to store Layer 2 and Layer 3 forwarding information. It is responsible for traffic buffering and transferring from the ingress interfaces to the egress interfaces.*

*When a packet enters through a front-panel port, its header is parsed to extract and save information such as the Layer 2 header, Layer 3 header, and TCP/IP protocol.*

*Then it is subject to Layer 2 switching and Layer 3 routing lookups. First, the forwarding process examines the Destination MAC (DMAC) address of the packet to determine whether the packet must be switched (Layer 2) or routed (Layer 3). If a match is found in the MAC address table, the packet transmits to the egress port.*

*If the packet must be routed, the destination IP (DIP) address is used for searches in the Layer 3 host table. This table stores forwarding entries for directly attached hosts and learned /32 host routes. In addition to forwarding lookup processing, the packet undergoes ingress access control list (ACL) processing.*

*The LS6400H1 ASIC also performs buffering, packet queuing, and scheduling. It is responsible for the application of egress policy and all packet rewrite operations before the packet transmits to the egress interface.*

*Note: All Cisco Nexus switches can be logically separated into management, control, and data plane but can differ based on internal architecture. For example, the modular Cisco Nexus 9000 Series switches take a distributed control plane approach. They have a multicore CPU on each I/O module and a multicore CPU for the switch control plane on the (dual) supervisor module.*

### Cisco NX-OS CoPP

*Because the data plane can manage much more traffic than the control plane, its capabilities can be exhausted when too many packets are destined to the control plane. Therefore, the traffic that is coming from the data plane to the control plane requires monitoring. Cisco NX-OS performs this monitoring with Control Plane Policing (CoPP).*

*The figure shows how packets are processed in the data and control planes.*

![Packet Processing](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/packet_processing.png)

### CoPP on Cisco Nexus 9000 Series Switches

*The supervisor module is hardware on the Cisco Nexus 9000 Series switch that is critical to network operation and responsible for both the management plane and control plane traffic. Any disruption or attacks on the supervisor module may result in serious network outages.*

*Denial of service (DoS) attacks typically involve high rates of traffic targeting the route processor itself. Cisco NX-OS provides CoPP to prevent possible DoS attacks from impacting the performance of the control plane. The CoPP feature works by monitoring the traffic and limiting the amount of traffic that transmits to the control panel.*

*Traffic that hits the CPU on the supervisor module can arrive via four paths:*

- *The in-band interfaces (front panel port) for traffic that line cards send.*

- *The management interface (mgmt0), which is used for management traffic.*

- *The control and monitoring processor interface that is used for the console.*

- *Switched Ethernet out-of-band channel (EOBC) to control the line cards from the supervisor module and exchange status messages.*

*Note: Only the traffic that is passing the supervisor module through the forwarding engines on the in-band interfaces is subject to CoPP.*

*To monitor the traffic, Cisco NX-OS uses a set of values to evaluate the packet load. An administrator can set a ***committed information rate*** (CIR) value that represents the desired bandwidth. You can specify it as a bit rate or a percentage of the link rate. You can also set a ***committed burst*** value that represents the size of a traffic burst that can exceed the CIR value within a given unit of time.*

*Set the level of protection on the Cisco Nexus 9000 Series Switches by choosing a CoPP policy option from the initial setup in the system configuration dialog: Strict, Moderate, Lenient, Dense, and Skip. Cisco does not recommend using the Skip option because it will impact the control plane of the network. All the options use different CIR and burst count values for policing.*

### Stateful Fault Recovery on Cisco Nexus 9000 Series Switches

*Another important feature that is included in Cisco NX-OS Software is Stateful Fault Recovery.*

![Stateful Fault Recovery](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/stateful_fault_recovery.png)

*Cisco NX-OS Software provides isolation between the control and data planes within the device. This isolation means that a failure within one plane does not disrupt the other plane.*

*When a restartable service fails, it restarts on the same supervisor. If the new instance of the service determines that the operating system abnormally terminated the previous instance, the service then determines whether a persistent context exists. The initialization of the new instance attempts to read the persistent context to build a run-time context that makes the new instance appear like the previous one.*

*After the initialization is complete, the service resumes the tasks that it was performing when it stopped. During the restart and initialization of the new instance, other services are unaware of the service failure. Any messages that transmit to the failed service by other services are available from the message and transaction service (MTS) when the service resumes.*

*The success of the new instance in surviving the stateful initialization depends on the cause of failure of the previous instance. If the service is unable to survive a few subsequent restart attempts, the restart is considered as failed.*

*In cases where the stateful restart fails, the system manager performs the action that the high-availability service policy specifies. This action forces a stateless restart, no restart, a supervisor switchover, or a reset.*

*In a stateless restart, the service initializes and runs as if it had just started with no prior state. A stateful restart of the service can retrieve this stored state information and resume operations from the last checkpoint service state, which means that system recovery time after a failure is reduced.*

*Before, during, and after a stateful restart, the following procedure takes place:*

1. *During normal operation, the running services make a checkpoint of their run-time state information to the Persistent Storage Service (PSS).*

2. *During normal operation, the system manager monitors the health of the running services using heartbeats.*

3. *The service encounters a fatal error.*

4. *The system manager restarts the service instantly when it crashes or stops responding.*

5. *After restarting, the service recovers its state information from the PSS and resumes all pending transactions.*

6. *If the service does not resume a stable operation after multiple restarts, the system manager initiates a reset or switchover of the supervisor.*

7. *Cisco NX-OS collects the process stack and core for debugging purposes with an option to transfer core files to a remote location.*

*The figure shows a failed OSPF process that is restarting.*

![Process Restart](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/process_restart.png)

*Stateful fault recovery is not always possible. In such eventualities, you can perform a stateless restart if the high-availability policy determines that recovery is impossible. During a stateless restart, the system manager replaces the failed service. The newly started service then attempts to build its run-time state from the running configuration or by exchanging information with other services.*

*An example of this type of behavior is OSPFv2:*

- ***Cisco Nonstop Forwarding in routing protocols:*** *The Cisco Nexus 9000 Series switch supports OSPFv2, Enhanced Interior Gateway Routing Protocol (EIGRP), and BGP. Each of these protocols includes network-level high-availability mechanisms to minimize network disruption because of process restarts or supervisor switchovers.*

- ***OSPFv2 stateless restart:*** *If a Cisco NX-OS system that runs OSPFv2 experiences a cold reboot, the network stops forwarding traffic to the system and removes the system from the network topology. In this scenario, OSPFv2 experiences a stateless restart and removes all neighbor adjacencies on the local system. Cisco NX-OS applies the startup configuration and OSPFv2 rediscovers the neighbors and re-establishes adjacencies.*

- ***OSPFv2 graceful restart on a switchover:*** *When a supervisor switchover begins, OSPFv2 initiates a graceful restart, or Cisco Nonstop Forwarding, by announcing that OSPFv2 will be unavailable for some time. During the switchover, neighbor devices continue to forward traffic and keep the system in the network topology. After the switchover, Cisco NX-OS applies the running configuration, and OSPFv2 informs the neighbors that it is operational again. The neighbor devices help to re-establish adjacencies.*

- ***OSPFv2 graceful restart on an OSFPv2 process failure:*** *OSPFv2 automatically restarts if the process experiences problems. After the restart, OSPFv2 initiates a graceful restart so that the platform is not removed from the network topology. If you manually restart OSPF, it performs a graceful restart, which is similar to a Stateful Switchover (SSO). The running configuration is applied in both cases. The graceful restart allows OSPFv2 to remain in the data forwarding path through the process restart.*

## Virtual Routing and Forwarding

*Virtual routing and forwarding (VRF) is a function of Cisco NX-OS. Routing information is segmented into Layer 3 logical segments or VRF instances that each have a separate routing information database. These virtual systems create Layer 3 routing segmentation, where several Routing Information Bases (RIBs) can exist simultaneously and where different services can use them when needed. This approach lets you use one device as if there were many, which saves power and management overhead while enabling you to create complex Layer 3 routing systems.*

### Layer 3 Routing Table Segmentation

*By default, a router or Layer 3 switch has a global routing table that uses a global RIB to support a single Layer 3 address domain. Each Layer 3 interface (logical or physical) belongs to the global routing table. There is no logical separation.*

*The RIB that is derived from the control plane consists of routing information obtained via static route definitions or any dynamic routing protocols that are running on a device. Only the best routes from all routing protocols are stored in this table.*

*The Forwarding Information Base (FIB), which works at data plane, is calculated based on the RIB. Compared to the RIB, this database holds only necessary information (such as next-hop information and network prefix) to make an extremely fast-forwarding decision for each packet.*

*To provide logical Layer 3 separation within a Layer 3 switch, you must segment the data plane and control plane functions of the Layer 3 switch into different VRF contexts. This process is similar to the way that a Layer 2 switch separates the Layer 2 control and data planes into different virtual LANs (VLANs).*

*Each VRF instance represents a unique Layer 3 addressing domain and is associated with a unique RIB. Each Layer 3 interface (logical or physical) belongs to only one VRF instance. Each VRF instance contains a separate address space with unicast and multicast route tables for IPv4 and IPv6 and makes routing decisions that are independent of any other VRF instance.*

*VRF virtualization can be represented as a stack of layers with the same functionality but different configurations.*

![VRF Representation](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vrf.png)

*A VRF instance includes the following components:*

- ***A subset of the Layer 3 interfaces on a Layer 3 switch:*** *Similar to how Layer 2 ports are assigned to a particular VLAN on a Layer 2 switch, the Layer 3 interfaces of the Layer 3 switch are assigned to a VRF instance. Because the elementary component is a Layer 3 interface, this component includes software interfaces such as subinterfaces, tunnel interfaces, loopback interfaces, and switched virtual interfaces (SVIs).*

- ***A routing table or RIB:*** *Traffic between Layer 3 interfaces that are in different VRF instances should remain separated. Therefore, a separate routing table is necessary for each VRF instance. The separate routing table ensures that traffic from an interface in one VRF instance cannot be routed to an interface in a different VRF instance.*

- ***A forwarding table or FIB:*** *The FIB is downloading to line cards and is used for actual packet forwarding. This table also must be separated by a VRF instance into one FIB for IPv4 and IPv6 for each configured VRF instance.*

- ***Routing protocol instances:*** *To ensure control plane separation between the different Layer 3 VPNs, it is necessary to implement routing protocols on a per-VRF-instance basis. To accomplish this task, you can run an entirely separate process for the routing protocol in each VRF instance. You can also use a subprocess or routing protocol instance in a global process that controls the routing information exchange for the VRF instance.*

*Per-VRF-instance characteristics are the following:*

- *There are independent routing and forwarding decisions.*

- *IPv4 and IPv6 unicast and multicast tables are created automatically.*

- *The number of programmed routes is limited.*

### Management and Default VRF Instances

*Each Cisco NX-OS device has a default VRF instance and a management VRF instance. All Layer 3 interfaces exist in the default VRF instance until you assign them to another VRF instance. By default, all EXEC commands are processed in the default VRF instance unless otherwise specified in command execution.*

*Here are the characteristics of the default VRF instance:*

- *All Layer 3 interfaces exist in the default VRF instance until they are assigned to another VRF instance.*

- *Routing protocols run in the default VRF context unless you specify another VRF context.*

- *The default VRF instance uses the default routing context for all ```show``` commands.*

- *The default VRF instance is similar to the global routing table concept.*

- *Commands that you execute in the command line, like ```ping```, use the default VRF instance to perform the requested action.*

*Here are the characteristics of the management VRF instance:*

- *The management VRF instance is for management purposes only.*

- *Only the mgmt0 interface can be in the management VRF instance; the mgmt0 interface cannot be assigned to another VRF instance.*

- *No routing protocols can run in the management VRF instance (static routing only).*

![VRF Instances](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vrf_instances.png)

*The following are VRF guidelines and limitations:*

- *When you make an interface a member of an existing VRF instance, Cisco NX-OS removes all Layer 3 configurations. Therefore, you should configure all Layer 3 parameters after adding an interface to a VRF instance.*

- *If you configure an interface for a VRF instance before the VRF instance exists, the interface is operationally down until you create the VRF instance.*

- *Cisco NX-OS creates the default and management VRF instances automatically. You should configure the mgmt0 IP address and other parameters after you add the mgmt0 interface to the management VRF instance.*

- *The ```write erase boot``` command does not remove the management VRF configurations. You must use the ```write erase``` command and then the ```write erase boot``` command.*

### VRF-Aware Services

*When separating routing information into VRF instances, the services can use any of the VRF instances for their operation with significantly different results. Therefore, a fundamental feature of the Cisco NX-OS architecture is that every IP-based feature is VRF-aware.*

*The following table shows you the VRF-aware services that can select a particular VRF instance to reach a remote server or to filter information based on the selected VRF instance:*

![VRF Aware Services](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vrf_aware_services.png)

## Lab: Configure VRF

VRF (Virtual Routing and Forwarding) lets a single Nexus switch juggle *multiple, fully isolated Layer 3 routing tables at the same time.*

Each VRF behaves like its *own router,* with independent IPv4/IPv6 unicast and multicast tables, its own routing protocols, and zero awareness of other VRFs unless explicitly configured.

Key implications (burn these into memory):

- Interfaces belong to *exactly one VRF*

- Routing decisions are based on the *VRF of the incoming interface*

- If you don’t specify a VRF in a command, NX-OS assumes *VRF ```default```*

- Overlapping IP space is totally allowed → hello multitenancy

### Verify the Management Interface Configuration

Management interface ≠ default VRF (this is the trap)

On Nexus devices, ```mgmt0``` is *always* placed into the ```management``` VRF.

That VRF exists by default, alongside ```default```, and is used exclusively for *out-of-band management* (SSH, Telnet, SNMP, etc).

Verification step of ```show running-config interface mgmt 0``` (what actually matters here):

```
interface mgmt0
  vrf member management
  ip address 10.1.1.101/24
```

From N9K-A:

```
N9K-A# ping 10.1.1.102
ping: sendto 10.1.1.102 64 chars, No route to host
```

This *does not* mean ```mgmt0``` is broken. It fails because:

- ```ping``` ran in *VRF default*

- The routing table being consulted was *VRF default*

- That table has *no route to 10.1.1.0/24*

Confirmed by:

```
N9K-A# show ip route
IP Route Table for VRF "default"
```

**The “aha” moment: correct VRF, correct routing table**

List VRFs:

```
show vrf
```

You’ll always see:

- ```default``` (VRF-ID 1, highest priority)

- ```management```

Now query the *right* routing table:

```
N9K-A# show ip route vrf management
```

Which correctly contains:

```
10.1.1.0/24 via mgmt0
```

So the fix is *not* a static route. The fix is *telling NX-OS which brain to use.*

**The correct ping (this is the key command):**

```
N9K-A# ping 10.1.1.102 vrf management
```

- The command explicitly uses the *management VRF*

- The routing table now matches the mgmt interface

*Mental model to keep forever:*

Think of VRFs as *parallel realities:*

- Same box

- Same CLI

- Totally different routing universes

If traffic “mysteriously” doesn’t route, the first question is always: *Which VRF am I actually in right now?*

### Configure VRF with OSPFv2 Routing

In NX-OS, VRFs don’t just isolate interfaces — they isolate *services* too. That means routing protocols like OSPF run separately inside each VRF. This lab proves exactly that: an OSPF process can exist in the default VRF, the management VRF, and a custom VRF simultaneously, each maintaining its own adjacencies and routing tables.

**1. Verify Initial VRFs:**

Every NX-OS switch starts with at least these VRFs:

- default

- management

- System/service VRFs (often things like VPC-KEEPALIVE)

```
N9K-C# show vrf
VRF-Name                           VRF-ID State   Reason
VPC-KEEPALIVE                           4 Up      --
default                                 1 Up      --
egress-loadbalance-resolution-          3 Up      --
management                              2 Up      --
```

*Important point:* If you *don’t* specify a VRF at the end of a command, NX-OS assumes ```vrf default```.

**2. Create the Custom VRF (“DCFNDU”):**

This VRF will host its own interfaces, its own route table, and its own OSPF instance.

```
N9K-C(config)# vrf context DCFNDU
N9K-C(config-vrf)# show vrf
VRF-Name                           VRF-ID State   Reason
DCFNDU                                  5 Up      --
default                                 1 Up      --
management                              2 Up      --
```

Notes:

- VRF names can be up to 32 chars.

- This is a pure routing table container until you put interfaces inside it.

**3. Check Current Interface IPs (default VRF):**

You want to see what lives in the default VRF before moving anything.

```
N9K-C# show ip interface brief
IP Interface Status for VRF "default"(1)
Interface    IP Address      Status
Vlan200      172.16.200.11   up/up
```

VLAN 200 is currently routed *in the default VRF.*

**4. Create Loopback 12 in VRF DCFNDU:**

Each switch gets one loopback, and they're placed *directly* into the new VRF.

```
interface loopback 12
  vrf member DCFNDU
  ip address 192.168.12.11/32   ← (C)
```

On D:

```
interface loopback 12
  vrf member DCFNDU
  ip address 192.168.12.21/32
```

Important: When you add an interface to a VRF, NX-OS wipes all L3 config. Loopback wipes are harmless, but SVI wipes are… painful.

**5. Enable OSPF Feature:**

NX-OS uses modular features.

```
feature ospf
```

**6. Configure OSPF Process 42:**

On C and D:

```
router ospf 42
```

Assign interfaces to OSPF:

```
interface vlan 200
  ip router ospf 42 area 0

interface loopback 12
  ip router ospf 42 area 0
```

A single process ID can run in *all VRFs* at once, but it behaves as separate processes per VRF. The process ID is only locally significant.

**7. Check OSPF Status in VRFs:**

OSPF in DCFNDU (only has the loopback so far — no adjacencies possible):

```
show ip ospf vrf DCFNDU
 Routing Process 42 with ID 192.168.12.11 VRF DCFNDU
```

Default VRF (SVI 200 is still here, so adjacency forms here):

```
show ip ospf neighbors
 Neighbor ID   Pri  State   Address         Interface
 172.16.200.12  1   FULL    172.16.200.12   Vlan200
```

**8. Attempt to Ping N9K-D’s Loopback (Will Fail):**

Because N9K-C *does not* have route info for DCFNDU yet — OSPF adjacency is not in that VRF.

**9. Move VLAN 200 Into VRF DCFNDU:**

This is the big moment. When you put an SVI into a VRF, NX-OS *deletes* all IP configuration:

```
interface vlan 200
  vrf member DCFNDU
  ip address 172.16.200.11/24
  ip router ospf 42 area 0
```

Same on N9K-D.

*Important:* Moving VLAN 200 into DCFNDU forces OSPF adjacency to move into that VRF as well. This is the whole point of the lab.

**10. Check OSPF Neighbor in DCFNDU:**

Now adjacency exists:

```
show ip ospf neighbors vrf DCFNDU
 Neighbor ID     Pri State   Address         Interface
 192.168.12.21     1 FULL    172.16.200.12   Vlan200
```

The loopbacks are now mutually reachable *inside the VRF.*

**11. Inspect the DCFNDU Routing Table:**

You should now see:

- Local subnet

- Local loopback

- Remote loopback (learned via OSPF)

```
show ip route vrf DCFNDU
192.168.12.21/32
  *via 172.16.200.12, Vlan200, [110/41], ospf-42
```

The next hop is the peer’s SVI address.

**12. Ping the Remote Loopback — Success:**

N9K-C can now ping 192.168.12.21 from VRF DCFNDU.

Routing information is correctly propagated solely *inside* the VRF.

**Key Takeaways for Future Me:**

*1. VRF = isolated routing universe*

Every VRF has its own:

- route table

- OSPF processes

- neighbors

- interfaces

*2. OSPF process ID isn’t tied to a VRF*

Same process ID can operate in several VRFs simultaneously, but each VRF runs an isolated instance.

*3. Moving an interface into a VRF nukes its L3 config*

SVIs suffer the most. Loopbacks barely notice.

*4. OSPF adjacencies form only inside the VRF an interface belongs to*

SVI 200 in default VRF → adjacency in default

SVI 200 moved to DCFNDU → adjacency only in DCFNDU

*5. Ping defaults to the default VRF unless you specify otherwise*

So always use:

```
ping <IP> vrf <vrf-name>
```

## Lab: Explore CoPP and Spanning Tree on Cisco Nexus Switches

CoPP is basically the bouncer for the supervisor module — anything that needs CPU attention must pass through hardware rate-limiters *and* CoPP policies. If something starts blasting traffic toward the control plane (loops, floods, rogue hosts, or straight-up attacks), CoPP steps in and prevents the supervisor from melting down. Think of it as a QoS policy specifically for the control plane. You can’t disable it, and you shouldn’t want to.

*Key Concepts You Need to Remember:*

- **Traffic destined** ***to*** **the switch**, not through it, gets evaluated by CoPP.

- **Policy maps** classify traffic into classes (BGP, OSPF, NDP, DHCP, exceptions, etc.).

- **Each class has a CIR (pps)** — anything beyond it gets dropped (CIR - committed input rate).

- **Profiles exist (strict, moderate, lenient, dense)** to tune how aggressively the switch protects itself.

- **Strict** is default, and recommended for data center designs.

**Exploring CoPP on NX-OS:**

Check CoPP help:

```
show copp ?
```

Check CoPP status:

```
show copp status
```

Example output:

```
Last Config Operation: None
Last Config Operation Timestamp: None
Last Config Operation Status: None
Policy-map attached to the control-plane: copp-system-p-policy-strict
```

*That last line is the key: it tells you exactly which policy the switch is currently enforcing.*

**Viewing CoPP Profiles:**

List profile options:

```
show copp profile ?
```

View dense profile:

```
show copp profile dense
```

Example block (preserved):

```
ip access-list copp-system-p-acl-auto-rp
  permit ip any 224.0.1.39/32
  permit ip any 224.0.1.40/32
ip access-list copp-system-p-acl-bgp
  permit tcp any gt 1023 any eq bgp
  permit tcp any eq bgp any gt 1023
ipv6 access-list copp-system-p-acl-bgp6
  permit tcp any gt 1023 any eq bgp
  permit tcp any eq bgp any gt 1023
ip access-list copp-system-p-acl-dhcp
  permit udp any eq bootpc any
  permit udp any neq bootps any eq bootps
<... output omitted ...>
```

*Profiles define which protocols get protected and at what rates. Dense/lenient ones are more relaxed; strict is, well… strict.*

**Comparing CoPP Profiles:**

Profile diff command:

```
show copp diff profile strict profile dense
```

Preserved block:

```
Prior Profile Doesn't Exist.

'+' Line presents only in profile strict(ver: 10.5(1)I9(1))
'-' Line presents only in profile dense(ver: 10.5(1)I9(1))
    -policy-map type control-plane copp-system-p-policy-dense
    -  class copp-system-p-class-l3uc-data
    -    set cos 1
    -    police cir 250 pps bc 32 packets conform transmit violate drop
    -  class copp-system-p-class-openflow
    -    set cos 5
    -    police cir 1000 pps bc 32 packets conform transmit violate drop
    -  class copp-system-p-class-critical
    -    set cos 7
    -    police cir 2500 pps bc 128 packets conform transmit violate drop
    -  class copp-system-p-class-important
    -    set cos 6
    -    police cir 1200 pps bc 128 packets conform transmit violate drop
    -  class copp-system-p-class-multicast-router
    -    set cos 6
    -    police cir 1200 pps bc 128 packets conform transmit violate drop
<... output omitted ...>
```

*Minus = line appears only in dense profile.*

*Plus = appears only in strict.*

This is a killer tool for quickly seeing how profiles differ.

**Seeing CoPP in Action (Class Maps & Counters):**

Full detailed statistics:

```
show policy-map interface control-plane
```

Preserved, detailed block:

```
Control Plane

  Service-policy  input: copp-system-p-policy-strict

    class-map copp-system-p-class-l3uc-data (match-any)
      match exception glean
      set cos 1
      police cir 250 pps , bc 32 packets
    class-map copp-system-p-class-critical (match-any)
      match access-group name copp-system-p-acl-bgp
      match access-group name copp-system-p-acl-rip
      match access-group name copp-system-p-acl-vpc
      match access-group name copp-system-p-acl-bgp6
      match access-group name copp-system-p-acl-ospf
      match access-group name copp-system-p-acl-rip6
      match access-group name copp-system-p-acl-eigrp
      match access-group name copp-system-p-acl-ospf6
      match access-group name copp-system-p-acl-eigrp6
      match access-group name copp-system-p-acl-auto-rp
      match access-group name copp-system-p-acl-mac-l3-isis
      set cos 7
      police cir 19000 pps , bc 128 packets
<... output omitted ...>
```

What this means:

- *class-map* = classification bucket

- *match access-group name …* = which ACL defines the traffic

- *set cos X* = marking for internal priority

- *police cir X pps* = traffic rate allowed before drops

The counters underneath (not shown above) reveal how many packets *conformed* or *violated* the CIR.

**Quick filtered view:**

```
show policy-map interface control-plane | include class|conform|violated
```

This is the go-to for spotting attacks, misconfigurations, loops, or suddenly chatty protocols.

**Viewing CoPP on Another Switch (N9K-B):**

Same commands apply:

```
show policy-map interface control-plane
```

Useful when comparing two devices: are they hitting CIR differently? Are certain routing protocols unexpectedly noisy on just one of them?

**STP Reminders (for the next lab):**

I’ll keep this tight, since STP theory is long but the practical takeaway is short:

- Only *one active Layer 2 path* can exist between any two endpoints.

- STP uses *BPDUs* to detect loops and choose the best loop-free tree.

- Redundant links stay *blocked,* and only come alive when the active link fails.

- All of this is invisible to end hosts — they just see a functioning Ethernet network.

This matters for CoPP because *insane amounts of BPDUs from a looped trunk can hammer the control plane — and CoPP is what stops the switch from catching fire.*

*Cisco’s General Recommendations:*

- Use *strict* profile as default.

- Customize later *only* if you know your environment deeply.

- Revisit CoPP periodically — protocols come and go, and your CoPP config must evolve with them.

### Evaluate a Simple Spanning Tree Topology

Spanning Tree Protocol (STP) keeps Layer 2 networks from eating themselves alive with loops. Every STP domain elects a *root bridge,* and all switches calculate a loop-free tree with a *single best path* toward that root.

NX-OS enables spanning tree by default in rapid-PVST mode.

**1. Get the STP Summary:**

Use this to see STP mode, root info per VLAN, and global STP behavior.

Command:

```
show spanning-tree summary
```

Example Output:

```
N9K-A# show spanning-tree summary
Switch is in rapid-pvst mode
Root bridge for: VLAN0001
L2 Gateway STP                           is disabled
Port Type Default                        is disable
Edge Port [PortFast] BPDU Guard Default  is disabled
Edge Port [PortFast] BPDU Filter Default is disabled
Bridge Assurance                         is enabled
Loopguard Default                        is disabled
Pathcost method used                     is short
STP-Lite                                 is disabled

Name                   Blocking Listening Learning Forwarding STP Active
---------------------- -------- --------- -------- ---------- ----------
VLAN0001                     0         0        0          6          6
---------------------- -------- --------- -------- ---------- ----------
1 vlan                       0         0        0          6          6
N9K-A#
```

*Key point:* This shows whether your switch is the root. If *Root bridge for: VLAN0001* appears → this box is the root for VLAN 1.

**2. Explore STP Command Variants:**

*This helps when you need specific info (root bridge, blocked ports, detailed interface behavior, etc.).*

Command:

```
show spanning-tree ?
```

The result:

```
active             Report on active interfaces only
blockedports       Show blocked ports
bridge             Status and configuration of this bridge
brief              Brief summary of interface information
detail             Detailed information
interface          Spanning Tree interface status and configuration
root               Status and configuration of the root bridge
summary            Summary of port states
vlan               VLAN Switch Spanning Trees
```

**3. Show STP Details for VLAN 1:**

This is where you figure out:

- who the root bridge is,

- what the root’s MAC is,

- port roles (Root, Designated, Alternate),

- costs, timers and path selection.

Command:

```
show spanning-tree vlan 1
```

The result:

```
VLAN0001
  Spanning tree enabled protocol rstp
  Root ID    Priority    32769
             Address     5235.42b0.1b08
             This bridge is the root
             Hello Time  2  sec  Max Age 20 sec  Forward Delay 15 sec

  Bridge ID  Priority    32769  (priority 32768 sys-id-ext 1)
             Address     5235.42b0.1b08

Interface        Role Sts Cost      Prio.Nbr Type
Eth1/1           Desg FWD 4         128.1    P2p
Eth1/2           Desg FWD 4         128.2    P2p
Eth1/3           Desg FWD 4         128.3    P2p
Eth1/4           Desg FWD 4         128.4    P2p
Eth1/5           Desg FWD 4         128.5    P2p
Eth1/6           Desg FWD 4         128.6    P2p
```

*Notes for Future Me:*

- *Root ID* MAC equals the *Bridge ID* MAC → this switch is the root.

- Root bridges have *no* root ports, only designated ports.

- Every other switch will have *one root port* pointing toward this switch.

**4. Check CDP Neighbors:**

This shows which devices are connected to which interfaces — extremely useful when mapping the physical STP tree.

Command:

```
show cdp neighbors
```

The result:

```
Device-ID          Local Intrfce ...
N9K-B(9BF8GDEP20F)
                    Eth1/3 ... N9K-C9300v        Eth1/3
```

Even though you already know N9K-A is the root, CDP helps you *validate* which links form the topology. If you were starting blind, this is how you'd follow “the trail” to the root device.

**5. Move to N9K-B and Inspect VLAN 1:**

This is where spanning tree gets interesting — you’ll see the *Root Port.*

Command:

```
show spanning-tree vlan 1
```

The result:

```
VLAN0001
  Root ID ... Address 5235.42b0.1b08
             Cost        4
             Port        3 (Ethernet1/3)

Interface        Role Sts
Eth1/1           Desg FWD
Eth1/2           Altn BLK
Eth1/3           Root FWD
Eth1/4           Altn BLK
Eth1/5           Altn BLK
Eth1/6           Altn BLK
```

Notes:

- Eth1/3 is the *Root Port* → the one single chosen path to N9K-A.

- All other redundant links become *Alternate/Blocked.*

- This is exactly what prevents L2 loops.

**6. Use CDP on N9K-B to Confirm Root Direction:**

Command:

```
show cdp neighbors
```

The result:

```
N9K-A(9NWIDD338NT)
                    Eth1/3 ... N9K-C9300v Eth1/3
```

Eth1/3 on N9K-B connects directly to N9K-A → perfect alignment with the root-port detection.

**7. Repeat on N9K-C:**

Every STP participant must identify the exact same root.

Command:

```
show spanning-tree vlan 1
```

The result:

```
Root ID ... Address 5235.42b0.1b08
Port        2 (Ethernet1/2)

Interface
Eth1/2           Root FWD
Eth1/3           Altn BLK
Eth1/4           Altn BLK
```

Notes:

- N9K-C chooses Eth1/2 as the best path toward the root.

- Everything else becomes alternate.

**8. Check BPDU Flow on the Root Port:**

BPDU counters rising = the port is actively participating in STP.

Command:

```
show spanning-tree interface ethernet 1/2 detail
```

The result:

```
Port 2 (Ethernet1/2) of VLAN0001 is root forwarding
   Port path cost 4
   Designated root ... address 5235.42b0.1b08
   BPDU: sent 9, received 2687
```

Notes:

- Run the command twice → *received* increments every 2 seconds.

- BPDU flow confirms link health and STP consistency.

*Tiny Final Reminder:*

Spanning tree is only stable when:

- all switches agree on the same root,

- each non-root switch has *exactly one root port,*

- redundant links become *alternate/blocked.*

Without this, Layer 2 becomes a haunted house of infinite frames ricocheting forever.
