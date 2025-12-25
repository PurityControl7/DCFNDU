# Describing Cisco NPV Mode and NPIV

## Cisco Switch Mode

*Cisco MDS Series Switches can operate in multiple modes. The default mode is fabric (switch) mode. In this mode, the switch operates as a Fibre Channel switch and performs all Fibre Channel operations locally. You must configure it as a Fibre Channel switch.*

![Cisco Switch Mode](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/cisco_switch_mode.png)

*The following are characteristics of a Cisco MDS device that is operating in switch mode:*

- *Full Fibre Channel switch operations are available.*

- *For Fibre Channel operation:*

1. *Each switch consumes a Fibre Channel domain ID.*

2. *Connection to third-party switches requires configuration in interop mode.*

3. *All Fibre Channel services are provided.*

- *FLOGI, name server, zoning, domain server, Fabric Shortest Path First (FSPF), and management.*

- *FSPF, zoning, and the name server databases are distributed among connected switches.*

1. *Local Fibre Channel switching is enabled.*

2. *Inter-Switch Links (ISLs) between switches become paths in the FSPF routing table.*

3. *Up to 16 ISLs may belong to a single port channel.*

*In traditional Fibre Channel switching operations, each Fibre Channel switch has one domain ID per VSAN and connects to the upstream Fibre Channel switch through an E Port. The host (server) that connects to the switch first sends the FLOGI to the switch. The switch then intercepts the FLOGI and assigns the Fibre Channel ID to the host by sending an Accept frame.*

*The Fibre Channel switch runs the FSPF routing protocol and computes the path to reach the remote domains using the Fibre Channel routing table. It also provides other Fibre Channel services such as Name Registration, Binding Check, Zoning Check, and others.*

*The Fibre Channel switch maintains the Fibre Channel ID–to-port mapping table (Station Table) for the locally attached hosts. When the Fibre Channel switch receives a frame, the Fibre Channel switch checks the domain ID of the destination ID first. If the domain ID is the same as the domain ID of the Fibre Channel switch, then the local Station Table determines the destination port. If the domain ID differs from the domain ID of the Fibre Channel switch, then the Fibre Channel switch searches the Fibre Channel routing table to identify the egress port.*

*Note: SAN switching is supported only on the Cisco Nexus 93180YC-FX and 93360YC-FX2 switches from the Cisco Nexus 9000 Series family.*

## Fibre Channel Domain Scalability

*Blade switch deployments are increasingly common among enterprise customers, and Fibre Channel deployments are becoming more common. Both deployments are likely to continue to grow in popularity, which will require Fibre Channel scalability planning.*

*The figure shows an example topology that you would use in a scaling process.*

![FC Domain Scalability](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/FC_domain_scalability.png)

*As the scale of Fibre Channel switch deployments increases, several challenges arise:*

- *Large increases in the number of domain IDs required in a fabric (one per switch)*

- *Increased network complexity (multiple technologies on a single switch)*

- *Increased management complexity (shared switch management)*

- *Interoperability concerns in multivendor environments*

*The Fibre Channel standards allow for up to 239 Fibre Channel domains per fabric or VSAN. A single domain ID identifies each Fibre Channel switch and puts a theoretical upper limit on the number of switches per fabric. The fact that each Fibre Channel switch requires one Fibre Channel domain ID per virtual fabric poses scalability problems for the fabric.*

*Cisco has validated up to 100 domain IDs per fabric, while other vendors have tested 40 or do not specify a number. As a result, the practical maximum number of switches per fabric is 100.*

*Blade switches and top-of-rack access layer switches that are running the Fibre Channel Protocol consume a domain ID. This domain ID limits the number of switches that you can deploy in data centers.*

*As data centers grow with an increasing number of devices in a converged fabric, the operational and management issues become more complex.*

*Interoperability with third-party switches is also a significant concern.*

## Cisco NPV Mode

*Another mode in which the Cisco MDS switch operates is N-Port Virtualization (NPV) mode. A switch that is operating in Cisco NPV mode relays received Fibre Channel frames from the server-facing ports. This relay occurs over an uplink to an upstream device in the SAN core for processing. The upstream SAN core switch provides F-port functionality (such as login and port security) and all the Fibre Channel switching capabilities.*

