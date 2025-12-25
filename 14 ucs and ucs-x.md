# Describing Cisco UCS and UCS-X Components

*Cisco Unified Computing System (Cisco UCS) simplifies your data center architecture. It reduces the number of devices to purchase, deploy, and maintain and improves your ability to scale and manage the infrastructure.*

*Here you will see the types of servers that are used in the Cisco data center. The list includes rack servers, blade servers, blade server chassis, storage servers, and hyperconverged systems. You will also become familiar with Cisco UCS Fabric Interconnect components and their functions within the data center.*

*The Cisco Integrated Management Controller (IMC) Supervisor enables centralized management of standalone Cisco UCS C-Series rack servers that are located across one or more sites. The purpose is to reduce costs and increase efficiency in managing Cisco standalone servers.*

*Cisco UCS Manager is the management system for all components in a Cisco UCS domain. Cisco UCS Manager runs on the management nodes (Cisco UCS Fabric Interconnects). Any interface with this management service can access, configure, administer, and monitor the network and server resources for all Cisco UCS devices that connect to the fabric interconnects.*

## Cisco UCS Server Hardware

*Cisco UCS represents a radical simplification of the traditional server deployment model. This solution offers simplified stateless blades and a blade-server chassis that is centrally provisioned, configured, and managed.*

### Cisco UCS B-Series Blade Servers

*Cisco UCS B-Series blade servers incorporate industry-standard server technologies and deliver a unified, architecture-driven solution for data centers. The Cisco UCS design reduces complexity at hardware and management levels across a distributed computing environment and consolidated management across blade and rack servers in a single tool.*

![UCS B-Series Blade Servers](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/UCS_B-series_blade_servers.png)

*All Cisco UCS blade servers come with Cisco UCS Manager capability. Cisco UCS with Cisco UCS Manager provides the following:*

- *Embedded integration of LAN, SAN, and management.*

- *Local (and optional global) service profiles and templates for policy-driven server provisioning.*

- *Autodiscovery with automatic recognition and configuration of blades.*

### Cisco UCS 5108 Blade Chassis

*The Cisco 5100 Series Blade Server Chassis is a crucial building block of Cisco UCS. This chassis delivers a scalable and flexible blade server chassis for the current and future data centers while reducing the total cost of ownership (TCO).*

![UCS 5108 Blade Chassis](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/UCS_5108_blade.png)

*The Cisco UCS 5108 Blade Server Chassis revolutionizes the use and deployment of blade-based systems. This chassis incorporates Cisco Unified Fabric, integrated and embedded management, and fabric extender technology. It uses fewer physical components, requires no independent management, and enables greater energy efficiency than traditional blade-server chassis.*

*This simplicity eliminates the need for dedicated chassis management and blade switches, reduces cabling, and allows Cisco UCS to scale to 20 chassis without adding complexity. The Cisco UCS 5108 chassis is a critical component in delivering Cisco UCS benefits of data center simplicity and IT responsiveness.*

*The Cisco UCS 5108 chassis also offers an architectural advantage. You have no need to power and cool excess switches per chassis. With a larger power budget for each blade server, Cisco can design uncompromised expandability and capability in its blade servers.*

### Cisco UCS B200 M6 Blade Servers

*The Cisco UCS B200 M6 is a half-width blade. Up to eight servers can reside in the 6RU Cisco UCS 5108 Blade Server Chassis. It offers one of the highest densities of servers for each rack unit of blade chassis in the industry.*

*The Cisco UCS B200 M6 Blade Server delivers performance, versatility, and density without compromise. This appliance addresses the broadest set of workloads from IT and web infrastructure through distributed databases. The enterprise-class Cisco UCS B200 M6 blade server extends the capabilities of the Cisco UCS portfolio from Cisco in a half-width blade form factor.*

![UCS B200 M6 Blade](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/UCS_B200_M6.png)

*The Cisco UCS B200 M6 Server is the follow-up server to the popular Cisco UCS B200 M5 Server and provides the following main features:*

- *Up to two third-generation Intel Xeon Scalable processors with up to 40 cores for each CPU.*

- *32 DIMM slots for industry-standard DDR4 memory at speeds up to 3200 MHz, with up to 8 TB of total memory when using 512 GB DIMMs. Up to 16 DIMM slots are ready for Intel Optane DC PMem to accommodate up to 12 TB of Intel Optane DC persistent memory.*

