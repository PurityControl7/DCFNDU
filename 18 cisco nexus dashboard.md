# Describing Cisco Nexus Dashboard

*IT is constantly being challenged to quickly align with company business needs. People want to easily obtain data center resources. A good starting point for automation is infrastructure delivery. Infrastructure includes a broad set of processes. Cisco offers a wide variety of tools that can help you automate tasks to be more efficient in delivering data center resources.*

*In this course, you will learn about Cisco Nexus Dashboard and Cisco Nexus Dashboard Fabric Controller.*

## Cisco Nexus Dashboard Overview 

*This content describes the Cisco Nexus Dashboard platforms and presents several use cases.*

*In the modern day and age, workloads run in various infrastructures and environments. Examples include cloud, data center, Internet of Things (IoT) edge, and colocations. Each of these tools has specific setup and operation procedures.*

*When you have workloads stretching between an on-premises data center and the cloud, you have the challenge of connecting the two platforms where your application is running. Furthermore, the application must be designed in such a way that it can distribute to various locations. The containerized architecture of modern applications allows you to achieve that goal.*

*To deploy applications in these environments, and especially to scale them, the best strategy is to use automation. Automation will give you predictable results and accurate deployment. Once your application is deployed, you need visibility into it to monitor how it is running and to see if you need resource adjustments.*

*Another aspect that you must consider when you deploy your applications in multiple locations is security. Technologies exist to enforce and monitor security policies so that your data is secure and your application is compliant.*

![Nexus Dashboard](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/nexus_dashboard.png)

*The Cisco Nexus Dashboard is a platform for the following services:*

- ***Insights:*** *A comprehensive solution for analysis, trending, anomaly detection, alerting, and other actions.*

- ***Orchestrator:*** *A solution to set up and operate multisite fabrics.*

- ***Data Broker:*** *A solution to build a packet broker network for further analysis.*

- ***Fabric Controller:*** *A solution to deploy Cisco Network Operating System (Cisco NX-OS)-based Virtual Extensible LAN (VXLAN) fabrics.*

- ***Fabric Discovery:*** *A solution to monitor Cisco NX-OS fabrics.*

- ***SAN Controller:*** *A solution to deploy and monitor SAN fabrics.*

## Physical and Virtual Cisco Nexus Dashboard Platforms

*Cisco Nexus Dashboard appliances are available in physical and virtual form factors. You can deploy the Cisco Nexus Dashboard cluster by using at least three physical server nodes.*

*The physical Cisco Nexus Dashboard deployment runs on three server nodes that are based on a Cisco Unified Computing System (Cisco UCS) C220 and C225 rack server:*

![SE-NODE-G5S](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/SE-NODE-G5S.png)

![SE-NODE-G5S Overview](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/SE-NODE-G5S_overview.png)

*You need a minimum of three servers to form a cluster. For deployments that require more performance, you can add up to four additional worker nodes. For additional redundancy, you can deploy up to two standby nodes also.*

## Virtual Cisco Nexus Dashboard Platform

*An alternative to a physical deployment is using virtual machines. Virtual machines give you more flexibility regarding placement; however, you must provide the required virtual CPU, memory, and disk resources on your shared hardware.*

![Nexus Dashboard 2](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/nexus_dashboard2.png)

*Two form factors of a virtual machine are available: App and Data. You select the appropriate one depending on which Cisco Nexus Dashboard application you are planning to run. For example, Cisco Nexus Dashboard Insights require Data nodes. They have more resources to accommodate telemetry streaming requirements.*

*Data nodes also require underlying solid-state drive (SSD) or Non-Volatile Memory Express (NVMe) storage. Choose an appropriate datastore in the hypervisor that you know is solid state.*

*Virtual Cisco Nexus Dashboard supports production deployments for Cisco Nexus Dashboard Insights, Cisco Nexus Dashboard Orchestrator, and Cisco Nexus Dashboard Fabric Controller (Cisco NDFC).*

*You also have two options to deploy virtual nodes in the public cloud:*

1. *Amazon Web Services (AWS) option:*

- *Instance type: m5.4xlarge*

- *Storage: 100G gp2 SSD, 300G gp2 SSD*

- *Network: Virtual private cloud (VPC)*

2. *Azure option:*

- *Instance type: Standard_D16s_v3*

- *Storage: Operating system 50 GB; data 250 or 500 GB*

- *Network: Two virtual networks (VNETs)*

