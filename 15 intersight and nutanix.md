# Cisco Intersight

*Cisco Intersight is a cloud and on-premises management platform that delivers intuitive computing. The platform offers a more intelligent level of management. It enables IT organizations to analyze, simplify, and automate their environments in ways that were impossible with prior generations of tools.*

*This capability empowers organizations to achieve significant savings in TCO and to deliver applications faster to support new business initiatives. The advantages of model-based management of the Cisco UCS platform (including Cisco Intersight) extend to Cisco UCS servers, Cisco Compute Hyperconverged with Nutanix, and third-party systems such as the Pure and NetApp solutions.*

*Cisco Intersight works by communicating with the devices in the data center through a secure connection. By simply associating different systems, IT staff can consistently align policy, server personality, and workloads. You can create these policies once and use them with minimal effort to deploy and manage data center systems. The result is improved productivity and compliance and a lower risk of failures due to inconsistent configuration.*

![Cisco Intersight](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/cisco_intersight.png)

## Cisco Intersight License Tiers

*Cisco Intersight uses a free or a subscription-based license with multiple editions. Customers can purchase a subscription duration in any combination of 1, 3, or 5 years. They can choose the Cisco UCS Server volume tier that they need for the selected subscription duration.*

*Several deployment types are available for Cisco Intersight. The most common (and most feature-rich) is the cloud Intersight software as a service (SaaS) that Cisco provides and hosts. The other two deployment types are designed for installation on the private infrastructure of a customer.*

*A Cisco Intersight virtual appliance is an on-premises deployment of Cisco Intersight and is installed and hosted on the customer infrastructure. The Intersight virtual appliance allows users more control over their data. Not all features of the cloud edition are available, though connectivity to the cloud is still required for operation.*

*Cisco Intersight Private Virtual Appliance is an on-premises deployment type that eliminates the need for connectivity to the cloud.*

*You can apply several license tiers to the systems in your Cisco Intersight:*

1. ***Base:***

- *Cisco Intersight Base provides a centralized systems health monitoring, TAC support, system inventory, customizable dashboard, tagging, search, and the capability to launch native endpoint management interfaces. Base only applies to Cisco Intersight SaaS.*

2. ***Essentials:***

- *Platform-level settings for user and SDK/API access, permissions, licensing, and audit.*

- *Support for health monitoring, tagging and search, basic data inventory, and multifactor authentication*

- *Support for Cisco UCS basic inventory, firmware, and dashboard management.*

- *Simplification of compute infrastructure management with policy-based configurations using server profiles for Cisco UCS, converged, and hyperconverged infrastructure.*

- *Monitor and track telemetry information (data collection every 10 minutes and 90 days of historical data).*

- *Custom explorations with Metrics Explorer.*

- *Cisco Intersight Add-On for Splunk*

- *Power policy management for servers, BIOS, and OS as well as dynamic power rebalancing.*

- *Support for Cisco Compute Hyperconverged with Nutanix.*

- *Monitor your Cisco UCS infrastructure from Splunk.*

- *Receiving alerts about endpoint devices that are impacted by supported security advisories and field notices along with recommended remediation.*

- *Acceleration of troubleshooting with hardware compatibility alerts, proactive RMAs, and automated gathering and uploading of log files for Cisco Intersight–connected devices through the Cisco Technical Assistance Center (TAC).*

3. ***Advantage:***

- *Create and execute complex workflows with a drag-and-drop designer or incorporate existing automations from Ansible, Terraform, or other tools using the Cisco Intersight API and SDKs.*

- *Simplify the cloud experience with visibility of virtualization infrastructure and normalization of operations across multiple clouds.*

- *Monitor and track telemetry information with enriched topology views that provide error metrics and network bandwidth/utilization along with data collection every minute and two years of historical data.*

- *Diagnose device-level issues using error metrics and view detailed information for physical connection links by hovering on connection links.*

- *FlexPod converged infrastructure inventory, including servers, networking, storage, virtualization, and Cisco fabric interconnects.*

- *Third-party storage support: view inventory and alarms of storage arrays and automate day-to-day operations using supported storage tasks.*

- *Resolve issues faster by ingesting data from Cisco Intersight–connected servers, storage, data-center networking, and virtual machines into the ServiceNow IT operations management platform using the Service Graph Connector for Cisco Intersight plug-in and by raising incidents in ServiceNow for alarms and advisories from Cisco Intersight using the Cisco Intersight Incident Management Integration plugin, available on the ServiceNow store.*