- *A modular LAN on motherboard (mLOM) card with Cisco UCS virtual interface card (VIC) 1440, a two-port, 40-Gigabit Ethernet, Fibre Channel over Ethernet (FCoE)–capable mLOM mezzanine adapter.*

- *An optional rear mezzanine VIC with two 40 Gbps unified I/O ports or two sets of four 10 Gbps unified I/O ports delivers 80 Gbps to the server. It adapts to either 10 or 40 Gbps fabric connections.*

- *Two optional, hot-pluggable solid-state drives (SSDs) or Non-Volatile Memory Express (NVMe) 2.5-inch drives are available. They come with a choice of enterprise-class Redundant Array of Independent Disks (RAIDs) and pass-through controllers or four M.2 Serial Advanced Technology Attachment (SATA) drives. These drives provide flexible boot and local storage capabilities.*

- *Support for one rear storage mezzanine card.*

### Cisco UCS C-Series Rack Servers

*Cisco UCS C-Series Rack Servers deliver unified computing in a rack-mount form factor. The Cisco UCS C-Series Rack Server family offers an entry point into unified computing. They provide the flexibility for standalone management or can be integrated into a Cisco UCS-managed environment.*

![UCS C-Series Rack](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/UCS_C-Series.png)

*The Cisco UCS C-Series models can address various workload challenges through a balance of processing, memory, I/O, and internal storage resources.*

*When used with Cisco UCS Manager, Cisco UCS C-Series Servers bring the power and automation of unified computing to enterprise applications, including Cisco SingleConnect technology. Cisco SingleConnect unifies LAN, SAN, and systems management into one simplified link for rack servers, blade servers, and virtual machines. This technology reduces the number of network adapters, cables, and switches. It also simplifies the network and reduces complexity.*

*Cisco currently offers two generations of Cisco UCS C-Series Rack Servers: M7 and M8.*

1. ***Cisco UCS C-Series M7 Rack Servers:***

- *Cisco UCS C220 M7 Rack Server*

- *Cisco UCS C225 M7 SFF Rack Server*

- *Cisco UCS C240 M7 Rack Server*

- *Cisco UCS C245 M7 SFF Rack Server*

2. ***Cisco UCS C-Series M8 Rack Servers:***

- *Cisco UCS C220 M8 Rack Server*

- *Cisco UCS C225 M8 SFF Rack Server*

- *Cisco UCS 240 M8 Rack Server*

- *Cisco UCS C245 M8 SFF Rack Servers*

*Intel-based servers encompass the 2x0 models. Examples are the Cisco UCS C220 M7 Rack Server and the Cisco UCS C240 M7 Rack Server. These models deliver a harmonious blend of processing power, memory, I/O capabilities, and internal storage resources. Integrated with Cisco UCS Manager and powered by Intel processors, these servers optimize unified computing, simplifying network infrastructure through Cisco SingleConnect technology.*

*The AMD counterparts introduce a shift with the 2x5 models, like the Cisco UCS C225 M7 SFF Rack Server, for customers wanting to use AMD processors. This AMD-based lineup provides an alternative processing architecture, offering enterprises flexibility and choice while ensuring reliability and performance.*

### Cisco Virtual Interface Cards

*Cisco UCS VICs extend the network fabric directly to servers and virtual machines. A single connectivity mechanism can connect both physical and virtual servers with as much visibility and control. Cisco VICs provide complete programmability of the Cisco UCS I/O infrastructure, with the number and type of I/O interfaces configurable on demand with a zero-touch model.*

![Virtual Interface Cards](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/virtual_interface_cards.png)

*Cisco VICs support Cisco SingleConnect technology, which provides an easy, intelligent, and efficient way to connect and manage computing in a data center. Cisco SingleConnect unifies LAN, SAN, and systems management into one simplified link for rack servers, blade servers, and virtual machines. This technology reduces the number of network adapters, cables, and switches and radically simplifies the network to reduce complexity.*

*Cisco VICs can support 256 Peripheral Component Interconnect Express (PCIe) virtual devices, either virtual NIC (vNIC) or virtual host bus adapter (vHBA), with a high rate of I/O operations per second (IOPS). They have support for lossless Ethernet and a 10, 25, 40, 100, and Gbps connection to servers. The PCIe Generation 4.0 x16 interface helps ensure optimal bandwidth to the host for network-intensive applications, with a redundant path to the fabric interconnects. Cisco VICs support NIC teaming with fabric failover for increased reliability and availability. These components provide a policy-based, stateless, agile server infrastructure for your data center.*

