# Describing Network Virtualization

*Businesses must provide high availability for applications while keeping operating expenses low. Applications must always be available, in all places, with optimal response times. Virtualization, multitenancy, and other advancements place increasing demands on the network. This connectivity must be provided without making changes to end systems or by compromising the stability of the overall network.*

*Overlays are independent of the underlying infrastructure technologies and services. They typically do not impose restrictions on the underlying infrastructure, provided the overlays can transport IP packets.*

*In the VMware environment, the network is virtualized. Most network components are virtualized, except for the network interface card (NIC), which resides in the host. Physical NICs usually act as uplink ports in the vSwitches that are created at the VMware hypervisor level.*

*In this module, you will learn the basic concepts of network overlays in data center design and the VMware vSwitch, including its function in the data center virtual infrastructure design.*

## Overlay Network Protocols

*An overlay network is a virtualized network that uses physical infrastructure for its operation but works as its own network with its own services and infrastructure nodes. Nodes in the overlay network are connected by virtual links that define a path through physical links in an underlying network. The underlying physical network must be considered when designing or managing the overlay network.*

*The figure shows a network with physical nodes that connect with physical links.*

![Physical Nodes](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/physical_nodes.png)

*The underlying networks for data centers should typically provide the following:*

- *High-capacity resilient fabric*

- *Intelligent packet processing*

- *Programmability and manageability*

*The figure displays two examples of overlay networks that are built on top of an underlying network.*

![Overlay Networks](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/overlay_networks.png)

![Overlay Networks 2](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/overlay_networks2.png)

*The overlay network presents new capabilities and features:*

- ***Mobility:*** *This capability tracks endpoints that are attached at the edges.*

- ***Scale:*** *This capability reduces the core state by distributing and partitioning the state to the network edge.*

- ***Flexibility and programmability:*** *This capability reduces the number of touch points.*

*Tunneling protocols such as Virtual Extensible LAN (VXLAN) and Network Virtualization Using Generic Routing Encapsulation (NVGRE) are available to enable virtual networks to be layered over a physical network infrastructure.*

### Overlay Network Service Types

*An overlay network relies on encapsulation to connect its virtual nodes. The traffic of a virtual network can be encapsulated in various layers of the Open Systems Interconnection (OSI) model.*

*Each encapsulation type has its advantages and disadvantages, which are important when designing a network infrastructure or adapting to an existing physical network.*

### Layer 2 Overlay

*The figure shows a Layer 2 overlay that is set up on top of an existing network.*

![Layer 2 Overlay](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/layer2_overlay.png)

*Typical functions of Layer 2 overlays are the following:*

- *Layer 2 LAN segment is emulated.*

- *Forwarding is based on Ethernet frame headers and transports IP and non-IP packets.*

- *Single subnet mobility (single Layer 2 domain) is created.*

- *Exposure to open Layer 2 flooding.*

*Layer 2 overlays are useful in emulating physical topologies. VXLAN is an example of a Layer 2 overlay that is tunneled over a Layer 3 network.*

### Layer 3 Overlay

*The figure illustrates a Layer 3 overlay that is set up on top of an existing network.*

![Layer 3 Overlay](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/layer3_overlay.png)

*Typical functions of Layer 3 overlays are the following:*

- *Abstract IP-based connectivity*

- *Transport IP packets*

- *Full mobility regardless of subnets*

- *Contained network-related failures (floods)*

*Layer 3 overlays are useful in abstracting connectivity and policy. NVGRE involves creating virtual Layer 2 or Layer 3 topologies on top of an arbitrary physical Layer 2 or Layer 3 network.*

### Network Virtualization Using GRE

*NVGRE is a tunneling protocol that Microsoft proposed as a Hyper-V solution. The protocol employs Generic Routing Encapsulation (GRE) to tunnel Layer 2 packets over Layer 3 networks.*

*The main features of NVGRE are the following:*

- *NVGRE creates virtual Layer 2 or Layer 3 topologies on top of an arbitrary physical Layer 2 or Layer 3 network.*

- *Connectivity in the virtual topology is provided by tunneling Ethernet frames in IP over the physical network.*

- *Virtual broadcast domains are realized as multicast distribution trees. The multicast distribution trees are analogous to the VLAN broadcast domains.*

- *Every virtual Layer 2 network is associated with a 24-bit identifier, called a virtual subnet identifier (VSID).*

- *A 24-bit VSID allows up to 16 million virtual subnets in the same management domain in contrast to only 4000 that are achievable with VLANs.*

- *Each VSID represents a virtual Layer 2 broadcast domain.*

*In the following figure, you can see NVGRE communication. Imagine that traffic must transport from the virtual machine with the IP address 10.0.0.5 and the virtual machine with IP address 10.0.0.7.*

*The original IP packet is encapsulated with the MAC header containing MAC addresses of the source and destination virtual machines. Then, a GRE header is added that contains a VSID for identifying each virtual network. Lastly, the outer IP header with the source and destination IP address of tunnel endpoints is added.*

![NVGRE](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/nvgre.png)

*Both VXLAN and NVGRE are used to overcome the limits of VLAN and offer the same functionality with only a few differences. Both methods are used to create up to 16 million virtual networks. The only difference is that NVGRE allows you to create either Layer 2 or Layer 3 networks, while VXLAN allows the creation of only Layer 2 segments.*

*Other differences between those two methods include an IP protocol and a difference in the packet header. VXLAN uses UDP, while NVGRE uses the GRE IP protocol, which means that there is no UDP header with the source and destination UDP ports.*

## VXLAN Overlay

*In modern data centers, a primary benefit of virtualization is the ability to move virtual machines between data centers while preserving the network configurations of the migrated virtual machines. To support mobility, virtual machines must remain in their native IP subnet, which ensures continuous network connectivity from the virtual machine to users. IP subnetting limits the virtual machine mobility domain to those hypervisors whose virtual switches are on common subnets.*

*Virtualization places increased demands on network designers. There is a need for more MAC address entries on switches. Wider Layer 2 networks are required to support mobility. Those Layer 2 networks run the Spanning Tree Protocol (STP), which blocks redundant links and therefore limits network bandwidth. At the same time, multitenancy requires segmentation between customers.*

*However, in a multitenant environment, you may have a duplication of virtual LAN (VLAN) numbers. There is also a growing need for more VLANs. The current limit of 4096 is inadequate.*

*You can overcome all these challenges with a VXLAN overlay network.*

### VXLAN Overview

*VXLAN is a tunneling protocol that encapsulates a Layer 2 frame with the MAC-in-UDP method to stretch Layer 2 connections over the underlying Layer 3 network.*

*To comprehend the VXLAN operation, you must familiarize yourself with three important terms:*

