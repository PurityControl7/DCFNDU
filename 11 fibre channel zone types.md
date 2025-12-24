# Describing Fibre Channel Zone Types and Their Uses

*Fibre Channel zoning allows you to partition a Fibre Channel fabric into one or more zones. Each zone defines a set of Fibre Channel initiators and Fibre Channel targets that can communicate with each other in a VSAN. Zoning also enables you to set up access control between hosts and storage devices or user groups.*

*You will discover how to configure the Fibre Channel SAN switching features on Cisco Nexus 9000 Series switches to support a design requirement that is based on Fibre Channel.*

## Fibre Channel Zoning

*VSANs are used to segment a physical fabric into multiple logical fabrics. Zoning provides security within a single fabric, whether physical or logical, to restrict access between initiators and targets. Logical unit number (LUN) masking provides additional security to LUNs after an initiator has reached the target device.*

*Now you will familiarize yourself with the concept of zoning and zone types.*

*For a zone, which is similar to the one in the following figure, the following facts apply:*

- *Fabric zoning provides a means of restricting visibility and connectivity among devices that share the same SAN fabric.*

- *The primary goal is to prevent certain devices from accessing other fabric devices.*

*Benefits of zoning:*

- *Provides basic device security.*

- *Permits overlapping zones for shared devices.*

*Registered State Change Notification (RSCN) messages that transmit to all nodes when changes are happening in the fabric are limited to a zone.*

![Zone Zoning](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/zone_zoning.png)

*The zoning service within a Fibre Channel fabric is designed to provide security between devices that share the same fabric. The primary goal is to prevent certain devices from accessing other devices within the fabric. With many different types of servers and storage devices on the network, the need for security is crucial.*

*For example, if a host were to access a disk that another host is using, potentially with a different operating system, then the data on the disk could become corrupted. To avoid any compromise of crucial data within the SAN, zoning allows the user to overlay a security map. This process dictates which devices (hosts) can see which targets and reduces the risk of data loss.*

*Zoning has the following limitations:*

- ***Scalability:*** *Devices are limited per zone, and zones are limited per fabric.*

- ***Fabric availability:*** *Fibre Channel services are shared within the fabric.*

- ***No traffic management:*** *There is a single Fabric Shortest Path First (FSPF) routing table.*

- ***Manageability:*** *There is common administration for all devices within the fabric.*

- ***Zone management security:*** *There are multiple administrators of a distributed zone set.*

- ***Accounting:*** *Accounting for bandwidth usage per device is difficult.*

## SAN Siloed Architecture

*Zoning does have its limitations. It was designed to prevent devices from communicating with other unauthorized devices. This distributed service is common throughout the fabric, so any installed changes to a zoning configuration are disruptive to the entire connected fabric. Also, zoning was not designed to address the availability or scalability of a Fibre Channel infrastructure.*

![Zone Architecture](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/zone_arhitecture.png)

*Enterprise applications are often organized in a siloed architecture, as you see in this figure:*

- *They have physically isolated redundant SANs (SAN islands).*

- *This design provides security and isolation between applications.*

- *It is easier to scale and manage.*

*Siloed architecture has the following limitations:*

- *It is difficult to share data and resources*

- *This approach produces poor utilization of resources*

- *Too many devices take up space, power, and cooling*

*Note: A SAN island is a completely physically isolated switch or group of switches that connects hosts to storage devices, as shown in the previous figure. The main reasons for building SAN islands include isolating different applications in their own fabric or increasing availability by minimizing the impact of fabric-wide disruptive events.*

## SAN Consolidation with VSAN

*Physically distinct SAN islands offer a higher degree of security because each physical infrastructure contains a distinct set of Cisco Fabric Services and management access. Unfortunately, in practice, this situation can become costly and wasteful in terms of fabric ports and resources.*

![Zone VSAN](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/zone_VSAN.png)

*As you see in the figure, VSANs allow SAN consolidation while maintaining logical isolation between application silos and departments:*

- *Departmental security and control are maintained.*

- *Space, power, and cooling are reduced.*

- *Disk and tape utilization are increased.*

- *Port utilization is improved.*

*Each VSAN provides its own fabric services:*

- *Name server*

- *Zone server*

- *Domain controller*

- *Alias server*

- *Login server*

- *FSPF routing*

- *Management*

*VSANs increase the efficiency of a SAN fabric by alleviating the need to build multiple physically isolated fabrics to meet organizational or application needs. Instead, you can build fewer less-costly redundant fabrics, each housing multiple applications and still providing island-like isolation.*

*Spare ports within the fabric can be quickly and nondisruptively assigned to existing VSANs to provide a clean method of virtually growing application-specific SAN islands.*

*VSANs provide not only hardware-based isolation but also a complete replicated set of Fibre Channel services for each VSAN. Therefore, when a VSAN is created, a completely separate set of Cisco Fabric Services, configuration management capability, and policies are created within the new VSAN.*