*The cloud deployment option is very practical, because you do not need to own the physical nodes, nor do you need resources on your virtualization clusters. Instead, you pay for the resources through a subscription to the public cloud. The Cisco Nexus Dashboard virtual machines are available in the AWS and Azure marketplaces.*

*You can use the cloud-based Cisco Nexus Dashboard nodes to host applications as you would with on-premises based ones.*

## Cisco Nexus Dashboard Cluster Node Roles

*Cisco Nexus Dashboard nodes can operate in one of three roles: master, worker, and standby.*

- *Master nodes form the control plane of a cluster. A master node performs scheduling tasks when point of delivery (PoD) units are instantiated based on the resources or load. This node maintains the state of the cluster and three nodes, and it must be on the same form factor. It can also replace one master node at any time.*

- *Worker nodes are for horizontal scaling-out and to execute containers applications. Four additional nodes must be the same type as the master node (physical or virtual).*

- *Standby nodes increase high availability in master node failure. Only a standby node can be promoted to a master node.*

*For example, Cisco NDFC tolerates the failure of up to one master node. The Cisco Nexus Dashboard and NDFC cluster goes into read-only when two master nodes are down.*

## Cisco Nexus Dashboard One View

*Cisco Nexus Dashboard One View provides a single cohesive view of all the sites that are being managed and the services that are installed across Cisco Nexus Dashboard clusters:*

- *Cisco Nexus Dashboard Federation is an association of several Cisco Nexus Dashboard clusters. It allows working across with them as if they were a single entity and simplifies the consumption of their resources.*

- *Cisco Nexus Dashboard clusters onboard other Cisco Nexus Dashboard clusters and create a trusted environment. It allows you to learn about those clusters and for them to communicate and share information with each other.*

- *Information that is shared between clusters is visible on each cluster within that federation. The data is also accessible from each cluster.*

- *Applications can query information that relates to other clusters in the federation for purposes such as onboarding (for example, Cisco Nexus Dashboard Insights and Sites) or grouping.*

*Cisco Nexus Dashboard One View provides a single view of all Cisco Nexus Dashboard clusters in a federation. This capability saves you time from logging in to every other Cisco Nexus Dashboard and viewing data of its applications locally.*

*You must have the remote username to set up and use Cisco Nexus Dashboard Federation. Afterwards, you only log in to the one Cisco Nexus Dashboard.*

## Viewing Other Cluster Information

*You can view other cluster information:*

- *After connecting a cluster, it will appear on the* ***Multi Cluster Connectivity*** *table.*

- *You can connect more clusters or disconnect clusters from the table.*

- *The cluster name on the header bar becomes a link to select the specific Cisco Nexus Dashboard group.*

- *The Central Dashboard is added to the header bar.*

- *The local cluster and federation manager are marked in the list.*

![Cluster Configuration](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/cluster_configuration.png)

*Adding a cluster to a federation in the Admin Console is straightforward. Once you have the cluster that is configured there, you can see its connectivity status, name, and URL to cross-launch the cluster user interface directly.*

## Central Dashboard

*The Central Dashboard is a primary benefit of One View.*

![Central Dashboard](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/central_dashboard.png)

*On the Central Dashboard, you can view a global summary of all your Cisco Nexus Dashboard clusters, including health information, connectivity status, and running services. You can then also review the statuses of each group.*

## Cisco Nexus Dashboard Insights Key Features

*The key features of Cisco Nexus Dashboard Insights are in three main groups:*

- *Assurance and compliance*

- *Visibility and troubleshooting*

- *Advisory and maintenance*

![Nexus Dashboard Insights](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/dashboard_insights.png)

*Assurance and compliance functions include configuration assurance, prechange analysis, and delta analysis. These functions are especially useful as planning tools. Another useful feature is the Connectivity Explorer, which is very intuitive. You can “ask” Cisco Nexus Dashboard Insights to perform a connectivity analysis to check if an endpoint can reach an IP address or another endpoint.*

*Visibility and troubleshooting tools include connectivity analysis, endpoint analytics, flow analytics, and topology view.*

*Advisory and maintenance tools include various Product Security Incident Response Team (PSIRT) and preupgrade alerts. Advisories include software and hardware-based known issues or hardware types, field notices, email notifications. Cisco Technical Assistance Center (Cisco TAC) assist is also available.*

