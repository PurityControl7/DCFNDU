# Describing Cisco UCS Manager and Cisco Intersight

*Cisco Unified Computing System (Cisco UCS) Manager is a central management and monitoring system for Cisco UCS servers. The system allows you to manage large-scale Cisco UCS deployments through a common interface. It supports monitoring, logging, and GUI management of Cisco UCS devices.*

*The Cisco UCS Manager software runs on the Cisco Fabric Interconnect devices as part of the device design. After configuring the Cisco UCS Fabric interconnect domain, the Cisco UCS Manager interfaces are available on the IP addresses of the Cisco fabric interconnects.*

## Cisco UCS Manager Overview

*Users can manage the entire Cisco UCS domain (Cisco UCS Fabric Interconnect devices and attached Cisco UCS Servers) through one GUI interface that allows more approachable configuration, monitoring, and management.*

*Cisco UCS Manager centralizes the management of resources and devices, rather than using multiple management points. This centralized management includes the following:*

- *Managed switch elements (fabric interconnects), including expansion modules (GEMs) and device ports*

- *Managed chassis elements, including the Chassis Management Controller, fan modules, and power supplies*

- *Managed server elements, including disks, mezzanine cards, Cisco Integrated Management Controller (IMC), BIOS, and others*

*The management interfaces of the managed Cisco UCS servers are initialized in a specialized managed mode when connected to fabric interconnects. The management interface is Cisco Integrated Management Controller (Cisco IMC). On the servers, it no longer provides full functionality, because it expects you to make changes from the central Cisco UCS Manager interface.*

![Hight Level Management View](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/high_lvl_mgmt_arch.png)

*The user can interface with a single management interface instead of connecting to management interfaces of individual systems. The Cisco UCS Manager then communicates with the device firmware to apply changes initiated by the user in the Cisco UCS Manager interface.*

*High-availability deployments of fabric interconnects also provide Cisco UCS Manager management redundancy. Both fabric interconnect devices are used simultaneously for upstream communication, but only one device is the primary device for management purposes. The subordinate fabric interconnect synchronizes the configuration in real time with the primary device and takes over the primary status if there is a failure of the initial primary device.*

*Functionally, it does not matter which device is primary. When the initial primary device returns to normal operation, it will not take over the primary status until there is a failure that requires this action. Or, the user may initiate such a request manually.*

## Cisco UCS Manager Management Interfaces

*Cisco UCS Manager has several front-end options through which you can manage the devices in Cisco UCS Manager. Some interfaces, such as the HTTPS user interface, are meant for manual use by the users, while the application programming interface (API) functionality is intended for automation uses.*

*The native language of Cisco UCS Manager configuration is XML, and you can explore it through the Visore subsystem available on the Cisco UCS Manager IP address.*

*The XML determines several communication aspects of Cisco UCS Manager:*

- *The Cisco UCS Manager database stores all configuration data in the XML format.*

- *When creating all configuration backups, the configuration backup is in XML.*

- *Whether you perform configuration or monitoring in the Cisco UCS Manager GUI, CLI, or a third-party application, all communication is in the XML format.*

*Note: Besides the XML-based full configuration backups, Cisco UCS Manager also supports a full-state backup. This backup is a binary configuration that not only contains the configuration itself but the entire Cisco UCS Manager binary along with the configuration.*

*When you are performing actions on Cisco UCS Manager, the XML configuration of Cisco UCS Manager changes and the changes apply to the end systems. Cisco UCS Manager is always aware what configuration applies to what end system (server). If you wipe that server, you can restore its configuration from Cisco UCS Manager.*

![Cisco UCS Manager](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/cisco_UCS_manager.png)

*Both the GUI and CLI are written using the Cisco UCS Manager XML API. Third-party tools can also use the Cisco UCS Manager XML API to integrate with Cisco UCS Manager. When administrators submit configuration requests for a managed device to Cisco UCS Manager, Cisco UCS Manager will call the appropriate device manager to deploy the management request.*

*The operational state of a device is communicated back to Cisco UCS Manager and reflected in the user interfaces (GUI and CLI). The Cisco UCS Manager database also stores the running state of components. For example, if you reboot the fabric interconnects, Cisco UCS Manager knows which service profile is associated with a given server.*

## Cisco UCS Manager Monitoring and Logging

*Since Cisco UCS Manager is in constant communication with the managed devices, it also aggregates all the status messages from those devices. These messages are logged and trigger alarms or notifications when necessary.*

*If you are using an external monitoring system, you can point the external monitor toward Cisco UCS Manager to get the information on all the individual systems managed by it.*

*Cisco UCS Manager supports various industry-standard protocols for management, monitoring, and logging. The protocols include, but are not limited to, the following:*

- *Simple Network Management Protocol (SNMP)*

- *Systems Management Architecture for Server Hardware (SMASH) Command Line Protocol (CLP)*

- *Keyboard, video, mouse (KVM) over IP*

- *Intelligent Platform Management Interface (IPMI) specification*

- *Common Information Model (CIM) XML*

- *Serial over LAN*

- *Call Home*

- *Cisco UCS Manager CLI and GUI*

- *Cisco UCS Manager XML API*

*SNMP provides monitoring, the SMASH CLP is a CLI management interface, and KVM enables remote operating system installation. You can manage all these services through Cisco UCS Manager.*

![UCS Monitoring](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/USC_monitoring.png)

*Cisco UCS Manager not only acts as a central point of management but also the central point of monitoring for the Cisco UCS domain. To allow for high availability of external communication services, the fabric interconnect domain presents a virtual IP address outward (the Cisco UCS Fabric Interconnect Virtual Management IP [VIP]). This IP address always points to the primary FI device, and you can migrate it between devices. This works similarly to how gateway redundancy protocols work such as HSRP, only in the reverse direction.*

*The Cisco UCS Manager XML API and corresponding software development kit (SDK) allows you to create custom wrappers around Cisco UCS configuration and monitoring:*

- *Create a multitenant portal with your own presentation and access control interface.*

- *Integrate with customized automation tools.*

- *Create scripts and integrate into customized management solutions.*

- *Extend the base functionality that Cisco UCS Manager provides.*

*In modern data centers, orchestration of the managed resources is an important aspect of effective day-to-day operations. These wider orchestration systems can use the remote communication capabilities of Cisco UCS Manager to provide orchestration of the entire data center infrastructure.*

## Primary Components of the Cisco UCS Manager GUI

*The primary way users typically interact with the Cisco UCS Manager management system is through the Cisco UCS Manager HTTPS interface. The interface has a highly hierarchical structure of elements and a standard pane layout.*

![Cisco UCS Manager GUI](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/UCS_manager_GUI.png)

*On the left, you can see the sidebar with eight sections. By selecting a specific section, the navigation pane for that section will open. In the example in the figure, the Equipment section is selected. It provides you an overview of your servers and fabric interconnects.*

*The Fault summary area, located at the top, contains various icons that represent four levels of faults: critical, major, minor, and warning. The number under each icon represents the cumulative totals for all Cisco UCS components.*

*Next to the Fault summary area, another toolbar holds many functions, including search, help, exit, and pending activities.*

*The toolbar under the Fault summary area is called the Work pane tab bar. It offers the operator a navigation trail of object hierarchies that have already been traversed. This toolbar includes the ability to rapidly return to a previous location along the trail. The current location is at the far-right portion of this bar.*

*The largest part of the Cisco UCS Manager interface is called the Work pane. It offers granular detail that describes varying objects that have been selected in the Work pane tab bar. Function buttons for committing, saving, and discarding configuration changes are at the bottom of the Work pane.*