*Note: Each higher licensing tier includes all the features of the lower tiers. The Premier license includes all the features available in Cisco Intersight. Fabric interconnect devices do not require licenses.*

## Cisco Intersight Connectivity and Device Connector

*To integrate the devices in your data center with Cisco Intersight, a connectivity service must be present on the systems that you want to register to Intersight. This system must be capable to receive regular automated updates, since Intersight is a continually developing platform. Cisco implements new features and improvements continuously, and these new features must also appear on the side of the systems that Intersight is managing.*

*This connectivity is provided through an integrated service on the side of the registered systems that is called a device connector. A device connector is an autonomous system that interacts with the hardware or software it is integrated into and provides communication with Cisco Intersight.*

*The device connector requires the minimum version of the system for installation on the system that you want to register to Intersight. Afterward, it can update independently of the device firmware or Nutanix software. This functionality allows the continual support for new features without any disruptive actions for the registered system.*

*Since Cisco Intersight cloud deployment relies on internet connectivity to provide management features to the Cisco data center, the security of its connectivity is extremely important. The connection between the device connector and Intersight is provided through a secure Transport Layer Security (TLS) socket. It establishes a secure two-way link over which data can transmit.*

*The device or system must support the device connector to register it to Cisco Intersight:*

- *The device connector initiates the TLS secured connection toward Intersight. You can also use an HTTP proxy to provide connectivity for additional security.*

- *A system is registered to Intersight by copying a device ID and claim code to Intersight, after the internet access is available on the management network.*

![Intersight Connectivity](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/intersight_connectivity.png)

*Note: HTTP proxy avoids direct connection of the managed systems to the internet since it forwards HTTP traffic only. It allows connections to be established in only one direction.*

*If a system does not support the device connector directly, such as the case with third-party devices that Intersight supports, you need an additional on-premises virtual appliance. This appliance acts as a proxy for communication with devices and systems that do not support Cisco Intersight directly through an integrated device connector.*

*An automated installer installs the Intersight Virtual Appliance as a virtual machine. Only a very basic configuration is necessary to deploy the appliance, but you must configure network connectivity to Intersight and the managed systems.*

*The Intersight Virtual Appliance can facilitate advanced features of Cisco Intersight. Examples include Intersight Workload Optimizer, which allows automated reconfiguration of your workload by following the requirements of the workload. It automatically applies appropriate actions to optimize performance or resource consumption.*

## Cisco Intersight Features

*Cisco Intersight uses its secure connectivity to deliver an ever-expanding number of features to the users, regardless of where their infrastructure is located and how distributed or centralized it is.*

*The goal of Intersight is to provide a single pane of glass for the entire Cisco data center and allow you to integrate third-party systems into its customizable interface.*

*Intersight has these features:*

- *Unified connectivity, monitoring, and management*

- *Configuration, provisioning, and policy configuration*

- *Inventory information, status, and capacity planning*

- *Enhanced support and end-customer experience*

- *Proactive notifications and advisories*

- *Hardware Compatibility List*

- *Third-party integration support*

*Since Cisco Intersight gathers the information and notifications from all the systems that are associated with it, it can provide powerful monitoring features. However, the monitoring side of Cisco Insight is not its main feature.*

*The main advantage of Cisco Intersight is its capability to manage and maintain associated resources. This functionality minimizes the overhead of the infrastructure and decreases the total cost of ownership (TCO).*

*Once all the devices and systems in your data center are registered in Cisco Intersight, you can inspect individual components and follow their health and potential issues. Whenever a known issue of a specific device or software version is discovered, Intersight can warn you of affected systems in your infrastructure through its HCL. This action eliminates manually comparing your systems to published advisories.*

*Intersight uses a modular system that transcends supported devices and systems beyond the Cisco data center portfolio and can integrate products from other vendors as well. It offers additional value to the already wide range of features of the Cisco portfolio.*

### Additional Notes:

Here’s the **Intersight essence without the Cisco perfume:** it’s a cloud-based control plane for UCS, HyperFlex, and friends, built around **policy-driven management** (profiles, templates, immutability over snowflake configs). The key thing to remember is **decoupling identity from hardware**—servers become disposable, configs live as code, and scaling or replacing nodes stops being ritual sacrifice. Cluster relationships matter because Intersight treats clusters as first-class objects: lifecycle, firmware, monitoring, and compliance are handled **centrally**, not box-by-box. If you remember one thing: *Intersight is about operational consistency, not raw technical magic.*

