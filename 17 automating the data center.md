# Automating the Data Center

*A programmable infrastructure can support dynamic and elastic cloud-computing environments without human intervention. It can manage the entire system as a single logical entity within a higher-level framework. It automates tedious, manual, error-prone processes while speeding deployment and reducing errors. Users can deploy the available programmability tools to increase resource utilization and provide greater flexibility and scalability.*

## Cisco NX-OS Programmability

*The automation of day-to-day management, monitoring, and configuration changes can increase the efficiency of infrastructure operations teams. The Cisco Nexus Operating System (Cisco NX-OS), with its rich set of programmable features, allows you to completely automate and streamline this process.*

*In typical environments, where the traditional infrastructure management process is used, network devices are managed via the CLI. This traditional method has its deficiencies. It is error-prone and not scalable.*

*Remember these key concepts of the traditional approach to network management:*

- *Traditional network management processes use the CLI to get and send commands to devices.*

- *Engineers prepare configurations in a text editor and use the copy-and-paste method.*

- *Some degree of automation happens via Tool Command Language (TCL) or Expect scripts.*

- *The CLI can return unexpected output.*

- *The process is error prone.*

*Challenges with a traditional network management process:*

- *Scalable infrastructure management.*

- *The network lacks industry automation capabilities.*

*If you focus on servers, the capital expenditures (CapEx) have been flat or declining for the past 15 years. However, the operating expenditures (OpEx) have been growing steadily and now represent as much as two-thirds of the total expenses that are associated with servers. You can see something similar in the network space.*

*Virtualization increases the problem because higher device usage comes at the price of increasing complexity that results in rising OpEx. The reason stems from the problem of the traditional approach to management in many IT organizations. Without a simpler approach to management, administration costs will continue to escalate.*

*Therefore, it is important to include automation in the network management process. An essential part of automation is programmability.*

*Programmability brings these benefits:*

- *Saves resources.*

- *Enables fast and flexible service delivery.*

- *Reduces human error.*

- *Allows customization and innovation.*

## Network Management Interfaces

*Cisco NX-OS Software supports traditional management interfaces like CLI, Simple Network Management Protocol (SNMP), Syslog, and others. Cisco NX-OS also supports Network Configuration Protocol (NETCONF), a newer network management protocol that is gaining popularity among network management protocols in recent years. You can use all those protocols to implement some degree of automation.*

*Cisco NX-OS supports the following network management protocols and technologies:*

- *CLI*

- *SNMP*

*Cisco Nexus platforms support the following programmability tools:*

- *NX-API support*

- *Python scripting*

- *TCL scripting*

*Cisco Nexus 9000 devices also support the following programmability tools:*

- *Broadcom shell*

- *Bash*

- *Bash shell access and Linux container support*

- *Guest Shell*

*The typical network management protocols and technologies are the following:*

1. ***CLI:***

- *It is designed as a human-readable interface.*

- *Returns unstructured data that requires post-processing.*

*Note: Cisco NX-OS allows users to ```pipe``` command output to XML or JSON.*

2. ***SNMP:***

- *Widely used for monitoring of network devices.*

- *Cisco NX-OS supports SNMPv1, v2, and v3.*

3. ***Cisco NX-OS programmable interface agents:***

- *NETCONF*

- *Representational State Transfer Configuration (RESTCONF)*

- *Google Remote Procedure Call (gRPC)*

## Open Cisco NX-OS Overview

*Open Cisco NX-OS Software allows administrators to manage a switch such as a Linux device. The Open Cisco NX-OS Software stack addresses several functional areas to address the needs of a DevOps-driven automation and programmability framework.*

*The open Cisco NX-OS Linux network architecture has two primary layers:*

1. ***User space processes and software that is composed of traditional Cisco NX-OS Software processes and third-party user applications:***

- *Traditional processes include Open Shortest Path First (OSPF), virtual port channel (VPC), Border Gateway Protocol (BGP), Cisco NX-OS, and Address Resolution Protocol (ARP).*

- *Third-party user applications include configuration management, visibility and analytics, and custom-built agents and tools.*

2. ***64-Bit Linux 3.4.10 Kernel Layer has Linux kernel network devices and the Linux networking stack (route and ARP tables)***

![Open Cisco NX-OS Overview](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/open_NX-OS_overview.png)

*What has been exposed in the Open Cisco NX-OS network architecture is access to the Linux kernel networking stack. Here, the switch physical and logical interfaces have representation as a net device and an IP address in the kernel layer. This design opens the door to managing the routing and front panel ports using unmodified Linux-based tools and applications. However, you need a synchronization function between Cisco NX-OS and the Linux kernel layer to ensure the two layers work effectively.*

*This synchronization function between user-space Cisco NX-OS processes and the netbroker module provides the kernel layer. It ensures that changes you implement to physical and logical Cisco NX-OS interfaces reflect correctly to the Linux net device interfaces. Cisco NX-OS routing applications and processes program routes, like BGP. They program these routes directly in the Cisco NX-OS route table. This table pushes it to the Linux kernel route table. Similarly, if you install a route at the Linux kernel layer, the netbroker module checks the validity of the route addition. It forwards it to the Cisco NX-OS Routing Information Base (RIB) process, which then programs the route table in the hardware table if it is valid.*

*In the architecture, virtual routing and forwarding (VRF) instances are implemented using Linux network namespaces. Network namespaces are a natural fit, providing the same isolation capabilities as VRFs. A kernel net device is associated with only one network namespace. The routing and ARP tables are local to a network namespace so that tasks running in the namespace see only the resources that are assigned to the namespace.*

## Linux Kernel Stack

*A core capability of Open Cisco NX-OS is exposing all interfaces on the device (including front panel switching ports) as Linux network devices, which enables these components:*

- ***Linux utilities for interface management:*** *Use standard Linux utilities like ifconfig, ethtool, and route to manage network interfaces, routing, and associated parameters.*

- ***Linux tools for troubleshooting:*** *Use tools like tcpdump, ping, and traceroute to troubleshoot network issues.*

- ***VRF capabilities with namespaces:*** *Each VRF created within Open Cisco NX-OS will have a corresponding namespace in Linux associated with it. It maintains the VRF isolation extension from Open Cisco NX-OS to the Linux Kernel.*

- ***Linux socket communications:*** *Open Cisco NX-OS and user applications use the Linux kernel’s networking stack (kstack) to send and receive packets to and from the external world. It enables applications that use standard Linux sockets, such as agents and monitoring tools, to work without custom compilation.*

*Kernel Stack (kstack) uses well-known Linux application programming interfaces (APIs) to manage the routes and front panel ports.*

*Linux Open Containers, like the Guest Shell, are Linux environments that are decoupled from the host software. You can install or modify software within that environment without impacting the host software packages. Guest Shell, Docker containers, and the host Bash Shell all use Kernel Stack.*

## Bash Shell and Guest Shell for Cisco NX-OS

*Cisco NX-OS supports two Linux environments:*

1. ***Bash shell:***

- *Allows access to the underlying Linux system.*

- *Disabled by default.*

2. ***Guest Shell:***

- *Secure Linux container environment running CentOS 7.*

- *Decoupled from the host Cisco Nexus 9000 Cisco NX-OS Software.*

- *Allows you to add software packages and update libraries as necessary without impacting the host system software.*

- *Enabled by default.*

## Bash Shell

*You can access Bash from the Cisco NX-OS CLI. Bash is accessible from user accounts that are associated with the Cisco NX-OS DevOps or network-admin role.*

*To access the Bash shell, use the following commands:*

- *First, you must enable the Bash feature:*

```
switch# configure terminal
switch(config)# feature bash-shell
```

- *After the feature is enabled, you can access the Bash:*

```
switch# run bash
```

- *You can then use standard Bash commands:*

```
bash-4.2$ whoami
admin
bash-4.2$ pwd
/bootflash/home/admin
```

*You can also execute a Bash command with the ```run bash command``` command. For example, if you want to check the current location in the filesystem, use the command ```run bash pwd```. You can also run Bash by setting the shell type to Bash for a particular user. Use the command ```username user shelltype bash```. This command puts you directly into the Bash shell upon login. In this case, you do not need to enable the Bash shell feature. You can also run Cisco NX-OS CLI commands from the Bash. Use the ```vsh -c``` command. You can run more commands by separating commands with a space and semicolon.*

*You can use the Bash shell to run various scripts that can help you to manage your Cisco Nexus 9000 devices.*

*The following example shows how you can use Bash scripts for managing the device.*

- *This script periodically counts the number of routes and stores the number of routes to the file:*

```
#!/bin/bash

i=0
while [ $i -lt 120 ]
do
  echo "`date`: `vsh -c "show ip route" | grep ubest | wc -l`" >> route_count
  sleep 30
  i=$[$i+1]
done
```

**Additional Note:**

This script samples the routing table every 30 seconds for about an hour and logs how many active routes exist at each moment. The main line runs ```show ip route``` inside NX-OS via ```vsh```, filters only the *best usable routes* (```ubest```), counts them with ```wc -l```, and appends that number to a file called ```route_count```, timestamp included. So each line becomes a little heartbeat: *time → number of installed routes.*

- *You can run this script from the Cisco NX-OS CLI:*

```
switch# run bash /bin/bash /bootflash/home/admin/script.sh
```

- *Now verify the file with outputs:*

```
switch# show file bootflash:home/admin/route_count
Fri Mar 22 10:27:09 UTC 2019: 16
Fri Mar 22 10:27:39 UTC 2019: 16
Fri Mar 22 10:28:10 UTC 2019: 16
```

*The features on the Cisco Nexus 9000 switches are distributed as packages. You can use the Bash shell to manage those packages.*

*You can use the ```yum``` utility to install, upgrade, downgrade, or patch various features.*

- *The ```yum list installed``` command displays the list of all installed packages with associated versions:*

```
bash-4.2$ yum list installed | grep n9000
base-files.n9000                        3.0.14-r74.2                   installed
bfd.lib32_n9000                         1.0.0-r0                       installed
core.lib32_n9000                        1.0.0-r0                       installed
eigrp.lib32_n9000                       1.0.0-r0                       installed
eth.lib32_n9000                         1.0.0-r0                       installed
isis.lib32_n9000                        1.0.0-r0                       installed
```

*You can use these options with the ```yum``` command:*

- *```yum list installed```: Displays a list of the Cisco NX-OS feature Red Hat Package Managers (RPMs) installed on the switch.*

- *```yum list available```: Displays a list of the available RPMs.*

- *```sudo yum -y install rpm```: Installs an available RPM package.*

- *```sudo yum -y upgrade rpm```: Upgrades an installed RPM.*

- *```sudo yum -y downgrade rpm```: Downgrades the RPM if any of the Yum repositories have a lower version of the RPM.*

- *```sudo yum -y erase rpm```: Erases the RPM.*

- *```yum list --patch-only```: Displays a list of the patch RPMs present on the switch.*

- *```sudo yum install --add URL_of_patch```: Adds the patch to the repository.*

- *```sudo yum install patch_RPM --nocommit```: Activates the patch RPM, where ```patch_RPM``` is a patch that is in the repository.*

- *```sudo yum install patch_RPM --commit```: Commits the patch RPM. You must commit the patch RPM to keep it active after reloads.*

- *```sudo yum erase patch_RPM --nocommit```: Deactivates the patch RPM.*

- *```sudo yum install --remove patch_RPM```: Removes an inactive patch RPM.*

## Guest Shell

*In addition to the Cisco NX-OS CLI and Bash access on the underlying Linux environment, the Cisco Nexus 9000 Series devices support access to Guest Shell. It is a decoupled execution space within a Linux Container (LXC). Guest Shell is accessible to the users with the network-admin role.*

*Here are the characteristics of Guest Shell:*

- *It is automatically enabled in the system.*

- *The Guest Shell is populated with CentOS 7 Linux.*

- *Use the ```run guestshell``` or ```guestshell``` commands to access the Guest Shell.*

- *Use the ```run guestshell command``` command to execute the command in Guest Shell.*

- *Use the ```dohost command``` command to run the Cisco NX-OS command from Guest Shell.*

*By default, the resources for the Guest Shell have a small impact on resources available for normal switch operations.*

*The table shows the default, minimum, and maximum resources for Guest Shell.*

![Guest Shell Resources](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/guess_shell_resources.png)

*The CPU limit is the percentage of the system compute capacity that tasks running within the Guest Shell receive when contention with other compute loads occurs in the system. When there is no contention for CPU resources, the tasks within the Guest Shell are unlimited.*

*Misbehaving or malicious application code can cause a denial of service (DoS) as the result of over-consumption of connection bandwidth, disk space, memory, and other resources. The host provides resource-management features that ensure fair allocation of resources between Guest Shell and services on the host.*

*Guest Shell has various utilities and capabilities available by default:*

- *Guest Shell lets you use ```yum``` install software for installing the packages.*

- *Guest Shell is prepopulated with many common Linux tools:*

1. *net-tools*

2. *iproute*

3. *tcpdump*

4. *OpenSSH*

- *Python 2.7.5 is included by default, as is the pip for installing additional Python packages.*

*The following list shows some commands that you can use to manage the Guest Shell:*

- *```guestshell enable```: Installs and activates the Guest Shell.*

- *```guestshell disable```: Shuts down and disables the Guest Shell.*