*Each separate virtual fabric is isolated by using a hardware-based frame-tagging mechanism on VSAN member ports and Extended Inter-Switch Links (EISL) links. Compared to the ISL link, the EISL link type establishes between two trunking E ports (TE Ports) and includes added tagging information for each frame within the fabric. The EISL link is supported between Cisco Multilayer Director Switch (Cisco MDS) and Cisco Nexus switch products. Membership in a VSAN is based on a physical port, and no physical port may belong to more than one VSAN.*

## VSANs vs. Zones

*A zone is always contained within a VSAN, where you can configure multiple zones. Because two VSANs are equivalent to two unconnected SANs, zone A on VSAN 1 is different and separate from zone A in VSAN 2.*

*There is a difference on how the traffic is limited to a zone or VSAN and how membership is defined. VSANs limit unicast, multicast, and broadcast traffic, while zones limit unicast traffic only. In a VSAN, membership is typically defined using the VSAN ID to F Ports. In zoning and zone membership, it is defined by the port World Wide Name (pWWN). A host bus adapter (HBA) or a storage device can belong only to a single VSAN, which is the VSAN associated with the F Port. An HBA or storage device can belong to multiple zones.*

*The following figure shows the possible relationships between VSANs and zones. In VSAN 2, three zones are defined: Zone A, Zone B, and Zone C. Zone C overlaps both Zone A and Zone B as permitted by Fibre Channel standards. In VSAN 7, two zones are defined: Zone A and Zone D. No zone crosses the VSAN. You can configure up to 8000 zones per VSAN and a maximum of 8000 zones for all VSANs on the switch.*

![Zone Zones](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/zone_zones.png)

## Zone Types

*The two main zone types that are used in modern deployments are the following:*

- ***Multi-initiator, single target:*** *Addresses of multiple initiators and the address of a single target are placed in the same zone. Multiple devices (initiators) can access the same target.*

- ***Single-initiator, single target:*** *The address of a single initiator and the address of a single target are placed in the same zone. A single device (initiator) can access a single target.*

*In the following figure, you can examine a zone set with two zones, Zone 1 and Zone 2, in a fabric. Zone 1 provides access from all three hosts (H1, H2, and H3) to the data residing on storage systems S1 and S2. Zone 2 restricts the data on S3 to access only by H3. H3 resides in both zones.*

![Zone Types](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/zone_types.png)

*You can use other ways to partition this fabric into zones. The following figure shows you another possibility. Assume that you must isolate storage system S2 for software testing. To achieve this goal, you configure Zone 3, which contains only host H2 and storage S2. You can restrict access to only H2 and S2 in Zone 3 and to H1 and S1 in Zone 1.*

![Zone Types 2](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/zone_types2.png)

## LUN Masking

*LUN masking is a mapping table inside the front-end array controllers. It determines which LUNs to advertise through which storage array ports and which host is allowed to own which LUNs. Now you will learn how to limit host access to LUNs.*

*LUN masking provides LUN security:*

- *Configured on the storage array.*

- *Ensures that hosts cannot access the wrong LUN.*

- *Ensures that hosts do not share the same LUN.*

- *Determines which LUNs are advertised on which ports.*

*The figure shows a combination of port-based LUN masking and pWWN-based LUN mapping. Both processes are performed concurrently to limit access to LUNs.*

![Zone Masking](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/zone_masking.png)

*LUN masking is the most common method of ensuring LUN security. Each Small Computer Systems Interface (SCSI) host uses several primary SCSI commands to identify its target, discover LUNs, and obtain their size:*

- ***Identify:*** *Which device are you?*

- ***Report LUNs:*** *How many LUNs are behind this storage array port?*

- ***Report capacity:*** *What is the capacity of each LUN?*

- ***Request sense:*** *Is a LUN online and available?*

*It is important to ensure that only one host can access each LUN on the storage array at a time unless the hosts are configured in a cluster. As the host mounts each LUN volume, it writes a signature at the start of the LUN to claim exclusive access. If a second host should discover and try to mount the same LUN volume, it overwrites the previous signature. LUN masking is one method that ensures that only one host can access a LUN; all other hosts are masked out.*

## LUN Mapping

*An alternative method to accomplish LUN security is LUN mapping. If LUN masking is unavailable in the storage array, you can uses LUN mapping. You can use both methods concurrently.*

*LUN mapping also provides LUN security:*

- *Configured on each host HBA.*

- *Ensures that hosts do not share the same LUN.*

- *Each host selects the LUN to which it maps.*

- *Used when LUN masking is unavailable on the array.*

- *HBA-persistent binding saves mapping across reboots.*

*The following figure shows pWWN-based filtering of hosts that are allowed to access LUNs.*

