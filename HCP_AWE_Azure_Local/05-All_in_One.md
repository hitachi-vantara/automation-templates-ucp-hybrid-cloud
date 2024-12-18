# Advancing File Services for the Hybrid Cloud Era: A Technical Guide to HCP Anywhere Enterprise, HCP for Cloud Scale, and UCP for Azure Local Integration

## Content Table

-   [01-Introduction](.\01-Introduction.md)
-   [02-Technical_Deep_Dive](.\02-Technical_Deep_Dive.md)
-   [03-Deployment](.\03-Deployment.md)
-   [04-Conclusion](.\04-Conclusion.md)
-   [05-All_in_One](.\05-All_in_One.md)   <----This doc




## Introduction 

In today's dynamic and data-driven business landscape, organizations are
increasingly adopting cloud and hybrid cloud strategies to enhance
agility, scalability, and cost-efficiency. As these IT environments
become more complex and distributed, the need for robust and intelligent
file sharing solutions has never been more critical. Advanced file
sharing solutions play a pivotal role in enabling seamless
collaboration, ensuring data accessibility, and maintaining the security
and integrity of corporate data across diverse platforms and locations.

The integration of HCP Anywhere Enterprise, HCP for Cloud Scale, and UCP
for Azure Local (previously known as Azure Stack HCI) is a powerful and
sophisticated file sharing solution that effectively addresses the
challenges faced by modern organizations. This integration provides
flexibility in both data placement and transportation, allowing
customers to choose from various scenarios based on their compliance
requirements and data usage patterns.

Customers can choose from various data placement and transportation
scenarios, depending on their specific requirements:

-   **On premises (purely off-cloud) approach**:

    -   Use Azure mainly as a global control plane for Azure Local
        clusters

    -   Ensure that data never traverses Hyperscalers' backbone networks

    -   Keep all data on-premises for strict compliance and data
        sovereignty

-   **Hybrid model**:

    -   Keep some data on-premises and some in the cloud

    -   Decide data placement based on specific compliance requirements
        and data usage patterns

    -   Maintain flexibility in data placement and transportation

-   **Cloud-first strategy**:

    -   Store all data in the cloud for maximum scalability and
        cost-efficiency

    -   Alternatively, keep most data in the cloud with a small portion
        on-premises

    -   Leverage cloud resources while maintaining some on-premises
        presence for specific requirements

Moreover, this integrated solution comes with various deployment
methods, making it easy for organizations to implement and manage their
file sharing infrastructure. One notable deployment method is **the use
of Azure Resource Manager (ARM) templates.** ARM templates enable
organizations to define their infrastructure as code, allowing for
consistent, repeatable, and auditable deployments across different
environments. By leveraging ARM templates, organizations can quickly
provision and configure the necessary components, such as the HCP
Anywhere Enterprise Portal, Edge Filers, and storage resources, in a
streamlined, automated, and manageable manner.

The ease of deployment extends to other methods as well, such as using
PowerShell scripts or the Azure portal for provisioning and management.
These diverse deployment options provide organizations with the
flexibility to choose the method that best aligns with their existing
processes and skill sets, ensuring a smooth and efficient implementation
of the integrated solution.

The following sections provide brief introductions to the respective
core components of this integrated solution.

**UCP for Azure Local** is a powerful hybrid cloud solution that
combines the flexibility and scalability of Azure with the control and
performance of on-premises infrastructure. It leverages Microsoft's
proven virtualization, storage, and networking technologies, such as
Hyper-V, Storage Spaces Direct (S2D), and Software-Defined Networking
(SDN), to deliver a highly resilient and efficient platform for running
virtualized workloads. It also works seamlessly with **Hitachi VSP One
File**, flexibilizing edge-core-cloud data integrations.

**HCP Anywhere Enterprise**, on the other hand, is a leading
enterprise-grade file sharing and data management solution that enables
organizations to securely store, sync, and share files across edge,
core, and cloud environments. HCP Anywhere Enterprise's platform
comprises two key components:

-   **HCP Anywhere Enterprise Portal**:

    -   Central management and control plane for the entire ecosystem

    -   Unified interface for configuration, monitoring, and management

    -   Communicates with Edge Filers for secure data access and
        synchronization

-   **HCP Anywhere Enterprise Edge Filer**:

    -   Deployed at remote locations for local file access and caching

    -   Interfaces with the Portal for configuration and management

    -   Synchronizes data with the central repository

    -   Ensures low-latency file access and sharing at remote locations

Together, the HCP Anywhere Enterprise Portal and Edge Filer provide a
comprehensive and unified approach to file services, data protection,
and collaboration, enabling organizations to securely store, sync, and
share files across edge, core, and cloud environments.

**HCP for Cloud Scale** is a software-defined object storage solution
from Hitachi Vantara that is built on a microservices architecture and
provides massive scalability, high performance, and S3 compatibility.
Key features include:

-   Scales out to support hundreds of nodes and billions of objects

-   Can be deployed on Hitachi or third-party servers, or in public
    cloud environments

-   Efficiently manages metadata separately from object data for
    scalability

-   Provides built-in data security, protection and advanced
    metadata-based data management

-   Enables hybrid cloud workflows and integration with cloud services

-   Offers S3 API compatibility along with valuable extensions

-   Includes an intelligent policy engine for automating data management
    tasks at scale

By integrating HCP Anywhere Enterprise and HCP for Cloud Scale with UCP
for Azure Local, organizations can unlock a host of strategic
advantages. This powerful combination allows businesses to:

-   **Enhance file sharing capabilities** across edge, core, and cloud
    environments, ensuring seamless access to data regardless of
    location with flexible data placement and transportation options
    based on compliance requirements and data usage patterns

-   **Improve data protection and business continuity** by leveraging
    HCP Anywhere Enterprise's advanced backup and disaster recovery
    features.

-   **Simplify management and reduce complexity** by consolidating file
    services and virtualization on a single, unified platform

-   **Achieve greater cost-efficiency** by optimizing storage resources
    and minimizing data transfer costs. Ensure compliance with industry
    regulations and data sovereignty requirements through flexible
    deployment options and granular control over versatile data
    placement

The integration of HCP Anywhere Enterprise and HCP for Cloud Scale with
Azure Local empowers organizations to build a future-ready IT
infrastructure that can adapt to evolving business needs, support
distributed workflows, and drive innovation in the era of hybrid cloud
computing.

## HCP Anywhere Enterprise, HCP for Cloud Scale, and Azure Local: A Technical Deep Dive

In this section, we'll dive into the technical aspects of integrating
HCP Anywhere Enterprise, HCP for Cloud Scale, and Azure Local. We'll
examine the architecture and key components of each technology and
explore how they work together to deliver a seamless, secure, and
scalable file sharing solution across edge, core, cloud, and hybrid
environments.

### HCP Anywhere Enterprise's File Sharing Capabilities

HCP Anywhere Enterprise's software-defined platform offers a suite of
components designed to establish a highly flexible and scalable
distributed file system, catering to the diverse requirements of modern
file sharing and collaboration in cloud and hybrid cloud environments.

#### HCP Anywhere Enterprise Portal

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr>
<th style="text-align: center;"><p><img
src=".\attachments\/media/image1.png"
style="width:6.4in;height:2.5in" /></p>
<p>Fig. High Level Diagram of Portal / Edge Filer interaction</p></th>
</tr>
</thead>
<tbody>
</tbody>
</table>

The HCP Anywhere Enterprise (AWE) Portal serves as the central
management and orchestration platform for HCP Anywhere Enterprise's file
sharing solution. It provides a web-based interface for administrators
to configure, monitor, and control the entire HCP Anywhere Enterprise
ecosystem. Key features of the HCP Anywhere Enterprise Portal include:

-   Centralized management of Edge Filers, users, and policies

-   Real-time monitoring and reporting of system health and performance

-   Integration with various storage providers, such as Azure, AWS, and
    Google Cloud, as well as **HCP for Cloud Scale**, enabling flexible
    hybrid multi-cloud strategies

-   Built-in data protection features, including backup, versioning, and
    disaster recovery for enhancing business continuity

-   Smart syncing with HCP Anywhere Enterprise Edge Filers, improving
    file caching and accessibility of each Edge Filer, saving storage
    and lowering network costs efficiently

-   Flexible data access for Edge Filers:

    -   Edge Filers can access files in storage through the Portal

    -   Alternatively, Edge Filers can access files directly from
        S3-compatible and blob storage destinations if direct mode is
        configured

##### Port Tables for HCP Anywhere Enterprise Portal

###### Inbound Ports

<table>
<colgroup>
<col style="width: 8%" />
<col style="width: 13%" />
<col style="width: 77%" />
</colgroup>
<thead>
<tr>
<th><strong>Port</strong></th>
<th><strong>Protocol</strong></th>
<th><strong>Notes</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>22</td>
<td>TCP</td>
<td>SSH. HCP recommends limiting SSH access to specific IP addresses
that may require access to the HCP application servers, for example to
perform scheduled maintenance and support related work.</td>
</tr>
<tr>
<td>53</td>
<td>UDP</td>
<td>DNS resolution server (If portal internal DNS server is registered
in DNS)</td>
</tr>
<tr>
<td>80</td>
<td>TCP</td>
<td>HTTP (redirects to port 443)</td>
</tr>
<tr>
<td>443</td>
<td>TCP</td>
<td>HTTPS</td>
</tr>
<tr>
<td>995</td>
<td>TCP</td>
<td>CTTP protocol communications with HCP Edge Filers and agents.</td>
</tr>
<tr>
<td>8443</td>
<td>TCP</td>
<td>Communications with HCP AWE Edge Filers for log collection</td>
</tr>
</tbody>
</table>

###### Outbound Ports

<table>
<colgroup>
<col style="width: 8%" />
<col style="width: 14%" />
<col style="width: 76%" />
</colgroup>
<thead>
<tr>
<th><strong>Port</strong></th>
<th><strong>Protocol</strong></th>
<th><strong>Notes</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>25</td>
<td>TCP</td>
<td>Default SMTP port. This port can be configured on the SMTP server
and specified in the portal Web interface</td>
</tr>
<tr>
<td>80</td>
<td>TCP</td>
<td>HTTP</td>
</tr>
<tr>
<td>88</td>
<td>TCP &amp; UDP</td>
<td>If Kerberos is used</td>
</tr>
<tr>
<td>111</td>
<td>TCP</td>
<td>NFS, only required if NFS version 3 storage is used</td>
</tr>
<tr>
<td>123</td>
<td>UDP</td>
<td>NTP (Network Time Protocol)</td>
</tr>
<tr>
<td>389</td>
<td>TCP &amp; UDP</td>
<td>LDAP/LDAP GC (Global Catalog)</td>
</tr>
<tr>
<td>443</td>
<td>TCP</td>
<td>HTTPS</td>
</tr>
<tr>
<td>514</td>
<td>UDP</td>
<td>Default Syslog port. This port can be configured on the Syslog
server</td>
</tr>
<tr>
<td>636</td>
<td>TCP</td>
<td>LDAP and LDAP GC with TLS (HCP recommends using LDAPS and LDAPS GC
instead of LDAP and LDAP GC)</td>
</tr>
<tr>
<td>1344</td>
<td>TCP</td>
<td>If using an antivirus server</td>
</tr>
<tr>
<td>2049</td>
<td>TCP</td>
<td>NFS, only required if NFS version 4.x storage is used</td>
</tr>
<tr>
<td>3128</td>
<td>TCP</td>
<td>Default Proxy server port, only required if a proxy server is
defined in the global administration, where a different port can be
configured</td>
</tr>
<tr>
<td>3268</td>
<td>TCP &amp; UDP</td>
<td>LDAP/LDAP GC (Global Catalog)</td>
</tr>
<tr>
<td>3269</td>
<td>TCP</td>
<td>LDAPS and LDAPS GC (HCP recommends using LDAPS and LDAPS GC instead
of LDAP and LDAP GC)</td>
</tr>
<tr>
<td>5671</td>
<td>TCP</td>
<td>Only required when using the Varonis service. This port can be
configured in Varonis Data Security Platform</td>
</tr>
<tr>
<td>5696</td>
<td>TCP</td>
<td>Only required when using the Key Management service to connect to
the Key Management Interoperability Protocol (KMIP) server</td>
</tr>
<tr>
<td>6514</td>
<td>TDP</td>
<td>Default Syslog port over TCP/TLS, can be configured on the Syslog
server</td>
</tr>
</tbody>
</table>