- *```guestshell upgrade```: Deactivates and upgrades the Guest Shell.*

- *```guestshell reboot```: Deactivates the Guest Shell and then reactivates it.*

- *```guestshell destroy```: Deactivates and uninstalls the Guest Shell.*

- *```guestshell resize {cpu | memory I rootfs}```: Changes the allotted resources available for the Guest Shell.*

- *```show guestshell detail```: Displays details about the Guest Shell.*

*Guest Shell is enabled by default. To disable Guest Shell, use the ```guestshell disable``` command. The following output shows a Guest Shell disabling example:*

```
switch# guestshell disable
You will not be able to access your guest shell if it is disabled. Are you sure you want to disable the guest shell? (y/n) [n] y
2018 Jul 30 06:42:20 switch %$ VDC-1 %$ %VMAN-2-ACTIVATION_STATE: Deactivating virtual service 'guestshell+'
2018 Jul 30 06:42:26 switch %$ VDC-1 %$ %VMAN-2-ACTIVATION_STATE: Successfully deactivated virtual service 'guestshell+'
```

*If you want to uninstall Guest Shell, use the ```guestshell destroy``` command. The following output shows a Guest Shell destroying example:*

```
switch# guestshell destroy
You are about to destroy the guest shell and all of its contents. Be sure to save your work. Are you sure you want to continue? (y/n) [n] y
2018 Jul 30 06:57:10 switch %$ VDC-1 %$ %VMAN-2-INSTALL_STATE: Destroying virtual service 'guestshell+'
2018 Jul 30 06:57:10 switch %$ VDC-1 %$ %VMAN-2-INSTALL_STATE: Successfully destroyed
```

*The ```guestshell enable``` command allows you to install and activate the Guest Shell. If you provide no additional parameters, the embedded package from the system image installs and activates. You can also provide your own software package. The following example shows the output when you enable the Guest Shell:*

```
switch# guestshell enable
2018 Jul 30 07:10:17 switch %$ VDC-1 %$ %VMAN-2-INSTALL_STATE: Installing virtual service 'guestshell+'
2018 Jul 30 07:10:32 switch %$ VDC-1 %$ %VMAN-2-INSTALL_STATE: Install success virtual service 'guestshell+'; Activating
2018 Jul 30 07:10:32 switch %$ VDC-1 %$ %VMAN-2-ACTIVATION_STATE: Activating virtual service 'guestshell+'
2018 Jul 30 07:11:06 switch %$ VDC-1 %$ %VMAN-2-ACTIVATION_STATE: Successfully activated virtual service 'guestshell+'
```

*To verify the Guest Shell details, use the ```show guestshell detail``` command. The following shows the output of the command:*

```
switch# show guestshell detail
Virtual service guestshell+ detail
  State                 : Activated
  Package information
    Name                : rootfs_puppet
    Path                : usb2:/rootfs_puppet
    Application
      Name              : GuestShell
      Installed version : 2.3(0.0)
      Description       : Exported GuestShell: 20170613T173648Z
    Signing
      Key type          : Unsigned
      Method            : Unknown
    Licensing
      Name              : None
      Version           : None
```

*The Guest Shell has access to the Linux network interfaces used to represent the management and data ports of the switch. You can use the typical Linux methods and utilities like ```ifconfig``` and ```ethtool``` to collect counters or ```tcpdump``` to capture packets. The following example shows the output of the ```ifconfig``` command for an interface:*