*Cisco NPV mode aggregates multiple local N ports into one or more external N port links. Switches operating in Cisco NPV mode do not join the fabric; they pass traffic between core switch links and end devices. Cisco NPV mode also simplifies the scalability and connectivity of the edge Fibre Channel topology. Most of the Fibre Channel-related configuration is removed from the Cisco NPV mode edge switch, and the switch is now configured only on the core SAN switch. The edge switch administrator now must configure only a minimal set of Fibre Channel functions.*

*A Cisco MDS device operating in Cisco NPV mode has the following characteristics:*

- *Minimal Fibre Channel switch operation.*

- *Fibre Channel operation is simplified in these ways:*

1. *Most Fibre Channel services are switched off.*

2. *There are fewer SAN switches to manage.*

3. *The NPV-enabled switch does not require a domain ID.*

4. *Standards-based implementation is interoperable with other vendors.*

5. *Fibre Channel switching is performed upstream in the SAN.*

6. *This functionality eliminates the need for network administrators to manage the SAN.*

*With Cisco NPV mode, Cisco MDS switches relay the FLOGI and Cisco Fabric Service parameters to the upstream Fibre Channel switch. The Cisco MDS switch operates as a proxy N port (NP port) and performs no Fibre Channel switching itself. There are no local switching and zoning checks. The Cisco NPV mode device appears as a host to the core SAN switches and as a Fibre Channel switch to the devices that are attached to it.*

*The figure shows the devices that are used in NPV mode configuration, including the host bus adapter (HBA).*

![Cisco NPV Mode](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/cisco_NPV_mode.png)

*Cisco NPV mode devices increase the scalability of the fabric and eliminate many of the switch-to-switch interoperability issues by not providing most Fibre Channel services. These devices also simplify network management because they do not participate in the Fibre Channel topology. Cisco NPV mode devices do not require an assigned Fibre Channel domain ID, and they do not participate in Fibre Channel operations.*

*The standards-based NPV implementation is compatible with any upstream SAN switch.*

*You can configure Cisco NPV mode on an edge switch to support fabric logins from each device that is connected through the NPV edge switch. The upstream Fibre Channel switch must support the N-Port ID Virtualization (NPIV) feature.*

## Cisco NPV Switches

*NPV is not supported on all devices. Also, you cannot use the NPIV capability of the upstream switch (required for NPV switch operation) on all devices.*

*NPV capabilities are supported on the following edge switches:*

- *Cisco Nexus 3000 Series Switches*

- *Cisco Unified Computing System (Cisco UCS) 6300, 6400, and 6500 Series Fabric Interconnects (NPV is the default)*

- *Cisco Multilayer Director Switch (Cisco MDS) 9148 and 9396S Multilayer Fabric Switches*

- *Cisco Nexus 9300 and 9200 Series Switches*

- *Cisco Nexus 9504 and 9508 switches with many line cards*

*The NPIV capability (required on the upstream switch when the edge switch operates in NPV mode) is supported on the following switches:*

- *Cisco MDS 9700 Series Multilayer Directors*

- *Cisco MDS 9500 Series Multilayer Directors*

- *Cisco MDS 9220 Multiservice Modular Switches*

- *Cisco MDS 9300 Series Multilayer Fabric Switches*

- *Cisco MDS 9124V 64-Gbps 24-Port Fibre Channel switch*

- *Cisco MDS 9148V 64-Gbps 48-Port Fibre Channel switch*

- *Cisco MDS 9148 Multilayer Fabric Switch*

- *Third-party switches must support NPIV when connecting to an NPV-enabled switch.*

## Cisco NPV Mode: Edge Switch

*Edge switches in NPV mode act as initiators, not as switches, and their Fibre Channel port types are usually configured automatically.*

*When an edge switch is configured in Cisco NPV mode, the following occurs:*

- *It appears as a Fibre Channel switch to its connected hosts.*

- *It appears as an initiator (not a switch) to the upstream SAN core switch.*

- *The NPV-enabled switch does not consume SAN resources.*

- *Fibre Channel traffic is relayed from the host ports to the SAN core switch via one or more uplink ports.*

- *The SAN core switch provides all the Fibre Channel switching capabilities and functionality. The connected device must be a Fibre Channel switching device with NPIV enabled.*

- *NPV edge switches support the F port, virtual F port (VF Port), NP ort, and Switched Port Analyzer (SPAN) destination port (SD Port) types.*

## Cisco NPV Mode Implementation

*On a switch operating in Cisco NPV mode, the interfaces that connect to upstream Fibre Channel switches are called border interfaces or external interfaces. The interfaces that connect to hosts are called server interfaces.*