- ***Virtual network instance (VNI):*** *Each VNI is a separate network that runs over the physical underlay network and provides traffic isolation. VLANs are then mapped to a VNI to extend a VLAN across Layer 3 infrastructure. VNI can also be referred to as bridge domain or overlay.*

- ***VXLAN network identifier (VNID):*** *This unique 24-bit identifier is added to an original frame. It can be compared to a VLAN identifier field and provides a unique identifier for the individual VXLAN segment (VNI).*

- ***VXLAN tunnel endpoint (VTEP):*** *Every router or switch that participates in VXLAN by doing encapsulation and de-encapsulation is called VTEP. Each VTEP has two interface types that provide connectivity between the overlay and underlay network. These types include one or more VNI interfaces and a regular interface called the VTEP interface that tunnels VNI interfaces between VTEPs. Each VTEP is assigned one or more IP addresses that are used as the source IP address when encapsulating MAC address frames to transmit on the network.*

*The figure shows two VTEP devices with one VTEP interface each. You can also see end devices connected to the VTEP device.*

![VTEP Devices](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vtep_devies.png)

*The VXLAN VNI tunnel (or overlay) keeps the traffic within it segregated from other traffic in other VXLANs. This functionality is similar to virtual routing and forwarding (VRF) or VPN isolation. Such an approach provides multitenancy in terms of security and scale. Using standard VLANs that have 12 bits to identify a unique Layer 2 network works well, but it is limited in scale (4096 VLAN IDs).*

*It is also restricted to the Layer 2 domain where the VLAN is configured unless you route the packets. Techniques such as IEEE 802.1Q-in-Q overlays use an extra outer VLAN header, but scalability is restricted, and you can arrange only a bridged topology, not a routable one.*

*VXLAN is supported and can be implemented on hardware and software:*

- ***Hypervisor-based virtual switches:*** *These switches allow scalable virtual machine deployments.*

- ***Physical switches:*** *These switches allow bridging of VXLAN segments back into VLAN segments:*

*1. The physical switch represents a VTEP and functions as a VXLAN.*

*2. Physical switches that act as a VXLAN gateway allow you to extend overlays between the two virtual machines and bare metal servers.*

*You can use VXLAN technology with the Cisco Nexus 9000 Series Switches in Cisco Nexus Operating System (Cisco NX-OS) mode. Also, VXLAN is used extensively with the Cisco Nexus 9000 Series switches in Cisco Application Centric Infrastructure (Cisco ACI) mode. It uniquely provides any-to-any connectivity and contains network policy information in the unused header bits for security and quality of service (QoS) features.*

![VXLAN Mechanism](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vxlan_mechanism.png)

*The figure shows an example of a VXLAN mechanism. On the left, you can see two servers, the first one is in VLAN 10 and the second one is in VLAN 20. You can also see two groups of virtual machines in the figure, with each group in a different VLAN. Connectivity between virtual machines and servers over the underlay Layer 3 network is possible by using two VNIs (each marked by a different color). The figure also indicates that VTEP tunnels can be terminated on physical switches and software virtual switches on hypervisors.*

*Imagine that one of the virtual machines in VLAN 10 must be migrated to the left server, which is in VLAN 10. This migration is possible because VLAN 10 is mapped the same VNI on both VTEPs.*

*When traffic reaches the VTEP device, in this case the leaf switch, it is encapsulated. The original frame stays intact, and on top of it are added the VXLAN header, UDP header, IP header, and lastly an outer MAC header. The VTEP then sends encapsulated traffic over the Layer 3 network to the destination VTEP where the traffic is de-encapsulated.*

*Once the headers are removed, the server receives the original unmodified frame. For this reason, it appears that virtual machines are on the same local subnet as the server on the left and can be moved without changing their IP address.*

### VXLAN Benefits

*The three motivating factors for VXLAN in traditional networks are great scalability, isolation for multitenancy, and any-to-any Layer 2 communications.*

![VXLAN Benefits](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vxlan_benefits.png)

*The first issue that VXLAN solves is scalability. Modern data centers are getting bigger and more complex. For security reasons, they use VLANs to segment the LAN. One problem is that the use of VLANs provides only 4094 Layer 2 segments, and that number might not be enough. VXLAN with its 24-bit VNI field provides 16 million isolated segments.*

*Increased use of virtualization also requires wider Layer 2 networks for virtual machine mobility. With VXLAN, you can extend Layer 2 segments over the underlying shared network infrastructure so that you can place workloads across physical pods in the data center. VXLAN allows you to move a virtual machine between hosts that are on different VLANs without changing the virtual machine IP address.*

*VXLAN also simplifies the network and allows you to better utilize all available network paths instead of blocking redundant connections with STP. VXLAN packets transfer through the underlying network based on Layer 3 headers, and you can use Equal-Cost Multipath (ECMP). Therefore, it can take complete advantage of Layer 3 routing and use all available paths and bandwidth to load-balance the traffic.*

*Another benefit of VXLAN is that it is supported not only on hardware devices but also software ones, such as virtual switches inside the ESXi hypervisor. On a hypervisor, it provides scalable virtual machine deployments. On physical switches, it allows you to bridge VXLAN segments back into VLAN segments.*

### VXLAN Frame Format

*A VXLAN frame adds 54 bytes to the original Layer 2 frame after encapsulation. This overhead includes the outer MAC header, outer IP header, outer UDP header, and a VXLAN header.*

![VXLAN Fields](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vxlan_fields.png)

*The VXLAN fields and headers are as follows:*

- *The original Layer 2 Ethernet frame with its own MAC header includes the source MAC address, destination MAC addresses, Ethernet type, plus an optional VLAN. One use case of the inner VLAN tag is with virtual machine-based VLAN tagging in a virtualized environment. The original Ethernet frame is not changing at all.*

*The VXLAN header includes the following parts:*

***1. Flags (8 bits):*** *In this part, the “I flag” must be set to 1 for a VNI. The other 7 bits (designated “R”) are reserved fields and must be set to zero.*

***2. VXLAN Segment ID (VNID):*** *In this part, a 24-bit value designates the individual VXLAN overlay network on which the communicating virtual machines are situated. Virtual machines in various VXLAN overlay networks cannot communicate with each other.*

***3. Reserved fields (24 and 8 bits):*** *In this part, the fields must be set to zero.*

- *The UDP header uses a source port number that is calculated using a hash of fields from the inner packet and the destination port. The destination port is the well-known UDP port 4789. The hashed source enables a level of entropy for ECMP and load balancing of traffic across the VXLAN overlay. The UDP checksum field is set to zero. Optionally, if the encapsulating endpoint includes a nonzero UDP checksum, it must be correctly calculated across the entire packet, or the receiver may discard the packet.*

- *The outer IP header includes the source IP address that is the address of the source VTEP. The destination IP address can be a unicast or multicast IP address. If it is a unicast IP address, it represents the IP address of the destination (peer) VTEP.*