```
[admin@guestshell ~]$ ifconfig Eth1-47
Eth1-47: flags=4098<BROADCAST,MULTICAST>  mtu 1500
        ether 38:90:a5:8d:2a:4d  txqueuelen 100  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

*When you place an interface into a VRF instance in the Cisco NX-OS CLI, the Linux network interface moves into a network namespace for that VRF. You can see the namespaces at* ***/var/run/netns.*** *The ```chvrf``` and ```vrfinfo``` utilities are provided for running in a different namespace and getting information about which namespace or VRF a process is running in.*

*The following output shows the example of the namespaces:*

```
[admin@guestshell ~]$ ls -al /var/run/netns
total 2
drwxrwxrwx 2 root root   80 Jan  2 17:03 .
drwxr-xr-x 9 root root 1024 Mar 22 11:34 ..
-r-------- 1 root root    0 Jan  2 17:03 default
-r-------- 1 root root    0 Jan  2 17:03 management
```

*When you are in a default namespace, for example, you can see all interfaces that are configured in the default VRF:*

```
[admin@guestshell ~]$ ifconfig | grep Eth1
Eth1-49: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
Eth1-50: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
Eth1-51: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
Eth1-52: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
```

*When you change the namespace, for example to management, you can see that the interfaces are no longer visible:*

```
[admin@guestshell ~]$ chvrf management
[admin@guestshell ~]$ ifconfig | grep Eth1
[admin@guestshell ~]$ ifconfig
eth1: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.1  netmask 255.255.255.0  broadcast 192.168.1.255
        ether 38:90:a5:8d:2a:46  txqueuelen 1000  (Ethernet)
        RX packets 3591060  bytes 270145826 (257.6 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 113579  bytes 27484538 (26.2 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 16436
        inet 127.0.0.1  netmask 255.255.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 0  (Local Loopback)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

*By default, the resources for the Guest Shell have a small impact on resources available for normal switch operations. If the network-admin requires additional resources for the Guest Shell, the ```guestshell resize {cpu | memory | rootfs}``` command changes these limits:*

```
switch# guestshell resize cpu 8
Note: System CPU share will be resized on Guest shell enable
```

*The CPU limit is the percentage of the system compute capacity that tasks running within the Guest Shell receive when contention with other compute loads occurs in the system. When there is no contention for CPU resources, the tasks within the Guest Shell are unlimited.*

*Note: A Guest Shell reboot is required after changing the resource allocations. You can accomplish this action with the ```guestshell reboot``` command.*

## Cisco NX-OS Model-Driven Programmability

*Automation is dramatically changing how users manage data center networks. The model-driven programmability of the Cisco NX-OS device allows you to automate the configuration and control of the device.*

*Data modeling provides a programmatic and standards-based method of writing configurations to the network device, replacing the process of manual configuration. Data models are written in a standard, industry-defined language. Although configuration using a CLI may be more human-friendly, automating the configuration using data models results in better scalability.*

*The Cisco NX-OS device supports the Yet Another Next Generation (YANG) data modeling language. You can use the YANG data modeling language to describe the configuration and operational data, remote procedure calls, and notifications for network devices.*

*Cisco NX-OS supports three standards-based programmable interfaces for operations on the data model: NETCONF, RESTCONF, and gRPC.*

![Model-Driven Programmability](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/model_driven_programmability.png)

*Model-driven configuration consists of the following main components:*

- ***Models:*** *Data models provide a structured, well-defined base that facilitates programmatic interaction with Cisco NX-OS network devices. Cisco NX-OS provides a comprehensive number of YANG models that allow you to manage the rich feature set available on the network device. The list of supported models includes native, OpenConfig, and IETF models. In addition, YANG provides a modeling language optimized for network devices and has a growing number of tools and utilities. OpenConfig and IETF are vendor-agnostic models that abstract the detailed configuration across operating systems and platforms.*

- ***Transport:*** *The two transport types that are used in the model-driven configuration are SSH and HTTP(S). Both provide the required security and flexibility level.*

- ***Encoding:*** *The separation of encodings from the choice of model and protocol provides additional flexibility. You can encode data in JavaScript Object Notation (JSON), XML, or Google Protocol Buffers (GPB) format. While some transports are currently tied to specific encodings, the programmability infrastructure is designed to support different encodings of the same data model if the transport protocol supports it. As an example, NETCONF uses XML encoding.*

- ***Protocols:*** *Model-driven programmability separates the models from the choice of protocol, which provides a high degree of flexibility. You can control the network device that is using NETCONF, RESTCONF, or gRPC. Your protocol choice will ultimately result from your networking, programming, and automation background, plus the available tooling.*

## Management Information Tree

*In model-driven architectures, software maintains a complete, explicit representation of the administrative and operational state of the system (the model).*

*In the Cisco NX-API-REST framework, configuration and state information of the switch is stored in a hierarchical tree structure. This tree is known as the management information tree (MIT) and is accessible through the API. You can make changes on a single object or an object subtree. Each node in the MIT represents a managed object or group of objects. These objects are organized in a hierarchical way, creating logical object containers, as shown in this figure.*

![management information tree (MIT)](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/management_information_tree.png)

*NX-API-REST uses an information-model-based architecture in which the model describes all the information that a management process can control. Object instances are referred to as managed objects (MOs). Every managed object in the system has a unique distinguished name (DN). This approach allows the object to be referred to globally.*

*The URL format is represented as follows:*

- ***System:*** *System identifier; an IP address or DNS-resolvable hostname​.*

- ***mo|class:*** *Specifies whether the operation will be for an MO or class.​*

- ***DN:*** *Specifies the unique distinguished name of the targeted managed object.​*

- ***className:*** *Specifies the name of the targeted class.​*

- ***Method:*** *Optional indication of the method being invoked on the object; applies only to POST requests​.*

- ***json|xml:*** *Defines the encoding format of the HTML body.​*

- ***Options:*** *Specify additional parameters (optional).​*

## YANG Data Modeling Language Overview

*You can use data models to enforce data consistency and validity. Rules govern data model structures (including the way you can insert, modify, access, or delete information) and who is able to manipulate the data model. These rules ensure that data is maintained in a known, valid state.*

*Data models represent the complete state of the network platform at any time. You can implement and use recovery features such as backups and snapshots that allow you to validate configuration changes and roll them back if necessary.*

*Data models are* ***extensible;*** *they can grow and adapt to accommodate additions or changes to features and elements, provided you observe any rules governing the structure of the data model.*

*Data models are* ***flexible;*** *once you choose a model structure, you can use it to encode more than one model simultaneously to meet the needs of multiple administrative audiences.*

![Data Models](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/data_models.png)

*Cisco Nexus 9000 Series NX-OS supports both open YANG models and native YANG models:*

- *Native data models provide most configuration and operational coverage.*

- *Open models are mapped to native data models.*

- *Departures from open models are specified as deviation modules.*

*A Cisco native YANG model is defined in the YANG data-modeling language but is specific to Cisco NX-OS. An open YANG model has various standards bodies and industry consortia: for example, the IEEE YANG model, IETF YANG model, and OpenConfig YANG model. OpenConfig is an informal working group of network operators who aim to move networks toward a more dynamic, programmable infrastructure. They promote software-defined networking principles such as declarative configuration and model-driven management and operations.*

*OpenConfig is compiling a consistent set of vendor-neutral OpenConfig YANG data models based on actual operational needs from use cases and requirements from multiple network operators. Compared with IEEE and IEFT YANG models, the OpenConfig YANG model has more defined models. It also imports some existing IEEE and IETF YANG models into its models. For example, the “openconfig-interfaces” model imports the “ietf-interfaces” model definition that the IETF defined.*

*You can use YANG to describe configuration and operational data, remote procedure calls (RPCs), and notifications for network devices.*

*YANG models the hierarchical organization of data as a tree in which each node has a name and either a value or a set of child nodes. YANG provides clear and concise descriptions of the nodes and the interaction between them.*

*Note: The OpenConfig YANG data models are published here: [github.com/openconfig/public/tree/master/release](https://github.com/openconfig/public/tree/master/release).*

*Please note that the OpenConfig YANG data models are updated frequently, with the latest revision number at this GitHub directory. Each vendor may not support the latest revision of the OpenConfig model. Because the OpenConfig model is vendor-neutral, the models are the least-common denominators among vendors. The number of OpenConfig models is much fewer than the number of native models. For a more complete set of feature support, and for support of specific Cisco NX-OS Software features, Cisco recommends using a native YANG model with Cisco NX-OS.*

*For Cisco Nexus 9000 Series Switches, beginning with Cisco Nexus NX-OS 7.0(3)I6(2), a Cisco native YANG model is included in the Cisco NX-OS image. It installs automatically when the image loads. However, OpenConfig YANG models are not included in the Cisco NX-OS image by default. You must download corresponding OpenConfig YANG Red Hat Package Manager (RPM) packages from the Cisco Artifactory and install them on the switch. Cisco NX-OS release-specific directories organize the OpenConfig YANG model RPM packages. They support specific revisions of the OpenConfig model that is defined by the OpenConfig consortium.*

*Note: Ensure that you are downloading the correct RPM packages from the corresponding Cisco NX-OS release directory: [devhub.cisco.com/artifactory/open-nxos-agents](https://devhub.cisco.com/artifactory/open-nxos-agents). This site requires a Cisco.com login.*

*Cisco NX-OS supports the YANG data modeling language, an open-source standard that is defined in RFC 6020.*

*Note: For more information about YANG, see the YANG RFC document here: [tools.ietf.org/html/rfc6020](https://tools.ietf.org/html/rfc6020).*

![Data Models 2](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/data_models2.png)

*You can implement data models by using numerous data representation and storage formats, including arrays, linked lists, stacks, and graphs (such as hierarchical trees). The hierarchical tree is very efficient in representing repetitive and hierarchical data and is typically associated with routing or switching platform configurations. Therefore, it is the most common data model format in use for networking platforms.*

*The nodes in tree-based data models can have parents, children, or both. The root of the tree has child nodes but no parent. Leafs have parents but no children, and nodes have both. In many data model implementations, there are potentially one or more trees, each containing information about some major group or important division of information pertaining to a modeled object.*

*Data models enable you to easily structure, group, and replicate data to represent information that relates to network devices, features, and solutions.*

![Data Models 3](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/data_models3.png)

*The example in the figure represents a data model of network interfaces:*

- *A root node that is described by the category “interfaces”*

- *Child nodes for various interface types and discrete interfaces*

- *Leafs containing information that pertains to specific object instances (interfaces), including configuration and operational state*

*Cisco Nexus 9000 Series NX-OS supports both open YANG models and native YANG models.*

## XML

*The API calls on Cisco Nexus devices can use the XML or JSON format.*

*XML is a text-based format for describing data. It is a widely used formats for sharing data between computers, people, or computers and people. The specification is provided by the World Wide Web Consortium (W3C).*

*The main characteristics of XML:*

- *XML documents use a self-described, simple syntax.*

- *The basic XML building block is an element that a tag defines.*

- *Each element has a beginning and an ending tag.*

- *Elements can be nested inside the other elements.*

- *The outermost element is the root element.*

- *Each element can contain attributes.*

*Tags are not defined by the XML standard. The author of the XML document chooses those tags and their names.*

*XML is very similar to HTML, but it is not a replacement. XML is designed to transport and store data, with a focus on what the data is. HTML is designed to display data, with a focus on how the data looks. HTML is about displaying information, while XML is about carrying information.*

*The following snippet shows an example of the XML document:*

```
<?xml version="1.0" encoding="UTF-8" ?>
 <root>
     <interfaceEntity>
         <children>
             <l1PhysIf>
                 <attributes>
                     <id>eth1/2</id>
                     <mode>trunk</mode>
                     <trunkVlans>15-20</trunkVlans>
                 </attributes>
             </l1PhysIf>
         </children>
     </interfaceEntity>
 </root>
```

*The example shows how to configure interface Ethernet 1/2 in trunk mode with the allowed VLANs 15–20.*

## JSON

*JSON is a lightweight format that you can use for data interchanging. It is an alternative to XML and is often the preferred format because the format is more lightweight.*

*The main characteristics of JSON:*

- *JSON was first defined in RFC 4627.*

- *It is a text-based format.*

- *It is language-independent.*

- *It allows nested elements to provide hierarchy.*

- *The elements can be objects, arrays, or key-value pairs.*

*The following snippet shows an example of a JSON document:*

```
{
  "interfaceEntity": {
    "children": [
      {
        "l1PhysIf": {
          "attributes": {
            "id": "eth1/2",
            "mode": "trunk",
            "trunkVlans": "15-20"
          }
        }
      }
    ]
  }
}
```

## YAML

*Yet Another Markup Language (YAML) is a data serialization language for all programming languages. It is human-friendly and commonly used for configuration files. YAML uses scope and begins each entry on its own line.*

- *The following snippet shows an example of the YAML document:*

```
interfaceEntity:
  children:
    - l1PhysIf:
        attributes:
          id: eth1/2
          mode: trunk
          trunkVlans: 15-20
```

*The example shows how to configure interface Ethernet 1/2 in trunk mode with the allowed VLANs 15–20.*

## NETCONF

*NETCONF is a configuration management protocol for communicating with network devices, retrieving operational data, and both setting and reading configuration data. Operational data includes interface statistics, memory utilization, errors, and others. The configuration data refers to how particular interfaces, routing protocols, and other features are enabled and provisioned.*

*The NETCONF protocol uses RPCs for communication. The data payload is encoded within XML for NETCONF RPC calls. NETCONF uses a client-server model, where the data transmits to the device over a secure, connection-oriented protocol. Secure Shell (SSH) is an example of this usage. Server response is also encoded in XML. The key part of this mechanism is the request. Both the request and the response are fully described in an agreed-upon communication model, and both parties recognize the syntax they are exchanging.*

*NETCONF provides you with operations such as get, get-config, edit-config, copy-config, and delete-config to read or manipulate data that are stored on devices.*

*A few steps occur during a NETCONF session; they are summarized as follows:*

1. *The client first connects to the server’s NETCONF SSH subsystem.*

2. *After the client connects to the server (network device) and establishes a connection, the server sends a hello and includes all its supported NETCONF capabilities.*

3. *When the server sends its hello, the client must return a hello with its supported capabilities. The client can respond with all the capabilities the server supports (assuming the client does, too), or just with the bare minimum to perform edits and gets.*

4. *Once the client sends its capabilities, it can then send NETCONF requests. When a request is received via NETCONF, the request converts into an abstract message object. That message object distributes to the underlying model infrastructure based on the namespace in the request. Using the namespace, the appropriate model is selected, and the request is passed to it for processing. The model infrastructure executes the request (read or write) on the device datastore.*

5. *The server processes the client’s request and responds with the configuration as expected.*

![NETCONF](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/NETCONF.png)

*NETCONF utilizes multiple configuration data stores (including candidate, running, and startup). This attribute is one of the most unique in NETCONF, though a device does not have to implement this feature to “support” the protocol.*

*NETCONF utilizes a candidate configuration that is simply a configuration with all proposed changes that apply in an uncommitted state. It is the equivalent of entering CLI commands and having them not take effect right away. You would then “commit” all the changes as a single transaction. When you make an API call configuring multiple objects and one fails, the entire transaction fails, and you do not end up with a partial configuration. Once committed, you would see them in the running configuration.*

## REST

*Representational State Transfer (REST) is an architectural style that abstracts architectural elements within a distributed hypermedia system. REST ignores the details of component implementation and protocol syntax. It focuses on the roles of components, the constraints upon their interaction with other components, and their interpretation of significant data elements. REST has emerged as a predominant web API design model.*

*REST-style architectures conventionally consist of clients and servers. Clients initiate requests to servers. Servers process requests and return appropriate responses. Requests and responses are built around the transfer of representations of resources. A resource can essentially be any coherent and meaningful concept that may be addressed, such as device configurations, devices, interfaces and protocols states. A representation of a resource is typically a document that captures the current or intended state of a resource.*

![REST](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/REST.png)

*The client begins sending requests when the client is ready to make the transition to a new state. While one or more requests are outstanding, the client is in transition. The representation of each application state contains links that may be used the next time that the client chooses to initiate a new state transition.*

*REST is intended to evoke an image of how a well-designed web application behaves. Presented with a network of web pages (a virtual-state machine), the user progresses through an application by selecting links (state transitions). The result is the next page (representing the next state of the application) being transferred to the user and rendered for their use.*

## RESTCONF

*RESTCONF, in the simplest terms, adds a REST API to NETCONF. It uses the HTTP POST, PUT, PATCH, and DELETE methods to edit data resources represented by YANG data models. These basic edit operations allow a RESTCONF client to alter the running configuration.*

![RESTCONF](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/RESTCONF.png)

*RESTCONF is not intended to replace NETCONF but rather to provide an HTTP interface that follows REST principles and is compatible with the NETCONF datastore model. RESTCONF provides a simplified interface that follows REST-like principles running on top of HTTP or HTTPS transport, making RESTCONF an attractive choice for application developers.*

*RESTCONF combines the HTTP protocol simplicity with the predictability and automation potential of a schema-driven API. It helps support a common, REST-based programming model for network programming in general. This model aligns with the wider trend in infrastructure programming to support REST APIs.*

## gNMI

*The Google Remote Procedure Call (gRPC) Network Management Interface (gNMI) protocol is an RPC-based network management interface that Google created. The gNMI works on top of the gRPC messaging protocol, which acts as a transport protocol.*

*The gNMI protocol is a unified management protocol for configuration management and streaming telemetry. While the IETF specifies NETCONF and RESTCONF, the gNMI specification is openly available at the OpenConfig repository.*

![gNMI](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/gNMI.png)

*The following gRPC operations describe all the necessary processes that define the work of gNMI:*

- ***gNMI CapabilitiesRequest:*** *This operation gives a gNMI client information from the switches about the gNMI versions that it uses and the data models and encodings it supports. It is up to the server (the switch in this case) to decide which YANG models and encodings it supports and the protocol version to use.*

- ***gNMI GetRequest:*** *When retrieving information from a gNMI server, you have two options: Get and Subscribe. GetRequest is most often used when retrieving a small amount of data. The data that it returns* ***(GetResponse)*** *is usually in the form of a snapshot.* ***SubscribeRequest*** *is used for retrieving larger amounts of data.*

- ***gNMI SetRequest:*** *Use gNMI SetRequest to update, replace, and delete configurations. It consists of an ordered set of edit operations. This procedure is atomic, which means that if any steps fail in operation or validation, no operations are applied. The SetResponse typically returns a list of responses, one per operation requested.*

- ***gNMI SubscribeRequest:*** *Use SubscribeRequest for applications such as telemetry or for larger queries of data. In the case of telemetry with gNMI, the subscriber (client) specifies a frequency of delivery, which could be one of the following:*

1. ***ONCE:*** *The data returns immediately and only once for all specified paths.*

2. ***POLL:*** *The data returns from the device when polled with the current values for all specified paths.*

3. ***STREAM:*** *The data returns continuously. It could either be in the* ***SAMPLE*** *mode (where data returns periodically in accordance with a sample interval) or in the* ***ON_CHANGE*** *mode (where the data returns upon a change in values).*

## Application Programming Interfaces

*An API is a set of requirements that governs how one application can use another application. An API exposes internal functions to the outside world and allows external applications to use functionality within the application. In practice, an API is a set of calls that transmit from one application to another. The other application recognizes and accepts these calls as commands. In this way, any outside solution that obeys the API framework of a service can control that service.*

*APIs are not new and are used often in systems where data must exchange between applications. For example, almost every website communicates with the back end through an API. What is new is how you can use APIs to control and manage devices and systems in your data center. You can use the API to make a request, and the device responds to you. You can use applications to manage devices in your data center instead of manually adjusting and tweaking various parts your infrastructure repeatedly.*

![API](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/API.png)

*Applications can use APIs exposed on devices, but often a controller is between applications and devices. Applications need only to interact with the controller that will take care of specific device configuration. Controller-based networking solutions centralize management of many devices in one single point of administration. This high-level view enables you to use abstractions and simplifications when provisioning new services.*

# Cisco Nexus API

*You connect to the CLI and execute commands to manage a Cisco Nexus device. Besides the CLI, Cisco Nexus devices allow you to use an API, which improves the accessibility of these commands by making them available outside the switch through HTTP or HTTPS.*

*These characteristics describe the Cisco Nexus API (NX-API):*

- *Provides programmatic access to the switches over HTTP or HTTPS.*

- *Allows you to remotely issue commands and receive responses.*

- *It supports show commands and configurations.*

- *It supports the following formats:*

1. *XML*

2. *JSON*

3. *JSON Remote Procedure Call (JSON-RPC)*

- *Security is integrated in the NX-API.*

*NX-API uses HTTP or HTTPS as its transport. Commands are encoded into the HTTP POST body. The NX-API back end uses the Nginx HTTP server.*

*If you use HTTPS, all communication to the device is encrypted. NX-API is integrated into the authentication system on the device. Users must have appropriate accounts to access the device through NX-API, which uses HTTP basic authentication. All requests must contain the username and password in the HTTP header. NX-API provides a session-based cookie, ```nxapi_auth```, when users successfully authenticate for the first time. Along with the session cookie, the username and password are included in all subsequent NX-API requests that transmit to the device.*

*The username and password are used with the session cookie to bypass the task of performing the entire authentication process again. If the session cookie is not included with subsequent requests, another session cookie is required and is provided by the authentication process. Avoiding multiple authentications helps reduce the devices’ workload. An ```nxapi_auth``` cookie expires in 600 seconds (10 minutes). This value is a fixed and cannot be adjusted.*

## Using NX-API

*By default, NX-API is disabled. Enable NX-API with the feature manager CLI command on the device.*

*Before you can use the NX-API, you must enable the API:*

- *Use the ```feature nxapi``` command to enable the NX-API:*

```
switch# configure terminal
switch(config)# feature nxapi
```

- *By default, the HTTP is enabled on port 80, HTTPS is disabled.*

- *Use the ```nxapi http``` command to change the HTTP port:*

```
switch(config)# nxapi http port 8080
```

- *Use the ```nxapi https``` command to enable HTTPS and set the listening port for HTTPS:*

```
switch(config)# nxapi https port 8443
```

*When you enable HTTPS, the switch generates the self-signed certificate. You can install your own certificate by using the ```nxapi certificate``` command. To verify the status of the NX-API, use the ```show nxapi``` command:*

```
switch# show nxapi

NX-API:       Enabled         Sandbox:      Enabled
HTTP Port:    8080            HTTPS Port:   8443

Certificate Information:
    Issuer:   /C=US/ST=CA/L=San Jose/O=Cisco Systems Inc./OU=nsstg/CN=nxos
    Expires:  Dec 19 07:53:19 2028 GMT
    Content:  -----BEGIN CERTIFICATE-----
<... Output omitted ...>
-----END CERTIFICATE-----
```

*When you send a request to a switch, follow these guidelines:*

- *Send an NX-API request to ```http://<ip-address-of-switch>/ins```.*

- *The HTTP request must contain the content-type field in the header:*

1. ***application/json-rpc*** *for JSON-RPC requests*

2. ***text/json*** *or* ***text/xml*** *for JSON or XML proprietary formats*

- *For authentication, use either the username and password or cookie:*

1. *Add the authorization header with an encoded username and password to the HTTP request.*

2. *Add the session cookie, which is received after first authentication.*

## Developer Sandbox

*The NX-API sandbox is a web-based user interface that you use to enter the commands, command type, and output type for the Cisco Nexus devices using HTTP or HTTPS.*

*The main features of the developer sandbox:*

- *Web GUI for user to try out and get easy guidance on Cisco NX-API.*

- *Commands are typed in to see an autogenerated request in a user-determined format (JSON-RPC, JSON, or XML).*

- *User can send requests and receive responses.*

- *Option to autogenerate a sample Python script for a user to easily adapt and send the specific commands.*

- *Autogenerated requests can be copied and pasted in the user script.*

- *It is enabled by default; if it is disabled, you can enable it with the ```nxapi sandbox``` command.*

*Verify if the sandbox is enabled or disabled with the ```show nxapi``` command.*

```
switch# show nxapi

NX-API:       Enabled         Sandbox:      Enabled
HTTP Port:    80              HTTPS Port:   Disabled
```

*Use a browser to access the NX-API sandbox.*

*Open a browser and enter ```http://[switch-mgmt-ip]``` to launch the NX-API sandbox.*

![NX-API](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/NX-API.png)

*In the NX-API sandbox, specify the commands, command type, and output type in the top pane. Click the* ***POST Request*** *button above the left pane to post the request. Brief descriptions of the request elements will display below the left pane.*

*After the request is posted, the output response displays in the right pane.*

*You can generate a Python code for each request posted through the sandbox. To generate Python code, click the* ***Python*** *button in the* ***Request*** *pane.*

*The example shows how to retrieve interface data from the switch.*

![NX-API 2](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/NX-API2.png)

*The example shows the ```show interface brief``` command. The Developer sandbox executes that command on the switch and returns the structured data. You can see the response in the right pane.*

*The example shows how to configure a switch using the Developer sandbox.*

![NX-API 3](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/NX-API3.png)

*In this example, two commands transmit to the switch. The input tag in the left pane shows that commands are separated by semicolon. In the right pane, you can see that you get a response for each command that you send to the switch. You can check the interfaces in the CLI, and you can see that commands apply successfully to the switch configuration.*

```
switch# show ip interface brief
IP Interface Status for VRF "default"(1)
Interface            IP Address      Interface Status
Lo0                  1.1.1.1         protocol-up/link-up/admin-up
```

## Cisco NX-OS Model-Driven Programmability

*When a request is received, whether via NETCONF, RESTCONF, or gRPC, the request is converted into an abstract message object. That message object is distributed to the underlying model infrastructure based on the namespace in the request. Using the namespace, the appropriate model is selected and the request is passed to it for processing.*

*The model infrastructure executes the request (read or write) on the device datastore. The results are returned to the agent of origin for response transmission back to the requesting client.*

![NX-API 4](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/NX-API4.png)

*Agents provide an interface between the device and clients. They specify the transport, the protocol, and the encoding of the communications with the device.*

*The device configuration is described in a YANG model that is called a device model. The device model is manifested in the model infrastructure as another model component with the device namespace.*

*A common model is another kind of model component that contains within its elements, YANG paths to the equivalent device model elements. These equivalent device model elements are used to read and write device model data in the device YANG context.*

*Note: Supported YANG models for each Cisco NX-OS release are provided at [devhub.cisco.com/artifactory/open-nxos-agents](https://devhub.cisco.com/artifactory/open-nxos-agents). This site requires a Cisco.com login.*

*You can choose from many open-source tools to automate the management of the Cisco Nexus switches. The following open-source tools give you the power to automate your network in a programmatic manner:*

- ***NCCLIENT:*** *This Python library facilitates client-side scripting and application development around the NETCONF protocol.*

- ***PYANG:*** *This YANG validator and code generator is written in Python. You can use it to validate YANG modules for correctness, transform YANG modules into other formats, and write plug-ins to generate code from the modules.*

- ***YDK:*** *The YANG Development Kit (YDK) is an open-source tool that Cisco developed to facilitate network programmability using data models. The YDK can generate APIs in various programming languages using YANG models.*

## Open Cisco NX-OS Programmability

*Open Cisco NX-OS is based on Wind River Linux 5. By using a standard and unmodified Linux foundation, it is possible to run any standard Linux-based application without changes or wrapper libraries. Users can use their common Linux server management tools and workflows to install their custom-developed Linux-based applications. They can also install other standard open-source programs and have them function out of the box on the Cisco Nexus switch.*

*Integrating common third-party configuration management agents like Puppet and Chef and telemetry applications such as ganglia, Splunk, collector, and Nagios on the switch is straightforward.*

![Open Cisco NX-OS](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/open_cisco_NX-OS.png)

*The most important Linux capabilities of Open Cisco NX-OS include the following:*

- ***Kernel 3.4:*** *At the core of Open Cisco NX-OS is a 64-bit Linux kernel based on version 3.4. This kernel provides a balance of features, maturity, and stability. It serves as a solid foundation for programmability and Linux-based management of a Cisco Nexus switch.*

- ***Kernel Stack:*** *Open Cisco NX-OS uses the native Linux networking stack instead of a custom-built user-space stack (NetStack) used in prior versions of Cisco NX-OS. Cisco Nexus switch interfaces, including physical, port-channel, vPC, virtual LAN (VLAN), and other logical interfaces, are mapped to the kernel as standard Linux netdevs. VRFs on the switch map to common Linux namespaces.*

- ***Open Package Management:*** *Open Cisco NX-OS uses standard package management tools, such as RPM and Yum for software management. You can use the same tools for Open Cisco NX-OS process-patching or installing external or custom-developed programs onto the switch.*

- ***Container Support:*** *Open Cisco NX-OS supports running Linux Containers (LXCs) directly on the platform and provides access to CentOS 7-based Guest Shell. This functionality allows customers and third-party application developers to add custom functionality directly on the device in a secure, isolated environment.*

*In addition, Open Cisco NX-OS continues to uphold some Linux best-practice capabilities that have always been part of Cisco NX-OS:*

- ***Modularity:*** *Modules are loaded into the kernel only when needed. Modules can be loaded and unloaded on demand.*

- ***Fault Isolation:*** *Provides complete process isolation for Cisco NX-OS features, services, and user application processes.*

- ***Resiliency:*** *Graceful restart or initialization of processes following unexpected exit conditions (segfault and panic).*

## Cisco NX-SDK

*Cisco NX-SDK provides a simple, flexible, modernized, powerful tool for off-the-box third-party custom application development. You gain access to Cisco Nexus infrastructure functionalities. When run inside the Cisco Nexus switches, they allow the custom applications to run natively just like any native Cisco Nexus applications. It is appropriate for do-it-yourself automation to develop custom applications to fit your needs and decouple application development from Cisco Nexus releases.*

*Cisco NX-SDK provides an abstraction or plug-in library layer that decouples the application from the underlying infrastructure. Therefore, it is easy and simple to change infrastructure without affecting the applications. Cisco NX-SDK is being used for developing native Cisco Applications also.*

![NX-SDK](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/NX-SDK.png)

*Cisco NX-SDK offers various functionalities like the ability to generate custom:*

- *CLIs*

- *Syslogs*

- *Event and error manager*

- *High availability*

- *Route manager*

- *Streaming telemetry*

- *Other custom applications*

*Cisco NX-SDK is built with the C++ language. You can also use the Python or Go programming languages for application development with Cisco NX-SDK.*

# Python

*The Cisco NX-OS CLI allows you only to execute the commands. There are no options to perform any loops or any conditions. Similar to some ```show``` command outputs, you cannot manipulate the result that you get back. By using the scripts, you can modify the output of the ```show``` command and implement your logic.*

*One of the most popular, easy to learn, and powerful programming languages is Python.*

*Python has efficient high-level data structures, and it has a simple but effective approach to object-oriented programming. Python’s elegant syntax and dynamic typing, together with its interpreted nature, makes it an ideal language for scripting and rapid application development in many areas on most platforms.*

*The two main releases of Python in use are 2.7 and 3.7. Beginning with Cisco NX-OS Release 9.3(5), Python 3 is now supported. Python 2.7 is currently supported in the transition stage.*

*Note: Python 2.7 is End of Support. Future releases of Cisco NX-OS Software will deprecate Python 2.7 support. Cisco recommends that for new scripts, use Python 3.7 instead. Type the ```python3``` command to use the new shell.*

*If you run Python 2.7 on the switch using the ```python``` command, you will see the following notification:*

```
switch# python
 
Warning: Python 2.7 is End of Support, and future NXOS software will deprecate
python 2.7 support. It is recommended for new scripts to use 'python3' instead.
Type "python3" to use the new shell. 
 
Python 2.7.11 (default, Jun 4 2024, 09:48:24) 
[GCC 4.6.3] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

*The Cisco Nexus 9000 Series switches support Python v2.7.11 and v3.7.3 in both interactive and noninteractive (script) modes and are available in the Guest Shell.*

*Note: For a list of Cisco Nexus switches that support Python scripting, refer to the [Platform Support for Programmability Features](https://www.cisco.com/c/en/us/td/docs/switches/datacenter/nexus9000/sw/93x/progammability/guide/b-cisco-nexus-9000-series-nx-os-programmability-guide-93x/b-cisco-nexus-9000-series-nx-os-programmability-guide-93x_chapter_0100101.html#id_110421).*

*You can use the Python SDK to automate compute infrastructure tasks in Cisco UCS. Since fast application deployment is important in agile data centers, you can use this SDK to develop tools that can provision Cisco UCS quickly. Hence, you can automate the configuration of Cisco Computing System Manager policies, resource pools, and resource profiles configuration, among others.*

*The Python interpreter and the extensive standard library are freely available in a source or binary form for all major platforms from the Python website: [www.python.org](http://www.python.org/).*

*The Python scripting capability enables you to perform tasks such as the following:*

- *Run a script to verify configuration on switch bootup.*

- *Back up a configuration.*

- *Perform proactive congestion management by monitoring and responding to buffer utilization characteristics.*

- *Integrate with Power-On Auto Provisioning (POAP) or Embedded Event Manager (EEM) modules.*

- *Perform a job at a specific time interval (such as Port Auto Description).*

- *Access the CLI to perform various tasks.*

*There are no configuration requirements to use Python on Cisco Nexus devices. The Cisco NX-OS CLI Python feature is enabled by default and can be used without any preconditions.*

*The Cisco Nexus devices support Python in both interactive and noninteractive (script) modes. You can invoke Python 2.7 in interactive mode in the CLI by entering the ```python``` command and invoke Python 3.7 entering the ```python3``` command. A Python script can run in noninteractive mode by providing the Python script name as an argument to the ```python``` or ```python3``` command. The ```bootflash:scripts``` directory is the default directory. Thus, you must store all scripts in the ```bootflash:scripts``` directory or in a subdirectory of it. Python is well suited for usage during troubleshooting, general usage, event-based actions, and other DevOps operations.*

*In addition, the Python programming language can use APIs that can execute CLI commands. These APIs are available from the Python CLI module.*

## Using Python with Cisco NX-OS Devices

*The Cisco NX-OS has a native Python command interpreter that runs either on Cisco NX-OS at the CLI prompt or in Bash on the Linux user prompt. The Cisco Python package in Cisco NX-OS enables access to many core network device modules. Examples include interfaces, VLANs, VRF instances, access control lists (ACLs), and routes. You can display the details of the Cisco Python package by entering the ```help()``` command, as indicated in this output:*

```
switch# >>> help()
Welcome to Python 2.7! This is the online help utility. 
If this is your first time using Python, you should definitely
check out the tutorial on the Internet at 
http://docs.python.org/tutorial/. 
Enter the name of any module, keyword, or topic to get help on writing 
Python programs and using Python modules. To quit this help utility and 
return to the interpreter, just type "quit".
```

*To obtain additional information about the classes and methods in a module, you can run the ```help``` command for a specific module. For example, ```help(cisco.interface)``` displays the properties of the ```cisco.interface``` module.*

*The following is an example of how to display information on the Cisco Nexus 9000 Series Switch about a Cisco Python package for Python 3:*

```
switch# python3
Python 3.7.3 (default, Nov 20 2019, 14:38:01)
[GCC 5.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
switch# >>> import cisco
switch# >>> help(cisco)
Help on package cisco:

NAME
    cisco

FILE
    /isan/python/scripts/cisco/__init__.py

PACKAGE CONTENTS
    acl
    bgp
    buffer_depth_monitor
    check_port_discards
    cisco_secret
    feature
    historys
    interface
    ipaddress
    key
    line_parser
    mac_address_table
    md5sum
    nxcli
    nxos_cli
    ospf
    routemap
    routes
    section_parser
    ssh
    system
    tacacs
    transfer
    vlan
    vrf

CLASSES
     builtins.dict(builtins.object)
     cisco.history.History
     builtins.object
     cisco.cisco_secret.CiscoSecret
     cisco.interface.Interface
     cisco.key.Key
```

## Interactive Mode

*Interactive mode is like normal Python. The ```python``` CLI command on the Cisco Nexus devices gives you the Python interpreter mode, while the prompt indicates that you have entered the Python interpreter mode. Thus, you can execute the commands according to your needs. You can also execute normal Python scripting language commands in the interpreter if needed. To exit from Python interpreter mode, use the ```exit``` command that switches back to the switch prompt.*

*This example shows how to invoke Python 3 from the CLI.*

```
switch# python3
Python 3.7.3 (default, Nov 20 2019, 14:38:01) 
[GCC 5.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from cli import *
>>> import json
>>> out=json.loads(clid('show version'))
>>> for k in out.keys():
... print("%30s - %s" % (k,out[k]))
...
header_str - Cisco Nexus Operating System (NX-OS) Software
TAC support: http://www.cisco.com/tac
Copyright (C) 2002-2020, Cisco and/or its affiliates.
All rights reserved.
<output omitted>
```

## Noninteractive Mode

*In noninteractive mode, you can run scripts mainly from the switch prompt itself. It is unnecessary to enter the Python interpreter mode.*

*You must place Python scripts under the bootflash or volatile scheme with the following features:*

- *A maximum of 32 command-line arguments for the Python script are allowed with the ```Python``` CLI command.*

- *By default, the scripts are stored in the ```bootflash:scripts``` directory.*

```
switch# show file bootflash:scripts/deltaCounters.py. <-- bootflash:scripts directory
#!/isan/bin/python3          <-- Invoke Python 3 to run deltaCounters.py script
from cli import *
import sys, time
ifName = sys.argv[1]
delay = float(sys.argv[2])
count = int(sys.argv[3])
cmd = 'show interface ' + ifName + ' counters'
out = json.loads(clid(cmd))
rxuc = int(out['TABLE_rx_counters']['ROW_rx_counters'][0]['eth_inucast'])
txuc = int(out['TABLE_tx_counters']['ROW_tx_counters'][0]['eth_outucast'])
print ('row rx_ucast tx_ucast')
print ('=========================================================')
print (' %8d %8d' % (rxuc, txuc))
print ('=========================================================')
i = 0
while (i < count):
    time.sleep(delay)
    out = json.loads(clid(cmd))
    rxucNew = int(out['TABLE_rx_counters']['ROW_rx_counters'][0]['eth_inucast'])
    txucNew = int(out['TABLE_tx_counters']['ROW_tx_counters'][0]['eth_outucast'])
    i += 1
    print ('%-3d %8d %8d' % (i, rxucNew - rxuc, txucNew - txuc))
```

**Additional Notes:**

This script is a **Cisco NX-OS Python helper** that measures how interface counters change over time. You pass it **three arguments:** interface name, delay (seconds), and how many samples to take; it then runs ```show interface <if> counters``` repeatedly via the NX-OS ```clid()``` API and parses the JSON output. It grabs the **initial RX/TX unicast counters**, then sleeps, re-queries, and prints the **delta** (difference) from the original values each time—basically a poor man’s traffic trend tool.

The key idea is: *not absolute counters,* but **how much traffic flowed during each interval**, which is way more useful for spotting bursts or verifying traffic paths.

*You can execute the Python script from the CLI by using the ```python3 <filename>``` command. You can use ```?``` to find available scripts.*

```
switch# python3 bootflash:scripts/deltaCounters.py mgmt0 1 5
row rx_ucast rx_mcast rx_bcast tx_ucast tx_mcast tx_bcast
=========================================================
      291     8233     1767      185       57        2
=========================================================
1          1        4        1        1        0        0
2          2        5        1        2        0        0
3          3        9        1        3        0        0
4          4       12        1        4        0        0
5          5       17        1        5        0        0
switch#
```

## Python Scripting and Aliasing

*Python is a valuable tool for scripting CLI inputs and printing CLI outputs from the Cisco NX-OS interface. Use these outputs to concatenate multiple commands and save time collecting information for troubleshooting or making numerous CLI changes to switches. As shown in the figure, Python can also save time to help aid in deployments and troubleshooting tasks.*

![Python Scripting and Aliasing](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/python_troubleshooting.png)

*You can alias the Python script using the ```alias``` command in CLI configuration mode. For example, the command ```cli alias name resolve source script.py``` aliases the Python script ```script.py``` to the alias ```resolve```. Just typing the single word ```resolve``` will cause the script to run. Also, you can call a Python script or program from inside EEM using the ```action number cli source script.py``` syntax. Use it, for example, to trigger several scripts to give you some show outputs automatically if an event such as syslog or a call home event occurs.*

## Cisco UCS Python SDK

*Cisco UCS can use the Python SDK to allow task automation in Cisco UCS.*

*Cisco UCS Python SDK is a Python module that helps automate all aspects of Cisco UCS management, including server, network, storage, and hypervisor management. Cisco UCS Python SDK works on the Cisco UCS Manager Management Information Tree (MIT). It performs create, modify, or delete operations on managed objects (MOs) in the tree. MOs are abstractions of Cisco UCS resources, such as fabric interconnects, chassis, blades, and rack-mounted servers.*

*The Cisco UCS Python SDK provides APIs to enable create, read, update, delete (CRUD) operations:*

- ***C****reate an object: ```add_mo```*

- ***R****etrieve an object: ```query_dn,query_classid,query_dns,query_classids```*

- ***U****pdate an object: ```set_mo```*

- ***D****elete an object: ```delete_mo```*

*You can combine these APIs in a transaction (All or None). The ```commit_mo``` commits the changes using the APIs. All these methods are invoked on an ```UcsHandle``` instance, which is referred as ```handle``` in the following examples.*

```
from ucsmsdk.ucshandle import UcsHandle

# Create a connection handle

 handle = UcsHandle("192.168.1.1", "admin", "password")

# Login to the server

handle.login()

# Logout from the server

 handle.logout()
```

*You can download the Cisco UCS Python SDK from the UCSM SDK section on GitHub, [github.com/CiscoUcs/ucsmsdk](https://github.com/CiscoUcs/ucsmsdk).*

## Cisco ACI Toolkit

*The Cisco ACI Toolkit exposes a small subset of the Cisco ACI object model. It introduces the Cisco ACI concepts and allows you to get the most common workflows operating as quickly as possible.*

**My Note:** The ACI Toolkit is a set of Python libraries designed to help users configure and manage the Cisco Application Centric Infrastructure (ACI) controller, known as APIC. It simplifies the use of the REST API, making it easier for users to automate tasks and manage network configurations.

![ACI Toolkit](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/ACI_toolkit.png)

*Note: The Cisco Application Centric Infrastructure (Cisco ACI) Toolkit documentation is available with a quick search here: [datacenter.github.io/acitoolkit](https://datacenter.github.io/acitoolkit). You can find a support forum on Cisco.com Communities.*

*The main goals of the Cisco ACI Toolkit are as follows:*

- *Ease the learning curve that is associated with learning and using Cisco ACI and the Cisco Application Policy Infrastructure Controller (APIC) REST APIs*

- *Allow you to get started doing something useful quickly*

- *Address the most common use cases*

- *Provide examples and sample scripts on which you can build*

*Note: You can find the latest versions of the Cisco ACI Toolkit code, examples, and applications at the GitHub web page: [github.com/datacenter/acitoolkit](https://github.com/datacenter/acitoolkit).*

## Cobra SDK and WebArya Overview

*The Cobra SDK and APIC REST to Python Adapter (Arya) are complementary tools. Cobra is an autogenerated Python API that covers the entire Cisco ACI object model. Cobra is like the API that the Cisco ACI Toolkit provides, but it is comprehensive because it provides access to all object types.*

*A consequence of the comprehensive and autogenerated nature of Cobra is that it is not consistently obvious which API you should use to create a given entity type. Arya, which is given a JSON or XML representation of an entity, will generate Cobra code with suitable APIs and class types.*

![Cobra SDK](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/cobra_sdk.png)

*Note: Cobra supports Python version 2.7 and later 2.x versions. Beginning in the APIC 4.2(3) release, Cobra supports Python version 3.6 and later 3.x versions.*

*The Cobra documentation is available at [cobra.readthedocs.io/en/latest/](https://cobra.readthedocs.io/en/latest/). Here you can also find the Cobra installation instructions. Cobra is based on a Python ```.whl``` file, which you download from your Cisco APIC server at [apic/cobra/_downloads/](https://apic/cobra/_downloads/), where “apic” is a domain name or IP address of your APIC. Cisco APIC will provide packages (```whl``` files) for installation under Python 2 or Python 3.*

# Ansible

*Integration of automation and orchestration software with the Cisco platforms enables you to perform programming and automation activities on the infrastructure so it can be aligned with application and business needs.*

- *Most automation tools do the following:*

1. *Apply IT tools to network management.*

2. *Manage multiple devices and the automation around it.*

3. *Perform repeatable and granular tasks.*

- *Some tools require you to install an agent on the device.*

*Ansible is an open-source software platform for configuring and managing compute and switching infrastructure that uses a concept of playbooks, which are scripts that run against devices in your environment. Ansible features a state-driven resource model that describes the desired state of computer systems and services. You can use it to automate the configuration of your company’s compute and switching resources in an agentless manner.*

*Ansible has the following features, which are typical for orchestration software with agentless architecture:*

- *Uses a push-based model.*

- *Scripts run on the management server, connect to the managed device, and execute tasks.*

- *No timer; control lies with the management server.*

*Use Ansible for configuration management, deployment, and orchestration of Cisco UCS servers, storage, fabric, hyperconverged infrastructure and converged infrastructure, and Cisco Nexus switches.*

*By default, Ansible requires Secure Shell Protocol (SSH) and Python support on the target node, but you can also easily extend Ansible to use any API. The connection setting ```ansible_connection: ansible.netcommon.network_cli``` is used in the SSH protocol, while the connection setting ```ansible_connection: ansible.netcommon.httpapi``` is used for the NX-API connection in the playbook.*

*Note: The connection setting ```ansible_connection: local``` has been deprecated in Ansible 2.9.*

*Ansible modules make API calls against the NX-API to gather real-time state data and to make configuration changes on Cisco Nexus devices. Configure NX-API on a Cisco Nexus device to allow Ansible modules to work properly. It does not require the use of a dedicated server. In fact, you can install Ansible on many machines and use them to simultaneously automate any given environment.*

*When a server runs a playbook, Ansible connects to devices according to the playbook and carries out the instructions from that file. The key technical concepts are the following:*

- ***Playbooks:*** *Specify a list of tasks that run in sequence across one or more hosts. Each task can also run multiple times with a variable taking a different value. Playbooks use the YAML format, a simple markup language, which, unlike XML, is very easily readable.*

- ***Inventory:*** *Represents information about the hosts. It describes the groups to which a host belongs and the properties of those groups and hosts. You can hierarchically organize groups.*

- ***Templates:*** *Enable you to generate configuration files from values set in various inventory properties, allowing you to store one template in the source control that applies to many different environments.*

- ***Roles:*** *Provide a way to encapsulate common tasks and properties for reuse. If you find yourself writing the same tasks in multiple playbooks, you can turn them into roles for reusability.*

## Using Ansible with Cisco NX-OS Devices

*This playbook has the following fields:*

- *The ```name:``` field defines the playbook name.*

- *The ```hosts: all``` field specifies the hosts that this playbook should run again. The keyword ```all``` indicates that it should include all devices that are defined in the hosts file in the Ansible directory.*

- *The ```connection: local``` field defines the connection will be made from the Ansible host. As previously indicated, you should take advantage of the ```network_cli``` connection method instead of ```local```, which is available since Ansible version 2.5.*

- *The ```tasks:``` field specifies the task that will run on the devices.*

```
- name: feature testing
    hosts: all
    connection: local
    gather_facts: no

    tasks:
# Ensure ospf is enabled
    - nxos_feature: feature=ospf
   state=enabled host={{ inventory_hostname}}
```

*For example, when you execute this playbook for a Cisco Nexus 9000 Series Switch, it performs the following set of tasks:*

- *The nxos-ansible Ansible library converts the modules to Cisco CLI.*

- *The Cisco CLIs transmit to the switch via NX-API using pycsco Python module, a Python module that simplifies working with Cisco NX-OS devices.*

- *No need for Python on the switch—simply enable the NX-API feature.*

*You can find examples for Cisco NX-OS and Ansible integration in the Ansible-NXOS section on GitHub, [github.com/datacenter/Ansible-NXOS](https://github.com/datacenter/Ansible-NXOS).*

## Ansible Modules

*Ansible provides many modules that are specific to Cisco device. The screenshot shows collections in the Cisco Namespace at Ansible.*

![Ansible](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/ansible.png)

# HashiCorp Terraform

*HashiCorp Terraform enables infrastructure automation for provisioning, compliance, and management of any cloud and data center.*

*HashiCorp Terraform is an Infrastructure as Code (IaC) tool that lets you define both cloud and on-premises resources in human-readable configuration files that you can version, reuse, and share. You can then use a consistent workflow to provision and manage your infrastructure throughout its lifecycle. Terraform can manage low-level components like compute, storage, and networking resources, as well as high-level components like Domain Name System (DNS) entries and software as a service (SaaS) features.*

*Terraform is for infrastructure management. It allows you to define and manage IaC, which can be versioned, tested, and reviewed. With Terraform, you can declaratively define the desired state of your infrastructure, making it possible to achieve the infrastructure design you want.*

*Terraform is a multiplatform IaC tool written in the Go programming language that compiles into binary files. Terraform is compatible with various operating systems, including Windows, macOS, and many Linux distributions. It can make API calls on your behalf to one or more providers, such as Cisco, Amazon Web Services (AWS), Azure, Google Cloud, Digital Ocean, and others.*

*HashiCorp Terraform provides a comprehensive set of commands, from initialization and configuration to planning, applying, and destroying infrastructure resources in a systematic and repeatable manner.*

![HashiCorp Terraform](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/terraform.png)

- *The ```terraform init``` command initializes a working directory containing Terraform configuration files. It is the first command that you should run after writing a new Terraform configuration or cloning an existing one from version control. It is safe to run this command multiple times.*

- *The ```terraform plan``` command creates an execution plan that lets you preview the changes that Terraform plans to make to your infrastructure. By default, when Terraform creates a plan, it does the following:*

1. *Reads the current state of any existing remote objects to help ensure that the Terraform state is up to date.*

2. *Compares the current configuration to the prior state and notes any differences.*

3. *Proposes a set of change actions that should, if applied, make the remote objects match the configuration.*

- *The ```terraform apply``` command executes the actions proposed in a Terraform plan.*

- *The ```terraform destroy``` command destroys all remote objects managed by a particular Terraform configuration.*

- *The ```terraform show``` command is used to provide human-readable output from a state or plan file. You can use it to inspect a plan to help ensure that the operations work as expected or to inspect the current state as Terraform sees it.*

*The Terraform Workflow is shown in the following figure:*

![Terraform 2](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/terraform2.png)

*As you begin to build your workflow, you will find that it follows a pattern. You start by using ```terraform init``` to configure and download all the necessary providers. After that, you will work on creating Terraform files to ensure that you have the correct settings. Next, you will execute a Terraform plan that will analyze and identify any errors and provide an overview of what will happen when it executes. Finally, you will apply the plan, and it will execute against the destination object.*

## Terraform Components

*The building blocks of Terraform enable you to manage your infrastructure in a modular, scalable, and repeatable way. Components include providers, resources, variables, data sources, and modules, which are the core constructs that define the infrastructure as code in Terraform. By recognizing each of these components, you will be able to use Terraform to manage your infrastructure with greater ease and efficiency, while also enjoying the benefits of automation and consistency that it offers. The core Terraform components work together to enable IaC management. Terraform is a tool that enables infrastructure engineers to define and manage infrastructure as code.*

*The following Terraform components are important:*

- *Providers are plug-ins that connect Terraform to the infrastructure you want to manage.*

	*The Terraform Registry is the main directory of publicly available Terraform providers. The registry hosts providers for most major infrastructure platforms. It includes documentation for a wide range of providers developed by HashiCorp, third-party vendors, and the Terraform community. The Terraform registry is available here: [registry.terraform.io/browse/providers](https://registry.terraform.io/browse/providers)*
	
- *Resources represent infrastructure components that you want to manage; they are constructed of a type, name, and block containing the configuration of the resource.*

- *You use variables to create reusable code and data sources enable Terraform to retrieve data from an external system.*

- *Use modules to organize and encapsulate Terraform code.*

- *When you start learning to use HashiCorp Terraform, you might begin with one configuration file containing all your infrastructure as code. As you learn more, you may start to share and collaborate on those configuration files with peers or teams. Eventually, multiple team members start creating, sharing, and collaborating on the same configurations.*

- *How do you scale your Terraform configuration as your team grows?*

	*You can break the Terraform configuration into modules to reduce dependencies between components.*
	
*The formats of Terraform project files are shown in the following figure:*

![Terraform 3](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/terraform3.png)

*Code in the HashiCorp Terraform Language (HCL) is stored in plain text files with the ```.tf``` file extension. There is also a JSON-based variant of HCL that is named with the ```.tf.json``` file extension.*

*Files containing Terraform code are often called configuration files. Terraform configuration files define the desired state of the infrastructure, including resources, variables, and providers. They use a simple, declarative syntax that is both human-readable and machine-parsable.*

# Lab: Configure Cisco NX-OS with APIs

*Automation and programmability capabilities in the data center components (computing, networking, storage, and services resources) enable end-to-end automated management. A modern network device (whether it is a switch, router, or service appliance) must support a wide range of automation features and provide robust APIs for external tools, both off-the-shelf and custom-built. These tools allow automatic provisioning of network resources, bandwidth allocation, and latency guarantees to support network service level agreements (SLAs) and monitoring of the network for performance and compliance needs.*

*The Cisco NX-OS API allows programmatic access on Cisco Nexus switches and offers the complete configuration and management capabilities of the CLI through APIs. You can instruct Cisco Nexus switches to publish the output of the API calls in either XML or JSON format. This comprehensive, easy-to-use API enables rapid deployment on the Cisco Nexus switches.*

*Built for continuous availability in mission-critical data center environments, Cisco NX-OS has set the standard for resiliency, extensibility, efficiency, and virtualization. Now, programmability and automation have been added to that list, too.*

## View XML and JSON Output Using the CLI

The Cisco Nexus 9000 Series CLI allows you to display command output in multiple formats: *human-readable, XML,* or *JSON.* These formats are particularly useful when integrating CLI output into automation scripts or API calls.

*Key Concepts:*

- **Multiple markup formats:** CLI output can be rendered in XML or JSON in addition to the standard CLI text.

- **Choice of format:** Often depends on the automation tool or personal preference, as most modern tools support both XML and JSON.

- **Automation-ready:** Structured output allows easier parsing for scripts or API consumption.

**1. Establish SSH session to the Nexus 9000 Switch:**

- From the Student VM, launch PuTTY.

- Connect to **N9K-A** using:

```
Username: admin
Password: 1234QWer
```

**2. Check the standard CLI output:**

- Run the show ```clock command``` to see the current time:

```
N9K-A# show clock
21:27:12.498 UTC Tue Apr 22 2025
Warning: No NTP peer/server configured. Time may be out of sync.
Time source is NTP
N9K-A#
```

- This output gives you the human-readable snapshot of the system clock, including potential warnings (like missing NTP configuration).

**3. View XML-formatted output:**

- Pipe the command through ```xml```:

```
N9K-A# show clock | xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<nf:rpc-reply xmlns="http://www.cisco.com/nxos:1.0:syscli" xmlns:nf="urn:ietf:params:xml:ns:netconf:base:1.0">
  <nf:data>
    <show>
      <clock>
        <__XML__OPT_Cmd_some_cmd_detail>
          <__XML__OPT_Cmd_some_cmd___readonly__>
            <__readonly__>
              <simple_time>21:27:41.568 UTC Tue Apr 22 2025</simple_time>
              <time_source>NTP</time_source>
            </__readonly__>
          </__XML__OPT_Cmd_some_cmd___readonly__>
        </__XML__OPT_Cmd_some_cmd_detail>
      </clock>
    </show>
  </nf:data>
</nf:rpc-reply>
]]>]]>
N9K-A#
```

*Key points about XML:*

- Combines *human-readable* and *machine-readable* structure.

- Markup elements start with ```<…>``` and end with ```</…>``` or with ```&…;```.

- The content between tags is the actual data (e.g., ```simple_time``` and ```time_source```).

- Think of XML as a tree—nodes (tags) are branches, and leaves are the actual values.

**4. View JSON-formatted output:**

- Pipe the command through ```json```:

```
N9K-A# show clock | json
{"simple_time": "21:32:34.630 UTC Tue Apr 22 2025", "time_source": "NTP"}
N9K-A#
```

*Key points about JSON:*

- Derived from JavaScript but language-independent.

- Concise, human-readable, and widely supported in automation tools.

- Data is stored in key-value pairs (```"key": "value"```).

- JSON is like a dictionary or a map—easy to grab and parse in scripts.

*Takeaways:*

- Use **XML** when a structured, hierarchical format is needed.

- Use **JSON** when you want a lightweight, concise format for scripting or API integration.

- Both formats allow automation tools to consume CLI outputs efficiently.

## Use NETCONF to Interface with Cisco NX-OS

NETCONF is a *configuration management protocol* that allows network devices to be managed, retrieve configuration data, and upload or modify configuration data in a structured way. Cisco NX-OS implements NETCONF using *XML-based RPC messages.*

**NETCONF Basics:**

- Uses XML as the data encoding format.

- Operates over secure, connection-oriented protocols (typically SSH).

- No REST interface support; everything is RPC-driven.

**XMLin Tool:**

- Converts CLI commands into NETCONF RPC format.

- Supports *show commands, EXEC commands, and configuration commands.*

- Example NETCONF operations: ```<get>```, ```<edit-config>```, ```<close-session>```, ```<kill-session>```, ```<exec-command>```.

- Prepares command output for automation or API consumption.

*Restriction highlights:*

- ```<edit-config>``` cannot include *show commands.*

- Each ```<get-config>``` request can contain only *one show command.*

**1. Generate NETCONF XML code for a CLI command:**

- Pipe a CLI command through ```xmlin``` to see the NETCONF RPC version of it:

```
N9K-A# show clock | xmlin
<?xml version="1.0"?>
<nf:rpc xmlns:nf="urn:ietf:params:xml:ns:netconf:base:1.0" xmlns="http://www.cisco.com/nxos:10.5.1.:syscli" message-id="1">
  <nf:get>
    <nf:filter type="subtree">
      <show>
        <clock/>
      </show>
    </nf:filter>
  </nf:get>
</nf:rpc>
]]>

% Success
N9K-A#
```

- The XML code here is what a NETCONF client would send to the device to get the same information as the CLI command. Think of ```xmlin``` as a translator between CLI and NETCONF.

**2. Enter xmlin tool execution mode:**

- Start xmlin mode:

```
N9K-A# xmlin
******************************************
Loading the xmlin tool. Please be patient.
******************************************
...
N9K-A(xmlin)#
```

- Note: Takes up to 30 seconds to load.

- Now, any show command you enter here returns *NETCONF XML-formatted output.*

**3. Generate XML for show clock inside xmlin mode:**

```
N9K-A(xmlin)# show clock
<?xml version="1.0"?>
<nf:rpc xmlns:nf="urn:ietf:params:xml:ns:netconf:base:1.0" xmlns="http://www.cisco.com/nxos:10.5.1.:syscli" message-id="1">
  <nf:get>
    <nf:filter type="subtree">
      <show>
        <clock/>
      </show>
    </nf:filter>
  </nf:get>
</nf:rpc>
]]>

