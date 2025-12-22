# Basic Data Center Storage Concepts

*IP-based networking has become the global standard for communicating over vast distances, and it has become performant enough to rival SAN speeds and latencies in recent years. Both network types are commonly used in modern data centers, with more emphasis on Ethernet.*

*Compared to the SAN, IP networks provide increasing levels of manageability, interoperability, and cost-effectiveness. By converging the storage with the current IP networks such as LANs, metropolitan-area networks (MANs), and WANs, immediate benefits appear through storage consolidation, virtualization, mirroring, backup, and management. The convergence also provides increased capacities, flexibility, expandability, and scalability.*

*With the rise of Ethernet and IP networking, the need for a separate physical network infrastructure dedicated to storage disappeared. This change enabled protocols that utilize Ethernet networks to be used more commonly for transferring storage information to a remote system.*

*Two approaches to network storage are commonly used in modern data centers. One is file-based storage, which uses a central server to share information across a network on a file-by-file basis. The other is block-based storage, where virtual hard drives called logical unit numbers (LUNs) are used to provide block-level storage to the remote device.*

*File-based protocols can use only the Ethernet and IP stack for communication over the network. Block-based protocols can use the native Fibre Channel SAN network or the Ethernet network.*

## Storage Connectivity Options in the Data Center 

*Storage connectivity options in the data center include file-based network storage, block-based network storage, Fibre Channel, and Internet Small Computer Systems Interface (iSCSI).*

### File-Based Network Storage

*File-based storage uses the IP stack communication and is represented with the Common Internet File System (CIFS) and Network File System (NFS) protocols. These protocols use a client/server architecture to provide the same information available on the server to many clients.*

*The client/server architecture is based on the concept that one system has the resources that another system requires. In file-based network storage, these resources are files. The system with the resources is called the server, and the system that requires the resources is called the client.*

*The server stores the resources on the block-level but presents them as file-based shares to the clients. This functionality is important, because the server performs on the block-level all the file-level read-and-write operations that come over the network. The same files can be shared to many clients, and the sharing system resolves potential conflicts.*

*A storage system using the CIFS and NFS protocols is referred to as a network-attached storage (NAS) system. Examples of NAS storage systems are consumer NAS devices that often run in homes. These devices almost exclusively run CIFS and NFS to share files over the network.*

*Although NAS is extremely flexible and feature rich, it lacks the reach of low latency of SAN systems that by design are as latency free as possible. The client/server model of NAS and the traditional TCP/IP networking stack that is used for NAS introduces this latency in a NAS environment.*

*File-based network storage has these features:*

- *Uses client/server architecture over TCP/IP.*

- *The server stores information and performs network-requested reads and writes.*

- *Many clients access the same share.*

- *The main file-based protocols are CIFS and NFS.*

- *The server accesses the stored information on block level.*

![File Based Network Storage](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/file_based_network_storage.png)

*The figure shows how a request transmits via TCP/IP to the server through a routed or switched Ethernet network and is received by the server redirector service. The server service translates the request into a local storage read or write command.*

*Both the client and server are operating system (OS)-level services, not physical devices. These services process the authentication and communication between the client and server. The application on the client side initiates a read or write operation that is locally intercepted by the redirector service that forwards the request over the network.*

*The benefits of the client/server architecture include cost reduction because of hardware and space requirements. The local workstations require less disk space because commonly used data can be stored on the server. Other benefits include centralized support (backups and maintenance) that are performed on the server.*

*Once the request has been fulfilled, the server responds with the requested data for reads or acknowledge for writes.*

![Example of the NFS protocol stack](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/nfs_protocol_stack.png)

*File-based network storage systems services reside at the application layer (Layer 7) of the OSI protocol stack. The underlying protocols are the standard TCP/IP over Ethernet. The example shows the protocol stack of the NFS protocol. CIFS puts up the same protocol stack, but not including Layer 6.*

*Because of the stack size, the NAS protocols have a higher latency. However, they can perform in unpredictable networks and multiuser environments much better, because they rely on TCP/IP and UDP/IP for communication.*

*Because of the same protocol stack, both CIFS and NFS can run on the same server simultaneously. They use different transport layer ports but can share the same files on the server.*

![Data Sharing Using a NAS Server](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/nas_server_file_sharing.png)

*This figure shows the communication between the NAS server and two other servers with different operating systems. The NAS server provides storage space for various files that is accessible to other devices over both the CIFS and NFS protocol at the same time.*

*The figure represents an example of data sharing between various devices. File I/O uses the CIFS protocol primarily for transferring files to and from Windows servers and uses the NFS protocol for transferring files to and from UNIX and Linux servers. CIFS and NFS are carried over TCP/IP, usually across the LAN, and have high latency and relatively low bandwidth. Most applications are file-based and can read and write entire files. Examples are the Microsoft Office applications (such as Microsoft Word, Excel, and PowerPoint), audio and video applications, and web server applications that transfer HTML files to a browser.*

### Common Internet File System

*The CIFS protocol is a NAS protocol that evolved from the IBM Server Message Block (SMB) file-sharing protocol. In fact, it is common to use the names interchangeably, although CIFS is a specific implementation of the SMB standard.*

*CIFS is a very prominent file system in home environments since it has traditionally been linked to Windows systems. It also has very good authentication support and is much more flexible than NFS when devices come and leave the network.*

*This feature set makes CIFS ideal when many small devices access the share dynamically, such as a company document repository, PowerPoint shares, and image and video shares over Wi-Fi. Its capability to use authentication provides a security layer that is unavailable in NFS3. It also capable of quickly joining an available Wi-Fi and quickly accessing the files that are shared there in a secure fashion.*

*The security and protocol implementation of CIFS causes additional communication overhead, and CIFS does not match the performance of NFS. It is also more difficult to set up, especially in Linux environments where there is no Windows Active Directory to provide the authentication and group policy framework. CIFS is therefore most used in data center virtual environments based on Windows and virtual environments utilizing the Microsoft Hyper-V hypervisor.*

*CIFS has traditionally had very good support on Linux systems through the Samba SMB protocol implementation. However, SMB does not support the Linux file permissions, which makes using and managing it more difficult on Linux systems. Different authentication options of a CIFS share can also cause issues with different Linux implementations of SMB. Generally, Linux works better as an SMB server than as a client.*

*The CIFS NFS has these characteristics:*

- *Commonly associated with Windows environments; in data center used in Hyper-V.*

- *Natively supports user authentication and encryption.*

- *Integration into the Windows Active Directory stack provides policy-based authentication and management.*

- *Based on the IBM SMB standard from the early 1980s.*

![File Copy Example](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/file_copy.png)

*This figure shows the initial actions that are taken on a file copy from the client to the server. The client initiates the connection, and the client and server negotiate the details of the transaction. After the negotiation, the session establishes and the transaction starts.*

*The client and server exchange many more messages before the file transfers successfully, depending on the size of the file.*

### Network File System

*The NFS file-based network storage protocol has traditionally been associated with Linux, Solaris, and Hewlett-Packard UNIX (HP-UX). Although Windows also supports NFS, its support is not part of the windows default feature set, and CIFS is nearly always the preferred option in a Windows NAS environment.*

*Sun Microsystems developed the protocol in the 1980s to address the need to share resources in a distributed networking environment. Networked computers can share files across networks without being in the same physical location as the server.*

*NFS has less overhead than the CIFS protocol but has traditionally lacked in security features. Many security features were addressed in NFS version 4, but NFS 3 is still the most used because of its simple set up and excellent performance.*

*NFS, excluding version 4, supports a fully stateless operation, meaning that the connectivity does not need to be established before communication is enabled. At the same time, this functionality makes NFS much less forgiving to network interruption and dynamic client connectivity than CIFS is. Therefore, NFS is a great choice for the high performance that NAS uses within the data center, where security aspects are mitigated by confinement within one secured location.*

*In data centers today, the NFS is commonly used in vSphere environments, where the NFS file share can be presented to many hosts to provide a shared datastore. NFS is also important in Linux environments, because NFS natively supports Linux file attributes and can integrate very well with a Linux environment. Once the remote NFS share is mounted in the local directory tree, it will be seen and managed as a local directory.*

*In the following figure, the server in the network is a network appliance storage system that is configured as a NFSv3 server. (The NFSv4 system no longer relies on the rpcbind for its operation.) The client in the example can be one of many versions of the UNIX or Linux operating system.*

![Network File System Communicating With a Client](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/nfs.png)

*The storage system provides services to the client. These services include mount daemon (mountd), Network Lock Manager (nlm_main), Network File System Daemon (NFSD), status monitor (sm_1_main), quota daemon (rquot_1_main), and portmap (also known as rpcbind). Each service is required for a successful operation of an NFS process. For example, a client cannot mount a resource if mountd is not running on the server. Similarly, if rpcbind is not running on the server, NFSv3 communication cannot be established between the client and the server.*

