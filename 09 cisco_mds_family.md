# Describing the Cisco MDS Family

*In this course, you will learn about the Cisco Multilayer Director Switch (MDS) family of Fibre Channel switches.*

*This list includes the Cisco MDS 9700 Series, Cisco MDS 9700 Line Cards, Cisco MDS 9200 Multiservice Switches, Cisco 9300 Series Multilayer Fabric Switches, and Cisco MDS 9100 Series Multilayer Fabric Switches.*

## Cisco MDS Overview

*Every day, the amount of data that end hosts and servers process passes onto the wire, and storage and back-up in the storage array increases multifold. Such growth requires high-performance storage arrays and storage networking switches with key characteristics such as reliability, stability, high availability, and flexibility for future scale requirements.*

*In this topic, you will learn features in Cisco Multilayer Director Switch (Cisco MDS) 9000 Series Multilayer Switches that address SAN requirements. Cisco MDS 9000 Series Multilayer Switches combine a robust, flexible hardware architecture with multiple layers of network and storage-management intelligence.*

*You can use Cisco MDS 9000 Series Multilayer Switches to build highly available and scalable storage networks with unified management and built-in automation:*

- ***Scale for large fabric:*** *Cisco MDS 9000 Series Multilayer Switches provide up to 768 line-rate 64-Gbps Fibre Channel ports delivering both scale and performance with fully populated Cisco MDS 9718 switches. Up to 4000 FLOGI and 16000 Zones per switch are supported.*

- ***Long-distance native Fibre Channel links:*** *Available with 16000 or 8000 credits per port.*

- ***Multiprotocol support:***

1. *2, 4, 8, 16, 32, and 64-Gbps Fibre Channel*

2. *Non-Volatile Memory Express (NVMe) over Fibre Channel*

3. *IBM Fibre Connection (FICON)*

4. *1, 10, 25, and 40 Gbps Ethernet for Fibre Channel over IP (FCIP)*

- ***Deep visibility:*** *Built-in hardware-based analytics enables faster troubleshooting and resolution. Cisco SAN Analytics provides visibility into Fibre Channel block storage traffic by inspecting frames natively on Fibre Channel switches without any external taps, probes, or appliances.*

*The overall architecture can be logically divided into three components: traffic inspection, traffic processing, and streaming of flow metrics to an external analytics and visualization engine. Traffic inspection is integrated with the latest generation Fibre Channel port application-specific integrated circuits (ASICs) that are available on Cisco MDS 9000 32 and 64 Gbps switches.*

*Flow metric calculation is performed on the switch itself with the help of an onboard Network Processing Unit (NPU). Cisco MDS 9000 switches stream the flow metrics to an external receiver in industry-leading open formats. An external receiver can bring the fabric-wide and end-to-end visibility into a single pane of glass.*

- ***Dynamic Ingress Rate Limiting:*** *Dynamic Ingress Rate Limiting (DIRL) bridges the performance gaps between the newer ultra-fast All-Flash Arrays (AFAs) for NVMe storage and slower application servers. DIRL prevents the spreading of congestion that is caused by performance issues or slow-drain conditions in a SAN.*

- ***Diagnostics and troubleshooting tools:***

1. ***Port-Monitor:*** *Cisco Port-Monitor (PMON) provides automatic alerting on congestion and other events at 1-second granularity.*

2. ***Slow-drain detection:*** *The Cisco MDS 9000 family of switches have software-based slow-drain detection features to constantly monitor the network for symptoms of slow-drain events and send alerts or take automatic recovery actions. In addition, these switches provide hardware-enhanced slow-drain features, which are a direct benefit of the advanced capabilities of the port ASIC.*

- ***Unified management:*** *The comprehensive management platform Cisco Nexus Dashboard SAN Controller (NDSC) provides management, automation, control, monitoring, and integration for SAN deployments.*

- ***Automation:*** *Improved agility and reduced errors with Ansible modules for Fibre Channel ports and the Cisco MDS Python software development kit (SDK).*

## Cisco MDS 9700 Series Multilayer Directors

*The Cisco MDS 9700 multilayer director-class switches meet the critical requirements of large, virtualized data center storage environments. Some requirements include high availability, performance, reliability, and resiliency. The Cisco MDS 9700 directors provide line-rate non-oversubscribed 64-Gbps Fibre Channel throughput with up to 3 Tbps of bidirectional front-panel bandwidth per slot.*