*Note: In the case of physical Cisco Nexus Dashboard appliances, the processing cluster must be deployed on* ***1, 3, or 6*** *physical nodes. You can add up to two additional standby nodes to 3-node or 6-node physical clusters for disaster recovery. Single-node clusters do not support standby nodes. In a virtual Cisco Nexus Dashboard cluster, you must deploy the cluster as six virtual machines. Three must be data nodes with larger resource specification, and three must be application nodes. Such processing power is required because incoming telemetry data streams from a substantial number of switches.*

## Cisco Nexus Dashboard Insights Overview Page

*You can quickly review health scores, advisories, and anomalies on the Overview page.*

![Dashboard Insights Overview](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/dashboard_insights_overview.png)

*On the* ***Overview*** *page, you are presented with a summary of alerts, an anomaly score, the timeline, and a breakdown of anomalies and advisories. All the elements that you see are clickable, so if you are interested in leaf nodes with a* ***Critical*** *anomaly score, click it to see the affected leaf nodes. This way, you can further drill down into an anomaly.*

## Cisco Nexus Dashboard Orchestrator Application Use Cases

*The Cisco Nexus Dashboard Orchestrator (Cisco NDO) tool runs on top of a Cisco Nexus Dashboard cluster. The main function of Cisco NDO is to configure, orchestrate, and monitor multiple data center sites with a common configuration. These sites can run networks based on either Cisco Application Centric Infrastructure (Cisco ACI) or Cisco Nexus switches in Cisco NX-OS mode. The switches are managed by the Cisco NDFC, formerly Data Center Network Manager (DCNM).*

*Use the Cisco Nexus Dashboard Orchestrator to manage multiple data center sites:*

- *Cisco ACI-based sites*

- *Cisco Cloud ACI sites*

- *Cisco NDFC-based sites*

![Dashboard Orchestrator](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/dashboard_orchestrator.png)

*Cisco Nexus Dashboard can unify operations from the on-premises infrastructure (Cisco ACI) or Cisco NX-OS with Cisco NDFC to colocations and to the public cloud.*

*Regardless of the site type, you can use the same procedures to deploy network configuration elements to multiple sites. If one of your sites is an on-premises data center running Cisco ACI and the other site is a Cisco Cloud ACI instance in one of the public clouds, both sites are managed in the same way.*

*The Cisco NDO deploys all the configuration necessary to have “stretched” network structures, such as tenants, virtual routing and forwarding (VRF) instances, and endpoint groups (EPGs) that interconnect between multiple sites. This way, you can have mixed workloads, with some applications or components running on the on-premises data center network and some running in the public cloud.*

## Cisco Nexus Dashboard Fabric Controller Application

*Cisco NDFC is a comprehensive management and automation solution for all Cisco Nexus and Cisco Multilayer Director Switch (Cisco MDS) platforms that are powered by Cisco NX-OS.*

*Cisco NDFC provides management, automation, control, monitoring, and integration for deployments spanning LAN, SAN, and IP Fabric for Media (IPFM) fabrics. Cisco NDFC facilitates seamless interconnectivity, automation, and management for hybrid cloud environments.*

*You can take advantage of these three main functions of Cisco NDFC:*

- ***Management:*** *Cisco NDFC gives you fabric-oriented configuration and operations management. It is optimized for large deployments with little overhead, but traditional deployments are supported, and you can customize them. Cisco NDFC also provides Representational State Transfer (REST)-ful application programming interfaces (APIs), allowing easy integration with Cisco or third-party overlay managers.*

- ***Automation:*** *You can use Cisco NDFC to bootstrap and deploy new fabrics in private and hybrid cloud deployments. The Cisco best practices are built into the fabric builder policy templates. The automatic bootstrap occurs with the click of a button, reducing provisioning times and simplifying deployments.*

- ***Monitoring and visualization:*** *Cisco NDFC maintains the active topology monitoring views per fabric into the new Cisco NDFC user interface. You can also combine it with Cisco Nexus Dashboard Insights (NDI) to get advanced support for Day 2 operations.*

*Cisco NDFC has the following features:*

- *Single pane of glass for data center fabrics*

- *VXLAN EVPN new deployment fabric provisioning and operation*

- *VXLAN EVPN existing deployments fabric onboarding and operation*

- *Classic LAN monitoring or operation*

- *Specialty cases, such as IP Fabric for Media (IFM) and SAN Controller roles*

*You can use Cisco NDFC to provision new data center fabrics based on Cisco Nexus switches. Provisioning can be zero-touch by using the PowerOn Auto Provisioning (POAP) mechanism to automatically bring up switches and build a VXLAN Ethernet VPN (EVPN) fabric on top of them.*