*The NFS client uses the standard UNIX mount command to mount the remote share to a local directory. To establish the NFS transfer, the client makes a remote procedure call (RPC) to the portmap or rpcbind daemon that is running on the server.*

*A portmap, sometimes known as rpcbind, is an RPC service that allows clients and servers to communicate with one another using interprocess communication methods. Network nodes use IP addresses to communicate with one another. Similarly, the portmap service allows RPC services (processes or programs) to use assigned port addresses to communicate with one another.*

*A portmap allows these RPC services to use assigned ports if they are registered with the portmap with program number, version, and transport protocol. The portmap program is usually registered on port 111, which is also known as a privileged port in UNIX. A privileged port is a port number lower than 1024 and it can be used as a source port only by a UNIX superuser. NFS servers usually use port 2049 as the default.*

*Next, the client application issues a read call that is processed by the mountd. The mountd verifies access to the resource and caches the results in the access. It returns either a successful result or an error. If the mount command was successful, the resource is now accessed at the mountpoint, as shown in the preceding figure.*

*Note: It is also possible to use an automounter service with NFS. The automounter automatically mounts remote NFS file shares when they are necessary and unmounts them after a period of inactivity. This approach has little application in simple client-server deployments. However, it can be very useful in Network Information Service (NIS) environments, where the information is shared with a distributed network of server machines.*

*NFS Version Comparison:*

![NFS Version Comparison](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/nfs_versions.png)

### Quick Notes and Clarifications:

**CIFS / SMB** is *stateful, chatty, and user-centric.* It feels like Windows thinking out loud: sessions, locks, permissions, ACLs, authentication baked deep into the protocol. It’s great for file sharing where identity, file locking, and “who touched what” really matter — but that richness makes it heavier and more latency-sensitive.

**NFS** is *stateless (mostly), quiet, and UNIX-brained.* It treats files like remote extensions of the local filesystem: simple ops, fewer handshakes, less ceremony. This makes NFS faster and cleaner for things like VM datastores, containers, and large-scale infrastructure workloads — but it assumes you already trust the network and the clients.

**Big picture comparison:**

- CIFS = *“enterprise collaboration protocol”*

- NFS = *“infrastructure plumbing protocol”*

- CIFS cares about *users*

- NFS cares about *performance and simplicity*

If storage is for humans, CIFS wins. If storage is for machines, NFS absolutely dunks on it.

### Block-Based Network Storage

*Block-based network storage protocols are based on transferring low-level storage commands over the network infrastructure. The commands that transmit are similar to the ones used to communicate with a locally attached drive within the system hardware chassis.*

*This low-level communication traditionally relies on a SAN to transport the messages between the initiator and the target. The initiator is effectively the client system while the target system is the server—a storage array.*

*SAN is a dedicated network that is intended for storage traffic that uses a specific SAN protocol (such as Fibre Channel) for communication. The dedicated network is the traditional SAN environment, developed to overcome the limitations of Ethernet-based communication, which was designed to handle high latencies, out-of-order message delivery, and message loss.*

*The evolution of Ethernet and introduction of Ethernet enhancement protocols such as data center bridging (DCB) now allows you to use Ethernet for storage traffic also. It removes the need for a separate dedicated network. The two main block-based network storage standards using the Ethernet protocol are Fibre Channel over Ethernet (FCoE) and iSCSI.*

*Regardless of the media used for SAN connectivity, the modern block-based network storage relies on the transfer of SCSI commands, either within Fibre Channel or Ethernet frames. The SCSI protocol was introduced in the early 1980s and used a parallel SCSI cable to transfer native SCSI commands. The parallel SCSI cables are regarded as legacy technology and are not used in modern data center deployments. However, the SCSI command stack is still in use as the payload in block-based network storage communication.*

*SCSI messages and data can be transported over different physical media:*

- ***Parallel SCSI cable:*** *This transport is mainly used in traditional deployments. The latency is low, but the distance is limited to 25m and is half-duplex, so that data can flow in only one direction at a time.*

- ***Fibre Channel cable:*** *This transport is the basis for a traditional SAN deployment. Latency is low and speed is high (64 Gbps). SCSI is carried in the payload of a Fibre Channel frame between Fibre Channel ports. Fibre Channel has a lossless delivery mechanism using buffer-to-buffer credits (BB_Credits).*

- ***FCoE:*** *This transport replaces the Fibre Channel cabling with Ethernet cables and provides lossless delivery over unified I/O.*

- ***iSCSI is SCSI over TCP/IP:*** *This transport has higher latency and uses normal LAN to transport SCSI commands. Because it uses LAN and is an open protocol, it is a relatively inexpensive option for remote block storage access. With ever faster LAN networks, the iSCSI protocol is becoming more prominent. Because of its TCP/IP stack, it is also used along with NAS protocols to provide permanent storage to nonpersistent systems such as containers.*

*SCSI parallel cable is a physical cable that was introduced in the 1980s and is a legacy connectivity type. The SCSI message protocol was used over the SCSI parallel cables and is still used for storage communication today.*

![SCSI parallel cable](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/scsi_parallel_cable.png)

*Note: Another block I/O protocol is the Serial Advanced Technology Attachment (SATA). This protocol is mostly used in home desktop and laptop computers.*

*SCSI technology supports writing blocks of one or more files or databases to an external disk in a SAN. The files are written using the host system attributes, including permissions, file size, and a modification date. The SCSI channel that is used to transmit SCSI commands, data, and status is the foundation for all communications in a SAN (for SCSI devices). Connectivity between a SCSI host and SCSI device can be supported on an internal or external connection.*

*Multiple devices are supported on the channel, enabling communication between the SCSI initiator and SCSI target. The physical connectivity allows for all the devices in a chain to communicate with the storage through the SCSI protocol.*

![SCSI](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/scsi.png)

*In this figure, you can see the initiator, which is a SCSI adapter, and the target RAID array. You can also see that the SCSI cable goes from the host adapter into device #1, and next from #1 to #2, and continues in this manner. This connectivity architecture is called daisy-chaining. The left side shows the protocol view, and the right side shows the physical device view.*

*The block-based and file-based network systems are often complementary. For example, you can boot the server operating system from the block network storage, which you cannot with NAS. The LUNS that are accessible from block storage work the same as locally attached disks. Because they run on a higher OSI layer, the NAS protocols also have higher latency than the SAN protocols.*

*Note: A "LUN" or logical unit number is a unique identifier used in computer storage to designate a specific logical unit, which can be a physical or virtual storage device that executes input/output commands. It is commonly associated with the SCSI protocol and helps manage storage resources in systems like storage area networks (SANs).*

![Modern data center approach using SAN and LAN](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/using_SAN_and_LAN.png)

*In the example, the LAN and SAN networks are separate physical networks. The LAN network runs Ethernet and TCP/IP, and the SAN uses Fibre Channel connectivity. The database server connects to both the block storage (to store the database) and the server operating system, which are on the storage array LUNs accessible through SAN. The application server accesses the database over LAN, and both the application and the database servers create backups on the NAS filer. The application server also runs containers that mount their storage using iSCSI from the database server. This setup is a very realistic modern data center approach that uses both SAN and LAN.*

*The example shows how the SAN and NAS approaches are complementary.*

*Note: HBA storage refers to a Host Bus Adapter, which is a hardware component that connects a computer or server to storage devices, facilitating data transfer and communication. It helps improve performance by offloading input/output processing from the host system, allowing for faster and more efficient data management.*

**Additional Notes and Thoughts About the Example:**

Think **LAN = file + app traffic, SAN = raw disk for serious workloads.** The database server lives a double life: over **SAN (Fibre Channel + SCSI)** it sees block devices (LUNs) like *local disks* for the DB and OS (low latency, high IOPS), while over **LAN (Ethernet + TCP/IP)** it talks to the app server and NAS. The **NAS filer** serves *files* via **NFS/CIFS** (backups, shared data), not disks—so clients ask for ```/file.sql```, not block 12345.

HBAs aren’t mentioned in the text, but I spotted the truth: **HBAs are mandatory for Fibre Channel SANs**—they offload SCSI/FC processing from the CPU and live in that “HBAs” bubble in the picture. Without HBAs, Fibre Channel SAN literally doesn’t exist.

Why this design rocks: **SAN for performance-critical state (databases), NAS for shared files and backups, LAN for app-to-app chatter,** and **iSCSI for flexible, Ethernet-based block storage when FC is overkill.** Old-school purists apparently hate the mix; modern data centers thrive on it.

