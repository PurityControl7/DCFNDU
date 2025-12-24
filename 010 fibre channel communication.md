# Describing Fibre Channel Communication Between the Initiator Server and the Target Storage

*The serial connectivity of a Fibre Channel provides a mechanism for transporting Small Computer Systems Interface (SCSI) information across high-speed networks. Fibre Channel provides high-speed transport for the SCSI payload but overcomes the distance and limitations that come with parallel SCSI technology.*

*An initiator is the consumer of storage, typically a server that includes an adapter card that is called a host bus adapter (HBA). The initiator “initiates” a connection over the fabric to one or more ports on the storage system, which are called target ports. Target ports are the ports on your storage system that deliver storage volumes that are called target devices or logical unit numbers (LUNs) to the initiators.*

## Fibre Channel Layered Model

*The Fibre Channel Protocol (FCP) is composed of five layers: FC-0 through FC-4, each having its own functions. You will examine these layers and some of the Fibre Channel Generic Services that are provided to the SAN infrastructure.*

*The following are the main functions of each Fibre Channel layer, as illustrated in the following figure:*

- ***FC-4 ULP mapping:*** *This layer provides protocol mapping of the upper layer protocols (ULP) such as SCSI and Non-Volatile Memory Express (NVMe) using the Fibre Channel (FC in the figure) layers.*

- ***FC-3 generic services:*** *This layer provides the common services that are required for advanced features. Examples include striping, which is the idea of multiplying the bandwidth using multiple N Ports in parallel to transmit a single information unit across multiple links. It also serves in features like hunt groups and multicast.*

- ***FC-2 framing and flow control:*** *This layer provides the framing and flow control (also known as sequence control) that is required to transport the ULP over the Fibre Channel.*

- ***FC-1 encoding:*** *This layer provides encoding and decoding of signals and error control.*

- ***FC-0 physical interface:*** *This layer provides physical connectivity, including cabling, connectors, and other compnents.*

![Fibre Channel Layered Model](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/FC_layered_model.png)

### Additional Notes and Clarifications:

Think of **Fibre Channel like a postal system,** bottom to top. **FC-0** is the road and trucks (cables, optics, physics). **FC-1** is the envelope format and checksum—how bits are encoded so they survive the trip. **FC-2** is the real workhorse: framing, sequences, exchanges, and flow control—this is where “read/write actually happens.” **FC-3** is optional power-ups (striping, multicast, hunt groups), rarely used but conceptually like “link aggregation for SAN brains.” **FC-4** is the translator at the top, mapping SCSI or NVMe commands into FC so storage protocols can ride the fabric without caring how it works underneath.

If you remember one thing: **FC-2 does the heavy lifting, FC-4 speaks storage, everything below just makes sure bits arrive alive.**

## FLOGI Process

*The Fibre Channel Name Server (FCNS) is a distributed database that the switch implements. The fabric login (FLOGI) process occurs when a device logs in to the fabric using well-known addresses, as shown in the figure. Based on an example and using figures, you will learn the FLOGI and port login (PLOGI) processes.*

![FCNS](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/FCNS.png)

*The FCNS is a distributed service that implements a database in the fabric for storing information about each node:*

- *Fibre Channel IDs*

- *pWWNs and nWWNs*

- *Fibre Channel operating parameters, such as ULPs and classes of service*

*Each switch in a fabric contains its own resident name server, which is called a Distributed Name Server. Each Distributed Name Server within a switch is responsible for the name entries that are associated with the domain that is assigned to the switch. The Distributed Name Server instances synchronize their databases by using the Registered State Change Notification (RSCN) process.*

*When a client N Port wants to query the name server, it submits a request to its local name server via the well-known address for the name server. If the required information is unavailable locally, then the distributed name server within the local switch responds to the request by making the necessary inquiries of other distributed name server instances in the other switches. The communication between switches that is performed to acquire the requested information is transparent to the original requesting client.*

*The FCNS supports soft zoning by performing WWN lookups to verify zone membership. Zoning is enforced by providing information only about nodes that are in the zone of the requestor. Management applications that must obtain information about the fabric use the FCNS.*