% Success
N9K-A(xmlin)# exit
******************************************
****** Exited from the xmlin tool. *******
******************************************
N9K-A#
```

**Things Worth Remembering:**

- ```xmlin``` is your *bridge* from CLI commands to NETCONF RPCs.

- ```<get>``` = show commands, ```<edit-config>``` = config commands. *Never mix show commands into ```<edit-config>```.*

- NETCONF is *XML-only;* JSON is not used for protocol communication.

- Multiple commands can be bundled in a single ```<edit-config>``` but not in ```<get>```—always one show command per ```<get>```.

- ```xmlin``` helps you *learn NETCONF syntax without writing XML manually.*

## Enable the NX-API in Cisco NX-OS and Use the NX-API Sandbox to Configure a Cisco Nexus 9000 Series Switch

The *NX-API* allows you to execute traditional CLI commands and receive responses in *XML* or *JSON* format via HTTP/HTTPS. This enables automated network management without logging directly into the CLI.

**Key Concepts:**

*NX-API CLI vs REST::*

- NX-API CLI: Encapsulates NX-OS commands, supports Bash commands, responds in XML or JSON.

- NX-API REST: Manipulates configurations via RESTful calls.

- Both serviced by a backend *nginx web server.*

*HTTPS and Authentication:*

- Uses HTTPS to encrypt traffic.

- Generates a *session cookie* (```nxapi_authv) for authentication reuse.