### Small Computer Systems Interface

*SCSI is an efficient block-based protocol for writing and reading data blocks to and from a storage device. It is suitable for block-based, structured applications such as database applications. These applications require many I/O operations per second (IOPS) to achieve high performance and transfer small blocks of data when updating fields, records, and tables. The data that SCSI transfers is in 512-byte blocks.*

*SCSI allows servers to connect to storage arrays using a single cable. Communication between the initiators (servers) and the target (storage array or any other storage device) on the SCSI bus is half-duplex, creating a multidrop topology. You will learn the characteristics of SCSI technology, the connection between initiators and targets in the SCSI protocol, and about the multidrop topology.*

*Most storage networks use the SCSI protocol for communication between servers and disk drive devices:*

- *The SCSI channel is used to transmit SCSI commands, data, and status.*

- *The most common channel is the basic parallel SCSI bus, which can be internal or external to a host.*

*SCSI uses a bus technology that supports multiple devices that attach to a controller and can support daisy chaining. Through the bus connection, a host can communicate with several SCSI devices using multiple half-duplex I/O channels.*

*Daisy chaining slightly increases SCSI scalability. Since daisy-chained storage devices are captive behind a server, this technology still has limitations from a networking perspective.*

### SCSI Protocol

*As shown in the figure, the two main functions of SCSI are the following:*

- *SCSI performs the passing of commands, status, and block data between initiators and targets.*

- *SCSI is a hierarchy of functions to assemble raw data blocks into application-readable files.*

![SCSI Protocol](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/scsi_protocol.png)

*One function of operating systems is to hide the complexity of the computing environment from the end user. Management of system resources, including memory, peripheral devices, display, and context-switching between concurrent applications, is generally concealed behind the user interface. The internal operations of the operating system must be robust and must closely monitor changes of state. They must also ensure that transactions complete within the allowable timeframes and must initiate recovery or retries if incomplete or failed procedures occur.*

*The SCSI protocol provides these functions for I/O operations for peripheral devices such as disk, tape, optical storage, printers, and scanners. This protocol is typically embedded in a device driver or logic onboard a host adapter.*

*The SCSI protocol layer sits between the operating system and the peripheral resources, so it has various functional components. Applications typically access data as files or records. Although this information might be stored on disk or tape media in the form of data blocks, retrieval of the file requires a hierarchy of functions. These functions assemble the raw data blocks into a coherent file that an application can manipulate.*

*The SCSI architecture defines the relationship between initiators (hosts) and targets (such as disks) as a client/server exchange. The Small Computer Systems Interface version 3 (SCSI-3) application client resides in the host and represents the upper layer application, file system, and operating system I/O requests. The SCSI-3 device server sits in the target device, responding to requests.*

*The bus, target, and LUN triad are defined from parallel SCSI technology. The bus represents one of several potential SCSI interfaces that are installed in the host, each supporting a string of disks. The target represents a single disk controller on the string. The LUN designation allows extra disks that a controller governs; for example, a RAID device.*

*Note: A computer bus is a communication system that transfers data between different components within a computer, such as the CPU, memory, and input/output devices. It simplifies connections by using shared pathways, which can be physical wires or circuits, to facilitate data exchange and improve efficiency.*

### Multidrop Topology and Addressing

*All the devices on a SCSI bus connect to one cable. This design, which called a multidrop topology, has these characteristics:*

- *Data bits transmit in parallel on separate wires. Control signals transmit on another set of wires.*

- *Only one device at a time can transmit, and the transmitting device has exclusive use of the bus.*

- *You must install special circuit that is called a terminator at the end of the cable. The cable must be terminated to prevent unwanted electrical effects from corrupting the signal.*

![SCSI Multidrop Topology](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/scsi_multidrop_topology.png)

*A multidrop topology has inherent limitations:*

- *Parallel transmission of data bits allows more data to be sent in a given period but complicates transmitter-receiver synchronization. Control signals cause this complication, such as clock signals transmitting on another set of wires.*

- *A multidrop topology is an inefficient way to use the available bandwidth, because only one communication session can exist at a time.*

- *Termination circuits are built into most SCSI devices, but the administrator must often set a jumper on the device to enable termination.*

- *Incorrect cable termination can cause a severe failure or intermittent, difficult-to-trace errors.*

![SCSI Multidrop Topology 2](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/scsi_multidrop_topology2.png)

*SCSI was designed to support a few devices at most. Therefore, the device addressing scheme is fairly simple and inflexible. SCSI devices use hard addressing, which has these characteristics:*

- *Each device has a series of jumpers that determine the physical address of the device, or SCSI ID. The ID is software-configurable on some devices.*

- *Each device must have a unique ID. Before adding a device to the cable, the administrator must know the ID of every other device that connects to the cable. The administrator must choose a unique ID for the new device.*

- *The ID of each device determines its priority on the bus. For example, the SCSI target with ID 7 has a higher priority than the SCSI initiator with ID 6. Each device must have exclusive use of the bus while transmitting, so ID 6 must wait until ID 7 has finished. Fixed priority makes it more difficult for administrators to control performance and quality of service (QoS).*

*The number of connectivity options for storage has continued to increase in recent years. In addition to the old standby of NAS, NFS, Fibre Channel, DAS, and iSCSI, the industry has now added FCoE.*

### Fibre Channel

*Fibre Channel is a SAN protocol that uses a dedicated SAN network to transfer SCSI storage calls between systems to transfer storage data from one system to the other. Fibre Channel is a very low latency, very reliable protocol for block storage communication over a network.*

*Fibre Channel networks use a redundant fabric approach to provide redundancy as there is direct communication between initiator and target within a fabric. Security is provided by SAN zoning, which defines where communication is allowed. LUN masking determines which initiators (Fibre Channel client interfaces) are allowed to connect to which targets (logical drives on storage array).*

*Note: SAN and Fibre Channel use specific terminology to describe its operation. The client/server relationship is not the proper way to describe the relationships but is used here for clarity.*

*Fibre Channel extends and networks SCSI:*

- *Provides high-speed transport for the SCSI payload.*

- *Uses a much more scalable serial standard.*

*Fibre Channel includes these features:*

- *Addressing for as many as 16 million devices*

- *Loop (shared) and fabric (switched) transport*

- *Host speeds of 100–12800 Mbps (1–64 Gbps)*

- *Segments of up to 10 km (without extenders)*

- *Multiple protocol support*

*Fibre Channel has become the dominant open-systems protocol for connecting servers to storage and combines the best attributes of a channel and a network.*

*The serial connectivity of Fibre Channel provides a mechanism for transporting SCSI information across high-speed networks. Fibre Channel provides high-speed transport for the SCSI payload but overcomes the distance and limitations that arise with parallel SCSI technology.*

*Fibre Channel is the integration of the best attributes of the host channel and networking technologies. It implements attributes from channel technology in the mainframe environment, including reliability and scalability. Fibre Channel also implements attributes from networking, including connectionless services, high connectivity, and long distances.*

*Fibre Channel switching is point-to-point-oriented, where the initiator and the storage target side are the points. It supports three topologies: point-to-point, arbitrated loop (similar to Token Ring), and switched fabric.*

![Fibre Channel Diagram of a Host and Storage Device](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/fibre_channel.png)

*The figure shows you the connection between a host (initiator) and a storage device (target). The connection has these characteristics:*

- *The smallest unit of data is a word. A word consists of 32 bits (4 bytes) of data that are encoded into a 40-bit form by the 8-bit or 10-bit encoding process.*

- *Words are packaged into frames. A Fibre Channel frame is equivalent to an IP packet.*

- *A sequence is a series of frames that transmit from one node to another node. Sequences are unidirectional; a sequence is a set of frames that one node uses.*

- *An exchange is a series of sequences that transmit between two nodes. The exchange is the mechanism that the two ports use to identify and manage a discrete transaction. The exchange defines an entire transaction, such as a SCSI read or write request. An exchange opens whenever a transaction begins between two ports and closes when the transaction ends. A Fibre Channel exchange is equivalent to a TCP session.*

### Fibre Channel Protocol

*The figure illustrates a SCSI-FCP ***read*** operation.*

![SCSI-FCP read operation](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/scsi-fcp_read.png)

*A SCSI-FCP ***read*** operation consists of these actions:*

1. *The initiator node generates a SCSI read request (***FCP_CMD***), which is packaged as IU 1.*

2. *The initiator FC-2 layer converts IU 1 to a single command chunk and sends it across the fabric as a single frame. This process constitutes sequence 1.*

3. *The target node processes IU 1, retrieves the requested data (***FCP_DATA***) from storage, and packages the data as IU 2.*