*If you have a provisioned fabric, you can onboard this fabric into Cisco NDFC. You will have the capability to monitor and configure such a fabric.*

*You also have the possibility to monitor only fabrics, for which you use the Fabric Discovery role. This role is noninvasive and allows you to simply monitor a fabric. Switches in this fabric can also be “classic” or legacy, without using VXLAN EVPN.*

## Cisco Nexus Dashboard Fabric Controller Overview Dashboard

*Cisco NDFC displays the Overview dashboard that represents your single pane of glass.*

![Nexus Dashboard Fabric Controller Overview](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/cisco_NDFC.png)

*The* ***Fabric Health*** *pane shows you the health of your Cisco NDFC-based fabrics. The* ***Event Analytics*** *pane displays any alarms pertaining to the switches in your fabric. You can also see if your switches are synchronized to the latest configuration in the fabric. The view includes a summary of switch health, roles (leaf or spine), switch hardware, software versions, and other elements. The* ***Overview*** *pane serves as your single pane of glass where you can quickly spot irregularities in the fabric.*

*Many other panes are available, including the* ***Network Topology pane,*** *which displays your switches that interconnect with links, configured networks, VRFs, endpoints, and other elements.*

## Cisco Nexus Dashboard Data Broker Application

*The Cisco Nexus Dashboard Data Broker provides pervasive packet and network visibility for network and security operations teams. It allows them to programmatically manage aggregating, filtering, and forwarding of complete flows to various analytics tools.*

*The main use cases of the Cisco Nexus Dashboard Data Broker include the following:*

- *Consolidate monitored traffic flows and transport them to analysis devices.*

- *Configure the test access port (TAP) or Switched Port Analyzer (SPAN) on production network switches.*

- *Manage the packet broker network.*

![Dashboard Data Broker](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/dashboard_data_broker.png)

*Using the Cisco Nexus Dashboard Data Broker controller software and Cisco Nexus switches, you have a new software-defined approach for monitoring both out-of-band and inline network traffic.*

*Cisco Nexus Dashboard Data Broker is a simple and scalable solution to monitor higher-volume and business-critical traffic. It replaces traditional, purpose-built matrix switches with one or more Cisco Nexus 3000 Series Switches or Cisco Nexus 9000 Series Switches. You can interconnect these switches to build a scalable network TAP and SPAN aggregation infrastructure.*

*Traffic is tapped into the bank of packet broker switches in the same manner as a matrix network. The data broker allows you to interconnect the Cisco Nexus switches to build a scalable TAP and SPAN aggregation infrastructure. You can use a combination of TAP and SPAN sources to bring a copy of the production traffic to visibility infrastructure, such as intrusion prevention systems (IPS) and intrusion detection systems (IDS) or some other analytics or monitoring systems.*

*Monitoring and analysis tools can be either physical appliances or virtual machines.*

*You can deploy Cisco Nexus Dashboard Data Broker in a few ways:*

- *As an application in the Cisco Nexus Dashboard*

- *Embedded in a switch, using Guest Shell*

- *On a virtual machine or server outside of TAP aggregation switches*

- *As an application on the Cisco Application Policy Infrastructure Controller (APIC) of a Cisco ACI fabric*

# Cisco Nexus Dashboard Fabric Controller Overview 

*Organizations around the world are facing numerous changes and, to cope with them, they rely on IT and especially on their network environments. Networks have evolved to become simpler, more agile, more proactive, more intuitive, and cloud-ready. Network administrators cannot rely on manual configuration of every switch if they want to meet business expectations.*

*Cisco Nexus Dashboard Fabric Controller (Cisco NDFC) has helped address many of the challenges of managing Cisco NX-OS switches. Cisco NDFC provides IT networking teams with end-to-end automation, extensive visibility, and consistent operations for data centers. These capabilities reduce the complexities and costs of operating Cisco Nexus and storage network deployments while connecting and managing hybrid cloud environments.*

*Cisco NDFC runs as a service on top of a physical or virtual Cisco Nexus Dashboard cluster.*

![Cisco NDFC](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/cisco-NDFC2.png)

*Cisco NDFC seamlessly integrates with other services running on the Cisco Nexus Dashboard, including the Cisco Nexus Dashboard Orchestrator (Cisco NDO) and Cisco Nexus Dashboard Insights (Cisco NDI):*