![Cisco NPV Mode Implementation](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/cisco_NPV_mode_implementation.png)

*A Cisco NPV-mode Fibre Channel switch interface also has an associated port type:*

- *A port that is connected to an HBA is an F port (native Fibre Channel).*

- *A port that is connected to another Fibre Channel switch is an NP port.*

*An NP port behaves like an N port but functions as a proxy for multiple N ports.*

*Converged Network Adapter (CNA) is an adapter technology which enables the adapter to process both Ethernet and Fibre Channel communication. This technology is commonly used in Cisco Virtual Interface Cards (VICs).*

## External Interfaces

*On a Cisco NPV-mode–enabled edge switch, an N port uplink is the connection from an edge switch NP port to the F port on the upstream core SAN switch. The NP port uplink must connect to an F port in NPIV mode on the connected Fibre Channel switching device.*

*In CLI commands output displays, NP port uplinks are called external interfaces. NP port uplinks must be native Fibre Channel interfaces.*

*When the physical NP port uplink is established, the NPV edge switch interface sends a FLOGI to the upstream core switch. The NPV edge switch interface (NP port) logs in to the core SAN switch as if the edge switch interface were an end device. The upstream SAN switch sees the NPV edge switch as simply an initiator.*

*You should use multiple NP port uplinks for resiliency and redundancy. NP port uplinks are not trunks, and you must configure each uplink in a virtual SAN (VSAN).*

*Subsequent FLOGIs from end devices that connect to the NPV edge switch are converted to fabric discovery (FDISC) messages. Then, they transmit on an NP port uplink in the same VSAN to the core SAN switch for processing. If an uplink in the same VSAN is not found, the FLOGI will fail.*

## Uplink Selection and Load Distribution

*When a server interface comes up, the NP port uplink interface that is in the same VSAN as the server interface with the minimum load is selected from the available NP port uplinks. This process is sometimes referred to as pinning the port.*

*Port pinning determines which port will use which physical uplink on the upstream device using NPV, because the same fabric can use several physical interfaces for communication.*

*When a new NP port uplink interface becomes operational, the existing load does not automatically redistribute to include the newly available uplink. Because the uplink choice happens when the interface comes up, only the server interfaces that become operational after the NP port uplink becomes operational can use the new N port uplink. The new NP port uplinks can be operational, but they carry little traffic if you enable them after the fabric is stable. This situation can lead to suboptimal fabric performance.*

*Manually reinitializing some or all the server interfaces will distribute server traffic to the new NP port uplink interfaces, but doing so may impact service.*

*You can replace this manual process with the disruptive load-balancing feature. Disruptive load balancing redistributes the server interfaces across all available NP port uplinks when a new N port uplink becomes operational.*

*NPV forcibly reinitializes the server interfaces that move to a different NP port uplink with the following impact:*

- *A system message is generated for each server interface that moves.*

- *The server performs a new login to the core switch.*

- *Traffic is disrupted to the attached end devices.*

*Storage traffic is very sensitive to disruptions, and for this reason, Cisco recommends that you enable the disruptive load-balancing feature only when you add new NP port uplinks. Disable this feature after server interface redistribution completes. Not taking this action can result in flapping server ports.*

*Note: Flapping is a term that describes an interface error where an interface keeps changing states from online to offline and online again. This error can result from configuration or hardware issues.*

## NPV Traffic Maps

*A traffic map allows you to administratively specify the NP port uplinks of an NPV-enabled device for pinning a server interface.*

*Use it to link a set of servers to a specific core switch. It associates the server interfaces with a set of NP port uplink interfaces that all connect to that core switch. The example is shown in the following figure:*

![NPV Traffic Maps](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/NPV_traffic_maps.png)

*The NPV traffic map provides the following features:*

- *It facilitates traffic engineering by allowing configuration of a fixed set of NP port uplinks for a specific server interface (or range of server interfaces).*

- *It allows the server interface to always connect to the same NP port uplink after the interface reinitialization or switch reboot. (This capability ensures the correct operation of the persistent Fibre Channel ID feature.)*

*When you configure an NPV traffic map for a server interface, the switch must select only one interface from the NP port uplinks in its traffic map for a specific server interface. Server interfaces cannot use an NP port uplink that is not in its defined set, even if all its interfaces are down. If no specified NP port uplinks are operational, the server interface remains in a nonoperational state.*