4. *The target converts IU 2 to one or more data chunks and sends them across the fabric. This process constitutes sequence 2.*

5. *The target node generates a status command (***FCP_RSP***) that informs the initiator that the requested data transmission is complete. The status command is packaged as IU 3.*

6. *The target converts IU 3 to a single command chunk and sends it across the fabric. This process constitutes sequence 3.*

*At this point, the I/O operation is complete. The collection of three sequences constitutes a single exchange.*

*Note: In Fibre Channel, an Information Unit (IU) is a structured collection of data that is transferred as a single sequence within the Fibre Channel protocol. IUs are used to carry commands, status, data, and control information during data transfer operations.*

![SCSI-FCP read operation](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/scsi-fcp_write.png)

**Additional Notes for Clarity:**

Think of a **SCSI-FCP read** as a **three-act play inside one envelope (the exchange):**

**Act 1 – Ask:** the initiator says *“give me blocks X–Y”* → **FCP_CMD** (IU1), one clean command flying across the fabric (sequence 1).

**Act 2 – Deliver:** the target grabs the data from disk and streams it back → **FCP_DATA** (IU2), potentially many frames but still *one logical data sequence (sequence 2).*

**Act 3 – Acknowledge:** the target finishes with *“done, no errors”* → **FCP_RSP** (IU3), another small command sequence (sequence 3).

Key mental anchor: **Command → Data → Status**, always in that order, and **all three sequences together = one exchange = one I/O**. Fibre Channel looks complex, but it’s brutally disciplined: low chat, deterministic flow, zero ambiguity — which is exactly why databases love it and Ethernet-based file protocols feel “chatty” by comparison.

*This next figure shows you a SCSI-FCP ***write*** operation, which consists of these actions:*

1. *The initiator node generates a SCSI write request (***FCP_CMD***), which the FC-4 layer packages as IU 1.*

2. *The initiator FC-2 layer converts IU 1 to a single command chunk and sends it across the fabric as a single frame. This process constitutes sequence 1.*

3. *The target node responds with a SCSI write request response (***FCP_XFR_RDY***), which is packaged as IU 2. The write request response is required for synchronization between the initiator and target.*

4. *The target converts IU 2 to a single data chunk and sends it across the fabric. This process constitutes sequence 2.*

5. *The initiator node retrieves the data* (***FCP_DATA***) *from its upper-layer protocol (ULP) buffers and packages it as IU 3.*

6. *The initiator converts IU 3 to one or more data chunks and sends them across the fabric. This process constitutes sequence 3.*

7. *The target node generates a status command (***FCP_RSP***) to confirm the end of the exchange. The command is packaged as IU 4.*

8. *The target converts IU 4 to a single command chunk and sends it across the fabric. This process constitutes sequence 4.*

*Note: The collection of four sequences constitutes a single exchange.*

![SCSI-FCP write operation](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/scsi-fcp_write2.png)

**Additional Notes for Clarity (Again):**

Think of **WRITE as “ask → get permission → send data → get receipt”.** First, the initiator sends **FCP_CMD** (“I want to write”) — that’s sequence 1. Then the *target* replies with **FCP_XFR_RDY** (“okay, I’m ready, send it”) — this extra step is the big difference vs READ and exists to avoid overruns and sync buffers. After that, the initiator pushes the actual **FCP_DATA** (sequence 3), and finally the target sends **FCP_RSP** (“got it, all good”) to close the exchange.

Easy memory trick: **READ = 3 acts (CMD → DATA → RSP), WRITE = 4 acts (CMD → XFR_RDY → DATA → RSP).**

Philosophically: READ is *target-driven* (target sends data when ready), WRITE is *target-controlled* (target explicitly says when it’s safe to receive). Once you see **XFR_RDY** as flow control, the whole thing snaps into place.

### Fibre Channel HBAs

*Host bus adapters (HBAs) are I/O adapters that maximize performance by performing protocol-processing functions in silicon. HBAs are roughly analogous to network interface cards (NICs) but are optimized for SANs and provide features that are particular to storage.*

*The following figure contrasts HBAs with NICs, showing that HBAs offload protocol-processing functions into silicon.*

![HBAs with NICs](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/HBAs_with_NICs.png)

*With NICs, software drivers perform protocol-processing functions such as flow control, sequencing, segmentation and reassembly, and error correction. The HBA offloads these protocol-processing functions onto the HBA hardware, usually some combination of an ASIC and firmware. Offloading these functions is necessary to provide the performance that storage networks require.*

*NICs can use more than 80 percent of a server CPU capacity. I/O processing adds considerable real cost to what might appear to be an inexpensive NIC.*

*HBAs manage I/O transactions with little or no involvement of the server CPU. Fibre Channel HBAs can provide throughput at nearly 95 percent of the link speed with less than 10 percent of server CPU utilization.*

### Internet Small Computer Systems Interface

*iSCSI is a network service streaming SCSI commands over TCP over longer distances. While SCSI is a client/server model, iSCSI links storage devices over TCP/IP. With free software-based drivers or a hardware implementation in a NIC, it discovers the targets using iSCSI node names. You will learn about iSCSI operation, its concepts, and the differences between software-based drivers and hardware-based NICs.*

*iSCSI encapsulates SCSI commands, data, and status over an IP transport for linking storage devices with servers. It supports the following features:*

- *iSCSI allows IP hosts to gain access to Fibre Channel-based storage targets.*

- *iSCSI uses current IP-based infrastructures and management facilities.*

- *TCP (port 3260) provides congestion control and in-order delivery of error-free data.*

- *iSCSI addresses distance limitations.*

- *The Cisco Multilayer Director Switch (Cisco MDS) 9000 18/4-Port Multiservice Module (MSM) provides transparent SCSI routing.*

*The iSCSI transport protocol operates in addition to TCP and encapsulates SCSI-level commands and data into IP for a TCP/IP byte stream, as illustrated in the figure. iSCSI is a means of transporting SCSI packets over TCP/IP, providing for an interoperable solution that can take advantage of the current IP-based infrastructures and management facilities. The SCSI protocol is mapped over various transports, including parallel SCSI, Intelligent Platform Management Interface (IPMI), IEEE 1394, FireWire, and Fibre Channel. These transports are I/O-specific and have limited distance capabilities.*

![iSCSI](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/iscsi_transport_protocol.png)

*Mapping SCSI (I/O) over TCP ensures that high-volume storage transfers have in-order delivery and error-free data with congestion control. This process allows IP hosts to gain access to previously isolated Fibre Channel-based storage targets and overcomes distance limitations.*

*iSCSI is an end-to-end protocol with human-readable SCSI device, node, and naming. It includes these base components:*

- *IP Security (IPsec) connectivity security*

- *Authentication for access configuration*

- *Discovery of iSCSI nodes*

- *Remote boot process*

- *iSCSI MIB standards*

*The IETF IP Storage Working Group defined the iSCSI protocol.*

### iSCSI Concepts

*iSCSI defines a client/server relationship between nodes: the iSCSI initiator (host) and the iSCSI target (storage). iSCSI standards define this concept as the network entity. The iSCSI node name identifies the iSCSI node.*

*If the target node is a storage array, it may contain one or more SCSI LUNs.*

*As shown in this figure, iSCSI initiator nodes communicate with iSCSI target nodes through network portals. Network portals connect to the IP network and are identified by an IP address.*

![iSCSI Communication](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/iscsi_communication_diagram.png)

### iSCSI Node Names

*iSCSI node names are associated with iSCSI nodes, not adapters. The Node_Name can be up to 255 bytes long and formatted as a human-readable string in UTF-8 encoding. It is used for iSCSI login and target discovery.*

*Every iSCSI node is identified by an iSCSI Node_Name in one of three formats:*

- ***IQN:*** *An iSCSI Qualified Name (IQN) can be as much as 255 bytes and is a human-readable UTF-8 encoded string.*

- ***EUI:*** *An Extended Unique Identifier (EUI) is an 8-byte hexadecimal number that the IEEE defines and allocates.*

- ***NAA:*** *A Network Address Authority (NAA) is an 8- or 16-byte hexadecimal number that the Fibre Channel T11 Committee defines and allocates.*

![iSCSI Name Types](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/iscsi_name_types.png)

*The iSCSI driver typically uses the IQN format. Manufacturers of native iSCSI devices use the EUI format.*

### Software-Based iSCSI Drivers

*The software-based iSCSI model that is represented in the following figure has these characteristics:*

- *iSCSI is a network service that is enabled using an iSCSI software driver and optional hardware.*

- *The internal TCP/IP stack consumes CPU resources during data transfer.*

- *The driver performs error handling and consumes even more CPU resources.*

