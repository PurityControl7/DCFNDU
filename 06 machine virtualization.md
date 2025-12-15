# Describing Machine Virtualization

*Virtualization technology transforms hardware into software. Virtualization allows you to run multiple operating systems as virtual machines on a single computer, and each copy of the operating system is installed in a virtual machine. In server virtualization, you install a layer of software between the server hardware and the operating system.*

*In this course, you will learn about the concepts of virtualization and the differences between virtual machines and virtual servers. You will also become familiar with the VMware product portfolio and how these products interact.*

## Virtual Machines

*A virtual machine emulates a computer system. As such, it is a virtual environment that mimics the hardware elements of a computing system inside a physical computing system. When an operating system runs in this kind of environment, it interacts with the emulated hardware.*

### Need for Virtualization

*Servers are often underutilized in nonvirtualized environments because each application or service is assigned to only one physical server to create one failure domain for each application. Assigning an individual server to only one application reduces the impact of failures. It also allows for a more granular administration, but unused resources that are available on each server cannot be redistributed.*

*Underutilization directly impacts both operational and capital expenditures by increasing the number of servers that are necessary. Every extra server requires additional physical space, power, and cooling systems. As the number of servers grows, management challenges also increase.*

*The figure shows how to better manage resources by consolidating three physical systems that run different operating systems on a single physical device that is split into three virtual machines.*

![Server Virtualization Benefits](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/server_virtualization_benefits.png)

*Depending on the average load of existing deployments, you can often put three or more operating systems onto a single piece of hardware. If the data center environment is designed with virtualization in mind, the ratio of virtual servers to physical servers can be much higher.*

*Virtualization also provides you with more flexibility because deployment of a new virtual server is easier and faster than deployment of a physical server. Also, virtual machines can be mobile. You can move them from one hardware platform to another for maintenance, resource balancing, or failure recovery.*

*A key element in the virtualization of computing systems is the hypervisor. A hypervisor is a system that abstracts (isolates) operating systems and applications from the underlying computer hardware. This abstraction allows the underlying host machine (hardware) to independently operate one or more virtual machines as guests.*

*The virtualization layer or hypervisor offers you several benefits, including the following:*

- *It provides a uniform virtualized hardware interface to the operating system, which is installed above the virtualization layer. Even if three vendors provide three different physical servers in the data center, the servers appear the same to the operating system. The operating system views each type of resource, such as network cards, in the same way, although differences in performance are recognized.*

- *It separates the physical hardware into multiple resource units that all draw from the same physical pool. You can have multiple instances of a single operating system, or even different types of operating systems, running simultaneously on a single server. Unless a nonredundant hardware component fails, these instances are independent of each other, as if they were running on separate physical servers.*

- *The virtualization layer can provide additional management options for interacting with the systems running on a virtual machine, making administration much easier.*

### Virtual Machine Components

*A virtual machine is an entity that is hosted on a virtualization server and is easy to create, remove, migrate, and fail over. A virtual machine is a logical container that holds all the resources that an operating system requires for normal operation. Examples include a graphics adapter, memory, processor, networking, and others. The operating system running in a virtual machine sees no difference between these components and the components that would be available in a physical server.*

*The following figure shows the components and capabilities of a vSphere 7.0.1 as an example, which has a virtual machine format version 18.*

![vSphere](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/virtual_machines.png)

*Like a physical PC or server, the virtual machine also has hardware specifications. The difference is that in the virtual machine environment, some hardware specifications vary according to the physical resources that are available, such as memory and CPU capacity. Other hardware specifications do not vary, such as network interface cards (NICs) and disk controllers.*

*These four primary resources are necessary for a virtual machine to function correctly:*

- *CPU and memory*

- *Virtual disk*

- *Virtual NICs*

- *Other controller devices*

### CPU and Memory

*CPU and memory are typically the two resources that strongly affect virtual machine performance. They are also the two resource types that depend most on server physical resources:*

- ***CPU:*** *The virtualization layer carries out the CPU instructions to ensure that the virtual machines run as though they are accessing the physical processor on the VMware vSphere ESXi host:*

- *A virtual CPU (vCPU) is assigned to a virtual machine. You can allocate more vCPUs, though it depends on the logical cores that are present in the ESXi host and the license that you purchased.*

- *It is possible to oversubscribe these resources, but Cisco avoids recommending such configuration, because it can have an adverse effect on all the virtual machines on the host.*

- ***Memory:*** *Virtual memory, or virtual RAM (vRAM), creates many virtual address spaces and allows the ESXi host to allocate the virtual address space to any licensed virtual machine:*

- *Each virtual machine has its own virtual memory, which allows the ESXi host to run more virtual machines simultaneously.*

- *Virtual memory for each virtual machine is protected from other virtual machines.*

*The figure shows the relationship of physical CPU and memory to the operating system within a virtual machine (VM in figures).*