- ***Cisco NDO:*** *Cisco NDFC integration with Cisco NDO allows you to scale-out deployment to more than one Cisco NDFC instance. You can extend an on-premises Cisco NDFC-managed data center into a public cloud.*

- ***Cisco NDI:*** *Cisco NDFC integration with Cisco NDI provides granular and scalable visibility for Day 2 operations. Data center operations teams benefit hugely from the deep-dive troubleshooting and maintenance operations features.*

- ***Cisco Nexus Dashboard Data Broker:*** *This packet-brokering solution provides visibility into the customer’s network. The solution enables NetOps and SecOps teams to programmatically manage aggregating, filtering, and forwarding of copied or mirrored traffic to custom analytics tools. This functionality allows troubleshooting, capacity planning, network and application performance monitoring, security inspection, and compliance regulation conformance.*

## Cisco NDFC Modes

*In Cisco NDFC, features start with functional modalities. Depending on the mode that you choose, you can see the related features and manage them.*

![NDFC Modes](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/NDFC_modes.png)

*Cisco NDFC available modes:*

- ***Fabric Discovery:*** *Discover, monitor, and visualize LAN deployments.*

- ***Fabric Controller:*** *LAN Controller for Classic Ethernet with virtual Port Channel (vPC), routed, VXLAN, and IPFM deployments.*

- ***SAN Controller:*** *SAN Controller for Cisco MDS and Cisco Nexus switches provides enhanced SAN analytics with streaming telemetry.*

## Cisco NDFC Feature Manager

*Cisco NDFC has a run-time feature installer that helps you choose a mode at installation for LAN, SAN, or IPFM.*

![NDFC Feature Manager](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/NDFC_feature_manager.png)

*This feature-management capability allows you to selectively enable or disable different features, including Fabric Controller (LAN), SAN, IPFM, and Fabric Discovery. It allows you to dynamically choose the role of the Cisco NDFC cluster to activate additional functionalities on the Cisco NDFC role. You have no need to redeploy the cluster to safely change these roles.*

## Fabric Discovery Mode

*Cisco NDFC includes a base capability selection for Fabric Discovery. Fabric Discovery is a lightweight version of Cisco NDFC and, when enabled, supports inventory discovery and monitoring only.*

*This solution provides discovery, inventory, and topology for LAN deployments. It also enables Day 2 operations capabilities without deploying the Fabric Controller. This option lets users who are using Cisco NDFC for monitoring or Day 2 operations minimize resource utilization and further customize Cisco NDFC for their specific needs.*

*Configuration and provisioning are not supported when you choose this option. This mode also provides an install base for other Cisco Nexus Dashboard applications, such as Cisco NDI.*

## Fabric Controller Mode

*With Fabric Controller Mode, your organization gains comprehensive management, control, monitoring, troubleshooting, and maintenance capabilities for LAN with automated multicloud connectivity and IPFM. This mode supports various network fabrics including VXLAN networks, Layer 3–routed networks, three-tier vPC designs, and IP-based broadcast media fabrics.*

*Cisco NDFC in Fabric Controller mode offers full Cisco NDFC features excluding SAN, adding provisioning capabilities to the discovery.*

*Compliance management ensures that the network is in sync with intended deployments and allows users to deploy any corrections.*

*Once the devices are discovered, deploying a fabric becomes a quick and easy task. Templates follow best-practice configurations that Cisco supports. As an administrator, you can change some parameters. You can define overlay virtual routing and forwarding (VRF) instances, networks, and external connections under the fabric settings. You can then attach them to the devices that require them, assign networks to the interfaces, and define customized policies and templates for maximum flexibility.*

## SAN Controller Mode

*SAN Controller provides a single pane of glass to manage and monitor storage networks that are built with Cisco MDS multilayer SAN switches and Cisco Nexus switches. It also enables SAN insights to collect and visualize Cisco MDS SAN analytics data and capabilities.*

*It provides a web-based zoning interface to drastically reduce the cycle time for common administration tasks. It provides an inter-VSAN routing (IVR) zoning function also, all on the same page.*

*Compliance management ensures that the network is in sync with intended deployments and allows users to deploy any corrections.*

*With this mode, you benefit from an easy transition to a web-based configuration method.*

## IP Fabric for Media