## Navigating the Cisco UCS Manager GUI

*The* ***Navigation*** *pane allows you to access various parts of the management system through a list of tabs that segment the functionally of the Cisco UCS Manager user interface.*

*Here you will become familiar with the eight sections of the Navigation pane.*

**Equipment Tab:**

*The* ***Equipment*** *tab allows you to select and interact with Cisco UCS components at the physical level. Major categories of the Equipment tab are* ***Chassis, Rack Mounts,*** *and* ***Fabric Interconnects.***

**Servers Tab:**

*In the* ***Servers*** *tab, Cisco UCS administrators create, modify, and delete logical server components such as service profiles and apply them to physical servers.*

*Items on the* ***Servers*** *tab are logical configuration elements that apply to physical servers.*

**LAN Tab:**

*In the* ***LAN*** *tab, Cisco UCS administrators create, modify, and delete configuration elements that are associated with the Ethernet network such as virtual LAN (VLAN) pools and virtual network interface card (vNIC) templates.*

*Items on the* ***LAN*** *tab are logical configuration elements that apply to physical servers.*

**SAN Tab:**

*In the* ***SAN*** *tab, Cisco UCS administrators create, modify, and delete configuration elements that are associated with Fibre Channel SAN and FCoE communications such as virtual SAN (VSAN) pools and virtual host bus adapter (vHBA) templates.*

*Items on the SAN tab are logical configuration elements that apply to physical servers.*

**VM Tab:**

*In the* ***VM*** *tab, Cisco UCS administrators create, modify, and delete configuration elements that are associated with VMware vSphere and Microsoft Hyper-V.*

**Storage Tab:**

*In the* ***Storage*** *tab, administrators manage storage with storage profiles. A storage profile specifies all the storage requirements of a service profile. Only local logical unit numbers (LUNs) are supported.*

**Chassis Tab:**

*In the* ***Chassis*** *tab, administrators can create chassis profiles and templates to manage storage, firmware, and maintenance characteristics of chassis systems like Cisco UCS S3260 Server.*

*Note: Cisco UCS S3260 is End of Sale from February 3, 2025.*

**Admin Tab:**

*In the* ***Admin*** *tab, Cisco UCS administrators create, modify, and delete configuration elements that regard general Cisco UCS administration tasks. With so many major categories in the Admin tab, category filtering can help you to display only the elements of interest.*

![Cisco UCS Manager GUI 2](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/UCS_manager_GUI2.png)

## Chassis Discovery in Cisco UCS Manager

*Cisco UCS Manager automatically discovers new servers and their components while following their progress, performance, and operations with a finite state machine (FSM). This implementation ensures minimal maintenance overhead while maintaining good performance overview.*

*Cisco UCS Manager is always in discovery mode. Through a series of presence sensors and voltage indications, Cisco UCS Manager knows when you add or remove components from the chassis.*

*During the following chassis discovery process, Cisco UCS Manager identifies components and, if necessary, verifies them:*

- *The presence sensor discovers a link on a server-facing port.*

- *Basic communication opens to the chassis management controller in the I/O module.*

- *It checks component compatibility.*

- *It determines device support.*

- *It verifies the serial number on the chassis:*

*Has the administrator removed this device from management?*

- *For a new link to an existing chassis, Cisco UCS Manager takes these actions:*

1. *If the chassis is new, it accepts the chassis.*

2. *Performs discovery of components such as model, firmware, fans, power supply units (PSUs), and slots.*

*The figure illustrates a repetitive chassis discovery process in Cisco UCS Manager.*

![UCS Chassis Discovery](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/UCS_chassis_discovery.png)

## Server Discovery in Cisco UCS Manager

*During the discovery of a server in the chassis, Cisco UCS Manager performs these steps:*

1. *If a slot raises a state, then the slot has presence (a server is present).*

2. *Opens communications with the Cisco IMC on the server in that slot.*

3. *The following server information is discovered: vendor, model, serial number, BIOS, Cisco IMC, CPUs, memory, HBAs, NICs, and local storage controller.*

4. *Boots the Cisco UCS Utility Operating System.*

5. *Performs a deep discovery of local disk, vendor-specific HBA, and NIC information.*

*Note: The Cisco UCS Utility Operating System is triggered at device discovery, service profile association, and service profile disassociation. This small utility operating system resides in fabric interconnect flash memory and is Preboot Execution Environment (PXE)-booted when needed by a blade server.*

*This figure shows the server discovery process.*

![UCS Server Discovery](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/UCS_server_discovery.png)

## Verify Device Discovery in Cisco UCS Manager

*Cisco UCS Manager discovers components using an FSM workflow model that relies on a finite number of possible operational states. FSM examines past stages and transitions between stages to audit an operation.*

*The following operations are subject to FSM validation:*

1. *Physical components:*

- *Chassis*

- *I/O module*

- *Servers*

2 *Logical components:*

- *Policies*

3. *Workflow:*

- *Server discovery*

- *Service profile association and disassociation*

- *Firmware downloads*

- *Component upgrades*

- *Back up and import jobs*

*Many components and processes in Cisco UCS have highly complex state transitions. FSMs are assigned to audit the state transitions and to validate correct operation through a series of finite state codes that the operations report.*

## Discovery Process in FSM

*The finite state machine tracks the transition states of I/O module discovery by following a predefined set of states that a module can report. Once the final state is reached, the discovery is successful.*

*Note: The FSM lists the states of the server from a finite list of states that the server can occupy. Here, you can follow actions and determine issues. The advantage of this approach is that you can always determine the history of state changes and follow along the states of initiated procedures.*

*The image shows a successful discovery process of a rack-mounted server that reached 100 percent.*

![UCS Successful Discovery](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/UCS_successful_discovery.png)

*In the image, the rack-mounted server was manually reset. The step sequence clearly indicates the successful steps of resetting the server.*

*The progress indicator provides a graphical representation of how far the FSM-processed tree has proceeded. There could be a long pause at a particular percentage point. This pause is process-specific and usually nothing to worry about. If the FSM stops responding for more than a certain amount of time, a timeout will occur, and the operation fails.*

*Discovery is successful when the FSM reaches 100 percent without errors.*

*FSM state transitions often occur too fast for a human operator to read. Click the* ***Events*** *tab to see a detailed list of all transitions.*

## Lab: Explore the Cisco UCS Server Environment

*Cisco UCS Manager is a powerful management tool for your Cisco UCS servers and networking. Cisco UCS Manager runs on Cisco UCS Fabric Interconnect devices, which provide connectivity to the underlying Cisco UCS servers and management of the entire Cisco UCS domain.*

*Cisco UCS Manager uses a structure of policies separated between organizational units. The policies are defined per organizational unit, and the same policies can be defined for each organizational unit. These policies can then be bundled together into templates and service profiles.*

*Because of the power that this system provides, you need to acquaint yourself well with different options and interfaces that Cisco UCS Manager provides before you can start using it effectively.*

**Big picture first (the thing Cisco never says plainly):**

Cisco UCS is not *“servers + switches”* — it’s ***policy-driven compute.***

You don’t manage machines; you manage *identities, templates, and intent,* and hardware becomes replaceable flesh.

Think of UCS as: *“PXE boot for entire servers — BIOS, NICs, HBAs, MACs, WWNs, firmware — all cloned from memory.”*

### Core UCS building blocks (memorize this triangle):

**1. UCS Manager (UCSM):**

- Runs *inside Fabric Interconnects (FIs)* — not on servers

Single point of truth for:

