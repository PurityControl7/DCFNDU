# Describing Cisco ACI

*Cisco Application-Centric Infrastructure (ACI) is a comprehensive software-defined network (SDN) architecture for data centers. It provides a policy-based automation solution to integrate physical and virtual environments under one policy model for networks, servers, storage, services, and security.*

*Cisco ACI provides a network that you deploy, monitor, and manage in a way that benefits various teams in your IT organization. Teams include the SDN network, cloud, DevOps, and security. It supports rapid application changes by reducing complexity with a common policy framework that can automate provisioning and resource management across data center, WAN, access, and cloud environments. This system empowers IT to be more responsive to changing business and application needs. This ability enhances agility and adds business value.*

*Cisco ACI is built on the following:*

- *Cisco Application Policy Infrastructure Controller (Cisco APIC)*

- *Cisco ACI fabric*

- *Cisco ACI partner ecosystem*

*Cisco ACI provides a single architecture for delivering performance, programmability, agility, and reduced complexity. An application-centric policy model dynamically defines the network fabric with the application requirements, so the application dictates the network, not the other way around.*

## Cisco ACI Overview 

*As traditional IT departments are under pressure to provide more agility and better outcomes to the business, a new model for operations has emerged, which is called Fast IT. Cisco ACI enables Fast IT by providing a common policy-based operational model across the entire Cisco ACI-ready system. Fast IT drastically reduces cost and complexity.*

*In the data center, Cisco ACI is a holistic architecture with centralized automation and policy-driven application profiles. Cisco ACI delivers software flexibility with the scalability of hardware performance that provides a robust transport network for today’s dynamic workloads. Cisco ACI is built on a network fabric that combines time-tested protocols with innovations to create a highly flexible, scalable, and resilient architecture of low-latency, high-bandwidth links.*

*This system-based approach simplifies, optimizes, and accelerates the entire application deployment lifecycle across the data center, WAN, access, and cloud environments.*

![APIC ACI](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/APIC_ACI.png)

*Main components of Cisco ACI:*

1. ***Spine switches:***

- *These switches represent the backbone of the Cisco ACI fabric.*

- *They connect to leaf switches.*

2. ***Leaf switches:***

- *These switches represent connection points for end devices, including the Application Policy Infrastructure Controller (APIC).*

- *They connect to spine switches.*

3. ***APICs:***

- *These managers provide a unified point of policy enforcement, health monitoring, and management for the Cisco ACI fabric.*

- *They are not involved in data-plane forwarding.*

*Key benefits of Cisco ACI:*

- *Automation of IT workflows and application deployment agility*

- *Open APIs and a programmable SDN fabric, with 65-plus ecosystem partners*

- *Security through allowlisting, policy enforcement, microsegmentation, and analytics*

- *Workload mobility at scale for physical and virtual load*

*The design of Cisco ACI is based on the whole fabric, as opposed to treating the fabric switches individually. All the physical components form the overall system.*

## Resolving Challenges of Traditional Network with Cisco ACI

*Let’s look at the following challenges of a traditional network and how Cisco ACI can resolve these challenges.*

*The first challenge of a traditional network is a complicated topology. Usually, traditional networks use traditional core-aggregation-access layers. When you add more devices, it can be complicated to manage this topology. Cisco ACI uses a spine-leaf topology. All the connections within the Cisco ACI fabric are from leaf to spine switches, and a mesh topology is between them. There is no leaf-to-leaf and no spine-to-spine connectivity. Leaf-and-spine topology is the basis of the Cisco ACI architecture.*

![ACI Topology](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/cisco_ACI_topology.png)

*Cisco Nexus 9000 switches are the physical devices that are used in Cisco ACI fabric. Compared to switches used in Cisco NX-OS mode, the difference is that the software that is used in Cisco ACI mode is the Cisco ACI operating system. Therefore, although the hardware may be the same, Cisco ACI provides a completely different product. Cisco ACI is not a feature of Cisco Nexus.*

![ACI Topology 2](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/cisco_ACI_topology2.png)

*The next challenge is avoiding the loop between Layer 2 devices. Traditional networks rely on the Spanning Tree Protocol (STP). In Cisco ACI, you do not rely on STP between leaf and spine switches; Equal Cost Multipathing (ECMP) is used instead.*

*There is IP reachability between leaf and spine switches. Therefore, you do not need STP, nor do you have to block any port to avoid the Layer 2 loops.*

