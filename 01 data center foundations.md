# Describing the Data Center Network Architectures

## Cisco Data Center Architecture Overview

*The modern data center differs considerably from older data centers. Data centers still must support the same functions: applications, access to those applications, high availability, security, and resiliency, to name a few functions. But the modern data center must also support a mobile workforce, varying device types, and a high-volume, data-driven business. To meet these ever-expanding requirements, Cisco offers the Cisco Unified Data Center platform.*

*The Cisco Unified Data Center platform architecture combines compute, storage, network, and management. It is more than a portfolio of new devices. This platform automates IT functions in physical and virtual environments. The result is the increased use of your new infrastructure. Your IT department can more quickly meet the needs of clients and administrators, all with a simplified (and more automated) approach to data center management.*

![Cisco Unified DataCenter](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/cisco_unified_datacenter.png)

*The figure shows the three functional areas in Cisco Unified Data Center:*

- **Cisco Unified Management:** *This platform uses automation, orchestration, and lifecycle management tools to simplify deployment and operation of physical or bare-metal installs. It includes virtual or hypervisor-supported environments with a heavy focus on virtual machines, plus private, public, and hybrid clouds. These management options remain focused on a centralized, multivendor, multi-interface (GUI, scripting, and third-party applications) approach.*

- **Cisco Unified Fabric:** *This solution combines high-performance data and storage networking into a single, next-generation chassis that offers simplified deployment that can meet budget needs. A unified fabric also offers high-speed connectivity, high availability, and increased application performance, while reducing security risks in multitenant environments.*

- **Cisco Unified Computing System (Cisco UCS):** *This highly scalable computing solution integrates servers, flash-memory acceleration, and networking with embedded management and automation to simplify operations for physical, virtual, and cloud workloads.*

## Three-Tier Network: Core, Aggregation, and Access

*A network design depends on the time or era, the available technology, and even the vendor solution that is used for a final product. Change is constant: as times change, technology changes, and approaches to a solution certainly change. A model is required that can remain consistent over time while adapting to changing technologies and requirements.*

![Three Tier Network](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/three_tier_network.png)

*The three-tier design approach is an architectural model. It defines functions and responsibilities, where those functions happen, and how tiers or layers interconnect. Using this approach, engineers design solutions that endure over time because users can upgrade them as technology changes, and they evolve as needs grow.*

*The three-tier approach to design is originally known as the Cisco Enterprise Composite Network Model (ECNM). This model is often used for campus server and desktop connectivity. It is also used for private and public external connections—for example, the campus edge (consisting of private WAN and VPN connections) and public internet connectivity. The model evolved to include a design for small and medium-sized environments, which need a particular focus on security and certain architectures.*

*In a data center design, the three tiers are core, aggregation, and access:*

1. **Core:** *The core layer of the three-tier model serves as the campus-wide backbone connecting all other switch blocks. Consider the core as the center of a sunflower from which all other petals or switch blocks radiate outward. The core layer provides fast packet transport for all other connecting switch blocks and is the boundary for the corporation when connecting to the outside world.*

2. **Aggregation:** *The aggregation layer of the three-tier model illustrates the high number of connected ports that the layer aggregates from the access layer below into the core layer above. The aggregation layer provides a termination point for VLANs, also referred to as Layer 2 boundaries. It is a first point of routing in the physical network and a central point for configuration of Layer 3 features, such as route summarization, DHCP relay, and access control lists (ACLs). In a data center discussion, you may find a Cisco UCS Series fabric interconnect as an aggregation layer device.*

3. **Access:** *The access layer of the three-tier model serves as a physical access point for end stations or hosts to connect to the network or aggregation layer. In a data center design, the access layer connects servers and hypervisors, such as VMware vSphere ESXi, into a certain VLAN or with a trunk connection to transport multiple VLANs.*

*Based on the size of the solution, it is common to see aggregation layer features present at the access layer or even a layer called the virtualized access layer. This approach allows a design to “push” the intelligence as close to the end device as possible, offering the greatest degree of reach and control. For example, a larger-scale design may have higher-end access layer switches offering routing and ACL features. They provide greater control over the traffic before it enters the aggregation and core layers.*

*A three-tiered approach offers many data center benefits:*

- **Modular and scalable solution:** *A tiered design enables you to add technologies in the future that were not necessary or unavailable during the initial design. The modular approach is achieved by designing with switch blocks and adding on switch blocks. A switch block is a new tier that you add to a central core. A corporation may start with a design idea for their campus environment. They can then add a campus edge, VPN, or internet edge switch block that securely and redundantly connects the campus to satellite offices or the internet.*

