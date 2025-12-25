# Describing FCoE

*Ethernet and Fibre Channel hardware and protocol requirements prevent several native protocols from existing on the same hardware physical links. The need for I/O consolidation of these protocols introduced a solution that uses encapsulation of one protocol in another to provide connectivity.*

*In this course, you will learn about the Fibre Channel over Ethernet (FCoE) protocol functions and hardware adapters that support FCoE. You will also see the protocols that require support on the Converged Network Adapter (CNA). You will learn the FCoE encapsulation features and the supporting protocols that enable the reliable communication that the Fibre Channel Protocol requires.*

## FCoE Architecture 

*In a typical data center, you would have two separate networks, one for Ethernet and one for Fibre Channel. To support various types of networks, the traditional approach (shown on the left side of the figure) uses separate redundant interface modules for each network. It includes Ethernet Network Interface Cards (NICs), Fibre Channel interfaces in their servers, and redundant pairs of switches at each layer in the network architecture. The use of parallel infrastructures increases capital cost, makes data center management more difficult, and diminishes business flexibility.*

![FCoE Architecture](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/FCoE_arhitecture.png)

*The consolidation of I/O in the data center (shown in the right side of the figure) brings the Fibre Channel and Ethernet networks into a single, integrated infrastructure. An important pillar of this consolidated approach is FCoE.*

*Note: Many terms are used for the consolidation of l/O: converged Ethernet, unified fabric, unified wire, converged enhanced Ethernet, data center Ethernet, and data center bridging. They all mean one thing: Ethernet and Fibre Channel on the same infrastructure.*

## FCoE Overview

*Unified fabric is the convergence of all the various data center I/O technologies over Ethernet. FCoE traffic consists of a Fibre Channel frame that a switch encapsulates within an Ethernet frame:*

- *The switch must support “jumbo” frames because a typical Fibre Channel payload is up to 2112 bytes.*

- *It translates between the Fibre Channel and Ethernet worlds by mapping Fibre Channel IDs to Ethernet MAC addresses.*

- *This approach ensures lossless delivery of Fibre Channel traffic and keeps all upper-layer Fibre Channel services. Examples include domain IDs, Fabric Shortest Path First (FSPF), fabric login (FLOGI), and others.*

![FCoE Overview](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/FCoE_overview.png)

*The FCoE protocol is based on the Fibre Channel layers that the ANSI T11 committee defines. FCoE replaces the lower layers of Fibre Channel with unified fabric I/O consolidation over Ethernet. Upper-layer Fibre Channel services, such as domain IDs, FSPF, Fibre Channel Name Service (FCNS), FLOGI, zoning, stay the same as in the Fibre Channel world.*

*The Fibre Channel frame, including FC Header, Payload, and Cyclic Redundancy Check (CRC), is encapsulated in FCoE. FCoE adds the FCoE header and End of Frame (EOF) fields. The Ethernet frame uses EtherType FCoE and appends the Frame Check Sequence (FCS) for error detection.*

*Because the Fibre Channel payload is typically up to 2112 bytes, a standard Ethernet frame of 1500 bytes is unable to accommodate Fibre Channel traffic. This large Maximum Transmission Unit (MTU) is why FCoE encapsulates Fibre Channel traffic into jumbo frames. The default MTU in FCoE is 2240 bytes.*

*Ethernet uses MAC addresses for communication and Fibre Channel uses Fibre Channel IDs. FCoE must therefore perform translation between MACs and Fibre Channel IDs.*

*Fibre Channel is inherently a lossless type of traffic, and Ethernet is inherently a lossy type of traffic. This difference is why FCoE must make special accommodations to transport traffic that needs lossless transport over infrastructure that, by default, expects lossy behavior. FCoE accommodates Fibre Channel traffic on Ethernet by following data center bridging standards.*

## Fibre Channel and FCoE Differences

*From a Fibre Channel perspective, FCoE introduces just another type of cable (Ethernet), while from an Ethernet perspective, FCoE represents just another upper-layer protocol. The following figure depicts the native Fibre Channel and FCoE correlations.*

![Fibre Channel and FCoE Differences](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/FC_and_FCoE.png)

*The solution in FCoE is the concept of virtual Fibre Channel (VFC) interfaces. It introduces a small set of control plane functions to build virtual links among pairs of VFC interfaces. Multiple VFC interfaces can be on the same physical Ethernet interface of a dual-stack switch.*

*After the virtual links establish among pairs of VFC interfaces, the result appears to the Fibre Channel stack as a set of point-to-point connections. These connections behave exactly like regular Fibre Channel connections, regardless of the number of FCoE pass-through switches that you physically insert between the actual Fibre Channel endpoints.*