*The Cisco VIC 1400 and 1500 Series are designed for UCS B-Series, X-series M7 and M8 Blade Servers, and C-Series M7 and M8 Rack Servers. The adapters can support 10, 25, 40, 100, and 200 Gigabit Ethernet and Fibre Channel over Ethernet (FCoE). It incorporates the next-generation converged network adapter (CNA) technology from Cisco and offers a comprehensive feature set, providing investment protection for future feature software releases.*

*The VIC also supports Cisco Data Center Virtual Machine Fabric Extender technology. This technology extends the Cisco UCS Fabric Interconnect ports to virtual machines, simplifying server virtualization deployment.*

*Cisco UCS VIC 1400 series provides the following features and benefits:*

- ***Stateless and agile platform:*** *The card’s personality is determined dynamically at boot time using the service profile that is associated with the server. It determines the number, type (NIC or HBA), identity (MAC address and World Wide Name [WWN]), failover policy, bandwidth, and quality of service (QoS) policies of the PCIe interfaces. The capability to define, create, and use interfaces on demand provides a stateless and agile server infrastructure.*

- ***Network interface virtualization:*** *Each PCIe interface that is created on the VIC is associated with an interface on a Cisco UCS Fabric Interconnect component. It provides complete network separation for each virtual cable between a PCIe device on the VIC and the interface on the fabric interconnect.*

*The following table compares Cisco VIC 1400 Series devices.*

![VIC 1400 Series Comparison](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/VIC_1400_series_comparison.png)

*The VIC 1500 series is designed for Cisco UCS X-Series M7 and M8 Blade Servers, Cisco UCS B-Series M6 Blade Servers, and Cisco UCS C-Series M7 and M8 Rack Servers. The adapters can support 10, 25, 40, 50, 100, and 200 Gigabit Ethernet and FCoE. They incorporate the Cisco next-generation CNA technology and offer a comprehensive feature set, providing investment protection for future feature software releases.*

*The Cisco UCS VIC 15000 Series provide high network performance and low latency for the most demanding applications:*

- *Big data and high-performance computing (HPC)*

- *Large-scale virtual machine deployments*

- *High-bandwidth storage targets and archives*

- *NVMe over Fabrics support for NVMe over Remote Direct Memory Access (RDMA) over Ethernet (RoCEv2), NVMe and Fibre Channel, and NVMe and TCP*

*The following table compares the Cisco VIC 1500 Series devices.*

![VIC 1500 Series Comparison](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/VIC_1500_series_comparison.png)

### Cisco UCS Fabric Interconnect

*The Cisco UCS Fabric Interconnect family is a core part of Cisco UCS. Fabric interconnects provide network connectivity and management capabilities. You can use them primarily to connect a Cisco UCS B-Series Blade Server, but you can also use them to connect and manage standalone Cisco UCS C-Series rack-mount servers. All chassis and servers that connect to fabric interconnects become part of a single and highly available management domain, which reduces costs and operational burdens.*

*The following are the primary functionalities of Cisco UCS fabric interconnects:*

- *Provides the management and communication backbone*

- *Supports unified fabric:*

1. *Provides LAN and SAN connectivity for all servers within the domain*

2. *Includes unified ports supporting Ethernet, FCoE, and Fibre Channel*

- *Possesses a fixed number of unified ports*

![UCS Fabric Interconnect](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/UCS_fabric_interconnect.png)

*Cisco UCS 6454 Fabric Interconnect is a core part of Cisco UCS, providing network connectivity and management capabilities for the system. Cisco UCS 6454 Fabric Interconnect offers line-rate, low-latency, lossless 10, 25, 40, and 100 Gigabit Ethernet, FCoE, and Fibre Channel functions.*

![UCS Fabric Interconnect 2](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/UCS_fabric_interconnect2.png)

*From a networking perspective, the Cisco UCS 6400 Series devices use a cut-through architecture. They support a deterministic, low-latency line-rate of 10, 25, 40, and 100 Gigabit Ethernet ports. The switching capacity is 3.82 Tbps for the 6454. It is 7.42 Tbps for the 64108 with 200 Gbps bandwidth between the 6400 Series Fabric Interconnect and the IOM 2408 for each 5108 blade chassis. Capacity is independent of packet size and enabled services.*