![VM CPU and Memory](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vm_cpu_and_memory.png)

*The physical resources of the hardware are assigned to the virtual resources of a virtual machine. The operating system detects the resources that are assigned to the virtual machine as though they are physical resources.*

*The operating system is often unaware that it is running in a virtual machine and is relying on the assigned resources. Therefore, it is unwise to oversubscribe the resources by assigning more resources to virtual machines than the physical hardware that is available.*

*CPU and memory are typically the two resources that are most dependent on server physical resources.*

### Virtual Disk

*When creating a virtual machine, you must select a datastore to locate the virtual machine. A datastore is a logical container on an ESXi level that provides storage space for files. For each virtual machine, a specific amount of space from a datastore is available that contains all the files of the virtual machine.*

*The figure shows an ESXi host with a datastore that contains virtual machines in virtual machine disk (.vmdk) file format.*

![VM Datastore](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vm_datastore.png)

*Each time that you create a new virtual machine, you must assign resources to it. The table shows one set of parameters and their sample values.*

![VM Parameters](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vm_parameters.png)

*If the virtual machine uses nonpersistent disks, it reverts to its original disk state when you power it off.*

*Virtual machine disks are made up of two files:*

- ***Disk descriptor file:*** *VM_name.vmdk*

- ***Disk data file:*** *VM_name-flat.vmdk*

*You can easily copy or move virtual disks on the same host or between hosts. Most of the configuration will be retained after the move.*

### Virtual Network Interface Cards

*A virtual network interface card (vNIC) is an interface on the virtual machine. It allows the virtual machine to connect and participate in the virtual network within the ESXi host and communication with physical network outside the ESXi. Determining the type to use typically depends on the type of guest operating system and installed applications.*

*The figure shows the relationship of a vNIC and a physical NIC.*

![VM NIC](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vm_nic.png)

*When creating a new virtual machine vNIC adapter, you can choose from several supported options. Your choice depends on the operating system (OS) that you will install on the virtual machine. For example, some older or legacy OS systems can use only the* ***vlance*** *vNIC, which is an emulated version of the AMD NIC that offered 10 Mbps speeds.*

*Selecting a wrong adapter type can result in low networking performance or the inability of the guest operating system to properly detect the virtualized hardware.*

*Some network adapters that you can choose for your virtual machine include the following:*

- ***vlance:*** *This adapter is also called PCNet32, and most 32-bit guest operating systems support it.*

- ***vmxnet:*** *This adapter provides significantly better performance than vlance.*

- ***Flexible:*** *This adapter can function as either a vlance or vmxnet adapter.*

- ***e1000:*** *This high-performance adapter is available only for some guest operating systems.*

- ***vmxnet2 (enhanced):*** *This adapter is a VMware vmxnet adapter with enhanced performance.*

- ***vmxnet3:*** *This adapter builds on the enhanced vmxnet adapter.*

*You can still choose from many networking adapters to support older or legacy systems. For this reason, it is important to select the* ***vmxnet3*** *adapter whenever possible to gain the best performance and newest features such as multiqueue support, jumbo frames, and IPv6 offloads.*

*Typically, you would see only one vNIC per virtual machine. However, you can add more vNICs (up to 10) if you want to connect a virtual machine to multiple vSwitches.*

*Note: You can use only one VLAN or port group on each vNIC.*

### Other Devices

*Various controllers, including Integrated Drive Electronics (IDE), floppy, and Small Computer Systems Interface (SCSI), let the virtual machine mount one or more types of disks and drives. These controllers do not require any physical counterparts. Instead of physical media, you can mount software images, CD-ROMs, or floppy drives.*

*The figure shows how the physical resources connect to the virtual machine through the hypervisor virtualization function.*

![VM Other Devices](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vm_other_devices.png)

*A newer version of the vSphere environment and virtual machine hardware version introduced new features, such as the following:*

- *Paravirtualized Remote Direct Memory Access (RDMA)*

- *High-performance virtual Non-Volatile Memory Express (NVMe)*

- *Virtual graphics processing unit (vGPU)*

- *USB 3.0 support*

- *Virtual Trusted Platform Module (TPM)*

- *Virtual nonvolatile DIMM (NVDIMM)*

### Shared Storage

*In the shared storage concept, several machines share the same storage hardware over the network. The term shared storage is interchangeable with network-attached storage (NAS). The name refers to the fact that several remote devices can access the same block device, which is not the case with direct-attached storage (DAS) and SAN storage.*

*NAS is an IP file-based storage option. The term NAS usually refers to the Common Internet File System (CIFS) and Network File System (NFS) storage protocols. There are several differences between them.*

*The figure shows a typical infrastructure with services and clients that have access to the NAS on the network.*

![VM Machine Storage](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vm_machine_storage.png)

*The operating system that shares a NAS storage has a complete overview of the files that are being shared.*