- Server identity

- Networking

- SAN

- Firmware

Everything is *stateless until associated.*

Mental trick: *UCSM = BIOS + switch + SAN zoning + Puppet, mashed into one GUI.*

**2. Fabric Interconnects (FI-A / FI-B):**

Act as:

- Ethernet switches

- Fibre Channel switches

- Control plane for UCS

Servers never talk “north” directly — ***all traffic funnels through FIs***

Key ideas:

- Always deployed in *pairs*

- Provide *redundancy + policy enforcement*

- Run UCSM themselves

Remember: *FIs are not optional switches — they are the system.*

**3. Servers (Blades or C-Series):**

- Physically dumb

- Logically empty until assigned a ***Service Profile***

What they *don’t* own:

- MAC addresses

- WWNs

- Boot order

- BIOS config

- Firmware version

*Mnemonic:*

Server ≠ identity

***Service Profile = identity***

### Service Profiles (this is the soul of UCS):

A *Service Profile* defines:

- UUID

- MAC addresses

- WWNN / WWPNs

- vNIC / vHBA layout

- Boot-from-SAN

- BIOS settings

- Firmware policy

Once created, you can:

- Bind it to a server

- Unbind it

- Rebind it to new hardware

Result: *A dead server can be resurrected in minutes.*

Think of it as: *A Git commit for a physical server.*

### Templates (where sanity lives):

Instead of cloning Service Profiles manually:

***Service Profile Templates***

- Ensure consistency

- Prevent configuration drift

Updating the template can update children (if bound).

*Rule:* One-off profiles = tech debt. Templates = civilization.

### Networking inside UCS (important mental shift):

**vNICs & vHBAs:**

- Created in UCSM

- Presented to the OS like physical adapters

- Mapped onto uplinks dynamically

Key idea:

- The OS thinks it has NICs

- The network thinks it has hosts

- UCS glues the illusion together

*This is why UCS pairs beautifully with FCoE.*

### Boot-from-SAN (classic UCS magic):

Instead of local disks:

- Server boots from SAN LUN

- Diskless hardware

- Stateless compute

Benefits:

- Faster replacement

- Centralized storage

- Clean lifecycle management

UCS philosophy: *Hardware is disposable. Identity is sacred.*

### What this lab is really teaching you:

Under the surface, the lab drills these truths:

1. **Discovery ≠ configuration**

- Servers appear first

- Identity comes later

2. **Everything flows through policy**

- BIOS

- Firmware

- Networking

- Storage

3. **Redundancy is structural, not optional**

- Dual FIs

- Fabric failover

- Active/standby control plane

4. **UCS is slow to learn, fast to operate**

- Pain upfront

- Bliss during outages

**“State of the world” mental topology:**

```
        Core Network / SAN
               |
        +------+------+
        |             |
     FI-A           FI-B
        |             |
   +----+-------------+----+
   |        UCS Chassis       |
   |  Blade  Blade  Blade    |
   +-------------------------+
```

- UCSM lives in the FIs

- Servers are just endpoints

- Policies define reality

# Identity and Resource Pools for Hardware Abstraction

*In a traditional data center computing environment, the operating system or hypervisor is installed on a compute node. Burned-in values for universally unique identifiers (UUID)s, MAC addresses, World Wide Node Names (WWNNs), and World Wide Port Names (WWPNs) are consumed during the installation process. If the underlying compute node becomes nonfunctional, then the replacement compute node will have different values for UUIDs, MAC addresses, WWNNs, and WWPNs. This difference can lead to time-consuming and expensive downtime for a server. In a virtualized server, this difference can also affect many hosts in virtual machines.*

*In a Cisco UCS stateless computing environment, hardware identifiers (such as the UUID, MAC, WWNN, and WWPN) and firmware versions are abstracted into a service profile. You can move this profile quickly to a replacement compute node.*

*Here you will take a closer look at the features of Cisco UCS Manager that allow rapid provisioning and the consistent application of policy.*

*Identity and resource pools provide a system that allows devices in the network to configure themselves with unique values. A well-known system that has such functionality is DHCP, which provides IP addressing within an IP network. In a data center environment, it is important that the devices have unique protocol numbers. Also, the numbers must be easily transferable between hardware and virtual machines if there is a failure. This approach is achieved by using hardware abstraction.*

## Hardware Abstraction Benefits

*Hardware abstraction is a concept in which the software layer functions independently of the underlying hardware properties. It may mean emulation of hardware, such as with vSwitches, or independent numbering, as with fast server mobility from one compute node to another if there are failures.*

*If a given physical host becomes nonfunctional, moving the operating system or hypervisor requires time-consuming reconfiguration.*

*Cisco UCS offers a new paradigm for data center computing. Because all the identity properties (MAC, UUID, WWNNs, and WWPNs) can be administered locally, you can move a SAN-booted server to a replacement compute node with minimal downtime.*

*A service profile that overrides server identity provides maximum flexibility and control. This profile allows you to override the identity values that are on the server at the time of association. You can use the resource pools and policies set up in Cisco UCS Manager to automate some administration tasks.*

*The figure shows a transfer of values as a single profile, allowing for stateless computing.*

![Hardware Abstraction](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/hardware_abstraction.png)

*The abstraction of hardware identities that allows the movement of a service profile is referred to as stateless computing.*

## Identity and Resource Pools

*Stateless computing requires unique identity resources for the UUID, MAC addresses, WWNNs, and WWPNs for Fibre Channel. Pooled resources ensure the uniqueness of the identities that are assigned to service profiles by leasing pooled numbers.*

*Using pooled resources ensures a consistent application of policy and reasonable assurance that identities are unique within Cisco UCS Manager.*

*Pools have the following benefits:*

- *Pools of identifiers simplify mobile service profiles.*

- *The use of pools promotes a consistent application of policy and ensures the uniqueness of identities within Cisco UCS Manager.*

*The pools in the figure provide unique identifiers to a device. Each individual pool provides its own identifier.*

![Resource Pools](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/resource_pools.png)

*Logical resource pools (identity pools) provide abstracted identities that service profiles consume in service profile templates to facilitate stateless computing.*

## Universally Unique Identifier Pools

*Physical resource pools are used to create blade-server groupings that are based on arbitrary administrative criteria. These pools can be used with service profile templates for rapid provisioning of compute resources. UUIDs provide a means for such grouping while allowing for mobile computing.*

*UUIDs are designed as globally unique identifiers (GUID)s for each compute node on a network. UUIDs are used in many ways, but in the context of Cisco UCS, the UUID refers to a 128-bit identifier that is coded into the compute node BIOS.*

*UUIDs have the following characteristics:*

- *UUIDs are essentially standardized serial numbers that identify a particular server.*

- *Traditional servers have hardware UUIDs that are stored in the system BIOS.*

- *Operating systems and software licensing schemes may use the UUIDs to detect whether they have moved between physical servers.*

- *Cisco UCS allows for the manual or automatic assignment of UUIDs to enhance the mobility of operating systems and applications.*

*The figure shows you the UUID format.*

![UUID Format](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/UUID_format.png)

*Operating systems, hypervisors, and applications can use the UUID for processes such as activation, internal disk labels, and others. Some applications use the UUID as an internal root value that propagates tightly within data structures. For these reasons, you should administer UUIDs locally in the service profile instead of deriving them from the BIOS. UUIDs within a service profile allow for mobile computing. If the underlying compute node fails, then the service profile carries the UUID to the replacement compute node.*

*There are many schemas for deploying and formatting UUIDs. It is the responsibility of Cisco UCS to determine which values to encode in the UUID prefix and suffix.*