#### HCP Anywhere Enterprise Edge Filer

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr>
<th style="text-align: center;"><p><img
src=".\attachments\/media/image2.png"
style="width:6.3in;height:1.63717in" /></p>
<p>Fig. Edge Filer interactions</p></th>
</tr>
</thead>
<tbody>
</tbody>
</table>

The HCP Anywhere Enterprise Edge Filer is a core component of HCP
Anywhere Enterprise's file sharing solution, designed to provide local
file services and caching at ROBO (remote offices and branch offices)
and edge locations. It offers a wide range of features, including:

-   Local file access and sharing using standard protocols like SMB and
    NFS

-   Intelligent caching of frequently accessed files to optimize
    performance

-   Integration with Active Directory and LDAP for user authentication
    and access control

-   Automated backup and synchronization with the HCP Anywhere
    Enterprise Portal

-   “Direct mode” allowing up to 10x faster transfer speeds compared to
    non-Direct Mode

##### Direct Mode Explained

HCP Anywhere Enterprise's Direct Mode enables data to be uploaded and
downloaded directly between Edge Filers and S3-compatible storage nodes,
such as, **HCP for Cloud Scale**, bypassing the HCP Anywhere Enterprise
Portal.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr>
<th style="text-align: center;"><img
src=".\attachments\/media/image3.png"
style="width:6.3in;height:1.44864in"
alt="A screenshot of a computer Description automatically generated" /></th>
</tr>
</thead>
<tbody>
</tbody>
</table>

Direct Mode offers up to 10x faster transfer speeds compared to
non-Direct Mode, depending on factors like disk type, network latency,
and antivirus software on the portal. It reduces latency by chunking
data and transferring it in parallel, using up to 100 concurrent
connections per endpoint, with only **metadata** sent to the Portal.

Data is securely transmitted using HTTPS when Direct Mode is enabled.

Direct Mode is ideal for distributed data-intensive workloads, such as
media files, healthcare imaging, and video surveillance.

In addition to enhanced transfer speed, Direct Mode provides the
capability to balance data sovereignty while providing high performance.
Users can store only metadata in the Portal (regardless of whether the
Portal is installed on-premises or in Azure), **while keeping the actual
data contents stored where they should be, according to compliance and
regulatory requirements**. This separation of metadata and data allows
organizations to maintain control over their actual data placement while
benefiting from the performance advantages of Direct Mode.

##### Port Tables for HCP Anywhere Enterprise Edge Filer

**Port Requirements**

###### Firewall ports opened for LAN communication and managing the Edge Filer user interface:

<table>
<colgroup>
<col style="width: 12%" />
<col style="width: 21%" />
<col style="width: 22%" />
<col style="width: 43%" />
</colgroup>
<thead>
<tr>
<th><strong>Port</strong></th>
<th><strong>Protocol</strong></th>
<th><strong>Direction</strong></th>
<th><strong>Notes</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>443</td>
<td>TCP</td>
<td>Inbound</td>
<td>HTTPS. This port should be behind the firewall.</td>
</tr>
</tbody>
</table>

###### Firewall ports opened to the HCP Anywhere Enterprise Portal:

<table>
<colgroup>
<col style="width: 8%" />
<col style="width: 12%" />
<col style="width: 13%" />
<col style="width: 65%" />
</colgroup>
<thead>
<tr>
<th><strong>Port</strong></th>
<th><strong>Protocol</strong></th>
<th><strong>Direction</strong></th>
<th><strong>Notes</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>443</td>
<td>TCP</td>
<td>Outbound</td>
<td>HTTPS. This port should only be open to the specific HCP AWE Portal
IP addresses.</td>
</tr>
<tr>
<td>995</td>
<td>TCP</td>
<td>Outbound</td>
<td>CTTP. Communications with the HCP AWE Portal. For details about
CTTP</td>
</tr>
<tr>
<td>8443</td>
<td>TCP</td>
<td>Outbound</td>
<td>Communications with HCP AWE Portal for log collection.</td>
</tr>
</tbody>
</table>

###### Firewall ports opened to the HCP Anywhere Portal backend storage when Direct Mode is set for the storage node in the portal:

<table>
<colgroup>
<col style="width: 27%" />
<col style="width: 16%" />
<col style="width: 20%" />
<col style="width: 35%" />
</colgroup>
<thead>
<tr>
<th><strong>Port</strong></th>
<th><strong>Protocol</strong></th>
<th><strong>Direction</strong></th>
<th><strong>Notes</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>443</td>
<td>TCP</td>
<td>Outbound</td>
<td>HTTPS</td>
</tr>
</tbody>
</table>

When Direct Mode is used, the edge filer requires the certificate to
enable the TLS handshake with the object storage.

###### Firewall ports opened for Active Directory:

<table>
<colgroup>
<col style="width: 13%" />
<col style="width: 20%" />
<col style="width: 22%" />
<col style="width: 42%" />
</colgroup>
<thead>
<tr>
<th><strong>Port</strong></th>
<th><strong>Protocol</strong></th>
<th><strong>Direction</strong></th>
<th><strong>Notes</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>88</td>
<td>TCP/UDP</td>
<td>Outbound</td>
<td>If Kerberos is used</td>
</tr>
<tr>
<td>389</td>
<td>TCP/UDP</td>
<td>Outbound</td>
<td>LDAP protocol</td>
</tr>
<tr>
<td>445</td>
<td>TCP</td>
<td>Outbound</td>
<td>SMB when joining to a domain as a Computer account</td>
</tr>
<tr>
<td>3268</td>
<td>TCP/UDP</td>
<td>Outbound</td>
<td>LDAP GC (Global Catalog) protocol</td>
</tr>
</tbody>
</table>

###### Firewall ports opened for antivirus updates:

<table>
<colgroup>
<col style="width: 27%" />
<col style="width: 16%" />
<col style="width: 22%" />
<col style="width: 34%" />
</colgroup>
<thead>
<tr>
<th><strong>Port</strong></th>
<th><strong>Protocol</strong></th>
<th><strong>Direction</strong></th>
<th><strong>Notes</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>80</td>
<td>TCP</td>
<td>Outbound</td>
<td>HTTP</td>
</tr>
</tbody>
</table>

###### Firewall ports opened for SMTP:

<table>
<colgroup>
<col style="width: 8%" />
<col style="width: 13%" />
<col style="width: 14%" />
<col style="width: 63%" />
</colgroup>
<thead>
<tr>
<th><strong>Port</strong></th>
<th><strong>Protocol</strong></th>
<th><strong>Direction</strong></th>
<th><strong>Notes</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>25</td>
<td>TCP</td>
<td>Outbound</td>
<td>The port is configurable in the edge filer user interface (in
the <strong>Configuration</strong> view, select <strong>Alerts &gt; Mail
Server</strong> in the navigation pane).</td>
</tr>
</tbody>
</table>

###### Firewall ports opened for NTP updates:

<table>
<colgroup>
<col style="width: 26%" />
<col style="width: 17%" />
<col style="width: 21%" />
<col style="width: 34%" />
</colgroup>
<thead>
<tr>
<th><strong>Port</strong></th>
<th><strong>Protocol</strong></th>
<th><strong>Direction</strong></th>
<th><strong>Notes</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>123</td>
<td>UDP</td>
<td>Outbound</td>
<td>—</td>
</tr>
</tbody>
</table>

**Warning: HCP Anywhere Enterprise Edge Filers operate behind a
firewall, and it is important to leave all other ports closed.**

###### Internal network file sharing protocols (not requiring any port configuration):

<table>
<colgroup>
<col style="width: 26%" />
<col style="width: 17%" />
<col style="width: 25%" />
<col style="width: 30%" />
</colgroup>
<thead>
<tr>
<th><strong>Port</strong></th>
<th><strong>Protocol</strong></th>
<th><strong>Direction</strong></th>
<th><strong>Notes</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>111, 2049</td>
<td>TCP</td>
<td>Inbound</td>
<td>NFS</td>
</tr>
<tr>
<td>445</td>
<td>TCP</td>
<td>Inbound</td>
<td>SMB</td>
</tr>
</tbody>
</table>

###### Browser Requirements

The latest two releases of Google Chrome, Apple Safari, Mozilla Firefox,
and Microsoft Edge.

###### Software Features

<table>
<colgroup>
<col style="width: 44%" />
<col style="width: 55%" />
</colgroup>
<thead>
<tr>
<th><strong>Features</strong></th>
<th><strong>Feature Description</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>Supported File Sharing Protocols</td>
<td>SMB 2.x/3.x (Windows File Sharing), NFS, FTP, WebDAV</td>
</tr>
<tr>
<td>Monitoring</td>
<td>SNMP</td>
</tr>
</tbody>
</table>

###### Cloud Service Features

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 74%" />
</colgroup>
<thead>
<tr>
<th><strong>Features</strong></th>
<th><strong>Feature Description</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>Backup Files Security</td>
<td>AES-256 Encryption, optional secret passphrase, file vetoing.</td>
</tr>
<tr>
<td>Protocol Security</td>
<td>TLS (Transport Level Security).</td>
</tr>
<tr>
<td>Efficiency</td>
<td>Incremental updates, data compression, block level deduplication,
simultaneous synchronization.</td>
</tr>
<tr>
<td>Versioning</td>
<td>Retention of previous file versions.</td>
</tr>
<tr>
<td>Additional Services</td>
<td>Centralized management, centralized monitoring, Cloud Drive caching
and synchronization, reporting, logging, remote access.</td>
</tr>
</tbody>
</table>

### HCP for Cloud Scale's Scalable Object Storage Platform

HCP for Cloud Scale is a software-defined object storage solution that
leverages a microservices architecture to deliver massive scalability,
high performance, and S3 compatibility. Its technical architecture is
designed to meet the growing demands of cloud-native applications and
large-scale data storage and management.

#### Distributed Metadata Management

One of the key innovations in HCP for Cloud Scale is its separation of
metadata management from object data storage. The platform employs a
purpose-built, distributed metadata database that ensures high
performance and scalability. Key features of the metadata management
system include:

-   A patent-pending partitioning scheme that evenly distributes
    metadata across the cluster, ensuring efficient access and load
    balancing

-   Support for dynamic partitioning and partition balancing, allowing
    the system to adapt to changing workload requirements

-   An optimized metadata routing mechanism that efficiently locates
    metadata partitions in a constantly evolving cluster

-   A distributed in-memory cache for frequently accessed metadata,
    reducing I/O load on the database

#### Scalable Data Storage

HCP for Cloud Scale's data storage layer is designed to scale out
horizontally, leveraging a combination of Hitachi Content Platform (HCP)
S series storage nodes and S3-compatible storage endpoints. The platform
presents a unified global namespace, regardless of the number of
underlying storage components. Key features of the data storage layer
include:

-   Support for Hitachi's high-density HCP S series storage appliances,
    which offer up to 15 PB of disk capacity per rack

-   Compatibility with any S3-compliant storage endpoint, including
    public cloud storage services like AWS S3, Microsoft Azure Blob
    Storage, and Google Cloud Storage

-   A virtualized 4 KiB block system with erasure coding data
    protection, ensuring high durability and storage efficiency

-   Intelligent data placement and load balancing across storage
    components, optimizing performance and resource utilization

#### Policy-Driven Data Management

HCP for Cloud Scale includes a powerful policy engine that enables
automated data management at scale. The engine leverages the platform's
rich metadata capabilities to enforce data lifecycle, protection, and
security policies. Key features of the policy-driven data management
system include:

-   A flexible, event-driven architecture that allows policies to be
    triggered based on predefined events or schedules

-   Integration with public cloud services, such as AWS Lambda, for
    executing data processing workflows