*The files on a NAS are readable locally from the operating system, which is why it is possible to create snapshots of the files (or file-based backups).*

*Ideally, the data on NAS storage is running on hardware storage in Redundant Array of Independent Disks (RAID). This location allows fast data backups and better reading speeds, depending on the RAID level.*

*NAS has significant advantages over other storage options such as local storage and SAN, including the following:*

- *Use of IP connectivity*

- *Low cost of management*

- *High availability*

- *Support for increasing storage growth*

- *Minimal impact of backup windows on the data center operation*

- *Support for disaster recovery solutions*

*NAS also supports storage encryption that does not require the guest to request the file to decrypt the traffic. It can also be used as the central backup storage for several servers.*

*You can use traditional NAS to share storage or file shares that NAS appliances export. NAS with a Fibre Channel SAN backend is very popular for big data solutions.*

*Recent data center implementations have used NAS storage with a SAN backend. This approach enables the NAS host to use the SAN benefits, while allowing NAS clients to share the same physical storage over NAS.*

## Hypervisor

*The hypervisor is a thin operating system between the hardware and a virtual machine that runs the virtual machines and allows you to manage them (create, destroy, and other actions). It also provisions the hardware resources (such as CPU process timesharing, memory span from physical memory, network, and storage) to make them available as virtual resources to the virtual machines.*

### Resource Abstraction

*The figure shows how the hypervisor abstracts virtual resources from virtual machines and translates them into virtual hardware resources.*

![Hypervisor Abstraction Layer](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/hypervisor_abstraction_layer.png)

*A hypervisor is like a translator that translates messages between the virtual machine and the physical hardware. Similar to the communication through a translator, some overhead occurs when you are using virtualization.*

*The hardware, hypervisor, and guest operating system can communicate in various ways.*

*A hypervisor allows one host computer to support multiple guest virtual machines by virtually sharing its resources, like memory and processing. The two main types of hypervisors are the following:*

- *Type 1 hypervisors, called “bare metal,” run directly on the host hardware.*

- *Type 2 hypervisors, called “hosted,” run as a software layer on an operating system, like other computer programs.*

### Type 2 Hypervisor

*The figure shows a VMware Workstation as an example of host operating system-based virtualization (Type 2). This type of virtualization is typically used for application development and testing.*

![Type 2 Hypervisor](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/type2_hypervisor.png)

*In operating system-based virtualization, the virtualization software runs as a normal program in an operating system environment.*

*The requirements and benefits of operating system-based virtualization are as follows:*

- *It requires a PC or server that has an installed operating system, such as a Windows or Linux server.*

- *In addition to the operating system, a virtualization application is installed, and the virtual machines are then deployed within that application.*

- *The benefit is that you can use a single PC for everyday requirements in addition to your virtualization needs.*

- *The downside is that the host operating system uses up some resources that could be assigned to the virtual machines.*

*Note: The VMware Workstation virtualization software replaced VMware server (now discontinued).*

### Type 1 Hypervisor

*The figure shows the VMware ESXi Hypervisor as an example of Type 1 virtualization.*

![Type 1 Hypervisor](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/type1_hypervisor.png)

*A bare-metal hypervisor-based system requires no operating system on which the virtual machine hypervisor runs as a program. The hypervisor itself is the operating system.*

*The requirements and benefits of the bare-metal hypervisor-based virtualization are as follows:*

- *Virtual machines are installed in the virtualization software.*

- *Resources that are available to the virtual machines are maximized, and potential bugs and security vulnerabilities of the host operating system are avoided.*

- *This approach is often used for server deployments where a server is dedicated as a host and all its resources are dedicated for virtual machine deployments.*

*The bare-metal hypervisor-based virtualization is usually employed on large-scale deployments and situations that require maximum performance.*

*In all virtualization configurations, the hypervisor enables the virtual environment.*

*A hypervisor performs the following tasks:*

- *Provides resources to individual operating systems or virtual machines by partitioning the resources of the physical server or host on which it is installed.*

- *Provides connectivity between virtual machines and between the virtual machines and external network resources.*

- *Provides isolation between individual virtual machines.*

- *Also provides tools and procedures for easier management and provisioning of the virtual machines running on it.*

### Virtual Switch Features

*A virtual switch (vSwitch) is a virtualized system that allows you to assign network virtual machine interfaces. This virtual element emulates a Layer 2 switch and allows devices in the same vSwitch to communicate.*

*A vSwitch runs as part of a hypervisor and provides the connectivity that each virtual machine requires.*

*Because it is usually impractical to have more than a few physical network adapters in a host, vSwitches allow you to assign fewer interfaces.*

*The figure shows four virtual machines that connect to the same switch, which has access to the outside network.*

![Virtual Network Components](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/virtual_network_components.png)

*A vSwitch has certain features:*

- *A vSwitch is necessary because it is usually impractical to have more than a few physical network adapters in a host.*