![MDS 9700 Series](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/MDS_9700_series.png)

![MDS 9700 Series Overview](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/MDS_9700_series2.png)

*The Cisco MDS 9700 family of directors includes these platforms:*

- *Cisco MDS 9718 is an 18-slot chassis with 16 line card slots and up to 16 power supplies.*

- *Cisco MDS 9710 is a 10-slot chassis with eight line card slots and up to eight power supplies.*

- *Cisco MDS 9706 is a 6-slot chassis with four line card slots and up to four power supplies.*

*All Cisco MDS 9700 Series switches offer two supervisor slots, six crossbar switching fabric slots, and three fan trays.*

*Each crossbar fabric module Fabric-3 provides the equivalent of 512 Gbps of Fibre Channel front-panel bandwidth to each line card. Six Fabric-3 Cards provide 3072 Gbps that is enough to support 64-Gbps line cards.*

*The Cisco MDS 9700 Multilayer Directors provide grid redundancy on power supply and support the following types of power supplies:*

- *3000W AC power supply (AC input and DC output)*

- *3000W DC power supply (DC input and DC output)*

*Depending on the chassis, you have several redundancy options for power supply units:*

- *The Cisco MDS 9718 Multilayer Director supports up to 16 hot-swappable power supplies. To power a fully populated chassis, you need only six power supply units. For grid redundancy, use 12 PSUs. For even better redundancy (N+2:N+2), place all 16 power supplies in the chassis.*

- *The Cisco MDS 9710 Multilayer Director supports up to eight hot-swappable power supplies. For a fully populated chassis, you need only three power supplies. For grid redundancy, use six PSUs. For additional redundancy (N+1:N+1), place all eight power supply units in the chassis.*

- *The Cisco MDS 9706 Multilayer Director supports up to four hot-swappable power supplies. A fully populated system requires two power supplies. Grid redundancy requires all four PSUs.*

## Cisco MDS 9700 Line Cards

*Cisco MDS 9700 line cards support the Fibre Channel and FCIP protocols.*

![Cisco MDS 9700 Line Cards](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/MDS_9700_line_cards.png)

*The Cisco MDS 48-port 64G Fibre Channel module has 48 native Fibre Channel ports that support speeds of 8, 16, 32, and 64 Gbps at line-rate. It is based on a new and advanced dual F64 ASIC, supporting 24 front-panel ports, so the switches ports are divided into two port groups.*

*The Arbiter and the crossbar are integrated in the F64 ASICs. Each port supports 1000 buffer credits for exceptional extensibility without the need for additional licenses. With the Cisco MDS 9000 Family Enterprise Package, you can allocate up to 16,000 buffer credits to an individual port.*

*The onboard Network Processing Unit (NPU) in the module allows I/O-level metrics to be computed at every switch. To achieve line-rate operation for the 64-Gbps modules, the Cisco MDS 9700 Director must be fully populated with six Fabric-3 modules. At the same time, the 64-Gbps module can exist in the same chassis with the 16-Gbps and 32-Gbps modules.*

*The Cisco MDS 9700 48-Port 32-Gbps Fibre Channel switching module has 48 Fibre Channel ports, which support speeds of 4, 8, 16, and 32 Gbps at line-rate. Each port supports 500 buffer credits for exceptional extensibility without the need for additional licenses. With the Cisco Enterprise Package license, you can allocate up to 8191 buffer credits to an individual port. The onboard NPU in the module allows I/O-level metrics to be computed at every switch.*

*The Cisco MDS 9000 24- and 10-Port SAN Extension Module provides a high-performance, flexible, unified platform for deploying enterprise-class disaster-recovery and business-continuance SAN extension solutions. The Cisco MDS 9000 24- and 10-Port SAN Extension Module is a special-purpose line card for Cisco MDS 9700 Series Multilayer Directors.*

*This module enables large and scalable deployment of SAN extension solutions:*

- 24 line-rate 2-, 4-, 8-, 10-, and 16-Gbps Fibre Channel ports

- Eight 1- and 10-Gigabit Ethernet ports

- Two 40 Gigabit Ethernet port Fibre Channel over IP (FCIP) ports