*VFC is a logical representation of Fibre Channel interface to the Ethernet world.*

## Data Center Bridging

*Cisco Data Center Bridging (Cisco DCB) architecture is based on a collection of open standards, Ethernet extensions that are developed through the IEEE 802.1 working group. These standards are designed to improve and expand Ethernet networking and management capabilities in the data center. Cisco DCB helps ensure delivery over lossless fabrics and I/O convergence onto a unified fabric.*

*Cisco DCB is a collection of these IEEE standards that enable FCoE transport of inherently lossless traffic over inherent infrastructure that is susceptible to loss:*

- ***PFC:*** *Priority Flow Control (PFC) is defined in IEEE 802.1Qbb and provides lossless delivery for selected types of traffic.*

- ***ETS:*** *Enhanced Transmission Selection (ETS) is defined in IEEE 802.1Qaz and enables bandwidth management and priority selection.*

- ***DCBX:*** *Data Center Bridging Exchange (DCBX) is defined in IEEE 802.1Qa and is used as protocol for exchanging parameters between DCB devices and extending Link Layer Discovery Protocol (LLDP).*

- ***QCN:*** *Quantized Congestion Notification (QCN) is defined in IEEE 802.1Qau and provides congestion awareness and avoidance (optional).*

*DCBX uses LLDP (standardized in IEEE 802.1AB) to negotiate FCoE compatibilities on devices. DCBX-exchanged parameters are packaged into organizationally specific type, length, value (TLV) parameters. Therefore, if you want to use FCoE on a device, you must enable LLDP on that device.*

## FCoE N-Port Virtualization

*FCoE N-Port Virtualization (NPV) works very similar to Fibre Channel NPV. The FCoE device that works in NPV mode is called a FCoE NPV bridge. It emulates an FCoE-capable host with multiple FCoE ports (eNodes), each with a unique FCoE ports MAC address. It also acts as a proxy for a Fiber Distributed Data Interface (FDDI) Interface Processor (FIP) control messages and the FLOGI between the CNA and the FCoE Fibre Channel Forwarder (FCF) device. The FCF device supports Fibre Channel functionality and FCoE functionality and can operate in NPIV mode. An example of such a device is the Cisco Multilayer Director Switch (Cisco MDS) 9000 Series Multilayer Switch.*

*An FCoE NPV is virtual SAN (VSAN)-aware and will take VSANs into account when mapping (or pinning) logins from the CNA to an FCF uplink. FLOGI from the initiators (eNodes), are load-balanced between the two links of each port channel interface in a virtual network port (VNP) that connects the FCoE NPV and FCF devices. By default, the VNP port is enabled in trunk mode.*

*Note: The FCoE NPV feature does not convert FLOGI to Fabric Discovery (FDISC) like Fibre Channel NPV.*

![FCoE N-Port Virtualization](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/FCoE_NPIV_virtualization.png)

## Lab: Review Unified Ports on a Cisco Nexus Switch and Implement FCoE

*In data centers across the world, you will find many communication protocols, and they all require hardware to run on. This requirement can become an issue when devices do not support all the necessary protocols. For this reason, SAN networks initially ran over a separate set of network hardware. For Fibre Channel SAN and Ethernet, this limitation is solved by the unified port feature that Cisco introduced to the networking hardware. This feature allows a unified set of hardware to run both native Fibre Channel and native Ethernet, as well as Fibre Channel over Ethernet links through the FCoE protocol.*

*Cisco Nexus unified ports allow you to configure a physical port on a Cisco Nexus device switch as Ethernet, FCoE, or native Fibre Channel ports.*

*FCoE allows you to encapsulate Fibre Channel traffic over a physical Ethernet link by using a unique EtherType that carries FCoE traffic and standard Ethernet traffic on the same link.*

*FIP allows the switch to discover and initialize FCoE-capable entities that are connected to an Ethernet LAN. FIP performs device discovery, initialization, and link maintenance. The initiator system can mount remote Fibre Channel LUNs normally as if a native Fibre Channel connectivity is available. However, you must configure the network properly on both Ethernet and Fibre Channel levels.*

**Additional Notes:**

Think of **unified ports** as Cisco saying “one set of muscles, multiple fighting styles.” Instead of separate hardware for Ethernet and Fibre Channel, the same physical ports can run **Ethernet, native FC, or FCoE,** depending on how you configure them. **FCoE** is basically Fibre Channel wearing an Ethernet coat — FC frames are encapsulated inside Ethernet using a special EtherType, so storage and regular traffic can share the same wire. **FIP** is the social protocol: it discovers FCoE-capable devices, initializes them, and keeps the relationship alive, making the host believe it’s talking to a real FC fabric. The magic only works if **both worlds are configured correctly** — Ethernet (VLANs, DCB, lossless behavior) *and* Fibre Channel (VSANs, zoning), otherwise the illusion collapses.