- Cookie expires after *600 seconds (10 minutes).*

*NX-API vs NETCONF:*

- NX-API XML does *not map directly* to NETCONF XMLIN.

- NX-API supports show, config, and Bash commands; NETCONF is strictly XML-RPC.

**1. Enable NX-API:**

```
N9K-A# configure
Enter configuration commands, one per line. End with CNTL/Z.
N9K-A(config)# feature nxapi
```

**2. Verify NX-API transport:**

```
N9K-A(config)# show nxapi
nxapi enabled
NXAPI timeout 10
NXAPI cmd timeout 300
HTTPS Listen on port 443
Certificate Information:
    Issuer:   issuer=C = US, ST = CA, L = San Jose, O = Cisco Systems Inc., OU = dcnxos, CN = nxos
    Expires:  Apr 23 21:37:08 2025 GMT
N9K-A(config)# exit
```

- Displays *HTTPS port, timeouts, and SSL certificate* for API communication.

**3. Access the NX-API Sandbox:**

- Open a browser on the Student VM: ```https://10.1.1.101```.

- Accept the certificate warning, log in as *admin / 1234QWer*, and save the password.

- The Sandbox allows you to execute NX-API calls and view responses in XML or JSON.

**4. Verify management interface configuration:**

```
N9K-A# show running-config interface mgmt0

interface mgmt0
  vrf member management
  ip address 10.1.1.101/24
N9K-A#
```