![Zone Mapping](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/zone_mapping.png)

*LUNs can be advertised on many storage ports and discovered by several hosts simultaneously. Many LUNs are visible, but it is the responsibility of the administrator to configure each HBA so that each host has exclusive access to its LUNs. When there are many hosts, mistakes are more likely to happen, and more than one host might access the same LUN by accident.*

## Zoning Configuration

*Zoning enables you to set up access control between storage devices or user groups. If you have administrator privileges in your fabric, you can create zones to increase network security and to prevent data loss or corruption.*

### Zoning Features

*Zoning includes the following features:*

1. *A zone consists of multiple zone members:*

- *Members in a zone can access each other; members in different zones cannot access each other.*

- *If zoning is not activated, all devices are members of the default zone.*

- *If zoning is activated, any device that is not in an active zone (a zone that is part of an active zone set) is a member of the default zone.*

- *A physical fabric can have a maximum of 16,000 members. This maximum includes all VSANs in the fabric.*

2. *A zone set consists of one or more zones:*

- *You can activate or deactivate a zone set as a single entity across all switches in the fabric.*

- *A zone can be a member of more than one zone set.*

- *A zone switch can have a maximum of 500 zone sets.*

3. *Zoning can be administered from any switch in the fabric.*

- *When you activate a zone (from any switch), all switches in the fabric receive the active zone set. Also, if this feature is enabled in the source switch, full zone sets are distributed to all switches in the fabric.*

- *If you add a new switch to an existing fabric, zone sets are acquired by the new switch.*

### Zone Membership

*Zone membership can be specified using the following identifiers:*

- ***pWWN:*** *This identifier specifies the pWWN of an N Port that is attached to the switch as a member of the zone.*

- ***Fabric pWWN:*** *This identifier specifies the WWN of the fabric port (switch port WWN). This membership is also referred to as port-based zoning.*

- ***FCID:*** *This identifier specifies the Fibre Channel ID of an N Port that is attached to the switch as a member of the zone.*

- ***Interface and sWWN:*** *This identifier specifies a switch interface that the switch WWN (sWWN) identifies. This membership is also referred to as interface-based zoning.*

- ***Interface and domain ID:*** *This identifier specifies a switch interface that the domain ID identifies.*

- ***Domain ID and port number:*** *This identifier specifies the domain ID of a Cisco switch domain and specifies a port that belongs to a switch manufactured by another vendor.*

*The following figure illustrates the recommended practice on how to configure a zone and a zone set.*

![Zone Configuration](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/zone_configuration.png)

### Device Aliases

*Cisco SAN switches support Distributed Device Alias Services (device aliases) on a fabric-wide basis. To configure features such as zoning and dynamic port VSAN membership (DPVM) in a Cisco SAN switch, you must specify the pWWN of a device. You must assign the correct device name each time you configure these features. An inaccurate device name may cause unexpected results.*

*You can circumvent this problem if you define a user-friendly name for a pWWN and use this name in all the configuration commands as required. These user-friendly names are referred to as device aliases.*

*Device aliases have the following features:*

- *The device alias information is independent of the VSAN configuration.*

- *The device alias configuration and distribution is independent of the zone server and the zone server database.*

- *The device alias application uses the Cisco Fabric Services infrastructure to enable efficient database management and distribution. Device aliases use the coordinated distribution mode and the fabric-wide distribution scope.*

*Device aliases have the following requirements:*

- *You can assign device aliases only to pWWNs.*

- *There must be a one-to-one relationship between the pWWN and the device alias that maps to it.*

- *A device alias name is restricted to 64 alphanumeric characters.*

## Zoning Management

*Cisco SAN switches automatically support the following basic zone features:*

- *Hard zoning cannot be disabled.*

- *Name server queries are soft-zoned.*

- *Only active zone sets are distributed.*

- *Unzoned devices cannot access each other.*

- *A zone or zone set with the same name can exist in each VSAN.*

- *Each VSAN has a full database and an active database.*

- *Active zone sets cannot be changed without activating a full zone database.*

- *Active zone sets are preserved across switch reboots.*

- *Changes to the full database must be explicitly saved.*

- *Zone reactivation (when a zone set is active, and you activate another zone set) does not disrupt existing traffic.*

### Active and Full Zone Sets

*Each VSAN can have multiple zone sets, but only one zone set can be active at any given time. When you create a zone set, that zone set becomes a part of the full zone set, as illustrated in the following example.*

![Zone Sets](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/zone_sets.png)

*When you activate a zone set, a copy of the zone set from the full zone set is used to enforce zoning and is called the active zone set. You cannot modify an active zone set. A zone that is part of an active zone set is called an active zone.*

![Zone Sets 2](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/zone_sets2.png)