### Verify the Device Connectivity and SAN Configuration

**1. Why this step exists (big picture):**

This phase is about answering one question: ***“Is my Nexus switch physically capable, properly licensed, and already seeing SAN devices before I touch FCoE?”***

We’re validating *hardware → licenses → ports → fabric visibility* in that order.

**2. License sanity check (what actually matters here):**

```
N5K-12# show license usage
```

*What you’re really looking for:*

- ```FC_FEATURES_PKG``` → **In use** (native Fibre Channel capability)

- ```FCOE_NPV_PKG``` → present (even if unused, grace is fine for lab)

If FC features weren’t available, *everything later would silently fail.*

**3. Hardware capability check (unified ports confirmed):**

```
N5K-12# show module
```

Key takeaway:

- ```N5K-C5548UP``` = **Unified Ports platform**

- This hardware can flip ports between **Ethernet / FC / FCoE**

Mental hook: “UP = *One port, many personalities.”*

**4. Port role overview:**

```
N5K-12# show interface brief
```

This tells you:

- Which ports are Ethernet vs Fibre Channel

- Which ones are already up and participating in SAN

Think of this as your **port role map** before touching configs.

**5. FLOGI = who is directly plugged into me:**

```
N5K-12# show flogi database
```

Key truths:

- FLOGI only happens **between directly connected devices**

- Seeing ```vfc1000``` + ```SRV_POD12``` means:

1. ESXi host is alive

2. vFC ↔ fabric login is working

Mental hook: *“If it’s in FLOGI, it’s physically next to me.”*

**6. FCNS = who exists in the fabric (global view):**

```
N5K-12# show fcns database
```

This is your **SAN directory service:**

- FCNS = ARP + DNS for Fibre Channel

- Shows **both local and remote devices**

- Used to pivot from WWNs → roles → vendors

Technique worth remembering: *FLOGI gives you the FCID → FCNS gives you the story behind it.*

**7. Why this lookup flow matters:**

You should always do this chain when troubleshooting SAN:

1. ```show flogi database``` → find FCID / interface

2. ```show fcns database``` → identify device, vendor, role

That’s how you *prove* connectivity without guessing.

**8. Interface descriptions (small thing, huge payoff):**

```
N5K-12(config)# int fc 1/21-22
N5K-12(config-if)# switchport description Connects to MDS-12
```

and...

```
N5K-12(config)# interface eth 1/9
N5K-12(config-if)# description Connects to ESX vmnic 0
```

Verification:

```
N5K-12# show interface description | inc Connects
```

Why this matters:

- SAN troubleshooting happens months later, under pressure

- Descriptions save *hours of archaeology*

Mental hook: *“Future-you is tired. Label things.”*

**9. State-of-the-world snapshot (so far):**

```
[ESXi Host]
   |
 (FCoE over Eth1/9)
   |
[N5K-12] —— FC1/21-22 —— [MDS-12] —— Core MDS —— NetApp
```

- ESXi logged in via vFC (FLOGI ✔)

- Nexus sees both server and storage (FCNS ✔)

- Hardware + licenses ready for FCoE work

**TL;DR (cookbook spine):**

- Licenses confirm *capability*

- Modules confirm *hardware support*

- FLOGI confirms *direct adjacency*

- FCNS confirms *fabric visibility*

- Descriptions prevent *future suffering*

### Verify the FCoE Configuration

This is a *verification-focused lab*, so the mental model is: *“prove that Ethernet, FCoE, and Fibre Channel are all correctly stitched together.”*

**1. VLAN ↔ VSAN mapping (the FCoE keystone):**

This is the *critical* FCoE concept.

```
N5K-12# show vlan fcoe
Original VLAN ID        Translated VSAN ID       Association State
1000                   1012                    Operational
```

Why this matters:

- VLAN **1000** is the *Ethernet carrier*

- VSAN **1012** is the *Fibre Channel identity*

- FCoE traffic arrives as **Ethernet (VLAN 1000)** → gets **translated into VSAN 1012**

- If this mapping is broken, *nothing SAN-related works*, even if everything else looks fine

Memory hook: *FCoE = VLAN outside, VSAN inside*

**2. VSAN existence and health:**

You’re verifying that the SAN “universe” exists and is operational.

```
N5K-12# show vsan
vsan 1012 information
  state: active
  operational state: up
```

Why this matters:

- VSAN 1012 must be **active + up**