![ACI Topology 3](https://github.com/PurityControl7/DCFNDU/blob/root/images/cisco_ACI_topology3.png)

*From the security perspective, in a traditional network device, you usually allow all the traffic by default, or you explicitly configure the device to block the traffic. However, Cisco ACI uses an allowlist model. By default, everything is blocked, unless you explicitly allow the traffic.*

![ACI Topology 4](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/cisco_ACI_topology4.png)

*Another challenge is device management. There can be tens or hundreds of devices in a leaf-and-spine topology. Instead of using Secure Shell (SSH) to each device to configure and build the Cisco ACI fabric, you use the centralized APIC. You can still directly access the leaf and spine switches, but you cannot configure anything directly on them. You always configure your Cisco ACI fabric from the Cisco APIC.*

*In Cisco ACI, three Cisco APIC controllers form an APIC group. If you lose one, you can still change and add new configurations through the remaining two controllers. If you lose all three, your traffic flow will not be impacted because the configurations are already pushed to the leaf and spine switches. So even if all the controllers are down, forwarding still happens on the leaf and spine switches. If you want to add changes, you must bring the Cisco APICs back up. Cisco APIC is simply a controller to push the configuration—it is not in the forwarding or data plane.*

*Another important point in the Cisco APIC is that it enables access via the Cisco API. In Cisco ACI, policies and objects can represent all configurations. You can store these policies and objects in the XML or JavaScript Object Notation (JSON) format. Policies and objects can be easily accessed via application programming interface (API) or configured via API.*

![ACI Topology 5](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/cisco_ACI_topology5.png)

*A traditional network usually has no automation, and users perform configuration manually and statically. In Cisco ACI, it is easy to automate configuration by using Representational State Transfer (REST) API calls. It is also possible to provide dynamic integrations where you can dynamically communicate and push the configuration to another vendor’s controller, such as VMware vCenter server, for example.*

![ACI Topology 6](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/cisco_ACI_topology6.png)

*Dynamic integration also helps with the last challenge: coordination between the network and server team. Typically, network and server teams differ. They must cooperate to ensure, for example, that the new service has correct security rules and a correct VLAN and that the correct VLAN is deployed in the correct place. Sometimes, that communication is not an easy task. By using the dynamic integration, such as VMware integration, you can dynamically push the configuration to the vCenter Server. Then you can verify that the network (ACI) side has deployed the configuration and that the server side has the mapped configuration.*

![ACI Topology 7](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/cisco_ACI_topology7.png)

## Cisco ACI Topology and Hardware

*Cisco ACI fabric uses a spine-leaf topology. High-bandwidth links between the spine and leaf switches provide transport to an integrated overlay. The host traffic that arrives at the ingress leaf and must transmit to an egress leaf is carried over an integrated overlay. All access links from endpoints attach to the leaf switches. They provide a high port density, while the spine switches (a minimum of two spine switches for redundancy) aggregate the fabric bandwidth.*

*Sometimes, the traditional model of multitier is still necessary. The primary reason is cable reach, and many hosts are located across floors or across buildings. However, due to the high cost of fiber cables and the limitations of cable distances, it is not ideal in some situations to build a full-mesh two-tier Clos fabric. In those cases, it is more efficient to build a spine-leaf-leaf topology and continue to benefit from the automation and visibility of Cisco ACI. Starting with the Cisco APIC Release 4.1(1), you can create a multitier Cisco ACI fabric topology that corresponds to the core-aggregation-access architecture. The new design for Cisco ACI incorporates the addition of a tier-2 leaf layer. It provides connectivity to hosts or servers on the downlink ports and connectivity to the leaf layer (aggregation) on the uplink ports.*

![Integrated Overlay](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/integrated_overlay.png)

*The Cisco ACI fabric is comprised of the Cisco APIC and the Cisco Nexus 9000 Series spine and leaf switches. The leaf switches connect to the spine switches but never to each other. The spine switches attach only to the leaf switches. The Cisco APIC and all other endpoints and devices in the data center connect to the leaf switches only as shown in the following figure.*

![Integrated Overlay 2](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/integrated_overlay2.png)

*With Cisco ACI, APICs manage the infrastructure IP address space and automatically allocate the proper IP addressing required for the leaf and spine. The infrastructure IP addresses are in a separate virtual routing and forwarding (VRF) than the user data traffic. This approach contains the infrastructure IP within the fabric so it will have no overlapping IP address issues. The infrastructure VRF instance is transparent to external traffic. You specify this IP address range, which is called a tunnel endpoint (TEP) pool, during the Cisco APIC initial configuration.*

*Time synchronization plays a critical role in the Cisco ACI fabric. It is important for proper analysis of traffic flows and for correlating debug and fault timestamps across multiple fabric nodes. You must configure the Cisco ACI fabric with an active Network Time Protocol (NTP) policy to assure that the system clocks on all devices are correct. Atomic counters that can be used to detect drops and misrouting in the fabric also require an active fabric NTP policy.*

## Spine-Leaf Topology Benefits

*By using a spine-leaf topology, the fabric is easier to build, test, and support. Scalability is achieved by simply adding more leaf nodes if there are not enough ports to connect hosts. You can also add spine nodes if the fabric is too small to carry the load of the host traffic. The symmetrical topology allows for optimized forwarding behavior, needing only two hops for any host-to-host connection. The design allows a high-bandwidth, low-latency, low-oversubscription, and scalable solution at low cost.*

*In summary, the advantages of the spine-leaf topology include:*

- *Simple and consistent topology*

- *Scalability for connectivity and bandwidth*

- *Symmetry for optimization of forwarding behavior*

- *Least-cost design for high bandwidth*

## IS-IS Fabric Infrastructure Routing

*The fabric applies a densely tuned Intermediate System-to-Intermediate System (IS-IS) environment utilizing Level 1 connections within the topology for advertising loopback addresses. Loopback addresses are the Virtual Extensible LAN (VXLAN) tunnel endpoints (TEPs) that are used in the integrated overlay. TEPs are advertised to all other nodes in the fabric for overlay tunnel use.*

*IS-IS is responsible for infrastructure connectivity in Cisco ACI:*

- *IS-IS provides IP reachability among TEP addresses.*

- *It is automatically deployed, and no user intervention is necessary.*

- *No IS-IS knowledge is required.*

![IS-IS Fabric Infrastructure Routing](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/IS-IS_fabric.png)

## Endpoint Forwarding Across Leaf Switches

*When a packet transmits from one leaf to another, a TEP IP of each node identifies an end host (called an endpoint in Cisco ACI) location. User data traffic is encapsulated with the VXLAN header when being forwarded to another leaf. The forwarding across switch nodes is performed based on the TEP IP in the VXLAN encapsulation. In case the ingress leaf is unaware of the destination endpoint location (TEP), Cisco ACI has a distributed database that is called the Council of Oracles Protocol (COOP) on each spine. It knows all the mapping of endpoint and TEP.*

![Endpoint Forwarding Across Leaf Switches](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/ACI_endpoint_forwarding.png)

## Cisco Nexus 9000 Series Hardware

*The Cisco Nexus 9000 Series is the next generation of data center switching infrastructure. In Cisco ACI mode, the Cisco Nexus 9000 Series provides the spine and leaf switches that build the fabric. The Cisco Nexus 9000 Series offers a powerful combination of hardware and software that provides a robust and comprehensive solution.*

*The Cisco Nexus 9000 Series includes the following:*

- *Cisco Nexus 9500 Series modular chassis with 4, 8, or 16 slots.*

- *Cisco Nexus 9300 Series ToR and spine switches with different Cisco ACI spine and leaf varieties.*

- *Cisco Nexus 9500 Series line cards:*

1. *Cisco Nexus X9700 Series line cards for Cisco ACI spine switches*
	
2. *Cisco Nexus X9500 Series line cards for Cisco ACI leaf switches*
	
- *Cisco Nexus X9600 and X9400 Series line cards are standalone Cisco NX-OS cards that are not part of Cisco ACI.*

![X9600 and X9400 Series line cards](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/X9600-X9400_line_cards.png)

*Note: Cisco Nexus 9200 Series switches support only Cisco NX-OS mode, and you cannot use them for Cisco ACI.*

## Cisco APIC

*Cisco APIC is a policy controller. It relays the intended state of the policy to the fabric. The APIC does not represent the control plane and does not sit in the traffic path. The hardware consists of a group of three or more servers in a highly redundant array.*

*Cisco APIC has these roles:*

- *As the policy controller:*

1. *Holds the defined policy.*

2. *Represents the management plane, ot the control plane.*

3. *Not located in the traffic path.*

4. *Instantiates the policy changes.*

- *Is deployed as a redundant group of servers.*

![Cisco APIC](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/cisco_APIC.png)

*As shown in the figure, the ACI APIC performs fabric discovery. The APIC uses Link Layer Discovery Protocol (LLDP) to discover ACI switches and DHCP to set up IP addresses on the switches. Loopback addresses are the VXLAN TEPs used for IS-IS routing.*

*The Cisco APIC appliance has two form factors for medium or large configurations. Medium configurations have a medium-size CPU, hard drive, and memory for up to 1000 edge ports. Large configurations have a large-sized CPU, hard drive, and memory for more than 1000 edge ports.*

*A Cisco APIC appliance comprises either a group of Cisco Unified Computing System (Cisco UCS) C220 or C240 M5 as third-generation appliances. These devices are referred as Cisco APIC M3 or Cisco APIC Layer 3 and are intended for medium or large configurations. An APIC has Cisco UCS C220 or C240 M4 (Cisco APIC-M2/L2) as second-generation appliances or Cisco UCS C220 or C240 M3 (Cisco APIC-M1/L1) as first-generation appliances.*

*The Cisco APIC software is delivered on the Cisco UCS server appliances with an Secure Socket Layer (SSL) certificate that allows the hardware to run Cisco APIC software. The product consists of the server hardware and preinstalled Cisco APIC software. Since the hardware is Cisco UCS C-Series, it comes with Cisco Integrated Management Controller (Cisco IMC). Make sure that Cisco IMC is running a compatible version from an APIC release note as well.*

*Cisco APIC is redundant on multiple levels, including the interface level and group level. Cisco APIC is deployed in a group with a minimum of three controllers. The ultimate size of the controller group is directly proportionate to the size of the Cisco ACI deployment and is based on transaction-rate requirements. Any controller in the group can service any user for any operation, and you can add or remove a controller transparently from the group. APICs form a group and talk to each other using an infrastructure network that is provided by the leaf-and-spine topology.*

# Cisco ACI Policy Model

*The policy model manages the entire fabric, including infrastructure, authentication, security, services, applications, and diagnostics. Logical constructs in the policy model define how the fabric meets the needs of any fabric function. The logical construct of a typical Cisco ACI tenant network consists of tenants, VRFs, bridge domains (BDs), endpoint groups (EPGs), and contracts. Contracts are applied between EPGs for communication policy control that is based on allow lists.*

![ACI Policy Model](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/ACI_policy_model.png)

*The Cisco ACI manages all the configurations as objects stored in the management information tree (MIT) database. As an overview, policies can be categorized in four major groups, as shown in the figure:*

- ***Security Group (Security and Application Tenant Policies):*** *Defines how the Cisco ACI fabric should allow network communication between two devices. Example policies are EPGs and contracts, among others.*

- ***Overlay Network (Network Tenant Policies):*** *Defines the overlay network that goes over the Cisco ACI fabric. These policies will be the logical topology of user networks, and you can define them without worrying about the underlay. Example policies include VRF and bridge domain, among others.*

- ***Fabric Access (Access Policies):*** *Defines how end hosts or external network devices connect to the Cisco ACI fabric by configuring port-channel, vPC, and other interface-level configurations.*

- ***Underlay Network (Fabric Policies):*** *Defines the VXLAN underlay built by the Cisco ACI fabric. It includes the infrastructure Multiprotocol Border Gateway Protocol (MP-BGP) and other protocols to manage Cisco ACI switches such as NTP.*

### Additional Notes:

*ACI is basically a giant intent engine.* You don’t configure switches; you *describe what you want,* and the fabric figures out *how* to make it real. Everything is an object in the *MIT (Management Information Tree)*, which is Cisco’s way of saying “the fabric remembers everything as structured policy, not CLI scars.”

Mental model that actually sticks:

- **Tenants** = parallel universes (total isolation domains).

- **VRFs** = routing brains inside a tenant.

- **Bridge Domains (BDs)** = L2 neighborhoods.

- **EPGs** = groups of endpoints that *behave the same.*

- **Contracts** = explicit allow-lists saying who may talk to whom (default is silence).

**The four policy layers (top → bottom, intention → physics):**

- **Security Group** → *Who can talk to who* (EPGs + contracts, zero-trust vibes).

- **Overlay Network** → *Logical network shape* (VRFs, BDs, no underlay anxiety).

- **Fabric Access** → How things plug in (ports, vPCs, attachment rules).

- **Underlay Network** → *The hidden machine* (VXLAN, MP-BGP, NTP — the fabric’s nervous system).

## Cisco ACI Access Policies

*Access policies configure external-facing interfaces that connect to devices such as hypervisors, hosts, network-attached storage, routers, or fabric extender interfaces. Access policies enable the configuration of port channels and virtual port channels, protocols such as LLDP, Cisco Discovery Protocol, or Link Aggregation Control Protocol (LACP). They also enable features such as statistics gathering, monitoring, and diagnostics.*

*In addition to access policies, Cisco ACI uses fabric policies that define functions that are internal to the fabric. The key features of access and fabric policies are the following:*

- *Policies define protocols and settings.*

- *They enable configuration modularity and reusability.*

- *Global administrators manage policies, not per-tenant administrators.*

- *Access policies have these functions:*

1. *Attaching any endpoints to leaf and spine switches (mandatory)*

2. *Identifying the access interfaces on Cisco ACI switches*

3. *Authorizing encapsulation resources (VLAN)*

- *Fabric policies define fabric functions such as NTP, Domain Name Server (DNS), and the MP-BGP route reflector on spine switches.*

![Access Policies](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/ACI_access_policies.png)

*Access policies are grouped into the following categories:*

- ***Pools:*** *Specify VLAN and multicast address pools.*

- ***Interface profiles:*** *Specify which access interfaces to configure and the interface configuration policy.*

- ***Switch profiles:*** *Specify which switches to configure and the switch configuration policy.*

- ***Module profiles:*** *Specify which leaf module to configure. But as of release 4.1, no leaf model has more than one module. Hence this profile is typically never used.*

- ***Global policies:*** *Enable the configuration of DHCP, quality of service (QoS), and Attachable Access Entity Profile (AAEP).*

- ***Physical and external domains:*** *Define a domain that bundles a set of interfaces (AAEP) and encapsulations (VLAN pool) to allow other components.*

- ***Monitoring and troubleshooting policies:*** *Specify what to monitor, the thresholds, how to handle faults and logs, and how to perform diagnostics that relate to external-facing interfaces.*

## Cisco ACI Logical Constructs

*The following figure provides an overview of the Cisco ACI policy model logical constructs.*

![ACI Logical Constructs](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/ACI_logical_constructs.png)

*The following is the outline of the main components in the Cisco ACI Tenant.*

- ***Logical policy grouping:***

- *Tenant*

- *Application Profile*

- ***Network grouping:***

- *Virtual routing and forwarding*

	- *Unique Layer 3 forwarding domain*

	- *Relation to application profiles with their policies*

- *Bridge domain:*

	- *Layer 3 functions*

	- *Subnet and default gateway*

	- *Bridge domain is the same as broadcast domain*

- *Layer 3 Out*

- ***Security grouping:***

- *Endpoint group:*

	- *Named groups of related endpoints, for example, finance*
	
	- *Static or dynamic membership*
	
- *Contracts:*

	- *The rules that govern the interactions of EPGs.*
	
	- *Contracts determine how applications use the network.*

*At the top level, the Cisco APIC policy model is built on a series of one or more tenants. A tenant is a logical container for application policies that enable an administrator to exercise domain-based access control. The fabric can contain multiple tenants. A tenant represents a unit of isolation from a policy perspective, but it does not represent a VRF. Tenants can represent a customer in a service provider setting or an organization or domain in an enterprise setting. Or, it can be only a convenient grouping of policies.*

*A VRF instance is the largest network component in a tenant. It provides an IP address spaces and a Layer 3 forwarding domain just like a normal router. Each tenant has its own VRFs, and all tenant components such as endpoints can belong only to a VRF within the same tenant except for tenant common.*

*In Cisco ACI, instead of VLAN, a bridge domain is the Layer 2 Forwarding domain within the fabric. When a packet arrives, Cisco ACI maps the VLAN into an EPG. Each EPG belongs to a bridge domain that is the Cisco ACI Layer 2 domain. It performs bridging or MAC address lookup within the bridge domain.*

*Use EPGs to create logical groupings of hosts or servers (endpoints) that perform similar functions within the fabric. This concept is new in Cisco ACI; a typical network infrastructure did not have it by default. Cisco ACI defines multiple EPGs within a Layer 2 bridge domain on top of Layer 2 network separation for security isolation purposes. In a traditional network device, Layer 2 network separation is the smallest segmentation that is achieved via VLAN ID. However, since the Cisco ACI Layer 2 bridge domain is not directly tied to a VLAN ID, Cisco ACI can provide one more layers of segmentation. It uses a VLAN ID that is smaller than the Layer 2 domain (EPG). Hence, in Cisco ACI, EPG is a security segmentation smaller than the Layer 2 domain, and the VLAN ID is a parameter for security separation instead of Layer 2 network separation.*

*Since EPG is for security separation, no endpoints can talk to each other across EPGs unless it is explicitly allowed. A policy that is called a contract allows the communication. Any endpoints within a same EPG can talk to each other because they are not segmented from each other.*

***Key points to remember about the tenant components:***

- *A VRF in Cisco ACI has the same function and does not differ compared to a VRF used in a traditional router.*

- *In Cisco ACI, the Layer 2 Forwarding domain is called a bridge domain; you can define subnets with pervasive default gateways in bridge domains.*

- *You can use the VLAN ID for segmentation and mapping the appropriate endpoints to EPGs.*

*The following figure shows a sample design with the basic logical constructs. To the left, you can see a bridge domain with two subnets and hosts that are in either of the two subnets. Hosts from EPGs A and B can also communicate with hosts from EPG C in subnet D. To the right, you can see another VRF with a bridge domain and two subnets and hosts without logical connectivity to the first VRF.*

![ACI VRF Bridge Domains](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/ACI_VRF_bridge_domains.png)

## Application Profile

*Application profiles are groups of EPGs. Each application profile that you create can have a unique monitoring policy and QoS policy applied.*

![Application Profile](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/ACI_application_profile.png)

*In the example, a group of physical and virtual web servers form a single tier of a three-tier application. Communication between these tiers and the policies that define that communication make up the complete application. Within Cisco APIC, this complete application definition is known as an application profile. The inbound/outbound policies that control the communication between a pair of EPGs are known as contracts.*

*An application profile is a convenient logical container for grouping EPGs. It contains as many (or as few) EPGs as necessary that are logically related to providing the capabilities of an application. You can put multiple applications in a single application profile if it is easier for you to maintain.*

*Contracts provide a way for the Cisco ACI administrator to control traffic flow within the Cisco ACI fabric between EPGs. You use a provider-consumer model to build contracts, where one EPG provides the services that it wants to offer, and another EPG consumes the services.*

*Basically, contracts consist of one or more* ***subjects.*** *Each subject contains one or more* ***filters.*** *Each filter contains one or more* ***entries.*** *Each entry is equivalent to an* ***Access Control Entry (ACE)*** *in an access control list (ACL) that applies between EPGs. When the leaf knows the source and destination EPG for a packet, it checks the contract rules between them and decides whether to allow the packet.*

*Cisco ACI offers an allowlist model, and no communication is allowed between EPGs without a contract. Hence, the contract filters are typical to allow a certain type of traffic instead of deny. However, just like a normal ACL, you can also create the deny filter if you need it.*

***The following are the core principles of contracts:***

- *They define the policies using subjects and filters (the type of traffic to allow or deny) between EPGs.*

- *Communication between EPGs is not allowed without a contract.*

- *The traffic direction is based on how the contract is attached to EPGs (provider/consumer).*

*Contracts define the relationship between application tiers such as Layer 3–Layer 4 traffic filters and Layer 4–Layer 7 services. Contracts contain a list of* ***subjects*** *and can optionally have a QoS class and a service graph definition.* ***Subjects*** *represent* ***application bundles*** *that an application tier provides over the network and that the contract should permit. The subjects contain filters that allow access to specific applications. You may also use labels to group objects, such as subjects and EPGs, to further define policy enforcement.*

#  Cisco ACI External Connectivity Options

*The Cisco ACI fabric supports a wide range of methods to interconnect the fabric with external networks, data center environments, or segments.*

*In Cisco ACI, any end hosts or network devices that are learned as an endpoint via a normal EPG is considered “inside” the ACI fabric. Cisco ACI provides those endpoints with an exit to other network domains. These domains are referred to as “outside” or External Connections. External devices, such as routers that connect to the WAN and enterprise core (or to existing Layer 2 switches) connect to the front panel interface of a leaf switch. The leaf switch that provides such connectivity is known as a* ***border leaf.*** *You can configure the border leaf switch interface that connects to an external device as either a bridged or routed interface. In the case of a routed interface, you can use static or dynamic routing. The border leaf switch can also perform all the functions of a normal leaf switch.*

*This outside network could be another simple Layer 2 network with many non-ACI switches. The connection to such a network is called* ***Layer 2 External Network Connectivity,*** *which can be achieved by Layer 2 Out or EPG and VLAN Extension.*

*Or, it could be a Layer 3 network where Cisco ACI must learn about it via the routing protocol or static route. This one is called* ***Layer 3 External Network Connectivity,*** *which can be achieved by Layer 3 Out. It is often simply called* ***L3Out.*** *Layer 3 Outs are deployed on Cisco ACI leaf switches.*

![ACI External Connectivity Options](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/ACI_external_connectivity.png)

***Layer 3 Out to external networks has these characteristics:***

- *Links to a network that contains multiple subnets.*

- *Provides reachability via Open Shortest Path First (OSPF), BGP, Enhanced Interior Gateway Routing Protocol (EIGRP), or static routes.*

***Layer 2 Out or EPG and VLAN Extensions to external networks have these characteristics:***

- *Extend the Layer 2 domain (bridge domain) outside of the Cisco ACI fabric.*

- *Support the VLAN for tagging.*

*Note: You can have multiple external Layer 2 or Layer 3 network connectivity from various VRFs on the same port because of VLAN.*

# Cisco ACI and Virtual Machine Manager Integration

*You can integrate Cisco ACI transparently integrated into virtual environments. In virtual environments, Cisco ACI delivers simplicity without compromising infrastructure scale, performance, responsiveness, security, or end-to-end visibility. Cisco ACI enables you to use a common policy-based operating model across your physical and virtual environments.*

*A virtual machine manager* ***(VMM)*** *domain is a component to connect Cisco ACI policies with virtual switches that are managed by third-party virtual machine controllers such as VMware vCenter, Microsoft SCVMM, and others.*

***The key functionalities of VMM domains are as follows:***

- *Push Cisco ACI policy such as EPG to virtual machine controllers.*

- *Retrieve information such as virtual machine inventory from virtual machine controllers.*

*Cisco APIC can integrate with multiple hypervisors that are applying network policy and automatically detect endpoints and policy placement. The policy is consistently implemented in virtual and physical servers.*

![Virtual Machine Manager Integration](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/ACI_hypervisor_policies.png)

*The Cisco ACI–integrated overlay is optimized for multihypervisor encapsulation and normalizes the traffic when it is inside the fabric:*

- *Innovative integration with hypervisor management.*

- *Integrated gateway for VLAN and VXLAN networks, from virtual to physical.*

- *Normalization for VXLAN and VLAN networks*

- *Intelligent policy placement with a virtual machine that attaches to the network.*

- *Network policy tracking that is based on virtual machine mobility.*

## VMware vCenter VDS Integration

*The following outlines the workflow of how a VMM domain integrates vSphere Distributed Switch (VDS) and pushes policies to the virtual environment in the example of VMware vCenter.*

*Note: Cisco uses the term Distributed Virtual Switch (DVS) in the Cisco ACI GUI.*

![VMware vCenter VDS Integration](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/ACI_vmware_VDC_integration.png)

1. *The APIC administrator creates a VMM domain.*

2. *The Cisco APIC performs an initial handshake and open TCP session with VMware vCenter specified by a VMM domain.*

3. *The APIC creates the VMware VDS with the VMM domain name or uses an existing VDS if there is one already created (matching the name of the VMM domain). If you use an existing VDS, the VDS must be inside a folder on vCenter with the same name.*

4. *The vCenter administrator adds the ESXi host to the integrated VDS and assigns the ESXi host ports as uplinks on the integrated VDS. These uplinks must connect to the Cisco ACI leaf switches.*

5. *The APIC automatically detects the leaf interfaces that are connected to the integrated VDS via LLDP or CDP from the integrated VDS.*

6. *The APIC administrator creates EPGs and associates EPGs to the VMM domain.*

7. *Cisco APIC dynamically picks a VLAN for the associated EPG and maps it to a port group in vCenter.*

8. *vCenter creates a port group with the VLAN under the integrated VDS. The port group name is a concatenation of the tenant name, the application profile name, and the EPG name.*

9. *The APIC pushes policies to leaf switches. The same VLANs used for mapping EPGs to port groups can then be trunked over the leaf switch ports where the ESXi is connected to.*

10. *The vCenter administrator instantiates and assigns virtual machines to the port group.*

*When a packet from those virtual machines arrives in the Cisco ACI leaf, it will be classified into the EPG based on the VLAN. Cisco ACI will apply appropriate policies such as contracts.* ***No manual VLAN trunking is necessary.*** *The APIC also provides better visibility for virtual machines on the vCenter with the information from the data plane and vCenter.*

*Note: Cisco APIC does not maintain any synchronization between the VMM configuration and the VMware vCenter VDS configuration. If you directly change VDS settings from the VMware vCenter, Cisco APIC does not try to overwrite the user settings.*

### Additional Notes

*Core idea first:*

**ACI does** ***intent,*** **vCenter does** ***placement,*** **VLANs become invisible glue.** You never “configure networking for VMs” manually — APIC *orchestrates it into existence.*

*The workflow as a story your brain can replay:*

**1. APIC declares intent**

- You create a *VMM domain* → this is APIC saying: *“I want to control a VMware universe.”*

- APIC shakes hands with *vCenter over TCP* and gains authority.

**2. APIC shapes the virtual switch world**

- APIC *creates or adopts a VDS* (name must match the VMM domain — symmetry matters).

- vCenter admins plug *ESXi hosts into that VDS,* with uplinks physically landing on *ACI leafs.*

**3. Fabric awareness kicks in**

- APIC *auto-discovers which leaf ports face ESXi* using LLDP/CDP.

- No guessing, no spreadsheets, no “which cable was that again?”

**4. EPGs become port groups (the magic step)**

- You bind *EPGs to the VMM domain.*

- APIC *auto-assigns VLANs* and maps them to *vCenter port groups.*

- Port group names = ```Tenant | App Profile | EPG``` → readable, deterministic, sane.

**5. Policy flows downhill, not sideways**

- APIC pushes policy to *leaf switches automatically.*

- VLANs are *trunked without you touching trunks* (this is huge).

- VMs get attached to port groups — *they inherit policy by existence.*

**What actually happens to traffic (mental checkpoint):**

- VM sends packet → VLAN tags it → leaf maps VLAN → *EPG identified → contracts enforced.*

- Zero trust by default. No contract = silence.

**Important reality check (Cisco being honest for once):**

- ***APIC does NOT babysit vCenter***

- If you manually mess with the VDS in vCenter, APIC won’t fix or fight you.

- This is power with responsibility, not dictatorship.

One-sentence memory spell: *“APIC declares intent, vCenter instantiates it, VLANs disappear, and policy rules all.”*

# Cisco ACI and Layer 4–Layer 7 Integration

*Traditionally, when you insert Layer 4 to Layer 7 services into a network, you must perform a highly manual and complicated VLAN (Layer 2) or VRF instance (Layer 3) stitching between network elements and service appliances. In a traditional network, users must configure ACLs on various network devices. They must also configure the interface depending on the complicated traffic flow and the location of the firewall or load balancer. The location may even potentially change if the Layer 4 to Layer 7 device is deployed in the form of a virtual machine. When an application is retired, removing a service device configuration (such as firewall rules) is difficult.*

*Cisco ACI provides a new set of service insertion features. These features include implicit automation of service insertion by using the Cisco APIC as a central point of automation and policy control.*

![ACI and Layer 4–Layer 7 Integration](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/ACI_and_layer_4-7_integration.png)

*Cisco ACI technology provides the capability to insert Layer 4 through Layer 7 functions using an approach called a* ***service graph.*** *The Cisco ACI treats services as an integral part of an application. Any necessary services are treated as a* ***service graph that instantiates on the Cisco ACI fabric from the Cisco APIC.*** *Users define the service for the application, while* ***service graphs identify the set of network or service functions that the application needs.***

*After the graph is configured in the Cisco APIC, the Cisco APIC automatically configures the services according to the service function requirements that you specify in the service graph. The Cisco APIC also automatically configures the network according to the needs of the service function that you specify in the service graph. It requires no change in the service device.*

*The Cisco APIC can* ***use policy to manage both the network fabric and service appliances.*** *It is a critical part of the Cisco ACI architecture. This ability to automate service insertion eliminates the challenge of managing complex traffic-steering techniques. The service insertion feature provides a means for automating the insertion of physical and virtual devices with a consistent and familiar interface. It supports the service policy automation using a REST API with JSON and XML data formats.*

# Cisco ACI Management and Automation

*A fundamental difference between operating a Cisco ACI fabric and traditional network hardware is a single point of management architecture that the Cisco APIC facilitates. Cisco APIC provides access to configuration, management, monitoring, and health functions. It supports the APIs that enable Cisco ACI programmability and automation during management.*

*Cisco APIC enables automated provisioning and management for all switches in the Cisco ACI fabric. Cisco APIC is deployed as a group of multiple controllers that facilitate real-time monitoring and diagnostic and configuration management of the Cisco ACI fabric. APIC is a policy controller that relays the intended state of the policy to the fabric. Still,* ***it does not represent the control plane and does not sit in the traffic path.***

*When using Cisco ACI, you benefit from these advantages:*

- ***Single point of management controller-based architecture:*** *Cisco APIC delivers a single point of control, a central API, and repository of global data. It also provides a repository of policy data for Cisco ACI.*

- ***Stateless hardware:*** *The APIC group manages the leaf and spine switches in a stateless fashion, decoupling the hardware from the applied policy and switch configuration.*

- ***Desired state-driven consistency model:*** *Enables declarative control-based management, which the APIC dictates. Furthermore, each object is responsible for knowing its current state and the necessary steps to get to the desired state.*

*You can configure Cisco APIC through a GUI, CLI, and REST API with no risk of inconsistency between them. The underlying interface for all access methods is provided through a REST API. It modifies the contents of a synchronized database that replicates across all the APICs in a group and provides an abstraction layer between all interfaces.*

![APIC Configs](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/APIC_configs.png)

*The Cisco APIC GUI provides these features that facilitate access to the Cisco ACI fabric:*

- *It is based on universal web standards (HTML5), without requiring installers or plug-ins.*

- *It provides access to monitoring (statistics, faults, events, and audit logs) and operational and configuration data.*

- *It provides access to the APIC and the spine and leaf switches through a single sign-on mechanism.*

- *Communication with the APIC is established through RESTful APIs, which are available to third parties.*

*The APIC Cisco Nexus Operating System (Cisco NX-OS)–style CLI uses similar syntax and other conventions to the Cisco NX-OS CLI, but the APIC operating system differs from Cisco NX-OS Software. Many Cisco NX-OS CLI commands will not work or may have a different function on the APIC CLI.*

*The following example illustrates an SSH login to the APIC CLI and how to view the running configuration.*

```
login as: admin
Application Policy Infrastructure Controller
admin@apic's password: xxxxxxxxx
apic1# show running-config
# Command: show running-config
  aaa banner 'Application Policy Infrastructure Controller'
  aaa authentication login console
    exit
  aaa authentication login default
    exit
  aaa authentication login domain fallback
    exit
  bgp-fabric
    asn 65001
    route-reflector spine 201
    exit
<output omitted>
```

*As in Cisco NX-OS Software, you can execute CLI show commands to examine portions of the Cisco APIC configuration and view operational data. You can also change the APIC settings by entering configuration commands in the configuration mode. The CLI offers additional capabilities that you may know from the Cisco NX-OS CLI, such as command abbreviation, completion, negation, filtering, and history.*

*The REST API interface in the Cisco APIC accepts and returns HTTP or HTTPS messages that contain JSON or XML documents. It provides access to the management information tree (MIT) and allows manipulation of the state of managed objects (MOs) in the tree. The same REST interface is used by the APIC CLI, GUI, and SDK. Therefore, you can use various programming languages (like Python) for automation, while using standard REST methods and JSON or XML-encoded messages.*

```
Creation of a tenant (fvTenant):

POST http://apic/api/mo/uni.xml
```

## Cisco ACI Programmability

*Most current networks are built on hardware with tightly coupled software, while the administrators are managing the infrastructure through the CLI. In small environments, with static network configurations and static workloads, this approach might still be applicable. However, as the data center networks are accommodating dynamic applications with physical and virtualized workloads and different cloud solutions, the traditional approach for network management is no longer effective.*

*Cisco ACI uses an object model that is based on the promise theory. It provides a scalable control architecture with autonomous objects responsible for implementing the desired state changes that the Cisco APIC group provides. This approach is more scalable than traditional top-down management systems, which require detailed knowledge of low-level configurations and the current state. With the promise theory, desired state changes push down, and objects implement the changes, returning faults when required.*

*The Cisco ACI object-oriented data model is designed from the foundation for network programmability. At the device level, the operating system has been rewritten as a fully object-based switch operating system designed for the fabric. Cisco ACI provides programmability for the whole fabric, including hardware and software devices, using an integrated protocol. It also uses device packages with scripts for third-party devices, such as Layer 4 to Layer 7 devices, which currently do not natively support the Cisco ACI protocol. The Cisco ACI logical model is composed of the desired state that the elements and agents in the concrete model build and translate into network configuration.*

*Given the comprehensiveness of the programmability features available on Cisco ACI, everyone can benefit. The network engineering and design teams can benefit from the rapid time to provision large configurations and the consistency from the ability to automate all the moving parts. Their operations teams can utilize the information that is contained within the APIC to streamline their processes, gather better metrics, and correlate events more accurately. Hence, they can focus on operational needs and perform tasks faster, which can ultimately increase the customer satisfaction.*

## Logical and Physical Model Framework

*The Cisco ACI object-oriented data model, which is the core of Cisco ACI programmability, is compounded of two major parts:* ***logical*** *and* ***physical.***

![Logical and Physical Model Framework](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/APIC_logical_and_physical_models.png)

*The Cisco ACI model-based framework provides an elegant way to represent data. This approach enables comprehensive access to the underlying information model, providing policy abstraction, physical models, debugging, and implementation data. The* ***logical model*** *is the interface with the system, while the* ***concrete model*** *encompasses the hardware configuration on the nodes. Hence, you can use an open programmatic interface during integration and automation of network implementation tasks. You can access the Cisco ACI model framework over REST APIs, which opens the system for programmability.*

*Administrators or upper-level cloud management systems interact with the logical model through the API, CLI, or GUI.* ***The logical model is composed of the desired state that the elements and agents in the concrete model build and translate into the network configuration.*** *Changes to the logical model then push down to the physical model, which typically becomes the hardware configuration.*

## Management Information Tree

*The MIT in the Cisco ACI framework, which represents the logical model, contains all managed objects (MOs) in the system.* ***The MOs are abstract representations of a physical or logical entity that contains a set with the configuration and properties.*** *For example, chassis, cards, and ports are physical entities that are represented as MOs. Similarly, resource pools, user roles, service profiles, and policies are logical entities that are represented as MOs. At run time, all MOs are organized in the MIT, which provides structured and consistent access to all MOs in the system. All objects in the MIT exist under the root object.*

*All information is stored as objects in MIT that you can easily process programmatically. Examples include configuration, hardware components (such as leaf and fan), control plane status (such as OSPF), statistics (such as for the interface), and some logs (faults, events, and audit logs).*

*These objects are accessible through the REST API, and most operations in Cisco ACI use the REST API in the background. You can directly use the REST API to access the Cisco ACI fabric data, or you can use a GUI or Cisco NX-OS–style CLI. But in the background, it calls the REST API.*

![Management Information Tree](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/APIC_MIT.png)

*Since the MIT has a hierarchical nature and uses the* ***attribute system to identify object classes,*** *you can perform various queries based on these levels:*

- ***Tree level:*** *Enables you to discover components of a larger system, for example, a query that discovers cards and ports of a given switch chassis.*

- ***Class level:*** *Enables you to use queries that return all the objects of a given class such as the type of cards.*

- ***Object level:*** *Enables you to use the DN to return a specific object, for example, information for a specific port or chassis.*

*For all MIT queries, you can optionally return the entire subtree or a partial subtree. Also, the* ***role-based access control (RBAC) mechanism in the system dictates which objects return.*** *Therefore, you can access objects according to your rights in the system.*

## Cisco ACI Open APIs and Ecosystem

*Cisco ACI supports a rich ecosystem through its open programmatic interfaces, which is built around northbound and southbound APIs.*

![ACI Open APIs and Ecosystem](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/ACI_northbound_and_southbound_APIs.png)

*The northbound interfaces use a RESTful API for scripting access with languages (such as Python) and automation integration with tools in the DevOps area (such as Ansible, Chef, and Puppet). Also, it provides open REST API support for integration with various software solutions for automation, hypervisor management tools, monitoring tools, system management tools, and existing and new orchestration frameworks.*

*Cisco ACI uses the OpFlex as a southbound OpenAPI and protocol, allowing the APIC to manage the Cisco ACI fabric and elements. Since the OpFlex agent is present in the network devices, the APIC uses OpFlex to translate the intended object-based state to a rendered configuration on the device. OpFlex is supported over TCP, SSL, and HTTP communications using a device REST-based API on the network devices.* ***The devices in the network are referred as policy elements.*** *These elements can be Cisco Nexus 9000 Series switches, hypervisor switches, or Layer 4 to Layer 7 devices.*

*Also, OpFlex provides integration with third-party partner devices. Examples include F5, Citrix, Embrace, Palo Alto, A10, Sourcefire, and other non-ACI–integrated devices from Cisco, such as the Cisco Adaptive Security Appliance (ASA) firewall.*

*For northbound and southbound API references and tools, Cisco DevNet offers a single central repository. On this site, you can find learning materials for network programmability basics, APIs and tools, a developer sandbox, sample code on GitHub (includes scripts and libraries for developers of Cisco ACI), and other resources. Also, you can use this site to find communities of interest, access to support, and more topics on this subject.*

# Lab: Explore Cisco ACI

*Cisco ACI is a spine and leaf infrastructure with exceptional flexibility and policy-based configuration of the network. Since the internal communication of the Cisco ACI fabric is running over a VXLAN overlay, the control over the communication across the fabric is extremely granular and powerful.*

*The Cisco ACI solution is especially powerful in large environments, where users can apply complex configurations on the fly by creating policy contracts between policy elements. This action is also possible through the powerful API that is available on the Cisco ACI controller.*

*The APIC controller manages the Cisco ACI instance and provides the user interface for its configuration. In this discovery, you will explore the basics of the APIC interface and perform a basic API configuration task in a Cisco ACI environment.*

## Explore the Initial Cisco ACI Fabric Configuration

**Big picture (lock this in first):**

- *APIC = the brain* of ACI. Nothing meaningful happens without it.

- *Initial setup starts in CLI*, but *real work lives in the GUI.*

- The GUI is split into *panes*, each showing the fabric from a *different philosophical angle* (system, tenants, hardware, ops, etc.).

**Step 1: Access the APIC GUI**

- Open Chrome (important — other browsers can glitch)

- Navigate to: ```https://10.10.1.144/```

- Accept the SSL warning

- Log in as: ```admin / 1234QWer```

After initial CLI config, **this HTTPS interface is the primary control surface.**

**Step 2: System pane (fabric health & APICs)**

*Top menu → System*

- Default landing page = *Dashboard*

- What lives here:

	- Fabric status overview
	
	- APIC inventory
	
	- Licensing
	
	- Event logs
	
Think: *“Is the fabric alive and sane?”*

**Step 3: Tenants pane (logical ownership)**

*Top menu → Tenants*

- Tenants = *highest logical boundary*

- Always present:

	- ```common```
	
	- ```infra```
	
	- ```mgmt```
	
- Used for:

	- Multitenancy
	
	- Department / application separation
	
Think: *“Who owns what intent?”*

**Step 4: Fabric pane (physical reality)**

*Top menu → Fabric*

- Controls the *actual switches and cables*

- Two big policy zones:

	- *Fabric Policies* → underlay & infrastructure
	
	- *Access Policies* → how things plug in
	
**Explore a leaf:**

- Left pane → *Pod 1*

- Select *Leaf-1*

- Expand the triangle to reveal *device-specific policies*

*Key concepts:*

- Devices are grouped into *Pods*

- You can run *single-pod or multi-pod*

- Policies are *deeply hierarchical*

**Step 5: Topology views (perspective matters)**

- With *Leaf-1 selected:*

	- *Work pane → Topology*
	
	- Shows *only what Leaf-1 can see*
	
- Select *Pod-1 instead:*

	- *Work pane → Topology*
	
	- Displays *entire pod topology*
	
Think: *“Topology is always shown from a point of view.”*

**Step 6: Virtual Networking pane**

*Top menu → Virtual Networking*

- Inventory of *VM managers / controllers*

- Where VMM integrations (vCenter, etc.) live

Think: *“Where virtual worlds touch the fabric.”*

**Step 7: Admin pane (control & governance)**

*Top menu → Admin*

Used for:

- Authentication (AAA)

- Firmware upgrades

- Monitoring integrations

- External services

Think: *“Who is allowed to touch the brain?”*

**Step 8: Operations pane (visibility & telemetry)**

*Top menu → Operations*

Provides:

- Traffic path visualization

- Fabric capacity metrics

- Endpoint (EP) tracking

- Graph-based traffic maps

Think: *“What is actually happening right now?”*

**Step 9: Integrations pane**

*Top menu → Integrations*

- Control surface for *third-party integrations*

- Automation, monitoring, external systems

Think: *“How ACI talks to the outside world.”*

**Mental state of the world map:**

- *System* → fabric health & controllers

- *Tenants* → intent ownership

- *Fabric* → switches, cables, underlay

- *Virtual Networking* → hypervisors & VMs

- *Admin* → authority & lifecycle

- *Operations* → truth from the data plane

- *Integrations* → external tentacles

*If ACI were a city:*

- Tenants = laws

- Fabric = roads

- APIC = city hall

- Operations = CCTV

- Integrations = border crossings

## Explore the APIC Command Line Interface

**What the APIC CLI is:**

- Looks and feels like Cisco *NX-OS*

- Runs on *Linux under the hood*

- Used for:

	- Initial setup
	
	- Diagnostics
	
	- Fabric visibility
	
- *Not* where day-to-day ACI policy is built (that’s GUI / API)

Think: *“CLI = inspection + surgery, not design.”*

**Step 1: Connect to APIC via SSH**

- From Student VM → open PuTTY

- Protocol: SSH

- IP: ```10.10.1.144```

- Credentials: ```admin / 1234QWer```

Example session:

```
apic1# login as: admin 
Pre-authentication banner message from server:
| Application Policy Infrastructure Controller
End of banner message from server
admin@10.10.1.144's password: 1234QWer
User admin Last logged in: 2025-04-17T19:49:15.000+00:00 UTC from 10.10.1.11 to ip:10.10.1.144/24,fc00::/7 using REST
apic1#
```

Notice: login history already tracks *REST access* — API is first-class.

**Step 2: Explore available commands (```?```)**

- At the prompt:

```
apic1# ?
```

Partial output (NX-OS déjà vu):

```
 configure            Configuration Mode
 reload               Reload a Node
 show                 Show running system information
 terminal             Enable or disable pager
 where                Show the current mode

 bash                 Bash shell for unix commands
 fabric               Show fabric related information
```

- Press ```q``` to exit help

Think: *“NX-OS syntax, ACI semantics.”*

**Step 3: Enter global configuration mode**

```
apic1# configure terminal
apic1(config)#
```

Key difference vs NX-OS:

- *Show commands still work here*

- Config mode ≠ dangerous by default

Example:

```
apic1(config)# show clock
Time : 17:58:56.815 UTC Thu Apr 17 2025
```

**Step 4: Drop into Linux (bash)**

From config mode:

```
apic1(config)# bash
admin@apic1:~> exit
exit
apic1(config)#
```

Important truths:

- APIC is Linux-based

- You can use standard Linux commands

- You *cannot configure ACI policy* from bash

Think: *“Linux shell = diagnostics only.”*

**Step 5: Discover the hidden weapon — ```acidiag```**

- Not shown in ```?```

- Fabric diagnostics toolkit

Run it:

```
apic1(config)# acidiag
```

You’ll see a massive subcommand list:

```
acidiag fnvread
acidiag health
acidiag cluster
acidiag logs
...
```

If you run it without arguments, it errors — expected behavior.

**Step 6: Inspect fabric nodes (```acidiag fnvread```)**

This is the *money command.*

```
apic1(config)# acidiag fnvread
```

Output:

```
ID   Pod ID   Name      Serial Number   IP Address        Role    State
-----------------------------------------------------------------------
101      1   Leaf-1    TEP-1-101        10.0.144.64/32    leaf    active
102      1   Leaf-2    TEP-1-102        10.0.144.66/32    leaf    active
103      1   Spine-1  TEP-1-103        10.0.144.65/32    spine   active

Total 3 nodes
```

What this tells you:

- Node IDs

- Pod membership

- TEP (tunnel endpoint) IPs

- Role (leaf / spine)

- Operational state

Think: *“This is the CLI mirror of the fabric topology.”*

**Mental anchor:**

- *GUI* → intent & policy

- *CLI* → visibility & diagnostics

- *bash* → Linux internals

- *acidiag* → fabric truth serum

If NX-OS is a switch CLI, *APIC CLI is a control-plane stethoscope.*

## Explore the APIC API Interfaces

**Big picture (before steps):**

- *Everything in ACI is an object*

- *GUI, CLI, and API all manipulate the same objects*

- The APIC simply exposes *different lenses* into the same MIT (Management Information Tree)

Mental hook: *“GUI clicks = API calls wearing a disguise.”*

**1. API Inspector — watch the fabric think:**

*GUI path:*

- APIC GUI → *Top-right gear icon*

- Select *Show API Inspector*

*What this gives you:*

- A *real-time feed of every API call* APIC receives

- Includes calls triggered by:

	- GUI clicks
	
	- Background processes
	
	- Automation tools
	
Notes:

- The gear menu also exposes APIC-specific tools (help, version info)

- You can *close the API Inspector after opening* — the lesson is awareness, not endurance

Remember: *“Every click leaves an API footprint.”*

**2. Object Store (Visore) — the raw object browser:**

Open in a new Chrome tab:

```
https://10.10.1.144/visore.html
```

- Log in as: ```admin / 1234QWer```

What Visore is:

- A *direct browser of the APIC Management Information Tree*

- Similar in spirit to *Cisco UCS Manager Visore*

- No abstraction, no sugar

**3. Searching objects (fabricNode example):**

Steps:

- In the *search bar*, start typing: ```fabric```

- Observe:

	- Matches appear dynamically
	
	- Search is *substring-based,* not prefix-based
	
Select:

- ```fabricNode```

- Click *Run Query*

Result:

- All fabric nodes (leafs, spines, controllers) appear

- Same data you saw in:

	- Fabric pane
	
	- CLI (```acidiag fnvread```)
	
**4. Inspect the API response (this is key):**

- Click *Show URL and response of last query*

What to notice:

- Response format ≠ GUI table format

- *Values are identical*

- This is the *actual data model* used by:

	- GUI
	
	- CLI
	
	- REST API
	
Core truth: *“Different tools, same object schema.”*

**5. Distinguished Name (DN) — the object’s true identity:**

- In the response, locate the ```dn``` property

- DN = *Distinguished Name*

- It’s a *path through the object hierarchy*

Think of it as:

```
/fabric/pod-1/node-101
```

Memory anchor: *“DN is the filesystem path of the fabric.”*

**6. Follow the DN in the GUI:**

*GUI path:*

- APIC GUI → *Fabric pane*

- Expand *Pod 1*

- Select *Leaf-1*

Now:

- Right-click *Leaf-1*

- Choose *Open in Object Store Browser*

Result:

- You land back in Visore

- Same object

- Same properties

- Same DN

Insight: *“GUI navigation == DN traversal.”*

**7. Tenants as universal schemas:**

*GUI path:*

- APIC GUI → *Tenants pane*

- Locate tenant *common*

- Right-click → *Open in Object Store Browser*

Then:

- Click *Show URL and response of last query*

Why this matters:

- Tenant schema is *universal*

- ```common```, ```infra```, ```mgmtv, and your future tenants:

	- Same structure
	
	- Same API
	
	- Different names / DNs
	
This is the automation bridge: *“If I can read it, I can create it.”*

**Mental state of the world map:**

- *API Inspector* → shows *what APIC hears*

- *Visore/Object Store* → shows *what APIC knows*

- *DN* → shows *where an object lives*

- *GUI* → just a friendly API client

## Use APIC API to Create a New Cisco ACI Tenant

**Big mental model (read this first):**

- *Visore = read-only microscope*

- *Postman = scalpel*

- You *copy an existing object,* reshape it, authenticate, then *POST / DELETE* it

- Errors are *expected* — they teach the object contract

Memory hook: *“Clone → rename → authenticate → simplify → send.”*

**1. Bootstrap the API call from Visore:**

Why this approach:

- Writing JSON from scratch is painful

- Copying a *known-good schema* is fast and safe

Steps:

- Open *Postman* from the Student VM desktop

- In *Visore,* copy the *URL* of the tenant query (```tn-common```)

- Paste it into Postman

- Change request type: *GET → POST*

**2. Clarifying the “remove query-target” step (important!):**

*What happened here:*

- Visore URLs often include query filters like:

```
?query-target=self
```

- These are *read-only query modifiers*

- POST requests *must target an object path,* not a filtered query

*What you did in Postman:*

- Open *Query Params*

- Uncheck ```query-target```

- This removes it from the URL automatically

Remember: *“query-target is for reading, not creating.”*

**3. Move the Visore response into Postman:**

Steps:

- In Visore → click *Copy Response*

- In Postman:

	- Go to *Body → raw*
	
	- Paste the response JSON
	
Now examine what you have (this is gold):

- No protocol (```https://```)

- No target system

- Points to ```tn-common.json```

- Nested too deeply (parent + child objects)

- Valid tenant schema

**4. Fix the URL (object targeting):**

*Step 1: add protocol + APIC IP*

```
https://10.10.1.144/api/node/mo/uni/tn-common.json
```

*Step 2: point to a* ***new tenant*** *object*

```
https://10.10.1.144/api/node/mo/uni/tn-dcfndu.json
```

Rule: *“Filename = object you are creating.”*

**5. De-nest the JSON (this always trips people):**

*Problem:*

- Visore responses include parent context

- POST expects *only the object being created*

*What to keep:*

```
{
  "fvTenant": {
    "attributes": {
      ...
    }
  }
}
```

*What to remove:*

- Everything above ```fvTenant```

- Everything below it

- Extra closing brackets

Think: *“One POST = one object.”*

**6. Rename the tenant cleanly:**

Steps:

- In Postman raw editor:

	- Find ```common```
	
	- Replace *all instances* with ```dcfndu```
	
- You should see *three replacements*

This updates:

- ```dn```

- ```rn```

- ```name```

**7. First POST attempt → expected failure (403):**

- Click *Send*

- Receive *HTTP 403*

Meaning:

- Not authenticated

- APIC rejected the request

Translation: *“Who are you?”*

**8. Authenticate with APIC:**

Create a new Postman tab:

*URL*

```
https://10.10.1.144/api/aaaLogin.json
```

*Method*

- POST

*Body → raw*

```
{
  "aaaUser": {
    "attributes": {
      "name": "admin",
      "pwd": "1234QWer"
    }
  }
}
```

- Click *Send*

- Verify *200 OK*

Cookie expires after *10 minutes.*

- If you get another 403 later → re-run this

**9. Retry tenant creation (second failure, also expected):**

- Re-send the tenant POST

- It fails again

Why:

- *Too many attributes*

- APIC is strict about object creation

**10. Minimal viable tenant (this is the key insight):**

Reduce ```fvTenant``` attributes to *only:*

```
"attributes": {
  "dn": "uni/tn-dcfndu",
  "name": "dcfndu",
  "rn": "tn-dcfndu",
  "status": "created"
}
```

Rules:

- No trailing comma

- Commas only between attributes

Click *Send:*

- *200 OK*

**11. Verify in the GUI:**

*APIC GUI:*

- Top menu → *Tenants*

- Confirm tenant ```dcfndu``` exists

You just created a tenant *purely via API.*

**12. Delete the tenant via API:**

In Postman:

- Change method: *POST → DELETE*

- Click *Send*

- Verify *200 OK*

Back in GUI:

- *Tenants pane*

- ```dcfndu``` is gone

Same object, different action — standardized verbs.

**Mental state of the world map:**

- *Visore teaches structure*

- *Postman enforces discipline*

- *403 errors teach authentication*

- *Attribute pruning teaches object contracts*

- *DELETE proves symmetry*

# Cisco ACI Anywhere

*Organizations are always trying to ensure proper alignment between IT capabilities and various business requirements (size and scale) that create disparate demands on data center networks. However, the needs of massively scalable data centers, service provider cloud solutions, and the mass market differ greatly. A single organization may have multiple data centers, each with different requirements and business usage. Some applications may be best suited for hosting on premises. Other applications may be best suited for hosting in a public cloud, and yet others may benefit from hybrid deployments. In fact, hybrid cloud is becoming the new normal for many businesses.*

*Cisco ACI Anywhere offers capabilities that enable seamless connectivity between the on-premises data center, remote small-scale data centers, and geographically dispersed multiple data centers under a single pane of policy orchestration. It can extend these capabilities to the public cloud also. Cisco ACI anywhere uses policy-driven abstraction on top of cloud-native APIs, regardless of the type of workload (physical, virtual, or containerized) across on-premises or public cloud deployments.*

*For example, a cloud service provider can have its own data center infrastructure for internal operations and another infrastructure for its customers’ cloud services. The data centers may be positioned in a single location, in multiple floors or buildings, or in multiple locations that require interconnection. Some workloads can be hosted on the public clouds.*

![ACI Anywhere](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/ACI_anywhere.png)

*With the increasing adoption of Cisco ACI as a pervasive data center fabric technology, enterprises and service providers commonly must interconnect separate Cisco ACI fabrics. They also must extend its capabilities into public clouds. This action enables a common policy-driven approach to management. The figure shows the various Cisco ACI fabric and policy domain extension options.*

*One site (like Site A in the figure) consists of a classic leaf-and-spine two-tier fabric (a single pod). In this configuration, all the deployed leaf nodes are fully meshed with all the deployed spine nodes. A single instance of Cisco ACI control-plane protocols runs between all the network devices within the pod. The entire pod is under the management of a single APIC group, which also represents the single point of policy definition.*

*The next option is to geographically separate the data centers, like Site A and Site B in the figure, where you can use the Cisco ACI Multi-Pod solution to manage the separated sites with a single APIC group. Each site has its own leaf-and-spine two-tier architecture. The main advantage of the Cisco ACI Multi-Pod design is hence operational simplicity, with separate pods managed as if they were logically a single entity. You can spread the leaf switches across different floors or buildings, while connectivity between pods establishes through the spine switches in different pods and an* ***interpod network (IPN).*** *You can provision WAN routers in the IPN while directly connecting them to the spine switches, or you can provide WAN connectivity through the border leaf switches.*

*The need for complete isolation across separate Cisco ACI networks led to the* ***Cisco ACI Multi-Site architecture.*** *Cisco ACI Multi-Site offers connectivity between the two completely independent ACI fabrics (sites). Each ACI fabric has an independent APIC group and control plane to provide complete fault isolation.* ***BGP Ethernet VPN (EVPN) exchanges control plane information between ACI sites.*** *VXLAN is used for data-plane communication between ACI sites and to extend the policy domain by carrying the* ***policy information in the VXLAN header.*** *A Cisco* ***Multi-Site Orchestrator (MSO)*** *manages the Cisco ACI fabrics in the multisite solution. MSO is a software solution that represents a single point of policy orchestration and visibility across multiple geographically dispersed ACI sites.*

*The development of the remote leaf architecture extends connectivity and consistent policies to remote locations where it is impossible or undesirable to deploy a full ACI pod (with physical leaf and spine nodes). With Cisco* ***Remote Leaf solutions,*** *the APIC controller that is deployed in the Cisco* ***ACI main data center*** *manages the remote leaf switches connected over a* ***generic IPN.*** *Remote location data centers may not be large, hence the Cisco Remote Leaf solution allows deployment of only leaf switches, while the* ***spines remain in the main Cisco ACI data center.*** *The APIC controller manages and operates the remote leaf nodes as if they were local leaf switches and pushes all the centrally defined ACI policies.*

*The Cisco ACI Virtual Pod architecture extends the Cisco ACI fabric to existing data centers, bare-metal clouds, remote locations, or colocation facilities where it is impossible or undesirable to deploy physical ACI equipment.*

*The Cisco ACI* ***Virtual Pod (vPod)*** *architecture allows you to* ***extend an existing ACI fabric by introducing the concept of a software-only pod.*** *This virtual pod is similar to a physical pod in the multipod architecture. A vPod interconnects with the physical ACI fabric using a generic IP network. The Cisco ACI vPod deployment remains functionally a single fabric, with all the nodes deployed across the physical and virtual pods under the control of a* ***single APIC group.*** *The main advantage of the Cisco ACI vPod design is the ability to deploy a Cisco ACI pod on an* ***existing physical infrastructure.*** *It removes the need to buy additional network hardware to achieve this functionality.*

*In a hybrid cloud environment, it is becoming more challenging to maintain a homogeneous enterprise operational model, comply with corporate security policies, and gain visibility across hybrid environments. The Cisco Cloud ACI solution extends the capabilities of Cisco ACI into public cloud environments. The* ***Cisco Cloud ACI*** *provides consistent policy management and visibility across multiple on-premises data centers and public clouds or hybrid cloud environments with the help of* ***Cisco MSO.*** *MSO can manage policies across multiple on-premises Cisco ACI data centers and public clouds.*

*The following table reviews the major deployment types:*

![ACI Anywhere Deployment Types](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/ACI_anywhere_deployments.png)

*Note: Learn more about deployment options in these links:*

- *[Cisco ACI Multi-tier Architecture White Paper](https://www.cisco.com/c/en/us/solutions/data-center-virtualization/application-centric-infrastructure/white-paper-c11-742214.html)*

- *[Cisco APIC Layer 3 Networking Configuration Guide, Release 5.0(x)](https://www.cisco.com/c/en/us/td/docs/switches/datacenter/aci/apic/sw/5-x/l3-configuration/cisco-apic-layer-3-networking-configuration-guide-50x.html)*

- *[Cisco ACI Virtual Pod Getting Started Guide, Release 5.0(x)](https://www.cisco.com/c/en/us/td/docs/switches/datacenter/aci/aci_vpod/getting-started/5-x/cisco-aci-virtual-pod-getting-started-guide-50x.html)*

- *[Cisco ACI Multi-Site Fundamentals Guide, Release 3.1(x)](https://www.cisco.com/c/en/us/td/docs/dcn/mso/3x/fundamentals/cisco-aci-multi-site-fundamentals-guide-311.html)*

- *[Cisco Cloud ACI on AWS White Paper](https://www.cisco.com/c/en/us/solutions/collateral/data-center-virtualization/application-centric-infrastructure/white-paper-c11-741998.html)*

## Cisco Cloud ACI

*Cisco Cloud APIC is a software deployment of Cisco APIC that you deploy on a cloud-based virtual machine. Cisco Cloud APIC runs natively on supported public clouds to provide automated connectivity, policy translation, and enhanced visibility of workloads in the public cloud.*

![Cisco Cloud APIC](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/cisco_cloud_APIC.png)

*This figure shows the overall high-level architecture of Cisco Cloud ACI with* ***Cisco ACI MSO acting as a central policy controller.*** *It manages policies across multiple on-premises Cisco ACI data centers and hybrid environments, with each cloud site abstracted by its own Cloud APICs.*

*Cisco Cloud APIC brings a suite of capabilities to extend on-premises data centers into true hybrid cloud architectures. It helps drive policy and operational consistency regardless of where the applications reside. Cisco Cloud APIC capabilities include:*

- *Providing an interface that is similar to the existing Cisco APIC to interact with the Amazon Web Services (AWS) and Azure public clouds.*

- *Automating the deployment and configuration of cloud constructs.*

- *Configuring the cloud router control plane.*

- *Configuring the data path between the on-premises Cisco ACI fabric and the cloud site.*

- *Translating Cisco ACI policies to a cloud-native construct.*

- *Discovering endpoints.*

- *Providing a consistent policy, security, and analytics for workloads deployed either on or across on-premises data centers and the public cloud.*

- *Providing an automated connection between on-premises data centers and the public cloud with provisioning and monitoring.*

- *Policies that Cisco MultiSite Orchestrator pushes to the on-premises and cloud sites. Cisco Cloud APIC translates the policies to the cloud to keep the policies consistent with the on-premises site.*

### Summary

*Now you should have a good foundation of the following:*

- *Cisco ACI as a comprehensive SDN architecture designed for data centers.*

- *The Cisco ACI provision of policy-based automation combining physical and virtual environments through a unified model.*

- *Benefits of Cisco ACI extending to various IT teams, such as SDN, cloud, DevOps, and security.*

- *Simplification of provisioning and resource management across diverse environments through Cisco ACI.*

- *Enhancement of agility to address evolving business requirements and the significant business value that Cisco ACI adds.*