- *TCP/IP causes high latency; it is unsuitable for latency-sensitive applications.*

- *The solution is inexpensive; it has a free iSCSI driver.*

![Software-Based iSCSI Drivers](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/software_iscsi_drivers.png)

*iSCSI drivers are typically free and provide a low-cost solution to customers that do not require high performance or low latency.*

*The iSCSI driver performs all SCSI processing, TCP/IP processing, and error recovery. Remember, because all these operations are performed on a CPU, an iSCSI driver running on a 1-GHz CPU spends nearly 95 percent of its CPU cycles when moving data through a NIC at 1 Gbps.*

*However, current host CPUs are much faster and thus use far fewer of their CPU cycles moving data at 1 Gbps, which makes this low-cost solution practical in some environments.*

### TCP and iSCSI Offload Engines

*The properties of iSCSI hardware implementation within the specialized NIC are the following:*

- *It offloads TCP and iSCSI processing into hardware:*

***Full offload:*** *This method involves iSCSI and TCP offload (iSCSI HBA).*

***Partial offload:*** *This method involves the TCP/IP Offload Engine (TOE).*

- *It relieves host CPU resources from iSCSI and TCP processing.*

- *It does not necessarily increase performance unless the CPU is busy.*

- *It offers wire-rate iSCSI performance. This property is useful only when the host must support high sustained loads.*

![iSCSI Offload Engines](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/iscsi_offload_engines.png)

*The figure shows the differences between a standard NIC, one with TOE, and one with an iSCSI HBA.*

*Partial-offload TOE cards offload TCP/IP processing to the TOE but pass all errors (packet loss) to the driver running on the host CPU. In a lossy network, partial-offload TOE cards may perform worse than usual.*

*Full-offload TOE cards offload TCP/IP processing and error recovery to the TOE card. The host CPU is still responsible for SCSI and iSCSI processing.*

*The iSCSI HBA offloads TCP/IP processing and iSCSI processing to custom ASICs on the iSCSI HBA. Although they are relatively expensive, iSCSI HBAs provide lower latency and higher throughput than iSCSI software drivers or TOE cards.*

*Note: The current host CPU processors have faster performance. Using NICs with TOE is rarely as cost-effective as using software iSCSI drivers.*

### Comparison of Block-Based and File-Based Protocols

*The table compares the protocols that are discussed in this section.*

![Protocols Comparison](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/comparison_of_file_protocols.png)

## Fibre Channel Storage Networking

*Fibre Channel is a high-speed network technology (commonly running at 2-, 4-, 8-, 16-, 32-, and 64-Gbps rates) primarily used to connect computer data storage. Fibre Channel is standardized in the T11 Technical Committee of the InterNational Committee for Information Technology Standards (INCITS).*

### Fibre Channel SAN Topologies

*SANs are deployed in various topologies, depending on the network configuration. You will learn about the difference between the three Fibre Channel SAN topologies that you can use for initiator-to-target connectivity.*

*In a storage environment, communication happens between an initiator and a target device. You can use three main topologies, which are shown in the figure, to connect the two devices:*

- *Point-to-point*

- *Fibre Channel Arbitrated Loop (FC-AL)*

- *Switched fabric network (usually referred to as the SAN)*

![SAN Topologies](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/SAN_topologies.png)

### Point-to-Point Topology

*The point-to-point topology is the simplest Fibre Channel storage configuration. This topology is often referred to as direct-attached storage (DAS) architecture. Originally, this architecture was achieved using a Small Computer System Interface (SCSI) bus, but Fibre Channel cabling has now superseded SCSI.*

*As the name suggests, a point-to-point configuration is a one-to-one connection between a host and a storage device. In this architecture, the storage is dedicated to the server. This design does not provide a very scalable solution, but it does provide very good security because no other device has access to the same storage device.*

*The figure illustrates a server that is connected to a storage device through a Fibre Channel (FC in figures) link.*

![FC point-to-point](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/FC_point-to-point.png)

### Arbitrated Loop Topology

*The following are important limitations of the FC-AL topology:*

- *Loops suffer from poor performance. Because there is only one data path, only one pair of devices can communicate at a given time. Therefore, all the devices on the loop share the available bandwidth.*

- *Loops have a higher latency than other topologies. Devices must negotiate for control of the loop before they can send traffic to their target devices.*

- *Loops are not very scalable. The FC-AL protocol provides for only 127 unique addresses, one of which is reserved for attaching the loop to a Fibre Channel switched fabric. The other 126 addresses are usable by nodes (servers and storage devices). In practice, only about a dozen devices can connect to the loop before performance drops below acceptable levels.*

- *Loop configurations are susceptible to device failures. If one device fails on the loop, many devices are affected.*

*The FC-AL topology is more scalable than the point-to-point topology. In the FC-AL topology, all servers have access to all storage devices, allowing storage resources to be better used. The I/O speed between the initiator and target depends on their locations in the loop. Although FC-AL is scalable to 127 devices, typically 12 or fewer devices are attached.*

![Arbitrated Loop](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/FC_arbitrated_loop.png)

### Switched Fabric Topology

*The most scalable topology for initiator-to-target connectivity is the switched fabric topology, often referred to as the SAN or fabric. The switched fabric topology incorporates one or more high-bandwidth Fibre Channel switches to manage data traffic between multiple host and storage devices.*

![Switched Fabric](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/FC_switched_fabric.png)

### Fibre Channel SAN Overview

*The Fibre Channel technology transports data between devices and is one of the protocols that are used for SANs. Traditional storage technologies, such as SCSI, are designed for controlled, local environments. They support few devices and only short distances, but they deliver data quickly and reliably. Traditional data network technologies, such as Ethernet, were originally designed for distributed environments. Ethernet supports many devices and long distances, but delivery of data can be delayed and often relies on upper-layer protocols (ULPs) to provide reliability and redelivery of traffic.*

*Fibre Channel combines the best of the SCSI and Ethernet worlds. Fibre Channel is designed to support many devices and longer distances, and it provides the reliable data delivery that the SCSI protocol requires between an initiator and target.*

*Servers often connect to the LAN and the SAN, as depicted in the figure.*

![Server with LAN and SAN](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/server_LAN_and_SAN.png)

### FC-SW Protocol

*The Fibre Channel Switched Fabric (FC-SW) protocol differs from the FC-AL topology in several important ways:*

- *Switches can support multiple simultaneous conversations. Each conversation between the two devices can use the full link bandwidth.*

- *The FC-SW protocol device-addressing scheme allows more than 16 million ports to connect to the SAN. Current implementations can support hundreds or thousands of nodes using large director-class switches.*

- *The FC-SW protocol defines several management services that increase the scalability, manageability, and security of the SAN.*

*Because of the limitations of the FC-AL topology, most modern organizations choose to implement a switched fabric network topology, which offers greater scalability, performance, reliability, and manageability.*

### Fibre Channel Port Types

*Servers and storage devices that communicate over the Fibre Channel have their ports that are configured in various types, depending on the operation. You will learn about the various Fibre Channel ports that can be found in the SAN.*

*Fibre Channel ports are intelligent interface points on the Fibre Channel SAN, as shown in the following figure. They are found embedded in various devices:*

- *I/O adapters*

- *Array or tape controllers*

- *Switched fabrics*

![FC Ports](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/FC_ports.png)

*When a server or storage device communicates, the interface point acts as the initiator or target for the connection. The server or storage device issues SCSI commands, which the interface point formats to transmit to the target device.*

*These ports recognize the Fibre Channel. The Fibre Channel switch recognizes which type of device is attaching to the SAN and configures the ports accordingly.*

*As depicted in the figure, you can configure various Fibre Channel port types on a switch:*

- ***E Port:*** *In expansion port (E Port) mode, an interface functions as a fabric expansion port. This port connects to another E Port to create an interswitch link (ISL) between the two switches. E Ports carry frames between switches for configuration and fabric management. They also serve as a conduit between switches for frames that are destined to remote node ports (N Ports) and node loop ports (NL Ports).*

- ***F Port:*** *In F-Port mode, an interface functions as a fabric port. This port connects to a peripheral device (such as a host or disk) that operates as an N Port. An F Port can attach to only 1 N Port.*

- ***FL Port:*** *In fabric loop port (FL Port) mode, an interface functions as a fabric loop port. This port connects to one or more NL Ports (including FL Ports in other switches) to form a public FC-AL. If more than one FL Port is detected on the FC-AL during initialization, only one FL Port becomes operational; the other FL Ports enter nonparticipating mode.*