*NPV traffic map is an optional feature and is disabled by default. As the name implies, it can be enabled only on switches that operate in NPV mode.*

## Trunking NP Ports

*VSAN trunking enables interconnect ports to transmit and receive frames in more than one VSAN, over the same physical link, using Enhanced Inter-Switch Link (EISL) frame format.*

*It is possible to configure NP port uplinks of a switch that works in the NPV mode as trunk ports. They become operational as trunking NP ports and are referred to as TNP ports. A TNP port may connect to a TF port to create a link to a core NPIV switch from an edge NPV switch. The TF ports must be in NPIV mode on the Fibre Channel switch.*

![Trunking NP Ports](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/trunking_NP_ports.png)

## Cisco NPV Mode Configuration

*Enabling and disabling Cisco NPV mode is disruptive and requires a switch reboot.*

*Before placing a Cisco MDS switch into Cisco NPV mode, you should save the running configuration to the bootflash, external server, or other location. The switch will issue a warning to prompt you to confirm that you want to enable NPV and the reload the switch. Confirming the warning will erase the configuration and reload the switch.*

*Once the system reload is complete, the switch will have a blank configuration, except for management information such as user credentials and the management IP address. If the previous configurations were saved to bootflash or to an external server, you can reuse portions. You can copy and paste configuration components from the saved file to accelerate the reconfiguration process.*

*The core-facing interfaces function as NP ports. To configure NP uplinks, you must map them to a VSAN. An NP uplink must be in the same VSAN as each server interface. If a server interface has no NP uplink in the same VSAN, the server interface will be disabled.*

*The NPV switch inspects the FLOGIs and keeps a table of the interface, VSAN, World Wide Name (WWN), and Fibre Channel ID.*

*If required, you can configure NPV traffic maps. This process allows the administrator to determine which uplink a server will use or provide consistency in the selection of uplinks.*

*Take the following main steps when you are configuring NPV.*

![NPV Configuration](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/NPV_configuration.png)

## Cisco Fabric Interconnects and NPV

*Fibre Channel is supported on Cisco MDS switches and Cisco Nexus Series switches. However, another device also supports Fibre Channel and can be frequently found in the data center—Cisco UCS Fabric Interconnects. The Fibre Channel switching mode determines how fabric interconnects behave as a Fibre Channel switching device between the servers and storage. Fabric interconnects can operate in one of two Fibre Channel switching modes: end-host mode or switch mode.*

*Switch mode is the traditional Fibre Channel switching mode that allows the fabric interconnect to connect directly to a storage device. Enabling Fibre Channel switch mode is useful in pod models where there is no SAN, such as a single Cisco UCS system that connects directly to storage. This model is also useful where a SAN exists with an upstream Cisco MDS device.*

*The switch mode is not the default Fibre Channel mode and to enable it on the fabric interconnects, a separate license is required.*

*End-host mode allows the fabric interconnect to act as an end host to the connected Fibre Channel networks, representing all servers (hosts) connected to it through virtual HBAs (vHBAs). This action is achieved by pinning (either dynamically pinned or hard-pinned) vHBAs to Fibre Channel uplink ports. It makes the Fibre Channel ports appear as server ports (N ports) to the rest of the fabric.*

*In terms of Fibre Channel communication, the end-host mode is synonymous with NPV mode. This functionality means that fabric interconnects do not consume the domain ID and that FI uplinks become NP ports. End-host mode is the default Fibre Channel switching mode.*

*Note: When you enable end-host mode and a vHBA is hard pinned to an uplink Fibre Channel port, if this uplink port goes down, the system cannot re-pin the vHBA. Therefore, the vHBA remains down.*

## NPIV Mode 

*N-Port ID Virtualization (NPIV) mode allows one physical N port on a host to have multiple port WWNs (pWWNs) and because of that multiple Fibre Channel IDs. Each application or virtual machine residing on a host uses a different virtual pWWN that is used exactly in the same way as a physical pWWN. This setup allows you to implement access control, zoning, and port security at the application or virtual device level.*

*If NPIV mode is unavailable, a single F port on a switch expects only one FLOGI from any single N port that has only one physical pWWN. In this case, the fabric sees all the applications and virtual machines on a host as a single entity. For this reason, presenting a Logical Unit Number (LUN) to only one virtual machine is impossible.*

![NPIV Mode](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/NPIV_mode.png)

*The NPIV feature is required in the following situations:*