Now the spicy take: people use this because *enterprises buy outcomes, not freedom.* Proprietary + licensed sucks philosophically, but it buys vendors *support contracts, liability transfer, and predictability,* which boards love. It’s very common in the wild—banks, healthcare, gov, big enterprises—especially where uptime and audits matter more than hacker joy.

# Cisco Compute Hyperconverged with Nutanix

*Cisco and Nutanix have partnered to create a hyperconverged solution that is built on Cisco compute hyperconverged nodes and Nutanix hyperconverged software. The Cisco Compute Hyperconverged with Nutanix solution combines the operational simplicity of the Nutanix Cloud Platform with the flexibility and efficiency of the award-winning Cisco UCS. It enables organizations to easily deploy, scale, and upgrade hyperconverged clusters with a more sustainable, future-ready solution.*

*This partnership includes the following:*

- *Cisco UCS C-series and X-series*

- *Cisco Intersight*

- *Nutanix*

- *Nutanix Acropolis Operating System (AOS)*

- *Nutanix Prism*

- *Acropolis Hypervisor (AHV)*

*The Cisco Compute Hyperconverged nodes family delivers performance, flexibility, and resiliency in a high-capacity solution. Physically, nodes are deployed into clusters, with a cluster consisting of one or more Cisco Compute Hyperconverged servers.*

*The Cisco Compute Hyperconverged with Nutanix family of appliances delivers preconfigured Cisco UCS servers that are ready for deployment as nodes to form Nutanix clusters in various configurations. Each server appliance contains three software layers: Cisco UCS server firmware, hypervisor (Nutanix AHV), and hyperconverged storage software (Nutanix AOS).*

## Cisco Compute Hyperconverged X-Series System

*The Cisco Compute Hyperconverged X-Series System uses front-loading, vertically oriented compute hyperconverged X210c M7 All NVMe nodes with Intel Xeon Scalable Processors and Cisco UCS X440p PCIe Node accelerator nodes. In the rear of the chassis, a unified Ethernet fabric is supplied with Cisco UCS 9108 100G IFMs and the Cisco UCS X9416 X-Fabric Module.*

![Hyperconverged X-Series](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/hyperconverged-X-series.png)

*Cisco Compute Hyperconverged X-Series Direct is a self-contained system with a pair of integrated Fabric Interconnect 9108 100G devices. You can use it if you do not want top-of-rack fabric interconnects and must support edge, retail, and small or remote-office use cases.*

*The Cisco Fabric Interconnect 9108 100G is an integrated 1, 10, 25, 40, and 100 Gigabit Ethernet, Fibre Channel over Ethernet (FCoE), and Fibre Channel switch. It offers up to 1.6 Tbps throughput and up to eight ports. The switch has six 40- and 100-Gbps Ethernet ports and two unified ports. They can support 40 or 100-Gbps Ethernet ports or eight Fiber Channel ports after breakout at 8-, 16-, and 32-Gbps Fibre Channel speeds.*

*The eight Fibre Channel ports after breakout can either operate as a Fibre Channel uplink port or as a Fibre Channel storage port. The switch supports two 1-Gbps speed after breakout, and all eight ports can break out for 10- and 25-Gbps Ethernet connectivity. All Ethernet ports can support FCoE. Beyond the eight external facing 100G ports, the Fabric Interconnect 9108 100G also provides eight 100G or 32 25G backplane Ethernet ports connectivity toward the Cisco UCS X-Series compute nodes. It depends on whether you are using the 100G or the 25G virtual interface card (VIC).*

**My Note:** Port breakout is a networking feature that allows a high-speed port on a device, like a switch, to be divided into multiple lower-speed ports. This enables better utilization of bandwidth and increases the number of connections available, making it useful for managing network traffic efficiently.

## Cisco Compute Hyperconverged with Nutanix Rack Servers

*The Cisco Compute Hyperconverged All-NVMe and All-Flash Server extends the capabilities of the Cisco Compute Hyperconverged with the Nutanix portfolio in a one or two rack units form factor.*

![Compute Hyperconverged with Nutanix](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/hyperconverged_nutanix_rack_servers.png)

*The following table shows the hardware specifications for the servers.*

![Compute Hyperconverged with Nutanix Specs](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/hyperconverged_nutanix_rack_servers_specs.png)

## Cisco Compute Hyperconverged Rack Servers