*The administrator can modify the full zone set even if a zone set with the same name is active. However, the modification will be enforced only upon reactivation. As you see in the following example, Zone D has been added to Zone set Z1, but did not take effect because reactivation of that zone set has not occurred.*

![Zone Sets 3](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/zone_sets3.png)

*When the activation completes, the active zone set is automatically stored in a persistent configuration, as shown in the following example. This action allows the switch to preserve the active zone set information across switch resets.*

![Zone Sets 4](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/zone_sets4.png)

*All other switches in the fabric receive the active zone set so they can enforce zoning in their respective switches.*

*A Fibre Channel ID or N Port that is not part of the active zone set belongs to the default zone, and the default zone information is not distributed to other switches.*

*Note: If one zone set is active, and you activate another zone set, the currently active zone set is automatically deactivated. You do not need to explicitly deactivate the currently active zone set before activating a new zone set.*

### Default Zone

*Each member of a fabric can belong to any zone. If a member is not part of any active zone, it is considered to be part of the default zone. Therefore, if no zone set is active in the fabric, all devices are considered to be in the default zone where traffic among members can be either permitted or denied.*

*Even though a member can belong to multiple zones, a member that is part of the default zone cannot be part of any other zone.*

*Unlike configured zones, default zone information is not distributed to the other switches in the fabric. For this reason, you must configure default zoning policy on each switch.*

*Note: When the switch is initialized for the first time, no zones are configured, and all members are considered to be part of the default zone. Members are not permitted to communicate with each other.*

*Configure the default zone policy on each switch in the fabric. If you change the default zone policy on one switch in a fabric, be sure to change it on all the other switches in the fabric.*

### Zone Enforcement

*The two types of zoning enforcement are soft zoning and hard zoning.*

*Each end device (N Port) discovers other devices in the fabric by querying the name server. When a device logs in to the name server, the name server returns the list of other devices that the querying device can access. If an N Port does not know about the Fibre Channel IDs of other devices outside its zone, it cannot access those devices.*

*In soft zoning, zoning restrictions are implemented in software and applied only during interaction between the name server and the end device. If an end device somehow knows the Fibre Channel ID of a device outside its zone, it can access that device.*

*With hard zoning, hardware enforces hard zoning on each frame that an N Port transmits. As frames enter the switch, source-destination IDs are compared with permitted combinations to allow the frame at wire speed. Hard zoning is applied to all forms of zoning.*

*Cisco SAN switches support both hard and soft zoning. By default, both types of zoning are enabled, with hard zoning used in priority over soft zoning. If the system is unable to use hard zoning due to hardware resource exhaustion, it will be disabled, and the system will fall back to use soft zoning.*

*Note: Hard zoning enforces zoning restrictions on every frame and prevents unauthorized access.*

### Enhanced Zoning

*In basic zoning, administrators can make simultaneous configuration changes, which means that one administrator can overwrite another administrator’s changes. However, in enhanced zoning, the administrator performs all configurations within a single configuration session. When you begin a session, the switch locks the entire fabric to implement the change to ensure zoning consistency within the fabric.*

*The default zone policy in basic zoning is defined per switch, and to ensure smooth fabric operation, all switches in the fabric must have the same default zone setting. Enhanced zoning enforces and exchanges the default zone setting throughout the fabric, which helps reduce troubleshooting time.*

*In basic zoning, to distribute the zoning database, you must reactivate the same zone set. This action may affect hardware changes for hard zoning on the local switch and on remote switches. However, enhanced zoning implements changes to the zoning database and distributes them without reactivation.*

*You can enable enhanced zoning in a VSAN. By default, the enhanced zoning feature is disabled in all Cisco SAN switches.*

## Lab: Configure Zoning

*Fibre Channel zoning is a functionality within Fibre Channel SAN that provides the ability to control the initiators and targets that can communicate by defining the permitted communication parameters on the network. This process differs from LUN masking, which is configured on the Storage HBA.*

*Zone sets and zones help ensure that a server has access to the correct disks but does not see others. The feature is similar to IP network access control lists (ACLs). However, zoning is enabled by default on a SAN network. After zoning is applied, it has the same assumed default policy as ACLs: deny all.*

### Verify the Default Zoning

**Baseline Reality Check:**

Before touching zoning, we **verify the fabric’s default security posture.** Fibre Channel is paranoid by design — *nothing talks unless you explicitly allow it.*

Why this matters:

- Default zoning = *deny*

- No implicit trust between devices

- Prevents accidental cross-talk, data leaks, and SAN chaos

**Step 1: Access the switches**

**MDS-12 (core / fabric switch):**

```
Host: 10.1.5.10
Username: admin
Password: 1234QWer
```

**N5K-12 (edge / UCS-facing switch):**

```
Host: 10.1.5.8
Username: admin
Password: 1234QWer
```

Mental model:

- **N5K-12** = talks directly to servers (UCS)