- *Physical NICs often act as uplink ports in the vSwitches that are created on the VMware hypervisor level.*

- *All virtual machines that are running on a single physical server share the physical switch ports for network access.*

- *Virtual machines can have one or more vNICs. You can attach vNICs to a vSwitch that uses one or more physical NICs in a host.*

- *When connected to a vSwitch, virtual machines behave as if they are connected to a normal network switch.*

*A vSwitch also presents these challenges:*

- *Configurations that you perform on a physical network switch that connects to a host will affect all the virtual machines on that host.*

- *If you move the virtual machine between hosts, a different configuration on the network switch port that is connected to the target host can impact it.*

- *In a virtual machine environment, you must avoid shutting down the switch port that connects to the server. Otherwise, it would impact the network access for all the virtual machines and cause a greater impact to the production environment.*

### Virtual Machine Benefits

*Virtual machines offer several benefits over physical devices. A virtualization approach is very cost-effective compared to the standard application architecture, which involves a single operating system that is installed on each computer.*

*The figure shows key properties of VMware virtualization products, such as the VMware ESXi hypervisor.*

![VM Benefits](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vm_benefits.png)

*Virtual machine benefits include the following:*

- ***Partitioning:***

*Virtual machines allow for a more efficient use of resources, because a single host can serve many virtual machines.*

*The host memory capacity and the memory requirements of the virtual machine are the only limiting factors.*

*A hypervisor divides the server system resources between virtual machines.*

- ***Isolation:***

*Virtual machines in a virtualized environment have as much security as in traditional physical server environments because VMs are not aware of the presence of other virtual machines.*

*Virtual machines that share the same host are completely isolated from each other.*

*Failure of a critical hardware component, such as a motherboard or power supply, can bring down all the virtual machines that reside on the affected host.*

*Recovery is much faster with virtual machines than with physical servers. Other hosts in the virtual infrastructure can take over virtual machines from the failed host and have less downtime.*

- ***Encapsulation:***

*Virtual machines reside in a set of files that describe them and define their resource usage and unique identifiers.*

*Virtual machines are extremely simple to back up, modify, or even duplicate in several ways.*

*This encapsulation can be deployed in environments that require multiple instances of the same virtual machine, such as classrooms.*

- ***Hardware abstraction:***

*You can provision or migrate any virtual machine to any other VMware ESXi server with similar physical characteristics.*

*Support is provided for multiple operating systems: Windows, Linux, and others.*

*There is broader support for hardware, because the virtual machine does not rely on drivers for physical hardware.*

*You can also move virtual machines between hosts. This mobility is beneficial for the following reasons:*

- ***Optimum performance:*** *If a virtual machine on a given host starts exceeding the resources of the host, you can move it to another host that has sufficient resources.*

- ***Maintenance:*** *If you must perform maintenance or upgrade a host, you can temporarily redistribute the virtual machines from that host to other hosts. After you complete the maintenance, you reverse the process, resulting in no downtime for users.*

- ***Resource optimization:*** *If the resource usage of one or more virtual machines decreases, one or more hosts may no longer be necessary. In this case, you can redistribute the virtual machines and power off the emptied hosts to reduce cooling and power requirements.*

### VMware vSphere Architecture

*VMware vSphere is a suite of software components for virtualization that include ESXi, vCenter Server, and other software components.*

*The figure shows the components of the VMware vSphere solution.*

![VMware vSphere](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/wmware_vsphere.png)

*vSphere includes the following software components:*

- ***ESXi:***

*This hypervisor runs virtual machines. Each virtual machine has a set of configuration and disk files that together perform all the functions of a physical machine.*

*Through the ESXi instance, you run the virtual machines, install operating systems, run applications, and configure the virtual machines. Configuration includes identifying the virtual machine resources, such as storage devices.*

- ***vCenter Server:***

*This service acts as a central administrator for VMware ESXi hosts that connect on a network. vCenter Server directs actions on the virtual machines and the ESXi hosts.*

*vCenter Server is a single Windows or Linux service and is installed to run automatically. The vCenter Server service runs continuously in the background and performs monitoring and management.*

- ***vSphere Web Client:***

*The vSphere Web Client is an HTML5-based lightweight client for administering your vSphere environment. It is the primary interface for connecting to and managing vCenter Server instances.*

*Note: In the past, there was an option to manage a vSphere environment with vSphere Client (Desktop). Starting with vSphere 6.5, the existing desktop vSphere Client (the thick client) is deprecated and was replaced by the vSphere Web Client.*

## Virtual Machine Manager

*ESXi supports a very robust remote management system that enables you to create, remove, and manage virtual machines. The VMware environment also supports various virtualization services that enable different functionalities like high-availability features, scalability, automation, and others. Together they form the vSphere platform.*

### VMware vCenter Server