- ***TE Port:*** *In trunking E Port (TE Port) mode, an interface functions as a trunking expansion port. This port connects to another TE Port to create an Enhanced Inter-Switch Link (EISL) between the two switches. TE Ports are specific to Cisco MDS 9000 Series Switches and expand the functionality of E Ports to support VSAN trunking and transport QoS parameters. When an interface is in TE Port mode, all frames that are transmitted are in the EISL frame format, which contains VSAN information. Interconnected switches use the VSAN_ID to multiplex traffic from one or more VSANs across the same physical link.*

- ***NP Port:*** *A node-proxy port (NP Port) is a port on a device that is in N-Port Virtualization (NPV) mode and connects to the core switch via an F Port. NP Ports function like N Ports but in addition to providing N-Port operations, they also function as proxies for multiple physical N Ports.*

- ***TF Port:*** *In trunking fabric port (TF Port) mode, an interface functions as a trunking expansion port. This interface connects to another trunking node port (TN Port) or trunked NP port (TNP Port) to create a link between a core switch and an NPV switch. (Or between an HBA link to carry tagged frames.) TF Ports are specific to Cisco MDS 9000 Series switches and expand the functionality of F Ports to support VSAN trunking. In TF-Port mode, all frames are transmitted in the EISL frame format, which contains VSAN information.*

- ***TNP-Port:*** *In TNP-Port mode, an interface functions as a trunking expansion port. This interface connects to a TF Port to create a link to a core N-Port ID Virtualization (NPIV) switch from an NPV switch to carry tagged frames.*

- ***Auto mode:*** *An interface that is configured in auto mode can operate in one of the following modes: F Port, FL Port, E Port, TE Port, or TF Port, with the port mode being determined during interface initialization.*

*In the figure, you can also see two other ports that you cannot configure on a Fibre Channel switch:*

- ***N Port:*** *A node port (N Port) is a port that connects the end device to an F port on a Fibre Channel switch. It allows nodes (storage devices and servers) to participate in Fibre Channel communication.*

- ***NL Port:*** *A node loop port (NL Port) has characteristics of an N port, but it is used in FC-AL.*

![FC Port Types](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/FC_port_types.png)

**Additional Notes and Summarization:**

Think **core idea first:** *ports are defined by who they talk to.*

- **Switch ↔ Switch = E / TE** (plain E is basic ISL, **TE = E on steroids** with VSAN trunking, Cisco-only).

- **Switch ↔ End device (host/storage) = F** (one device only, classic fabric edge).

- **Loop weirdness = FL / NL** (legacy FC-AL, mentally file this under “museum tech”).

Now the **virtualization twist:**

- **NP / TNP / TF** exist to let **many virtual N ports pretend to be one** when talking to the core — that’s NPV/NPIV magic. **TF is basically “F-port but VLANs-for-FC (VSANs)”**, and **TNP is the NPV-side mate.**

Finally, the killer shortcut: **E/TE = fabric plumbing, F/TF = device edge, NP/TNP = virtualization proxies, Auto = YOLO negotiator.** If you remember *who talks to whom* and *whether VSAN tagging is involved,* the ports soup suddenly snaps into focus.

### Fibre Channel Addressing

*Fibre Channel uses World Wide Names (WWNs) (64 bits) and Fibre Channel IDs (24 bits). WWNs are unique identifiers that are hardcoded into Fibre Channel devices while Fibre Channel IDs are dynamically acquired addresses that are routable in a switch fabric. You will learn about the Fibre Channel port and node addresses, what they serve, the two types of addresses, the addressing scheme, and the address space.*

![FC Addressing](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/FC_addressing.png)

*Each Fibre Channel port has at least one WWN. Vendors buy blocks of WWNs from the IEEE and allocate them to devices in the factory.*

*WWNs are important for enabling Cisco Fabric Services, which simplifies provisioning by automatically distributing configuration information to all switches in the network. WWNs have the following characteristics:*

- *Guaranteed to be globally unique*

- *Associated permanently with devices*

*These characteristics ensure that the fabric can reliably identify and locate devices.*

*When a management service or application must quickly locate a particular device, the following events occur:*

1. *The service or application queries the switch name server service with the WWN of the target device.*

2. *The name server looks up and returns the current port address that is associated with the target WWN.*

3. *The service or application communicates with the target device, using the port address.*

*The two types of WWNs are node WWNs (nWWNs) and port WWNs (pWWNs):*

- *nWWNs uniquely identify devices. Every HBA, array controller, switch, gateway, and Fibre Channel disk drive has a single unique nWWN.*

- *pWWNs uniquely identify each port in a device. A dual-ported HBA has three WWNs: one nWWN and one pWWN for each port.*

*The nWWNs and pWWNs are necessary because devices can have multiple ports. If a device has only one port, the nWWN and pWWN may be the same. If a device has multiple ports, the pWWN is used to uniquely identify each port.*

*Ports must be uniquely identifiable because each port participates in a unique data path. On the other hand, nWWNs are required because the node itself must sometimes be uniquely identified. For example, path failover and multiplexing software can detect redundant paths to a device by observing that the same nWWN is associated with multiple pWWNs.*

### Switched Fabric Address Space

*The 24-bit Fibre Channel ID address consists of these elements:*

- *The domain ID (8-bit) is used to define a switch. Each switch receives a unique domain ID. 1 byte allows up to 256 possible addresses. Because some of these addresses are reserved, such as the one for broadcast, only 239 addresses are available. This number means that you can theoretically have as many as 239 switches in your SAN environment.*

- *The area ID (8-bit) is used to identify groups of ports within a domain or within a switch. Areas are also used to uniquely identify fabric-attached arbitrated loops where each fabric-attached loop receives a unique area ID.*

- *The Port ID (8-bit) is the final part of the address and provides 256 addresses for identifying attached N Ports and NL Ports.*

![Switched Fabric Address Space](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/switched_fabric_address_space.png)

## VSAN Configuration and Verification

*A SAN is a dedicated network that interconnects hosts and storage devices primarily to exchange SCSI traffic. They can be designed with various topologies where interconnections between devices are made by using physical links (cables). A set of protocols that run over the SAN manage routing, naming, and zoning.*

*A VSAN is a virtual SAN. Similar to VLANs in LANs, VSANs allow multiple logical SANs on a single fabric, providing data consolidation and security. They are used in data centers for servers to access the data on storage devices.*

*Cisco Nexus switches and Cisco Multilayer Director Switches (MDS) support VSAN technology for easier configuration of your storage needs.*

*You will learn the purpose of VSANs in a network and how to configure, manage, and verify VSANs on Cisco Nexus switches and Cisco MDS switches.*

*VSANs are logical SANs, allowing data consolidation of multiple users on a single shared SAN infrastructure that is transparent to the user. VSANs (sometimes referred to as virtual domains) allow you to configure the shared storage infrastructure, based on your security and data privacy needs. The concept of VSANs is similar to the VLAN technology used in LANs where the tagged frame maintains the identifier until it reaches its destination.*

*Virtual domains are similar to VLANs in many ways:*

- *Hardware-based isolation of tagged traffic belonging to various VSANs requires no special drivers or configuration at the end nodes, such as hosts and disks.*

- *Traffic is tagged at the ingress port and carried across VSANs.*

- *Each Fibre Channel fabric service maintains a distinct database for each newly created VSAN. These services include the zone server, name server, management server, and principal switch choice. Each service runs independently on each VSAN and is independently managed and configured.*

- *Each VSAN has its own principal switch and domain ID allocation policy, which is static or dynamic. Principal switches for various VSANs do not need to reside on the same physical switch. Each switch has a distinct domain ID for each active VSAN.*

*Built on the common physical fabric, VSANs provide fabric services on their own, independently from one another. You can configure Inter-Virtual Fabric Routing (IVR) without extra hardware for sharing common resources.*

![VSAN Numbers](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vsan_numbers.png)

*Similar to VLANs, where some VLANs are reserved and cannot be deleted, some VSANs are reserved as well. You can see them in this table.*

### VSAN Configuration

*The example shows a three-step procedure that is necessary for the VSAN configuration. The first task that you must perform is the VSAN database configuration. Then, you create the VSAN by specifying the ID and name of a new VSAN. Remember that VSAN names are not required but are recommended for ease of management. The last step is assigning the membership of the specified interface to a particular VSAN.*

![VSAN Configuration Steps](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vsan_config.png)

*When you delete an active VSAN, all its attributes are removed from the running configuration. All ports in that VSAN are made inactive, and the ports are moved to the isolated VSAN (VSAN 4094).*

*If you re-create the same VSAN, the ports are not assigned to that VSAN, and you must reconfigure them.*

### VSAN Trunking and Configuration

*A single link between two devices can carry multiple VLANs or VSANs using trunking with various trunking modes.*

![VSAN Trunking](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vsan_trunking.png)