### Well-Known Addresses

*Fibre Channel is a request-response protocol. Therefore, services are necessary that allow devices in a network to request a certain amount of information, and the service to respond with that information. A few generic services are used to manage a Fibre Channel network. All such services have a unique well-known address (FFFFFx). You will look at some common well-known addresses and the Cisco Fabric Services they represent. The well-known addresses are the highest 16 addresses in the 24-bit fabric address space.*

```
Generic Service                  | Address | Mandatory / Optional
---------------------------------|---------|----------------------
Broadcast Alias                  | FFFFFF  | Mandatory
Fabric Login Server              | FFFFFE  | Mandatory
Fabric Controller                | FFFFFD  | Mandatory
Name Server                      | FFFFFC  | Optional
Time Server                      | FFFFFB  | Optional
Management Server                | FFFFFA  | Optional
QoS Facilitator                  | FFFFF9  | Optional
Alias Server                     | FFFFF8  | Optional
Key Distribution Server          | FFFFF7  | Optional
Clock Synchronization Server     | FFFFF6  | Optional
Multicast Server                 | FFFFF5  | Optional
Reserved                         | FFFF F0 – FFFF F4 | Reserved
```

**My note (mental hook):** all these live at the *top end* of the FC address space (```FFFFFx```) → think *“fabric gods live at the ceiling.”* Mandatory ones are the bare minimum for a fabric to even exist; the rest are convenience, policy, or optimization brains layered on top.