- *The outer MAC header includes the outer source MAC address. This address is set to the address of your local VTEP and the destination MAC address, which is usually the next-hop Layer 3 router. The outer VLAN tag is optional. If present, it may be used for delineating VXLAN traffic on the LAN.*

## VXLAN BGP EVPN Control Plane

*The scalability of the overlay network depends on if it can manage broadcast, unknown unicast, and multicast data (BUM) traffic. The control plane of overlay network technology defines how to manage BUM traffic. In VXLAN, the standard does not describe the control plane signaling protocol for determining the location of endpoints. Therefore, you can choose the control plane implementation that fits your particular network environment.*

*Two of the most widely used control planes for VXLAN technology with Cisco equipment are as follows:*

- *Multicast control plane (flood-and-learn)*

- *Multiprotocol Border Gateway Protocol (MP-BGP) Ethernet VPN (EVPN) control plane*

### Multicast Control Plane (Flood-and-Learn): ARP Request

*The first type of VXLAN control plane operation is the flood-and-learn mode that uses a multicast-enabled transport IP network. In this mode, the process of traffic-forwarding triggers end-host information learning and VTEP discovery. There is no control protocol to distribute end-host reachability information among VTEPs.*

*For the flood-and-learn control plane type, the transport IP infrastructure must support any-source multicast (ASM). Every VTEP that you configure for a particular VXLAN with a certain VNI will join the same multicast group. Initially, each VTEP will learn only the MAC addresses of its local end hosts and virtual machines. To learn remote MAC addresses, your VTEP will use the conversational MAC address learning technique.*

*This mechanism works as shown in the figure.*

![Flood-and-Learn](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/flood_and_learn.png)

*For example, End System A must send some data to End System B.*

*1. End System A generates an ARP request to discover the MAC address of End System B. The ARP request goes with the source MAC address MAC-A, and the destination MAC address is broadcast (FF:FF:FF:FF:FF:FF). When the VTEP receives the Layer 2 frame, it looks up its local table for the proper destination for this frame. It can be a local interface or remote VTEP IP address.*

*2. In BUM traffic, VTEP encapsulates the original Layer 2 frame and sends it over the multicast group that you configured for the VNI. So, the VTEP adds the VXLAN, outer UDP, IP, and Ethernet headers to your original ARP request. In the outer IP header, you can see the multicast address (239.1.1.1) as the packet destination IP address. It allows you to deliver that packet to all VTEPs that work with the same VNI. For the outer destination MAC address, your VTEP also uses the multicast MAC address (01:00:5E:01:01:01). The VTEP obtained this value from the known IP multicast address. The VTEP next forwards the encapsulated Layer 2 frame to the multicast rendezvous point (RP), which forwards a copy of the packet to every VTEP that has joined the multicast group.*

*3. Each VTEP receives and de-encapsulates the VXLAN packet and learns the MAC address of End System A (MAC-A) pointing to the remote VTEP address (IP-1).*

*4. Each VTEP forwards the ARP request to its local network.*

### Multicast Control Plane (Flood-and-Learn): ARP Response

*At this moment, End System B received an ARP request from End System A. The next step is to send the ARP response back to End System A.*

![ARP Response](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/arp_response.png)

*1. End System B generates a unicast ARP response with the source MAC address, MAC-B, and the destination MAC address, MAC-A.*

*2. When VTEP-2 receives the ARP response, it looks up its local table and finds the corresponding entry. At this point, VTEP-2 knows that traffic going to End System A must transmit to the VTEP-1 address. VTEP-2 encapsulates the ARP response with a VXLAN header and sends the unicast packet to VTEP-1.*

*3. VTEP-1 receives and de-encapsulates the original ARP response. VTEP-1 learns the source MAC address of End System B and creates an entry in its local table with the information about how to reach End System B.*

*4. VTEP-1 sends the original ARP response frame to End System A.*

### MP-BGP EVPN Control Plane Overview

*MP-BGP EVPN is a standards-based VXLAN control protocol. It introduces control-plane learning for end hosts behind remote VTEPs. It provides control-plane and data-plane separation and a unified control plane for Layer 2 and Layer 3 forwarding in a VXLAN overlay network.*

*The MP-BGP EVPN control plane offers the following benefits:*

- *It uses industry standards, allowing multivendor interoperability.*

- *It enables control-plane learning of end-host Layer 2 and Layer 3 reachability information, enabling organizations to build more robust and scalable VXLAN overlay networks.*

- *It uses the decade-old MP-BGP VPN technology to support scalable multitenant VXLAN overlay networks.*

- *It allows the EVPN address family to carry Layer 2 and Layer 3 reachability information, thus providing integrated bridging and routing in VXLAN overlay networks.*

- *It minimizes network flooding through protocol-based host MAC and IP route distribution and ARP suppression on the local VTEPs.*

- *It provides optimal forwarding for east-west and north-south traffic and supports workload mobility with the distributed anycast function.*

- *It provides VTEP peer discovery and authentication, mitigating the risk of rogue VTEPs in the VXLAN overlay network.*

- *It provides mechanisms for building active-active multihoming at Layer 2.*

*With MP-BGP EVPN, VXLAN control plane devices might be Multiprotocol Internal Border Gateway Protocol (MP-IBGP) EVPN peers or route reflectors or Multiprotocol External BGP (MP-EBGP) EVPN peers. Their operating system software must support MP-BGP EVPN so that it can recognize the MP-BGP EVPN updates and distribute them to other MP-BGP EVPN peers using the standards-defined constructs.*

*For data forwarding, IP transport devices perform IP routing that is based only on the outer IP address of a VXLAN-encapsulated packet. They are not required to support the VXLAN data encapsulation and decapsulation functions.*

### MP-BGP EVPN Host Information Learning and Distribution

*Similar to other network routing control protocols, MP-BGP EVPN distributes Network Layer Reachability Information (NLRI) for the network. A unique feature of EVPN NLRI is that it includes the Layer 2 and Layer 3 reachability information for end hosts that resides in the EVPN VXLAN overlay network. It advertises MAC and IP addresses of EVPN VXLAN end hosts, a capability that forms the basis for VXLAN-integrated routing and bridging support.*

![MP-BGP EVPN](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/mp-bgp_evpn.png)

*The process for the MP-BGP EVPN control plane operation includes the following steps:*

*1. A VTEP in the MP-BGP EVPN learns the MAC addresses and IP addresses of locally attached end hosts through local learning. This learning can be local-data-plane–based using the standard Ethernet and IP learning procedures. Examples include source MAC address learning from the incoming Ethernet frames and IP address learning when the hosts send Gratuitous ARP (GARP) and Reverse ARP (RARP) packets or ARP requests for the gateway IP address on the VTEP.*