*The product family supports Cisco low-latency, lossless 10, 25, 40, and 100 Gigabit Ethernet unified network fabric capabilities, which increase the reliability, efficiency, and scalability of Ethernet networks. The fabric interconnect supports multiple traffic classes over a lossless Ethernet fabric from the server through the fabric interconnect.*

*The Cisco UCS 64108 Fabric Interconnect is a 2RU top-of-rack switch that mounts in a standard 19-inch rack, such as the Cisco R Series rack. The 64108 is a 10, 25, 40, and 100 Gigabit Ethernet, FCoE, and Fiber Channel switch offering up to 7.42 Tbps throughput and up to 108 ports.*

![UCS Fabric Interconnect 3](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/UCS_fabric_interconnect3.png)

*The Cisco UCS 64108 Fabric Interconnect has 16 unified ports (port numbers 1 to 16) that can support 10 and 25 Gbps SFP28 Ethernet ports. Or it can support 8, 16, and 32 Gbps Fibre Channel ports. It has 72 10 and 25 Gbps Ethernet SFP28 ports (port numbers 17 to 88). It has eight 1, 10, and 25 Gbps Ethernet SFP28 ports (port numbers 89 to 96). It has 12 40 and 100 Gbps Ethernet QSFP28 uplink ports (port numbers 97 to 108). All Ethernet ports can support FCoE.*

*The Cisco UCS 6536 36-Port Fabric Interconnect is a 1RU 1, 10, 25, 40, and 100 Gigabit Ethernet, FCoE, and Fibre Channel switch. It offers up to 7.42 Tbps throughput and up to 36 ports.*

![UCS Fabric Interconnect 4](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/UCS_fabric_interconnect4.png)

### Fabric Interconnect Cluster Peers Connectivity

*Cisco fabric interconnect devices are most often deployed in a high availability deployment, with two devices forming a redundant fabric. To exchange the management information, the devices must link through the Layer 1 to Layer 2 connections using standard RJ-45 Ethernet cables. This link is never used for the transmission of nonmanagement data and does not provide a valid workload traffic path.*

*Before you configure a cluster relationship between two Cisco UCS fabric interconnects, remember two important requirements:*

- *Cluster peers are generally the same model. A Cisco UCS 6248 would peer only with a Cisco UCS 6296 to upgrade the cluster to a pair of Cisco UCS 6296 Fabric Interconnects.*

- *Each peer requires identical licensing. If fabric A has an installed port license for additional ports, fabric B must be licensed for the same number of ports.*

*For the cluster to complete negotiations, both peers must be connected via the cluster links. One connection from port Layer 1 to Layer 1 and one from Layer 2 to Layer 2 must be made with straight-through Category 6 Ethernet cables. The following figure displays this configuration.*

![Fabric Interconnect Cluster Peers Connectivity](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/fabric_interconnect_cluster_peers_connectivity.png)

### Cisco UCS Fabric Interconnect Topology

*You can assign Cisco UCS Fabric Interconnect line card ports to different roles, depending on the traffic that will pass through the Cisco unified port. First, assign a port to a port mode. Then you can assign a port role, which is based on the port mode.*

*Port modes define the protocol that the port will use for communication. Either the port will communicate in native Fibre Channel configuration and no IP traffic will be supported or an FCoE port role will be used.*

*Cisco UCS supports these Fibre Channel port roles:*

- ***Fibre Channel uplink port:*** *This port is used to connect fabric interconnects to an upstream switch that supports Fibre Channel. It does not support Ethernet traffic.*

- ***Fibre Channel storage port:*** *This port is used to connect fabric interconnects to directly attached Fibre Channel storage.*

*Cisco UCS supports these Ethernet port roles:*

- ***Server port:*** *This port is used to connect fabric interconnects to servers.*

- ***FCoE storage port:*** *This port is used to connect fabric interconnects to a storage device that supports simultaneous FCoE and Ethernet traffic.*

- ***FCoE Unified uplink port:*** *This port is used to connect fabric interconnects to an upstream switch that supports FCoE. It can carry both Fibre Channel and Ethernet traffic.*

- ***Appliance port:*** *This port is used to connect fabric interconnects to directly attached Network File System (NFS) storage.*

*The figure shows a Cisco UCS infrastructure topology.*

![UCS infrastructure topology](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/UCS_infrastructure_topology.png)

*The port roles define the traffic types and the devices that connect to a specific port.*

*When configuring a storage port, remember that a Fibre Channel storage port or FCoE storage port cannot function in end-host NPV switching mode. Instead, you must use Fibre Channel switching mode.*