*UUIDs have these properties:*

- *UUIDs are 128-bit numbers (represented in hexadecimal) that are expected to be globally unique.*

- *Cisco UCS Manager uses a configurable 64-bit prefix and allows administrators to specify a range of suffixes for use by compute nodes.*

- *Cisco recommends that prefixes be set to the same 24-bit Organizationally Unique Identifier (OUI) as used in WWNN pools and padded as necessary.*

- *A UUID suffix pool ensures that these variable values are unique for each server that is associated with a service profile that uses that particular pool to avoid conflicts.*

## MAC Pools

*A MAC pool is a collection of network identities (or MAC addresses) that are unique in their Layer 2 environment. They are available for assignment to VNICs on a server.*

*In a system that implements multitenancy, you can use the organizational hierarchy to ensure that only specific applications or business services can use MAC pools. Cisco UCS uses the name resolution policy to assign MAC addresses from the pool.*

*The figure shows that a MAC address pool was created to supply MAC addresses for the compute node Ethernet communication.*

![MAC Pool](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/MAC_pool.png)

*You can specify your own MAC addresses or use a group of MAC addresses that Cisco provides.*

*If you use MAC pools in service profiles, you do not have to manually configure the MAC addresses for use by the server that associates with the service profile.*

## WWNN and WWPN Pool

*A World Wide Name (WWN) pool is a collection of WWNs (WWNNs and WWPNs) that are used by the Fibre Channel vHBAs in a Cisco UCS domain as communication addresses. They facilitate Fibre Channel connectivity.*

*A WWN pool can include only WWNNs or WWPNs in the ranges from 20:00:00:00:00:00:00:00 to 20:FF:FF:FF:FF:FF:FF:FF or from 50:00:00:00:00:00:00:00 to 5F:FF:FF:FF:FF:FF:FF:FF. All other WWN ranges are reserved. To ensure the uniqueness of the Cisco UCS WWNNs and WWPNs in the SAN fabric, Cisco recommends using the following WWN prefix for all blocks in a pool: 20:00:00:25:B5:XX:XX:XX.*

*To deploy the WWNN, you need the following:*

- *A unique WWNN that is assigned to each HBA*

- *A unique WWPN for each HBA port*

![WWNN Pool](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/WWNN_pool.png)

## Server Pools

*A server pool contains a set of servers. These servers typically share the same characteristics. Those characteristics can be their location in the chassis or an attribute such as server type, amount of memory, local storage, type of CPU, or local drive configuration.*

*If your system implements multitenancy through organizations, you can designate one or more server pools for use by a specific organization. For example, you could assign a pool that includes all servers with two CPUs to the marketing organization. You could assign all servers with 64 GB of memory to the finance organization.*

**My Note:** Multitenancy networking refers to a system where multiple customers (tenants) share the same network infrastructure while keeping their data and operations isolated from each other. This approach is commonly used in cloud computing and managed services, allowing for efficient resource use and simplified management.

*Note: You can use server pools even without organizations.*

*When assigning servers to pools, you must follow these guidelines:*

- *Server pools can be manually populated or use server pool policies and server pool policy qualifications to automate the assignment.*

- *A blade server can be in multiple pools at the same time.*

- *Associate a service profile with a pool:*

1. *A compute node is selected automatically from the pool.*

2. *Cisco UCS Manager selects only a blade server that is not associated with another logical server and is not in the process of being disassociated.*

*A compute node can be in multiple pools at the same time, as the figure shows. The profile that is associated with a specific compute node owns the node, regardless of the number of pools in which the blade server resides.*

![Server Pool](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/server_pool.png)

*A server pool can include servers from any chassis in the system. A given server can belong to multiple server pools.*

*To use a server pool, associate the service profile with the pool. Cisco UCS Manager automatically selects an available compute node from the pool.*

# Service Profiles and Service Profile Templates

*You can create service profiles from predefined templates that contain predefined common values for certain situations. Templates offer significant benefits when managing or creating new profiles. As an administrator, you will find yourself in certain repetitive situations where it will be practical to use a predefined set of values for a certain application.*

## Service Profile Overview

*A service profile is a software construct that contains the identity and operational policies that make up a compute node.*

***Each compute node in a Cisco UCS B-Series or C-Series integrated server requires a unique service profile.***

![Service Profile](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/service_profile.png)

*The following are the benefits of service profiles:*

- *They are planned and preconfigured once for collaborative server, storage, and network planning and configuration.*

- *Incremental deployment is nondisruptive.*

- *A server replacement is easy. Simply replace the physical blade and reassociate the service profile.*

- *Server upgrades are easy. Move the service profile to a server with more capabilities.*

*The primary benefit of service profiles is server mobility (stateless computing).*

*With a service profile template, you can quickly create several service profiles with the same basic parameters and with identity information that draws from the same pools. Examples include the number of VNICs and vHBAs. The service profile templates allow rapid scaling of the Cisco UCS solution.*

![Service Profile 2](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/service_profile2.png)

## Service Profile Template

*The process of creating a service profile template is nearly identical to creating a service profile manually. The principal differences are that service profile templates cannot be directly applied to a compute node and that no hardware elements can use a derived value.*

*The service profile template has the following characteristics:*

- *It is similar to creating a service profile.*

- *It requires a server pool (you cannot select an individual blade).*

- *It requires pooled identities (UUID, MAC, WWNN, and WWPN).*

- *It can also have policies such as boot, BIOS, and maintenance policies.*

![Service Profile Template](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/service_profile_template.png)

## Service Profile Template Types

*Templates can serve as an initial framework when creating a service profile but can also help you make mass changes to all profiles that are created from a template.*

*Cisco UCS supports the following types of service profile templates:*

- ***Initial template:*** *Service profiles that are created from an initial template inherit all the properties of the template. Service profiles that are created from an initial service profile template are bound to the template. However, changes to the initial template do not automatically propagate to the bound service profiles. If you want to propagate changes to bound service profiles, unbind and rebind the service profile to the initial template.*

- ***Updating template:*** *Service profiles that are created from an updating template inherit all the properties of the template and remain connected to the template. Any changes to the template automatically update the service profiles that are created from the template.*

### Service Profile Template Benefits

*Templates allow consistent policy application to meet application requirements in heterogeneous computing environments.*

*Another benefit of using service profile templates is that the Cisco UCS administrator can automate the provisioning of one to hundreds of compute nodes in simple operations.*

### Create Service Profiles from Templates

*After a service profile template is built and points to identity and resource pools with sufficient resources, automation processes can begin creating service profiles from the templates. Provide the naming prefix and the number of service profiles that you want to extract based on the service profile template.*

# Lab: Configure a Cisco UCS Service Profile

*Cisco UCS Service Profiles are policy bundles that you apply to a server. By applying a service profile to a server, you assign configuration to that server. Configuring an individual server may be simpler than creating all the necessary policies and service profiles; however, when you are running several servers at once, the ability to create standardized configurations for servers becomes more practical.*

*When you are running a specific workload, most often you must configure the servers that run that workload in the same way. Having the ability to simply duplicate an existing server configuration when adding servers to a workload makes scaling much simpler. If the requirements of a workload change, it is also practical to change the configuration for all the servers simultaneously.*

*Cisco UCS Manager allows you to create service profile templates from which you derive your service profiles. When you create a service profile template, you also must define policies and pools (value ranges) for use in that service profile template. When you create a service profile from a template, the policies are automatically associated with that service profile and values are assigned from the associated pools.*