- **MDS-12** = fabric brain / SAN backbone

**Step 2: Inspect default zoning policy (N5K-12)**

```
N5K-12# show zone policy
Vsan: 1
   Default-zone: deny
   Distribute: active only
   Broadcast: disable
   Merge control: allow
   Generic Service: read-write

Vsan: 1012
   Default-zone: deny
   Distribute: active only
   Broadcast: disable
   Merge control: allow
   Generic Service: read-write
```

Key takeaways:

- **Default-zone: deny** → no communication unless zoned

- **Distribute: active only** → only active zones propagate

- **VSAN 1012 exists** → this is our SAN playground

**Step 3: Inspect default zoning policy (MDS-12)**

```
MDS-12# show zone policy
Vsan: 1
   Default-zone: deny
   Distribute: active only
   Broadcast: unsupported
   Merge control: allow
   Generic Service: read-write
   Smart-zone: disabled

Vsan: 12
   Default-zone: deny
   Distribute: active only
   Broadcast: unsupported
   Merge control: allow
   Generic Service: read-write
   Smart-zone: disabled

Vsan: 1012
   Default-zone: deny
   Distribute: active only
   Broadcast: unsupported
   Merge control: allow
   Generic Service: read-write
   Smart-zone: disabled
```

Clarification:

- **MDS supports multiple VSANs** (1, 12, 1012)

- Zoning is per-VSAN — they are logically isolated fabrics

**Step 4: Confirm there are NO zones or zonesets**

**MDS-12:**

```
MDS-12# show zone active
Zone not present

MDS-12# show zoneset active
Zoneset not present
```

**N5K-12:**

```
N5K-12# show zone active
Zone not present

N5K-12# show zoneset active
Zoneset not present
```

Clean slate confirmed.

**Step 5: Verify zoning status for VSAN 1012 (N5K-12)**

```
N5K-12# show zone status vsan 1012
VSAN: 1012 default-zone: deny distribute: active only Interop: default
    mode: basic merge-control: allow
    session: none
    hard-zoning: enabled broadcast: disabled
Default zone:
    qos: none broadcast: disabled ronly: unsupported
Full Zoning Database :
    DB size: 37 bytes
    Zonesets:0  Zones:1 Aliases: 0
Active Zoning Database :
    Database Not Available
```

**Important clarifications:**

*Why VSAN 1012?*

- You typically discover this via:

```
show vsan
show flogi database
show interface fc / vfc brief
```

- Earlier labs showed the UCS server logged into **VSAN 1012**, so zoning must match that VSAN.

**Concept recap (this is SAN gospel):**

- **Zone** = who can talk to whom

- **Zoneset** = collection of zones

- **Only one zoneset can be active per VSAN**

- **No active zoneset = nobody talks**

**Step 6: Enable enhanced modes (MDS-12 first — important!)**

Order matters. Whoever distributes first overwrites others.

**On MDS-12:**

```
MDS-12(config)# device-alias distribute
MDS-12(config)# device-alias mode enhanced
MDS-12(config)# device-alias commit
```

Enable enhanced zoning:

```
MDS-12(config)# zone mode enhanced vsan 1012
WARNING: This command would distribute the zoning database of this switch throughout the fabric. Do you want to continue? (y/n) [n]
y
```

**Step 7: Repeat on N5K-12**

```
N5K-12(config)# device-alias distribute
N5K-12(config)# device-alias mode enhanced
N5K-12(config)# device-alias commit
```

Enable zoning:

```
N5K-12(config)# zone mode enhanced vsan 1012
WARNING: This command would distribute the zoning database of this switch throughout the fabric. Do you want to continue? (y/n) [n]
y
```

Important outcome:

- The zone you created earlier **was wiped**. Why?

→ MDS-12 distributed its empty zoning DB first

→ Fabric consistency beats local config

**Step 8: Confirm device presence (sanity check)**

```
N5K-12# show flogi database
--------------------------------------------------------------------------------
INTERFACE        VSAN    FCID           PORT NAME               NODE NAME
--------------------------------------------------------------------------------
vfc1000          1012  0xcf0000  20:00:00:25:b5:55:0a:12 20:00:00:25:b5:55:0f:12
                           [SRV_POD12]

Total number of flogi = 1.
```

Good — server is still logged in.

**Step 9: Re-create the zone (enhanced mode)**

```
N5K-12(config)# zone name DCFNDU vsan 1012
Enhanced zone session has been created. Please ‘commit’ the changes when done.
```

Add member:

```
N5K-12(config-zone)# member device-alias SRV_POD12
```

Commit:

```
N5K-12(config-zone)# zone commit vsan 1012
Commit operation initiated. Check zone status
```

**Step 10: Verify zone distribution**

**On N5K-12:**

```
show zone vsan 1012
```

