# Describing the Cisco Nexus Family and Cisco NX-OS Software

## Cisco Nexus Data Center Product Overview

*The Cisco Nexus product portfolio is a primary component of the Cisco Unified Fabric pillar of the Cisco Data Center architecture. These products are designed to meet the stringent requirements of the next-generation data center.*

*The Cisco Nexus product portfolio of switches offers these advantages:*

- *Transport that can navigate the transition to multispeed Gigabit Ethernet and unified fabric.*

- *Architectural change management for virtualization, Web 2.0 applications, and cloud computing.*

- *Real-time network visibility for capacity planning, security, and debugging.*

- *Operational continuity to meet your need for an environment where system availability is assumed and maintenance windows are rare or nonexistent.*

*All Cisco Nexus Series Switches run Cisco NX-OS Software. Cisco NX-OS is designed specifically for the data center and is engineered for high availability, scalability, and flexibility.*

*The Cisco Data Center family also includes Cisco MDS Series Switches and Cisco Unified Computing System (Cisco UCS) products.*

![Cisco Nexus](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/nexus.png)

## Cisco 6000 Series Switches

*Cisco Nexus Hyperfabric is a cloud-managed vertical stack solution consisting of purpose-built hardware, software, a cloud controller, Day 2 operations, automation, and Cisco support. When the Cisco 6000 Series Switches arrive on site and you deploy them, they automatically connect to the cloud. From there, the cloud controller claims and provisions them with a zero-touch plug-and-play approach.*

![Cisco Nexus Hyperfabric](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/nexus_hyperfabric.png)

## Cisco Nexus 9000 Series Modular Switches

*Cisco Nexus 9000 Series Switches include modular and fixed-port switches in these families:*

- *Cisco Nexus 9400 Series modular switches provide Cisco NX-OS or Application Centric Infrastructure (Cisco ACI) spine functionality:*

*Eight expansion slots support 64 ports of 400G, or 128 ports of 200G, or 176 ports of 10G, 25G, and 50G.*

*MACsec capability on all ports.*

- *Modular Cisco Nexus 9500 Series switches provide a highly available, resilient data center platform with great performance and scalability:*

*They are four, eight, and sixteen slot chassis.*

*Line cards support 1-, 10-, 25-, 40-, 50-, 100-, 200-, and 400-Gigabit Ethernet interfaces.*

- *Modular Cisco Nexus 9800 Series Switches are dual supervisor, resilient data-center switches:*

*Available with four-slot or eight-slot chassis.*

*Line cards support 10-, 25-, 100-, and 400-Gigabit Ethernet interfaces.*

![Cisco Nexus 9000](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/nexus2.png)

*Cisco Nexus 9500 and 9800 are highly modular with a zero service-loss architecture and redundant supervisors for core, distribution, or spine layers.*

## Cisco Nexus 9300 Series Fixed Switches:

*Cisco Nexus 9300 fixed switches provide multispeed Gigabit Ethernet connectivity in 1 or 2 rack unit form factor. The switches support Cisco NX-OS or ACI mode.*

![Cisco Nexus 9300](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/nexus3.png)

*Cisco Nexus 9300 top of rack (ToR) switches deliver high-performance, high-density multispeed Gigabit Ethernet. The switches are deployed in enterprise-class data center server access layer and smaller-scale, midmarket data center aggregation deployments.*

## Cisco Nexus 3000 Series Switches

*Cisco Nexus 3000 Series Switches offer low-latency, highly programmable, high-density switches. You can use them also for general-purpose deployments, high-performance computing (HPC), high-frequency trading (HFT), massively scalable data center (MSDC), and cloud networks.*

**Note:** *Features such as Active Latency Monitoring and Active Buffer Monitoring make these compact fixed switches excellent also for high-frequency trading and online banking environments, video streaming, and online games.*

*The figure displays some switches in the Cisco Nexus 3000 family.*

![Cisco Nexus 3000](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/nexus4.png)

*Switches from this series always come in a compact 1RU form factor but have many flavors. For example, the Cisco Nexus 3636C-FX2 switch (for the data center spine) offers 36 ports that can support speeds from 10 to 100 gigabits. The Cisco Nexus 3432D-S switch offers even faster speeds with 32 400-Gigabit Ethernet quad small form-factor pluggable–double density (QSFP-DD) ports.*

*Special modular networking interfaces achieve high speeds and more flexibility, including small form-factor pluggable (SFP) or faster ones with additional four lanes (quad small form-factor pluggable [QSFP]). The benefit of using SFP and QSFP ports compared to Ethernet ones is that you can pair them with many types of transceivers. The type of transceiver will determine the speed of the link, its connector, distance that can be covered by signal, and medium.*

# Cisco NX-OS Software Architecture

*The design goal for every data center is continuous operation with no service disruption. Cisco NX-OS was created because of this need for a consistent, predictable, and highly available system that would run on networking equipment.*

*The Cisco NX-OS network operating system was designed specifically for the data center and runs on Cisco Nexus Series Switches, Cisco MDS Series Switches, and the Cisco Unified Computing System (Cisco UCS) product line. It integrates Cisco SAN-OS Software and Cisco IOS Software to provide a consistent user interface across the entire data center product portfolio. Because of this integration, it can operate in both SAN and LAN environments and offers a comprehensive and scalable feature set.*

*Cisco NX-OS features:*

- *In-Service Software Upgrade (ISSU)*

- *Process restartability*