-   Support for advanced data management tasks, such as data retention,
    disposition, replication, and event notification

-   A scalable job processing framework that distributes policy
    execution across the cluster, ensuring high performance and resource
    efficiency

#### Security and Data Protection

HCP for Cloud Scale incorporates a comprehensive set of security and
data protection features to ensure the confidentiality, integrity, and
availability of stored data. Key security features include:

-   Support for data-at-rest encryption (DARE) using a built-in key
    management system (KMS) that generates unique encryption keys for
    each object

-   Data-in-flight encryption (DIFE) using industry-standard TLS
    protocols

-   Integration with Active Directory (AD) and LDAP for user
    authentication and access control

-   Fine-grained, role-based access control (RBAC) with support for
    custom roles and permissions

-   Bucket-level access control lists (ACLs) for managing data sharing
    and collaboration

### UCP for Azure Local: Core Features

<img src=".\attachments\/media/image4.png"
style="width:6in;height:3.33503in" />

Fig.
<https://learn.microsoft.com/en-us/azure/azure-local/hybrid-capabilities-with-azure-services>

UCP for Azure Local is built upon foundational technologies from
Microsoft's software-defined datacenter stack and extends the hybrid
capabilities of Azure into your on-premises environment.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr>
<th style="text-align: center;"><p><img
src=".\attachments\/media/image5.png"
style="width:6in;height:2.82564in" /></p>
<p>Fig. <a
href="https://azurestackhcisolutions.azure.microsoft.com/#/catalog?Search=Hitachi+Advanced">https://azurestackhcisolutions.azure.microsoft.com/#/catalog?Search=Hitachi+Advanced</a></p></th>
</tr>
</thead>
<tbody>
</tbody>
</table>

#### Hyper-V for Virtualization

Azure Local leverages Microsoft's Hyper-V hypervisor to provide robust
and scalable virtualization capabilities. Hyper-V enables organizations
to:

-   Create and manage virtual machines (VMs) running various operating
    systems and workloads

-   Utilize advanced features like live migration, replication, and
    failover clustering for high availability

-   Integrate with Azure services, such as Azure Backup and Azure Site
    Recovery, for additional data protection and disaster recovery
    options

#### Storage Spaces Direct (S2D) for Storage

Storage Spaces Direct is a software-defined storage solution that
enables the creation of highly available and scalable storage pools
using local disks on Azure Local nodes. S2D provides:

-   Automatic data distribution and replication across nodes for fault
    tolerance

-   Support for various storage tiers, including all-flash and hybrid
    configurations

-   Integration with Azure Local's management tools for simplified
    storage provisioning and monitoring

#### Software-Defined Networking (SDN) for Networking

Azure Local incorporates Software-Defined Networking capabilities to
enable the creation and management of virtual networks. SDN in Azure
Local offers:

-   Centralized network configuration and control through the Azure
    Local management tools

-   Support for network virtualization and micro-segmentation using
    Virtual Networks (VNs) and Network Controller

-   Integration with Azure Network Adapter to connect virtual machines
    to Azure virtual networks

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr>
<th style="text-align: center;"><p><img
src=".\attachments\/media/image6.png"
style="width:6.30445in;height:2.1in" /></p>
<p>Fig. Summary - Core Features of Azure Local</p></th>
</tr>
</thead>
<tbody>
</tbody>
</table>

### Types of Files and their Typical Sizes

When considering the types of files and their typical sizes that the
integrated solution of Azure Local, HCP Anywhere Enterprise, and HCP for
Cloud Scale can help to share, it's essential to understand the diverse
needs of organizations across various industries. This solution is
designed to handle a wide range of file types and sizes, enabling
efficient collaboration and data management. Let's explore some common
file types and their typical sizes:

1.  **Office** **Documents**:

    -   File types: Microsoft Word (.docx), Excel (.xlsx), PowerPoint
        (.pptx), PDF (.pdf)

    -   Typical sizes: Few kilobytes (KB) to several megabytes (MB)

    -   Usage: Frequently shared and collaborated on by teams across
        various departments

2.  **Multimedia Files:**

    -   File types: Images (.jpg, .png, .tiff), Audio (.mp3, .wav),
        Video (.mp4, .avi, .mov)

    -   Typical sizes: Few megabytes (MB) to several gigabytes (GB)

    -   Usage: Marketing materials, training videos, product demos, and
        creative assets

3.  **CAD and Design Files:**

    -   File types: AutoCAD (.dwg), Revit (.rvt), 3D models (.obj, .3ds,
        .stl)

    -   Typical sizes: Few megabytes (MB) to several gigabytes (GB)

    -   Usage: Architects, engineers, and designers collaborating on
        complex projects

4.  **Scientific and Research Data:**

    -   File types: Large datasets (.csv, .hdf5, .nc), Genome sequences
        (.fasta, .fastq)

    -   Typical sizes: Gigabytes (GB) to terabytes (TB)

    -   Usage: Researchers, data scientists, and healthcare
        professionals analyzing large datasets

5.  **Software Development Files:**

    -   File types: Source code (.java, .py, .cpp), Repositories (.git),
        Dependencies and libraries

    -   Typical sizes: Kilobytes (KB) to several gigabytes (GB)

    -   Usage: Software developers collaborating on codebase and version
        control

6.  **Financial and Legal Documents:**

    -   File types: Contracts (.pdf), Financial reports (.xls, .csv),
        Legal briefs (.doc, .pdf)

    -   Typical sizes: Few kilobytes (KB) to several megabytes (MB)

    -   Usage: Financial institutions, legal firms, and compliance
        departments managing sensitive documents

7.  **High-Resolution Imagery and Geospatial Data:**

    -   File types: Satellite imagery (.tiff, .jp2), GIS data (.shp,
        .geojson), LiDAR point clouds (.las)

    -   Typical sizes: Gigabytes (GB) to terabytes (TB)

    -   Usage: Government agencies, energy companies, and environmental
        organizations analyzing geospatial data

The integration of Azure Local, HCP Anywhere Enterprise, and HCP for
Cloud Scale provides a flexible and scalable solution that can
accommodate this wide variety of file types and sizes. The solution
enables organizations to:

-   Efficiently share and collaborate on office documents and multimedia
    files across distributed teams

-   Manage and synchronize large CAD and design files between
    on-premises and cloud environments

-   Store and process massive scientific and research datasets using
    scalable object storage

-   Facilitate seamless collaboration on software development projects
    and version control

-   Securely share and manage sensitive financial and legal documents
    with fine-grained access control

-   Analyze and process high-resolution imagery and geospatial data
    using the scalability and performance of cloud storage

By leveraging the combined capabilities of Azure Local, HCP Anywhere
Enterprise, and HCP for Cloud Scale, organizations can effectively
share, manage, and collaborate on diverse file types and sizes,
unlocking productivity and innovation across various industries and use
cases.

### Integration Options

The integration of HCP Anywhere Enterprise, HCP for Cloud Scale, and UCP
for Azure Local creates a powerful, synergistic solution for enhanced
file sharing capabilities. Let's explore the high-level mechanism and
deployment options available.

#### High-Level Architecture - Components

The integration architecture consists of the following key components:

1.  **HCP Anywhere Enterprise Portal**: Hosted either on-premises on
    Azure Local or in Azure cloud, the Portal serves as the centralized
    management and orchestration platform for the entire HCP Anywhere
    Enterprise ecosystem.

2.  **HCP Anywhere Enterprise Edge Filers**: Deployed on Azure Local
    nodes as virtual machines, Edge Filers provide local file access,
    caching, and synchronization capabilities.

3.  **Storage Destinations**: The HCP Anywhere Enterprise Portal can
    write data to various storage destinations, including local
    filesystems, NFS storage, and object storage services such as Amazon
    S3, Azure Blob, Google Cloud Storage, and **<u>HCP for Cloud Scale
    instances</u>**.

4.  **HCP for Cloud Scale**: Instances of HCP for Cloud Scale can be
    deployed on Azure Local nodes or other chosen destinations,
    providing scalable and performant S3-compatible object storage.

#### Deployment Models and Options

Organizations can choose from several deployment models when integrating
HCP Anywhere Enterprise and HCP for Cloud Scale with Azure Local,
depending on their specific requirements and constraints. These
deployment models can be implemented using either the Default mode or
the Direct mode, each offering unique benefits and considerations.

##### On-Premises Deployment: 

-   **Default Mode**: In this model, both the HCP Anywhere Enterprise
    Portal and Edge Filers run on Azure Local nodes, with data stored
    locally on filesystems or HCP for Cloud Scale instances within the
    on-premises environment. Data is transferred through the Portal,
    providing centralized management, control, and simplification of the
    infrastructure, albeit with potential performance trade-offs.
    
    <img src=".\attachments\/media/image7.png"
    style="width:5.4in;height:1.25068in" />

    1.  Portal: Installed on Azure Local nodes on-premises

    2.  Edge Filers: Installed on Azure Local nodes on-premises

    3.  Data Path: Data is transferred through the Portal, which manages
        the storage on filesystems or HCP for Cloud Scale instances
        within the on-premises environment

    4.  Use Cases/Scenarios:

        -   Organizations with strict data sovereignty requirements that
            mandate all data remain on-premises

        -   Industries with tight regulatory compliance, such as
            healthcare or finance, where data must be kept within
            specific geographic boundaries

        -   Environments with limited or unreliable internet
            connectivity, where cloud-based solutions are not feasible

-   **Direct Mode**: With Direct Mode enabled, the HCP Anywhere
    Enterprise Portal and Edge Filers run on Azure Local nodes, with
    metadata stored in the Portal and data stored directly on HCP for
    Cloud Scale instances or other S3-compatible storage within the
    on-premises environment. This option ensures that data never leaves
    the on-premises infrastructure while benefiting from the performance
    advantages of Direct Mode. However, it requires additional network
    configurations and management for Edge Filers to access storage
    directly. 
    <img src=".\attachments\/media/image8.png"
    style="width:5.4in;height:1.60381in" />

    1.  Portal: Installed on Azure Local nodes on-premises, storing only
        metadata

    2.  Edge Filers: Installed on Azure Local nodes on-premises

    3.  Data Path: Data is stored directly on HCP for Cloud Scale
        instances or other S3-compatible storage within the on-premises
        environment, bypassing the Portal

    4.  Use Cases/Scenarios:

        -   Organizations with high-performance requirements for
            on-premises data access and transfer

        -   Environments with large datasets or data-intensive
            workloads, such as media and entertainment or scientific
            research

        -   Scenarios where minimizing latency between Edge Filers and
            storage is crucial for optimal user experience

##### Hybrid Deployment: 

-   **Default Mode**: The HCP Anywhere Enterprise Portal and Edge Filers
    are deployed on Azure Local nodes, while data is stored in a
    combination of on-premises and cloud storage destinations, such as
    Azure Blob, HCP for Cloud Scale instances, or other locations chosen
    by the end-users. Data is transferred through the Portal, providing
    centralized management and simplification, but with potential
    performance trade-offs.
    
    <img src=".\attachments\/media/image9.png"
    style="width:5.4in;height:1.25068in" />

    1.  Portal: Installed on Azure Local nodes on-premises

    2.  Edge Filers: Installed on Azure Local nodes on-premises

    3.  Data Path: Data is transferred through the Portal, which manages
        the storage on a combination of on-premises (filesystems or HCP
        for Cloud Scale instances) and cloud storage destinations (Azure
        Blob, HCP for Cloud Scale instances, or other locations)

    4.  Use Cases/Scenarios:

        -   Organizations transitioning from fully on-premises to hybrid
            cloud environments

        -   Scenarios where some data must remain on-premises due to
            compliance or privacy concerns, while other data can be
            stored in the cloud for scalability and cost-efficiency

        -   Environments with varying performance requirements, where
            some workloads can tolerate the latency of cloud storage
            while others require local storage for faster access