**On MDS-12:**

```
MDS-12# show zone vsan 1012
zone name DCFNDU vsan 1012
  device-alias SRV_POD12
```

Zone successfully distributed across the fabric.

**“State of the World” Topology Map:**

```
[ UCS Server ]
   |
 vFC (VSAN 1012)
   |
[ N5K-12 ]  <-- zoning created here
   |
 FC fabric
   |
[ MDS-12 ]  <-- zoning distributed here
   |
[ (future storage not yet visible) ]
```

**Final intuition drop:**

Zoning isn’t about *connecting devices* — it’s about **preventing everything else.** Default deny, explicit allow, fabric-wide consistency. That’s SAN philosophy in a sentence.

### Enable the Configuration Between MDS-12 and the Core-MDS

**Goal:** Physically and logically integrate MDS-12 into the larger Fibre Channel fabric so zoning, device-aliases, and FCNS entries propagate correctly.

At this point:

- **N5K-12** hosts the UCS server (SRV_POD12)

- **Core-MDS** hosts NetApp storage

- **MDS-12** sits in between and must join the fabric cleanly

**1. Enable the Fibre Channel Interfaces Toward Core-MDS (MDS-12):**

We start by bringing up the FC interfaces that physically connect **MDS-12 → Core-MDS.**

```
MDS-12(config)# interface fc 1/5-6
MDS-12(config-if)# no shutdown
```

Now verify interface health and trunking:

```
MDS-12(config-if)# sh int fc1/5-6
```

Key things to notice in the output:

- **Port mode is TE** → this is a trunk (switch-to-switch)

- **Trunk vsans (up)** includes **1012**

- VSAN 12 is isolated (expected in many labs)

- B2B credits exchanged successfully

This confirms:

- Physical link

- FC trunk

- VSAN 1012 propagating

**2. Verify Device-Alias Distribution Reached MDS-12:**

Because **device-alias distribution** was enabled earlier, MDS-12 should now have aliases learned from the fabric.

```
MDS-12(config-if)# show device-alias database
```

Example output:

```
device-alias name SRV_POD12 pwwn 20:00:00:25:b5:55:0a:12
device-alias name Server-24 pwwn 20:00:00:25:b5:55:0a:24
...
```

*Important takeaway:*

- Device-alias is **fabric-wide state** once distribution + enhanced mode are enabled. You *do not* manually recreate aliases everywhere.

**3. Remove the Locally-Created Zone on MDS-12:**

This is a subtle but *very* important SAN hygiene rule: **only one switch should be the zoning authority.**

In this lab, zoning will come from **Core-MDS**, so we delete the local copy.

```
MDS-12(config)# no zone name DCFNDU vsan 1012
MDS-12(config)# zone commit vsan 1012
```

Verify it’s gone:

```
MDS-12(config)# show zone vsan 1012
Zone not present
```

This prevents:

- Split-brain zoning

- Merge conflicts

- Silent fabric weirdness (the worst kind)

**4. Reset the FC Trunk to Force Database Sync:**

A classic SAN “nudge the fabric” move.

```
MDS-12(config)# interface fc 1/5-6
MDS-12(config-if)# shut
MDS-12(config-if)# no shut
```

Check VSAN status using a filtered command:

```
MDS-12(config-if)# sh int fc 1/5-6 | inc 1012
```

Tiny pipe explanation:

- ```|``` pipes output into another command

- ```inc 1012``` means *“only show lines containing 1012”*

- This keeps FC output readable instead of scrolling forever

**5. Verify End-to-End Fabric Visibility (FCNS):**

Now the payoff: both **server and storage** should be visible everywhere.

**On MDS-12:**

```
MDS-12# show fcns database
```

Expected result:

```
VSAN 1012
-------------------------------------------------------------------------
0x03fb7a   N   50:0a:09:81:86:78:22:ca (NetApp)  scsi-fcp
0xcf0000   N   20:00:00:25:b5:55:0a:12           scsi-fcp:init fc-gs
           [SRV_POD12]
```

**On N5K-12:**

```
N5K-12# show fcns database
```

Same two entries should appear. This confirms:

- Fabric is fully stitched

- FCNS is global

- UCS server ↔ NetApp storage are now mutually visible

- Zoning can safely proceed next

**Mental Topology Snapshot (State of the World):**

```
[ UCS Server ]
     |
  (FLOGI)
     |
  N5K-12
     |
 (FC Trunk, VSAN 1012)
     |
  MDS-12
     |
 (FC Trunk)
     |
 Core-MDS
     |
 [ NetApp Storage ]
```

- **Device-alias:** Distributed, enhanced

- **Zoning:** Centralized (Core-MDS will own it)

- **FCNS:** Consistent across fabric

- **VSAN 1012:** Operational end-to-end