*If you create an updating service profile template, the service profiles created from that template will automatically change when you change the service profile template. This functionality allows you to make changes to entire groups of servers at once.*

*When deploying service profiles, the best practice is to first create the policies, pools, interface templates, and firmware packages that the service profile templates use and then create the service profiles. This sequence allows you more flexibility during configuration, but you can also create some policies and pools during service profile creation.*

## Configure Ports on the Cisco UCS 6400 Series Fabric Interconnect

**Big Picture (remember this first):**

- **Fabric Interconnect (FI)** ports are *role-less* until you assign them.

- **Network ports = northbound uplinks** (to LAN / upstream switches).

- **Server ports = southbound** (to blades / rack servers).

- UCS Manager **will not function correctly** until ports have correct roles.

*Mnemonic:*

***North = Network = Uplink***

***South = Server = Compute***

**Step 1: Log in to UCS Manager**

1. Open browser → go to ```https://10.10.1.130/```

2. Click *Launch Cisco UCS Manager*

3. Log in

4. Bypass the certificate warning

- Chrome: *Advanced → Proceed*

- Firefox: *Advanced → Add Exception → Confirm*

**Step 2: Navigate to the Fabric Interconnect**

***Equipment tab***

→ *Fabric Interconnects*

→ Click *Fabric Interconnect A*

You should now see:

- Navigation Pane (left)

- Physical / graphical representation (right)

This view is gold — you’ll use it constantly.

**Step 3: Configure Port 1 as a Network (Uplink) Port**

GUI path:

***Fabric Interconnect A***

→ expand *Fixed Module*

→ expand *Ethernet Ports*

→ select *Port 1*

Actions:

1. Click *Reconfigure*

2. Select *Configure as Uplink Port*

3. Click *Yes*, then *OK*

Verification:

- Status: *Up*

- Role: *Network*

- Right-click menu → *Configure as Uplink Port* is now **grayed out**

→ this confirms the role is locked in

**Step 4: Configure Port 2 as a Server Port**

GUI path:

***Fabric Interconnect A***

→ *Fixed Module*

→ *Ethernet Ports*

→ select *Port 2*

Actions:

1. Click *Reconfigure*

2. Select *Configure as Server Port*

3. Click *Yes*, then *OK*

Verification:

- Status: *Up*

- Role: *Server*

This port now expects a **UCS server connection**, not a switch.

**Step 5: Visual Status Check (don’t skip this)**

- *Green port = active and happy*

- Click ports directly in the *graphical chassis view* to inspect status

- If a port isn’t green:

1. Click *Disable Port*

2. Then *Enable Port*

Classic UCS move — surprisingly effective.

**What to Burn Into Memory:**

- Port roles are *manual and mandatory*

- Wrong role = silent failure later (service profiles won’t bind)

- UCS forces discipline: *you define intent first, traffic later*

- The physical GUI view is not cosmetic — it’s operational truth

## Verify the Server Discoveries and Create an Organization

**Big picture (remember this first):**

- **Server discovery is automatic in UCS:** the *moment* you mark a Fabric Interconnect port as a **Server Port**, UCS starts probing whatever is connected.

- **Organizations** are logical containers — think *folders with RBAC attached.* Everything meaningful (policies, pools, service profiles) lives inside one.

- UCS visually mirrors reality: **Fabric Interconnects → FEX → Chassis → Servers.** If you can “see” it in the GUI, UCS already knows about it.

**1. Verify server discovery:**

*Why this matters:* If the server shows up here, cabling + port roles are correct. If it doesn’t, stop everything and fix Layer 0 (cables, ports).

*GUI path:*

```
Equipment → Main Topology View
```

*What you should see:*

- Fabric Interconnect A connected to:

1. *Two FEXs*

2. *Two chassis*

- This confirms:

1. Uplink ports are working

2. Server ports are correctly assigned

3. UCS discovery is healthy

**2. Inspect discovered servers:**

**Rack-mounted server (standalone, not in a chassis):**

```
Equipment → Rack-Mounts → Enclosures → Rack Enclosure 1
→ Servers → Server 1
```

- This is an *unassociated Cisco UCS C220 M4S*

- *Unassociated* = no Service Profile yet → no personality → just raw hardware

**Blade server (inside a chassis):**

```
Equipment → Chassis → Chassis 3 → Servers → Server 1
```

- This is a *Cisco UCS B200 M5 blade*

- Blades *cannot exist alone* — they slide into a chassis and rely on it for:

1. Power

2. Cooling

3. Networking (via FEX inside the chassis)

**Quick clarity (Cisco really botched this explanation):**

- **Rack server** = full pizza box server, its own NICs & power

- **Blade server** = half a server, *must* live inside a chassis

- **Chassis** = server hotel (power + cooling + networking aggregation)

**3. Create an Organization (this is foundational):**

*Why we do this now:*

Before policies or service profiles, you need a *home* for them.

*GUI path:*

```
Servers → Service Profiles
→ root (right-click) → Create Organization
```

*What an Organization really is:*

- A *logical container* for:

1. Service Profiles

2. Pools (MAC, UUID, WWPN, etc.)

3. Policies

- Also a *security boundary* (RBAC applies here)

- Best practice: *never* dump production configs in ```root```

**4. Create your org:**

*Action:*

- Name: ```DCFNDU```

- Click *OK* twice

*Verify:*

```
Navigation Pane → Sub-Organizations
```

You should now see:

```
root
└── DCFNDU
```

This confirms UCS accepted and instantiated the org.

**Mental snapshot:**

- *Server Port enabled → discovery happens automatically*

- *Topology View = physical truth*

- *Rack servers = standalone*

- *Blade servers = chassis-dependent*

- *Organizations = policy containers + RBAC boundary*

- Always build *inside an org*, never in root

## Create a MAC Pool and VLAN

**What pools are (why we care):**

- Pools define reusable *ranges* (MACs, WWNs, UUIDs, etc.) for service profiles.

- Each service profile pulls a *unique value* from the pool → no address collisions inside the UCS domain.

- Think of pools as deterministic identity vending machines.

**1. Create a MAC Pool (identity plumbing):**

- Navigate: *LAN tab → Pools → root → Sub-Organizations → DCFNDU*

- Right-click *MAC Pools → Create MAC Pool*

- Name: *MAC_POOL → Next*

- Create *8 MAC addresses*, starting at *00:25:B5:00:80:00*

- Click *OK*, then verify the pool appears in the *Work Pane*

**2. Create a VLAN (network plumbing):**

- Navigate: *LAN → LAN Cloud → Fabric A*

- Right-click *VLANs → Create VLANs*

- VLAN Name/Prefix: *VM_Network*

- VLAN ID: 12

- Scope: *Common/Global* (important — usable by both fabrics)

- Click *OK* twice

**3. Verify VLAN creation:**

- Navigate: *LAN → LAN Cloud → VLANs*

- Confirm *VM_Network (VLAN 12)* is listed and available

**Mental model (worth remembering):**

- *MAC Pool = server identity source*

- *VLAN = traffic segmentation rule*

- Service profiles later *bind these together*, turning stateless hardware into a predictable server personality

## Configure UUID Prefix and Suffix Pools

**What a UUID is (why we care):**

- The UUID uniquely identifies a *server identity* to the operating system.

- If you move an OS or service profile to different hardware, the UUID is how the OS notices “this is a different machine.”

- In UCS, UUIDs are *abstracted* and assigned from pools, not tied to physical metal.

**UUID structure (mental anchor):**

- UUID = *Prefix + Suffix*

- Prefix = usually static and vendor/environment specific