*Cisco IP Fabric for Media (IPFM) enables content providers and broadcasters to migrate from legacy serial digital interface (SDI) to a flexible and scalable IP-based infrastructure. This migration meets the evolving demand for more content and rich media experiences, including more camera feeds, higher resolutions with 4K and 8K video, and virtual reality capabilities.*

![IPFM](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/cisco_IPFM.png)

*The IPFM fabric topology is specific to the operations performed by the Cisco NDFC IPFM and applicable for both the IPFM Non-Blocking Multicast (NBM) and Generic Multicast modes.*

*IPFM features include flow control, visualization and health, provisioning, and automation.*

*To ease your IPFM network provisioning, Cisco NDFC will now start supporting the availability of preconfigured policy templates to build your IPFM underlay in minutes.*

*Remember that IPFM and Fabric Builder are mutually exclusive in the Fabric Controller Mode.*

## Fabric Controller Topology

*The* ***Topology*** *window displays color-encoded nodes and links that correspond to various network elements, including switches, links, fabric extenders, port-channel configurations, vPCs, and others.*

![Fabric Controller Topology](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/fabric_controller_topology.png)

*The* ***Topology Operation*** *pane gives a quick overview of the fabric operational status. The* ***Topology Configuration*** *view provides a quick overview of the configuration compliance.*

*Cisco NDFC compares the actual configuration with the one rendered based on the intent and notifies the users if something is out of sync.*

*The map is interactive. Users can expand additional options by right-clicking the nodes.*

## SAN Controller Topology

*Similarly, the* ***SAN > Topology*** *window displays color-encoded nodes and links that correspond to various network elements, including switches, links, and VSANs.*

![SAN Controller Topology](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/SAN_controller_topology.png)

*The output shows a fabric that is named mds-fabric. When you click the switch, you will see the switch details on the right.*

## One View

*Cisco NDFC One View is a new feature that provides a single pane of glass to get a holistic view of the larger enterprise from within Cisco NDFC.*

![NDFC One View](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/one_view.png)

*This view provides high-level summary information about all the managed fabrics from within Cisco NDFC. This manager-of-managers view is critical for the successful management of multisite deployments. The Executive Dashboard provides important and relevant information, providing a centralized view of the fabric and switch health. This information greatly facilitates troubleshooting.*

*The functionality also provides built-in click-through capabilities so that the end user can explore that site in more detail to further enhance management and troubleshooting operations. Thanks to single sign-on (SSO), navigation to any of the servers that participate in Cisco NDFC One View is seamless. Regardless of the participating Cisco NDFC server, One View is always easily accessible through a breadcrumb, just a click away.*

*The feature also facilitates collaboration through easy access management using role-based access control (RBAC).*

*Furthermore, high availability is ensured; each participating Cisco NDFC server can run on a three-node active-active Cisco Nexus Dashboard cluster.*

*With all the benefits that this feature brings, it comes at no additional cost.*

## VMware vSphere Integration

*Cisco NDFC integrates VMware topology into its dynamic topology views.*

![VMware vSphere Integration](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vsphere_integration.png)

*In a virtualized environment, troubleshooting is initiated by identifying the network attachment point for virtual machines. This process discovers critical details such as the server, virtual switch, port group, VLAN, associated network switch, and physical port. These elements require multiple touch points and communication between the server, network administrator, and other applications such as compute orchestrator, compute manager, network manager, and network controller.*

*You “discover” a vCenter that controls the host-based networking on the fabric to show how the virtual machine, host, and virtual switches are interconnected. The network operator benefits from compute visibility, which is ordinarily the purview of compute administration.*

*As part of the Virtual Infrastructure Manager, and in addition to the Virtual Machine Manager (VMM) Visualizer, other features include:*

- *Kubernetes Visualizer*

- *OpenStack Visualizer*

*The Virtual Infrastructure Manager window displays the characteristics of the various instances and also allows the execution of management functions such as Add, Edit, Delete, and Rediscover instances.*

**My Notes:** Kubernetes is an open-source system for automating the deployment, scaling, and management of containerized applications. It is maintained by the Cloud Native Computing Foundation and is widely used for managing workloads in cloud environments and data centers.

OpenStack is an open-source cloud computing platform that allows users to manage and deploy virtual machines and other resources in public and private clouds. It provides a set of software tools for building and managing cloud infrastructure, making it easier to scale and manage computing resources.

### Summary

*In this course, you learned the following about Cisco data center platforms:*

- *Cisco Nexus Dashboard*

- *Cisco Nexus Dashboard Fabric Controller*