- *Supervisor restart*

- *Stateful supervisor failover*

- *Dual supervisor support (on Cisco Nexus modular switches)*

- *Role-based access control (RBAC)*

- *Cisco NX-API support*

*One feature that helps Cisco NX-OS to be highly available is Cisco IOS Software* ***In-Service Software Upgrade (ISSU).*** *This process upgrades an image to another image on a device while the network continues to forward packets. This functionality helps network administrators avoid a network outage when performing a software upgrade.*

***Process restartability*** *ensures that a failed service can recover and resume operations without disrupting the data plane or other services. Because of persistent storage service (PSS), a service can recover the last known operating state that preceded a failure, which allows for a stateful restart.*

*Features such as* ***supervisor restart*** *and* ***stateful supervisor failover*** *also make a big difference regarding system high availability. If a service that runs on a hardware supervisor module cannot be restarted by high-availability policies, a whole supervisor module restarts. In this case, the supervisor and all services reset and start with no prior state information.*

*Systems that support two supervisor modules, such as the Cisco Nexus 9500 and 9800 series, provide 1+1 redundancy for the control and management plane. This functionality is achieved by constantly synchronizing the configuration and state data between two supervisors. One supervisor is always in an active state and the other one in a standby state. If a supervisor-level unrecoverable failure occurs, the currently active, failed supervisor triggers a switchover. The standby supervisor becomes the new active supervisor and uses the synchronized state and configuration while the failed supervisor reloads. In this case, no services must restart.*

*Role-based access control (RBAC) allows network administrators to define the rules and user roles that dictate the operations allowed for the users in a specific group. For example, one role would allow access only to configuration operations, another one to debug operations, and the third would provide only read access for virtual device contexts (VDC) operators.*

*Last, but not least, Cisco NX-OS supports the Cisco NX-API. This web interface (through which commands traditionally entered via the CLI) can be encoded using either XML or JSON. Cisco NX-API is transmitted via HTTP or a secure transport (HTTPS) to the device. This feature is becoming more important in the era of automation, DevOps, and programmability.*

## Linux Kernel

![Linux Kernel](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/linux_kernel.png)

*The figure shows an architectural overview of Cisco NX-OS Software. An important design goal of Cisco NX-OS Software is to separate the protocols from the hypervisor and supervisor. This separation makes implementation of new protocols in the future easier and more efficient.*

**Additional Notes:**

Supervisor → the brains of the switch itself. It’s the control-plane OS component running on the supervisor module, handling routing processes, system services, management tasks—basically the “operating system layer” of the box.

Hypervisor → the layer that *hosts* and isolates those processes like virtual machines. NX-OS runs many of its features (like routing protocols) as separate processes on top of a tiny, hardened hypervisor-like kernel. It’s not a “VMware ESXi” hypervisor, but it plays a similar role: isolation, stability, crash containment.

So:

- Supervisor = the commander.

- Hypervisor = the containment field the commander uses to keep all the subsystems from wrecking each other.

By keeping protocols **off** the supervisor and running them as isolated processes, Cisco can update, reload, or add new protocol services without rebooting the whole switch or nuking the control plane.

*The Cisco NX-OS Software kernel architecture has several main components:*

- *The Linux kernel provides preemptive multitasking, virtual memory, and multithreading and is the foundation on which all other processes run.*

- *The system infrastructure and high-availability managers from Cisco SAN-OS Software are used to provide the same levels of reliability and resiliency in Cisco NX-OS Software.*

- *Multiple separate protocol suites are supported (based on the platform), including storage protocol services, a scalable Layer 3 protocol implementation, and a data center-focused, standards-based Layer 2 feature set.*

*The full-featured, modular, and scalable Cisco NX-OS Software is available on the entire Cisco data center switching portfolio and helps enable the Cisco Unified Fabric. Its modular building-block approach helps you to quickly integrate innovations and evolving industry standards.*

*Built as the foundation of Cisco Data Center architecture, Cisco NX-OS Software helps ensure continuous availability in mission-critical environments. Its self-healing, highly modular design makes zero-impact operations a reality and provides exceptional operational flexibility and scalability.*

*Delivering the critical features for next-generation networks, Cisco NX-OS Software is based on four pillars: resiliency, virtualization, efficiency, and extensibility:*

- **Resiliency:** *Cisco NX-OS Software delivers highly secure continuous operations, with failure detection, fault isolation, self-healing features, and hitless ISSU, which helps reduce maintenance outages. Hitless ISSU (In-Service Software Upgrade) allows for software upgrades on network devices with minimal or no disruption to traffic. This process enables the system to upgrade while maintaining service continuity, often by restarting only the necessary components instead of the entire system. Cisco juniper.net*

- **Virtualization:** *Cisco NX-OS Software enhances virtual machine portability and converges multiple services, platforms, and networks to reduce infrastructure sprawl and total cost of ownership (TCO).*

- **Efficiency:** *Operational tools and clustering technologies reduce complexity and offer consistent features and operations without compromising functionality.*

- **Extensibility:** *Cisco NX-OS Software scales current and future multiprocessor hardware platforms and offers easy portability across varying platforms with consistent features. It facilitates the integration of innovations and evolving standards and delivers long-term feature extensibility.*

## Process Separation

*Cisco NX-OS Software provides process separation:*

- *Processes are instantiated on demand.*

- *System resources are allocated only when the specific feature is enabled.*