- Suffix = incrementing values taken from a pool (one per service profile)

**1. Create the UUID Suffix Pool:**

- Go to *Servers tab*

- Expand *Pools > root > Sub-Organizations > DCFNDU*

- Right-click *UUID Suffix Pools → Create UUID Suffix Pool*

- Name the pool: *UUID_POOL*

- In the *Prefix* section, select the *manual* radio button

- Enter prefix: *00000000-0000-0080*

- Click *Next*

**2. Populate the suffix values:**

- Click *+Add*

- In the *From* field, enter the starting suffix for your pod (example: *8000-000000000001*)

- Create *8 total UUID suffix entries* (one per future service profile)

- Click *Finish*, then *OK*

**Why this matters later:**

- Every service profile will now get a *stable, predictable UUID*

- OS licensing, clustering, and VM identity all depend on this behaving consistently

- This is one of the *core illusions* of UCS: hardware becomes replaceable, identity does not

## Configure Boot Policy

**What a boot policy is (why it matters):**

- A boot policy defines *which devices the server checks for an OS, and in what order.*

- UCS abstracts this away from physical hardware, so *any server using this service profile will boot identically*, no matter which blade or rack unit it lands on.

- You can temporarily override this order with *F6 during POST*, but the policy always wins on the next reboot.

**1. GUI navigation:**

- Go to *Servers tab*

- Expand: ```Policies > root > Sub-Organizations > DCFNDU```

- Right-click *Boot Policies → Create Boot Policy*

**2. Boot policy configuration:**

- Name: *BOOT_POLICY*

- *Boot Order:*

1. *CD/DVD* (first priority — typical for installs, recovery, or ISO-based provisioning)

2. *Local Disk* (second priority — normal production boot path)

**Why this order is common (extra wisdom):**

- CD/DVD first allows *hands-off OS installation+ (ISO via virtual media, KVM, or automation).*

- Local Disk second ensures *normal boot once the OS is installed*, without touching the policy again.

- In larger environments, this same idea extends to *SAN boot, iSCSI boot, or PXE*, just by swapping devices — zero hardware reconfiguration.

## Create an Updating Service Profile Template

**Concept snapshot (worth remembering):**

- *Updating Service Profile Template* = a living blueprint.

- Any service profile created from it *inherits changes automatically* (until you unbind it).

- This is how UCS achieves *stateless servers:* identity, boot, networking, and management are abstracted away from hardware.

**1. Create the Updating Template:**

- Navigate to:

```
Servers > Service Profile Templates > root > Sub-Organizations
```

- Right-click *DCFNDU → Create Service Profile Template*

- In *Identify Service Profile Template:*

1. Template Type: *Updating Template*

2. Name: *SPT*

3. UUID Pool: *UUID_POOL*

- Click *Next*

You’re explicitly saying: *this server boots locally, no SAN trickery.*

**2. Networking (vNIC creation):**

- In *Networking:*

1. Select *Expert*

2. Click *+ Add* to create a vNIC

- Configure *Fabric A* vNIC:

1. Name: *vNIC0*

2. MAC Pool: *MAC_POOL*

3. Allowed VLANs: *1, 12*

- Click *Next*

***Why VLAN 1 and 12?***

- *VLAN 12* = ```VM_Network``` you created earlier (this is intentional continuity).

- *VLAN 1* is often kept for default/native traffic or legacy expectations.

**3. SAN Connectivity:**

- In *SAN Connectivity:*

1. Select *No vHBAs*

- Click *Next*

You’re skipping Fibre Channel entirely because this server uses *local disks only.*

**4. Zoning:**

- Leave defaults

- Click *Next*

**5. vNIC / vHBA Placement:**

- Leave defaults (system auto-placement)

- Click *Next*

UCS is smart enough to map logical NICs to physical hardware — trust it here.

**5. vMedia Policy:**

- Leave defaults

- Click *Next*

**6. Server Boot Order:**

- Select Boot Policy: *BOOT_POLICY*

- Click *Next*

This ties directly to your earlier work: CD/DVD → Local Disk.

**7. Maintenance Policy:**

- Select *Default Maintenance Policy*

- Click *Next*

Default = safe rolling updates, minimal surprise reboots.

**8. Server Assignment:**

- Leave defaults (manual or later assignment)

- Click *Next*

**9. Operational Policies – Management IP Pool:**

- Expand *Management IP Address (+)*

- Select *Outband IPv4*

- Click *Create IP Pool*

**10. IP Pool Wizard:**

- Name: *MGMT_POOL*

- Add IPv4 Block:

1. Start IP: ```10.10.1.151/24```

2. Count: *5*

3. Gateway: ```10.10.1.254```

4. DNS: ```192.168.10.40```

- Leave IPv6 defaults

- Click *Finish*, then *OK*

*Critical insight:*

- These IPs go to the *IMC (server BMC)*, not the OS.

- OOB management = dedicated path, higher reliability, less blast radius.

- Must be in the ***same subnet as the Fabric Interconnect management IPs.***

**11. Finalize Template:**

- Select *MGMT_POOL* from Management IP Policy drop-down

- Click *Finish* → *OK*

**12. Verify:**

- Navigate to:

```
Servers > Service Profile Templates > root > Sub-Organizations > DCFNDU
```

- Confirm *SPT* exists

**Mental anchor (remember this):**

- *Service Profile Template = identity + behavior + wiring diagram*

## Create a Service Profile from the Updating Template and Assign a Server to the New Profile

**Concept refresher (why this step exists):**

- *Service Profile Templates ≠ Servers*

You cannot assign a template directly to hardware.

- *Service Profiles* are the *instantiated identities:*

1. They pull *MACs, UUIDs, IPs* from pools *at creation time*

2. Those values stay *reserved* until the service profile is deleted

- Because this is an *Updating Template*, profiles stay *linked* and inherit future template changes unless explicitly unbound.

**1. Create Service Profiles from Template:**

- Navigate to:

```
Servers > Service Profile Templates > root > Sub-Organizations > DCFNDU
```

- Right-click *Service Template ```SPT```*

- Choose *Create Service Profiles From Template*

- Create *2 service profiles*

1. Prefix: ```SP```

2. Starting suffix: ```1```

→ This results in ```SP1```, ```SP2```

- To view:

```
Servers > Service Profiles > root > Sub-Organizations > DCFNDU > SP1
```

*Expected warning:*

You’ll see a warning because ```SP1``` is bound to an *updating template.* This is *normal* — direct edits are blocked unless you unbind.

**2. Associate the Service Profile to Physical Hardware:**

- Go to:

```
Equipment > Chassis > Chassis 3 > Servers > Server 1
```

- Right-click *Server 1*

- Choose *Associate Service Profile*

- Select *Service Profile ```SP1```*

- Click *OK → Yes → OK* to confirm

Result:

- Server *reboots*

- Hardware identity is rewritten (MAC, UUID, boot order, NICs, etc.)

*Big idea:* you didn’t “configure the server” — you *attached an identity* to it. That’s UCS’s whole philosophy.

**3. Monitor the Association Process (this part matters):**

- Open *SP1*

Watch progress under:

- *General > Status Details*

- or *FSM tab* (Finite State Machine)

- FSM may be hidden → click the *right-arrow* at the top to scroll tabs

- Expected completion time: up to 15 minutes

If it *fails or stalls:*

- Something earlier is wrong — UCS is *brutally strict*

Common causes:

- Missing pool entries

- VLAN mismatch

- Boot policy misconfig

- Management IP pool errors

**Final Outcome (why this is the finish line):**