*The vCenter Server is a central component of the vSphere platform. The vCenter system allows you to manage the VMware virtual environment and its functionalities:*

- *It requires an extra license and serves as a focal point for management of multiple hosts.*

- *It correlates traffic between hosts for functionalities that span more than a single host. Features like VMware vMotion, VMware vSphere Distributed Switch (vDS), fault tolerance, and others require the vCenter Server.*

- *It is considered a crucial component of advanced ESXi deployments. Failure of a vCenter Server does not stop production traffic or affect virtual machine operations. However, features like central management of ESXi hosts, high availability, vSphere Distributed Switch, Distributed Resource Scheduler (DRS), and vMotion are unavailable until failure is not restored. For that reason, Cisco recommends that you have a redundant vCenter deployment.*

![vCenter Server Appliance Systems](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/machine_server.png)

*The vCenter Server can exist as a physical device, or you can install it as a virtual machine on a host that it manages. VMware vCenter (vCenter) is available in a Windows and an appliance version. vCenter Server Appliance is a preconfigured Linux-based virtual machine with an embedded PostgreSQL database that is optimized for running vCenter Server and the associated services. vCenter Version 7.0 can manage up to 2500 ESXi hosts per vCenter Server and 40,000 powered-on virtual machines.*

### vSphere Client

*vSphere Web Client is a lightweight HTML5-based GUI component for the vCenter Server that allows interaction with the ESXi servers and virtual machines.*

*The following screenshot is from the vSphere Web Client.*

![vSphere Web Client](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vsphere_web_client.png)

*Depending on the access permissions, the user can access some of the virtualized environment or the entire environment. For example, users who can connect to the consoles of the virtual machines have no ability to start or stop those virtual machines or change the parameters of the underlying host.*

*To simplify user management, the VMware environment supports integration with the Active Directory user database, so when users log in to the vSphere client, they can use their domain credentials. This approach allows administrators to define user roles for users with different permissions such as administrator and read only. These permissions can then be used to access and manage all systems that connect to the Active Directory database. Users also use only one set of credentials to access multiple systems or devices. This functionality allows administrators to create user accounts, change user permissions, or disable a user account at a central location only (the Active Directory database) and not on each system or device separately.*

### vSphere Features

*The vSphere infrastructure has an extensive feature set that provides virtual environments with unique functionalities that are not easily replicated on a physical infrastructure, like high availability with seamless failover.*

#### vSphere vMotion

*The ability to move virtual machines around the virtual infrastructure without any downtime or other impact on service availability is valuable for day-to-day data center operations:*

- *It is a powerful tool for maintenance or resource distribution situations, but it is not designed for disaster recovery.*

- *If a host on which a VMware vMotion virtual machine resides fails, then that virtual machine goes offline until another host recovers it.*

![vMotion Technology](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vmotion_technology.png)

#### vSphere High Availability

*When the virtual infrastructure detects the failure of a host, one or more backup hosts will restart the virtual machines that the host maintains:*

- *The hosts monitor each other with heartbeats every 15 seconds. If a host fails to respond and is unreachable by ping for 15 seconds, it is isolated. Virtual machines that are running on that host will restart on another host.*

- *The isolated host is also aware of other hosts. If it does not receive a heartbeat from any other host in the group, it declares itself isolated from the network.*

*Because the feature allows fast recovery from a failed state without much overhead, this common resiliency option is used in the vSphere environment.*

![vSphere High Availability](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vsphere_ha.png)

#### vSphere Fault Tolerance

*This function allows the virtual machine to survive the failure of a host with zero downtime.*

- *If the active host fails, the I/O requests are simply redirected, and transactions continue without interruption or loss.*

- *Any change that happens on the active (primary) host is immediately synchronized to the standby (secondary) through the VMware Fast Checkpointing system.*

*vSphere Fault Tolerance provides instantaneous failover and continuous availability with the following benefits:*

- *Zero downtime*

- *Zero data loss*

- *No loss of TCP connections*

*The following figure shows how VMware Fast Checkpointing synchronizes the primary and secondary virtual machines. It follows the changes on the primary virtual machine and mirrors them to the secondary virtual machine.*

![VMware Fast Checkpointing](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vmware_fast_checkpointing.png)

*Due to synchronization limitations and overhead, this option is not often used.*

#### vSphere DRS

*The VMware vSphere Distributed Resource Scheduler (DRS) feature load-balances virtual machines across the available hosts to provide optimum performance. Migrating the virtual machines happens automatically through the underlying vMotion feature:*

- *If usage of the resources on a current host exceeds the defined limit, one or more virtual machines are relocated to other hosts to prevent degraded performance.*

- *If you must perform an upgrade on one host in the group, vSphere DRS allows you to automatically migrate all virtual machines to other hosts once you place it into maintenance mode.*

*The figure shows how vSphere DRS helps dynamically balance virtual machine workloads across resource pools.*

![vSphere DRS](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vsphere_drs.png)