*A data center example is adding a server switch block that is complete with redundant Cisco UCS fabric interconnects that connect into fabric extenders within a Cisco UCS server chassis that houses blade servers.*

*A tiered design allows you to better recognize the features that you need, where to put them, and which devices require the features within your final solution. Knowing which feature goes where helps when purchasing the devices. For example, a company may benefit by purchasing an entry-level switch and using the base switch license when connecting to desktops at a small remote location. In this scenario, the company does not need an enterprise-class Cisco Nexus 9500 chassis with an advanced feature set license to support a small branch location.*

- **Investment protection:** *A tiered design endures over time. The tiered approach adapts to and supports the needs of changing environments and technologies. This adaptability allows a corporation to continue with a design philosophy and reuse (or repurpose) equipment, perhaps at a lower level, as the corporation upgrades in the future.*

- **Easy-to-discuss and easy-to-learn solution:** *A tiered design with its modular approach makes it easy to discuss and learn about a particular section of the solution. By referencing a switch block (for example, servers that are connected by Cisco UCS), you can focus on only the design, architecture, and features in that portion of your network.*

## Spine-and-Leaf Network

*A three-tiered architecture is invaluable for an overall corporate solution. However, the recent growth in data centers and advances in data center technologies introduced a new approach to data center design. This new approach is known as spine-and-leaf architecture, or simply spine and leaf. The spine-and-leaf architecture resembles the original Cisco collapsed core design when using the three-tier approach.*

*The collapsed core topology merges the core and aggregation layers into a single layer, maintaining all services of both. This approach reduces the number of devices, cabling, and the complexity of the design. This approach was made possible by the technological capabilities of Cisco devices since the devices in the collapsed core must provide all the necessary features. The spine-and-leaf approach further improves the concept of collapsed core topology.*

![Spine And Leaf](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/spine_leaf.png)

*A spine-and-leaf approach, also known as a Clos network, allows architects to build a data center that can expand and collapse (be more elastic) as necessary. You can add components (servers, hypervisors, switches, and ports) dynamically as a load of applications grows. This elastic approach ideally supports data centers that host a few applications that are distributed across many hosts, adding hosts dynamically as the solution grows.*

*The main concerns that the spine-and-leaf model addresses are the addition of new leaf (access) layer switches and the redundant cross-connections that are necessary for a scalable data center. It is estimated that a spine-and-leaf model allows for 25 percent greater scalability over a three-tier model when used for data center designs.*

*In a spine-and-leaf topology, each leaf device connects to each spine device, which provides extra benefits for a modern data center: scalability, high performance (up to 400 Gbps), traffic optimization and control.*

*Data centers have the following challenges:*

- *Increased port density from connecting servers and hypervisors*

- *Increased throughput from 10G, 25G, 40G, 50G, 100G, and 400G port speeds*

- *Increased use of hypervisors and virtual machines*

- *Increased number of features moving from physical deployment to virtual deployment*

*If oversubscription of a link occurs, the process for expanding capacity is straightforward. You can add an extra spine switch and extend uplinks to every leaf switch, resulting in the addition of interlayer bandwidth and reduction of the oversubscription. If device port capacity becomes a concern, you can add a new leaf switch by connecting it to every spine switch and adding the network configuration to the switch.*

*With a spine-and-leaf architecture, the traffic crosses the same number of devices to get to another server, regardless of the server to which the leaf switch is connected. This approach keeps latency at a predictable level because a payload only must hop to a spine switch and another leaf switch to reach its destination.*

## Storage Area Networks

*Traditional Ethernet IP-based networks have great benefits in communication over long distances because they have many integrated systems that manage traffic loss and latency. The tendency to expect packet loss and out-of-order traffic has historically made them far less suitable for storage communication.*

*Relatively inexpensive cabling also meant that Ethernet transfer speeds were not keeping up with the data center demands. Even today, most home computers and laptops still run 1 Gigabit Ethernet, while in the data center 400 Gigabit Ethernet connections are available.*

*Before the storage networks and centralized storage arrays became prominent, most servers ran directly attached Redundant Array of Independent Disks (RAID) storage. In RAID storage, the drives are located inside a server chassis and attached to RAID cards. RAID cards create virtual storage drives by merging many drives into a single virtual drive that provides failure redundancy and data protection capabilities. Although RAID is common in many servers today, it is mostly used in single-server deployments and small environments.*

*With the evolution of the data center and ever greater demand for redundancy and ease of maintenance, the more traditional RAID model was becoming constraining. The concept of a centralized storage array was introduced.*