*(...the continuation of Cisco's text...)*

*Well-known addresses allow devices to reliably access switch services. All services are addressed in the same way that an N Port is addressed. Nodes communicate with services by sending and receiving Extended Link Services (ELS) commands (frames) to and from well-known addresses.*

### Fabric Login

*Before an N Port can begin exchanging data with other N Ports, three processes must occur:*

1. *The N Port must log in to its attached F Port. This process is known as the FLOGI.*

2. *The N Port must log in to its target N Port. This process is known as the PLOGI.*

3. *FLOGI is the initial bootstrap process that is mandatory for N Ports and optional for NL Ports. FLOGI occurs when an N Port is connected to an F Port. It is used by an N Port to discover if a fabric is present. Communication with other N Ports may not be attempted until the FLOGI process is complete.*

*The FLOGI protocol follows this process:*

1. *The F Port sends a primitive not operational sequence (NOS in the figure) to the N Port.*

2. *When the N Port receives the not operational sequence, it responds with a primitive offline state sequence (OLS in the figure) to begin link initialization.*

![FLOGI](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/FLOGI.png)

1. *After the N Port begins the initialization process by sending an offline state sequence, the F Port tries to reset the port. It sends a long reach (LR in the figure) command.*

2. *The N Port responds with a Link Reset Response (LRR) command.*

![FLOGI2](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/FLOGI2.png)

1. *Now the link is active and IDLE fill words flow in both directions on the link.*

![FLOGI3](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/FLOGI3.png)

*Following link initialization, a new N Port uses a source ID (SID) of 0x000000 or an arbitrated loop physical address (AL-PA) of 0x0000 to indicate that the port is unidentified during the FLOGI. An existing N Port uses its existing port address as its SID.*

1. *After the N Port has established a link to its F Port, the N Port obtains a port address. The N Port performs this process by sending a FLOGI link services command to the switch login server (at the well-known address 0xFFFFFE).*

2. *The login server sends a Link Service Accept (LS_ACC) reply that contains the N Port address in the Destination ID field.*

*When an N Port performs a FLOGI and receives an accept (ACC) frame, that action indicates that the ACC came from another N Port. Then, the N Port that is logging in assumes that it is in a point-to-point configuration. The N Port immediately initiates PLOGI with the other N Port after completing the FLOGI.*

![FLOGI4](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/FLOGI4.png)

1. *After receiving a port address, the N Port logs in to the fabric name server at the address 0xFFFFFC. The N Port transmits its service parameters, such as the number of buffer credits it supports, its maximum payload size, and the supported class of services (CoS).*

2. *The name server responds with an LS_ACC frame.*

![FLOGI5](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/FLOGI5.png)

#### Additional Notes and Clarifications:

**Big picture first (mental anchor):**

Before Fibre Channel does *anything useful,* a host must (1) prove a fabric exists, (2) get an address, and (3) introduce itself to everyone who matters. Think of it as **plug in → wake up → get an ID → register → talk to targets.**

**The 3 required logins (the “order of reality”):**

1. **FLOGI (Fabric Login)** – *“Hello fabric, do you exist?”*

Mandatory bootstrap when an **N Port meets an F Port.** No FLOGI = no fabric life.

2. **Name Server registration** – *“Here’s who I am and what I can do”*

Happens *after* FLOGI, still fabric-facing.

3. **PLOGI (Port Login)** – *“Hello specific target, let’s talk SCSI”*

Happens *only after* the fabric groundwork is done.

Shortcut memory trick: **FLOGI → FABRIC, PLOGI → PEER**

**FLOGI, step-by-step (clean and linear):**

**Phase 1: Link initialization (pure PHY sanity)**

- F Port sends **NOS** → “You’re not operational yet”

- N Port replies **OLS** → “Okay, let’s reset”

- F Port sends **LR**, N Port replies **LRR**

- Link comes up → **IDLE fill words flow**

**Phase 2: Fabric discovery & address assignment**

- New N Port uses **SID = 0x000000** (aka “I have no identity yet”)

- N Port sends **FLOGI LS command to Login Server (0xFFFFFE)**

- Fabric replies **LS_ACC** with a **24-bit FC address**

This is where the port becomes *someone.*

**Important subtlety (often misunderstood):**

If an N Port receives an **ACC directly from another N Port,** it assumes **point-to-point,** *not a fabric.*

→ In that case, it **skips fabric services** and immediately starts **PLOGI.**

This is how **direct-attached FC** works.

**Name Server registration (fabric phonebook):**

- After address assignment, N Port logs into **Name Server (0xFFFFFC)**

Advertises:

- Buffer credits

- Max payload size

- Supported Classes of Service

Name Server replies **LS_ACC**

Now the fabric knows *who you are and what you support.*

**Final mental map:**

```
Cable up
 ↓
Link init (NOS → OLS → LR/LRR)
 ↓
FLOGI → get FC address
 ↓
Register with Name Server
 ↓
PLOGI to target
 ↓
Actual SCSI I/O
```

**One-liner to remember everything:** *FLOGI proves the fabric, Name Server publishes you, PLOGI starts the real conversation.*

### Port Login

*PLOGI allows the requested N Port to create a communication channel with the remote N Port, with which it wants to communicate, by setting and exchanging operational parameters.*

*After completing the FLOGI process, the N Port can log in to another N Port by using the PLOGI protocol. PLOGI must be completed before the nodes can perform a ULP operation.*

*The PLOGI protocol follows this process:*

1. *The initiator N Port sends a PLOGI frame that encapsulates the N Port operating parameters in the payload.*

![PLOGI](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/PLOGI.png)

1. *The target N Port responds to the initiator N Port by sending an LS_ACC frame that specifies the target N Port operating parameters. The operating system driver that manages the initiator N Port stores this information in a parameter block.*

![PLOGI 2](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/PLOGI2.png)

*An N Port can be logged in to multiple N Ports simultaneously. N Ports typically perform a process logout (PRLO) only when one of the nodes goes offline.*

#### Additional Notes and Clarifications:

Think of **PLOGI as the “actual handshake” between two endpoints,** while FLOGI was just getting permission to exist in the fabric. After FLOGI says *“you’re allowed in here”*, PLOGI says *“okay, you and I specifically can talk, and here’s how.”* The initiator sends its capabilities (buffers, payload size, service classes), the target replies with its own, and both sides lock those parameters in like a negotiated contract. No PLOGI, no SCSI/NVMe — upper-layer traffic is **forbidden until this pact is signed.**

Mental hook: **FLOGI = passport control, PLOGI = private conversation agreement.** One N Port can juggle many PLOGIs at once, and PRLO is basically hanging up the phone only when someone leaves the room or dies dramatically.

### Port and Address Discovery

*After FLOGI and PLOGI are complete, the N Port can use the following ELS commands. These commands retrieve updated information or verify information about port addresses and service parameters:*

- *An initiator N-Port sends a Discover Address (ADISC) command to verify that the addresses of the target have not changed.*

- *Fabric discovery (FDISC) is used if subsequent logins transmit from the same E Node for different servers. FDISC also finds virtual machines after an E Node performs an initial FLOGI to log in to a switch. This command is used with NPV mode.*

- *An N Port initiates a Port Discovery (PDISC) command to verify the service parameters of another N Port.*

*These commands allow ports to query and verify fabric and port parameters without performing PLOGI. They force a logout of the current session.*

### Process Login

*PRLI is performed using the ELS PRLI command. PRLI allows one or more images at one N Port to be related to corresponding images at another N Port, creating an image pair.*

*After completing the PLOGI protocol, each N Port knows about the Fibre Channel operating parameter capabilities of the other. At this point, the driver for the initiator port can use the PRLI protocol to open a channel with the driver for the target port. The PRLI protocol establishes a session between two FC-4 logical processes.*

*The PRLI protocol follows this process:*

1. *The initiator sends a PRLI frame that contains information about its ULP support.*

![PRLI](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/PRLI.png)

1. *The target port responds with an LS_ACC frame that contains details about its ULP support. At this point, a channel has successfully opened, and communication can now take place. The relationship between the initiator process and the target process is known as an image pair.*

![PRLI 2](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/PRLI2.png)

1. *When the initiator has finished exchanging data with the target, the initiator sends a PRLO frame.*

2. *The target responds with an ACC frame, and the image pair is then terminated.*

![PRLI 3](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/PRLI3.png)

*At this point, the image pair must be established again before further communication can take place.*

#### Additional Notes and Clarifications:

**PRLI is the “ULP handshake”**, and here’s the clean mental model:

FLOGI says *“I exist in the fabric”*, PLOGI says *“you and I can talk”,* and **PRLI** says ***“what exactly are we going to talk as?”.***

PRLI binds **FC-4 personalities** (like SCSI initiator ↔ SCSI target) into an **image pair,** which is basically *one logical session per protocol per port.*

After PRLI succeeds, **real I/O can finally flow;** before it, everything was just introductions and capability exchange. PRLO is simply the polite goodbye—tear down the image pair, and if you want more I/O later, you must PRLI again.

Memory hook: **FLOGI = fabric, PLOGI = peer, PRLI = role** — *where am I, who are you, and what are we doing together.*

## Fibre Channel Flow Control

*In a Fibre Channel environment, it is important to ensure that frames are not lost between the initiator and target. Therefore, you must provide a lossless environment. In Fibre Channel, the receiver is in control rather than the sender, as in an Ethernet network.*

*To improve performance under high traffic loads, Fibre Channel uses a credit-based flow-control strategy. The receive (Rx) Port must issue a credit for each frame that the transmitter sends. This strategy prevents frames from being lost when the Rx Port runs out of free buffers. Preventing lost frames maximizes performance under high-traffic-load conditions because the transmit (Tx) Port does not need to resend frames.*

*The figure shows a credit-based flow-control process:*

- *The Tx Port counts the number of free buffers at the Rx Port.*

- *Before the Tx Port can send a frame, the Rx Port must notify the Tx Port that the Rx Port has a free buffer and is ready to accept a frame. When the Tx Port receives the notification, it increments its count of the number of free buffers at the Rx Port.*

- *The Tx Port sends frames only when it knows that the Rx Port can accept them.*

![FC Flow Control](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/FC_flow_control.png)

*The base credit management method works as follows:*

- *When the Tx Port sends a PLOGI request, the Rx Port responds with an ACC frame. The ACC frame includes information on the size and number of frame buffers that it has (BB_Credit).*

- *The Tx Port stores the BB_Credit value in a table. The Tx Port also stores another value, the buffer-to-buffer credit count (BB_Credit_CNT), which represents the number of used buffer credits (the number of transmitted frames). The BB_Credit_CNT is set to zero after the ports complete the login process. Each time the Tx Port sends a frame, the BB_Credit_CNT is incremented.*

- *Upon receiving the frame, the Rx Port processes the frame and moves it to the ULP buffer space.*

- *The Rx-Port then sends a receiver ready (R_RDY) acknowledgment (ACK) signal back to the Tx Port, informing it that a buffer is available.*

- *When the Tx Port receives the R_RDY signal, it then decrements its BB_Credit_CNT.*

*The Tx Port never allows the BB_Credit_CNT (the count of frames that have been sent but not yet acknowledged) to exceed the BB_Credit (the total number of frame buffers in the Rx Port). If the Tx Port cannot confirm that the Rx Port has a free buffer, it stops sending frames. The Tx Port sends only when the BB_Credit_CNT is less than BB_Credit.*

## Lab: Validate FLOGI and FCNS

*Fabric Login (FLOGI) and Fibre Channel Name Server (FCNS) are Fibre Channel functionalities that you can use with Cisco Nexus and Cisco MDS ```show``` commands to analyze the status of the Fibre Channel communication.*

*Fibre Channel switches have domain IDs that identify them in the fabric. The principle switch automatically assigns these domain IDs. The principal switch is automatically elected (no configuration necessary), but you can also statically assign domain IDs if desired.*

*When a device connects to the fabric switch, it will perform a FLOGI. The FLOGI tells the fabric about your World Wide Node Name (WWNN) and port World Wide Name (pWWN) [sometimes referred to as World Wide Port Name (WWPN)]. WWNNs are similar to MAC addresses in the Ethernet world. They can be either burned-in physical addresses or assigned addresses from a pool, such as when using Cisco virtual interface cards (VICs). WWPNs are used in zoning and define the node port identifier.*

*When you connect your server or storage, it will send a FLOGI request. The FLOGI request serves two purposes:*

- *The Fibre Channel Identifier (FCID) is the WWPN connection to this port from the FLOGI server.*

- *It exchanges buffer credits information with the switch.*

*The fabric will then assign a logical FCID to each WWPN to use for switching in the data plane. Think of FCIDs that are assigned to WWPNs as IP addresses.*

*The FCNS creates the WWPN-to-FCID table, similar to the ARP cache and DNS. The FCNS database is global to the fabric. Because no other switches are in the fabric yet, you see the same output as the FLOGI database.*

### Additional Notes:

This is a perfect place to pause and build a mental anchor before the lab.

Think of **FLOGI + FCNS as the Fibre Channel version of “plugging into the network and getting an identity.”** When a host or storage port connects, it does a **FLOGI** to the switch, basically saying: *“Hi, I’m this WWNN/WWPN, here are my buffer credits—can I join the fabric?”* The **principal switch** (the fabric’s quiet leader) hands back a **FCID**, which you should mentally treat like an **IP address**, even though zoning still keys off **WWPNs** (like immutable MACs).

Once that happens, the **FC Name Server (FCNS)** becomes the fabric’s **authoritative phonebook:** WWPN → FCID mappings, globally visible across the fabric, not per-switch. Early on, when there’s only one switch, **FLOGI DB and FCNS look identical**, which is why Cisco mentions that overlap—it’s normal, not magic.

If Ethernet is *ARP + DHCP + DNS mashed together,* Fibre Channel is **FLOGI (identity + resources) → FCNS (who’s who) → then PLOGI/PRLI for actual conversations.** Clean, strict, deterministic—and very SAN-ish.

### Verify the FLOGI and FCNS Databases

**Big picture (mental map first):**

Think of this lab as **naming + identity + prep** for zoning in a Fibre Channel fabric.

Order of ideas:

1. **FLOGI** → “Who are you?”

2. **FCID assignment** → “Here’s your fabric address”

3. **FCNS** → “Global phonebook of the fabric”

4. **Device Alias** → “Human-readable names”

5. **Zones** → “Who is allowed to talk to whom”

Nothing is *passing storage traffic* yet. This is all **control-plane groundwork.**

**1. FLOGI recap (why we look at it):**

**FLOGI happens only between directly connected devices.** It tells the switch:

- Node WWN (WWNN)

- Port WWN (pWWN / WWPN)

- Buffer credits + capabilities

In return, the switch assigns an **FCID** (fabric-local address).

Mental shortcut: **FLOGI = ARP + DHCP + link negotiation, all in one.**

**2. Why MDS shows nothing, but N5K does:**

**On MDS-12:**

```
show flogi database
```

**Empty,** because:

- MDS is *not directly connected* to the host

- FLOGI does **not propagate across the fabric**

**On N5K-12:**

```
show flogi database
```

You see:

- Interface: ```vfc1000```

- VSAN: ```1012```

- FCID: ```0xcf0000```

- pWWN + nWWN of the UCS server

This confirms:

- FCoE → vFC → UCS is alive

- The host successfully logged into the fabric edge

**3. FCNS = fabric-wide name server:**

Now we pivot from **link-level (FLOGI) to fabric-level (FCNS).**

```
show fcns database
```

Key ideas:

- FCNS is **global per fabric**

It maps:

- pWWN → FCID

- Capabilities (SCSI initiator, target, etc.)

Comparable to **DNS + ARP merged together**

Your detailed lookup:

```
show fcns database fcid 0xcf0000 detail vsan 1012
```

Important fields to remember:

- ```port-wwn``` → what we zone on

- ```node-wwn``` → identity of the host

- ```connected interface``` → vfc1000

- ```port-type : N``` → this is an end device

**4. Why we use pWWN in device-alias:**

You configured:

```
device-alias name SRV_POD12 pwwn 20:00:00:25:b5:55:0a:12
```

Why this exact value? Because:

- **Zoning is done on pWWNs,** not FCIDs

- FCIDs are **dynamic**

- pWWNs are **stable identity**

Rule to remember: **WWPN is to zoning what MAC is to switch security.**

**5. Device-alias: why bother?**

Without aliases:

```
zone member pwwn 20:00:00:25:b5:55:0a:12
```

With aliases:

```
zone member device-alias SRV_POD12
```

Benefits:

- Readable configs

- Easier audits

- Survives FCID changes

- Safer in large fabrics

**Commit is mandatory!**

Until you run:

```
device-alias commit
```

…the database is **staged, not active.**

**6. Basic vs Enhanced device-alias mode:**

**Basic:**

- Aliases expand to pWWNs internally

**Enhanced:**

- Aliases stay aliases everywhere

- Apps track alias changes directly

Cisco wants **Enhanced** in real fabrics:

```
device-alias mode enhanced
device-alias commit
```

Think:

- Basic = compile-time

- Enhanced = runtime

**7. First zone (still no storage!)**

You created:

```
zone name DCFNDU vsan 1012
 member device-alias SRV_POD12
```

Important clarification:

- This zone is **incomplete**

- A zone with only one member allows nothing

- This is intentional groundwork

Zoning rule of thumb: **At least one initiator + one target, or nothing flows.**

**8. “State of the world” snapshot:**

```
[ UCS Server ]
   |
  vFC1000 (FCoE, VLAN 1000)
   |
[ N5K-12 ]
   - FLOGI complete
   - FCID assigned (0xcf0000)
   - FCNS entry present
   - Device-alias: SRV_POD12
   - Zone: DCFNDU (solo, inactive for traffic)
   |
[ Fabric continues... ]
```

Nothing is broken. Nothing is missing. You’re exactly where you should be **before adding storage and zoning pairs.**

**One-sentence memory hooks:**

- **FLOGI** → “I exist, give me an address”

- **FCID** → “Fabric-local IP”

- **FCNS** → “Global fabric phonebook”

- **Device-alias** → “DNS for humans”

- **Zone** → “Explicit permission, not discovery”