![Process Separation](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/process_separation.png)

*Cisco NX-OS Software supports distributed multithreaded processing on symmetric multiprocessors, multicore CPUs, and distributed line-card processors. Computationally intensive tasks, such as hardware table programming, can be offloaded to dedicated processors distributed across the line cards.*

*Cisco NX-OS Software modular processes are instantiated on demand, each in a separate, protected memory space. Therefore, processes start and system resources are allocated only when you enable a feature. A real-time preemptive scheduler governs the modular processes and helps ensure the timely processing of critical functions. Processes are fault-isolated, which allows the high-availability manager to determine the best recovery action for each process.*

## Cisco NX-OS Coding

*Cisco NX-OS supports many hardware platforms and has many releases and software types. Therefore, it is crucial for network administrators who work with Cisco Nexus and MDS devices to recognize the release names of Cisco NX-OS Software to avoid possible outages.*

*Find and download all this software from the [Cisco Software Central](https://software.cisco.com/#) platform.*

![NX OS Coding](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/nxos_coding.png)

*Cisco NX-OS Software consists of one Cisco NX-OS Software image that is necessary to load Cisco NX-OS.*

*As shown in the figure, the coding format of the Cisco NX-OS Software versions contains the following:*

1. ***Cisco NX-OS image filename:***

- *The 32-bit Cisco NX-OS image file has the image filename that begins with “nxos” (for example, nxos.10.1.1.bin).*

- *The 64-bit Cisco NX-OS image file has the image filename that begins with “nxos64” (for example, nxos64.10.1.1.bin).*

- *Beginning with Cisco NX-OS Release 10.2(2)F, all Cisco Nexus platforms will be operating on one of two 64-bit images:*

*The 64-bit Cisco NX-OS image file has the image filename that begins with “nxos64-cs” (for example, nxos64-cs.10.2.2.F.bin). This image is supported on Cisco Nexus 9000-EX, -FX, -GX, and -GX2 series modular switches and Cisco Nexus 9000 series fixed switches.*

*The 64-bit Cisco NX-OS image file has the image filename that begins with “nxos64-msll” (for example, nxos64-msll.10.2.2.F.bin). This image is supported on Cisco Nexus 9000-R and -R2 series modular switches, Cisco Nexus 3600 series fixed switches, and Cisco Nexus 3500-XL switches.*

2. ***Release designations:***

- ***F:*** *A Cisco NX-OS Software release that provides new features and new platform support in addition to bug fixes.*

- ***M:*** *A Cisco NX-OS Software release that provides bug fix support or Product Security Incident Response Team (PSIRT) fixes as part of ongoing software maintenance.*

3. ***Extension:***

- *Each file also has a file extension that determines that the file is a compressed binary file.*

# Cisco NX-OS Software CLI Tools

*When working with devices that run Cisco NX-OS Software, it is useful to know basic commands, shortcuts, and tools that will help you to navigate, explore, and verify the device environment faster.*

***Command Line Help:***

![CLI Help](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/cli_help.png)

*Two options are available to display CLI help. Enter the question mark (```?```) symbol at any point on the command line to display full parser help. It includes accompanying descriptions that are based on the current user context within the CLI.*

*The ***Tab*** key still provides command completion. Reserved and user-defined names can also be completed by pressing the Tab key.*

*The ***Ctrl+Z*** key combination exits configuration mode but retains the user input on the command line.*

*The ```end``` command can also be used to exit configuration mode. The ```exit``` command navigates one level higher in the CLI.*

*The ```where``` command displays the current configuration context and the login credentials of the current user.*

*Place the pipe parameter (```|```) at the end of any CLI command to qualify, redirect, or filter the output of the command.*

## Cisco NX-OS Neighbor Discovery Tools

*Cisco Discovery Protocol is a Cisco proprietary protocol that lets you discover basic information about neighboring Cisco devices without knowing the passwords for the neighboring devices. To discover information, routers and switches send Cisco Discovery Protocol messages to each of their interfaces. The messages essentially announce information about the device that sent the Cisco Discovery Protocol message. Devices that support Cisco Discovery Protocol learn information about other devices by listening for the advertisements that these devices send.*

*Cisco Discovery Protocol provides the following information about each neighboring device:*

- ***Device identifiers:*** *Identifiers include items like the configured hostname of the switch.*

- ***Address list:*** *This list provides up to one network layer address for each protocol that is supported.*

- ***Port identifier:*** *This identifier is the name of the local port and remote port, in the form of an ASCII character string such as Ethernet0.*

- ***Capabilities list:*** *This list includes the supported features, for example, the device acting as a source-route bridge and also as a router.*

- ***Platform:*** *The platform is the hardware platform of the device, for example, the Cisco Nexus 9000 Series switch.*

*To permit the discovery of devices that are not manufactured by Cisco, Cisco devices also support Link Level Discovery Protocol (LLDP). LLDP is a vendor-neutral device discovery protocol that the IEEE 802.1AB standard defines. LLDP allows network devices to advertise information about themselves to other devices on the network. This protocol runs over the data link layer and allows two systems that are running different network layer protocols to learn about each other.*

*LLDP is a one-way protocol that transmits information about the capabilities and the status of a device and its interfaces. LLDP devices use the protocol to solicit information only from other LLDP devices.*

*LLDP supports a set of attributes that it uses to discover other devices. These attributes contain type, length, value (TLV) descriptions. LLDP devices can use TLV descriptions to send and receive information to and from other devices on the network. Using this protocol, devices can advertise details such as configuration information, device capabilities, and device identity.*

## Cisco NX-OS Connectivity Tools

*You can use common Cisco NX-OS tools to verify connectivity.*

*A device’s Address Resolution Protocol (ARP) cache is a common initial point for troubleshooting IP connectivity. The ARP cache will display entries that map Layer 2 MAC addresses to Layer 3 IP addresses. A record of each correspondence remains in a cache for a predetermined amount of time and is then discarded. To display the ARP cache (the ARP table), use the ```show ip arp``` command.*

*Once you verify the entries in various tables (MAC, ARP, and route), the next step is to confirm end-to-end connectivity. To diagnose basic network connectivity, you can use the ```ping``` command. By default, five Internet Control Message Protocol (ICMP) packets transmit, and five replies are necessary for a perfectly successful test.*

*The one overwhelming issue with using only the ```ping``` command to troubleshoot connectivity is that ```ping``` shows only if there is (or is not) end-to-end connectivity. If you would like to see where the failure occurred, or which device processes your packet every step of the way, then use the ```traceroute``` command.*

```
N9K-1# ping 192.168.10.125
 PING 192.168.10.125 (192.168.10.125): 56 data bytes 
 64 bytes from 192.168.10.125: icmp_seq=0 ttl=254 time=1.124 ms 
 64 bytes from 192.168.10.125: icmp_seq=1 ttl=254 time=1.124 ms 
 64 bytes from 192.168.10.125: icmp_seq=2 ttl=254 time=0.971 ms 
 64 bytes from 192.168.10.125: icmp_seq=3 ttl=254 time=1.003 ms 
 64 bytes from 192.168.10.125: icmp_seq=4 ttl=254 time=1.011 ms
N9K-1# traceroute 192.168.10.125 
 traceroute to 192.168.10.185 (192.168.10.125), 30 hops max, 40 byte packets 
 1  192.168.10.125 (192.168.10.125)  1.193 ms  0.995 ms  0.949 ms
```

# Cisco NX-OS Virtual Routing and Forwarding

*Device virtualization is a main feature of the Cisco Nexus platform. Cisco NX-OS supports virtual routing and forwarding instances (VRFs), which are independent virtual routers that run on a physical switch. Each VRF makes routing decisions independent of any other VRF because it contains a separate address space, subnets, routing protocol, and dedicated physical interfaces.*

*By default, two VRFs are present in the system: the default and the management VRF. The mgmt0 interface can be assigned only to the management VRF. As the name implies, it provides management access to the device via Secure Shell (SSH) or Telnet.*

*The second VRF is the default VRF, where routing protocols run unless you specify another context. By default, all interfaces are assigned to the default VRF. These interfaces (except mgmt0) can then be reassigned to other VRF instances after an administrator creates them. Cisco NX-OS supports up to 1000 VRFs per system.*

*Management VRF characteristics are as follows:*

- *The management VRF instance is for management purposes only.*

- *Only the mgmt0 interface can be in the management VRF instance.*

- *The mgmt0 interface cannot be assigned to another VRF instance.*

- *No routing protocols can run in the management VRF instance (static only).*

*However, the default VRF instance characteristics are the following:*

- *All Layer 3 interfaces exist in the default VRF instance until they are assigned to another VRF instance.*

- *Routing protocols run in the default VRF context unless another VRF context is specified.*

- *The default VRF instance uses the default routing context for all ```show``` commands.*

- *The default VRF instance is similar to the global routing table concept in Cisco IOS Software.*

*All unicast and multicast routing protocols support VRF instances. When you configure a routing protocol in a VRF instance, you set routing parameters for virtual routing and forwarding. These parameters are independent of routing parameters in another VRF instance for the same routing protocol instance.*

*You can assign interfaces and route protocols to a VRF instance to create virtual Layer 3 networks. An interface exists in only one VRF instance.*

![VRF Instances](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vrf_instances.png)

*The figure illustrates one physical network split into two virtual networks with two VRF instances. Routers Z, A, and B exist in VRF Red and form one address domain. These routers share route updates that do not include Router C because Router C is configured in a different VRF instance. By default, Cisco NX-OS uses the VRF instance of the incoming interface to select which routing table to use for a route lookup.*

*VRF instances have the following configuration guidelines and limitations:*

- *When you make an interface a member of an existing VRF instance, Cisco NX-OS removes all Layer 3 configurations. You should configure all Layer 3 parameters after adding an interface to a VRF instance.*

- *Add the mgmt0 interface to the management VRF instance and configure the mgmt0 IP address and other parameters after you add it to the management VRF instance.*

- *If you configure an interface for a VRF instance before the VRF exists, the interface is operationally down until you create the VRF instance.*

- *Cisco NX-OS creates the default and management VRF instances automatically. You should make the mgmt0 interface a member of the management VRF instance.*

- *The ```write erase boot``` command does not remove the management VRF configurations. You must use the ```write erase``` command and then the ```write erase boot``` command.*

**Additional Notes:**

On NX-OS, there are *two* separate places where configuration lives:

1. The regular system configuration

2. The boot-related configuration (stuff that tells the device how to boot: images, kickstart, loader info, etc.)

Now:

- ```write erase``` wipes the *main* configuration — including things like the *management VRF*, interfaces, routing protocols, etc.

- ```write erase boot``` wipes the *boot variables*, but *does NOT touch the management VRF.*

So if you only do ```write erase boot```, your management VRF survives like some cockroach after a nuclear event.

BUT if you do:

```
write erase
write erase boot
```

You nuke both the running config *and* the boot config — a true clean slate.

Think of it like a two-layer cake:

- Top layer (normal config): ```write erase```

- Bottom layer (boot config): ```write erase boot```

```write erase boot``` wipes your boot variables, meaning:

- which NX-OS image to load

- any kickstart image settings (on older platforms)

- any saved boot-related environment entries

After you run it, the switch won’t remember which image it’s supposed to boot from. You’ll normally have to:

1. Reconfigure your boot variables (```boot nxos bootflash:nxos.whatever.bin```)

2. Save

3. Reload

So yeah — it absolutely nukes the active NX-OS boot setting. Be careful with it, especially on hardware that doesn’t fall back gracefully! And the trick is: *You can erase the bottom layer alone, but the top layer won’t disappear unless you hit it explicitly.*

## Labs: Explore the Cisco NX-OS CLI

This lab was basically your introduction to the *language* and *navigation rules* of the Nexus CLI. You SSH’d into two Nexus 9Ks, got comfortable with their environment, and explored two core usability features:

1. Context-Sensitive Help (```?```)

- Typing ```?``` shows everything valid in your current spot.

- Commands aren’t flat — they’re hierarchical, and help reflects that.

- ```<CR>``` means the command is complete and ready to run.

- If ```<CR>``` doesn’t show up, you haven’t given it enough info.

2. Tab Autocompletion

- Hit Tab after typing letters to fill in the rest of a command.

- Works for commands *and* arguments.

- Once your input is unique, NX-OS fills it automatically.

3. Building a Command Step by Step

The lab walked you through constructing a command piece by piece:

```
show
show interface
show interface status
show interface status up
```

Each step showed new valid arguments with ```?```, and you learned how the CLI only gives you options that make sense in the current context.

4. Seeing Real Output

You executed:

```
show interface status up
```

and saw the active/connected ports — a clean, focused view compared to the full ```show interface```, which is like a firehose.

## Manipulate the Cisco NX-OS Command Output and Explore the ```Show Interface``` Command

1. NX-OS lets you filter output just like Linux

Any big, noisy ```show``` command can be trimmed using pipes (```|```). Think of it like *grep for network people.*

You get tools like:

- ```egrep``` → search patterns (case-insensitive, context lines, etc.)

- ```no-more``` → dump everything without pagination

- ```head``` → first lines only

- ```tail``` → last lines only

You can chain pipes endlessly like a little command alchemist.

2. Long outputs automatically pause with ```--More--```

NX-OS doesn’t vomit 300 lines at once. It feeds it in chunks.

At ```--More--```, you can:

- **Enter** → one line

- **Space** → next page

- **q** → quit

- **Ctrl+C** → force-stop

- **h** → help

So you’re not drowning in text unless you want to.

3. Filtering is nice, but specific commands are nicer

Instead of:

```
show interface
```

you can do:

```
show interface mgmt0
```

Boom → tiny, relevant, crisp output. NX-OS rewards being precise.

4. ```show interface status``` is the god-tier quick overview

This command gives you the “whole switch at a glance”: port, speed, duplex, VLAN, link state, interface type, and transceiver type.

Because 64 ports is chaos, but this format calms the chaos.

5. What each column actually means

Using interface ```Eth1/1``` as the model:

- **Port** → physical port name (```Ethernet 1/1```)

- **Name** → description field (your custom label)

- **Status** → is link up? Is cable/SFP good?

- **Vlan:**

says ```routed``` for L3 ports

says VLAN number or ```trunk``` for L2 ports

- **Duplex** → auto/half/full

- **Speed** → negotiated speed (1G/10G/40G etc.)

- **Type** → the transceiver + capability summary

Example: ```QSFP-40G-SR-BD``` = 40G, short-range, bidirectional

This is your quick health check for a switch.

6. ```egrep``` is surprisingly powerful in NX-OS

Example:

```
show spanning-tree | egrep ignore-case next 4 rstp
```

Breaks down as:

- run ```show spanning-tree```

- pipe it to egrep

- match ```rstp``` without worrying about case

- show the next *4 lines* of context after the match

Super handy for digging up config bits buried in giant outputs.

**Additional Notes:** Here’s the real, full-ish set of pipe filters you can use on Cisco Nexus switches. This is the stuff that actually exists on NX-OS (not IOS, not IOS-XE… specifically NX-OS).

*Filtering / Matching:*

```
| include <pattern>
| exclude <pattern>
| grep <pattern>
| egrep <options> <regex>
| awk <expression>
```

- ```include``` → show only lines containing pattern

- ```exclude``` → hide lines containing pattern

- ```grep``` → classic regex search

- ```egrep``` → extended regex + options: ```ignore-case```, ```count```, ```next <N>``` (show N following lines), ```before <N>``` (show lines before match), ```color``` (highlight matches)

- ```awk``` → mini text-processing beast (but limited version)

*Pagination / Flow Control:*

```
| no-more
```

- disables ```--More--```, dumps everything at once

- very useful when piping into ```grep``` or redirecting output

*Redirection:*

```
> filename
>> filename
| redirect <file>
```

- ```>``` overwrite file

- ```>>``` append file

- ```redirect``` works both locally and across VRFs (the lab hints at this with ```>``` and ```>>```)

*Output Transformation:*

```
| json
| xml
| section <title>
| count
| sort <field>
| uniq
```

- ```json``` → forces JSON output where supported

- ```xml``` → same but XML

- ```section <title>``` → pulls the whole config "block" that starts with that word

- ```count``` → count matching lines

- ```sort``` → alphabetical sort

- ```uniq``` → collapse duplicates

*Head/Tail:*

```
| head <N>
| tail <N>
```

- first N lines or last N lines

**Super-short mnemonic:** *“GHOST CRUSH”*

Every letter = a pipe you can throw at NX-OS output:

- **G** → grep / egrep

- **H** → head

- **O** → output modes (json/xml)

- **S** → section / sort

- **T** → tail

- **C** → count

- **R** → redirect

- **U** → uniq

- **S** → search (include/exclude)

- **H** → no-more (handler for pagination)

## Explore Command-Line Navigation and Shortcuts

NX-OS keeps a history of your commands so you can recall, edit, and re-run them without retyping everything like a medieval scribe.

Use *Up Arrow* to step backward through history, and *Left/Right Arrows* to move the cursor inside the recalled command. Backspace edits normally; anything typed gets inserted at the cursor.

If you mistype something like ```snow inter```, hitting *Tab* won’t autocomplete because the parser doesn’t recognize that string. That failure is a signal that you're off-syntax.

When you press *Enter*, NX-OS shows a *parser error arrow (^)* under the exact character where the syntax breaks. It’s a simple but powerful way to pinpoint the issue. The arrow lines up correctly only with *monospaced fonts*, so don’t use anything weird.

**Useful editing shortcuts:**

- **Ctrl+A** → Jump to start of line

- **Ctrl+E** → Jump to end of line

- **Up Arrow** → Recall last command

- **Tab** → Autocomplete (works only if valid up to that point)

NX-OS supports Home/End/Delete too, but these keys can misbehave depending on your keyboard layout and terminal — sometimes Delete inserts a literal ```~``` instead of deleting. When in doubt, stick to the *Ctrl+* shortcuts.

**Additional Notes:** NX-OS likes to be a little diva about clearing the terminal. The actual way to clear your terminal on NX-OS is:

```
Ctrl+L
```

There is a command too, but it's hidden in plain sight:

```
clear screen
```

But you can’t “do” it from inside config mode — NX-OS just doesn’t support the IOS-style ```do``` hack here. So:

- In exec mode → ```clear screen``` works

- In config mode → you’re stuck with *Ctrl+L*

## Explore Cisco Nexus Device Configuration

NX-OS keeps things simple: *running-config = live, volatile* and *startup-config = saved, persistent.* Anything you want to survive a reboot must be copied to startup.

- Use SSH to connect to ```N9K-A``` → log in as ```admin / 1234QWer```.

- View the whole active config with:

```
show running-config
```

NX-OS hides defaults, so the file looks shorter than IOS. Knowing the defaults matters when troubleshooting.

You can drill into specific parts of the config:

```
show running-config interface mgmt0
```

Common abbreviations work (```sh run int mgmt0```).

```mgmt0``` lives inside the *management VRF*, which has its own routing table.

- Anything that uses routing (like ```ping```) must specify the VRF or it defaults to ```default```.

**Filtering Output:**

Like any show command, you can pipe it:

```
show running-config | include <string>
show running-config | section <string>
```

- **include** → prints only the matching lines

- **section** → prints entire config blocks that contain the match

This is gold for hunting interfaces, features, or odd ghosts in the config.

Unlike IOS, NX-OS lets you run show commands directly in config mode. No ```do``` prefix needed. Ever. It’s lovely.

Check what’s currently saved:

```
show startup-config
```

Save your changes so the switch remembers them:

```
copy running-config startup-config
```

This overwrites the old startup config with the running one.

## Explore Network Status Tools

NX-OS gives you the usual troubleshooting toys — ```ping```, ```traceroute```, etc. — but they live inside a world of *multiple VRFs*, so context matters. Two VRFs are always present:

- **management** → for ```mgmt0```

- **default** → for everything else

If you run a command without specifying VRF, NX-OS uses *default*, which often means *“haha nope, wrong table.”*

On ```N9K-A```, verify the mgmt IP:

```
show ip interface mgmt0 | include address
```

From ```N9K-B```, try pinging that mgmt IP:

```
ping 10.1.1.101
```

It fails with *No route to host* — because you pinged from the *default VRF*, which has *zero knowledge* of the management network.

Run the ping *properly:*

```
ping 10.1.1.101 vrf management
```

Now it works. The first ICMP may drop — that’s just ARP pounding the door asking, “Who lives at this IP?” After that, it’s smooth sailing.

Check if ```N9K-B``` learned ```N9K-A```’s mgmt MAC:

```
show ip arp vrf management
```

Traceroute for path insight:

```
traceroute 10.1.1.101 vrf management
```

Since both switches sit in the same subnet, you’ll see no intermediate hops — just a straight line through the void.

## Explore Command Aliases

*What aliases are:*

- NX-OS lets you create *custom commands* (aliases) that act as shortcuts for longer commands.

- Aliases are *global*, affect all users, and *persist across reboots* if saved to startup-config.

- They always replace the *first keyword* in a command line.

- Default aliases (like ```alias``` for ```show cli alias```) cannot be overridden.

*Alias Mechanics:*

- Aliases take precedence over *any* normal keyword in any mode.

- One alias can reference another, but *nesting depth* = 1 max.

- You can define aliases in any configuration submode.

- They work like macro triggers — the alias runs the target command silently beneath.

*Viewing Existing Aliases:*

```
show cli alias
```

(or ```alias``` — which itself is a built-in alias!)

To view only lines containing alias definitions in the config:

```
show running-config | include alias
show startup-config | include alias
```

*Creating Your Own Alias:*

Enter config mode:

```
conf
```

(Yes — this is the NX-OS version of ```configure terminal```.)

Make the classic IOS-style ```wr``` alias:

```
cli alias name wr copy running-config startup-config
```

Meaning: typing ```wr``` will internally run ```copy running-config startup-config```.

Like any config change, aliases only persist if saved:

```
wr
```

or

```
copy running-config startup-config
```

(Using your new alias to save itself is allowed.)

*Notes & Gotchas:*

- If you rely too much on aliases, you might forget real commands.

- On certification exams or unfamiliar devices, your aliases won’t be there, so don’t let them replace your core muscle memory.

- Because alias resolution happens first, a poorly chosen alias name can accidentally block real commands.

## Labs: Explore Topology Discovery

### Explore the Cisco Nexus Platform and Software

When you step into an unfamiliar network, first job = *identify devices and how they’re built.*

In this lab, you SSH from the Student VM into every Nexus switch’s management interface so you can jump between them quickly. Use PuTTY or anything similar.

*Check Device Model & NX-OS Version:*

```
show version
```

This command tells you:

- The exact Nexus model (e.g., 9000v, 93180YC-EX, etc.)

- The NX-OS version it’s running

- Hardware platform details

- System uptime, BIOS version, kickstart image, and so on

Features are *hardware-dependent* in NX-OS. Some things work only on N7K, others on certain N9K models. So the show version output is basically your “what can this thing do?” snapshot.

*Viewing Hardware Modules:*

```
show module
```

NX-OS devices treat every major hardware block as a *module*, even virtual ones. This output always includes *four tables*, each with a different purpose:

1. Hardware + software modules (actual cards, virtual linecards, supervisor components)

2. Module software versions

3. Port MAC address ranges

4. Operational status

Example:

```
N9K-A# show module
Mod Ports                  Module-Type                            Model           Status
--- ----- ------------------------------------------------ --------------------- --------
1    64   Nexus 9000v 64 port Ethernet Module              N9K-X9364v            ok
27   0    Virtual Supervisor Module                        N9K-vSUP              active *

Mod  Sw                       Hw    Slot
---  ----------------------- ------ ----
1    10.5(1)                  0.0    LC1
27   10.5(1)                  0.0    SUP1


Mod  MAC-Address(es)                         Serial-Num
---  --------------------------------------  ----------
1    52-35-42-b0-01-01 to 52-35-42-b0-01-40  9R2WKW457J9
27   52-35-42-b0-1b-01 to 52-35-42-b0-1b-12  9TLIVYJ4NXK

Mod  Online Diag Status
---  ------------------
1    Pass
27   Pass

* this terminal session
N9K-A#
```

But wait... *why does the module have a MAC address?*

It is weird at first glance. Here’s the deal:

- A module (real or virtual) has *MAC address blocks* assigned to it.

- These aren’t “one MAC for all ports” — it’s actually a *range* used to allocate per-port MACs internally.

- On virtual devices (like *9000v*), the simulator gives each “linecard” a single representative MAC block, so it looks like one MAC per whole module.

It’s not that the module *uses* a MAC — it *owns* a chunk of MAC space to assign to interfaces. In real hardware:

- linecards = own MAC pools

- supervisors = own MAC pools

- FEXes = own pools

*Checking SFP Modules:*

```
show interface status
```

This command tells you what is physically plugged into each port:

- SFPs

- QSFPs

- Twinax cables

- Or nothing at all

**SFPs are NOT modules** in the NX-OS sense. They're *transceivers*, not logic/hardware modules. Think of it like this:

- ```show module``` = big hardware blocks (linecards, supervisors, ASICs)

- ```show interface status``` = physical optics/transceivers plugged into individual ports

*Why?* Because an SFP is basically a small removable PHY, not an FPGA/ASIC module. It doesn’t run code or have a software version — so it doesn’t belong in the module inventory.

*Interface Status Values (SFP Indicators):*

In ```show interface status```, *“Type” field values include:*

- Listed product number → This is the *SFP model name*, shown directly in the interface status output. Example:

```
Eth1/1    1G    SFP-10G-LR     connected
```

- *xcvrAbsen* → No SFP or transceiver inserted.

- *1000BASE-T* → Classic gigabit copper SFP (“GLC-T”), with RJ45 tip.

- *Unknown Type-(unknown)* → The SFP is unsupported, faulty, or not recognized by NX-OS.

**Additional Notes:** The product number appears directly under the “Type” column of:

```
show interface status
```

Example:

```
Eth1/5   sfpAbsent    xcvrAbsen
Eth1/6   1G           GLC-T
Eth1/7   10G          SFP-10G-SR
```

The “GLC-T”, “SFP-10G-SR”, etc. — those are the product numbers. It is not from the ```show module``` output.

**Quick Summary:**

- Use ```show version``` to identify model + NX-OS version + feature support.

- Use ```show module``` to see hardware blocks (linecards, supervisors). Includes MAC ranges — modules own MAC pools, even virtual ones.

- Use ```show interface status``` to see SFP/QSFP/Twinax presence & type. Only here do you see product numbers like ```GLC-T``` or ```SFP-10G-LR```.

### Explore Link Discovery Protocols

Network devices rarely exist alone — they live in a buzzing ecosystem of neighbors. Knowing who’s plugged into who lets you design, troubleshoot, and change things without wandering blindfolded into a rack and hugging the wrong cable.

*Discovering Neighbors with CDP:*

*CDP (Cisco Discovery Protocol)* is Cisco’s proprietary L2 discovery tool. It’s enabled by default on almost all Cisco interfaces and gives you the best visibility into neighboring Cisco devices.

Use it like this:

```
show cdp neighbors
```

What CDP tells you:

- *Device ID* → typically the hostname

- *Address list* → one IP per protocol

- *Local port / remote port* → where you connect

- *Capabilities* → router, switch, phone, etc.

- *Platform* → hardware model (N9K, ISR, etc.)

The output uses *two rows per neighbor:*

- Row 1: hostname + serial

- Row 2: your interface → their interface

Timers:

- Sends CDP updates every *60s*

- Neighbors age out after *180s*

- Hold time refreshes with each advertisement

CDP can be disabled:

```
no cdp enable
cdp enable
```

But unless you intentionally turned it off, it’s running on everything.

*LLDP — The Vendor-Neutral Cousin:*

*LLDP* works exactly like CDP, but across *all* vendors. On Nexus? It’s *disabled by default*, and the commands don’t even exist until you activate the feature.

Enable it globally:

```
conf t
feature lldp
```

Control per interface:

```
lldp transmit
lldp receive
no lldp transmit
no lldp receive
```

After enabling, wait a minute, then:

```
show lldp neighbors
```

*Interface Ranges on Nexus — the Gotcha:*

My IOS muscle memory said:

```
interface range e1/1 - 6
```

But Nexus said: *lol nope.* Instead, NX-OS wants:

```
interface ethernet 1/1-6
```

*No space. No “range” keyword.*

That’s why doing them individually worked but felt stupid.

Once inside, you can manipulate all ports at once:

```
shutdown
no shutdown
description Uplink-to-B
```

Very clean, very efficient — as long as:

- ports are sequential

- you triple-check you’re not touching production links

***Admin-Down vs Physically Idle Ports:***

*Administratively down:*

- ```show interface status``` → ```admin down```

- CDP/LLDP → no entries ever

- ```show interface e1/x``` → explicitly says *Administratively down, line protocol down*

*Physically connected but unused:*

- ```show interface status``` → connected / notconnect

- If cable present → CDP/LLDP info pops up

- If no cable → *down/down*, but **not** admin down

In short:

- Admin down = command shut the port

- Down/down = nothing plugged in / dead cable

- Up/down = mismatch or config problem

- Up/up = living link

*Spanning Tree Reality Check:*

STP protects the universe from L2 loops. One active path, others blocked. A blocked port:

- Still passes CDP/LLDP

- Still gives you topology clues

- Does NOT forward traffic

And yes: never re-enable random L2 ports in production unless you like BYOB — Bring Your Own Broadcast-Storm.

Check STP:

```
show spanning-tree
```

Your lab may show N9K-A as root or another switch depending on priorities.

Good Practice:

- Document interfaces with:

```
description <text>
```

Look up specific ports:

```
show running-config interface e1/2
show interface status
```

- Dead ports + no CDP/LLDP after shutdown = no way to tell remote side without checking the physical cable.

Topology diagrams are nice, but interface descriptions live forever. On that note, here is topology diagram used in the labs:

![Lab Topology](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/topology.png)

### Explore Cisco Discovery Protocol Further

You can poke around the CDP command set using:

```
show cdp ?
```

NX-OS gives you a bunch of subcommands to fine-tune what you want to see.

*Global CDP Settings:*

Use:

```
show cdp global
```

This reveals the core behavior:

**CDP enabled:**

- On most Cisco devices — including Nexus — CDP is globally enabled by default.

- Every interface participates unless explicitly disabled.

**Refresh timer:**

- Default: 180 seconds

- How long a neighbor stays in the table before aging out if nothing is heard.

- These timers can be changed, but in the real world almost nobody touches them.

*Per-Interface CDP Lookup:*

```
show cdp neighbors interface ethernet 1/2
```

- This filters neighbors only for that interface.

- Useful when you’re drowning in tons of CDP entries.

- But: no extra information — just a scoped-down view.

*The Money Command: ```detail```*

```
show cdp neighbors interface ethernet 1/2 detail
```

Or universally:

```
show cdp neighbors detail
```

This is the *only* CDP command that exposes:

- Layer 3 IP address of the neighbor

- Exact software version

- Platform and serial numbers

- Device capabilities in readable form (R, S, I, etc.)

- Management IP

This is true on NX-OS and IOS. The plain ```show cdp neighbors``` output? Cute but minimal.

```detail```? That’s the real inspection tool — the network equivalent of prying open a skull and reading the firmware inside. LLDP has its own “detail” version too (```show lldp neighbors detail```), but CDP usually gives richer vendor-specific information.

*Mini-Mnemonic for CDP Commands:*

- **neighbors** → “Who’s around me?”

- **interface X/Y** → “Who’s on this wire?”

- **detail** → “Tell me their secrets.”

- **global** → “How CDP behaves everywhere.”