#### vSphere DPM

*VMware vSphere Dynamic Power Management (DPM) reduces operating expenses in the data center by migrating the virtual machines to as few of the hosts as possible. Migrating the virtual machines happens automatically with the underlying vMotion feature:*

- *Hosts that are unnecessary are powered off to conserve power and cooling.*

- *Wake-up protocols restart the host if more resources are needed.*

*The figure depicts vSphere DPM consolidating virtual machine workloads to reduce power consumption.*

![vSphere DPM](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vsphere_dpm.png)

## Lab: Install VMware ESXi and vCenter

**Install VMware ESXi on Cisco UCS C-Series:**

*Big Picture (Why all these steps exist)*

You are doing *three distinct things* that just happen to overlap during boot:

1. *Out-of-band server management* via *Cisco IMC + KVM* (remote hands).

2. *Disk presentation* via the *LSI RAID controller* (how ESXi sees storage).

3. *Hypervisor installation* (ESXi installed onto whatever storage RAID exposes).

Once you separate those layers mentally, the process becomes far less confusing.

**Accessing the Server (IMC + KVM):**

- Log into *Cisco Integrated Management Controller (IMC)* at ```https://10.1.6.9```.

- Launch *KVM Console* → this gives you keyboard/video/mouse access *as if you were physically in front of the server.*

*Note: What is the ```.jnlp``` file?*

- The ```.jnlp``` file launches a *Java-based KVM client.*

- Its sole purpose is to establish a *secure remote console session.*

- This is legacy-but-common in enterprise gear; newer platforms use HTML5 instead.

**Virtual Media (Mounting the ESXi ISO):**

- *Virtual Media* → *Activate Virtual Devices*

- *Map CD/DVD* → select the ESXi ISO

- Result: the ISO appears to the server as a *physical DVD drive (vDVD).*

This is how you install ESXi *without physical access.*

**Boot Control:**

- Set *Boot Device* = *vDVD*

- Perform a *warm reboot*

At this point the server will boot into *whatever the ISO contains* — not the disks.

**RAID Configuration (LSI MegaRAID):**

This is the part that feels chaotic — here’s what’s *actually* happening.

*Why RAID at all?*

- ESXi *does not manage raw disks directly.*

- The RAID controller must present *one logical disk (LUN)* to ESXi.

*Easy Configuration explained:*

- *Clear Configuration* → removes any old RAID metadata.

- *Easy Configuration* → fastest way to create a basic array.

- Selecting disk → marks it as a RAID member.

- *RAID 0* → single disk, no redundancy (lab‑friendly, fast, disposable).

Result: LSI presents *a single virtual disk* to the OS. This is what ESXi will later see as *"Local Disk".*

Screenshot from the lab:

![Easy Configuration](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/array_configuration_finished.png)

**Why the RAID gets “destroyed” later (Important clarification):**

This is the subtle but critical part.

- During ESXi installation, the installer *reinitializes disk metadata.*

- On this *specific UCS + LSI combo,* that action invalidates the RAID config.

- The RAID controller still exists — it just loses the logical drive definition.

That’s why you must:

- *Re-select RAID as the boot device* after installation

- Let the controller rebuild/re-recognize the array

This is *hardware-specific weirdness,* not a universal ESXi behavior.

**Static Macros (Why Ctrl-Alt-Del matters):**

- KVM intercepts certain key combos.

- *Static Macros* ensure Ctrl-Alt-Del is sent to the *server,* not your OS.

Without this, you’d reboot *your VM desktop,* not the UCS server.

**ESXi Installation Flow:**

- Boot from ISO

- Accept EULA

- Select *local disk* (this is the RAID LUN you created earlier)

- Set keyboard layout

- Set root password

- Confirm install → reboot

Even though you chose a *"TOSHIBA disk"* (as seen during the lab), you are still installing onto *RAID-presented virtual disk backed by that physical drive.*

**Post-Install Boot Fix (LSI quirk):**

- Switch *Boot Device = RAID*

- Reboot

- Enter LSI utility if prompted

This ensures the firmware boots from the RAID logical disk where ESXi now lives.

Last step in this stage of the lab:

![LSI MegaRAID](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/lsi_mega_raid.png)

**Mental Model (TL;DR)**

```
IMC/KVM → gives you hands
vDVD → feeds installer
RAID → creates disk ESXi can see
ESXi → installs onto RAID LUN
Boot fix → tells firmware where ESXi lives
```

### Configure ESXi LAN Connectivity

*Goal of this section:*

Before ESXi is usable, you must:

- Bind *one physical NIC (vmnic)* to management

- Assign a *static IPv4 address*

- Verify *routing and reachability*

- Enable SSH for CLI-based validation

This all happens *locally on the ESXi DCUI* (yellow/gray screen).

Example from the lab:

![ESXI IP config](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/ip_config_esxi.png)

