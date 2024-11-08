
# Configure virtual machines

# Introduction

Azure Virtual Machines enables you to create on-demand, scalable computing resources. Azure Architects commonly use virtual machines to gain greater control over the computing environment.

Your company is doing consumer research, and your team manages the on-premises servers. The servers you administer run the entire company infrastructure from web servers to databases. However, the hardware is aging and starting to struggle to keep up with some of the new data analysis applications being deployed. Rather than upgrade the hardware, the company decided to deploy Azure virtual machines. You're responsible for deploying the new virtual machines. Your deployment tasks include correctly sizing the machines, selecting storage, and configuring networking.

In this module, you learn how to configure virtual machine names and locations. You examine virtual machine pricing models and discover how to determine the correct virtual machine size. You learn how to configure virtual machine storage, and how to create a virtual machine in the Azure portal. You select a secure virtual machine connection method, and how to configure Windows and Linux virtual machine connections.

The goal of this module is to learn how to configure and manage virtual machines in Azure.

## Learning objectives

In this module, you learn how to:

- Determine the responsibilities of cloud service providers and customers in a cloud computing environment.
- Identify the key considerations and factors involved in planning for virtual machines. Considerations include workload requirements, resource allocation, and secure access.
- Configure virtual machine storage and virtual machine sizing.
- Create a virtual machine in the Azure portal.
- Practice deploying an Azure virtual machine and verify the configuration.

## Skills measured