*The default fabric interconnect switching mode is N-Port Virtualization (NPV) end-host mode.*

*Cisco UCS devices also support management ports that you can use to manage the device. The management port is always assigned to the management virtual routing and forwarding (VRF) instance. You can also reach the Cisco Integrated Management Controller (Cisco IMC) interface through a management port. The management port cannot be assigned a role, because it is not a line card port and uses a special dedicated network interface.*

### Cisco UCS I/O Modules

*Cisco UCS devices support expansion modules that attach to the Cisco UCS blade chassis and provide different additional functionalities. These functionalities can be physical, as with I/O modules (IOM), or virtual, as with VICs.*

*An IOM functions as a line card with physical unified ports that extend to the Cisco Unified Fabric. Because they extend the Cisco Unified Fabric, they are also known as fabric extender modules. Because they are responsible for transferring large amounts of data, it is critical for an IOM to have sufficient throughput.*

![UCS I/O Modules](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/UCS_IO_modules.png)

### Cisco UCS 2300 Series Fabric Extenders

*The Cisco UCS 2304 Series Fabric Extender (shown in the figure) is the third-generation IOM. It has four 40 Gigabit Ethernet, FCoE-capable, Quad Small Form-factor Pluggable Plus (QSFP+) ports that connect the blade chassis to the fabric interconnect. Each Cisco UCS 2304 can provide one 40 Gigabit Ethernet port that connects through the midplane to each half-width slot in the chassis. It has a total of eight 40 Gigabit Ethernet interfaces to the compute.*

![UCS 2300 Series](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/UCS_2304.png)

### Cisco UCS 2400 Series Fabric Extenders

*The Cisco UCS 2408 connects the I/O fabric between the Cisco UCS 6454 Fabric Interconnect, Cisco UCS 64108 Fabric Interconnect, Cisco UCS 6536 Fabric Interconnect, and the Cisco UCS 5100 Series Blade Server Chassis. It enables a lossless and deterministic converged fabric to connect all blades and chassis and is shown in this figure.*

![UCS 2400 Series](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/UCS_2408.png)

*The Cisco UCS 2408 Fabric Extender has eight 25 Gigabit Ethernet, FCoE-capable, Small Form-Factor Pluggable (SFP28) ports that connect the blade chassis to the fabric interconnect. Each Cisco UCS 2408 provides 10 Gigabit Ethernet ports that connect through the midplane to each half-width slot in the chassis. The result is a total of 32 10G interfaces to Cisco UCS blades.*

### Fabric Interconnect Cluster-to-IOM Connectivity

*When an IOM of a new Cisco UCS 5108 chassis connects to a fabric interconnect, chassis discovery begins an information exchange. The IOM sends its own fabric ID and serial numbers and sends the process ID (PID), version ID (VID), and the serial number of the chassis. The fabric interconnect sends its PID, VID, serial number, and cluster ID to the IOM. After the exchange completes without error, the cluster takes ownership of the chassis. No other cluster of fabric interconnects will accept the registration of that chassis unless it is decommissioned from that cluster.*

*Data that exchanges during discovery is used to validate the topology from the chassis to the cluster.*

*In the upper-left corner of the following figure, IOM A is connected to the fabric interconnect that acts as fabric A. When IOM B is connected to the fabric interconnect B, the PID, VID, serial number, fabric ID, and cluster ID are exchanged. Because the fabric ID matches, the fabric interconnect knows that IOM B is not a connection attempt by IOM A to register to a second fabric.*

*In the upper-right corner of the figure, IOM A attempts to register with fabric interconnect B. When fabric interconnect B reads the fabric ID “A” from IOM A, it rejects the registration.*

*In the lower part of the illustration, IOM A registers with the fabric interconnect A and exchanges IDs. When IOM B attempts to register with the fabric interconnect B, the fabric interconnect detects an invalid cluster ID and rejects the registration. The two fabric interconnects have not formed a cluster.*

![Fabric Interconnect Cluster-to-IOM Connectivity](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/cluster_IOMconnect.png)

### Cisco UCS X-Series Modular System

*The Cisco UCS X-Series with Cisco Intersight is a modular system that you manage from the cloud. It is shaped to meet the needs of modern applications and improve operational efficiency, agility, and scale through an adaptable, future-ready, modular design.*

![UCS X-Series Modular System](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/UCS_X-series.png)