Once status = *OK:*

- Server is fully initialized

- Identity is consistent and repeatable

- The system is now *ready for OS installation*

From ESXi’s point of view, this looks like a *brand-new physical server.* From your point of view, this is *infrastructure as code, but physical.*

# Cisco Intersight Overview

*Cisco Intersight is a cloud operations platform that consists of optional modular capabilities of advanced infrastructure, firmware updates, and workload optimization services. This software as a service (SaaS) management platform is augmented by other intelligent systems.*

*Cisco Intersight services include the deployment, monitoring, management, and support of your physical and virtual infrastructure. You can connect to Intersight from anywhere and manage the infrastructure through a browser or mobile application. Cisco Intersight Secure Connector provides lifecycle management of Cisco Unified Computing System (Cisco UCS) servers, Cisco Hyperconverged with Nutanix, and third-party devices.*

## Cisco Intersight Overview

*Cisco Intersight is a modular platform of integrated SaaS offerings that address your unique requirements and use cases.*

![Intersight Overview](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/intersight_overview.png)

*According to your use case, choose one of the following Cisco Intersight services:*

- ***Cisco Intersight Infrastructure Service:*** *Apply intelligent lifecycle management for Cisco data center products such as Cisco UCS, Cisco Hyperconverged with Nutanix, Cisco converged infrastructure solutions, and third-party endpoints that are powered by proactive support and enterprise-class security. Automate server, fabric, and storage provisioning as well as device discovery, inventory, configuration, diagnostics, monitoring, fault detection, auditing, and statistics collection. Apply unified policies and integrate with third-party system management tools.*

- ***Cisco Intersight Virtualization Service:*** *Streamline the operation and management of virtual machines through a common inventory and extensible workflow framework spanning the private and public clouds.*

- ***Cisco Intersight Cloud Orchestrator:*** *Automate infrastructure and workload delivery across on-premises equipment and public clouds with an easy-to-use, low-code workflow designer. Create and execute complex workflows and benefit from a curated library of tasks to standardize orchestration across domains.*

- ***Cisco Intersight Workload Optimizer:*** *Revolutionize how you manage application resources across any environment with real-time, full-stack visibility to help ensure performance and better cost control with a single tool. Monitor physical servers, hypervisors, Kubernetes clusters, and serverless and application components anywhere they are, recognizing all the connections to stay ahead of issues and avoid lengthy troubleshooting when problems arise. Integrate with Cisco AppDynamics software to combine real-time awareness of business outcomes and user experience with infrastructure automation.*

*The Cisco Intersight architecture is extensible and accessible to automation with an open, RESTful application programming interface (API). It allows you to integrate with Ansible, Chef, Puppet, and other DevOps and IT operations management (ITOM) tools using the Python and PowerShell software development kits (SDKs). ServiceNow integration provides inventory and alerts to your IT service management (ITSM) platform to show Cisco Intersight inventory and configuration details, elevating the ITSM experience.*

*In addition, Cisco Intersight Secure Connect provides a framework to scale and extend the universe of Cisco Intersight cloud-managed devices. It offers enterprise-class, secure connectivity to Cisco UCS, Cisco converged infrastructure, and an expanding set of third-party hardware and software platforms.*

## Cisco Intersight SaaS

*You can deploy Cisco Intersight infrastructure services and all Cisco Intersight cloud operations services in a traditional off-premises SaaS mode.*

![Intersight SaaS](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/intersight_saas.png)

*Cisco Intersight was conceived and designed as a SaaS service from the ground up. The location of its data lake and core services enables a broad degree of agility, flexibility, and security. Services include role-based access control (RBAC), policy management, license management, monitoring, analytics, and others in the cloud. This functionality makes SaaS the preferred model for most Cisco Intersight customers.*

*Cisco Intersight SaaS customers are relieved of most management burdens that accompany traditional on-premises software deployments. Examples include infrastructure allocation and support, software monitoring and backup, upgrade and change management, and security hardening. SaaS customers receive new features, bug fixes, and security updates immediately as they emerge from the agile continuous integration and continuous deployment (CI/CD) development pipeline. Essentially, unless an organization has specific reasons why it cannot utilize Cisco Intersight via SaaS, SaaS is the recommended model.*

*Most users enjoy the benefits of full SaaS management. The full lifecycle management of distributed infrastructure and workloads spans data centers, remote sites, branch offices, edge environments, and public cloud platforms. Users can observe, analyze, optimize, update, maintain, and automate their environments through a unified platform in ways that were previously impossible. As a result, an organization can achieve significant total cost of ownership (TCO) savings, delivering hybrid IT infrastructure, resources, and applications faster in support of new business initiatives.*

*Benefits of Cisco Intersight SaaS deployment include the following:*

- *Reduces complexity and manual effort to deploy, maintain, and upgrade Cisco Intersight–connected devices.*

- *Delivers proactive support and Return Materials Authorizations (RMAs) through tight integration with Cisco TAC.*

- *Shifts the burden of building, maintaining, and securing your management environment to Cisco.*

- *Learns and evolves to deliver greater capabilities and improved insights to help you proactively manage your environment.*

- *It is fully programmable, and you can integrate it with third-party systems and tools.*

- *You can add workload optimization and Kubernetes services seamlessly.*

**My note:** Kubernetes is an open-source system for automating the deployment, scaling, and management of containerized applications. It is maintained by the Cloud Native Computing Foundation and is widely used for managing workloads in cloud environments and data centers.

## Cisco Intersight Virtual Appliance

*In addition to the SaaS deployment model running on Intersight.com, you can purchase on-premises options separately.*

![Intersight Virtual Appliance](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/intersight_virtual_appliance.png)

*The always-connected cloud management model has many advantages, but internet connectivity and information sharing with Cisco are required for the SaaS Intersight deployment.*

*Some customers have additional data locality and security requirements for managing systems, whether on the edge or in more traditional data centers, that SaaS-delivered management cannot fulfill. These customers have significant regulatory and compliance needs that require certain details about systems under their management to remain within the borders of countries or on their premises.*

*For these customers, additional control over the data collection is necessary. The Cisco Intersight Virtual Appliance can provide this benefit while maintaining access to the SaaS capabilities of Cisco Intersight. The Cisco Intersight Virtual Appliance enables additional control to specify what data transmits to Cisco with a single point of egress from your network.*

*The Cisco Intersight Connected Virtual Appliance is an on-premises virtual machine. It still needs a connection to the internet, whereas the Cisco Intersight Private Virtual Appliance removes the need for internet connectivity.*

*You can download the components of on-premises Cisco Intersight from the Cisco Software Central website and deploy them as vSphere open virtual appliances.*

*You can deploy Cisco Intersight Virtual Appliance in one of the following modes:*

- *Cisco Intersight Connected Virtual Appliance*

- *Cisco Intersight Private Virtual Appliance*

## Cisco Intersight Connected Virtual Appliance

*Cisco used the microservices that provide the capabilities of the SaaS version of Cisco Intersight. They are now optimized to run in an easy-to-deploy VMware Open Virtual Appliance (OVA) hosted on your infrastructure. Cisco Intersight Virtual Appliance uses the same device connector technology that is embedded in the Cisco UCS and Cisco Hyperconverged with Nutanix systems. It facilitates a connection between that virtual appliance and services running in the Cisco cloud.*

*All Cisco UCS and Cisco Hyperconverged with Nutanix systems can now connect directly to the virtual appliance. You can control what data about those systems transmits to Cisco, based on the settings you specify. This function helps address both government regulations and organization-specific data-sharing preferences.*