The content in the module helps you prepare for [Exam AZ-104: Microsoft Azure Administrator](https://learn.microsoft.com/en-us/credentials/certifications/exams/az-104/).

## Prerequisites

- Cloud computing concepts. Familiarity with Infrastructure as a Service (IaaS), virtualization, and resource provisioning in a cloud environment.
    
- Azure fundamentals. Understanding of basic Azure concepts, including Azure subscriptions, resource groups, and storage accounts.
    
- Networking fundamentals. Knowledge of basic networking concepts, including IP addressing, virtual networks, and subnets.
    
- Azure portal. Ability to create and configure resources in the Azure portal.

# Review cloud services responsibilities

The primary advantage of working with virtual machines is to have more control over installed software and configuration settings. Azure Virtual Machines supports more granular control than other Azure services, such as Azure App Service or Azure Cloud Services.

### Things to know about Azure Virtual Machines

Consider the following characteristics of Azure Virtual Machines.

- Azure Virtual Machines is the basis of the Azure infrastructure as a service (IaaS) model. IaaS is an instant computing infrastructure, provisioned and managed over the internet.
    
- A virtual machine provides its own operating system, storage, and networking capabilities, and can run a wide range of applications.
    
- You can implement multiple virtual machines, and configure each machine with different software and settings to support separate operation scenarios, such as development, testing, and deployment.
    
- You can use virtual machines to quickly scale up and down with demand and pay only for what you use.
    
- The responsibilities associated with configuring and maintaining virtual machines is shared between Microsoft and the customer. The following chart shows how the responsibilities are handled across the IaaS (virtual machines), PaaS, SaaS, and on-premises offerings.
    
    ![Diagram of the shared responsibility areas for IaaS, PaaS, SaaS, and on-premises offerings.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-virtual-machines/media/responsibility-layers-4ffbf946.png)
    

### Things to consider when using IaaS and virtual machines

Let's look at some scenarios for working with IaaS and virtual machines. Think about how you can implement virtual machines in Azure.

- **Consider test and development**. Teams can quickly set up and dismantle test and development environments, bringing new applications to market faster. IaaS and virtual machines make it quick and economical to scale up dev-test environments up and down.
    
- **Consider website hosting**. Running websites by using IaaS and virtual machines can be less expensive than traditional web hosting.
    
- **Consider storage, backup, and recovery**. Virtual machines let organizations avoid the expense for storage and complexity of storage management. Recovery typically requires a skilled staff to manage data and meet legal and compliance requirements. IaaS is useful for handling unpredictable demand and steadily growing storage needs. You can simplify planning and management of backup and recovery systems.
    
- **Consider high-performance computing**. Virtual machines enable high-performance computing (HPC) on supercomputers, computer grids, or computer clusters. HPC helps solve complex problems involving millions of variables or calculations. You can support scenarios such as earthquake and protein folding simulations, climate and weather predictions, financial modeling, and evaluating product designs.
    
- **Consider big data analysis**. Big data is a popular term for massive data sets that contain potentially valuable patterns, trends, and associations. Mining data sets to locate or tease out these hidden patterns requires a huge amount of processing power, which IaaS economically provides.
    
- **Consider extended datacenters**. Add capacity to your datacenter by adding virtual machines in Azure. Avoid the costs of physically adding hardware or space to your physical location. Connect your physical network to the Azure cloud network seamlessly.

# Plan virtual machines

Before you create an Azure virtual machine, it's helpful to make a plan for the machine configuration. You need to consider your preferences for several options, including the machine size and location, storage usage, and associated costs.

### Things to know about configuring virtual machines

Let's walk through a checklist of things you need to consider when configuring a virtual machine.

- Start with the network.
- Choose a name for the virtual machine.
- Decide the location for the virtual machine.
- Determine the size of the virtual machine.
- Review the pricing model and estimate your costs.
- Identify which Azure Storage to use with the virtual machine.
- Select an operating system for the virtual machine.

#### Network configuration

Virtual networks are used in Azure to provide private connectivity between Azure Virtual Machines and other Azure services. Virtual machines and services that are part of the same virtual network can access one another. By default, services outside the virtual network can't connect to services within the virtual network. You can, however, configure the network to allow access to the external service, including your on-premises servers.

Network addresses and subnets aren't trivial to change after configuration. If you plan to connect your private company network to the Azure services, make sure you consider the topology before you put any virtual machines into place.

#### Virtual machine name

The virtual machine name is used as the computer name, which is configured as part of the operating system. You can specify a name with up to 15 characters on a Windows virtual machine and 64 characters on a Linux virtual machine.

The virtual machine name also defines a manageable Azure resource, and it's not trivial to change later. You should choose names that are meaningful and consistent, so you can easily identify what the virtual machine does. A good convention uses several of the following elements in the machine name:

Expand table

|Name element|Examples|Description|
|---|---|---|
|**Environment or purpose**|`dev` (development), `prod` (production), `QA` (testing)|A portion of the name should identify the environment or purpose for the machine.|
|**Location**|`uw` (US West), `je` (Japan East), `ne` (North Europe)|Another portion of the name should specify the region where the machine is deployed.|
|**Instance**|`1`, `02`, `005`|For multiple machines that have similar names, include an instance number in the name to differentiate the machines in the same category.|
|**Product or service**|`Outlook`, `SQL`, `AzureAD`|A portion of the name can specify the product, application, or service that the machine supports.|
|**Role**|`security`, `web`, `messaging`|A portion of the name can specify what role the machine supports within the organization.|

Let's consider how to name the first development web server for your company, hosted in the US South Central location. In this scenario, you might use the machine name `devusc-webvm01`. `dev` stands for development and `usc` identifies the location. `web` indicates the machine as a web server, and the suffix `01` shows the machine is the first in the configuration.

#### Virtual machine location

Azure has datacenters all over the world filled with servers and disks. These datacenters are grouped into geographic regions like West US, North Europe, Southeast Asia, and so on. The datacenters provide redundancy and availability.

Each virtual machine is in a region where you want the resources like CPU and storage to be allocated. The regional location lets you place your virtual machines as close as possible to your users. The location of the machine can improve performance and ensure you meet any legal, compliance, or tax requirements.

There are two other points to consider about the virtual machine location.

- The machine location can limit your available options. Each region has different hardware available, and some configurations aren't available in all regions.
    
- There are price differences between locations. To find the most cost-effective choice, check for your required configuration in different regions.
    

#### Virtual machine size

Azure offers different memory and storage options for different [virtual machine sizes](https://learn.microsoft.com/en-us/azure/virtual-machines/sizes). The best way to determine the appropriate machine size is to consider the type of workload your machine needs to run. Based on the workload, you can choose from a subset of available virtual machine sizes.

#### Azure Storage

[Azure Managed Disks](https://learn.microsoft.com/en-us/azure/virtual-machines/managed-disks-overview) handle Azure storage account creation and management in the background for you. You specify the disk size and the performance tier (Standard or Premium). Azure creates and manages the disk. As you add disks or scale the virtual machine up and down, you don't have to worry about the storage being used.

#### Virtual machine pricing options

A subscription is billed two separate costs for every virtual machine: _compute_ and _storage_. By separating these costs, you can scale them independently and only pay for what you need.

- **Compute expenses** are priced on a per-hour basis but billed on a per-minute basis. If the virtual machine is deployed for 55 minutes, Azure charges you for only 55 minutes of usage. Azure doesn't charge for compute capacity if you stop and deallocate the virtual machine. The [hourly price](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) varies based on the virtual machine size and operating system you select. For the compute costs, you're able to choose from two payment options:
    
    - **Consumption-based**: With the consumption-based option, you pay for compute capacity by the second. You're able to increase or decrease compute capacity on demand and start or stop at any time. Use consumption-based pricing if you run applications with short-term or unpredictable workloads that can't be interrupted. An example scenario is if you're doing a quick test or developing an app in a virtual machine.
        
    - **Reserved Virtual Machine Instances**: The Reserved Virtual Machine Instances (RI) option is an advance purchase of a virtual machine for one or three years in a specified region. The commitment is made up front, and in return, you get up to 72% price savings compared to pay-as-you-go pricing. RIs are flexible and can easily be exchanged or returned for an early termination fee. Use this option if the virtual machine has to run continuously, or you need budget predictability, and you can commit to using the virtual machine for at least a year.
        
- **Storage costs** are charged separately for the Azure Storage used by the virtual machine. The status of the virtual machine has no relation to the Azure Storage charges that are incurred. Azure always charges you for any Azure Storage used by the disks.
    

#### Operating system

Azure provides various operating system images that you can install into the virtual machine, including several versions of Windows and flavors of Linux. Azure bundles the cost of the operating system license into the price.

- If you're looking for more than just base operating system images, you can search [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/compute). There are various install images that include not only the operating system but popular software tools, such as WordPress. The image stack consists of a Linux server, Apache web server, a MySQL database, and PHP. Instead of setting up and configuring each component, you can install an Azure Marketplace image and get the entire stack all at once.
    
- If you don't find a suitable operating system image, you can create your own disk image. Your disk image can be uploaded to Azure Storage and used to create an Azure virtual machine. Keep in mind that Azure only supports 64-bit operating systems.

# Determine virtual machine sizing

Rather than specify processing power, memory, and storage capacity independently, Azure provides different virtual machine sizes that offer variations of these elements in different size configurations. Azure provides a wide range of virtual machine size options that allow you to select the appropriate mix of compute, memory, and storage for your needs.

### Things to know about virtual machine sizes

The best way to determine the appropriate virtual machine size is to consider the type of workload your virtual machine needs to run. Based on the workload, you can choose from a subset of available virtual machine sizes.

The following table shows size classifications for Azure Virtual Machines workloads and recommended usage scenarios.

Expand table

|Classification|Description|Scenarios|
|---|---|---|
|**General purpose**|General-purpose virtual machines are designed to have a balanced CPU-to-memory ratio.|- Testing and development  <br>- Small to medium databases  <br>- Low to medium traffic web servers|
|**Compute optimized**|Compute optimized virtual machines are designed to have a high CPU-to-memory ratio.|- Medium traffic web servers  <br>- Network appliances  <br>- Batch processes  <br>- Application servers|
|**Memory optimized**|Memory optimized virtual machines are designed to have a high memory-to-CPU ratio.|- Relational database servers  <br>- Medium to large caches  <br>- In-memory analytics|
|**Storage optimized**|Storage optimized virtual machines are designed to have high disk throughput and I/O.|- Big Data  <br>- SQL and NoSQL databases  <br>- Data warehousing  <br>- Large transactional databases|
|**GPU**|GPU virtual machines are specialized virtual machines targeted for heavy graphics rendering and video editing. Available with single or multiple GPUs.|- Model training  <br>- Inferencing with deep learning|
|**High performance computes**|High performance compute offers the fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).|- Workloads that require fast performance  <br>- High traffic networks|

#### Resizing virtual machines

Azure allows you to change the virtual machine size when the existing size no longer meets your needs. You can resize a virtual machine if your current hardware configuration is allowed in the new size. This option provides a fully agile and elastic approach to virtual machine management.

When you stop and deallocate the virtual machine, you can select any size available in your region.

 Important

Be cautious when resizing production virtual machines. Resizing a machine might require a restart that can cause a temporary outage or change configuration settings such as the IP address.

# Determine virtual machine storage

Just like any other computer, virtual machines in Azure use disks as a place to store the operating system, applications, and data.

### Things to know about virtual machine storage and disks

All Azure virtual machines have at least two disks: an operating system disk and a temporary disk. Virtual machines can also have one or more data disks. All disks are stored as virtual hard disks (VHDs). A VHD is like a physical disk in an on-premises server but, virtualized.

![Diagram that shows disks used by an Azure virtual machine, including disks for the OS, data, and temporary storage.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-virtual-machines/media/virtual-machine-disks-ff57089c.png)

#### Operating system disk

Every virtual machine has one attached operating system disk. The OS disk has a preinstalled operating system, which is selected when the virtual machine is created. The OS disk is registered as a SATA drive (Serial Advanced Technology Attachment) and labeled as the `C:` drive by default.

#### Temporary disk

Data on a temporary disk might be lost during a maintenance event or when you redeploy a virtual machine. During a standard reboot of the virtual machine, the data on the temporary drive should persist. However, there are cases where the data might not persist, such as moving to a new host. Therefore, any data on the temporary drive shouldn't be data that's critical to the system.

- On Windows virtual machines, the temporary disk is labeled as the `D:` drive by default. This drive is used for storing the **pagefile.sys** file.
- On Linux virtual machines, the temporary disk is typically `/dev/sdb`. Azure Linux Agent formats this disk and mounts it to `/mnt`.

 Important

Don't store data on the temporary disk. This disk provides temporary storage for applications and processes and is intended to only store data like page or swap files.

#### Data disks

A data disk is a managed disk attached to a virtual machine to store application data or other data you need to keep. Data disks are registered as SCSI drives and are labeled with a letter you choose. The size of a virtual machine determines how many data disks you can attach and the type of storage you can use to host the data disks.

### Things to consider when choosing storage for your virtual machines

Review the following considerations about using Azure Storage and Azure Managed Disks with your virtual machines.

- **Consider Azure Premium Storage**. You can choose Premium Storage to gain high-performance, low-latency disk support for your virtual machines with input/output (I/O)-intensive workloads. Virtual machine disks that use Premium Storage store data on solid-state drives (SSDs). To take advantage of the speed and performance of premium storage disks, you can migrate existing virtual machine disks to Premium Storage.
    
- **Consider multiple Storage disks**. In Azure, you can attach several Premium Storage disks to a virtual machine. Using multiple disks gives your applications up to 256 TB of storage per virtual machine. With Premium Storage, your applications can achieve 80,000 I/O operations per second (IOPS) per virtual machine, and a disk throughput of up to 2,000 megabytes per second (MB/s) per virtual machine. Read operations completed with Premium Storage yield low latencies.
    
- **Consider managed disks**. An Azure-managed disk is a VHD. Azure-managed disks are stored as page blobs, which are a random IO storage object in Azure. The disk is described as _managed_ because it's an abstraction over page blobs, blob containers, and Azure storage accounts. With managed disks, you provision the disk, and Azure takes care of the rest. When you choose to use Azure-managed disks with your workloads, Azure creates and manages the disk for you. The available types of disks are Ultra Solid State Drives (SSD), Premium SSD, Standard SSD, and Standard Hard Disk Drives (HDD).
    
     Note
    
    Managed disks are required for the single instance virtual machine SLA.
    
- **Consider migrating to Premium Storage**. For the best performance for your application, we recommend that you migrate any virtual machine disk that requires high IOPS to Premium Storage. If your disk doesn't require high IOPS, you can help limit costs by keeping it in standard Azure Storage.

# Create virtual machines in the Azure portal

When you create virtual machines in the Azure portal, one of your first decisions is to specify which image to use. Azure supports Windows and Linux operating systems, and there are server and client platforms to choose from. You can also search Azure Marketplace for other supported images:

![Screenshot that shows disk images for virtual machines in Azure Marketplace.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-virtual-machines/media/server-versions-b93232ca.png)

## Configure virtual machine image

The Azure portal guides you through the configuration process to create your virtual machine image. The process includes configuring basic and advanced options, and specifying details about the disks, virtual networks, and machine management.

![Screenshot that shows the UI for creating a virtual machine in the Azure portal.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-virtual-machines/media/create-virtual-machines-a75605ba.png)

- The **Basics** tab contains the project details, administrator account, and inbound port rules.
    
- On the **Disks** tab, you select the OS disk type and specify your data disks.
    
- The **Networking** tab provides settings to create virtual networks and load balancing.
    
- On the **Management** tab, you can enable automatic shutdown and specify backup details.
    
- On the **Advanced** tab, you can configure agents, scripts, or virtual machine extensions.
    
- Other settings are available on the **Monitoring** and **Tags** tabs.
    

### Learn how to reduce costs when creating your virtual machine

![](https://youtu.be/n9QRCdCNtG0)


# Connect to virtual machines

There are several ways to access your Azure virtual machines. The Azure portal supports options for connecting your Windows and Linux machines, and making connections by using Azure Bastion. The following diagram shows how you can connect Azure virtual machines with the SSH and RDP protocols, Cloud Shell, and Azure Bastion.

![Diagram that shows virtual machine access with the SSH and RDP protocols, Cloud Shell, and Azure Bastion.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-virtual-machines/media/bastion-connections-29c60c68.png)

### Things to know about connecting with Azure Bastion

The Azure Bastion service is a fully platform-managed PaaS service. Azure Bastion provides secure and seamless RDP/SSH connectivity to your virtual machines directly over SSL. When you connect via Azure Bastion, your virtual machines don't need a public IP address. The following example shows a virtual machine connection with Azure Bastion in the Azure portal.

![](https://youtu.be/epWKTGGa_wY)  

Azure Bastion provides secure RDP and SSH connectivity to all virtual machines in the virtual network. Azure Bastion protects your virtual machines from exposing RDP/SSH ports to the outside world while still providing secure access with RDP/SSH. Azure Bastion lets you connect to the virtual machine directly from the Azure portal. You aren't a client, agent, or another piece of software.

### Things to know about connecting Windows-based virtual machines

To connect to a Windows-based virtual machine hosted on Azure, use the Microsoft Remote Desktop application with the remote desktop protocol (RDP). The Remote Desktop app provides a graphical user interface (GUI) session to an Azure virtual machine that runs any supported version of Windows. The following image shows how to use the RDP protocol to connect to a Windows-based virtual machine in the Azure portal.

![Screenshot that shows how to use the RDP protocol to connect to a Windows-based virtual machine in the Azure portal.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-virtual-machines/media/rdp-connect.png)

To create an RDP connection, you specify the IP address for the virtual machine. As an option, you can select the port to use for the connection. The system provides you with a downloadable RDP file to use for the connection.

### Things to know about connecting Linux-based virtual machines

To connect to a Linux-based virtual machine, you can use a secure shell protocol (SSH) client. SSH is an encrypted connection protocol that allows secure sign-ins over unsecured connections. Depending on your organization's security policies, you can reuse a single public-private key pair to access multiple Azure virtual machines and services. You don't need a separate pair of keys for each virtual machine or service you wish to access. The following image shows how to use the SSH protocol to connect to a Linux-based virtual machine in the Azure portal.

![Screenshot that shows how to use the SSH protocol to connect to a Linux-based virtual machine in the Azure portal.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-virtual-machines/media/connect-ssh.png)

- The **public key** is placed on your Linux virtual machine, or any other service that you wish to use with public-key cryptography.
- The **private key** remains on your local system.

 Important

**Protect your private key**. Don't share your private key. Your public key can be shared with anyone, but only you (or your local security infrastructure) should possess your private key.

# Interactive lab simulation

## Lab scenario

Your organization is planning on using virtual machines in Azure. As the Azure Administrator you need to:

- Be able to use virtual machine Quickstart templates.
- Use templates to create and configure virtual machines.
- Be able to monitor virtual machine activity.

## Objectives

- **Task 1**: Use the Azure Quickstart Template gallery to deploy a virtual machine.
    - Browse to the [Azure Quickstart Template gallery](https://azure.microsoft.com/resources/templates/).
    - Search for a template that deploys a simple Windows Server virtual machine.
    - Edit the template and customize the parameters and variables.
    - Deploy the template to create the virtual machine.
- **Task 2**: Verify and monitor your virtual machine.
    - In the portal, locate your new virtual machine.
    - View monitoring data for CPU, network, and data usage.
    - View activity log information.

 Note

Click on the thumbnail image to start the lab simulation. When you're done, be sure to return to this page so you can continue learning.

[![Screenshot of the simulation page.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-virtual-machines/media/simulation-create-virtual-machine.png)](https://mslearn.cloudguides.com/en-us/guides/AZ-900%20Exam%20Guide%20-%20Azure%20Fundamentals%20Exercise%209)

---