*The Cisco Hyperconverged C240 M7, C240 M8, C220 M7, and C220 M8 node families provide one- and two-unit form factor compute for hyperconverged infrastructure.*

![Compute Hyperconverged Rack Servers](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/hyperconverged_rack_servers.png)

*The following table shows the hardware specifications for the servers.*

![Compute Hyperconverged Rack Servers Specs](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/hyperconverged_rack_servers_specs.png)

## Cisco Intersight for Cisco Compute with Nutanix

*Cisco Intersight provides a cloud-hosted, management and analytics platform for all Cisco Compute Hyperconverged with Nutanix, Cisco UCS, and other supported third-party infrastructure deployed across the globe. It provides an efficient way of deploying, managing, and upgrading infrastructure in the data center, Remote Office/Branch Office (ROBO), edge, and colocation environments.*

![Cisco Intersight for Cisco Compute with Nutanix](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/cisco_intersight_compute_nutanix.png)

*Cisco Intersight is a software as a service (SaaS)-based management platform providing global visibility and fleet management for all Cisco Compute Hyperconverged with Nutanix nodes.*

## Nutanix Architecture

*The Nutanix hyperconverged infrastructure (HCI) converges the data center stack, including compute, storage, storage networking, and virtualization. Nutanix replaces the separate servers, storage systems, and SANs found in conventional data center architectures and reduces complexity.*

![Nutanix Architecture](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/nutanix_arhitecture.png)

*Each node in a Nutanix cluster includes compute, memory, and storage, and nodes are pooled into a cluster. The Nutanix Acropolis Operating System (AOS) software running on each node pools storage across nodes and distributes operating functions across all nodes in the cluster for performance, scalability, and resilience.*

*The Nutanix Prism management layer provides central access to configure, monitor, and manage virtual environments. It uses machine learning to mine large volumes of system data easily and quickly, generating actionable insights for optimizing all aspects of virtual infrastructure management.*

![Nutanix Architecture 2](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/nutanix_arhitecture2.png)

*Nutanix Prism has two core components:*

- ***Prism Element:*** *This service is built into the platform for every deployed Nutanix cluster. Prism Element fully configures, manages, and monitors Nutanix clusters running any supported hypervisor.*

- ***Prism Central:*** *Because Prism Element manages only the cluster that it is part of, each deployed Nutanix cluster has a unique Prism Element instance for management. Prism Central allows you to manage different clusters across separate physical locations on one screen and gain an organizational view into a distributed Nutanix environment.*

*Nutanix Foundation Central allows the creation of clusters from factory-imaged nodes (and the reimage of existing nodes that are already registered with Foundation Central) or remotely from Prism Central.*

*The Acropolis Hypervisor (AHV) is the Nutanix-native hypervisor that natively converges compute and storage into a single application. It offers powerful virtualization capabilities such as core virtual machine operations, live migration, virtual machine high availability, and virtual network management. These features are fully integrated in the infrastructure stack rather than being standalone products that require separate deployment and management.*

![Nutanix AOS](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/nutanix_AOS.png)

*The AOS provides the core functionality that the workloads and services running on the platform use. It uses a distributed approach that combines the storage resources of all nodes in a Nutanix cluster to deliver the capabilities and performance that you expect from SAN storage. It eliminates much of the cost, management overhead, and hassle that comes with managing traditional storage.*

*Intelligent software enables AOS Storage to appear on a hypervisor—such as VMware ESXi or Nutanix AHV—as a single, uniform storage pool. Over the years, Nutanix has expanded its features and capabilities, making AOS Storage a leader in software-defined distributed storage.*

*Each node in a Nutanix cluster runs a virtual machine that is called the Controller Virtual Machine (CVM). The CVM runs the distributed storage services and other services necessary for a cluster environment. Because storage and other Nutanix services are distributed across the nodes in the cluster, no one entity is a single point of failure. Any node can assume leadership of any service.*

![Nutanix AVH Node Arhitecture](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/nutanix_AVH.png)

## Intersight Standalone Mode

*In Intersight Standalone Mode (ISM), nodes are directly connected to a pair of top of rack (ToR) switches. Servers are centrally managed using Cisco Intersight.*

![Intersight Standalone Mode](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/intersight_standalone_node.png)

*ISM requires Cisco Compute Hyperconverged rack servers M7 or M8. The servers are connected to the ToR Cisco Nexus 9000 switch with 10G, 25G, 40G, and 100G Ethernet uplinks. The servers are claimed through Cisco Intersight. Once the servers are claimed into Cisco Intersight, the Nutanix cluster will install on these nodes using Nutanix Prism and the Foundation Central software components.*