*A storage array is an extra physical system within the data center that is dedicated to providing storage to external devices. Instead of those devices (usually servers) containing the storage within the chassis (such as with RAID), that data is instead stored in the central storage array. This functionality makes the compute part (RAM and CPU) independent of storage and allows you to make hardware replacements and upgrades much easier. For example, when you replace a server, you no longer must migrate the data from one server to another, since it is always stored on the storage array.*

*For storage arrays to become possible, a way to effectively transfer data from storage arrays to servers was necessary. Since Ethernet was not well suited to the job at the time, a new network stack was introduced, called storage area network (SAN). Although this concept also expanded over time with Ethernet-based storage protocols, a SAN network is traditionally a fully separate network using a reliable and low-latency communication protocol instead of Ethernet. In the Cisco space, this protocol is Fibre Channel.*

![Storage](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/storage.png)

*A SAN topology uses a dedicated set of edge and core switches, creating a new storage switch block. The switches that are being used in the SAN network are called Cisco Multilayer Director Switches (Cisco MDS) and look like LAN switches but are designed with one major difference. They provide a network with lossless data transmission and low latency.*

*Dedicated network and SAN switches were dictated by Fibre Channel Protocol (FCP). FCP needs devices that support the protocol stack on the hardware level. Fibre Channel networks use specialized host adapters and networking equipment that allow higher speeds. They use less overhead and allow a lower load on the CPU, which was very important on older systems.*

*This type of approach is called a two-tier storage network and is most commonly used in environments with larger storage solutions.*

### Two-Tier Storage Network Benefits

*The two-tier architecture is scalable and redundant on many levels. It offers a high degree of throughput, but a small or small-to-medium–sized environment may not need a solution of this size. In that case, a one-tier storage network design with only one set of SAN switches is ideal.*

*SANs offer many benefits:*

- **Scalability:** *A SAN allows multiple servers to access storage located in one storage array. Scalability in terms of storage capacity is also much better, because you can simply add more disks into the storage array if necessary.*

- **Security:** *SAN implements security features that allow or disallow storage access to different parts of storage in a network that runs completely separately from the Ethernet access. This way, servers can access the storage, but users cannot, even if they have physical access to the server.*

- **Dual fabric redundancy:** *The storage array connects with servers through two different but identical storage networks (fabrics). Those two fabrics are separated on a physical level and provide two paths always. If failure or misconfiguration occurs on one of the fabrics, there is still another fully operating path between the storage array and servers on the other side.*

- **Easier maintenance:** *Since storage is not directly attached to the server, you can replace the server and retain the storage at the same time. Dual fabrics in the topology also make a difference here, because you can maintain the system without downtime.*

*Network design in SAN networks includes who will use the storage array. Consider a company whose new servers are the only devices accessing the new storage array. These servers have a hypervisor installed, which is software that allows you to host multiple emulated computer systems on a single server. These emulated computers are called virtual machines and provide the functionality of physical computers. No other server throughout the company campus or remote locations will access the newly installed storage array. Such an environment is ideal for directly attaching the storage array to the servers that will use the array.*

![Storage2](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/storage2.png)

*The central points of connectivity are the redundant Cisco UCS fabric interconnects, which provide connectivity southbound to the Cisco UCS Blade Server Chassis. The chassis holds multiple servers and allows direct connectivity to the storage array while providing access to northbound data connections. Fibre Channel uplink allows servers to access storage, while Ethernet uplink connects servers with a LAN network and provides internet access.*

*Cisco solved the hardware duality of Ethernet and Fibre Channel communication by offering devices with unified ports. You can configure unified ports for both Fibre Channel and Ethernet communication. In this way, customers have much more flexibility.*

### Drawbacks of Storage Area Networks

*Despite the many benefits that SANs offer, there are drawbacks of having a separate network for storage and a large monolithic storage array at the center of that network:*

- *Increased complexity due to additional switches and connections.*

- *Forklift upgrade is necessary when the storage array must be upgraded. The term forklift upgrade is used to describe the process of replacing one set of IT equipment with another, generally used in storage to refer to the time-consuming process of array replacement.*

- *Multiple teams are necessary for deployment, maintenance, and management.*

![Storage3](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/storage3.png)

*The separation of centralized storage, storage networks, and servers often leads to silos. When individual sections of the infrastructure are maintained by different teams of experts, these teams operate within a so-called silo. A silo represents an independent administrative unit that must be consulted before making changes to a section of infrastructure. Silos can pose challenges even when implementing minor changes. Each individual team must be involved, with their own process structure and specific skill sets, causing delays and even severe bureaucratic overhead. This situation can create management overhead when maintaining an infrastructure.*