- *On Cisco Nexus 9000 Series switches to support connected virtualized servers that host multiple virtual machines and operating systems that connect through an NPIV-enabled HBA.*

- *On the core Fibre Channel switch when the edge switch is configured in Cisco NPV mode.*

- *On a server interface that supports multiple end devices or applications that require separate storage.*

- *On any device where an F port is expected to manage multiple FLOGIs.*

*NPIV usage applies to virtual server applications such as VMware, Microsoft Hyper-V, and Linux Xen servers. To benefit from NPIV, you must enable it on a virtual machine level and on a switch that connects to a host where virtual machines reside. You can enable NPIV on a Cisco NX-OS device with the ```feature npiv``` command, which is a nondisruptive command and will not erase switch configuration.*

*On Cisco MDS 9000 Series Multilayer Switches, the NPIV feature is enabled by default since version 8.4(2).*

*In the following figure, you can see an example of the edge switch (configured in NPV mode) that connects to a core switch. The switch in NPV mode does not require a Fibre Channel ID and forwards FLOGI requests and other Fibre Channel frames to an upstream switch. Remember that, in this case, you must enable the NPIV feature on the core switch, because the NPV switch connected to it behaves as an NPIV-enabled host.*

![NPIV Mode 2](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/NPIV_mode2.png)

*Another possible scenario includes a switch with the enabled NPIV feature, another switch with the enabled NPV feature, and a server on which multiple virtual machines are running. You can also see that the switch in NPV mode has NPIV mode enabled. In this case, it is the nested NPIV.*

![NPIV Mode 3](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/NPIV_mode3.png)

### Additional Notes and Conclusions:

**The Big Picture (TL;DR first)**

*NPIV = many identities on one port*

*NPV = no fabric brain, just a fabric proxy*

Together, they exist to **make large virtualized environments sane** without exploding your fabric with ports, domains, and zoning chaos.

**NPIV** — ***One Port, Many Personalities***

*What it is:*

NPIV lets **multiple WWPNs share a single physical N Port.**

*Why it exists:*

Virtualization broke the “one server = one WWPN” assumption. Each VM needs its *own* identity for:

- zoning

- LUN masking

- security

- SAN sanity

**Key takeaways:**

- One physical HBA → many virtual WWPNs

- Each VM looks like a *real host* to the SAN

- Requires **NPIV support on the switch AND host**

- Common in ESXi, Hyper-V, UCS

**Memory hook:** *NPIV = Identity multiplication*

**NPV** — ***The Fabric That Isn’t***

*What it is:*

NPV mode turns a switch into a **fabric edge device**, not a fabric participant.

*What it removes:*

- No domain ID

- No zoning database

- No name server

- No fabric services

*What it does instead:*

- Acts like a **giant host**

- Forwards FLOGI/PLOGI upstream

- Relies entirely on the **core switch**

*Why it exists:*

Large environments hit limits:

- domain IDs

- zoning sprawl

- management pain

NPV centralizes *all intelligence* in the core

**Memory hook:** *NPV = Fabric minimalism*

**NPV + NPIV** — *Why They’re Married*

This is the important part Cisco loves but explains poorly.

*Without NPIV:*

- NPV switch = one WWPN → terrible for virtualization

*With NPIV:*

- NPV switch presents **many virtual N Ports upstream**

Core switch still sees:

- individual WWPNs

- separate hosts

- clean zoning targets

Result:

- Edge = dumb, scalable, cheap

- Core = smart, controlled, authoritative

**Memory hook:** *NPV scales ports, NPIV scales identities*

**Zoning & Security Implications**

- Zoning is *always done on the core*

- Edge switches never decide who talks to whom

Each VM still gets:

- its own zone membership

- its own LUN access

- proper isolation

This is *zero-trust SAN design*, long before zero-trust was trendy.

**Operational Reality (What You’ll Actually See)**

- FLOGIs appear *on the core*, not the NPV switch

- FCNS lives *only in the core*

- Edge switch feels eerily quiet (that’s the point)

- Troubleshooting always walks *upstream*

**Final One-Glance Mental Model:**

```
VMs
 ↓ (NPIV: many WWPNs)
Edge Switch (NPV: no brain)
 ↓ (forward everything)
Core MDS (real fabric)
 ↓
Storage
```

NPV/NPIV is Unix philosophy applied to SANs: *Do one thing, do it well, and let the core think.*