-   **Direct Mode**: With Direct Mode enabled, the HCP Anywhere
    Enterprise Portal can be deployed either on-premises on Azure Local
    nodes or in the cloud, storing only metadata. Edge Filers are
    deployed on Azure Local nodes, and data is stored directly on a
    combination of on-premises and cloud storage destinations, such as
    Azure Blob, HCP for Cloud Scale instances, or other S3-compatible
    locations chosen by the end-users. This model offers flexibility,
    allows organizations to leverage both on-premises and cloud
    resources, and benefits from the performance enhancements of Direct
    Mode. However, it requires additional network configurations and
    management for Edge Filers to access storage directly.
    
    <img src=".\attachments\/media/image10.png"
    style="width:5.4in;height:1.60381in" />

    1.  Portal: Can be installed either on Azure Local nodes on-premises
        or in the cloud, storing only metadata

    2.  Edge Filers: Installed on Azure Local nodes on-premises

    3.  Data Path: Data is stored directly on a combination of
        on-premises (HCP for Cloud Scale instances or other
        S3-compatible storage) and cloud storage destinations (Azure
        Blob, HCP for Cloud Scale instances, or other S3-compatible
        locations), bypassing the Portal

    4.  Use Cases/Scenarios:

        -   Organizations with distributed workforces and multiple
            branch offices requiring fast local access to data while
            leveraging cloud storage for scalability and cost-efficiency

        -   Environments with a mix of high-performance workloads and
            less latency-sensitive data, where Direct Mode can be
            selectively enabled for specific Edge Filers or datasets

        -   Scenarios where the Portal must be hosted in the cloud for
            easier management and maintenance while ensuring data can be
            stored in the most appropriate location

##### Cloud-First Deployment: 

-   **Default Mode**: In this scenario, the HCP Anywhere Enterprise
    Portal is hosted in Azure, while Edge Filers run on Azure Local
    nodes. Data is primarily stored in Azure, with the option to
    integrate HCP for Cloud Scale instances. Data is transferred through
    the Portal, providing centralized management and control, but with
    potential performance trade-offs.
    
    <img src=".\attachments\/media/image11.png"
    style="width:5.4in;height:1.25068in" />

    1.  Portal: Hosted in Azure

    2.  Edge Filers: Installed on Azure Local nodes on-premises

    3.  Data Path: Data is transferred through the Portal, which manages
        the storage primarily in Azure, with the option to integrate HCP
        for Cloud Scale instances

    4.  Use Cases/Scenarios:

        -   Organizations adopting a cloud-first strategy to maximize
            the use of cloud services and benefits

        -   Scenarios where most data can be stored in the cloud for
            scalability, cost-efficiency, and easy access from anywhere

        -   Environments with limited on-premises infrastructure or IT
            resources, where managing storage in the cloud is preferred

-   **Direct Mode**: With Direct Mode enabled, the HCP Anywhere
    Enterprise Portal is hosted in Azure, storing only metadata, while
    Edge Filers run on Azure Local nodes. Data is primarily stored
    directly in Azure Blob storage or HCP for Cloud Scale instances,
    optimizing cloud ingress/egress costs, and benefiting from the
    performance improvements of Direct Mode. However, it requires
    additional network configurations and management for Edge Filers to
    access storage directly.
    
    <img src=".\attachments\/media/image12.png"
    style="width:5.4in;height:1.63324in" />

    1.  Portal: Hosted in Azure, storing only metadata

    2.  Edge Filers: Installed on Azure Local nodes on-premises

    3.  Data Path: Data is stored directly in Azure Blob storage, or HCP
        for Cloud Scale instances on premises, bypassing the Portal

    4.  Use Cases/Scenarios:

        -   Organizations with high-performance requirements for
            cloud-based data access and transfer

        -   Environments with large datasets or data-intensive workloads
            that can benefit from the scalability and elasticity of
            cloud storage

        -   Scenarios where minimizing data transfer costs between
            on-premises Edge Filers and cloud storage is a priority, as
            Direct Mode reduces the need for data to traverse through
            the Portal

The choice of deployment model and mode depends on various factors,
including data sovereignty requirements, latency considerations,
performance needs, simplification of infrastructure management, and the
desired level of integration with Azure services. Default mode offers
simplification and centralized management, while Direct mode provides
performance benefits at the cost of additional network configurations
and management. By offering multiple deployment options and modes, the
integration of HCP Anywhere Enterprise, HCP for Cloud Scale, and Azure
Local provides organizations with the flexibility to tailor the solution
to their specific needs and constraints, ensuring a seamless and
efficient file sharing experience across on-premises and cloud
environments.

## Deployment of HCP Anywhere Enterprise with HCP for Cloud Scale

This section provides concise guides on deploying HCP Anywhere
Enterprise Portal and Edge Filers, along with considerations for
networking and integrating HCP for Cloud Scale. By following these
steps, you can ensure a smooth and successful installation of the HCP
Anywhere Enterprise solution.

### Prerequisites

Before beginning the deployment process, ensure that you have the
following:

1.  Access to the Azure portal and an active Azure subscription

2.  Access to an Azure Local environment (if deploying on Azure Local)

3.  Appropriate permissions to create and manage resources in your Azure
    and Azure Local environments. A few examples of resources required
    (work with the respective Azure Admins, not an exhaustive list
    below):

-   Allocate public facing IP address.

-   Key Vault Administrator role.

-   Manage network Security Groups.

1.  HCP Anywhere Enterprise Portal and Edge Filer images obtained from
    HCP Anywhere Enterprise support

### Obtaining HCP Anywhere Enterprise Images

To deploy HCP Anywhere Enterprise Portal and Edge Filers, <u>you'll need
to acquire the necessary images from HCP Anywhere Enterprise
support</u>. The specific images required depend on your deployment
target:

#### For Installing HCP AWE Portal on Azure

-   Request the following image files from **HCP Anywhere Enterprise
    support**:

    -   CentOS-HCP-AWE-Portal-Image-x-y-z-OS-disk.vhd (OS disk image)

    -   CentOS-HCP-AWE-Portal-Image-x-y-z-Data-Disk.vhd (Data disk
        image)

#### For Installing HCP AWE Portal and Edge Filer on Azure Local

-   Request the Hyper-V based \*.vhd file for the HCP Anywhere
    Enterprise Portal and Edge Filer from HCP Anywhere Enterprise
    support.

#### Storing and Uploading HCP Anywhere Enterprise Images

Once you have obtained the necessary images, follow these steps to store
and upload them:

1.  Store copies of the image files on your self-managed storage for
    backup purposes.

2.  Upload the images to the proper location based on your deployment
    target:

    -   **Azure Blob Storage**:

        -   Create a new storage account in the Azure portal (or use an
            existing one).

        -   Create a new container within the storage account.

        -   Upload the HCP Anywhere Enterprise Portal and Edge Filer
            image files to the container.

        -   Or use **AzCopy.exe** with the command AzCopy.exe cp
            "&lt;source\_uri&gt;" "&lt;destination\_uri&gt;" for all the
            VHD files.

    -   **Azure Compute Gallery (Recommended for Azure deployment)**:

        -   Create a new Compute Gallery in the Azure portal.

        -   Add
            the CentOS-HCP-AWE-Portal-Image-x-y-z-OS-disk.vhd and CentOS-HCP-AWE-Portal-Image-x-y-z-Data-Disk.vhd files
            as image definitions within the gallery.

    -   **USB Stick (Optional – for air-gapped environment)**:

        -   Copy the Hyper-V based HCP Anywhere Enterprise Portal and
            Edge Filer image files to a USB stick for manual transfer to
            your Azure Local environment in the field.

### Installing HCP Anywhere Enterprise Portal on Azure

#### Warning

-   Do not clone an existing/running HCP Anywhere Enterprise Portal as
    template for installation. Always use the provided VHD template
    file.

#### Installation Workflow