*A drawback of storage networks is also increased complexity. The process of adding additional SAN switches, connections, and storage arrays creates a separate network that must be properly configured and managed. This environment is more complex and harder to deploy, maintain, and also troubleshoot when problems occur.*

*Because company growth is an unpredictable factor, network designers typically design a much more performant network than is necessary. They tend to choose network devices that provide higher speeds and bandwidth and storage devices that provide much more storage capacity than is necessary to allow for future growth. This side effect of infrastructure scalability limitations causes a much greater upfront cost to accommodate future growth. It also means that not all capabilities of the infrastructure are utilized at any given moment.*

*For this reason, some storage arrays offer a possibility to add more storage into the array if there is a storage space shortage. This approach increases the total storage space but is usually limited by the physical size of the storage array. At the same time, adding storage to the array does not expand the capabilities of the SAN network to the storage array. With more storage in a storage array, there is also a greater need for higher throughput of the storage network.*

*An extra consideration with hardware upgrades is making sure that hardware from different vendors works together. Systems architects usually spend a lot of time on interoperability of devices and protocol implementations. They must ensure that storage devices are interoperable with SAN switches and servers, a required performance is reachable, and certain standards will be met. They must check multiple device datasheets and compare many device models.*

*There is often no single point of support in a multivendor environment for all vendors. This situation can increase the time needed to fix potential problems.*

### Converged Data Center Systems

*Converged systems attempt to address some general issues of a SAN-based infrastructure, such as interoperability and design limitations. Converged systems network refers to an integrated IT infrastructure that combines computing, storage, and networking components into a single optimized package, allowing for centralized management and efficient resource sharing.*

*Converged systems still use storage arrays connected through SAN switches. In fact, they are basically SAN systems, but the equipment is easier to design, order, deploy, and maintain than these more traditional systems.*

- *Validated designs to ease design and ensure optimal performance*

- *Single point for purchase and support for the entire solution*

- *Well-established performance and scalability*

- *Well-known protocol stack lowers training overhead*

- *Can be prebuilt in a factory*

![Converged Systems](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/converged_systems.png)

*Converged systems are prevalidated and tested designs of traditional systems. Cisco engineers make sure that devices work as expected and that maximum performance is achieved for a specific workload. These validated systems are documented as Cisco Validated Designs with instructions on how to install, configure, and manage the entire system. Several purpose-built validated designs are available for different workloads and implementations.*

*Converged systems provide a single point of purchase, so you can order an entire system from Cisco that includes a storage solution from a third-party vendor. Support is similar, as you can contact Cisco or the storage vendor support when there is a problem with any part of the converged system. This approach accelerates problem fixes and reduces potential downtime.*

*Each converged solution consists of Cisco Unified Computing System (Cisco UCS) servers, Cisco Multilayer Director Switch (Cisco MDS) devices, and Cisco Nexus switches with a storage solution from a third-party vendor.*

*Converged solutions on the market:*

- **FlexPod** *(Cisco and NetApp)*

- **FlashStack** *(Cisco and Pure Storage)*

- **Hitachi Adaptive Solutions for CI** *(Cisco and Hitachi)*

*Remember to always refer to a converged solution as one integrated system and not as individual devices.*

##  Hyperconverged Storage Systems

*By looking at current IT trends and the usage of DevOps practices, users have realized that the SAN-based storage infrastructures do not fit the quickly evolving needs of modern data centers. Developing new software and delivering it to the markets quickly is a day-to-day necessity. Nor can companies afford the complex management, long deployment times, and multiple teams that are necessary for SAN infrastructure operation.*

*By removing the storage array and SAN from the system and replacing it with software-defined Ethernet networking and software-defined storage, a new system appeared on the market. This system is called hyperconverged infrastructure (HCI).*

*Hyperconverged infrastructure is built with x86-based servers that connect to a LAN network. Each server has its own processor, memory, and local disks. The figure shows three servers connected to a LAN. Each server is virtualized with a hypervisor (the example in the figure is VMware ESXi), and each server also runs an intelligent piece of software for hyperconvergence. This intelligent piece of software usually comes in the shape of a controller virtual machine.*

![Hyperconverged Infrastructure](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/hyperconverged_storage.png)

*Controller virtual machines communicate with each other to create one large pool of resources for the virtual machines to consume. All the disks in all the servers in the hyperconverged group are bundled together using hyperconvergence software to present it to virtual machines as a Network File System (NFS) volume. The virtual machine administrator can then simply define one or more datastores and use them when provisioning the virtual machines.*