**5. Create VLANs via CLI:**

```
N9K-A# configure
N9K-A(config)# vlan 200
N9K-A(config-vlan)# end
N9K-A# show vlan brief
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Eth1/1, Eth1/2, ...
200  VLAN0200                         active
N9K-A#
```

**6. Verify VLANs via NX-API Sandbox (XML, cli_show_ascii):**

```
Post pane command: show vlan
Message format: XML
Command type: cli_show_ascii
```

- Response mirrors CLI output.

- NX-API converts ASCII CLI commands into XML/JSON requests automatically.

**7. Configure VLANs via NX-API Sandbox (cli_conf):**

- Example: VLAN 100

```
Post pane command: vlan 100
Command type: cli_conf
Message format: XML
```

- Response code ```200``` = success.

- Test invalid command: ```vlanf 150``` → Response code ```400``` indicates error.

**8. Verify VLAN via NX-API Sandbox:**

```
Post pane command: show vlan id 100
Command type: cli_show_ascii
```

- Output should match CLI output.

**9. Create and configure VLAN 150 via NX-API Sandbox:**

```
Commands:
show vlan id 150
configure terminal
vlan 150
name NXAPI
end
show vlan id 150
Command type: cli_conf
Message format: XML
```

- Success responses show VLAN 150 active, confirming configuration.