*2. After learning the local-host MAC and IP addresses, a VTEP advertises the host information in the MP-BGP EVPN control plane so that this information can distribute to other VTEPs. This approach enables EVPN VTEPs to learn the remote end hosts in the MP-BGP EVPN control plane. VTEPs advertise EVPN routes through the Layer 2 VPN EVPN address family. The BGP Layer 2 VPN EVPN routes include the following information:*

- ***Route distinguisher (RD):*** *This information is an 8-bit octet number that distinguishes one set of routes (one VRF instance) from another set of routes. It is a unique number that is prepended to each route so that if the same route is used in various VRF instances, BGP can treat them as distinct routes. The route distinguisher transmits with the route through MP-BGP when EVPN routes are exchanged with MP-BGP peers.*

- ***MAC address length:*** *This information is provided in 6 bytes.*

- ***MAC address:*** *This information is the host MAC address.*

- ***IP address length:*** *This information is 32 or 128.*

- ***IP address:*** *This information is the host IP address (IPv4 or IPv6).*

- ***Layer 2 VNI:*** *This information is the VNI of the bridge domain to which the end host belongs.*

- ***Layer 3 VNI:*** *This information is the VNI associated with the tenant VRF routing instance.*

*MP-BGP EVPN uses the BGP extended community attribute to transmit the exported route targets in an EVPN route. When an EVPN VTEP receives an EVPN route, it compares the route-target attributes in the received route to its locally configured route-target import policy to decide whether to import or ignore the route. This approach uses the decade-old MP-BGP VPN technology (RFC 4364). It provides scalable multitenancy, in which a node that has no VRF instance locally does not import the corresponding routes.*

*When a VTEP switch originates MP-BGP EVPN routes for its locally learned end hosts, it uses its own VTEP address as the BGP next hop. This BGP next hop must remain unchanged through the route distribution across the network. The remote VTEP must learn the originating VTEP address as the next hop for VXLAN encapsulation when forwarding packets for the overlay network.*

*11. The route reflector works like a neighbor relationship aggregation point and provides BGP update exchange.*

*12. As a result of the MP-BGP EVPN control plane operation, every VTEP knows how to reach every end system.*

### VTEP Peer Discovery and Authentication in MP-BGP EVPN

*Before MP-BGP EVPN, VXLAN had no control-protocol-based VTEP peer-discovery mechanism or a method for authenticating VTEP peers. These limitations present major security risks in real-world VXLAN deployments because they allow easy insertion of a rogue VTEP into a VNI segment to send or receive VXLAN traffic.*

![VTP Peer Discovery and Authentication](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vtp_peer_discovery_and_auth.png)

*With the MP-BGP EVPN control plane, VTEPs use the following peer discovery and authentication mechanism:*

*1. The VTEP device must first establish BGP neighbor adjacency with other VTEPs or with Internal Border Gateway Protocol (IBGP) route reflectors. In addition to the BGP updates for end-host NLRI, VTEPs exchange the following information about themselves through BGP:*

- *Layer 3 VNI*

- *VTEP address*

- *Router MAC address*

*5. When a VTEP receives BGP EVPN route updates from a remote VTEP BGP neighbor, it adds the VTEP address from that route advertisement to the VTEP peer list.*

*6. The local VTEP uses this VTEP peer list as an allow list of VTEP peers.*

*7. If your local VTEP receives a packet from another VTEP that is not on the allow list, it considers the source of the packet invalid or unauthorized.*

*8. As a result, your local VTEP discards VXLAN-encapsulated traffic from that invalid VTEP.*

*For extra security, you can apply the current BGP Message Digest 5 (MD5) authentication to the BGP neighbor sessions. Then, switches cannot become BGP neighbors to exchange MP-BGP EVPN routes until they successfully authenticate each other.*

### Distributed Anycast Gateway in MP-BGP EVPN

*In MP-BGP EVPN, you can configure a VTEP in a VNI as the distributed anycast gateway for end hosts in its IP subnet. In this case, all VTEPs have the same virtual gateway IP address and virtual gateway MAC address.*