*The installation for this type of deployment requires Prism Central and Intersight. ISM supports single-, two-, and up to 32-node clusters. This mode is suitable for new or existing Nutanix customers. Depending on the size of the cluster, it may run at the edge or at the data center.*

## Intersight Managed Mode

*In Intersight Managed Mode (IMM), nodes connect to Cisco UCS fabric interconnects, and Intersight manages them.*

![Intersight Managed Mode](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/intersight_managed_mode.png)

*IMM works only with Cisco Compute Hyperconverged X210c M7 (or later generation) All NVMe nodes that are installed in Cisco UCS X-Series chassis. An IMM cluster can scale from a single Cisco UCS X-Series chassis with eight nodes up to 32 nodes. Multiple clusters under the same fabric interconnect domain are supported.*

*Single Cisco UCS X-Series chassis deployment uses Cisco Fabric Interconnect 9108. This solution is suitable for most applications at the edge.*

*With multiple chassis deployment, Cisco UCS X-Series devices are uplinked to the Cisco Fabric Interconnect 6400 or 6500. This model is appropriate for all kinds of applications running at the data center.*

## Cisco UCS Managed Mode

*The Cisco UCS Managed Mode (UMM) deployment option connects the server to Cisco Fabric Interconnect devices operating in Cisco UCS Manager mode.*

![UCS Managed Mode](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/UCS_managed_mode.png)

*UMM requires Cisco Compute Hyperconverged rack servers M6 or M7. The servers connect to the pair of Cisco Fabric Interconnects 6400 or 6500. The installation for this type of deployment is performed using the Nutanix Foundation virtual machine.*

*UMM supports single-, two-, and up to 32-nodes clusters. This mode is suitable for new or existing Cisco UCS customers. Typically, UMM clusters are deployed at the data center.*

### Additional Notes:

**Nutanix — the mental model that sticks!**

Nutanix is basically **“storage + compute + virtualization smashed into one appliance”**. Instead of SAN + FC + zoning + pain, every node has disks, and all nodes cooperate as a **single distributed system**. Think *scale-out cluster*, not *central brain.*

**The core ideas worth remembering:**

- **HCI (Hyper-Converged Infrastructure):**

Each node = CPU + RAM + local disks. No external SAN. Storage is pooled and replicated across nodes automatically.

- **AOS (Acropolis OS):**

This is the real secret sauce. It’s Nutanix’s distributed storage + control plane that runs on every node. If AOS is down, Nutanix is down.

- **CVM (Controller VM):**

Every node runs a CVM. CVMs talk to each other and *are* the storage system. No CVM = that node’s storage brain is gone.

- **Replication Factor (RF):**

RF2 or RF3 = how many copies of data exist across nodes. This replaces RAID *and* SAN redundancy thinking.

- **Metadata everywhere:**

No single metadata master → fewer “this thing just bricked the cluster” moments.

- **Hypervisor flexibility:**

AHV (their KVM-based hypervisor), but also supports ESXi and Hyper-V. AHV is free — that’s not an accident.

- **Prism:**

Single-pane-of-glass UI that doesn’t hate you. Genuinely one of Nutanix’s strongest points.

**Cluster formation (this is the gold part)**

- Minimum *3 nodes* (realistically).

- Cluster is formed by **discovering nodes + electing leadership dynamically.**

- No FC zoning, no LUN carving, no “which WWPN did I typo”.

- Expansion = add node → cluster rebalances automatically.

This is why people love it in practice.

**Why Nutanix exists at all:**

Traditional DC model: *SAN + FC switches + zoning + HBAs + firmware hell + vendor finger-pointing*

Nutanix says: *“No SAN. Ethernet only. Software handles redundancy.”* That’s not marketing fluff — it actually reduces failure domains and operational complexity.

**Critical perspective:**

- *Deployed in the wild?*

Yes. A lot. Especially mid-size enterprises, VDI, ROBO sites, private clouds.

- *Is it proprietary?*

Absolutely. AOS, Prism, licensing — all closed.

- *Vendor lock-in?*

Real, but operationally comfortable. You trade freedom for sanity.

- *Licensing pain?*

Yes, but still often cheaper than SAN + FC + maintenance contracts + staff burnout.

The one-line memory hook: *Nutanix = “SANless SAN” built from software, not switches.*