1.  **Option 1: Create a Portal Instance with VHD image in Azure Compute
    Gallery** :

    -   Follow the steps on the documentation of Azure Compute Gallery
        for creating “Specialized” VM
        (<https://learn.microsoft.com/en-us/azure/virtual-machines/vm-specialized-image-version?tabs=portal%2Ccli2%2Ccli3%2Ccli4%2Cportal5>).

2.  **Option 2: Create a Portal Instance with VHD image in Azure Blob
    Storage** :

    -   In Azure, go to the Images service and click Create.

    -   Fill in the basics: Resource group (with premium storage), Name,
        Region, OS type (Linux), VM generation (Gen 1), and Storage blob
        URI for the OS VHD file.

    -   Add the data disk VHD file as a data disk.

    -   Select Premium SSD for both disks.

    -   Review and create the image.

    -   From the Images service, select the created HCP AWE Portal image
        and click Create VM.

    -   Configure the VM settings: Resource group, Virtual machine name,
        Region, Size (based on requirements), Authentication type
        (Password), Username, and Password.

    -   Set inbound rules to include HTTPS (443).

    -   On the Disks tab, create and attach a new disk for the archive
        storage if it's a primary or replication server. Use Premium SSD
        and set Host caching to Read/write.

    -   Review and create the VM.

3.  **Configure Network Settings**:

    -   After VM deployment, note/configure the Public IP address.

    -   Add necessary inbound and outbound port rules as per HCP AWE's
        requirements.

4.  **Logging in and Configuring the Server**:

    -   SSH into the server using the root user and the initial, default
        password (ctera321), then change the password.

    -   Identify the disk for the archive pool using **fdisk -l**.

    -   Create the archive pool with **portal-storage-util.sh**
        **create\_db\_archive\_pool &lt;Device&gt;**.

    -   Start HCP AWE Portal services with **portal-manage.sh start**.

5.  **Set a Default Gateway** (if needed):

    -   Run **echo
        "GATEWAY=&lt;****default\_gateway\_ip\_address&gt;****" &gt;
        /****etc/****sysconfig/network** and restart the network service
        with **service network restart**.

### Installing HCP Anywhere Enterprise Portal on Azure Local (Hyper-V)

#### Warning

-   Do not clone an existing/running HCP Anywhere Enterprise Portal as
    template for installation. Always use the provided VHD template
    files.

#### Installation Workflow (as **Non-Arc VM**)

-   Non-Arc VMs on Azure Local are managed using **traditional
    on-premises tools** and local access controls, while Arc VMs
    leverage Azure’s management tools.

##### Create a Portal Instance in Hyper-V:

-   Open the Azure Local management interface:

    1.  Option 1: Use Windows Admin Center

    2.  Option 2: Use PowerShell

    3.  Option 3: Use Windows Admin Center on Azure portal (if your
        Azure Local cluster is registered with Azure and WAC on Azure
        enabled)  
        <img src=".\attachments\/media/image13.png"
        style="width:3in;height:2.17in"
        alt="A screenshot of a computer Description automatically generated" />

-   Specify storage locations for the VM and its data pool disk.
    (**Note**: a Portal VM requires running both the provided OS and
    Data VHD files as a set. To add additional storage aside from the
    default Data partition, check **step 2**.)

-   Finish the wizard and start the virtual machine.

##### **Configure Additional Storage** (for primary and replication servers):

-   Right-click the VM and go to Settings.

-   Add a new hard drive under the IDE Controller, selecting VHDX format
    and dynamically expanding disk type.

-   Specify the size (**minimum 200GB, recommended 2% of expected global
    file system size**).

##### Log in to the Server to Create the Archive Pool:

-   Connect to the VM (default password: ctera321) and change the
    password.

-   Identify the disk for the archive pool using **fdisk -l**.

-   Create the archive pool with **portal-storage-util.sh**
    **create\_db\_archive\_pool &lt;Device&gt;**.

-   Start HCP AWE Portal services with **portal-manage.sh start**.

##### Configure Network Settings:

-   By default, DHCP is used. For production, a static IP is
    recommended.

-   Use **nmtui** to configure network settings, including setting a
    static IP, default gateway, and DNS servers.

-   Restart the network service with **service network restart** for
    changes to take effect.

##### Configuring a Default Gateway (if needed):

-   Run **echo "GATEWAY=&lt;****default\_gateway\_ip\_address&gt;****"
    &gt; /****etc/****sysconfig/network**.

-   Restart the network service.

#### Installation Workflow (as **Arc VM** – Option 1)

-   This option (Option 1) is highly manual and **not preferred** due to
    the current Azure Portal’s support for Arc VM on Azure Local.
    However, the procedure includes valuable skills that can assist with
    the ongoing management of HCP Anywhere Enterprise on Azure Local.

-   Arc VMs on Azure Local utilize Azure’s management tools and security
    features for a unified management experience across on-premises and
    cloud environments. However, the OS partition of the Portal VM is
    immutable, and only basic Arc VM features are used, without Guest
    Management enabled.  
    <img src=".\attachments\/media/image14.png"
    style="width:4in;height:2.65641in"
    alt="A screenshot of a computer Description automatically generated" />

-   The Azure Portal UI does not support deploying Gen1 Linux VMs, which
    our images are based on. Therefore, we must partially use the ARM
    template method for deployment.

-   The procedure below will begin with copying the Portal OS and Data
    VHD files from your Azure Storage Account to your Azure Local
    cluster’s CSV (cluster shared volume), allowing you to create the
    Portal VM using these images later.

##### Load the OS and Data VHD files onto Azure Local as “VM Image”

-   **Prerequisite**:

    1.  Basic understanding of ARM (Azure Resource Manager) template
        operations.

    2.  The Portal OS and Data VHD files are already uploaded to an
        Azure Storage Account that you have access to and permission to
        share.

    3.  Understand how to generate SAS Links (example shown using
        Microsoft Azure Storage Explorer below) and save the SAS links
        of the OS and Data VHD files to a place that you can access
        later  
        <img src=".\attachments\/media/image15.png"
        style="width:4in;height:3.80043in"
        alt="A screenshot of a computer Description automatically generated" />

-   Use ARM template to deploy the “VM Images”:

    1.  Use “**Deploy a customer template**” service on Azure Portal  
        <img src=".\attachments\/media/image16.png"
        style="width:3in;height:1.33641in"
        alt="A screenshot of a computer Description automatically generated" />

    2.  Choose “**Build your own template in the editor**”

    3.  Copy the example ARM template below, paste into UI on Azure, and
        click “Save”


```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "apiVersion": {
            "type": "string"
        },
        "customLocationId": {
            "type": "string"
        },
        "location": {
            "type": "string"
        },
        "osImageName": {
            "type": "string"
        },
        "dataImageName": {
            "type": "string"
        },
        "osType": {
            "type": "string"
        },
        "osImagePath": {
            "type": "securestring"
        },
	"dataImagePath": {
            "type": "securestring"
        },
        "hyperVGeneration": {
            "type": "string"
        }
    },
    "resources": [
        {
            "apiVersion": "[parameters('apiVersion')]",
            "extendedLocation": {
                "name": "[parameters('customLocationId')]",
                "type": "CustomLocation"
            },
            "location": "[parameters('location')]",
            "name": "[parameters('osImageName')]",
            "properties": {
                "osType": "[parameters('osType')]",
                "hyperVGeneration": "[parameters('hyperVGeneration')]",
                "imagePath": "[parameters('OSImagePath')]"
            },
            "tags": {},
            "type": "microsoft.azurestackhci/galleryimages"
        },
		        {
            "apiVersion": "[parameters('apiVersion')]",
            "extendedLocation": {
                "name": "[parameters('customLocationId')]",
                "type": "CustomLocation"
            },
            "location": "[parameters('location')]",
            "name": "[parameters('dataImageName')]",
            "properties": {
                "osType": "[parameters('osType')]",
                "hyperVGeneration": "[parameters('hyperVGeneration')]",
                "imagePath": "[parameters('dataImagePath')]"
            },
            "tags": {},
            "type": "microsoft.azurestackhci/galleryimages"
        }
    ]
}

```


<img src=".\attachments\/media/image17.png"
style="width:6.3in;height:6.13644in"
alt="A screenshot of a computer program Description automatically generated" />  
Figure – Save the template after you have pasted the content

1.  Fill in the parameters:  
    <img src=".\attachments\/media/image18.png"
    style="width:3in;height:4.20389in" />

    1.  **Resource Group**: New or Existing group

    2.  **Region**: The region where your Azure Local cluster and the
        **Custom Location** (see below) are located.

    3.  **API Version**: Use “2023-09-01-preview”

    4.  **Custom Location ID**: Each Azure Local Cluster comes with a
        Custom Location ID, which you can find it by hunting down to the
        resource and click into the JSON View like this  
        <img src=".\attachments\/media/image19.png"
        style="width:4in;height:1.55632in" />  
        Where you can also find the “**location**” parameter

    5.  **Location**: The same as “Region” but needs to be entered again
        using the corresponding code found in the **Custom Location**
        JSON View.

    6.  **OS Image Name**: A name you will recognize for the OS VHD

    7.  **Data Image Name**: A name you will recognize for the Data VHD

    8.  **OS Type**: Enter “Linux”

    9.  **OS Image Path**: Paste the SAS Link of the OS VHD image you
        generated previously

    10. **Data Image Path**: Paste the SAS Link of the Data VHD image
        you generated previously

    11. **Hyper V Generation**: Enter “**V1**” (must be “**V1**” for Gen
        1 image).

    12. **Note 1** – This template is a working example. Experienced ARM
        users can easily customize as they see fit.

    13. **Note 2** – ARM templates can be created to deploy all the
        resources needed for the Portal VM on your Azure Local cluster;
        this advanced topic will be covered in a later section of this
        document.

2.  Click “**Review + Create**” after filling in the parameters

3.  If no error alerts showing up, click “**Create**” and wait the
    process to finish

4.  The copying time depends on the internet speed at the location of
    the Azure Local

5.  After the successful ARM deployment, you can find the images in “VM
    images” section of your Azure Local cluster  
    <img src=".\attachments\/media/image20.png"
    style="width:3in;height:2.09103in"
    alt="A screenshot of a computer Description automatically generated" />

##### Create a Portal VM Instance from Azure Portal:

-   **Note**: Advanced users can use PowerShell / Az CLI / ARM templates
    to create the Portal VM instance. Below only shows deployment using
    Azure Portal

-   **Prerequisite**:

    1.  Ensure the VM images are uploaded to the cluster and accessible

    2.  Ensure there are “Logical networks” created and configured on
        the cluster for the VM usage

-   “**Create VM**” in the Azure Local UI on Azure  
    <img src=".\attachments\/media/image21.png"
    style="width:3in;height:2.84171in"
    alt="A screenshot of a computer Description automatically generated" />

-   Fill in the parameters for the VM:

    1.  Choose the Subscription and Resource Group where your VM will be

    2.  Enter unique “**Virtual machine name**”

    3.  Skip “**Custom location**” and “**Virtual machine kind**” as
        they are assigned automatically when you create the Arc VM from
        the UI

    4.  Choose “Standard” for “**Security type**”

    5.  For “**Storage path**”, you can select either option based your
        preference

    6.  For “**Image**”, choose the OS image you uploaded previously

    7.  Enter the desired capacities for “**Virtual processor count**”
        and “**Memory (MB)**”

    8.  Use “Static” for “**Memory type**”

    9.  Uncheck “**Enable guest management**” since the OS partition is
        immutable  
        <img src=".\attachments\/media/image22.png"
        style="width:3in;height:0.71827in"
        alt="A screenshot of a computer Description automatically generated" />

    10. (Optional) Fill in “**VM proxy configuration**” if you want to
        use a proxy. Details are not covered here

    11. For “**Root user**” section, enter dummy values since the OS
        partition is immutable

-   For “**Add new disk to Arc VM**” -- The Data disk uploaded
    previously **cannot** attach to the Arc VM directly. We should skip
    this step.

-   Add network interface  
    <img src=".\attachments\/media/image23.png"
    style="width:3in;height:1.44663in" />

-   (Optional) Add Tags

-   Finally, create the Arc VM. This step will generate a Private key
    PEM file. **You don’t have to keep it since the OS partition is
    immutable**. This step will take about **20** minutes to complete VM
    creation and Azure Arc registration.

-   Finish the wizard and start the virtual machine.

-   At this point, there is no Data Disk attached to the Arc VM yet.

-   Finally, stop the Portal VM.

##### Create the Data Disk and Attach to the Arc VM

-   The steps in this section are the most complex and require careful
    attention. This complexity arises from the current limitations of
    the Azure Portal and Azure REST API in supporting Arc VM disks.

-   Therefore, in this section, we will first create a Dummy Data Disk,
    replace the Dummy Data Disk with a copy of the Data VHD, attach it
    to the Arc VM, and finally test if the Arc VM is functioning
    properly.

-   Create a Dummy Data Disk via ARM template

    1.  Due to Azure Portal only supporting creating a Data Disk in VHDX
        format, we use ARM template to create a Dummy Data Disk in VHD
        format.

    2.  Use “**Deploy a customer template**” service on Azure Portal and
        “**Build your own template in the editor**”

    3.  Use a template like below or customize it based your needs:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "customLocationId": {
      "type": "string"
    },
    "location": {
      "type": "string"
    },
    "vmName": {
      "type": "string"
    }
  },
  "resources": [
	{
      "type": "Microsoft.AzureStackHCI/virtualHardDisks",
      "apiVersion": "2023-09-01-preview",
      "name": "[concat(parameters('vmName'), '-data')]",
      "location": "[parameters('location')]",
      "extendedLocation": {
        "name": "[parameters('customLocationId')]",
        "type": "CustomLocation"
      },
      "properties": {
        "diskFileFormat": "vhd",
        "diskSizeGB": 60,
        "dynamic": false,
        "hyperVGeneration": "V1"
      }
    }
  ]
}
```


1.  Fill in the parameters (details not provided) then Deploy:  
    <img src=".\attachments\/media/image24.png"
    style="width:3in;height:2.76378in" />

2.  Verify Deployment by checking “Disks” resources:  
    <img src=".\attachments\/media/image25.png"
    style="width:3in;height:3.31929in"
    alt="A screenshot of a computer Description automatically generated" />

-   Replace the Dummy Data Disk with a copy of the Data VHD. The steps
    are

    1.  Copy the ACL information from the Dummy Data Disk.

    2.  Remove the Dummy Data Disk.

    3.  Copy the Portal Data VHD to the location of the deleted Dummy
        Data Disk, ensuring it has the same name.

    4.  Apply the previously copied ACL information to the Portal Data
        Disk

```powershell
\# Step 0: Find the path to the Dummy Data Disk VHD file. It resides in
Cluster Storage. Example:
C:\ClusterStorage\UserStorage\_2\e254bb98922eeec\PortalDemo2-data-&lt;subscription\_id&gt;-&lt;resource
group\_name&gt;.vhd

\# Step 1: Copy the ACL information from the Dummy Data Disk

$acl = Get-Acl -Path "C:\Path\To\DummyDataDisk.vhd"

\# Step 2: Remove the Dummy Data Disk

Remove-Item -Path "C:\Path\To\DummyDataDisk.vhd" -Force

\# Step 3: Copy the Portal Data VHD to the location of the deleted Dummy
Data Disk, ensuring it has the same name

Copy-Item -Path "C:\Path\To\PortalDataVHD.vhd" -Destination
"C:\Path\To\DummyDataDisk.vhd"

\# Step 4: Apply the previously copied ACL information to the Portal
Data Disk

Set-Acl -Path "C:\Path\To\DummyDataDisk.vhd" -AclObject $acl
```
-   Attach The Portal Data VHD to the Arc VM

    1.  Get familiar with Azure CLI. Details are not provided here.

    2.  Use “az stack-hci-vm disk attach” to attach the Portal Data VHD
        to the Portal VM
```powershell
az stack-hci-vm disk attach \\

--resource-group "your-resource-group" \\

--vm-name "your-vm-name" \\

--disks "your-disk"

\# If error occurs due to the incompatible version of “stack-hci-vm”,
use commands below to install the needed version:

az extension remove --name stack-hci-vm

az extension add --name stack-hci-vm --version
&lt;the-compatible-version&gt;
```
-   Test if the Arc VM is functioning

    1.  Go to the Portal VM resource page

    2.  Check if the data disk shows up  
        <img src=".\attachments\/media/image26.png"
        style="width:3in;height:1.89784in"
        alt="A screenshot of a computer Description automatically generated" />

    3.  Start the Portal VM (we stopped it earlier) and wait until the
        VM “Status” shows “Running

##### **Configure Additional Storage** (for primary and replication servers):

-   Add new disk  
    <img src=".\attachments\/media/image27.png"
    style="width:3in;height:2.29167in"
    alt="A screenshot of a computer Description automatically generated" />

-   Add a new hard drive under the IDE Controller, selecting dynamically
    provisioning type with minimum **200GB**, recommended **2%** of
    expected global file system size.  
    <img src=".\attachments\/media/image28.png"
    style="width:3in;height:1.82857in"
    alt="A screenshot of a computer Description automatically generated" />

-   Save the configuration to create the disk  
    <img src=".\attachments\/media/image29.png"
    style="width:3in;height:1.08716in"
    alt="A screenshot of a computer Description automatically generated" />

-   Wait until the disk is created and the VM is updated  
    <img src=".\attachments\/media/image30.png"
    style="width:3in;height:2.18493in"
    alt="A screenshot of a computer Description automatically generated" />

##### Log in to the Server to Create the Archive Pool:

-   **IMPORTANT:** Although the Portal VM has an assigned IP address,
    its networking setup is not yet complete. To connect, use either a
    locally set up Windows Admin Center (WAC) or WAC on Azure. For this
    example, we will use WAC on Azure.

-   Connect to the WAC on Azure from the Azure Local UI  
    <img src=".\attachments\/media/image31.png"
    style="width:3in;height:2.14359in"
    alt="A screenshot of a computer Description automatically generated" />

-   Find the Portal VM  
    <img src=".\attachments\/media/image32.png"
    style="width:3in;height:2.15833in"
    alt="A screenshot of a computer Description automatically generated" />

-   Enter the VM’s UI and Connect  
    <img src=".\attachments\/media/image33.png"
    style="width:3in;height:2.58034in"
    alt="A screenshot of a computer Description automatically generated" />

-   Enter the credentials that can manage the VM on the local cluster.
    This is typically a legitimate network login.  
    <img src=".\attachments\/media/image34.png"
    style="width:3in;height:1.73526in"
    alt="A screenshot of a computer Description automatically generated" />

-   Log in to the VM using the default credentials (username: root,
    password: ctera321), and then change the password.  
    <img src=".\attachments\/media/image35.png"
    style="width:3in;height:1.12127in"
    alt="A screenshot of a computer Description automatically generated" />

-   Identify the disk for the archive pool using **fdisk -l**.

-   Create the archive pool with **portal-storage-util.sh
    create\_db\_archive\_pool &lt;Device&gt;**.  
    <img src=".\attachments\/media/image36.png"
    style="width:4in;height:2.59017in"
    alt="A screenshot of a computer screen Description automatically generated" />

-   Start HCP AWE Portal services with **portal-manage.sh start**.  
    <img src=".\attachments\/media/image37.png"
    style="width:4in;height:0.39188in" />

##### Configure Network Settings:

-   During the previous step of creating a Portal VM, an IP address was
    assigned to the VM. Locate this IP address in the Azure Portal
    before proceeding.

-   Use **nmtui** to configure network settings, including setting a
    static IP, default gateway, and DNS servers.

-   Restart the network service with **service network restart** for
    changes to take effect.

#### Installation Workflow (as **Arc VM** – Option 2)

-   This option (Option 2) is **preferred** and has less steps than
    Option 1. This option heavily utilizes ARM template, covering the
    step 1, 2, and partial 3 in Option 1, reducing manual works. This
    option deploys several resources, with dependencies configured, at
    once.

##### Deploy a Portal VM instance with all the required resources in a single ARM template

-   **Prerequisites**:

    1.  Ensure the VM images are uploaded to the cluster and accessible

    2.  Ensure there are “Logical networks” created and configured on
        the cluster for the VM usage

    3.  Ensure you have created a dummy Key pair that the dummy public
        key can be used as “Key Data” parameter. You can use OpenSSL to
        create or other tools convenient to use.

    4.  **IMPORTANT** – The ARM template example below includes
        hardcoded parameters for processors and memory sizes. Adjust
        these (in the “**hardwareProfile**” key ) based on your
        requirements or create additional input parameters.

-   Use ARM template to deploy all the resources at once:

    1.  Use “**Deploy a customer template**” service on Azure Portal  
        <img src=".\attachments\/media/image16.png"
        style="width:3in;height:1.33641in"
        alt="A screenshot of a computer Description automatically generated" />

    2.  Choose “**Build your own template in the editor**”

    3.  Copy the example ARM template below, paste into UI on Azure, and
        click “Save”

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "customLocationId": {
      "type": "string"
    },
    "location": {
      "type": "string"
    },
    "osImageName": {
      "type": "string"
    },
	"osImagePath": {
      "type": "securestring"
    },
	"dataImageName": {
      "type": "string"
    },
	"dataImagePath": {
      "type": "securestring"
    },
    "vmName": {
      "type": "string"
    },
    "adminUsername": {
      "type": "string"
    },
    "adminPassword": {
      "type": "securestring"
    },
    "securityType": {
      "type": "string"
    },
    "keyData": {
      "type": "securestring"
    },
    "logicNetworkId": {
      "type": "string"
    },
    "logicNetworkGateway": {
      "type": "string"
    }
  },
  "resources": [
    {
      "type": "microsoft.azurestackhci/galleryimages",
      "apiVersion": "2023-09-01-preview",
      "name": "[parameters('osImageName')]",
      "location": "[parameters('location')]",
      "extendedLocation": {
        "name": "[parameters('customLocationId')]",
        "type": "CustomLocation"
      },
      "properties": {
        "osType": "Linux",
        "hyperVGeneration": "V1",
        "imagePath": "[parameters('osImagePath')]"
      },
      "tags": {}
    },
	{
      "type": "microsoft.azurestackhci/galleryimages",
      "apiVersion": "2023-09-01-preview",
      "name": "[parameters('dataImageName')]",
      "location": "[parameters('location')]",
      "extendedLocation": {
        "name": "[parameters('customLocationId')]",
        "type": "CustomLocation"
      },
      "properties": {
        "osType": "Linux",
        "hyperVGeneration": "V1",
        "imagePath": "[parameters('dataImagePath')]"
      },
      "tags": {}
    },
    {
      "type": "Microsoft.HybridCompute/machines",
      "apiVersion": "2023-06-20-preview",
      "name": "[parameters('vmName')]",
      "kind": "HCI",
      "location": "[parameters('location')]",
      "identity": {
        "type": "SystemAssigned"
      }
    },
    {
      "type": "Microsoft.AzureStackHCI/networkInterfaces",
      "apiVersion": "2023-09-01-preview",
      "name": "[concat(parameters('vmName'), '-nic')]",
      "location": "[parameters('location')]",
      "extendedLocation": {
        "name": "[parameters('customLocationId')]",
        "type": "CustomLocation"
      },
      "properties": {
        "ipConfigurations": [
          {
            "name": "[concat(parameters('vmName'), '-nic')]",
            "properties": {
              "gateway": "[parameters('logicNetworkGateway')]",
              "subnet": {
                "id": "[parameters('logicNetworkId')]"
              }
            }
          }
        ]
      }
    },
	{
      "type": "Microsoft.AzureStackHCI/virtualHardDisks",
      "apiVersion": "2023-09-01-preview",
      "name": "[concat(parameters('vmName'), '-data')]",
      "location": "[parameters('location')]",
      "extendedLocation": {
        "name": "[parameters('customLocationId')]",
        "type": "CustomLocation"
      },
      "properties": {
        "diskFileFormat": "vhd",
        "diskSizeGB": 60,
        "dynamic": false,
        "hyperVGeneration": "V1"
      }
    },
    {
      "type": "Microsoft.AzureStackHCI/VirtualMachineInstances",
      "apiVersion": "2023-09-01-preview",
      "name": "default",
      "scope": "[concat('Microsoft.HybridCompute/machines/', parameters('vmName'))]",
      "extendedLocation": {
        "name": "[parameters('customLocationId')]",
        "type": "CustomLocation"
      },
      "dependsOn": [
        "[resourceId('Microsoft.HybridCompute/machines', parameters('vmName'))]",
        "[resourceId('Microsoft.AzureStackHCI/networkInterfaces', concat(parameters('vmName'), '-nic'))]",
        "[resourceId('microsoft.azurestackhci/galleryimages', parameters('osImageName'))]",
		"[resourceId('microsoft.azurestackhci/galleryimages', parameters('dataImageName'))]",
		"[resourceId('Microsoft.AzureStackHCI/virtualHardDisks', concat(parameters('vmName'), '-data'))]"
      ],
      "properties": {
        "osProfile": {
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]",
          "computerName": "[parameters('vmName')]",
          "linuxConfiguration": {
            "provisionVMAgent": false,
            "provisionVMConfigAgent": false,
            "ssh": {
              "publicKeys": [
                {
                  "keyData": "[parameters('keyData')]",
                  "path": "[concat('/home/', parameters('adminUsername'), '/.ssh/authorized_keys')]"
                }
              ]
            },
            "disablePasswordAuthentication": false
          }
        },
        "hardwareProfile": {
          "vmSize": "Default",
          "processors": 4,
          "memoryMB": 8192
        },
        "storageProfile": {
		  "dataDisks": [
		    {
              "id": "[resourceId('Microsoft.AzureStackHCI/virtualHardDisks', concat(parameters('vmName'), '-data'))]"
            }
		  ],
          "imageReference": {
            "id": "[resourceId('microsoft.azurestackhci/galleryimages', parameters('osImageName'))]"
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.AzureStackHCI/networkInterfaces', concat(parameters('vmName'), '-nic'))]"
            }
          ]
        }
      }
    }
  ]
}

```


4.  Fill in the parameters:  
    <img src=".\attachments\/media/image38.png"
    style="width:3in;height:4.6535in" />

    1.  **Resource Group**: New or Existing group

    2.  **Region**: The region where your Azure Local cluster and the
        **Custom Location** (see below) are located.

    3.  **Custom Location ID**: Each Azure Local Cluster comes with a
        Custom Location ID, which you can find it by hunting down to the
        resource and click into the JSON View like this  
        <img src=".\attachments\/media/image19.png"
        style="width:4in;height:1.55632in"
        alt="A screenshot of a computer Description automatically generated" />  
        Where you can also find the “**location**” parameter

    4.  **Location**: The same as “Region” but needs to be entered again
        using the corresponding code found in the **Custom Location**
        JSON View.

    5.  **OS Image Name**: A name you will recognize for the OS VHD

    6.  **OS Image Path**: Paste the SAS Link of the OS VHD image you
        generated previously

    7.  **Data Image Name**: A name you will recognize for the Data VHD

    8.  **Data Image Path**: Paste the SAS Link of the Data VHD image
        you generated previously

    9.  **VM Name**: The name of the Portal VM instance to be created

    10. **Admin Username**: This can be **any dummy username**, not to
        be used, to satisfy Azure Rest API requirements

    11. **Admin Password**: This can be **any dummy password**, not to
        be used, to satisfy Azure Rest API requirements

    12. **Security Type**: Enter “Standard”

    13. **Key Data**: Enter the dummy public key generated previously

    14. **Logic Network ID**: The resource ID that you can acquire in
        the JSON view of the logic network resource

    15. **Logic Network Gateway**: The gateway IP to be supplied to the
        Portal VM’s NIC

    16. **Note** – This template is a working example. Experienced ARM
        users can easily customize as they see fit.

5.  Click “**Review + Create**” after filling in the parameters

6.  If no error alerts showing up, click “**Create**” and wait the
    process to finish

7.  Check if the Portal VM and related resources are created and running

8.  Stop the Portal VM

##### Replace the Dummy Data Disk

-   Replace the Dummy Data Disk with a copy of the Data VHD. The steps
    are

    1.  Copy the ACL information from the Dummy Data Disk.

    2.  Remove the Dummy Data Disk.

    3.  Copy the Portal Data VHD to the location of the deleted Dummy
        Data Disk, ensuring it has the same name.

    4.  Apply the previously copied ACL information to the Portal Data
        Disk
    
    5. Start the Portal VM.
```powershell
# Step 0: Find the path to the Dummy Data Disk VHD file. It resides in
Cluster Storage. Example:
C:\ClusterStorage\UserStorage\_2\e254bb98922eeec\PortalDemo2-data-&lt;subscription\_id&gt;-&lt;resource
group\_name&gt;.vhd

# Step 1: Copy the ACL information from the Dummy Data Disk

$acl = Get-Acl -Path "C:\Path\To\DummyDataDisk.vhd"

# Step 2: Remove the Dummy Data Disk

Remove-Item -Path "C:\Path\To\DummyDataDisk.vhd" -Force

# Step 3: Copy the Portal Data VHD to the location of the deleted Dummy
Data Disk, ensuring it has the same name

Copy-Item -Path "C:\Path\To\PortalDataVHD.vhd" -Destination
"C:\Path\To\DummyDataDisk.vhd"

# Step 4: Apply the previously copied ACL information to the Portal
Data Disk

Set-Acl -Path "C:\Path\To\DummyDataDisk.vhd" -AclObject $acl

# Step 5: Start the Portal VM.
```


##### Follow Step 4 to 6 in Option 1

-   **Note 1**: Step 4 to 6 is the common steps that can be used in
    Option 2

-   **Note 2**: Experienced ARM template users can include “Additional
    Storage” in the ARM template to further simplify the deployment
    process

#### Add Storage Nodes for HCP AWE Portal

This procedure is standard for all Portal Installation Workflows.

1.  **Log in to the Server**:

    -   For NFS storage nodes, log in to the server as **root** using
        SSH.

2.  **Create an NFS Mount Folder**:

    -   On the server, create a folder specifically for the NFS mount.

3.  **Mount the NFS Storage Node**:

    -   Run the following script on each server (except the preview
        server):

    -   portal-mount.sh mount\_storage\_node NFS\_IP:/NFS\_FOLDER

**Note**: Replace NFS\_IP with the IP address of the NFS mount point
and NFS\_FOLDER with the name of the folder created on the NFS server.

4.  **Access the Global Administration View**:

    -   In the HCP AWE Portal, navigate to **Main &gt; Storage
        Nodes** in the navigation pane.

5.  **Add or Edit a Storage Node**:

    -   Either add a new storage node by clicking **New Storage Node
        or** edit an existing one by clicking the node’s name.

    -   Enter the generic details for the storage node (applicable to
        all types).

    -   Depending on the storage node type (e.g., Amazon S3, Azure Blob,
        Hitachi HCP, etc.), complete the additional fields specific to
        that type.

#### Add HCP for Cloud Scale as Storage Nodes for HCP AWE Portal

This procedure is standard for all Portal Installation Workflows.

-   Log in to the “Admin” portal and select “Administration” context and
    click the “Storage Nodes”. Then click the “New Storage Node” to
    initiate the wizard.

<img src=".\attachments\/media/image39.png"
style="width:5in;height:3.41346in" />

<img src=".\attachments\/media/image40.png"
style="width:6.5in;height:3.39583in" />

-   Change the first dropdown “Type:” to Amazon S3. This will change the
    wizard UI as seen in the next screenshot.

<img src=".\attachments\/media/image41.png"
style="width:5.17433in;height:4.5625in" />

-   Provide the required fields

    -   Your access key and secret access key can be generated from the
        HCP CS Console.

<img src=".\attachments\/media/image42.png"
style="width:6.5in;height:1.09375in" />

-   Once completed, you will see the S3 bucket has successfully
    connected:

<img src=".\attachments\/media/image43.png"
style="width:6.5in;height:0.94792in" />

#### Additional Notes

-   For backup, block-storage-level snapshots are an option, but they
    have limitations regarding point-in-time recovery and data loss on
    failure.

-   For detailed network configuration, including static routes and DHCP
    settings, refer to the **nmtui** tool and the provided network
    service commands.

### Installing HCP Anywhere Enterprise Edge Filer on Azure Local (Hyper-V) 

#### Warning

-   Do not clone an existing/running HCP Anywhere Enterprise Edge Filer
    at template for installation. Always use the provided VHD template
    file.

#### Installation Workflow (as Non-Arc VM)

##### Create a Portal Instance in Hyper-V:

-   Open the Azure Local management interface:

    1.  Option 1: Use Windows Admin Center

    2.  Option 2: Use PowerShell

    3.  Option 3: Use Windows Admin Center on Azure portal (if your
        Azure Local cluster is registered with Azure and WAC on Azure
        enabled)  
        <img src=".\attachments\/media/image13.png"
        style="width:3in;height:2.17in"
        alt="A screenshot of a computer Description automatically generated" />

-   Create a new virtual machine with the following specifications:

    1.  Generation: 1

    2.  Memory: Assign the default startup memory recommended by the
        wizard

    3.  Virtual Processors: Adjust based on the HCP AWE Edge Filer
        license (see step 3)

    4.  Network Adapter: Connected to the appropriate virtual switch

    5.  Hard Disk: Attach the HCP AWE Edge Filer VHD file provided by
        HCP Anywhere Enterprise Support

##### Configure the Virtual Machine:

-   Attach an additional virtual hard disk to the VM for storing data:

    -   Format: VHDX

    -   Disk Type: Fixed size (recommended for performance) or
        Dynamically expanding

    -   Size: According to your license and needs (20% of the Portal
        Global Name Space recommended)

##### Set Virtual Processors:

-   Adjust the number of virtual processors based on the HCP AWE Edge
    Filer license:

    1.  EV16: up to 4 processors

    2.  EV32: up to 8 processors

    3.  EV64: up to 16 processors

    4.  EV128: up to 32 processors

    5.  EV256: up to 64 processors

##### Start the Virtual Machine:

-   Power on the Edge Filer VM to proceed with the initial setup.

#### Installation Workflow (as **Arc VM**)

-   Unlike illustrated in the Installation Workflows for Portal VM, this
    only describes how to deploy the Edge Filer VM using one ARM
    template. Users can break it down to separate deployments of the
    different resources as needed.

##### Deploy an Edge Filer VM instance with all the required resources in a single ARM template

-   **Prerequisites**:

    1.  Ensure the VM images are uploaded to the cluster and accessible

    2.  Ensure there are “Logical networks” created and configured on
        the cluster for the VM usage

    3.  Ensure you have created a dummy Key pair that the dummy public
        key can be used as “Key Data” parameter. You can use OpenSSL to
        create or other tools convenient to use.

    4.  **IMPORTANT** – The ARM template example below includes
        hardcoded parameters for processors and memory sizes. Adjust
        these (in the “**hardwareProfile**” key) based on your
        requirements or create additional input parameters.



-   Use ARM template to deploy all the resources at once:

    1.  Use “**Deploy a customer template**” service on Azure Portal  
        <img src=".\attachments\/media/image16.png"
        style="width:3in;height:1.33641in"
        alt="A screenshot of a computer Description automatically generated" />

    2.  Choose “**Build your own template in the editor**”

    3.  Copy the example ARM template below, paste into UI on Azure, and
        click “Save”

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "customLocationId": {
      "type": "string"
    },
    "location": {
      "type": "string"
    },
    "imageName": {
      "type": "string"
    },
    "imagePath": {
      "type": "securestring"
    },
    "name": {
      "type": "string"
    },
    "adminUsername": {
      "type": "string"
    },
    "adminPassword": {
      "type": "securestring"
    },
    "securityType": {
      "type": "string"
    },
    "keyData": {
      "type": "securestring"
    },
	"logicNetworkId": {
      "type": "string"
    },
	"logicNetworkGateway": {
      "type": "string"
    }
  },
  "resources": [
    {
      "type": "microsoft.azurestackhci/galleryimages",
      "apiVersion": "2023-09-01-preview",
      "name": "[parameters('imageName')]",
      "location": "[parameters('location')]",
      "extendedLocation": {
        "name": "[parameters('customLocationId')]",
        "type": "CustomLocation"
      },
      "properties": {
        "osType": "Linux",
        "hyperVGeneration": "V1",
        "imagePath": "[parameters('imagePath')]"
      },
      "tags": {}
    },
    {
      "type": "Microsoft.HybridCompute/machines",
      "apiVersion": "2023-06-20-preview",
      "name": "[parameters('name')]",
      "kind": "HCI",
      "location": "[parameters('location')]",
      "identity": {
        "type": "SystemAssigned"
      }
    },
    {
      "type": "Microsoft.AzureStackHCI/networkInterfaces",
      "apiVersion": "2023-09-01-preview",
      "name": "[concat(parameters('name'), '-nic')]",
      "location": "[parameters('location')]",
      "extendedLocation": {
        "name": "[parameters('customLocationId')]",
        "type": "CustomLocation"
      },
      "properties": {
        "ipConfigurations": [
          {
            "name": "[concat(parameters('name'), '-nic')]",
            "properties": {
              "gateway": "[parameters('logicNetworkGateway')]",
              "subnet": {
                "id": "[parameters('logicNetworkId')]"
              }
            }
          }
        ]
      }
    },
    {
      "type": "Microsoft.AzureStackHCI/VirtualMachineInstances",
      "apiVersion": "2023-09-01-preview",
      "name": "default",
      "scope": "[concat('Microsoft.HybridCompute/machines/', parameters('name'))]",
      "extendedLocation": {
        "name": "[parameters('customLocationId')]",
        "type": "CustomLocation"
      },
      "dependsOn": [
        "[resourceId('Microsoft.HybridCompute/machines', parameters('name'))]",
        "[resourceId('Microsoft.AzureStackHCI/networkInterfaces', concat(parameters('name'), '-nic'))]",
        "[resourceId('microsoft.azurestackhci/galleryimages', parameters('imageName'))]"
      ],
      "properties": {
        "osProfile": {
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]",
          "computerName": "[parameters('name')]",
          "linuxConfiguration": {
            "provisionVMAgent": false,
            "provisionVMConfigAgent": true,
            "ssh": {
              "publicKeys": [
                {
                  "keyData": "[parameters('keyData')]",
                  "path": "[concat('/home/', parameters('adminUsername'), '/.ssh/authorized_keys')]"
                }
              ]
            },
            "disablePasswordAuthentication": false
          }
        },
        "hardwareProfile": {
          "vmSize": "Default",
          "processors": 4,
          "memoryMB": 8192
        },
        "storageProfile": {
          "imageReference": {
            "id": "[resourceId('microsoft.azurestackhci/galleryimages', parameters('imageName'))]"
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.AzureStackHCI/networkInterfaces', concat(parameters('name'), '-nic'))]"
            }
          ]
        }
      }
    }
  ]
}

```


4.  Fill in the parameters:  
    <img src=".\attachments\/media/image44.png"
    style="width:3in;height:4.05224in"
    alt="A screenshot of a computer Description automatically generated" />

    1.  **Resource Group**: New or Existing group

    2.  **Region**: The region where your Azure Local cluster and the
        **Custom Location** (see below) are located.

    3.  **Custom Location ID**: Each Azure Local Cluster comes with a
        Custom Location ID, which you can find it by hunting down to the
        resource and click into the JSON View like this  
        <img src=".\attachments\/media/image19.png"
        style="width:4in;height:1.55632in"
        alt="A screenshot of a computer Description automatically generated" />  
        Where you can also find the “**location**” parameter

    4.  **Location**: The same as “Region” but needs to be entered again
        using the corresponding code found in the **Custom Location**
        JSON View.

    5.  **Image Name**: A name you will recognize for the EF VHD

    6.  **Image Path**: Paste the SAS Link of the EF VHD image you
        generated previously

    7.  **Name**: The name of the Edge Filer VM instance to be created

    8.  **Admin Username**: This can be **any dummy username**, not to
        be used, to satisfy Azure Rest API requirements

    9.  **Admin Password**: This can be **any dummy password**, not to
        be used, to satisfy Azure Rest API requirements

    10. **Security Type**: Enter “Standard”

    11. **Key Data**: Enter the dummy public key generated previously

    12. **Logic Network ID**: The resource ID that you can acquire in
        the JSON view of the logic network resource

    13. **Logic Network Gateway**: The gateway IP to be supplied to the
        Portal VM’s NIC

    14. **Note** – This template is a working example. Experienced ARM
        users can easily customize as they see fit.

5.  Click “**Review + Create**” after filling in the parameters

6.  If no error alerts showing up, click “**Create**” and wait the
    process to finish

7.  Check if the Edge Filer VM and related resources are created and
    running

8.  Stop the Edge Filer VM

##### Configure the Virtual Machine:

-   Attach an additional virtual hard disk to the VM for storing data as
    needed:

    -   Format: VHDX

    -   Disk Type: Fixed size (recommended for performance) or
        Dynamically expanding

    -   Size: According to your license and needs (20% of the Portal
        Global Name Space recommended)

-   Perform the action using the Azure Portal after creating the EF VM,
    or define additional resources in the ARM template before creating
    the EF VM.

##### Start the Virtual Machine:

-   Power on the Edge Filer VM to proceed with the initial setup.

#### Initial Network Configuration

This procedure is standard for all Portal Installation Workflows.

-   **For DHCP**:

    -   Log in to the VM console using the username **setup** with no
        password.

    -   The DHCP-assigned IP address will be displayed on the console.

-   **For Static IP**:

    -   Access the VM console and log in as above.

    -   Navigate to Network settings and select Static IP mode.

    -   Enter the required network details: static IP, netmask, default
        gateway, and DNS server IPs.

    -   Confirm the settings with OK.

#### Additional Notes

-   Ensure that the virtual network and subnet for the HCP AWE Edge
    Filer VM are properly configured in Azure Local.

-   Configure the necessary inbound and outbound firewall rules for the
    HCP AWE Edge Filer based on the communication requirements.

-   Follow best practices for securing and managing your virtual
    machines, such as regularly applying updates, configuring backup and
    disaster recovery, and monitoring resource utilization.

### Recommendation: Deployments with Azure Resource Manager templates

Azure Resource Manager (ARM) templates are JSON files that declaratively
define the infrastructure and configuration of Azure resources. They
allow you to create, update, and delete resources consistently and
repeatedly. ARM templates consist of parameters for customization,
variables for reusability, resources for specifying the desired state of
infrastructure, and outputs for returning important information after
deployment.

To deploy an ARM template, you use Azure PowerShell, Azure CLI, or the
Azure portal, providing the template file and required parameters. ARM
validates the template, creates a deployment plan, and provisions the
specified resources in the target Azure subscription and resource group.
ARM templates enable infrastructure as code, consistency across
environments, modularity, and extensibility, making it easier to
automate the provisioning and management of Azure resources.

#### Core Concepts

-   **ARM Templates Overview:** This is the foundational starting point
    to understanding the concept behind ARM
    templates. <https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/overview>

-   **ARM Templates Structure & Syntax:** Dive deeper into how to
    compose ARM templates and the elements
    within. <https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/template-syntax>

Below is an example of deploying HCP Anywhere Enterprise Edge Filer
using ARM templates on Azure (not on Azure Local). The workflow would as
well apply to deployments for HCP Anywhere Enterprise Portal. In order
to leverage Azure Resource Manager, a <u>template</u> is required. The
easiest method to create a template is to navigate to <u>an existing
successful deployment</u> and downloading the template.

<img src=".\attachments\/media/image45.png"
style="width:6.5in;height:2.125in" />

Select the deployment you would like to create a template from:

In this example, we will create a template from an HCP AWE Edge filer we
previously deployed via Azure Portal.

<img src=".\attachments\/media/image46.png"
style="width:6.5in;height:4.82292in" />

Once you click the deployment, navigate to the “Template” option and
click “Download”.

<img src=".\attachments\/media/image47.png"
style="width:6.5in;height:3.78125in" />

The download will provide you with two files.

1.  Template file – contains the configuration information of the VM.

2.  Parameter file – contains some of the unique parameters for the VM.
    You can modify this file to reflect changes you want to make to the
    new VM.

From the machine you wish to deploy from, install the required Azure
PowerShell Module:
```powershell
Install-Module -Name Az -Repository PSGallery -Force
```
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr>
<th>Install-Module -Name Az -Repository PSGallery -Force</th>
</tr>
</thead>
<tbody>
</tbody>
</table>

Run the following commands to connect to your Azure account:
```powershell
Connect-AzAccount
```


Run the following command to set the context to your subscription:
```powershell
Set-AzContext SubscriptionName
```

A simple PowerShell script below will create a new resource group and
deploy a VM in the resource group.
```powershell
$resourceGroupName = Read-Host -Prompt "Enter a resource group name that is used to generate resource" 

New-AzResourceGroup -Name $resourceGroupName -Location "Central US"

$templateFile = Read-Host -Prompt "Enter the template file path and file name"
$parameterFile = Read-Host -Prompt "Enter the parameter file path and file name"

New-AzResourceGroupDeployment -Name DeployLocalTemplate -ResourceGroupName $resourceGroupName -TemplateFile $templateFile -TemplateParameterFile $parameterFile -verbose

```


This will trigger the deployment of the template:

<img src=".\attachments\/media/image48.png"
style="width:6.5in;height:4.03542in" />

Once the VM is deployed, the parameters will be configured from our
parameters file:

<img src=".\attachments\/media/image49.png"
style="width:6.5in;height:5.875in" />

Your deployment is complete, and you can now validate that the VM is up
and running:

<img src=".\attachments\/media/image50.png"
style="width:6.5in;height:3.61458in" />

We navigate to the public IP Assigned and see the Edge filer **webui**
is running.

<img src=".\attachments\/media/image51.png"
style="width:6.5in;height:3.58333in" />

### Connect Edge Filers with Portal

This section explains the process to connect an Edge Filer to the
Portal.

1.  Create your portal admin account.

-   Connect to the Admin Portal and switch context to your portal
    instance. In our screen shots, our context is “Test-portal”.

-   Click New User and fill out the required fields. The ‘Role’ should
    be “Read/Write Administrator”.

<img src=".\attachments\/media/image52.png"
style="width:4.77344in;height:4.9315in" />

#### Click Save and your new user is created.

<img src=".\attachments\/media/image53.png"
style="width:6.5in;height:2.42708in" />

-   Open a new browser tab and navigate to the Services Portal this time
    and validate that your login is working as expected.

<img src=".\attachments\/media/image54.png"
style="width:5.9375in;height:3.20833in" />

1.  Connect your Edge Filer to Portal.

#### Log in to your Edge Filer instance. You will be presented with the setup up wizard. 

<img src=".\attachments\/media/image55.png"
style="width:4.92708in;height:3.96882in" />

-   Enter the Portal IP.

-   Enter the credentials of the account created in the previous step.

-   Complete the rest of the wizard and your edge filer is connected to
    the portal. You can validate that it is visible in the Portal under
    “Devices”.

<img src=".\attachments\/media/image56.png"
style="width:4.98958in;height:4.35417in" />

### **Important: Additional Considerations on Networking and Firewall Settings**

When checking for network connectivity issues where traffic goes through
a firewall, verify if the firewall is configured to ‘reject’ or ‘deny’
traffic to port **995**. A firewall with a setting of ‘reject’ traffic
might let TCP sessions be established before stopping any application
traffic after the session is created. **This can make it seem like port
995 traffic is passing through the firewall when it is not.**

## Conclusion

The integration of <u>HCP Anywhere Enterprise, HCP for Cloud Scale, and
UCP for Azure Local</u> provides organizations with a powerful,
flexible, and secure solution for file sharing and collaboration across
on-premises, cloud, and hybrid environments. By leveraging the
scalability, resilience, and performance of UCP for Azure Local,
combined with HCP Anywhere Enterprise's advanced file sharing and data
management capabilities and HCP for Cloud Scale's scalable object
storage, organizations can modernize their file services infrastructure
and enable seamless collaboration for their users.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr>
<th style="text-align: center;"><img
src=".\attachments\/media/image57.png"
style="width:5.99931in;height:2.17341in" /></th>
</tr>
</thead>
<tbody>
</tbody>
</table>

The key benefits of this integrated solution include:

-   **Increased scalability and resilience** through the use of
    hyperconverged infrastructure, global file system technologies, and
    scalable object storage

-   **Enablement of hybrid and multi-cloud strategies**, allowing
    organizations to leverage the best combinations of on-premises and
    cloud resources

-   **Enhanced data security and compliance** through local data
    storage, encryption, granular access controls, and the inherent
    security features of HCP for Cloud Scale

-   **Improved performance and user experience with local file access**,
    intelligent caching mechanisms, and the high-performance object
    storage capabilities of HCP for Cloud Scale

-   **Simplified management and control** through centralized
    administration, policy enforcement, and the unified management
    capabilities of HCP Anywhere Enterprise and HCP for Cloud Scale on
    Azure

As organizations continue to adopt hybrid and multi-cloud strategies,
the need for flexible, secure, and scalable file sharing solutions will
only grow. The integration of HCP Anywhere Enterprise, HCP for Cloud
Scale, and Azure Local represents a significant step forward in
addressing these evolving requirements, providing organizations with a
future-ready platform for file services and collaboration.

Moving forward, we can expect to see further advancements in file
sharing technologies, such as:

-   Increased use of artificial intelligence and machine learning for
    data classification, insights, and automation, leveraging the rich
    object capabilities of HCP for Cloud Scale

-   Greater integration with enterprise content management and
    collaboration platforms, facilitated by the open APIs and
    extensibility of HCP Anywhere Enterprise and HCP for Cloud Scale

-   Continued emphasis on data security, privacy, and compliance, with
    the adoption of zero-trust architectures, advanced encryption
    technologies, and the robust security features of HCP for Cloud
    Scale

-   Expansion of edge computing capabilities to support remote and
    branch office scenarios, enabled by the distributed architecture of
    HCP Anywhere Enterprise and the geo-dispersed replication
    capabilities of HCP for Cloud Scale

-   Seamless interoperability and data portability across multiple cloud
    platforms and services, supported by the S3 compatibility and
    multi-cloud integration capabilities of HCP for Cloud Scale

As these trends unfold, the combination of HCP Anywhere Enterprise, HCP
for Cloud Scale, and UCP for UCP for Azure Local will be well-positioned
to help organizations navigate the complexities of the hybrid cloud
landscape and deliver a modern, agile, and secure file sharing
experience to their users.

Given the compelling benefits and future-ready capabilities of the HCP
Anywhere Enterprise, HCP for Cloud Scale, and UCP for Azure Local
integration, organizations should strongly consider adopting this
solution to meet their evolving file sharing and collaboration needs. By
embracing this integrated approach, organizations can:

-   Modernize their file services infrastructure and enable seamless
    collaboration across on-premises, cloud, and hybrid environments

-   Address the complex security, compliance, and data sovereignty
    requirements of their industry and region, leveraging the advanced
    security and compliance features of HCP for Cloud Scale

-   Simplify the management and control of their file sharing
    environment, reducing operational complexity and costs through the
    unified management capabilities of HCP Anywhere Enterprise and HCP
    for Cloud Scale

-   Ensure the scalability, resilience, and performance of their file
    services, supporting the needs of their users and business with the
    scalable object storage capabilities of HCP for Cloud Scale

-   Position themselves for success in the era of hybrid and multi-cloud
    computing, with a flexible and adaptable platform for file sharing
    and collaboration that leverages the best of on-premises
    infrastructure and cloud services

To get started, organizations should assess their current file sharing
infrastructure, identify key challenges and requirements, and engage
with HCP Anywhere Enterprise, HCP for Cloud Scale, and UCP for Azure
Local to develop a tailored implementation plan. By taking a proactive
and strategic approach to modernizing their file services, organizations
can lay the foundation for a more agile, secure, and collaborative
future, powered by the advanced capabilities, validated by Hitachi UCP’s
Engineering and Product Management teams.