*The default configuration on Cisco switches is that trunking is ON. The table shows you all other possible combinations of the administrative and operational modes between the two switches.*

![VSAN Combinations](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/vsan_combinations.png)

*Trunking mode is specific to Cisco switches that support Fibre Channel and FCoE.*

*Three trunking mode options are available:*

- ***On:*** *This option explicitly enables trunking mode.*

- ***Off:*** *This option explicitly disables trunking mode.*

- ***Auto:*** *This option is a passive mode. The other end of the connection must request the forming of a trunk; otherwise, the trunk mode will be off.*

*Trunking mode is specific to Cisco switches that are Fibre Channel–capable. A Cisco proprietary parameter transmits over the E Port link to determine if the remote switch is another Cisco switch and therefore supports trunk mode. If the device on the other end of the link responds with the same parameter, the port becomes a TE Port. If the other device does not support trunk mode, the parameter is ignored. Therefore, the equipment of other vendors will not operate in trunking mode; they operate as regular E Ports in interoperability mode. VSANs are not present in interoperability mode except for the one VSAN in which the port of the Cisco switch is configured.*

### SAN Port Channels

*SAN port channels refer to the aggregation of multiple physical interfaces into one logical interface to provide higher aggregated bandwidth, load balancing, and link redundancy.*

*In a data center, storage devices usually connect to the Cisco MDS switches, which connect to the aggregation devices, like the Cisco Nexus 9000 Series switches. Between these devices, a SAN port channel is configured.*

*You can create a SAN port channel with members that are TE ports, as you can see on the right side of the figure. In this configuration, the port channel implements a logical EISL (carrying traffic for multiple VSANs).*

![SAN Port Channels](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/san_port_channels.png)

*VSAN trunking enables a link transmitting frames in the EISL format to carry traffic for multiple VSANs. When trunking is operational on an E Port, that E Port becomes a TE Port. EISLs connect only between Cisco switches, as shown on the right side of the figure.*

*Before configuring a SAN port channel, consider the following guidelines:*

## Lab: Configure VSANs

### Verify the Inventory of Cisco Nexus 5000 Switch and Configure Interfaces

**1. Big Picture First (mental anchor):**

Think of this lab as answering *one core question:* “How do I turn a Nexus 5000 from an Ethernet switch into *part* of a Fibre Channel SAN — without adding new hardware?”

The answer is:

- **VSANs** = VLANs for Fibre Channel

- **Unified Ports** = ports that can *be* Ethernet **or** Fibre Channel

- **FCoE** = a bridge that lets FC logic live on Ethernet-capable hardware

You’re not *yet* doing zoning, FCoE frames, or storage traffic — you’re just *teaching the switch to speak Fibre Channel at the port level.*

**2. VSAN vs SAN (the clean mental split):**

Physical SAN:

- Separate physical network

- Fibre Channel only

- Dedicated switches, HBAs, cabling

VSAN:

- Logical fabric inside FC switches

- Ports are grouped into isolated fabrics

- Exactly like VLANs, but for FC control + data planes

- Failures, routing, zoning stay *inside* the VSAN

One physical FC switch can host *many independent SANs.*

**3. Why the Nexus 5000 Matters Here:**

Your switch model:

```
N5K-C5548UP-SUP
```

**UP = Unified Ports** ← yes, this is the important part! That tells you:

- Each port can be Ethernet *or* Fibre Channel

- But not arbitrarily — ports are grouped into *port groups*

- Changing mode = *ASIC behavior change* → reboot required

**4. Why ```show module``` Matters:**

This output answers:

- What hardware is installed

- Whether FC is even *possible*

- Which ports belong to which ASIC / port group

**5. The “Why Slot 1?”**

I wanted to be sure how they knew to use **slot 1.** Here’s the logic chain:

- ```show module``` shows:

```
Mod 1 → N5K-C5548UP-SUP
```

- Ports ```Eth1/21–32``` live on **module 1**

- Nexus unified ports are reconfigured **per module / port group**

Therefore:

```
slot 1
port 21-32 type fc
```

**6. Why Ports 21–32 All Flip Together:**

This is *classic Nexus behavior:*

- Ports share internal forwarding resources

- FC and Ethernet use *different buffer models*

- Mixing modes inside a group would break flow control

So Cisco forces: *“All ports in this group must agree on reality.”*

That’s why *one FC port = many ports converted.*

**7. Key Config Blocks (worth preserving verbatim):**

These are *core cookbook artifacts* — definitely smart to keep them.

```
feature fcoe
```

Enables the FC/FCoE personality logic.

```
slot 1
port 21-32 type fc
```

Physically converts ports to Fibre Channel.

```
copy running-config startup-config
reload
```

Mandatory because this is a hardware-mode change.

**8. Post-Reload Sanity Check:**

This ```show interface brief``` output is your *golden confirmation:*

```
fc1/21
fc1/22
```

Key signals:

- Interfaces now appear as ```fc1/x```, not ```eth1/x```

- Separate FC table = correct ASIC pipeline active

- ```sfpAbsent``` is fine — FC optics aren’t inserted everywhere

Loss of previous interface config? Expected and normal.

**9. Why the SFP Looked “Wrong” Earlier:**

Before conversion:

- FC SFPs were plugged into Ethernet-mode ports

- Switch didn’t understand the optics

- Result: weird SFP types, disabled links

After conversion:

- Same optics suddenly make sense

- FC stack activates

- Links can come up (once connected to MDS)

**10. One-Line Mental Summary:**

*Ethernet ports become Fibre Channel ports only after the switch itself changes personality — and that change happens in groups, not individually.*

## Create a SAN Port Channel and Add Interfaces to the Port Channel

**Big picture first (mental map):**

Think of a *SAN port channel* as *EtherChannel for Fibre Channel:* multiple FC links bundled into one logical pipe for *redundancy + throughput + failure tolerance.*

Unlike LAN hiccups, SAN failures can **panic servers or corrupt data,** so *port channels are not optional fluff*—they’re survival gear.

**Topology-wise:**

- Hosts / storage → **Cisco MDS**

- MDS → **Nexus 5K/9K**

- Between MDS and Nexus → **SAN port-channel**

*Key concepts to lock into memory:*

**1. SAN Port Channel ≠ Ethernet Port Channel:**

- Same idea, different rules.

- *All member ports must match* (speed, mode, etc.) or the channel won’t form.

- FC is *much stricter* than Ethernet. Mnemonic: *LAN = forgiving, SAN = unforgiving*

**2. Port-channel IDs:**

- Valid range: **1–256**

- IDs **do NOT have to match** on both sides

- *Cisco strongly recommends matching IDs* for sanity and troubleshooting

Use this before picking a number:

```
show san-port-channel usage
```

**3. Why ```force``` exists (important clarity):**

You hit this error:

```
command failed: port not compatible [speed]
```

What happened?

- You configured *speed 4G* on the *port-channel*

- The *physical FC ports still had default settings*

- SAN said: *“Nope. Mismatch.”*

```channel-group 10 force``` does this:

- Overwrites the *physical interfaces*

- Forces them to *inherit the port-channel’s config*

- Prevents subtle mismatches that would otherwise break the fabric

Think of ```force``` as: *“Stop arguing, you’re all wearing the same uniform now.”*

Why Cisco warns you: If you do this on live links *without an alternate path,* traffic will flap. That’s why they recommend using it carefully.

**4. Shutdown behavior (classic Cisco gotcha):**

When you add FC interfaces to a SAN port channel:

- Cisco *automatically shuts them down*

This is *intentional:*

- Prevents half-formed fabrics

- Avoids inconsistent FC states

Best practice:

```
no shutdown
```

→ *on the port-channel interface,* not each physical port (one command, all members come up cleanly)

**Cookbook-friendly command flow:**

**On Nexus 5K (N5K-12):**

```
configure terminal
interface san-port-channel 10
 switchport speed 4
```

Add member ports:

```
interface fc 1/21-22
 channel-group 10 force
```

Bring it up:

```
interface san-port-channel 10
 no shutdown
```

**On Cisco MDS (MDS-12):**

```
configure terminal
interface fc 1/1-2
 channel-group 10 force
 no shutdown
```

Verify:

```
show port-channel database
```

Expected sanity output:

- Operational mode: **on**

- Ports: **up**

- First operational port listed

**Practical “state of the world” sanity map:**

```
[ Nexus 5K ] ==== SAN Port-Channel 10 ==== [ Cisco MDS ]
   fc1/21 \                              / fc1/1
   fc1/22  \____ logical FC bundle _____/  fc1/2
```

- One logical FC link

- Multiple physical paths

- Fabric stays alive if one link dies

**Final takeaways:**