**Entering ESXi System Customization:**

- Press F2 → log in as ```root```

- This menu configures the *management plane only* (vmk0)

Think of this like configuring ```mgmt0``` on a Nexus switch.

**Selecting the Management NIC:**

- *Configure Management Network* → *Network Adapters*

- Ensure *vmnic1* is selected (X in brackets)

*Notes:*

- ESXi names physical NICs as ```vmnicX```

- The selected NIC backs the *vmkernel interface vmk0*

- Lab uses *untagged (native) VLAN*, so no VLAN ID is required

- VLAN ID left empty

- This means *native VLAN / access port* behavior

If this were a tagged management VLAN, you would enter the VLAN ID here.

**Assigning a Static IPv4 Address:**

- *IPv4 Configuration* → *Set static IPv4 address*

Configured values:

- IP Address: ```10.1.5.9```

- Subnet Mask: ```255.255.255.0```

- Default Gateway: ```10.1.5.1```

This creates:

- A vmkernel interface (```vmk0```)

- A connected route for the local subnet

- A default route via the gateway

**Applying Changes:**

- Press Esc → accept changes

- *Restart Management Network*

Why restart?

- ESXi restarts only the management stack, not the whole host

- Similar to bouncing an interface, not rebooting the switch

**Enabling SSH (Troubleshooting Options):**

- *Troubleshooting Options* → *Enable SSH*

SSH is disabled by default for security reasons. In labs, SSH is essential for:

- ```esxcli```

- Network verification

- Scripted configuration

**Rebooting the Host:**

Reboot ensures:

- NIC bindings persist

- Management services fully reload

F12 via KVM sends a *hardware-level reboot,* not just an ESXi service restart.

**Verifying Connectivity via SSH:**

Once the host is back online:

- SSH to ```10.1.5.9``` using PuTTY

Verify IP configuration:

```
[root@localhost:~] esxcli network ip interface ipv4 get
Name IPv4 Address IPv4 Netmask IPv4 Broadcast Address Type Gateway DHCP DNS
---- ------------ ------------- -------------- ------------ -------- --------
vmk0 10.1.5.9 255.255.255.0 10.1.5.255 STATIC 10.1.5.1 false
```

Key takeaways:

- ```vmk0``` = ESXi management interface

- STATIC confirms no DHCP dependency

Verify routing table:

```
[root@localhost:~] esxcli network ip route ipv4 list
Network Netmask Gateway Interface Source
-------- ------------- -------- --------- ------
default 0.0.0.0 10.1.5.1 vmk0 MANUAL
10.1.5.0 255.255.255.0 0.0.0.0 vmk0 MANUAL
```

This confirms:

- Local subnet is directly connected

- Default route points to the gateway

**Connectivity Test:**

- ```ping 10.1.5.1```

ESXi’s ```ping``` behaves very similarly to IOS / NX-OS:

- ICMP only

- No fancy options & pure reachability test

**Why the Firefox step appears next?**

At this point the lab is transitioning from *host-level access (DCUI / SSH)* to *service-level access (Web UI / vCenter setup).*

The browser will be used next to access:

- ESXi Host Client (HTTPS)

- vCenter installer

This step makes sense *only in the context of what follows.*

### Add a Datastore on the VMware ESXi

*Goal of this section:*

Here we transition from *host bring-up* to *usable virtualization* by:

- Verifying ESXi networking constructs (vmk, vSwitch, port groups)

- Understanding how traffic leaves the ESXi host

- Preparing the host to consume *shared storage (NFS datastore)*

This is foundational for vCenter, vMotion, and multi-host clusters.

**Accessing the ESXi Host Client:**

- Open a new browser tab

- Navigate to ```https://10.1.5.9```

- Log in as ```root```

The ESXi Host Client is:

- A lightweight web UI

- Host-local (not vCenter)

- Used for single-host management and bootstrap tasks

**Verifying Networking Constructs:**

Navigate to:

- *Networking* → *Virtual Switches*

Key components to understand here: *VMkernel NICs (vmk)*

- ```vmk0``` = management interface

Bound to: *A port group* which lives on a *vSwitch.*

This mirrors a logical stack:

```
Physical NIC (vmnic)
↓
vSwitch
↓
Port Group
↓
VMkernel NIC (vmk0)
```

vmk interfaces are used for:

- Management

- vMotion

- NFS / iSCSI

- vSAN

**Port Groups (Important Concept):**

Navigate to:

- *Networking* → *Port Groups*

Notes:

- Port groups are *ESXi-only constructs*

- They act like policy containers

- VLAN ID, security settings, and traffic shaping live here

This lab includes *VM Network port group.* This port group will later be used by the vCenter virtual machine NIC.

Example from the lab:

![Port Groups](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/port_groups.png)

**Relationship Between Port Groups and vSwitches:**

Click *vSwitch0* from the VM Network pane.