![Distributed Anycast Gateway](https://github.com/PurityControl7/DCFNDU/blob/root/images/distributed_anycast_gateway.png)

*With the anycast gateway function in EVPN, end hosts in a VNI can use their local VTEPs for this VNI as their default gateway to send traffic outside of their IP subnet. This capability enables optimal forwarding for northbound traffic from end hosts in the VXLAN overlay network. A distributed anycast gateway also offers the benefit of seamless host mobility in the VXLAN overlay network. The gateway IP and virtual MAC address are the same on all VTEPs within a VNI. So, when an end host moves from one VTEP to another VTEP, it is not required to send another ARP request to relearn the gateway MAC address.*

### ARP Suppression in MP-BGP EVPN

*To reduce network flooding caused by broadcast traffic from ARP requests, the MP-BGP EVPN control plane provides an ARP suppression feature. When you enable the ARP suppression feature for a VNI, each VTEP maintains an ARP suppression cache table for known IP hosts and their associated MAC addresses in the VNI segment.*

![ARP Suppression](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/arp_suppression.png)

*When an end host in the VNI sends an ARP request for another end-host IP address, its local VTEP intercepts the ARP request and checks for the IP address from the ARP request in its ARP suppression cache table. If it finds a match, the local VTEP sends an ARP response on behalf of the remote end host. The local host learns the MAC address of the remote host in the ARP response. If the local VTEP lacks information about the IP address from the ARP request in its ARP suppression table, it floods the ARP request to the other VTEPs in the VNI.*

*This ARP flooding can occur for the initial ARP request to a silent host in the network. The VTEPs in the network do not see traffic from the silent host until another host sends an ARP request for its IP address and it returns an ARP response. After the local VTEP learns about the MAC and IP addresses of the silent host, the information distributes through the MP-BGP EVPN control plane to all other VTEPs. Subsequent ARP requests do not require flooding.*

*Most end hosts send GARP or RARP requests to announce themselves to the network right after they come online. Therefore, the local VTEP immediately can learn their MAC and IP addresses and distribute this information to other VTEPs through the MP-BGP EVPN control plane. Therefore, VTEPs should learn the most active IP hosts in a VXLAN EVPN through local learning or control-plane-based remote learning. As a result, ARP suppression reduces the network flooding that is caused by host ARP learning behavior.*

*The process for ARP suppression in MP-BGP EVPN consists of the following steps:*

*1. Host 1 in VLAN 10 sends an ARP request for the IP address of Host 2 (IP-2).*

*2. VTEP-1 intercepts the ARP request and checks in its ARP suppression cache. VTEP-1 finds a match for IP-2 in VLAN 10 in its ARP suppression cache.*

*3. VTEP-1 sends an ARP response back to Host 1 with MAC-2.*

*4. Host 1 learns the IP-2 and MAC-2 mapping.*

### Additional Notes and Clarifications (With Summary):

*The Big Picture:*

VXLAN is the data plane, EVPN is the control plane, and MP-BGP is the distributed database that replaces flooding, guessing, and pain.

**1. Multicast Control Plane (Flood-and-Learn): ARP Request**

This is classic *VXLAN without EVPN* — VXLAN-as-a-big-L2-segment.

When a host sends an ARP request, the ingress VTEP *floods it via multicast* to **all** VTEPs in that VNI. Every VTEP learns source MAC/IP from seeing traffic (data-plane learning).

This is literally *traditional L2 flooding,* just stretched over IP with VXLAN encapsulation. It scales badly, burns bandwidth, and makes troubleshooting miserable.

*Mental tag: “ARP = multicast blast radius”*

**2. Multicast Control Plane (Flood-and-Learn): ARP Response**

The ARP reply is usually *unicast,* but learning is still opportunistic.

Remote VTEPs only learn because traffic happened to pass through them. If traffic never flows, knowledge never exists. This is why flood-and-learn behaves like a haunted network: information appears *after* packets move, not before.

*Mental tag: “Learning happens after the crime”*

**3. MP-BGP EVPN Control Plane Overview:**

EVPN flips everything. *No guessing, no flooding, no multicast dependency.*

Each VTEP becomes a *BGP speaker* and advertises what it *knows* (MACs, IPs, VNIs, gateways) using EVPN routes. MP-BGP is not “routing traffic” here — it is *publishing reachability facts,* like a distributed control-plane ledger.

*Key shift:*

- Old: *data plane teaches control plane*

- EVPN: *control plane teaches data plane*

**4. MP-BGP EVPN Host Information Learning & Distribution:**

When a host appears, the local VTEP learns it *locally* and immediately advertises:

- MAC

- IP (optional but crucial)

- VNI

- VTEP IP

Other VTEPs now know *exactly* where that host lives before any traffic is sent. This kills flooding and turns VXLAN into something that behaves more like *L3 routing with MAC awareness.*

*Mental tag: “Learn once, announce once, everyone knows”*

**5. VTEP Peer Discovery & Authentication (MP-BGP EVPN):**

No multicast discovery needed.

VTEPs discover each other because *BGP sessions already exist* (often via route reflectors). Authentication, policy, filtering — all inherited from BGP. This is why operators trust EVPN: it uses tooling we already understand.

*Comparison:*

- Multicast VXLAN: *“Who’s out there?”*

- EVPN: *“Here’s the membership list.”*

**6. Distributed Anycast Gateway (EVPN magic):**

Every VTEP uses the *same gateway IP and MAC* for hosts in a subnet. Hosts always talk to “their” gateway — but the gateway is *everywhere.*

Traffic never hairpins, first-hop routing is local, and failover becomes trivial. This is something classic L2/L3 simply cannot do cleanly.

*Mental tag: “The gateway is a myth, and that’s good”*

**7. ARP Suppression in MP-BGP EVPN:**

Because VTEPs already know *IP → MAC → VTEP mappings,* ARP requests don’t need to flood.

The VTEP replies *locally* on behalf of the remote host using EVPN-learned data. This is the moment VXLAN stops acting like Ethernet and starts acting like a *distributed ARP* cache.

*Comparison:*

- Classic L2: flood ARP

- VXLAN flood-and-learn: multicast ARP

- EVPN: *ARP is basically a lookup*

**Final Mental Map:**

```
Classic L2:
Flood → Learn → Pray

VXLAN Flood-and-Learn:
Encapsulate → Multicast → Learn late → Cry quietly

VXLAN EVPN:
Learn locally
↓
Advertise via MP-BGP
↓
Populate everyone’s tables
↓
Unicast from the first packet
↓
ARP mostly disappears
```

EVPN isn’t “BGP being abused.” It’s *BGP finally doing what it’s best at:* distributing structured reachability information at scale, reliably, and predictably. Once we see MP-BGP as a *control-plane bus* instead of a routing protocol, the whole thing snaps into place.

##  VXLAN Data Plane 

*When you configure the VXLAN protocol, your switch forwards traffic differently depending on the destination MAC address and learned VXLAN topology. If the source and destination MAC addresses are available on the same VLAN, and the switch learned those MAC addresses, it forwards traffic locally with no VXLAN encapsulation.*

*If your switch has an entry in the local VXLAN VTEP tunnel table in which the destination MAC address is behind a remote VTEP, the switch encapsulates the frames in the correct VXLAN header and forwards them to the remote VTEP. The remote VTEP de-encapsulates the VXLAN packet and forwards the inner frame to the port where the recipient is connected. If the local VTEP does not know the destination MAC address, further steps depend on the control plane implementation.*

*The control plane implementation determines one of three possible actions:*

- *Drop unicast frames with unknown destination MAC address.*

- *Forward unicast frames with an unknown destination MAC address using a predefined multicast group.*

- *Replicate unicast frames with unknown destination MAC address to all corresponding VTEPs using multiple unicast packets.*

### VXLAN Unicast Forwarding Layer 2 Packet Flow

*After the VTEPs collect all necessary information about the MAC addresses of the end hosts and virtual machines, you can start traffic forwarding.*

![VXLAN Unicast Layer 2 Packet Flow](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vxlan_unicast_layer2_flow.png)

*In the scenario in the figure, the two end hosts, Host-A and Host-B, reside in the same subnet but behind distinct VTEPs. If two end devices are in the same VNI, you describe the traffic as bridged.*

*The process for traffic forwarding has the following steps in this scenario:*

1. *Host-A sends a Layer 2 frame with its own source MAC and IP addresses, and the destination MAC and IP addresses are Host-B addresses. When the hosts belong to the same subnet, the traffic behavior looks like they reside on the same switched physical network. Based on the switching tables of the local switches, the original frame will come to the local VTEP-1.*

2. *VTEP-1 verifies its local MAC address table and finds that the destination MAC address is located behind remote VTEP-2. VTEP-1 encapsulates the original Layer 2 frame with VXLAN, UDP, IP, and Ethernet headers and sends the frame through the transport IP network to the remote VTEP-2. When Host-A belongs to VXLAN 10, VTEP uses VXLAN network identifier (VNID) 10 in the VXLAN header. In the outer IP header, VTEP-1 uses its own IP address as the source and the IP addresses of VTEP-2 as the destination. In the outer Ethernet header, VTEP-1 uses its own MAC address as the source and the MAC addresses of the next-hop router as the destination MAC address.*

3. *The VXLAN packet travels through the transport IP network from VTEP-1 to VTEP-2.*

4. *Router-2 has VTEP-2 as the next-hop router. Router-2 forwards the encapsulated packet to the VXLAN tunnel destination.*

5. *VTEP-2 de-encapsulates the packet, verifies its local MAC address table, and forwards the original Layer 2 frame to its final destination, which is Host-B.*

### VXLAN Unicast Forwarding Layer 3 Packet Flow

*After the VTEPs collected all necessary information about the MAC addresses of the end hosts and virtual machines, you can start traffic forwarding.*

![VXLAN Unicast Layer 3 Packet Flow](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vxlan_unicast_layer3_flow.png)

*In the figure, Host-A (attached to VTEP-1) belongs to the Layer 2 virtual network with VNI 10, and Host-B (attached to VTEP-2) belongs to Layer 2 VNI 11. The subnets for the two networks host distinct IP address ranges. So, the traffic between them is routed.*

*The reachability information for the two end hosts transmits through the MP-BGP EVPN control plane. Examples include the Layer 3 VNI and MAC and IP addresses, in addition to the subnet address of the switch virtual interface (SVI). The ARP and forwarding tables of the source and target switch VTEPs are populated with the end-host reachability information.*

*The process for traffic forwarding has the following steps in this scenario:*

1. *When Host-A sends traffic to VTEP-1, the destination MAC of the packet is encapsulated with the MAC address of the (distributed IP anycast) gateway.*

2. *VTEP-1 performs a lookup, notes the VTEP where Host-B is attached, and checks the VRF instance (and associated Layer 3 VRF VNI). VTEP-1 VXLAN encapsulates the traffic that Host-A transmits and sends it toward VTEP-2.*

3. *The routed traffic from VTEP-1 to VTEP-2 logically traverses through the Layer 3 VRF 1000. In practice, the traffic traverses through the underlay.*

4. *When the packet reaches VTEP-2, VTEP-2 does a control plane lookup, notes that the Host-B IP address is in VRF 1000, and next performs a MAC table lookup for Host-B. After identifying the port to which Host-B is attached, the packet transmits to Host-B.*

### VXLAN Forwarding with vPC

*If you configure vPC topology with an enabled VXLAN protocol, you can apply the benefits of anycast VTEP configuration.*

![VXLAN Forwarding with vPC](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vxlan_forwarding_with_vpc.png)

*When you enable the vPC feature, the switch programs an anycast VTEP address on the two vPC peers. The result is symmetrical forwarding behavior on the two peers. The multicast topology prevents duplication of flooded packets. You must enable the vPC peer-gateway feature on the two peers to enable this behavior.*

*From an MP-BGP EVPN perspective, you must apply the following configurations:*

- *The vPC VTEP switches should have a secondary IP address on the loopback interface as the VTEP address for the source of the VXLAN tunnels (interface name is nve1). The rest of the EVPN VXLAN configuration remains the same as for a standard single VTEP.*

- *The two switches must have their own BGP configurations with a unique router ID.*

- *MP-BGP uses the anycast VTEP address as the next hop when building BGP updates for EVPN routes.*

### Additional Notes and Conclusions:

**1. VXLAN Unicast Forwarding – Layer 2 flow:**

*Think: “MAC-to-MAC delivery, but tunneled.”*

Classic L2:

- Switch learns *MAC → port*

- Frame is forwarded based on destination MAC

- Broadcasts flood the VLAN

VXLAN L2 unicast:

- MAC still matters, but it’s mapped to *VTEP IP + VNI*

Flow looks like this:

1. Source host sends Ethernet frame (dest MAC known)

2. Local VTEP already learned:

MAC → remote VTEP IP (via EVPN)

3. Frame is encapsulated:

- Inner: original Ethernet frame

- Outer: IP/UDP/VXLAN (dest = remote VTEP)

4. Remote VTEP decapsulates and forwards locally

*Key shift:* Flood-and-learn is replaced by *control-plane-learn, data-plane-unicast.* No MAC flooding once EVPN has done its job.

**2. VXLAN Unicast Forwarding – Layer 3 flow:**

*Think: “Routing first, tunneling second.”*

Classic L3:

- Host → default gateway

- Router does IP lookup

- Packet routed to next hop

VXLAN L3 (EVPN IRB model):

1. Host sends packet to *Anycast Gateway MAC*

2. Local VTEP performs:

- Routing lookup (VRF + IP)

- Determines destination subnet

3. EVPN already knows:

- Destination IP → remote VTEP

4. Packet is:

- Routed (L3 decision)

- Then VXLAN-encapsulated

5. Remote VTEP decapsulates and delivers to host

*Mental anchor: Routing happens at ingress VTEP, not “in the fabric.”* The underlay never sees tenant IPs — only VTEP IPs.

**3. VXLAN + vPC:**

The core problem:

With vPC you have *two physical switches acting as one L2 device.* With VXLAN you normally want *one VTEP = one tunnel endpoint.*

So… what happens when:

- Two switches

- One logical gateway

- One set of VXLAN tunnels?

Answer: *vPC VTEP model (shared VTEP).*

**The “secondary loopback IP” mystery (demystified):**

That confusing sentence in my materials is pure Cisco-speak, so here’s the translation:

- Each vPC peer has:

Its *own loopback IP* (for BGP, control-plane, management). BUT…

- They *share a VTEP identity* for VXLAN

This is done by:

- Adding *a secondary IP* on the loopback. That secondary IP is:

- The *source IP for VXLAN tunnels (nve1)*

- Identical on both vPC peers

So both switches advertise:

- Same VTEP IP

- Same Anycast Gateway MAC

- Same VNIs

To the rest of the fabric, they look like: *One VTEP with two bodies.*

**Practical mental model for vPC + VXLAN:**

Imagine:

- Two guards at one gate

- Both wear the same badge

- Outsiders don’t care *which* guard answered

*Traffic behavior:*

Either vPC peer can:

- Encapsulate traffic

- Decapsulate traffic

- vPC peer-link handles synchronization

- No asymmetric VXLAN tunnels

- No duplicate learning

*Why EVPN still works unchanged?*

Because:

- BGP EVPN talks about *VTEP IPs,* not physical switches

- As long as the VTEP IP is shared, the fabric is happy

That’s why: *“The rest of the EVPN VXLAN configuration remains the same”*

**Big-picture comparison:**

```
Classic DC:
- L2 floods
- L3 hops everywhere
- Gateways = single points

VXLAN EVPN:
- Control plane learns everything
- Data plane is mostly unicast
- Gateways are distributed
- Fabric only sees VTEP IPs
```

Or even shorter: *EVPN tells the fabric* ***where,*** *VXLAN moves the bits, vPC hides redundancy.*

VXLAN only feels hard because Cisco explains it *inside-out* instead of saying: *“It’s routing dressed up as switching”.*

Once you see that:

- EVPN = distributed control plane database

- VXLAN = delivery wrapper

- VTEP = edge router in disguise

…the fog lifts.

### Additional Examples and Thoughts (for drilling this into my mind):

**1. VXLAN Unicast Forwarding — Layer 2 (same subnet):**

Mental model:

Think *“Ethernet-in-a-tunnel”.*

- Host A wants to talk to Host B *in the same VLAN*

- The *ingress VTEP:*

Learns Host B via EVPN (MAC → VTEP mapping).

Wraps the original Ethernet frame inside:

- Outer IP (VTEP → VTEP)

- UDP 4789

- VXLAN header (VNI = VLAN)

The *egress VTEP* unwraps and forwards locally. Key shift from classic L2:

- *No flooding* if EVPN already knows the MAC

- MAC learning is *control-plane-driven,* not data-plane sniffing

```
Host A → VTEP1 ===VXLAN tunnel=== VTEP2 → Host B
```

**2. VXLAN Unicast Forwarding — Layer 3 (different subnets):**

Mental model:

This is where VXLAN gets interesting. Instead of:

- VLAN hop → router → VLAN hop

You get:

- *Routing at the ingress VTEP*

What really happens:

1. Host A sends packet to default gateway

2. Ingress VTEP:

- Acts as *Anycast Gateway*

- Performs *routing locally*

3. Packet is VXLAN-encapsulated using:

- *L3 VNI* (not L2 VNI)

4. Egress VTEP decapsulates and forwards

Important to remember:

- *No tromboning*

- *No centralized router*

- First-hop routing is *distributed*

```
Host A
  ↓
Anycast GW (VTEP1 does routing)
  ↓
VXLAN (L3 VNI)
  ↓
VTEP2 → Host B
```

**3. VXLAN + vPC — the “shared brain” problem:**

This is the part that rightfully messes with people. The core problem:

Two physical switches:

- Act as *one logical access switch* (vPC)

- But VXLAN wants *unique tunnel endpoints*

That’s a contradiction.

**The magic trick: vPC VTEP (Anycast VTEP):**

Mental model:

Two switches pretending to be:

- One L2 switch (vPC)

- One VXLAN endpoint (shared VTEP IP)

How Cisco solves it:

- *Each switch has its own loopback*

- They also share *one secondary loopback IP*

- That shared IP is the *VTEP address*

**The confusing sentence — decoded again:**

*“The vPC VTEP switches should have a secondary IP address on the loopback interface as the VTEP address…”*

Translation into human language:

*“Each switch keeps its own identity, but VXLAN tunnels must originate from a* ***shared IP,*** *so remote VTEPs see the vPC pair as one endpoint.”*

**Minimal, practical config (THIS is the missing piece):**

Loopback config (both switches)

```
interface loopback0
  ip address 10.10.10.1/32        ! unique per switch
  ip address 10.10.10.100/32 secondary   ! SHARED vPC VTEP IP
```

- ```10.10.10.1``` → Router-ID / BGP identity

- ```10.10.10.100``` → VXLAN tunnel source

NVE interface (both switches):

```
interface nve1
  no shutdown
  source-interface loopback0
  host-reachability protocol bgp
```

Remote VTEPs:

- Don’t know

- Don’t care which physical box sent the packet

They just see *10.10.10.100*

**vPC domain glue (already familiar territory):**

```
vpc domain 10
  peer-switch
  peer-keepalive destination 192.0.2.2 source 192.0.2.1
```

This ensures:

- MAC consistency

- No duplicate advertisements

- Clean EVPN behavior

**VXLAN forwarding with vPC — packet flow:**

*From a host’s POV:*

- Sends frame → either switch

- Both switches are valid gateways

- Life is good etc.

*From VXLAN’s POV:*

Packet always exits using:

- *Shared VTEP IP*

- Same EVPN advertisements

- No asymmetry

- No MAC flapping

Think of it as: *Two mouths, one voice.*

**Classic vs VXLAN behavior (sticky-note version):**

```
| Old World              | VXLAN EVPN          |
| ---------------------- | ------------------- |
| Flood ARP              | ARP suppression     |
| MAC learned by traffic | MAC learned by BGP  |
| Central router         | Distributed routing |
| STP fear               | ECMP joy            |
| One failure hurts      | Failure is boring   |
```

If you remember *only three things,* remember these:

1. VXLAN = IP transport, not magic L2

2. EVPN = who lives where

3. vPC VTEP = shared face, separate brains

And yeah — Cisco documentation absolutely explains this like it hates humans.

## VMware vSphere Virtual Switches

*VMware virtual switches allow virtual machines on the same ESXi Server host to communicate with each other, without the need for extra networking hardware. ESXi Server virtual switches also support VLANs that are compatible with standard VLAN implementations.*

### VMware Virtual Standard Switch

*A Virtual Standard Switch (VSS) is a virtual construct that performs network switching between the virtual machines on a VMware host and the external network.*

*In the figure, you can examine a vSwitch setup example with four virtual machines and physical NICs as uplink ports added to the same vSwitch.*

![vSwitch setup](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vswitch_example.png)

*The switching component on the hypervisor, internal to the host, supports the Cisco network design paradigm of access, aggregation, and distribution network layers.*

*Devices containing the access layer that were traditionally connected to the hosts moved closer to the aggregation layer. The vSwitch infrastructure within the host replaces the access layer in the traditional Cisco data center architecture.*

*The main features of a vSwitch are the following:*

- *Associates physical switches with VNICs.*

- *Provides connectivity for the following:*

*Virtual machine communication within and between ESXi hosts*

*Virtual Machine Kernel (VMK) for VMware vMotion, Internet Small Computer Systems Interface (iSCSI), and VMware fault tolerance logging*

- *Assigns a management port to a VLAN.*

- *Assigns VMK ports to a VLAN.*

- *Assigns virtual machine port groups to a VLAN and assigns virtual machines to a port group.*

- *Uses uplinks for external connectivity and associates a virtual machine NIC with a single vSwitch only.*

### VMware vSwitch Operation

*vSwitches function like normal Layer 2 switches and support very similar functionality to physical Layer 2 switches with some particular details.*

*A single VMware host can have multiple vSwitches configured and segregated from each other, in a manner similar to virtual machines.*

*The figure shows an example of a standard switch operation in a virtual network, including virtual guest tagging and NIC teaming. Because vSwitches are Layer 2 devices, they do not route Layer 3 traffic.*

![VMware vSwitch Operation](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vmware_vswitch_operation.png)

*The following are functions of a vSwitch:*

- *Forwards frames per MAC address and maintains a MAC address table.*

- *Performs internal switching for virtual machines.*

- *Ensures that other traffic is forwarded to the uplink port.*

- *Does not participate in STP, Dynamic Trunking Protocol (DTP), or Port Aggregation Protocol (PAgP).*

*Note: PAgP is a Cisco-proprietary protocol that can run only on Cisco IOS devices. Cisco NX-OS devices do not support PAgP.*

- *Manages testing and traffic isolation using internal vSwitches, which are accessible through VMware vCenter.*

- *Performs virtual guest tagging using VLAN 4095 and tags traffic passed up to the guest operating system.*

- *Connects multiple virtual machine NICs to a single vSwitch and applies failover order for active and standby ports using NIC teaming.*

*vSwitches support trunking, port channels, and Cisco Discovery Protocol.*

*You can assign vSwitch with 0, 1, or up to 32 network ports. Bandwidth and reliability increase with the number of assigned ports. If you assign no ports, the vSwitch can switch the traffic only between the virtual machines within the host.*

### VMware vSphere Distributed Switch

*A vSphere Distributed Switch (VDS) is an aggregation of per-host virtual switches that are presented and controlled as a single distributed switch through a vCenter server at the data center level. The VDS abstracts the configuration of individual virtual switches and enables centralized provisioning, administration, and monitoring.*

*The VDS is the next step toward improved functionality when compared to a standard vSwitch.*

*Whereas the vSwitch is managed individually on the host where it was created, the VDS is managed globally across all the hosts as a single switch.*

*The figure shows a single VDS that connects to the ESXi hosts.*

![VDS](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vds.png)

*The VDS requires a vCenter. The VDS provides greater management uniformity, because segmentation can be avoided. The VDS was introduced because vMotion requires that networking access for all cluster hosts be equally configured.*

*The VMware VDS eliminates management overhead in a cluster that needs vMotion support with many hosts.*

*Several types of VDSs are available, including the following options:*

- ***Single VDS:*** *All the virtual machines are migrated to VDS, including the VMK and service control ports of the server.*

- ***Hybrid VDS and VSS:*** *Only virtual machines of the ESXi server are migrated to a VDS. VMK ports and service control ports remain in the VMware vNetwork Standard Switch (VSS).*

- ***Multiple VDSs:*** *All the virtual machines are added to multiple VDSs, including VMK and service control ports of the ESXi server.*

### Additional Notes and Conclusions:

Big mental map first:

- **vSwitch (VSS)** = *a local,* per-ESXi-host Layer-2 switch.

- **vSwitch operation** = behaves like a dumb but fast L2 switch glued inside the hypervisor.

- **vSphere Distributed Switch (VDS)** = many vSwitches pretending to be *one big switch,* centrally controlled by vCenter.

- **VMkernel port** = *not a VM,* but the ESXi host itself speaking on the network.

That last one is the key that unlocks the confusion.

**VMware Virtual Standard Switch (VSS):**

Think of a VSS as the *Top-of-Rack switch inside a single ESXi host.*

- Lives *only on one ESXi host*

Connects:

- VM vNICs

- VMkernel ports (management, vMotion, iSCSI, etc.)

- Physical NICs (uplinks)

VLANs work exactly like normal VLANs. Configuration is *host-local* (painful at scale).

Cisco analogy: A VSS ≈ a standalone access switch you must configure box-by-box.

**VMware vSwitch Operation (how it actually behaves):**

This part trips people up because VMware keeps saying “it’s like a switch” — it *is,* but with caveats.

What a vSwitch *does:*

- Learns MAC addresses

- Forwards frames at Layer 2

- Switches traffic *internally* VM ↔ VM at memory speed

- Sends unknown / external traffic to uplinks

What it does NOT do:

- No STP

- No DTP

- No PAgP

- No routing

Why no STP? Because VMware assumes *you* control the topology. The physical switch is responsible for loop protection.

Important quirk:

- VLAN *4095* = “guest tagging” (VM handles VLANs itself)

- Otherwise VLANs are enforced at the port group level

**VMware vSphere Distributed Switch (VDS):**

This is where VMware finally admits: *“Okay, clusters exist.”*

A VDS is:

- One logical switch

- Spanning *multiple ESXi hosts*

- Managed *only via vCenter*

- Required for sane vMotion at scale

Why VDS exists:

- vMotion demands identical networking on every host

- Humans are bad at consistency

- VDS centralizes port groups, VLANs, policies

Cisco analogy: VDS ≈ fabric-wide switch config pushed to all ToRs.

**VSS vs VDS (burn this into memory):**

```
| Feature              | VSS       | VDS            |
| -------------------- | --------- | -------------- |
| Scope                | One host  | Entire cluster |
| Managed by           | ESXi host | vCenter        |
| vMotion friendly     | No        | Yes             |
| Operational sanity   | Low       | High           |
| Required for labs    | Yes       | Not strictly   |
| Required for real DC | No        | Absolutely     |
```

**Now… the confusing Cisco quote:**

*“We also do virtual networking so we can manage the ESXi host… that requires a VMkernel port.”*

This is the *most important concept* in this section.

What a VMkernel (vmkX) port REALLY is:

- The ESXi host’s *own network interface*

- Used for *host services,* not VMs

Examples:

- Management (SSH, HTTPS, vCenter)

- vMotion

- iSCSI / NFS

- Fault Tolerance

- vSAN

ESXi is *not* a black box. It is an OS that must:

- Have an IP

- Send ARP

- Route packets

- Talk TCP/UDP

That’s what a VMkernel port is for.

*Why this matters?* Without a VMkernel port:

- ESXi cannot be managed

- vCenter cannot talk to it

- vMotion cannot work

- Storage traffic cannot flow

So when Cisco says: *“We do virtual networking for management”*

They mean: *“We give the* ***hypervisor itself*** *a NIC, VLAN, and IP.”*

Cisco analogy: VMkernel port = loopback / SVI of the ESXi host.

**Typical ESXi networking stack (visualized):**

```
[ VM ] ----+
           |
[ VM ] ----+--> Port Group --> vSwitch --> Uplink --> Physical Switch
           |
[ vmk0 ] --+   (Management / vMotion / Storage)
```

Same switch. Same VLAN rules. Different *consumer* of the network.

*Final sanity snapshot:*

- VMs talk via *vNICs*

- ESXi talks via *VMkernel ports*

- Both plug into port groups

- Port groups live on *vSwitches*

- VDS just makes this sane across many hosts

If you remember only one thing: ***VMkernel ports are the ESXi host acting like a machine on the network.***

Think of *VMkernel ports as the ESXi host itself putting on a NIC costume:* they’re not VMs, but logical interfaces the hypervisor uses to exist on the network (management, vMotion, iSCSI, NFS, VXLAN, etc.).

They’re *not all auto-created though* — ***Management vmk (vmk0)*** is created during install, but everything else (vMotion, storage, VXLAN) is explicit and intentional.

And yes: at the physical level, ESXi only needs *uplinks* — once packets hit ESXi, VMkernel ports + vSwitches decide who inside the host is allowed to speak. It's like saying: *VMs talk through vNICs, ESXi talks through VMkernel ports* — same wire, different souls.