- If the VSAN is down, zoning, FLOGI, FCNS, and storage visibility all silently fail

**3. Which ports belong to which VSAN:**

This tells you *who participates in the SAN.*

```
N5K-12# show vsan membership
vsan 1012 interfaces:
  fc1/21
  fc1/22
  san-port-channel 10
  vfc1000
```

Key insight:

- ```vfc1000``` = **FCoE virtual FC port**

- ```fc1/21-22``` = **native Fibre Channel uplinks**

- This confirms **Ethernet + FC are in the same VSAN**

If ```vfc1000``` is missing here → FCoE is dead.

**4. The vFC interface (the FCoE bridge itself):**

This is the most information-dense command in the whole section.

```
N5K-12# show int vfc 1000
Bound interface is Ethernet1/9
Port mode is TF
Port vsan is 1012
Trunk vsans (up) (1012)
```

What actually matters here:

- **Bound interface:** ```Ethernet1/9``` → this is the physical wire

- **Port mode TF:** Trunking F-Port (fabric-facing FCoE)

- **VSAN 1012:** confirms correct SAN identity

- **Trunk vsans (up):** means FCoE is *actually forwarding traffic*

Memory hook: *No “Bound interface” = no FCoE*

**5. Ethernet side sanity check:**

You confirm the Ethernet half isn’t lying to you.

```
N5K-12# show vlan
1000 VLAN1000 active Eth1/9
```

Why this matters:

- VLAN 1000 must be **allowed on Eth1/9**

- If Eth1/9 isn’t in VLAN 1000 → FCoE frames never reach vfc1000

**6. FCoE control-plane confirmation:**

This proves the switch is acting as an FCoE Forwarder (FCF).

```
N5K-12# show fcoe
Global FCF details
FCF-MAC is 54:7f:ee:28:80:c0
FC-MAP is 0e:fc:00
```

What this confirms:

- The switch is advertising itself as an FCF

- FIP discovery and login can occur

- vFC MACs exist → FCoE sessions are alive

If ```show fcoe``` looks empty or weird → FIP/FCoE control plane is broken.

**The Big Picture:**

End-to-end FCoE chain:

```
ESXi NIC
  ↓
Ethernet1/9 (VLAN 1000)
  ↓
vfc1000 (VSAN 1012)
  ↓
Native FC ports (fc1/21-22)
  ↓
MDS / Core SAN / Storage
```

**If any single link** in that chain is misconfigured, FCoE fails *quietly.*

### Create an ESXi Datastore Using a Fibre Channel LUN

**1. Sanity check: SAN visibility (before touching ESXi)**

You verify from **N5K-12** that *both ends of the SAN conversation exist* — initiator **and** target.

```
N5K-12# show fcns database
```

Key takeaway:

- You must see **both:**

1. NetApp target (scsi-fcp)

2. ESXi host initiator ```[SRV_POD12]```

- If either is missing → zoning, VSAN, or FCoE is broken upstream.

Think of this as: *“Does the fabric know everyone who wants to talk?”*

**2. Why delete the existing datastore first?**

In the lab they force you to delete **LUN Datastore** to:

- Avoid VMFS signature conflicts

- Ensure the LUN is freshly discovered via **your new zoning**

- Prove the SAN config actually works end-to-end

In other words: *If zoning were wrong, the LUN would NOT reappear.*

**3. ESXi GUI flow (cookbook-friendly):**

Clean, deterministic sequence:

1. **Login to ESXi:**

- ```https://10.1.5.9```

- ```root / 1234QWer```

2. **Remove old datastore:**

- *Storage → Datastores*

- Select *LUN Datastore*

- *Actions → Delete → Confirm*

3. **Create new datastore:**

- *New Datastore*

- *Create new VMFS datastore*

- Name: ```LUN Datastore```

- Target: *NETAPP LUN*

- *Use full disk*

- *VMFS 6*

- *Finish → Yes*

Result:

- LUN is formatted

- VMFS metadata written

- Datastore mounts like a local disk

**4. What actually happened:**

From ESXi’s point of view:

- It sent *SCSI commands*

- Over *Fibre Channel*

- Encapsulated as *FCoE*

- Traversed *VLAN 1000 → VSAN 1012*

- Hit the NetApp array

This datastore:

- Looks local

- Behaves local

- Is absolutely not local

Performance depends on:

- SAN fabric health

- Buffer credits

- Congestion

- Storage array speed

**5. Final mental anchor:**

*Zoning enables visibility.*

*FCoE enables transport.*

*VMFS makes it usable.*

If ESXi sees the LUN → your fabric is alive and sane.

This lab is now concluded.