*The Cisco UCS X-Series provides blade and rack server functionalities by offering compute density, storage capacity, and expandability in a single system. This functionality embraces a wide range of workloads in your data center.*

*The Cisco UCS X-Series Modular System begins with the Cisco UCS X9508 Chassis, which is engineered to be adaptable and future-ready. The chassis has a unified Ethernet fabric with Cisco UCS Intelligent Fabric Modules (IFMs) and Cisco UCS X-Fabric Technology. With the chassis’ midplane-free design, you can upgrade either fabric independently.*

*The Cisco UCS X210c M6 Compute Node has third-generation Intel Xeon Scalable processors. It provides the functionalities of both blade and rack servers by offering compute density, storage capacity, and expandability in a single form factor.*

*Cisco UCS X-Series X9508 Chassis provides the following:*

- *Seven-rack unit (7RU) form factor*

- *Eight front-facing flexible slots for compute nodes and PCIe nodes*

- *Two Cisco UCS 9108 IFMs for unified Ethernet fabric*

- *Optional Cisco UCS X-Fabric Technology with the Cisco UCS X9416 X-Fabric Module*

![UCS X-Series Modular System 2](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/UCS_X-series2.png)

*Cisco UCS X210c M6 Compute Node has these features:*

- *Up to two third-generation Intel Xeon Scalable processors*

- *Up to 12 TB of memory*

- *Up to two Cisco UCS VICs exclusively designed for Cisco UCS x210 Compute Node:*

1. *Cisco UCS VIC 14425 is a 4x25 Gbps Ethernet and FCoE-capable mLOM*

2. *Cisco UCS VIC 14825 is a 4x25 Gbps Ethernet and FCoE-capable mezzanine card*

3. *Cisco UCS VIC 15231 is a 2x100 Gbps Ethernet and FCoE-capable mLOM*

- *Up to six SAS, SATA, and NVMe disk drives plus up to two M.2 drives*

- *Up to two GPUs*

*Cisco UCS X210c M7 Compute Node has these features:*

- *Four 4th Gen Intel Xeon Scalable Processors with up to 60 cores per processor.*

- ***Up to 16 TB of main memory with 64x 256 GB DDR5-4800 Memory DIMMs mLOM VICs:***

1. *Cisco UCS VIC 15420 occupies the server’s mLOM slot. It enables up to 50 Gbps of unified fabric connectivity to each chassis IFM for 100 Gbps connectivity per server with secure boot capability.*

2. *Cisco UCS VIC 15231 occupies the server’s mLOM slot. It enables up to 100 Gbps of unified fabric connectivity to each chassis IFM for 100 Gbps connectivity per server.*

3. *Cisco UCS VIC 15230 occupies the server’s mLOM slot. It enables up to 100 Gbps of unified fabric connectivity to each chassis IFM for 100 Gbps connectivity per server with secure boot technology.*

- ***Optional mezzanine card:***

1. *Cisco UCS 5th Gen VIC 15422 can occupy the server’s mezzanine slot at the bottom rear of the chassis. This card’s I/O connectors link to Cisco UCS X-Fabric technology. An included bridge card extends this VIC’s 2x 50 Gbps of network connections through IFM connectors. It brings the total bandwidth to 100 Gbps per fabric (for a total of 200 Gbps per server) with secure boot capability.*

2. *Cisco UCS PCI Mezz card for Cisco UCS X-Fabric can occupy the server’s mezzanine slot at the bottom rear of the chassis. This card’s I/O connectors link to Cisco UCS X-Fabric modules and enable connectivity to the Cisco UCS X440p PCIe Node.*

- ***Security:*** *The server supports an optional Trusted Platform Module (TPM). Additional features include a secure boot Field-Programmable Gate Array (FPGA) and ACT2 anticounterfeit provisions.*

- *Up to six SAS, SATA, and NVMe disk drives plus up to two M.2 drives.*

*The Cisco UCS X215c M8 provides these main features:*

- ***CPU:*** *Up to two 5th and 4th Gen AMD EPYC Processors with up to 160 cores per processor and up to 384 MB of Level 3 cache per CPU.*

- ***Memory:*** *Up to 6 TB of main memory with 24 256 GB DDR5 6000 MT/s or DDR5 4800 MT/s DIMMs depending on the CPU installed.*

- ***Storage:*** *Up to six hot-pluggable SSDs or NVMe 2.5-inch drives with a choice of enterprise-class RAIDs or pass-through controllers. Up to two M.2 SATA drives with optional hardware RAID, or up to two M.2 NVMe drives in pass-through mode.*