This lab is doing a fantastic job teaching the real SAN lesson most docs skip: *discipline beats configuration skill.*

### Additional Device Alias Verification

**What we’re validating here:**

Device aliases are *human-readable labels* mapped to **pWWNs**, meant to save your sanity when zoning. In **enhanced mode**, aliases are first-class citizens: zoning, FCNS output, and fabric distribution all understand them natively. This section is about *confirming* that:

- aliases exist,

- they’re distributed,

- and they’re actively referenced in the fabric view (FCNS).

Think of this as a **sanity check after fabric integration**, not configuration-heavy work.

**Enter device-alias database mode (inspection, not creation):**

From global config on **N5K-12**, enter the device-alias database context:

```
N5K-12(config)# device-alias database
N5K-12(config-device-alias-db)#
```

This mode is where aliases are *defined, inspected, and modified* before being committed.

Explore what’s available with ```?```:

```
N5K-12(config-device-alias-db)# ?
  device-alias  Device-alias configuration commands
  no            Negate a command or set its defaults
  end           Go to exec mode
  exit          Exit from command interpreter
  pop           Pop mode from stack or restore from name
  push          Push current mode to stack or save it under name
  where         Shows the cli context you are in
```

Why this matters: Cisco loves deep CLI sub-modes. Always sanity-check where you are before typing destructive commands.

**Verify FCNS visibility** ***with aliases applied:***

Still on **N5K-12**, list the Fibre Channel Name Server database:

```
N5K-12(config-device-alias-db)# show fcns database

VSAN 1012
-------------------------------------------------------------------------
FCID       TYPE  PWWN                    (VENDOR)        FC4-TYPE:FEATURE  
-------------------------------------------------------------------------
0x03fb7a   N     50:0a:09:81:86:78:22:ca (NetApp)        scsi-fcp
0xcf0000   N     20:00:00:25:b5:55:0a:12 (Cisco)         scsi-fcp:init fc-gs
                 [SRV_POD12]

Total number of entries = 2
```

*Key observations (this is the “aha” moment):*

- The **Cisco UCS server** is now shown as ```[SRV_POD12]```

- That bracketed name is pulled directly from the **device-alias database**

- The NetApp does *not* yet have an alias (still raw PWWN)

This confirms:

- FCNS is fabric-wide

- Device aliases are being resolved

- Enhanced mode is actually doing something useful

**Verify the device-alias database itself:**

Now explicitly list the alias mappings:

```
N5K-12(config-device-alias-db)# show device-alias database
device-alias name test pwwn 20:00:00:25:b1:00:00:01 
device-alias name Conflict pwwn 20:00:00:25:b1:00:00:02 
device-alias name SRV_POD12 pwwn 20:00:00:25:b5:55:0a:12 
device-alias name Server-24 pwwn 20:00:00:25:b5:55:0a:24

Total number of entries = 4
```

Interpretation:

- ```SRV_POD12``` → your UCS server (actively used)

- Other aliases (```test```, ```Conflict```, ```Server-24```) are present in the fabric but not zoned yet

- This database is already **distributed** across switches (thanks to earlier steps)

**Exit cleanly:**

```
N5K-12(config-device-alias-db)# exit
N5K-12(config)# exit
```

**Takeaway (cookbook-style bullets):**

- **Device aliases = pWWN → human name**

- **Enhanced mode** allows aliases to appear in:

1. FCNS output

2. zoning rules

3. distributed fabric databases

- Seeing ```[SRV_POD12]``` inside ```show fcns database``` is proof the setup is correct

- Alias creation happens *once*, zoning references it *everywhere*

- This is why large fabrics stay sane instead of becoming hexadecimal horror stories

### Configure Zoning

**Big picture first:**

Zoning is the *actual security enforcement* layer in Fibre Channel. FLOGI/FCNS tell devices *who exists*; zoning decides *who may talk to whom*. With **default-zone: deny**, *nothing* communicates unless explicitly allowed.

You’re now building a **classic single-initiator / single-target zone:**

- Initiator → Cisco UCS server (```SRV_POD12```)

- Target → NetApp storage (by PWWN)

- Wrapped inside a zoneset

- Activated and distributed fabric-wide

**1. Sanity check: device-alias database exists everywhere**

On **N5K-12:**

```
N5K-12# show device-alias database
device-alias name test pwwn 20:00:00:25:b1:00:00:01 
device-alias name Conflict pwwn 20:00:00:25:b1:00:00:02 
device-alias name SRV_POD12 pwwn 20:00:00:25:b5:55:0a:12 
device-alias name Server-24 pwwn 20:00:00:25:b5:55:0a:24

Total number of entries = 4
```

On **MDS-12:**