**Things Worth Remembering:**

- *NX-API = CLI in a box:* You can run NX-OS commands remotely using HTTP/S.

- *Session cookie* (```nxapi_auth```) avoids repeated authentication.

- *Multiple commands* can be sent in a single API call using the Post pane.

- *Response codes matter:* ```200``` = success, ```400``` = CLI error.

- Sandbox is excellent for *learning NX-API syntax* and generating XML/JSON for scripts.

- For automation, scripts using NX-API over HTTP/S are *faster and safer* than manual CLI.

## Use a REST Client to Interface with a Cisco Nexus 9000 Series Switch

NX-API REST is the next evolution beyond the sandbox: instead of clicking buttons on-box, you now send *real HTTP requests from an external tool.* This is what automation actually looks like in the wild.

**Big Idea:**

- *NX-API REST = model-driven, RESTful access* to NX-OS

- Third-party tools (like *Postman*) talk to the switch over the network

- The *NX-API Sandbox becomes your request generator*

- Postman becomes your *external automation client*

**Task Flow Overview:**

1. Generate XML requests using *NX-API Sandbox*

2. Send those requests externally using *Postman*

3. Observe real HTTP-based automation behavior

4. Modify device configuration remotely

**Step 1: Prepare a GET Request in Postman**

- Open *Postman* on the Student VM

- Click *+ New* → create a new request tab

- Select *GET* initially (you’ll switch to POST shortly)

**Step 2: Generate XML Request via NX-API Sandbox**

In the NX-API Sandbox, prepare a ```show vlan brief``` command and copy the generated XML request.

Example request:

```
<?xml version="1.0"?>
<ins_api>
  <version>1.0</version>
  <type>cli_show</type>
  <chunk>0</chunk>
  <sid>sid</sid>
  <input>show vlan brief</input>
  <output_format>xml</output_format>
</ins_api>
```

This XML is the *actual payload* that automation tools send — not some abstract example.

**Step 3: Configure Postman Request**

*Request Settings:*

- URL:

```
https://10.1.1.101/ins
```

- Method: POST

- **Important:** ```/ins``` is mandatory — without it, NX-API will not respond

*Authorization:*

- Tab: *Authorization*

- Type: *Basic Auth*

- Credentials: ```admin /1234QWer```

**Step 4: Send XML Payload**

- Go to *Body* tab

- Select *raw*

- Paste the XML request copied from the Sandbox

- *Disable SSL verification* (certificate is self-signed)

- Click *Send*

First response may fail due to SSL — disable certificate checking when prompted.

*Result:*

- Response matches *NX-API Sandbox output*

Key difference:

- Request originated from an *external application*

- This mirrors real-world automation workflows

**Step 5: Create VLAN 300 via Postman**

*Generate XML in NX-API Sandbox:*

- Command type: ```cli_conf```

- Command:

```
vlan 300
```

Example:

```
<?xml version="1.0"?>
<ins_api>
  <version>1.0</version>
  <type>cli_conf</type>
  <chunk>0</chunk>
  <sid>sid</sid>
  <input>vlan 300</input>
  <output_format>xml</output_format>
</ins_api>
```

*Execute in Postman:*

- Paste XML into *Body → raw*

- Click *Send*

- Response code ```200``` confirms success

**Step 6: Verify VLAN 300**

- Use *Postman History*

- Re-run the previous ```show vlan brief``` request

- Confirm VLAN 300 appears in the output

Key realization: verification uses the *same* API path as configuration — no CLI needed.

**Things Worth Remembering:**

- *POST + /ins* is non-negotiable for NX-API REST

- NX-API Sandbox = request generator, not automation

- Postman = proof your automation works off-box

- XML payloads are *transportable artifacts*

- If it works in Postman, it works in Python, Ansible, CI/CD

- SSL errors are expected in labs — don’t panic

## Run Python Interactively in the Switch CLI

**Goal:**

- This lab shows *Python living inside the switch,* not talking to it remotely.

- You’re no longer automating *toward* NX-OS — you’re automating *from within it.*

**1. Verify the Interface Does Not Exist (Baseline Check):**

Always confirm the starting state.

```
N9K-A# show interface loopback 1
                               ^
Invalid range at '^' marker.
N9K-A#
```

- NX-OS throws an error → *Loopback1 does not exist yet*

- This is expected and confirms a clean slate.

**2. Enter Python Mode from NX-OS:**

Drop directly into the embedded Python interpreter:

```
N9K-A# python
Python 3.8.18 (default, Jul 15 2024, 10:11:58)
[GCC 5.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

Key points:

- This is *real Python,* not a toy shell.

- You’re still operating *inside* the switch OS context.

**3. Explore Python Help (Orientation Step):**

Enter interactive help:

```
>>> help()
```

You’ll see the standard Python help utility. This step is mostly about confidence-building: nothing exotic is hiding here.

**4. Discover Available Modules (Important One: ```cli```):**

From the help prompt:

```
help> modules
```

Example output (trimmed, but preserved in spirit):

```
InterfaceSysCMD     requests           resource
OpenSSL             mem_monitor         SmartTelemetry
...
<output omitted>
```

*Critical insight:*

- The ```cli``` *module* is what lets Python speak native NX-OS CLI.

- This is the magic glue between scripting and configuration.

Exit help mode:

```
help> quit
```

**5. Import the NX-OS CLI API into Python:**

Back at the Python prompt:

```
>>> from cli import *
>>>
```

- This exposes functions like ```cli()```, ```clip()```, and ```clid()```

- Think of this as unlocking the switch’s throat chakra

**6. Create and Enable Loopback 1 via Python:**

Run configuration commands *as a single CLI string:*

```
>>> cli('configure terminal ; interface loopback 1 ; no shutdown')
''
>>>
```

*Important rules:*

- *Spaces before and after semicolons are mandatory*

- The empty string (```''```) means the command executed successfully

- You just configured NX-OS *without touching config mode manually*

**7. Verify the Interface Using clip() (Readable Output):**

Show the interface state:

```
>>> clip('show interface loopback 1')
loopback1 is up
admin state is up,
  Hardware: Loopback
  MTU 1500 bytes, BW 8000000 Kbit , DLY 5000 usec
  reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation LOOPBACK, medium is broadcast
  Auto-mdix is turned off
    0 packets input 0 bytes
    0 multicast frames 0 compressed
    0 input errors 0 frame 0 overrun 0 fifo
    0 packets output 0 bytes 0 underruns
    0 output errors 0 collisions 0 fifo
    0 out_carrier_errors
```

Note:

- ```clip()``` is like ```cli()```, but *formatted for human eyes*

- Ideal for verification, logging, and sanity checks

**8. List Connected Interfaces via Python:**

Filter for connected ports:

```
>>> clip('show interface stat | include connected')
mgmt0         --                 connected routed    full    1000    --
Eth1/1        --                 connected 1         full    1000    10g
Eth1/2        Connects to N9K-C  connected 1         full    1000    10g
Eth1/3        Connects to N9K-B  connected 1         full    1000    10g
Eth1/4        Connects to N9K-B  connected 1         full    1000    10g
Eth1/5        Connects to Server connected 1         full    1000    10g
Eth1/6        Connects to N9K-D  connected 1         full    1000    10g
Lo1           --                 connected routed    auto    auto    --
```

- Loopback1 now appears as *connected*

- Proof that Python-created config is fully native

**9. Final Interface Overview:**

Full brief status:

```
>>> clip('show interface brief')
```

Excerpt (important parts preserved):

```
Port   VRF          Status IP Address                              Speed    MTU
mgmt0  --           up     10.1.1.101                              1000    1500
...
Eth1/1          1       eth  access up      none                     1000(D)
...
Lo1             --      up     --                                    auto
```

- Loopback is up

- Physical and logical interfaces coexist cleanly

**10. Exit Python, Return to NX-OS CLI:**

```
>>> exit()
N9K-A#
```

You’re back — but now the switch remembers what Python whispered to it.

## Activity Verification

*In this discovery, you demonstrated how the CLI can translate commands and the command output into XML- or JSON-encoded data. You also learned how to use the NX-API RESTful interface via the CLI and GUI (the NX-API Sandbox). These approaches are most valuable from a learning perspective. To make automation more useful, use a web REST client such as Postman to configure Cisco NX-OS (although any web REST client is acceptable).*

*Realistically, even a web REST client is not that useful. Ultimately, a programming language such as Python, or configuration management tools such as Puppet, Chef (both use Ruby), or Ansible (based on Python), are better tools for automating Cisco Nexus devices in the data center.*

![Activity Verification](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/lab_programmability.png)

*XMPP and Data Management Engine (DME) were not demonstrated in this exercise.*

![Automation Table](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/automation_overview.png)

# Lab: Explore the Cisco UCS Manager XML API Management Information Tree

*API models are not only used by users that want to automate an API-enabled solution. Vendors also use the API calls to create user front ends for their systems. One example is Cisco UCS Manager.*

*API systems use API models that are predetermined command formats and are accepted by the API implementation. This model is used in API calls and usually includes command keywords and their expected values.*

*The values provided in an API call can apply to different subsystems of a target system. These subsystems are usually referred to by a distinguished name (```DN```). Distinguished names are unique names for objects (or subsystems). Often, they are formatted in a hierarchical fashion. In Cisco UCS Manager, this hierarchy is provided by a forward slash ( ```/``` ), but various solutions can use different approaches.*

*Whenever an API call is made, the variables defined by the model are defined in a call for an object defined by its DN. The API call is made by using a transfer protocol such as HTTP. If that protocol is insecure, the contents of an API call transmit unencrypted and can be read by someone who captures the API call traveling to its destination through a network. Modern API implementations therefore usually disallow insecure transport protocols.*

## Demonstrate DN Queries with the Managed Object Browser

**Big Picture:**

- Cisco UCS is *entirely object-driven* — *everything* is a Managed Object (MO).

- Configuration isn’t “commands”, it’s *creating, modifying, and querying objects.*

- The MIT is the mental model you *must* internalize before XML / API work makes sense.

**1. Accessing the Managed Object Browser (Visore):**

This is your X-ray vision into UCS internals.

- Open browser → go to:

```
https://10.10.1.130/visore.html
```

- Log in: ```admin / 1234QWer```

- Ignore certificate warnings:

1. Chrome → *Advanced → Proceed*

2. Firefox → *Advanced → Add Exception → Confirm*

Visore lets you *browse the live object database* without writing any API code yet — perfect for learning structure.

**2. What the DME Actually Is (Demystified):**

Cisco buzzwords decoded:

- *DME (Data Management Engine)*

→ A distributed database running on the Fabric Interconnects

- It stores *every hardware component and configuration detail*

- When you use the API, you’re:

1. Reading objects from the DME

2. Writing objects into the DME

Nothing mystical — just a structured object store with rules.

**3. Managed Objects (MOs): The Core Concept**

- Every physical or logical component = *Managed Object*

1. Chassis

2. Blades

3. Adapters

4. Fans, PSUs (auto-created)

5. Policies (user-defined)

- Some MOs are *created by you*

- Some MOs are *created automatically by UCS*

Either way, they all live in the same hierarchy.

**4. The Management Information Tree (MIT):**

*This is the critical abstraction.*

- The MIT is a *hierarchical tree*

- The root is always:

```
sys
```

- Parent/child relationships define *containment*

- Each object has a *Distinguished Name (DN)*

Think filesystem paths — but for infrastructure.

**5. Distinguished Names (DNs) — The UCS GPS System:**

DNs answer two questions at once:

*1. What is this object?*

*2. Where does it live in the hierarchy?*

Filesystem analogy:

- ```/sys/chassis-1/blade-2/adaptor-1```

- Not files — *subordinate systems*

You never “guess” DNs. You *navigate the tree and discover them.*

**6. Example MIT Branch (Preserved as Sacred Text):**

```
Tree (topRoot):—————————————-Distinguished Name:
|——sys———————————––– (sys)
       |——chassis-1————————(sys/chassis-1) 
                |——blade-1————— (sys/chassis-1/blade-1) 
                         |——adaptor-1—– (sys/chassis-1/blade-1/adaptor-1) 
                |——blade-2————— (sys/chassis-1/blade-2) 
                         |——adaptor-1—– (sys/chassis-1/blade-2/adaptor-1) 
                         |——adaptor-2—– (sys/chassis-1/blade-2/adaptor-2) 
                |——blade-3————— (sys/chassis-1/blade-3) 
                         |——adaptor-1—– (sys/chassis-1/blade-3/adaptor-1) 
                         |——adaptor-2—– (sys/chassis-1/blade-3/adaptor-2) 
                |——blade-4————— (sys/chassis-1/blade-4) 
                         |——adaptor-1—– (sys/chassis-5/blade-4/adaptor-1)