- SAN port channels are *mandatory for resilience*

- *Config consistency matters more than speed*

- ```force``` is powerful, necessary, and dangerous if misused

- Always bring links up via the *port-channel*

- If SAN breaks, *servers cry first*

### Configure the Inter-Switch Links and Default VSAN Configuration

**Cookbook Mental Map:**

Think of this section as *“making the SAN links actually carry the right traffic”.* You already built the roads (FC ports + SAN port-channel). Now you’re defining *which virtual SANs are allowed to drive on them.*

**1. Big Picture (TL;DR Mental Model):**

- VSAN = VLAN for Fibre Channel

- ISL (E/TE port) = trunk

- VSAN allowed list = VLAN allowed list

- Both ends must agree or nothing works

- Default VSAN 1 exists, but is evil → don’t use it

Imagine two switches shouting *“I speak VSAN 1012!”* If one side doesn’t, traffic just silently dies.

**2. Trunking in Fibre Channel (Key Concepts):**

*FC Trunking Basics:*

- FC links can carry *multiple VSANs over one physical link*

- Cisco enables VSAN trunking *by default*

- Between Cisco switches, an ISL becomes an *EISL (TE Port)* automatically

*Trunk Modes (memorize like Ethernet):*

- **on** → force trunk

- **off** → never trunk

- **auto** → passive (other side must request)

Rule of pain avoidance: the VSAN must be *allowed on both ends,* or it does not exist.

**3. Why Allowed VSAN Lists Matter:**

- TE ports allow *all VSANs by default*. That’s convenient but sloppy.

- Best practice: *allow only active VSANs*

- Same logic as pruning VLANs on Ethernet trunks

*Command you must remember:*

```
switchport trunk allowed vsan <list>
```

**4. Create VSAN 1012 (Fabric-Wide Step):**

**On MDS-12:**

```
conf t
vsan database
vsan 1012
```

**On N5K-12:**

```
conf t
vsan database
vsan 1012
exit
exit
```

Why both? VSANs are *local objects.* No magic propagation.

**5. Default VSAN Reality Check:**

- All FC ports start in *VSAN 1*

- VSAN 1 *cannot be deleted*

- Exactly like VLAN 1: exists, works, should not be used

You can leave ports in VSAN 1 temporarily—but move them ASAP.

**6. Bind VSAN 1012 to the SAN Port Channel:**

This is the *“assign VLAN to trunk”* moment.

**On N5K-12:**

```
conf t
vsan database
vsan 1012 interface san-port-channel 10
```

**On MDS-12:**

```
conf t
vsan database
vsan 1012 interface san-port-channel 10
```

**Important:** VSAN membership is applied to the **port-channel**, not individual FC ports.

**7. Bring the Port Channel to Life (Speed + No Shut):**

You previously forced speed mismatches—now normalize it.

**On N5K-12:**

```
conf t
interface san-port-channel 10
switchport speed auto
no shutdown
```

**On MDS-12:**

```
conf t
interface port-channel 10
switchport speed auto
no shutdown
```

**Rule:** Speed must match on both ends, but **auto is safest** once negotiation is allowed.

**8. Verification (What Actually Matters):**

You don’t need the whole ```show interface brief``` dump every time. Focus on:

- Port-channel is up

- Mode = TE

- VSAN = 1012

- Speed negotiated

- Members are up

Key command:

```
show interface brief
```

or on MDS:

```
show port-channel database
```

**9. Why This Order Matters (Hidden Logic):**

Cisco didn’t explain it well, so here it is clean:

1. **Physical FC ports** → exist

2. **SAN port-channel** → aggregates them

3. **VSAN created** → defines fabric

4. **VSAN bound to port-channel** → allows traffic

5. **Trunking enabled** → multiplexes VSANs

5. **No shut** → traffic finally flows

Miss *any* step → silent failure (classic SAN behavior).

**10. “State of the World” Sanity Map:**

```
[N5K-12] ==== san-port-channel 10 ==== [MDS-12]
     |                                     |
     |---- VSAN 1012 allowed & active -----|
     |                                     |
  fc1/21-22                           fc1/1-2
     |                                     |
   TE Port                              TE Port
```

- Redundant links

- Trunking enabled

- VSAN scoped & controlled

- Ready for zoning next

Cisco SAN labs are overly verbose but conceptually simple. If you reduce everything to:

**“VSAN = VLAN, ISL = trunk, SAN port-channel = EtherChannel”**

…you suddenly stop suffering.

### Configure the FCoE SAN Towards the Host System

**Big Picture: What This Step Actually Does (Mental Map First):**

You are *extending the Fibre Channel SAN to a host using Ethernet* via *FCoE.*

In one sentence: **Ethernet (VLAN 1000) → FCoE → virtual FC interface (vfc1000) → VSAN 1012 → FC fabric**

Think of this as *wrapping FC frames inside Ethernet,* then unwrapping them at the switch and injecting them into the SAN fabric.

**SAN Port Rules:**

Let’s lock these in first!

- **E ↔ E** → switch-to-switch (fabric)

- **F ↔ N** → switch-to-host/storage (**1:1** only)

- **F Port limitation** → one host, one port (problem in virtualized hosts)

- **NPIV / NPV** → solve the “many VMs, one wire” problem

- **TF ↔ TN** → trunked FCoE version of F↔N (this lab uses this)

In *this lab,* **vfc1000 becomes a TF port,** and the UCS side presents **TN** ports.

**Step-by-Step: What You’re Really Building**

**1. Identify the Host-Facing Ethernet Port:**

```
show run interface eth 1/9
```

Key insight:

- *Eth1/9 connects to UCS*

- It stays *Ethernet,* not FC

- FCoE will ride *on top* of this

**2. Create the FCoE VLAN (Ethernet Side):**

```
vlan 1000
fcoe vsan 1012
```

Mental model:

- VLAN 1000 = *FCoE envelope*

- VSAN 1012 = *SAN fabric destination*

- This command is the *bridge between Ethernet and FC worlds*

Verification (good to preserve):

```
show vlan fcoe 1000
```

**3. Create a Virtual Fibre Channel Interface (The Magic Glue):**

```
interface vfc1000
bind interface Ethernet1/9
```

*What this means:*

- ```vfc1000``` = a *logical* FC port

- It borrows the *physical wire* from Eth1/9

- This is how *FCoE becomes “real FC” inside the switch*

No bind = no SAN traffic. Period.

**4. Control Which VSANs Are Allowed (Trunking Rules):**

```
switchport trunk allowed vsan 1012
```

Optional expansion:

```
switchport trunk allowed vsan add 2212
```

*Think VLAN trunks, but for VSANs:*

- Allowed ≠ member

- This only controls *what may pass*

**5. Actually Add vfc1000 to the VSAN (Easy to Forget):**

This is a classic gotcha — Cisco loves this separation.

```
vsan database
vsan 1012 interface vfc1000
```

Now it’s truly part of the SAN fabric.

Verification (excellent to keep):

```
show vsan membership
```

**6. Make Sure VLAN 1000 Is Allowed on Ethernet1/9:**

Remember:

- Nexus 5K defaults Ethernet ports to *routed*

- Routed ports *drop VLAN traffic*

Fix it explicitly:

```
interface ethernet 1/9
switchport
switchport mode trunk
switchport trunk allowed vlan 1000
```

Verification:

```
show vlan id 1000
```

**7. Bring Interfaces Up (Order Matters!):**

First, vFC:

```
interface vfc1000
no shutdown
```

If you see:

```
errDisabled
```

That’s normal if Eth1/9 is still down. Fix it:

```
interface ethernet 1/9
no shutdown
```

Final verification:

```
show interface vfc1000
```

*Key fields to notice:*

- Port mode: TF

- VSAN: 1012

- Bound interface: Ethernet1/9

- Trunk vsans (up): 1012

**Final “State of the World” Sanity Map:**

```
[ UCS Server ]
      |
      |  (FCoE frames)
      |
[ Eth1/9 ]  VLAN 1000 (FCoE)
      |
      |  bind
      v
[ vfc1000 ]  (TF Port)
      |
      |  VSAN 1012
      |
[ SAN Fabric ]
      |
[ MDS / Storage ]
```

Everything lines up:

- Ethernet → VLAN → FCoE

- vFC → VSAN → FC Fabric

- TF ↔ TN trunking in place

- No illegal port-type pairings

**TL;DR (Cookbook Summary):**

- VLAN = FCoE carrier

- VSAN = SAN fabric

- vfc = FC personality for Ethernet

- bind = mandatory

- allowed VSAN ≠ VSAN membership

- TF/TN = FCoE equivalent of F/N

- Bring up Ethernet before vFC

This lab is now concluded.