```
MDS-12# show device-alias database
device-alias name test pwwn 20:00:00:25:b1:00:00:01 
device-alias name Conflict pwwn 20:00:00:25:b1:00:00:02 
device-alias name SRV_POD12 pwwn 20:00:00:25:b5:55:0a:12 
device-alias name Server-24 pwwn 20:00:00:25:b5:55:0a:24

Total number of entries = 4
```

*Key insight:*

Device aliases are now **fabric-wide** and usable in zoning because you’re in **enhanced mode.** This is what makes large fabrics survivable by humans.

**2. Create (or complete) the zone on N5K-12:**

Even though the core already created ```DCFNDU```, you’re explicitly defining its members here (good practice for labs and cookbooks).

Enter config mode and create the zone:

```
N5K-12(config)# zone name DCFNDU vsan 1012
Enhanced zone session has been created. Please ‘commit’ the changes when done.
N5K-12(config-zone)#
```

Check what devices are visible (FCNS = naming truth):

```
N5K-12(config-zone)# show fcns database

VSAN 1012
-------------------------------------------------------------------------
FCID       TYPE  PWWN                    (VENDOR)        FC4-TYPE:FEATURE  
-------------------------------------------------------------------------
0x03fb7a   N     50:0a:09:81:86:78:22:ca (NetApp)        scsi-fcp
0xcf0000   N     20:00:00:25:b5:55:0a:12 (Cisco)         scsi-fcp:init fc-gs
                 [SRV_POD12]

Total number of entries = 2
```

**Mental model:**

- FCNS answers *“who exists?”*

- Zoning answers *“who may talk?”*

**3. Add zone members (initiator + target):**

Add **NetApp storage** by raw PWWN:

```
N5K-12(config-zone)# member pwwn 50:0a:09:81:86:78:22:ca
```

Add server by device-alias:

```
N5K-12(config-zone)# member device-alias SRV_POD12
```

Commit the zone:

```
N5K-12(config-zone)# zone commit vsan 1012
Commit operation initiated. Check zone status
```

Verify:

```
N5K-12(config-zone)# show zone vsan 1012
zone name DCFNDU vsan 1012
  pwwn 50:0a:09:81:86:78:22:ca
  device-alias SRV_POD12
```

*Why this mix is normal:*

- Storage is often referenced by **PWWN** (vendor-owned, stable)

- Servers are friendlier via **device-alias** (admin-owned abstraction)

**4. Create and populate the zoneset:**

Zones don’t do *anything* until placed in a zoneset.

Create zoneset:

```
N5K-12(config)# zoneset name DCFNDU vsan 1012
Enhanced zone session has been created. Please ‘commit’ the changes when done.
N5K-12(config-zoneset)#
```

Add the zone:

```
N5K-12(config-zoneset)# member DCFNDU
```

Commit:

```
N5K-12(config-zoneset)# zone commit vsan 1012
Commit operation initiated. Check zone status
```

**5. Activate the zoneset (this is the real switch flip):**

```
N5K-12(config)# zoneset activate name DCFNDU vsan 1012
WARNING: This command would distribute the zoning database of this switch throughout the fabric. Do you want to continue? (y/n) [n]
```

Enter ```y```, then commit:

```
N5K-12(config)# zone commit vsan 1012
Commit operation initiated. Check zone status
```

**Important truth:**

Activation = *enforcement.* Everything before this was just writing rules on paper.

**6. Verify zoning state (control plane + data plane):**

```
N5K-12(config)# show zone status vsan 1012
VSAN: 1012 default-zone: deny distribute: full Interop: default
    mode: enhanced merge-control: allow
    session: none
    hard-zoning: enabled broadcast: disabled
Default zone:
    qos: none broadcast: disabled ronly: unsupported
Full Zoning Database :
    DB size: 156 bytes
    Zonesets:1  Zones:1 Aliases: 0 Attribute-groups: 1
Active Zoning Database :
    DB size: 152 bytes
    Name: DCFNDU  Zonesets:1 Zones:2
Status: Commit completed at 09:48:48 UTC May 10 2017
```

**What to actually care about here:**

- ```mode: enhanced``` → correct

- ```distribute: full``` → fabric synchronized

- ```Active Zoning Database``` exists → traffic allowed

**7. Final proof: allowed communication**

```
N5K-12(config)# show zone active vsan 1012
zone name DCFNDU vsan 1012
 * fcid 0x03fb7a [pwwn 50:0a:09:81:86:78:22:ca]
 * fcid 0xcf0000 [device-alias SRV_POD12]
```

*This is the victory screen.* The initiator and target are now explicitly permitted to communicate inside a deny-by-default fabric.

**Final mental snapshot (pin this in your mind):**

- **FCNS** = fabric phonebook

- **Device-alias** = human-readable labels

- **Zone** = who may talk

- **Zoneset** = which rules are active

- **Activation + commit** = enforcement

- **Default-zone deny** = SAN paranoia (correct)

This lab is now concluded.