- ***Optional front mezzanine GPU module:*** *The Cisco UCS front mezzanine GPU module is a passive PCIe Gen 4.0 front mezzanine option. It supports up to two NVMe drives and two half height, half length (HHHL) GPUs.*

- ***mLOM Virtual Interface Cards (VICs):***

1. *Cisco UCS VIC 15420 occupies the server’s mLOM slot. It enables up to 50 Gbps of unified fabric connectivity to each of the chassis IFMs for 100 Gbps connectivity per server.*

2. *Cisco UCS VIC 15230 occupies the server’s mLOM slot. It enables up to 100 Gbps of unified fabric connectivity to each of the chassis IFMs for 100 Gbps connectivity per server with secure boot technology.*

- ***Optional mezzanine card:***

1. *Cisco UCS 5th Gen Virtual Interface Card (VIC) 15422 can occupy the server’s mezzanine slot at the bottom rear of the chassis. This card’s I/O connectors link to Cisco UCS X-Fabric technology. An included bridge card extends this VIC’s two 50 Gbps of network connections through IFM connectors. It brings the total bandwidth to 100 Gbps per fabric (for a total of 200 Gbps per server) with secure boot technology.*

2. *Cisco UCS PCI Mezz card for X-Fabric can occupy the server’s mezzanine slot at the bottom rear of the chassis. This card’s I/O connectors link to Cisco UCS X-Fabric modules and enable connectivity to the Cisco UCS X440p PCIe Node.*

*The Cisco UCS X210c M8 provides these main features:*

- ***CPU:*** *Up to two Intel Xeon 6 Scalable Processors with up to 86 cores per processor and up to 336 MB of Level 3 cache per CPU.*

- ***Memory:*** *Up to 8 TB of main memory with 32 256 GB DDR5-6400 DIMMs and support for MRDIMMs at up to 8000 MT/s.*

- ***Storage:***

1. *Up to nine hot-pluggable EDSFF E3.S NVMe drives with a new pass-through front mezzanine controller option new to the Cisco UCS X210c M8.*

2. *Up to six hot-pluggable SSDs or NVMe 2.5-inch drives with a choice of enterprise-class RAIDs or pass-through controllers with four lanes each of PCIe Gen 5 connectivity.*

3. *Up to two M.2 SATA drives or two M.2 NVMe drives for flexible boot and local storage capabilities.*

- ***Optional front mezzanine GPU module:*** *The Cisco UCS front mezzanine GPU module is a passive PCIe Gen 4 front mezzanine option. It supports up to two U.2 or U.3 NVMe drives and two HHHL GPUs.*

- ***Optional PCIe node connectivity for additional GPU support:*** *You can pair the Cisco UCS X210c M8 Compute Node with the Cisco UCS X440p PCIe Node. This configuration supports up to two x16 full-height, full-length dual-slot GPUs, or four x8 full-height, full-length single-slot GPUs.*

- ***mLOM virtual interface cards:***

1. *Cisco UCS VIC 15420 occupies the server’s mLOM slot. It enables up to 50 Gbps (two at 25 Gbps) of unified fabric connectivity to each of the chassis IFMs for 100 Gbps connectivity per server with secure boot technology.*

2. *Cisco UCS VIC 15230 occupies the server’s mLOM slot. It enables up to 100 Gbps of unified fabric connectivity to each of the chassis IFMs for 100 Gbps connectivity per server with secure boot technology.*

- ***Optional mezzanine card:***

1. *Cisco UCS VIC 15422, a 5th Gen virtual interface card, can occupy the server’s mezzanine slot at the bottom rear of the chassis. This card's I/O connectors link to Cisco UCS X-Fabric technology. An included bridge card extends this VIC’s four 25 Gbps of network connections through IFM connectors. It brings the total bandwidth to 100 Gbps per fabric (for a total of 200 Gbps per server).*

2. *Cisco UCS PCI mezzanine card for Cisco UCS X-Fabric can occupy the server’s mezzanine slot at the bottom rear of the chassis. This card’s I/O connectors link to Cisco UCS X-Fabric modules and enable connectivity to the Cisco UCS X440p PCIe Node.*

*Cisco UCS X440p PCIe Node has support for up to eight GPUs.*

*The system comprises modular components that you can assemble into systems through the Cisco Intersight cloud-operations platform.*