Important rules:

- A vSwitch can host *multiple port groups*

- A port group belongs to *exactly one vSwitch*

- A vSwitch requires an *uplink (vmnic)* to reach the external network

*Critical takeaway:* if a vSwitch has *no physical uplink,* all attached VMs are isolated. This is a very common troubleshooting pitfall.

**Uplink Constraints:**

In this lab:

- Only *one physical NIC* is available

- That NIC is already bound to *vSwitch0*

Therefore:

- You cannot assign the same vmnic to another vSwitch

- All traffic (management + VM traffic) shares this uplink

In real deployments multiple vmnics are used for redundancy and separation.

**Transition to Storage Configuration:**

Navigate to:

- *Storage* in the left menu

Observation: *only datastore1* exists. Why this matters?

Local datastore:

- Single point of failure

- Not shared

- No vMotion

This is why:

- NFS, iSCSI, or SAN-backed datastores are preferred

- Shared storage enables cluster-level features

This step completes the triangle:

```
Compute (ESXi)
Networking (vSwitch / vmk)
Storage (NFS datastore)
```

### Deploy the VMware vCenter Server Appliance

*What vCenter actually is (mental anchor):*

- ESXi alone = *single-host island*

- vCenter = *control plane* for clusters, HA, vMotion, permissions, sanity... If you’re managing more than one host, vCenter isn’t optional — it’s inevitable.

*Installer Launch (Windows VM):*

Path in the lab (shared storage):

```
S:\Software\VMware\VMware-VCSA-all-6.7.0-8217866\
```

Run:

```
vcsa-ui-installer\win32\installer.exe
```

- Accept security warning

- Choose *Install*

- Accept license

**Stage 1 – Appliance Deployment:**

Deployment type:

- vCenter Server *with Embedded PSC* → Default, recommended, fewer moving parts

Target ESXi:

```
Host: 10.1.5.9
User: root
Pass: 1234QWer
```

- Certificate warning = expected (self-signed ESXi)

Appliance settings:

```
VM name: VMware vCenter Server Appliance
Root password: 1234QWer
Deployment size: Tiny
Datastore: datastore1
Disk mode: Thin
```

Tiny is perfect for labs; thin disks save storage and pain.

**Network Configuration (do not rush this):**

Static config:

```
IP address:     10.1.5.209
Subnet mask:    255.255.255.0
Gateway:        10.1.5.1
DNS server:     192.168.10.40
```

Notes:

- DNS is *mandatory* for vCenter stability

- IP-only setups work short-term, hurt later

Finish Stage 1 → ~10–15 minutes. This stage *deploys and powers on* the appliance VM.

Example from the lab:

![Stage 1 completed](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/config_review_vcenter.png)

**Stage 2 – vCenter Services Configuration:**

Time:

- Sync with ESXi host (default)

SSO (vSphere Identity):

```
SSO domain: vsphere.local
User: administrator@vsphere.local
Password: 1234QWer
```

Important distinction:

- ```root``` → appliance OS

- ```administrator@vsphere.local``` → vCenter itself

CEIP: optional → Next

Review → Finish

Do *not* close the installer during this phase.

**Accessing vCenter:**

Open:

```
https://10.1.5.209:443
```

- Accept browser security warning

- Launch *vSphere Client (HTML5)*

Login:

```
administrator@vsphere.local
1234QWer
```

**State of the world (checkpoint):**

You now have:

```
ESXi host (compute)
↓
Datastore (storage)
↓
vCenter (management/control plane)
```

### Create a Data Center and Add ESXi Hosts

Once vCenter is alive, it becomes the *authority layer* — ESXi hosts no longer live alone, they get absorbed into a hierarchy. You start by right-clicking the vCenter IP and creating a *Datacenter,* which is purely a logical container (think *geographic / organizational boundary,* not hardware). Inside that datacenter, you *add hosts,* authenticating as ```root```, accepting certificates, licenses, and leaving Lockdown disabled for lab sanity. When the wizard finishes, vCenter takes over host management and you’ll see the ESXi host *and* the vCenter VM nested beneath it — that visual nesting is the “it worked” signal.

Example from the lab:

![VMware vCenter Server At Last](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/data_center_summary_step.png)

*Important clarifications worth keeping in the notes:*

- *Datacenter* = logical scope (permissions, inventory, grouping).

- *Host* = actual ESXi hypervisor being managed.

- vCenter itself is just another VM, but once registered, it manages the host it runs on — a delightful bootstrap paradox.

- Clusters come later; this lab stops just before HA/DRS magic.

Here's our final *state-of-the-world sanity map,* fresh and clean:

```
vCenter (10.1.5.209)
└── NY Data Center
    └── ESXi Host (10.1.5.9)
        ├── datastore1
        ├── vSwitch0
        └── VMware vCenter Server Appliance (VM)
```

This lab is now concluded.