*The FCIP module delivers outstanding SAN extension performance, reducing latency for disk and tape operations with FCIP acceleration features, including FCIP Write Acceleration and FCIP tape write and read acceleration.*

*Hardware-based encryption helps secure sensitive traffic with IP Security (IPsec), and hardware-based compression dramatically enhances performance for both high- and low-speed links, enabling immediate cost savings in expensive WAN infrastructure. You can group multiple FCIP interfaces within a single engine or across service engines into a port channel of up to 16 links for high availability and increased aggregate throughput.*

## Cisco MDS 9200 Series Multiservice Switch

*Cisco MDS 9220i Multiservice Fabric Switch is an optimized platform for deploying high-performance SAN-extension solutions, distributed intelligent fabric services, and cost-effective multiprotocol connectivity for both open systems and mainframe environments.*

![Cisco MDS 9200 Series](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/MDS_9200_series.png)

*The Cisco MDS 9220i multiservice and multiprotocol switch provides 12 native Fibre Channel ports, which can operate at speeds of 4, 8, 16 and 32 Gbps. Four Ethernet ports support 1 and 10 Gbps. Also, the fourth of these ports and a fifth one can operate at 25 Gbps.*

*When you want to use the two 25 Gbps ports, you must shut down the first three Ethernet 1- and 10-Gbps ports. You also must shut down the sixth Ethernet port, which operates at 40 Gbps. When you want to use the one 40-Gbps Ethernet port, the rest of the Ethernet ports must be down.*

*The switch supports the Fibre Channel Protocol (FCP), the Fibre Channel over IP protocol (FCIP) and the FICON protocol for mainframe connectivity. The Cisco MDS 9220i is a 1 rack unit (1RU) switch. It has two redundant 500W power supply units (PSUs) and up to four redundant, hot-swappable fan modules with reversible air flow.*

## Cisco MDS 9300 Series Multilayer Fabric Switches

*The Cisco MDS 9300 Series Multilayer Fabric Switches are 96-port compact 2RU devices.*

![Cisco MDS 9300 Series](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/MDS_9300_series.png)

*The Cisco MDS 9396T switch comes with 48 enabled ports at 4-, 8-, 16-, and 32-Gbps Fibre Channel speeds, with up to 48 additional ports available with expansion licenses. Also, the Cisco MDS 9396T switch offers state-of-the-art analytics and telemetry capabilities that are built into its next-generation ASIC platform.*

*Cisco MDS 9396V 64-Gbps 96-Port Fibre Channel switch has 96 8-, 16-, 32-, and 64-Gbps non-oversubscribed line-rate ports. The switch also supports SAN Analytics and telemetry.*

## Cisco MDS 9100 Series Multilayer Fabric Switches

*The Cisco MDS 9100 Series are built for small- and medium-scale SANs and data-center edge applications.*

![Cisco MDS 9100 Series](https://raw.githubusercontent.com/PurityControl7/DCFNDU/refs/heads/root/images/MDS_9100_series.png)

*The Cisco MDS 9132T is a 32-Gbps Fibre Channel switch that uses a next-generation 32-Gbps line-rate ASIC with built-in telemetry capability. The Cisco MDS 9132T Switch has a semimodular architecture with an expansion module. It supports both entry-level and enterprise-class SAN deployments using 4-, 8-, 16-, and 32-Gbps Fibre Channel server connectivity. This switch provides analytics and telemetry capabilities that are built into its next-generation ASIC platform.*

*The Cisco MDS 9148T platform provides 48 32-Gbps Fibre Channel line-rate ports. Also, Cisco MDS 9148T Switch offers analytics and telemetry capabilities that are built into its next-generation ASIC platform.*

*The next-generation Cisco MDS 9124V is a 64-Gbps 24-Port Fibre Channel Switch.*

*The next-generation Cisco MDS 9148V is a 64-Gbps 48-Port Fibre Channel Switch.*

*The Cisco MDS 9124V and Cisco MDS 9148V switches provide high-speed Fibre Channel connectivity for all-flash arrays and high-performance hosts.*

*The Cisco MDS 9124V and Cisco MDS 9148V switches offer analytics and telemetry capabilities that are built into its next-generation ASIC chipset. These switches allow seamless transition to Fibre Channel Non-Volatile Memory Express (NVMe over Fibre Channel) workloads whenever available without any hardware upgrade in the SAN.*