*Cisco Intersight brings the power of software as a service (SaaS) to deliver proactive monitoring, automation, and optimization of workloads across hybrid cloud environments. This functionality allows you to take these actions:*

- ***Adapt to any application:*** *Consolidate onto a platform that combines blade server density and efficiency with rack server expandability.*

- ***Prepare for the future:*** *Embrace new technology and cut risk with a system that is designed to support future technology with management delivered by SaaS.*

- ***Simplify with cloud operations:*** *Respond at the speed and scale of your business by shaping Cisco UCS X-Series to workload requirements with Cisco Intersight.*

### Cisco UCS Intelligent Fabric Modules

*Cisco UCS X-Series devices are connected by two Cisco UCS 9108 IFMs. Like the fabric extenders in the Cisco UCS 5108 Blade Server Chassis, these modules carry all network traffic to a pair of Cisco UCS 6400 series or Cisco UCS 6536 Fabric Interconnect devices.*

*Establishing a singular point of network connectivity and control within a system ensures deterministic latency. This latency allows for the placement of workloads without being constrained by whether the compute nodes reside in the same chassis.*

*Cisco UCS 9108-25G IFM features include the following:*

- ***Server ports:*** *Up to 200 Gbps of unified fabric connectivity per compute node with two IFMs.*

- ***Uplink ports:*** *Eight 25 Gbps SFP28 ports.*

![UCS Intelligent Fabric Modules](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/UCS_fabric_modules.png)

*Cisco UCS 9108-100G IFM:*

- ***Server ports:*** *Up to 200 Gbps of unified fabric connectivity per compute node with two IFMs.*

- ***Uplink ports:*** *Eight 100 Gbps QSFP8 ports.*

![UCS Intelligent Fabric Modules 2](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/UCS_fabric_modules2.png)

*The unified fabric carries management, production, and FCoE traffic to the fabric interconnects. There, management traffic connects to the Cisco Intersight cloud operations platform. FCoE traffic passes to native Fibre Channel interfaces through universal ports on the fabric interconnects. Production Ethernet traffic passes upstream to the data center network. Up to two IFMs plug into the back of the Cisco UCS X9508 chassis.*

*The IFMs serve as line cards in the chassis and multiplex data from the Cisco UCS X210c or X410c compute nodes to the fabric interconnect. They also monitor and manage chassis components such as fan units, power supplies, environmental data, the LED status panel, and other chassis resources. The compute node’s keyboard, video, mouse (KVM) data, Serial over LAN (SoL) data, and Intelligent Platform Management Interface (IPMI) data also travel to IFMs for monitoring and management purposes. To provide redundancy and failover, the IFMs are always used in pairs.*

### Fabric Interconnect Cluster-to-Intelligent Fabric Modules Connectivity

*Cisco UCS X9108-100 G or X9108-25 G IFM in each Cisco UCS X-Series chassis maintains connectivity from the Cisco UCS X9508 X-series chassis to fabric interconnects of the 4th or 5th generation.*

![Fabric Interconnect Cluster-to-Intelligent Fabric Modules Connectivity](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/fabric_interconnect_cluster-to-intelligent_fabric_modules_connectivity.png)

*Do not mix cables between the upper and lower IFMs. Use 25 GbE or 100 GbE cables as appropriate for the model of IFM in the chassis.*

## Additional Notes and Conclusion:

Cisco documentation: written by machines, for machines, to gently repel humans. Let's distill the signal from that UCS / UCS-X fog.

Here’s the stuff *actually worth remembering:*

- **UCS is about identity, not hardware:** servers are disposable meat; *service profiles are the soul.* MACs, WWNs, firmware, boot order — all abstracted so you can kill a blade and resurrect it elsewhere without grief.

- **Clusters matter because management must never blink:** establishing a UCS Manager cluster (or Intersight domain relationship in UCS-X) ensures state consistency, quorum, and zero “split-brain hell.” If clustering breaks, you don’t lose packets — you lose reality.

- **UCS-X is UCS admitting the future is modular chaos:** compute is disaggregated, I/O is centralized, and Intersight becomes the brain instead of Fabric Interconnects alone. Think “cloud control plane wearing on-prem clothes.”

- **Fabric is the hidden god:** everything hinges on unified fabric behaving perfectly — FC, FCoE, Ethernet, management — one fabric to rule them all, one misconfig to ruin your night.

- **Mental model to keep:** *UCS = stateless servers + authoritative control plane.* If you remember only that, the rest snaps into place like a quiet click in the dark.