```

Key observations:

- Each node = *one MO*

- Each DN is *globally unique*

- Hierarchy expresses *physical reality*

**7. Policies vs Hardware Objects (Subtle but Important):**

- *Hardware MOs* → represent physical things

- *Policy MOs* → define *behavior*

1. Boot policies

2. Power policies

3. Network policies

- APIs don’t “run commands”. They *create, update, or delete policy objects.*

## Object Naming in Cisco UCS (DNs vs RNs, properly untangled)

**Big idea (burn this in):**

- *Every Managed Object (MO) has a precise address*

- That address can be:

1. *Absolute* → Distinguished Name (DN)

2. *Relative* → Relative Name (RN)

- APIs don’t “guess” — they operate *exactly* on the object you name

**Distinguished Name (DN) — the full address**

- A DN *uniquely identifies one MO in the entire system*

- Structure:

```
DN = {RN}/{RN}/{RN}/{RN}/...
```

- Think: *absolute filesystem path*

Example:

```
<dn ="sys/chassis-1/blade-1/adaptor-1" />
```

What this really means:

- Start at ```sys``` (root)

- Go into ```chassis-1```

- Then ```blade-1```

- Then target *exactly* ```adaptor-1```

This DN tells the API *precisely* which object to read or modify.

**Special case: Rack-mount servers**

- No chassis/blade hierarchy

- Instead:

```
sys/rack-unit-<id>/...
```

- Important:

- ```rack-unit-<id>``` is *system-assigned*

- It is *not guaranteed to be rack-unit-1*

This trips people up constantly — *always discover*, never assume.

**Relative Name (RN) — local identity**

- An *RN identifies an object only within its parent*

- DNs are just *chains of RNs*

- Same RN can exist in multiple places — context matters

Example DN:

```
sys/chassis-1/blade-1/adaptor-1/host-eth-2
```

Broken into RNs (cleanly explained):

- topSystem MO

```
RN = "sys"
```

- equipmentChassis MO

```
RN = "chassis-<id>"
```

- computeBlade MO

```
RN = "blade-<slotId>"
```

- adaptorUnit MO

```
RN = "adaptor-<id>"
```

- adaptorHostEthIf MO

```
RN = "host-eth-<id>"
```

Each RN only makes sense *inside its parent object.*

**Using the Managed Object Browser (Visore) to query by DN:**

*Task: Inspect a specific MO*

- In Visore, enter this into *Class or DN* field:

```
sys/rack-unit-3/adaptor-1/ext-eth-1
```

- If you see:

```
No objects found at this level
```

- Wait a few minutes

- UCS may still be discovering hardware

What’s happening:

- Visore sends a query to the *DME*

- The DME returns *everything it knows* about that MO

- Scroll to inspect:

1. Attributes

2. Status

3. Operational data

**Viewing the actual XML query (very important):**

- Click *“Display XML of last query”*

- You’ll see something like:

```
<configResolveDn
  dn="<dn>"
  cookie="<real_cookie>"
  inHierarchical="false"/>
```

Why this matters:

- This is the *exact API call* UCS uses internally

- You are learning the *real* language of UCS Manager

**```inHierarchical``` — power tool with a warning label**

- ```inHierarchical="false"```

Return *only the specified MO*

- ```inHierarchical="true"```

Return the MO *plus all child objects*

**Burn-this-into-your-mind warning:**

- Using ```true``` high in the tree (like ```sys```)

- Can return *nearly the entire UCS configuration*

- Massive responses, slow queries, angry automation scripts

Use hierarchical queries surgically, not casually.

*Also:*

- DNs are absolute truth — APIs don’t work without them

- RNs are local names, not global identities

- Visore is your oracle: *discover first, automate second*

- UCS is a graph of objects, not a pile of commands

- Once DNs feel natural, UCS automation becomes boringly powerful

## Configure the XML String to Log in to Cisco UCS Manager

**Core idea (burn this in):**

- *UCS APIs are stateful:* you authenticate once, then reuse a session cookie

- That cookie is your *temporary identity* inside the UCS universe

- No cookie = no power

**Why authentication works this way:**

- API calls can *reconfigure nearly everything* in UCS

- Re-authenticating for every call would be inefficient and noisy

Instead:

- You authenticate once

- UCS returns an *authentication cookie*

- Cookie validity: *600 seconds (10 minutes)*

Think of it as a short-lived passport stamped by the Fabric Interconnect.

**Task: Authenticate via Postman**

*Open Postman:*

- From the Student VM desktop create a new request

- URL:

```
https://10.10.1.130/nuova
```

- Method: ```POST```

- This ```/nuova``` endpoint is *specifically* for UCS XML API requests

**XML login payload (raw body):**

```
<aaaLogin inName="admin" inPassword="1234QWer"/>
```

Important details:

- XML is *minimal by design*

- No wrapping tags, no verbosity

- UCS expects *exactly* this structure

**SSL warning (expected behavior):**

- UCS typically uses self-signed certificates

- If prompted: disable SSL certificate validation

- This is normal in labs and internal environments

**What success looks like:**

- HTTP Status:

```
200 OK
```

- In the response body:

1. Locate the ```outCookie``` attribute

2. This is a *47-character session token*

3. You must reuse this cookie in *all subsequent API calls*

If you don’t capture the cookie, the login was pointless.

**Things worth remembering:**

- ```/nuova``` is the front door to UCS XML APIs

- ```aaaLogin``` creates *session context*, not just authentication

- Cookies expire — automation scripts must refresh them

- Every future request quietly asks: *“Do you still have the cookie?”*

## Running an XML Query via Postman (Visore → Real API)

**Core idea (burn this in):**

- Visore shows you the truth

- Postman proves the truth works remotely

- Same API, different lenses

**Step 1: Discover the object in Visore**

Target object:

```
sys/user-ext/user-admin
```

What you’re doing:

- Asking UCS Manager for the *current state* of the ```user-admin``` object

- This is a *read-only verification* step

**Step 2: Extract the real XML query**

In Visore:

- Click *Display XML of last query*

- Select *all XML*

- Copy it to clipboard

Why this matters:

- Visore is not “magic”

- It’s literally generating *the same XML* you’d send via automation

**Step 3: Refresh your session cookie (important habit)**

In Postman:

- Click *Send* on your previous ```aaaLogin``` request

Why:

- Cookies expire after *600 seconds*

- This resets your timer and avoids silent failures later

Automation wisdom: *always refresh before a multi-step sequence*

**Step 4: Prepare the new API request**

- Right-click the login request tab

- Choose *Duplicate Tab*

Why:

- Keeps:

1. Same URL (```/nuova```)

2. Same method (```POST```)

3. Same SSL settings

- Reduces human error

**Step 5: Paste the Visore XML**

- Go to *Body → Text (raw)*

- Replace the login XML with the XML copied from Visore

You are now sending a *pure read query* directly to UCS Manager.

**Step 6: Execute and verify**

- Click *Send*

- Confirm:

```
Status: 200 OK
```

Compare:

- Visore response vs Postman response

What you’ll notice:

- Formatting differs

- Data values are *identical*

This is expected — and healthy.

**Why formatting differences don’t matter:**

- APIs care about *structure*, not presentation

- Tools may:

1. Indent differently

2. Reorder attributes

3. Collapse whitespace

- The underlying XML schema stays rigid

**Things worth remembering:**

- Visore is a *query discovery engine*

- Postman is a *transport mechanism*

- If it works in Visore, it will work over the network

- Cookies silently gate everything

## Capturing a UCSM Authorization Call with Wireshark (Why HTTPS Is Non-Negotiable)

**Core idea:**

- *APIs are just network traffic*

- If they’re not encrypted, *they betray you*

**Step 1: Log in to UCS Manager (baseline setup)**

Access UCS Manager:

- Browser →

```
https://10.10.1.130/
```

- Click *Launch UCS Manager*

- Log in: ```admin / 1234QWer```

- Accept the security warning (expected in lab environments)

**Step 2: Disable HTTPS redirection (danger zone)**

GUI navigation path:

- *Admin tab*

- Filters drop-down → *Communications Management*

- *Communications Services*

*Change setting:*

- *Redirect HTTP to HTTPS* → ```Disabled```

- Click *Save Changes*

- Confirm: *Yes → OK*

- Exit UCS Manager and log in again

*Why this matters:*

- UCS normally *forces* HTTPS

- You are temporarily removing that guardrail

**Step 3: Prepare the insecure API call in Postman**

*Body (raw XML):*

```
<aaaLogin inName="admin" inPassword="1234QWer"/>
```

- Ensure *raw* is selected in Body tab

- This is the same login call you used before — but now it’s vulnerable

**Step 4: Start packet capture in Wireshark**

Launch Wireshark and accept profile creation prompt if shown.

Capture setup:

- *Capture → Options*

- Interface: ```ens160```

- Click *Start*

Apply display filter:

```
ip.addr == 10.10.1.130
```

This narrows the noise to *only UCS traffic.*

**Step 5: Send the login over HTTP (the sin)**

In Postman:

- URL *must be HTTP:*

```
http://10.10.1.130/nuova
```

- Click *Send*

- Verify:

```
Status: 200 OK
```

At this moment, you’ve done something unspeakable on a real network.

**Step 6: Expose the credentials**

In Wireshark:

- Stop capture (red square)

- Locate:

```
POST /nuova
```

- Right-click → *Follow → TCP Stream*

What you’ll see:

- *Red text* → request (your XML)

- *Blue text* → response

- Username and password visible *in clear text*

**Things worth remembering:**

- HTTP APIs leak credentials instantly

- Wireshark doesn’t need skill — just opportunity

- XML APIs are *especially* readable when unencrypted

- Security defaults exist because humans override them

## Securely Creating an Organization in Cisco UCS Manager via XML API

**Why this matters (big picture):**

- Authentication cookies are *power tokens*

- If stolen over HTTP → full control for ~10 minutes

- Over HTTPS → useless to attackers

- This lab closes the loop from *exposure → containment*

**Step 1: Prepare the XML payload**

XML used to create a new organization:

```
<configConfMos
cookie="1609588043/dcfededd-ecbb-44ad-9acc-edd8f6b7afc5"
inHierarchical="false">
    <inConfigs> 
        <pair key="org-root/org-MIA">
            <orgOrg 
                descr="Miami" 
                name="MIA" 
                dn="org-root/org-MIA" 
                status="created" 
                sacl="addchild,del,mod"> 
            </orgOrg> 
        </pair>
    </inConfigs> 
</configConfMos>
```

What each important part actually means (Cisco soup, clarified):

- *configConfMos* → “configure managed objects” (write operation)

- *cookie* → your authentication session (valid 10 minutes)

- *inHierarchical="false"* → only act on this object, not children

- *org-root/org-MIA* → DN where the new org will live

- *status="created"* → tells UCSM this is a create operation

- *sacl* → permissions on the org object

This is not a script — it’s a *declarative state change.*

**Step 2: Harvest the cookie (intentionally unsafe origin)**

- From your *previous Wireshark capture*

- Locate the ```<aaaLogin>``` response

- Copy the *outCookie value only* (no quotes)

Yes — this cookie was obtained via insecure HTTP. That’s intentional: you’re proving *why* HTTPS matters.

**Step 3: Reset Wireshark for the secure run**

- Click the *blue fin* icon → *Restart capture*

- Choose *Continue without Saving*

- Apply filter again:

```
ip.addr == 10.10.1.130
```

**Step 4: Re-authenticate securely (HTTPS restored)**

In Postman:

- URL:

```
https://10.10.1.130/nuova
```

- Send login request again if needed

- Confirm:

```
Status: 200 OK
```

You are now back in the encrypted world.

**Step 5: Create the organization via Postman**

- *Duplicate Tab*

- Body → *raw*

- Paste your edited XML payload (with *your* cookie)

- Ensure:

1. Protocol: *HTTPS*

2. URL: ```https://10.10.1.130/nuova```

- Click *Send*

- Verify:

```
Status: 200 OK
```

**Step 6: Verify in Cisco UCS Manager**

GUI navigation:

- *Server tab*

- Filters drop-down → *Service Profiles*

- Confirm new organization:

```
MIA
```

If it’s there — the API worked. No CLI. No GUI clicks. Just intent.

**Step 7: Observe Wireshark**

- You *will* see traffic

- It will be labeled *TLSv1.2*

- You will *not* see:

1. XML

2. Cookies

3. Credentials

That’s what success looks like.

**Key takeaways:**

- Cookies = keys to the kingdom

- HTTPS turns intercepted traffic into noise

- APIs don’t care *who* you are — only what you present

- UCS XML API is brutally powerful and brutally honest

### Summary

*In this course, you learned the following about automating tools in the Cisco data center:*

- *Cisco NX-OS Programmability*

- *Cisco NX-OS Model-Driven Programmability​*

- *Cisco Nexus API*

- *Python*

- *Ansible*

- *HashiCorpTerraform*