![Intersight Connected Virtual Appliance](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/intersight_connected_virtual_appliance.png)

*The Cisco Intersight Connected Virtual Appliance requires a connection back to Cisco and Cisco Intersight services for updates and to deliver some product features. Updates to the virtual appliance are automated and applied during a user-specified recurring maintenance window. This connection also facilitates the streamlining of Cisco Technical Assistance Center (Cisco TAC) services for Cisco UCS and Cisco Hyperconverged with Nutanix systems, via features like automated support log collection.*

*Cisco Intersight Connected Virtual Appliance provides the following benefits:*

- *Same look and feel, API, and basic features as the SaaS solution, including Cisco single sign-on (SSO) and automatic upgrades.*

- *Meets customers’ data locality or security requirements that are not met by the SaaS solution.*

- *Still requires connectivity to the internet.*

## Cisco Intersight Private Appliance

*The Cisco Intersight Private Virtual Appliance is provided in a form factor for users who operate in disconnected (air-gap) environments. The Private Virtual Appliance requires no connection to public networks or back to Cisco to operate.*

![Intersight Private Appliance](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/intersight_private_appliance.png)

*Cisco Intersight offers the Private Virtual Appliance model for organizations with strict requirements for an air-gapped approach. The Private Virtual Appliance is a wholly self-contained, offline instantiation of Cisco Intersight in a single virtual machine that does not communicate with Cisco Intersight.com. Administrators separately download the appliance and the required licensing from Cisco Software Central or Cisco Intersight.com and deploy it manually in the disconnected facility.*

*Cisco Intersight Private Virtual Appliance provides the following benefits:*

- *Does not require internet connectivity.*

- *Appropriate for air-gapped deployments.*

- *No connected features.*

## Cisco UCS Server Profiles

*You use server profiles to configure Cisco UCS servers. You can assign a server profile only to a single Cisco UCS server.*

*There are two types of server profiles:*

- ***Standalone:*** *A rack-mount server not connected to a fabric interconnect*

- ***Fabric interconnect-attached:*** *A rack-mount or a blade server that connects to a fabric interconnect*

![UCS Server Profiles](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/UCS_server_profiles.png)

*The Cisco UCS server administrator creates a server profile. This server profile uses configuration policies that the server, network, and storage administrators create. Server administrators can also create a server profile template for later use to create server profiles more easily. A server template can be derived from a server profile, with abstracted server and I/O interface identity information. Instead of specifying exact values for the UUID, MAC address, and WWN, a server template specifies where to get these values. For example, a server profile template might specify the standard network connectivity for a web server and the pool from which to obtain its interface MAC addresses. You can use server profile templates to provision many servers with the same simplicity as creating one.*

*Server profile templates enable the user to define a template from which multiple server profiles can be derived and deployed. Any property modification that you make in the template synchronizes with all the derived profiles. You can deploy these modified profiles individually. This feature eases and accelerates the configuration, because you can create and edit multiple profiles simultaneously.*

![UCS Server Profiles 2](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/UCS_server_profiles2.png)

## Cisco UCS Pools and Server Policies

*Pools are basic building blocks for uniquely identifying hardware resources. In Cisco Intersight, pools are used for consumable resources or identifiers such as management addresses, WWNs, and MAC addresses that are unique for each server. Pools are preconfigured ranges of these addresses that are consumed when attached to a server profile.*

![UCS Pools and Server Policies](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/UCS_pools.png)

*As the basis for the Cisco UCS management model, pools allow you to associate service profiles with any blade server. They still provide the same ID and presentation to the upstream LAN or SAN.*

*Three basic sets of pools are used in Cisco Intersight:*

- ***IP pools:*** *Flexibility to assign IP addresses dynamically for services that are running on a network element*

- ***MAC address pools:*** *Unique IDs for network interface ports*

- ***Node WWN (nWWN) and port WWN (pWWN) pools:*** *Unique IDs for Fibre Channel resources on a server (Fibre Channel nodes and ports)*

*You use pools for policies that are specific to the Cisco UCS server (fabric interconnect–attached) as a target platform.*

*Internet Small Computer Systems Interface (iSCSI) Qualified Name (IQN) provides a unique logical name that is not linked to an IP address. You must create an IQN pool to configure an iSCSI boot policy and use Auto as the option for the target interface.*

## Server Profile Templates

*In Cisco Intersight, you use a server profile template to create multiple server profiles.*

*Server profile templates enable you to define a template from which multiple server profiles can be derived and deployed. Any property modification that you make in the template synchronizes with all the derived profiles. You can deploy these modified profiles individually. This feature eases and accelerates the configuration, because you can create and edit multiple profiles simultaneously.*

![Server Profile Templates](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/server_profile_templates.png)

*You can perform the following template actions:*

- ***Derive profiles:*** *You can derive multiple profiles from a single template. You can use the Derive Profiles option while creating a template or the Derive Profiles option that is present on the template list view. You can derive a maximum of 100 profiles from a template.*

- ***Clone:*** *You can clone the server profile template into many copies. Cloning allows you to reuse the same configuration for multiple templates. Each copy can have a distinct description, name, prefix, and suffix.*

- ***Delete:*** *You can delete a server profile template only if its corresponding usage value (the number of derived profiles) is 0.*

- ***Edit:*** *You can edit the template at any time. Any edit you make in the template is reflected in the derived server profiles. If the changes are valid, the status of all the derived profiles changes to Not Deployed Changes after the template update.*

## Server Profile Template Creation

*In the server profile template, you will configure the following:*

- ***On the General page:***

1. *Name of the server profile template.*

2. *Target platform for which the profile template is applicable. You can use standalone servers or fabric interconnect–attached servers.*

3. *Tag for the profile template. Tags must be in the key:value format. For example, Org:IT or Site:APJ.*

4. *Organization for the profile template.*

5. *Profile template description.*

- ***On the Compute Configuration page:*** *UUID pool, Server Policies: BIOS, boot order, and virtual media.*

- ***On the Management Configuration page:*** *Here, select the existing policies or create new policies from Device connector, IPMI over LAN, Lightweight Directory Access Protocol (LDAP), local user, network connectivity, Simple Mail Transfer Protocol (SMTP), SNMP, Secure Shell (SSH), serial over LAN, syslog, Network Time Protocol (NTP), certificate management, and virtual KVM policies.*

- ***On the Storage Configuration page:*** *Select the existing policies or create new policies from the Secure Digital (SD) card and storage policies.*

- ***On the Network Configuration page:*** *Select the existing policies or create new policies from LAN connectivity policies and SAN connectivity policies.*

![Server Profile Template Creation](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/server_profile_template_creation.png)

*Now you should have a good foundation of the following:*

- ***Cisco UCS Manager:*** *The Cisco UCS Manager plays a central role in managing and monitoring Cisco UCS servers.*

- ***Unified interface:*** *The manager provides a unified interface that is designed for large-scale deployments, facilitating monitoring, logging, and GUI-based management.*

- ***Operation on Fabric Interconnect:*** *The software operates on Cisco Fabric Interconnect devices, serving as a foundation for its functionalities.*

- ***Accessibility via IP addresses:*** *After configuring the Cisco UCS Fabric interconnect domain, the Cisco UCS Manager becomes accessible through the IP addresses of the interconnected devices.*

- ***Cisco Intersight:*** *Cisco Intersight is a cloud operations platform for deployment, monitoring, management, and support of your physical and virtual infrastructure: Cisco Unified Computing System (Cisco UCS) servers, Cisco Hyperconverged with Nutanix, and third-party devices.*