**Note:** *Software-defined storage (SDS) is software that manages data storage resources and functionality and has no dependencies on the underlying physical storage hardware. Hyperconverged systems combine disks in different servers, and software abstracts them into one single storage pool.*

### Hyperconverged Infrastructure Benefits

*In most hyperconverged solutions, the minimum size group is three servers (commonly referred to as nodes). The servers are then transformed into a single pool of compute, memory, and storage resources.*

*When you are running low on resources in your group, you can scale up the group by adding more drives into the servers or scale out by adding more nodes. It would seamlessly expand your pool of resources. Expanding the group in a hyperconverged solution usually means buying new servers, connecting them to the upstream LAN connection, and running an expansion wizard. As you have probably discovered, this approach is simpler for scaling compared to traditional two- and three-tier infrastructure.*

*The same principle applies to server retirement or maintenance. When you retire a server or turn it off to replace a component, the pool of resources for your virtual machines becomes smaller. Similarly, if one of the servers fails, the pool of resources will shrink.*

*Expansion or shrinking of the group (either through retiring old servers or through failures) should not impact the workload. Benefits of hyperconverged infrastructure include easy deployment and expansion, failure handling, and no need for a SAN network.*

![Hyperconverged Storage 2](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/hyperconverged_storage2.png)

*Another benefit of such a system is the deployment process. The deployment consists of preparing the infrastructure, such as top-of-rack (ToR) switches and various protocols, connecting servers to an upstream Ethernet connection, and running the installation wizard. You have no need to configure any SAN protocols such as Fibre Channel or Small Computer Systems Interface over IP (iSCSI). Nor must you configure Fibre Channel zoning and device aliases or create or mask a logical unit number (LUN). The deployment of hyperconverged systems is fast and easy.*

*Because a hyperconverged solution is a very flexible and relatively simple architecture in your data center, it can easily serve as the foundation for building your enterprise private cloud. You can start small and expand when necessary, so you have no worries about overprovisioning or underprovisioning resources for your applications and business. The expansion by adding more nodes also removes the need for regular forklift upgrades.*

### Cisco Compute Hyperconverged with Nutanix

*Some vendors define hyperconverged solutions as software only, which means that when you buy hyperconverged software, you can use any hardware. But you must follow the hardware compatibility list (HCL) for your individual solution, or you will have no vendor support. Often, huge disadvantages emerge when using mixed hardware, and uniform systems are highly recommended.*

*Therefore, the Cisco hyperconverged system tightly integrates software and hardware for an easy-to-install and easy-to-operate solution.*

![Nutanix](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/nutanix.png)

*Cisco and Nutanix have come together to offer a simple, comprehensive hyperconverged solution. The Cisco Compute Hyperconverged with Nutanix solution combines the Cisco UCS server, networking, and software as a service (SaaS) management with the Nutanix HCI foundation. This fully integrated and validated system has flexible deployment options and a unified, enhanced support model backed by two organizations.*

*You can deploy compute nodes on Cisco UCS hyperconverged 1RU, 2RU, or UCS-X Modular Servers with All-Flash or All-NVMe drive capacity options.*

*Each server appliance contains three software layers:*

- **Server firmware:** *Cisco UCS*

- **Hypervisor:** *Nutanix Acropolis Hypervisor (AHV) or vSphere ESXi*

- **Hyperconverged storage software:** *Nutanix Acropolis Operating System (AOS)*

*You can interconnect and manage the servers in three ways:*

- **Cisco UCS Managed Mode:** *The nodes connect to a pair of Cisco UCS 6400 Series or Cisco UCS 6500 Series fabric interconnects and are managed as a single system using UCS Manager.*

- **Intersight Standalone Mode:** *The nodes connect to a pair of top-of-rack (ToR) switches and servers and are centrally managed using Cisco Intersight.*

- **Intersight Management Mode:** *The nodes connect to a pair of Cisco UCS 6400 Series or a pair of Cisco UCS 6500 Series fabric interconnects or Cisco UCS 9108 100G fabric interconnect and servers and are centrally managed using Cisco Intersight.*

*Nutanix HCI converges the data-center stack with compute, storage, storage networking, and virtualization, replacing the separate servers, storage systems, and SANs found in conventional data-center architectures and reducing complexity.*

*Each node in a Nutanix cluster includes compute, memory, and storage, and nodes that are pooled into a cluster. The Nutanix AOS software running on each node controller virtual machine pools storage across nodes and distributes operating functions across all nodes in the cluster for performance, scalability, and resilience.*

*The Nutanix Prism management layer provides central access to configure, monitor, and manage virtual environments.*
