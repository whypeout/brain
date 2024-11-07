
# Configure virtual networks

# Introduction

Azure virtual networks are an essential component for creating private networks in Azure. They allow different Azure resources to securely communicate with each other, the internet, and on-premises networks.

Suppose you work for a company in the healthcare industry. Your company is looking to migrate their on-premises infrastructure to Azure. They want to ensure secure communication between their resources in Azure and their on-premises network. The company is also concerned about scalability and availability. By using Azure virtual networks, they can create a private network in Azure and securely connect their resources.

The topics covered in this module include subnetting, creating virtual networks, and using private and public IP addresses. You also learn about the different scenarios where virtual networks can be used, such as creating a dedicated private cloud-only network or extending a data center securely. The module provides a detailed explanation of subnets and their benefits, and how to plan IP addressing for Azure resources.

By the end of this module, you have a clear understanding of how to create and configure virtual networks in Azure. You're able to effectively use subnets, assign IP addresses, and ensure secure communication between your Azure resources and on-premises network.

## Learning objectives

In this module, you learn how to:

- Describe Azure virtual network features and components.
- Identify features and usage cases for subnets and subnetting.
- Identify usage cases for private and public IP addresses.
- Create a virtual network and assign an IP address.

## Skills measured

The content in the module helps you prepare for [Exam AZ-104: Microsoft Azure Administrator](https://learn.microsoft.com/en-us/certifications/exams/az-104).

## Prerequisites

- Basic knowledge of virtual networking in cloud environments.
- Familiarity with IP address formats and subnetting.

# Plan virtual networks

A major incentive for adopting cloud solutions like Azure is to enable information technology departments to transition server resources to the cloud. Moving resources to the cloud can save money and simplify administrative operations. Relocating resources removes the need to maintain expensive datacenters with uninterruptible power supplies, generators, multiple fail-safes, or clustered database servers. For small and medium-sized companies, which might not have the expertise to maintain their own robust infrastructure, moving to the cloud is particularly appealing.

After resources are moved to Azure, they require the same networking functionality as an on-premises deployment. In specific scenarios, the resources require some level of network isolation. Azure network services offer a range of components with functionalities and capabilities, as shown in the following image:

![Screenshot that shows the main components of Azure network services.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-virtual-networks/media/network-components-66dff480.png)

### Things to know about Azure virtual networks

You can implement Azure Virtual Network to create a virtual representation of your network in the cloud. Let's examine some characteristics of virtual networks in Azure.

- An Azure virtual network is a logical isolation of the Azure cloud resources.
    
- You can use virtual networks to provision and manage virtual private networks (VPNs) in Azure.
    
- Each virtual network has its own Classless Inter-Domain Routing (CIDR) block and can be linked to other virtual networks and on-premises networks.
    
- You can link virtual networks with an on-premises IT infrastructure to create hybrid or cross-premises solutions, when the CIDR blocks of the connecting networks don't overlap.
    
- You control the DNS server settings for virtual networks, and segmentation of the virtual network into subnets.
    

The following illustration depicts a virtual network that has a subnet containing two virtual machines. The virtual network has connections to an on-premises infrastructure and a separate virtual network.

![Diagram of a virtual network with a subnet of two virtual machines. The network connects to an on-premises infrastructure and separate virtual network.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-virtual-networks/media/virtual-networks-c016972b.png)

### Things to consider when using virtual networks

Virtual networks can be used in many ways. As you think about the configuration plan for your virtual networks and subnets, consider the following scenarios.

Expand table

|Scenario|Description|
|---|---|
|_Create a dedicated private cloud-only virtual network_|Sometimes you don't require a cross-premises configuration for your solution. When you create a virtual network, your services and virtual machines within your virtual network can communicate directly and securely with each other in the cloud. You can still configure endpoint connections for the virtual machines and services that require internet communication, as part of your solution.|
|_Securely extend your data center with virtual networks_|You can build traditional site-to-site VPNs to securely scale your datacenter capacity. Site-to-site VPNs use IPSEC to provide a secure connection between your corporate VPN gateway and Azure.|
|_Enable hybrid cloud scenarios_|Virtual networks give you the flexibility to support a range of hybrid cloud scenarios. You can securely connect cloud-based applications to any type of on-premises system, such as mainframes and Unix systems.|

# Create subnets


Subnets provide a way for you to implement logical divisions within your virtual network. Your network can be segmented into subnets to help improve security, increase performance, and make it easier to manage.

### Things to know about subnets

There are certain conditions for the IP addresses in a virtual network when you apply segmentation with subnets.

- Each subnet contains a range of IP addresses that fall within the virtual network address space.
    
- The address range for a subnet must be unique within the address space for the virtual network.
    
- The range for one subnet can't overlap with other subnet IP address ranges in the same virtual network.
    
- The IP address space for a subnet must be specified by using CIDR notation.
    
- You can segment a virtual network into one or more subnets in the Azure portal. Characteristics about the IP addresses for the subnets are listed.
    
    ![Screenshot that shows multiple subnets for a virtual network in the Azure portal.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-virtual-networks/media/azure-subnets-a5c893d5.png)
    

#### Reserved addresses

For each subnet, Azure reserves five IP addresses. The first four addresses and the last address are reserved.

Let's examine the reserved addresses in an IP address range of `192.168.1.0/24`.

Expand table

|Reserved address|Reason|
|---|---|
|`192.168.1.0`|This value identifies the virtual network address.|
|`192.168.1.1`|Azure configures this address as the default gateway.|
|`192.168.1.2` _and_ `192.168.1.3`|Azure maps these Azure DNS IP addresses to the virtual network space.|
|`192.168.1.255`|This value supplies the virtual network broadcast address.|

### Things to consider when using subnets

When you plan for adding subnet segments within your virtual network, there are several factors to consider. Review the following scenarios.

- **Consider service requirements**. Each service directly deployed into a virtual network has specific requirements for routing and the types of traffic that must be allowed into and out of associated subnets. A service might require or create their own subnet. There must be enough unallocated space to meet the service requirements. Suppose you connect a virtual network to an on-premises network by using Azure VPN Gateway. The virtual network must have a dedicated subnet for the gateway.
    
- **Consider network virtual appliances**. Azure routes network traffic between all subnets in a virtual network, by default. You can override Azure's default routing to prevent Azure routing between subnets. You can also override the default to route traffic between subnets through a network virtual appliance. If you require traffic between resources in the same virtual network to flow through a network virtual appliance, deploy the resources to different subnets.
    
- **Consider service endpoints**. You can limit access to Azure resources like an Azure storage account or Azure SQL database to specific subnets with a virtual network service endpoint. You can also deny access to the resources from the internet. You might create multiple subnets, and then enable a service endpoint for some subnets, but not others.
    
- **Consider network security groups**. You can associate zero or one network security group to each subnet in a virtual network. You can associate the same or a different network security group to each subnet. Each network security group contains rules that allow or deny traffic to and from sources and destinations.
    
- **Consider private links**. Azure Private Link provides private connectivity from a virtual network to Azure platform as a service (PaaS), customer-owned, or Microsoft partner services. Private Link simplifies the network architecture and secures the connection between endpoints in Azure. The service eliminates data exposure to the public internet.

# Create virtual networks

You can create new virtual networks at any time. You can also add virtual networks when you create a virtual machine.

### Things to know about creating virtual networks

Review the following requirements for creating a virtual network.

- When you create a virtual network, you need to define the IP address space for the network.
    
- Plan to use an IP address space that's not already in use in your organization.
    
    - The address space for the network can be either on-premises or in the cloud, but not both.
        
    - Once you create the IP address space, it can't be changed. If you plan your address space for cloud-only virtual networks, you might later decide to connect an on-premises site.
        
- To create a virtual network, you need to define at least one subnet.
    
    - Each subnet contains a range of IP addresses that fall within the virtual network address space.
        
    - The address range for each subnet must be unique within the address space for the virtual network.
        
    - The range for one subnet can't overlap with other subnet IP address ranges in the same virtual network.
        
- You can create a virtual network in the Azure portal. Provide the Azure subscription, resource group, virtual network name, and service region for the network.
    
    ![Screenshot that shows how to create a virtual network in the Azure portal.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-virtual-networks/media/create-virtual-networks-b4f1fd40.png)
    

 Note

Default limits on Azure networking resources can change periodically. Be sure to consult the [Azure networking documentation](https://learn.microsoft.com/en-us/azure/networking/) for the latest information.

# Plan IP addressing

You can assign IP addresses to Azure resources to communicate with other Azure resources, your on-premises network, and the internet. There are two types of Azure IP addresses: _private_ and _public_.

**Private IP addresses** enable communication within an Azure virtual network and your on-premises network. You create a private IP address for your resource when you use a VPN gateway or Azure ExpressRoute circuit to extend your network to Azure.

**Public IP addresses** allow your resource to communicate with the internet. You can create a public IP address to connect with Azure public-facing services.

The following illustration shows a virtual machine resource that has a private IP address and a public IP address.

![Illustration of a resource with a private IP address and a public IP address.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-virtual-networks/media/ip-addressing-54476e47.png)

### Things to know about IP addresses

Let's take a closer look at the characteristics of IP addresses.

- IP addresses can be statically assigned or dynamically assigned.
    
- You can separate dynamically and statically assigned IP resources into different subnets.
    
- Static IP addresses don't change and are best for certain situations, such as:
    
    - DNS name resolution, where a change in the IP address requires updating host records.
    - IP address-based security models that require apps or services to have a static IP address.
    - TLS/SSL certificates linked to an IP address.
    - Firewall rules that allow or deny traffic by using IP address ranges.
    - Role-based virtual machines such as Domain Controllers and DNS servers.


# Create public IP addressing

You can create a public IP address for your resource in the Azure portal.

![Screenshot that shows how to create a public IP address in the Azure portal.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-virtual-networks/media/create-public-ip-address-f07bd67d.png)

### Things to consider when creating a public IP address

To create a public IP address, configure the following settings:

- **IP Version**: Select to create an **IPv4** or **IPv6** address, or **Both** addresses.
    
- **SKU**: Select the SKU for the public IP address, including **Basic** or **Standard**. The value must match the SKU of the Azure load balancer with which the address is used.
    
- **Name**: Enter a name to identify the IP address. The name must be unique within the resource group you select.
    
- **IP address assignment**: Identify the type of IP address assignment to use.
    
    - **Dynamic** addresses are assigned after a public IP address is associated to an Azure resource and is started for the first time. Dynamic addresses can change if a resource such as a virtual machine is stopped (deallocated) and then restarted through Azure. The address remains the same if a virtual machine is rebooted or stopped from within the guest OS. When a public IP address resource is removed from a resource, the dynamic address is released.
        
    - **Static** addresses are assigned when a public IP address is created. Static addresses aren't released until a public IP address resource is deleted. If the address isn't associated to a resource, you can change the assignment method after the address is created. If the address is associated to a resource, you might not be able to change the assignment method.
        

 Note

If you select **IPv6** for the IP version, the assignment method must be **Dynamic** for the Basic SKU. Standard SKU addresses are **Static** for both IPv4 and IPv6 addresses.

# Associate public IP addresses

A public IP address resource can be associated with virtual machine network interfaces, internet-facing load balancers, VPN gateways, and application gateways. You can associate your resource with both dynamic and static public IP addresses.

### Things to consider when associating public IP addresses

The following table summarizes how you can associate public IP addresses for different types of resources.

Expand table

|Resource|Public IP address association|Dynamic IP address|Static IP address|
|---|---|---|---|
|Virtual machine|NIC|Yes|Yes|
|Load balancer|Front-end configuration|Yes|Yes|
|VPN gateway|VPN gateway IP configuration|Yes|Yes *****|
|Application gateway|Front-end configuration|Yes|Yes *****|

***** Static IP addresses are available on certain SKUs only.

#### Public IP address SKUs

When you create a public IP address, you select the Basic or Standard SKU. Your SKU choice affects the IP assignment method, security, available resources, and redundancy options.

The following table summarizes the differences between the SKU types for public IP addresses.

Expand table

|Feature|Basic SKU|Standard SKU|
|---|---|---|
|IP assignment|Static or Dynamic|Static|
|Security|Open by default|Secure by default, closed to inbound traffic|
|Resources|Network interfaces, VPN gateways, Application gateways, and internet-facing load balancers|Network interfaces or public standard load balancers|
|Redundancy|Not zone redundant|Zone redundant by default|

# Allocate or assign private IP addresses


A private IP address resource can be associated with virtual machine network interfaces, internal load balancers, and application gateways. Azure can provide an IP address (dynamic assignment) or you can assign the IP address (static assignment).

### Things to consider when associating private IP addresses

The following table summarizes how you can associate private IP addresses for different types of resources.

Expand table

|Resource|Private IP address association|Dynamic IP address|Static IP address|
|---|---|---|---|
|Virtual machine|NIC|Yes|Yes|
|Internal load balancer|Front-end configuration|Yes|Yes|
|Application gateway|Front-end configuration|Yes|Yes|

#### Private IP address assignment

A private IP address is allocated from the address range of the virtual network subnet that a resource is deployed in. There are two options: dynamic and static.

- **Dynamic**: Azure assigns the next available unassigned or unreserved IP address in the subnet's address range. Dynamic assignment is the default allocation method.
    
    Suppose addresses 10.0.0.4 through 10.0.0.9 are already assigned to other resources. In this case, Azure assigns the address 10.0.0.10 to a new resource.
    
- **Static**: You select and assign any unassigned or unreserved IP address in the subnet's address range.
    
    Suppose a subnet's address range is 10.0.0.0/16, and addresses 10.0.0.4 through 10.0.0.9 are already assigned to other resources. In this scenario, you can assign any address between 10.0.0.10 and 10.0.255.254.

# Interactive lab simulation

## Lab scenario

Your organization is migrating network infrastructure and virtual machines to Azure. As the Azure Administrator you need to:

- Configure Azure virtual networks and subnets.
- Connect remotely to Azure virtual machines by using RDP.
- Verify virtual machines in the same virtual network can communicate.

## Architecture diagram

![Diagram of the architecture as explained in the text.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-virtual-networks/media/create-network-architecture.png)

## Objectives

- **Task 1**: Create a virtual network.
    - Create a virtual network, **vnet1**, with an IP address space of 10.1.0.0/16.
    - Create a subnet, **default**, with an IP address space of 10.1.0.0/24.
- **Task 2**: Create two virtual machines.
    - Create a virtual machine, **vm1**, in **vnet1** and allow inbound RDP.
    - Create a second virtual machine, **vm2**, in **vnet1** and allow inbound RDP.
    - Ensure both virtual machines are deployed and running before continuing.
- **Task 3**: Test the virtual machine connections.
    - Connect to **vm1** with RDP.
    - Connect to **vm2** with RDP.
    - Disable the public and private Windows Firewall on both virtual machines.
    - Use Azure PowerShell to confirm **vm1** can ping **vm2**.

 Note

Select the thumbnail image to start the lab simulation. When you're done, be sure to return to this page so you can continue learning.

[![Screenshot of the simulation page.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-virtual-networks/media/simulation-create-networks.png)](https://mslearn.cloudguides.com/en-us/guides/AZ-900%20Exam%20Guide%20-%20Azure%20Fundamentals%20Exercise%204)

# Summary and resources

In this module, you learned about Azure virtual networks and their importance in creating private networks in Azure. You explored the benefits of using virtual networks, such as scalability, availability, and isolation. You learned how to create virtual networks with subnetting and how to determine which resources require public or private IP addresses.

The main takeaways from this module are:

- Azure virtual networks allow different Azure resources to securely communicate with each other, the internet, and on-premises networks.
    
- Subnets within virtual networks provide logical divisions, improving security, performance, and management.
    
- When creating virtual networks, ensure that the IP address space is unique and doesn't overlap with other subnets.
    
- IP addresses can provide public or private access to resources.
    

## Learn more with documentation

- [What is Azure Virtual Network?](https://learn.microsoft.com/en-us/azure/virtual-network/virtual-networks-overview). This article is your starting point to learn about virtual networks.
    
- [Public IP addresses](https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/public-ip-addresses). This article reviews the basics of when to use public IP addresses.
    
- [Private IP addresses](https://learn.microsoft.com/en-us/azure/virtual-network/private-ip-addresses). This article reviews the basics of when to use private IP addresses.
    

## Learn more with self-paced training

- [Introduction to Azure Virtual Networks](https://learn.microsoft.com/en-us/training/modules/introduction-to-azure-virtual-networks/). Learn how to design and implement core Azure Networking infrastructure.
    
- [Design an IP addressing schema for your Azure deployment (sandbox)](https://learn.microsoft.com/en-us/training/modules/design-ip-addressing-for-azure/). Learn about network IP addressing and integration.
    
- [Implement Windows Server IaaS virtual machine IP addressing and routing](https://learn.microsoft.com/en-us/training/modules/implement-windows-server-iaas-virtual-machine-ip-addressing-routing/). Learn about IP addressing and virtual networks for virtual machines.

---

# Configure network security groups

# Introduction

Network security groups are a way to limit network traffic to resources in your virtual network. Network security groups contain a list of security rules that allow or deny inbound or outbound network traffic.

Suppose your company has several locations and wants to migrate to a cloud based solution. The company only considers moving key systems onto the cloud platform if stringent security requirements can be met. These requirements include tight control over which computers have network access to the app servers. You need to secure both virtual machine networking and Azure services networking. Your goal is to prevent unwanted or unsecured network traffic from being able to reach key systems.

In this module, you learn how to create a network security group, configure inbound and outbound port rules, and verify secure connectivity.

The goal of this module is to teach you how to control network traffic with network security groups.

## Learning objectives

In this module, you learn how to:

- Determine when to use network security groups.
- Create network security groups.
- Implement and evaluate network security group rules.
- Describe the function of application security groups.

## Skills measured

The content in the module helps you prepare for [Exam AZ-104: Microsoft Azure Administrator](https://learn.microsoft.com/en-us/certifications/exams/az-104).

## Prerequisites

- Familiarity with Azure virtual networks and resources such as virtual machines.
- Working knowledge of the Azure portal so you can configure the network security groups.
- Basic understanding of traffic routing and traffic control strategies.

# Implement network security groups


You can limit network traffic to resources in your virtual network by using a network security group. You can assign a network security group to a subnet or a network interface, and define security rules in the group to control network traffic.

### Things to know about network security groups

Let's look at the characteristics of network security groups.

- A network security group contains a list of security rules that allow or deny inbound or outbound network traffic.
    
- A network security group can be associated to a subnet or a network interface.
    
- A network security group can be associated multiple times.
    
- You create a network security group and define security rules in the Azure portal.
    

Network security groups are defined for your virtual machines in the Azure portal. The **Overview** page for a virtual machine provides information about the associated network security groups. You can see details such as the assigned subnets, assigned network interfaces, and the defined security rules.

![Screenshot that shows details for a network security group for a virtual machine in the Azure portal.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-network-security-groups/media/network-security-groups-1ebf7bed.png)

#### Network security groups and subnets

You can assign network security groups to a subnet and create a protected screened subnet (also referred to as a demilitarized zone or _DMZ_). A DMZ acts as a buffer between resources within your virtual network and the internet.

- Use the network security group to restrict traffic flow to all machines that reside within the subnet.
    
- Each subnet can have a maximum of one associated network security group.
    

#### Network security groups and network interfaces

You can assign network security groups to a network interface card (NIC).

- Define network security group rules to control all traffic that flows through a NIC.
    
- Each network interface that exists in a subnet can have zero, or one, associated network security groups.

# Determine network security group rules

Security rules in network security groups enable you to filter network traffic. You can define rules to control the traffic flow in and out of virtual network subnets and network interfaces.

### Things to know about security rules

Let's review the characteristics of security rules in network security groups.

- Azure creates several default security rules within each network security group, including inbound traffic and outbound traffic. Examples of default rules include `DenyAllInbound` traffic and `AllowInternetOutbound` traffic.
    
- Azure creates the default security rules in each network security group that you create.
    
- You can add more security rules to a network security group by specifying conditions for any of the following settings:
    
    - **Name**
    - **Priority**
    - **Port**
    - **Protocol** (Any, TCP, UDP)
    - **Source** (Any, IP addresses, Service tag)
    - **Destination** (Any, IP addresses, Virtual network)
    - **Action** (Allow or Deny)
- Each security rule is assigned a Priority value. All security rules for a network security group are processed in priority order. When a rule has a low Priority value, the rule has a higher priority or precedence in terms of order processing.
    
- You can't remove the default security rules.
    
- You can override a default security rule by creating another security rule that has a higher Priority setting for your network security group.
    

#### Inbound traffic rules

Azure defines three default inbound security rules for your network security group. These rules **deny all inbound traffic** except traffic from your virtual network and Azure load balancers. The following image shows the default inbound security rules for a network security group in the Azure portal.

![Screenshot that shows default inbound security rules for a network security group in the Azure portal.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-network-security-groups/media/inbound-rules-a554314b.png)

#### Outbound traffic rules

Azure defines three default outbound security rules for your network security group. These rules **only allow outbound traffic** to the internet and your virtual network. The following image shows the default outbound security rules for a network security group in the Azure portal.

![Screenshot that shows default outbound security rules for a network security group in the Azure portal.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-network-security-groups/media/outbound-rules-ff90d802.png)

# Determine network security group effective rules

Each network security group and its defined security rules are evaluated independently. Azure processes the conditions in each rule defined for each virtual machine in your configuration.

- For inbound traffic, Azure first processes network security group security rules for any associated subnets and then any associated network interfaces.
- For outbound traffic, the process is reversed. Azure first evaluates network security group security rules for any associated network interfaces followed by any associated subnets.
- For both the inbound and outbound evaluation process, Azure also checks how to apply the rules for intra-subnet traffic.

How Azure ends up applying your defined security rules for a virtual machine determines the overall _effectiveness_ of your rules.

### Things to know about effective security rules

Let's explore how network security group rules are defined and processed within a virtual network to yield the effective rules.

Consider the following virtual network configuration that shows network security groups (NSGs) controlling traffic to virtual machines (VMs). The configuration requires security rules to manage network traffic to and from the internet over TCP port 80 via the network interface.

![Diagram that shows how network security group security rules control traffic to virtual machines.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-network-security-groups/media/security-groups-7a9d5c84.png)

In this virtual network configuration, there are three subnets. Subnet 1 contains two virtual machines: VM 1 and VM 2. Subnet 2 and Subnet 3 each contain one virtual machine: VM 3 and VM 4, respectively. Each VM has a network interface card (NIC).

Azure evaluates each NSG configuration to determine the effective security rules:

Expand table

|Evaluation|Subnet _NSG_|NIC _NSG_|Inbound rules|Outbound rules|
|---|---|---|---|---|
|**VM 1**|Subnet 1  <br>_NSG 1_|NIC  <br>_NSG 2_|_NSG 1_ subnet rules have precedence over _NSG 2_ NIC rules|_NSG 2_ NIC rules have precedence over _NSG 1_ subnet rules|
|**VM 2**|Subnet 1  <br>_NSG 1_|NIC  <br>_none_|_NSG 1_ subnet rules apply to both subnet and NIC|Azure default rules apply to NIC  <br>and _NSG 1_ subnet rules apply to subnet only|
|**VM 3**|Subnet 2  <br>_none_|NIC  <br>_NSG 2_|Azure default rules apply to subnet  <br>and _NSG 2_ rules apply to NIC|_NSG 2_ NIC rules apply to NIC and subnet|
|**VM 4**|Subnet 3  <br>_none_|NIC  <br>_none_|Azure default rules apply to both subnet and NIC  <br>and all inbound traffic is allowed|Azure default rules apply to both subnet and NIC  <br>and all outbound traffic is allowed|

#### Inbound traffic effective rules

Azure processes rules for inbound traffic for all VMs in the configuration. Azure identifies if the VMs are members of an NSG, and if they have an associated subnet or NIC.

- When an NSG is created, Azure creates the default security rule `DenyAllInbound` for the group. The default behavior is to deny all inbound traffic from the internet. If an NSG has a subnet or NIC, the rules for the subnet or NIC can override the default Azure security rules.
    
- NSG inbound rules for a subnet in a VM take precedence over NSG inbound rules for a NIC in the same VM.
    

#### Outbound traffic effective rules

Azure processes rules for outbound traffic by first examining NSG associations for NICs in all VMs.

- When an NSG is created, Azure creates the default security rule `AllowInternetOutbound` for the group. The default behavior is to allow all outbound traffic to the internet. If an NSG has a subnet or NIC, the rules for the subnet or NIC can override the default Azure security rules.
    
- NSG outbound rules for a NIC in a VM take precedence over NSG outbound rules for a subnet in the same VM.
    

### Things to consider when creating effective rules

Review the following considerations regarding creating effective security rules for machines in your virtual network.

- **Consider allowing all traffic**. If you place your virtual machine within a subnet or utilize a network interface, you don't have to associate the subnet or NIC with a network security group. This approach allows all network traffic through the subnet or NIC according to the default Azure security rules. If you're not concerned about controlling traffic to your resource at a specific level, then don't associate your resource at that level to a network security group.
    
- **Consider importance of allow rules**. When you create a network security group, you must define an **allow** rule for both the subnet and network interface in the group to ensure traffic can get through. If you have a subnet or NIC in your network security group, you must define an allow rule at each level. Otherwise, the traffic is denied for any level that doesn't provide an allow rule definition.
    
- **Consider intra-subnet traffic**. The security rules for a network security group that's associated to a subnet can affect traffic between all virtual machines in the subnet. By default, Azure allows virtual machines in the same subnet to send traffic to each other (referred to as _intra-subnet traffic_). You can prohibit intra-subnet traffic by defining a rule in the network security group to deny all inbound and outbound traffic. This rule prevents all virtual machines in your subnet from communicating with each other.
    
- **Consider rule priority**. The security rules for a network security group are processed in priority order. To ensure a particular security rule is always processed, assign the lowest possible priority value to the rule. It's a good practice to leave gaps in your priority numbering, such as 100, 200, 300, and so. The gaps in the numbering allow you to add new rules without having to edit existing rules.
    

### View effective security rules

If you have several network security groups and aren't sure which security rules are being applied, you can use the **Effective security rules** link in the Azure portal. You can use the link to verify which security rules are applied to your machines, subnets, and network interfaces.

![Screenshot of the Networking page in the Azure portal showing the Effective security rules link highlighted.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-network-security-groups/media/effective-security-rules-d93ab464.png)

# Create network security group rules

It's easy to add security rules to control inbound and outbound traffic in the Azure portal. You can configure your virtual network security group rule settings, and select from a large variety of communication services, including HTTPS, RDP, FTP, and DNS.

### Things to know about configuring security rules

Let's look at some of the properties you need to specify to create your security rules. As you review these settings, think about the traffic rules you need to create and what services can fulfill your network requirements.

![Screenshot that shows how to configure source and destination settings to create a security rule in the Azure portal.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-network-security-groups/media/add-network-security-rule-2f306d23.png)

- **Source**: Identifies how the security rule controls **inbound** traffic. The value specifies a specific source IP address range that's allowed or denied. The source filter can be any resource, an IP address range, an application security group, or a default tag.
    
- **Destination**: Identifies how the security rule controls **outbound** traffic. The value specifies a specific destination IP address range that's allowed or denied. The destination filter value is similar to the source filter. The value can be any resource, an IP address range, an application security group, or a default tag.
    
- **Service**: Specifies the destination protocol and port range for the security rule. You can choose a predefined service like RDP or SSH or provide a custom port range. There are a large number of services to select from.
    
    ![Screenshot that shows service rule options for a security rule in the Azure portal.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-network-security-groups/media/security-services.png)
    
- **Priority**: Assigns the priority order value for the security rule. Rules are processed according to the priority order of all rules for a network security group, including a subnet and network interface. The lower the priority value, the higher priority for the rule.
    
    ![Screenshot that shows how to set the priority value for a security rule in the Azure portal.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-network-security-groups/media/security-priority.png)

# Implement application security groups

You can implement [application security groups](https://learn.microsoft.com/en-us/azure/virtual-network/application-security-groups) in your Azure virtual network to logically group your virtual machines by workload. You can then define your network security group rules based on your application security groups.

### Things to know about using application security groups

Application security groups work in the same way as network security groups, but they provide an application-centric way of looking at your infrastructure. You join your virtual machines to an application security group. Then you use the application security group as a source or destination in the network security group rules.

Let's examine how to implement application security groups by creating a configuration for an online retailer. In our example scenario, we need to control network traffic to virtual machines in application security groups.

![Diagram that shows how application security groups combine with network security groups to protect applications.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-network-security-groups/media/application-security-groups.png)

#### Scenario requirements

Here are the scenario requirements for our example configuration:

- We have six virtual machines in our configuration with two web servers and two database servers.
- Customers access the online catalog hosted on our web servers.
- The web servers must be accessible from the internet over HTTP port 80 and HTTPS port 443.
- Inventory information is stored on our database servers.
- The database servers must be accessible over HTTPS port 1433.
- Only our web servers should have access to our database servers.

#### Solution

For our scenario, we need to build the following configuration:

1. Create application security groups for the virtual machines.
    
    1. Create an application security group named `WebASG` to group our web server machines.
        
    2. Create an application security group named `DBASG` to group our database server machines.
        
2. Assign the network interfaces for the virtual machines.
    
    - For each virtual machine server, assign its NIC to the appropriate application security group.
3. Create the network security group and security rules.
    
    - **Rule 1**: Set **Priority** to 100. Allow access from the internet to machines in the `WebASG` group from HTTP port 80 and HTTPS port 443.
        
        Rule 1 has the lowest priority value, so it has precedence over the other rules in the group. Customer access to our online catalog is paramount in our design.
        
    - **Rule 2**: Set **Priority** to 110. Allow access from machines in the `WebASG` group to machines in the `DBASG` group over HTTPS port 1433.
        
    - **Rule 3**: Set **Priority** to 120. **Deny** (X) access from anywhere to machines in the `DBASG` group over HTTPS port 1433.
        
        The combination of Rule 2 and Rule 3 ensures that only our web servers can access our database servers. This security configuration protects our inventory databases from outside attack.
        

### Things to consider when using application security groups

There are several advantages to implementing application security groups in your virtual networks.

- **Consider IP address maintenance**. When you control network traffic by using application security groups, you don't need to configure inbound and outbound traffic for specific IP addresses. If you have many virtual machines in your configuration, it can be difficult to specify all of the affected IP addresses. As you maintain your configuration, the number of your servers can change. These changes can require you to modify how you support different IP addresses in your security rules.
    
- **Consider no subnets**. By organizing your virtual machines into application security groups, you don't need to also distribute your servers across specific subnets. You can arrange your servers by application and purpose to achieve logical groupings.
    
- **Consider simplified rules**. Application security groups help to eliminate the need for multiple rule sets. You don't need to create a separate rule for each virtual machine. You can dynamically apply new rules to designated application security groups. New security rules are automatically applied to all the virtual machines in the specified application security group.
    
- **Consider workload support**. A configuration that implements application security groups is easy to maintain and understand because the organization is based on workload usage. Application security groups provide logical arrangements for your applications, services, data storage, and workloads.

# Interactive lab simulation

## Lab scenario

Your organization wants to ensure that access to virtual machines is restricted. As the Azure Administrator, you need to:

- Create and configure network security groups.
- Associate network security groups to virtual machines.
- Deny and allow access to the virtual machines by using network security groups.

## Architecture diagram

![Diagram showing the architecture as explained in the text.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-network-security-groups/media/architecture-create-networks.png)

## Objectives

- **Task 1**: Create a virtual machine to test network security.
    - Create a Windows Server virtual machine.
    - Don't configure any inbound port rules or NIC network security groups.
    - Verify the virtual machine is created.
    - Review the **Inbound port rules** tab, and note there are no network security groups associated with the virtual machine.
- **Task 2**: Create a network security group, and associate the group with the virtual machine.
    - Create a network security group.
    - Associate the network security group with the virtual machine network interface (NIC).
- **Task 3**: Configure an inbound security port rule to allow RDP.
    - Verify you can't connect to the virtual machine by using RDP.
    - Add an **inbound port rule** to allow RDP to the virtual machine on port 3389.
    - Verify you can now connect to the virtual machine with RDP.
- **Task 4**: Configure an outbound security port rule to deny internet access
    - Verify you can access the internet from the virtual machine.
    - Add an **outbound port rule** to deny internet access from the virtual machine.
    - Verify you can no longer access the internet from the virtual machine.

 Note

Select the thumbnail image to start the lab simulation. When you're done, be sure to return to this page so you can continue learning.

[![Screenshot of the simulation page.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-network-security-groups/media/simulation-create-networks.png)](https://mslearn.cloudguides.com/en-us/guides/AZ-900%20Exam%20Guide%20-%20Azure%20Fundamentals%20Exercise%2013)

---

# Configure Azure Virtual Network peering

# Introduction

Azure Virtual Network peering lets you connect virtual networks in the same or different regions. Azure Virtual Network peering provides secure communication between resources in the peered networks.

Suppose your engineering company is migrating services to Azure. The company is deploying services into separate Azure virtual networks. Private connectivity between the virtual networks isn't yet configured. Several business units identified services in the virtual networks that need to communicate with each other.

You're responsible for implementing an Azure Virtual Network peering solution and enabling connectivity between the virtual networks. Two of your strategy goals include preventing exposure of the services to the internet, and keeping the integration as simple as possible. Your solution should address transit and connectivity concerns.

The goal of this module is to successfully implement Azure Virtual Network peering.

## Learning objectives

In this module, you learn how to:

- Identify usage cases and product features of Azure Virtual Network peering.
- Configure your network to implement Azure VPN Gateway for transit connectivity.
- Extend peering by using a hub and spoke network with user-defined routes and service chaining.

## Skills measured

The content in the module helps you prepare for [Exam AZ-104: Microsoft Azure Administrator](https://learn.microsoft.com/en-us/certifications/exams/az-104).

## Prerequisites

- Basic understanding of cloud networking including virtual networks and virtual machines.
    
- Familiarity with the command line connectivity testing tools.

# Determine Azure Virtual Network peering uses

Perhaps the simplest and quickest way to connect your virtual networks is to use Azure Virtual Network peering. Virtual Network peering enables you to seamlessly connect two Azure virtual networks. After the networks are peered, the two virtual networks operate as a single network, for connectivity purposes.

### Things to know about Azure Virtual Network peering

Let's examine some prominent characteristics of Azure Virtual Network peering.

- There are two types of Azure Virtual Network peering: _regional_ and _global_.
    
    ![Diagram that demonstrates the two types of Azure Virtual Network peering: global and regional.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-vnet-peering/media/network-peering-5beae28a.png)
    
- **Regional virtual network peering** connects Azure virtual networks that exist in the same region.
    
- **Global virtual network peering** connects Azure virtual networks that exist in different regions.
    
- You can create a regional peering of virtual networks in the same Azure public cloud region, or in the same China cloud region, or in the same Microsoft Azure Government cloud region.
    
- You can create a global peering of virtual networks in any Azure public cloud region, or in any China cloud region.
    
- Global peering of virtual networks in different Azure Government cloud regions isn't permitted.
    
- After you create a peering between virtual networks, the individual virtual networks are still managed as separate resources.
    

### Things to consider when using Azure Virtual Network peering

Consider the following benefits of using Azure Virtual Network peering.

Expand table

|Benefit|Description|
|---|---|
|**Private network connections**|When you implement Azure Virtual Network peering, network traffic between peered virtual networks is private. Traffic between the virtual networks is kept on the Microsoft Azure backbone network. No public internet, gateways, or encryption is required in the communication between the virtual networks.|
|**Strong performance**|Because Azure Virtual Network peering utilizes the Azure infrastructure, you gain a low-latency, high-bandwidth connection between resources in different virtual networks.|
|**Simplified communication**|Azure Virtual Network peering lets resources in one virtual network communicate with resources in a different virtual network, after the virtual networks are peered.|
|**Seamless data transfer**|You can create an Azure Virtual Network peering configuration to transfer data across Azure subscriptions, deployment models, and across Azure regions.|
|**No resource disruptions**|Azure Virtual Network peering doesn't require downtime for resources in either virtual network when creating the peering, or after the peering is created.|

# Determine gateway transit and connectivity

When virtual networks are peered, you can configure Azure VPN Gateway in the peered virtual network as a _transit point_. In this scenario, a peered virtual network uses the remote VPN gateway to gain access to other resources.

Consider a scenario where three virtual networks in the same region are connected by virtual network peering. Virtual network A and virtual network B are each peered with a hub virtual network. The hub virtual network contains several resources, including a gateway subnet and an Azure VPN gateway. The VPN gateway is configured to allow VPN gateway transit. Virtual network B accesses resources in the hub, including the gateway subnet, by using a remote VPN gateway.

![Diagram of a regional virtual network peering. One network allows VPN gateway transit and uses a remote VPN gateway to access resources in a hub virtual network.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-vnet-peering/media/gateway-transit-173a51a0.png)

### Things to know about Azure VPN Gateway

Let's take a closer look at how Azure VPN Gateway is implemented with Azure Virtual Network peering.

- A virtual network can have only one VPN gateway.
    
- Gateway transit is supported for both regional and global virtual network peering.
    
- When you allow VPN gateway transit, the virtual network can communicate to resources outside the peering. In our sample illustration, the gateway subnet gateway within the hub virtual network can complete tasks such as:
    
    - Use a site-to-site VPN to connect to an on-premises network.
    - Use a vnet-to-vnet connection to another virtual network.
    - Use a point-to-site VPN to connect to a client.
- Gateway transit allows peered virtual networks to share the gateway and get access to resources. With this implementation, you don't need to deploy a VPN gateway in the peer virtual network.
    
- You can apply network security groups in a virtual network to block or allow access to other virtual networks or subnets. When you configure virtual network peering, you can choose to open or close the network security group rules between the virtual networks.

# Create virtual network peering

Azure Virtual Network peering can be configured for virtual networks by using PowerShell, the Azure CLI, and in the Azure portal. In this module, we review the steps to create the peering in the Azure portal for virtual networks deployed through Azure Resource Manager.

### Things to know about creating virtual network peering

There are a few points to review before we look at how to create the peering in the Azure portal.

- To implement virtual network peering, your Azure account must be assigned to the `Network Contributor` or `Classic Network Contributor` role. Alternatively, your Azure account can be assigned to a custom role that can complete the necessary peering actions. For details, see [Permissions](https://learn.microsoft.com/en-us/azure/virtual-network/virtual-network-manage-peering?tabs=peering-portal#permissions).
    
- To create a peering, you need two virtual networks.
    
- The second virtual network in the peering is referred to as the _remote network_.
    
- Initially, the virtual machines in your virtual networks can't communicate with each other. After the peering is established, the machines can communicate within the peered network based on your configuration settings.
    
![](https://youtu.be/pSqDlQlcsLo)

## How to connect virtual networks across Azure regions with Azure Global VNet peering

## How to check your peering status

In the Azure portal, you can check the connectivity status of the virtual networks in your virtual network peering. The status conditions depend on how your virtual networks are deployed.

 Important

Your peering isn't successfully established until both virtual networks in the peering have a status of **Connected**.

- For deployment with the Azure Resource Manager, the two primary status conditions are **Initiated** and **Connected**. For the classic deployment model, the **Updating** status condition is also used.
    
- When you create the initial peering _to_ the second (remote) virtual network from the first virtual network, the peering status for the first virtual network is **Initiated**.
    
- When you create the subsequent peering _from_ the second virtual network to the first virtual network, the peering status for both the first and remote virtual networks is **Connected**. In the Azure portal, you can see the status for the first virtual network change from **Initiated** to **Connected**.


# Extend peering with user-defined routes and service chaining

Virtual network peering is nontransitive. The communication capabilities in a peering are available to only the virtual networks and resources in the peering. Other mechanisms have to be used to enable traffic to and from resources and networks outside the private peering network.

Suppose you have three virtual networks: A, B, and C. You establish virtual network peering between networks A and B, and also between networks B and C. You don't set up peering between networks A and C. The virtual network peering capabilities that you set up between networks B and C don't automatically enable peering communication capabilities between networks A and C.

### Things to know about extending peering

There are a few ways to extend the capabilities of your peering for resources and virtual networks outside your peering network:

- Hub and spoke networks
- User-defined routes
- Service chaining

You can implement these mechanisms and create a multi-level hub and spoke architecture. These options can help overcome the limit on the number of virtual network peerings per virtual network.

The following diagram shows a hub and spoke virtual network with an NVA and VPN gateway. The hub and spoke network is accessible to other virtual networks via user-defined routes and service chaining.

![Diagram that shows a hub virtual network with an NVA and VPN gateway that are accessible to other virtual networks.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-vnet-peering/media/service-chains-5c9286d1.png)

Expand table

|Mechanism|Description|
|---|---|
|**Hub and spoke network**|When you deploy a hub-and-spoke network, the hub virtual network can host infrastructure components like a network virtual appliance (NVA) or Azure VPN gateway. All the spoke virtual networks can then peer with the hub virtual network. Traffic can flow through NVAs or VPN gateways in the hub virtual network.|
|**User-defined route (UDR)**|Virtual network peering enables the next hop in a user-defined route to be the IP address of a virtual machine in the peered virtual network, or a VPN gateway.|
|**Service chaining**|Service chaining is used to direct traffic from one virtual network to a virtual appliance or gateway. A user-defined route defines the peered networks.|

# Interactive lab simulation

## Lab scenario

Your organization has three datacenters connected with a mesh wide-area network. As the Azure Administrator, you need to implement the on-premises infrastructure in Azure.

- There are two offices, New York and Boston, in one region.
- There's one office, Seattle, in another region.
- All the offices need to be networked together so they can share information.
- This simulation focuses on the connectivity of the offices, and not creating the individual Azure resources.

## Architecture diagram

![Architecture diagram as explained in the text.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-vnet-peering/media/lab-05.png)

## Objectives

 Note

You may find slight differences between the interactive simulation and the Azure environment, but the core concepts and ideas being demonstrated are the same.

- **Task 1**: Create the infrastructure environment. In this task, you deploy three virtual machines. Virtual machines are deployed in different regions and virtual networks.
    - Use a template to create the virtual networks and virtual machines in the different regions. You can review the [lab templates](https://github.com/MicrosoftLearning/AZ-104-MicrosoftAzureAdministrator/tree/master/Allfiles/Interactive%20Lab%20Simulation%20Files/05).
    - Use Azure PowerShell to deploy the template.
- **Task 2**: Configure local and global virtual network peering.
    - Create a local virtual network peering between the two virtual networks in the same region.
    - Create a global virtual network peering between virtual networks in different regions.
- **Task 3**: Test intersite connectivity between virtual machines on the three virtual networks.
    - Test the virtual machine connections in the same region.
    - Test the virtual machine connections in different regions.

 Note

select the thumbnail image to start the lab simulation. When you're done, be sure to return to this page so you can continue learning.

[![Screenshot of the simulation page.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-vnet-peering/media/simulation-intersite-thumbnail.jpg)](https://mslabs.cloudguides.com/guides/AZ-104%20Exam%20Guide%20-%20Microsoft%20Azure%20Administrator%20Exercise%209)

# Summary and resources

In this module, you learned Azure Virtual Network peering lets you connect virtual networks in a hub and spoke topology. You learned how to configure your virtual networks with Azure VPN Gateway for transit connectivity. You explored how to extend peering with user-defined routes and service chaining.

The main takeaways from this module are:

- Azure Virtual Network peering allows for the connection of virtual networks in a hub and spoke topology.
    
- There are two types of peering: regional and global. Regional peering connects virtual networks in the same region. Global peering connects virtual networks in different regions.
    
- Network traffic between peered virtual networks is private and kept on the Azure backbone network.
    
- You can configure Azure VPN Gateway in the peered virtual network as a transit point to access resources in another network.
    
- Network security groups can be applied to block or allow access between virtual networks when configuring virtual network peering.

---

# Configure network routing and endpoints

# Introduction

Administrators use network routes to control the flow of traffic through a network. Azure virtual networking provides capabilities to help you customize your network routes, establish service endpoints, and access private links.

In this module, suppose your company recently suffered a security incident that exposed customer personal information. This security incident has resulted in the loss of customers' confidential data and confidence. To address this scenario, the IT team has recommended implementing network virtual appliances (NVAs). You need to ensure traffic is properly routed through the virtual appliances. You're exploring other security options like service endpoints and private links.

## Learning objectives

In this module, you learn how to:

- Implement system routes and user-defined routes.
- Configure a custom route.
- Implement service endpoints.
- Identify features and usage cases for Azure Private Link and endpoint services.

## Skills measured

The content in the module helps you prepare for [Exam AZ-104: Microsoft Azure Administrator](https://learn.microsoft.com/en-us/certifications/exams/az-104). The module concepts are covered in:

Configure and manage virtual networking (25–30%)

- Implement and manage virtual networking.
    - Configure user-defined network routes.
    - Configure endpoints on subnets.
    - Configure private endpoints.

## Prerequisites

- Familiarity with network routing.

# Review system routes

Azure uses _system routes_ to direct network traffic between virtual machines, on-premises networks, and the internet. Information about the system routes is recorded in a _route table_.

### Things to know about system routes

Let's take a closer look at how Azure implements system routes.

- Azure uses system routes to control traffic for virtual machines in several scenarios:
    
    - Traffic between virtual machines in the same subnet
    - Traffic between virtual machines in different subnets in the same virtual network
    - Traffic from virtual machines to the internet
- A route table contains a set of rules (called _routes_) that specifies how packets should be routed in a virtual network.
    
- Route tables record information about the system routes, where the tables are associated to subnets.
    
- Each packet leaving a subnet is handled based on the associated route table.
    
- Packets are matched to routes by using the destination. The destination can be an IP address, a virtual network gateway, a virtual appliance, or the internet.
    
- When a matching route can't be found, the packet is dropped.
    

#### Business scenario

Suppose you have a virtual network with two subnets. In this configuration, you can use Azure system routes to control communication between the subnets and between subnets and the internet. A front-end subnet can use a system route to access the internet. A back-end subnet can use a system route to access the front-end subnet. Both subnets access a route table. The following illustration highlights this scenario:

![Diagram that shows two subnets that use system routes as described in the text.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-network-routing-endpoints/media/system-routes-08992506.png)

# Identify user-defined routes

Azure automatically handles all network traffic routing, but in some cases, a custom configuration is preferable. In these situations, you can configure _user-defined routes_ (UDRs) and _next hop_ targets.

### Things to know about user-defined routes

Let's examine the characteristics of user-defined routes.

- UDRs control network traffic by defining routes that specify the _next hop_ of the traffic flow.
    
- The next hop can be one of the following targets:
    
    - Virtual network gateway
    - Virtual network
    - Internet
    - Network virtual appliance (NVA)
- Similar to system routes, UDRs also access route tables.
    
- Each route table can be associated to multiple subnets.
    
- Each subnet can be associated to one route table only.
    
- There are no charges for creating route tables in Microsoft Azure.
    

#### Business scenario

Suppose you have a virtual machine that performs a network function like routing, firewalling, or WAN optimization. You want to direct certain subnet traffic to the NVA. To accomplish this configuration, you can place an NVA between subnets or between one subnet and the internet. The subnet can use a UDR to access the NVA and then the internet. The subnet can use another UDR and NVA to access the back-end subnet. The following illustration highlights this scenario:

![Diagram that shows two subnets that use a UDR to access an NVA as described in the text.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-network-routing-endpoints/media/user-defined-routes-2417e693.png)

# Determine service endpoint uses

A virtual network _service endpoint_ provides the identity of your virtual network to the Azure service. After service endpoints are enabled in your virtual network, you can secure Azure service resources to your virtual network by adding a _virtual network rule_ to the resources.

Today, Azure service traffic from a virtual network uses public IP addresses as source IP addresses. With service endpoints, service traffic switches to use virtual network private addresses as the source IP addresses when accessing the Azure service from a virtual network. This switch allows you to access the services without the need for reserved public IP addresses that are typically used in IP firewalls.

### Things to know about service endpoints

Review the following characteristics of service endpoints.

- Service endpoints can extend your virtual network identity to your Azure services to secure your service resources.
    
- You secure your Azure service resources to your virtual network by using virtual network rules.
    
- Virtual network rules can remove public internet access to resources, and allow traffic only from your virtual network.
    
- Service endpoints always take service traffic directly from your virtual network to the service on the Microsoft Azure backbone network.
    
- Service endpoints are configured through the subnet. No extra overhead is required to maintain the endpoints.
    

The following illustration shows a virtual machine connecting to the Azure service through a service endpoint. A virtual machine in a subnet accesses an Azure Storage account through a service endpoint. Virtual network rules allow the virtual machine to access the Azure service resource, but not communicate with the internet.

![Diagram of a virtual machine in a subnet connecting to an Azure service through a service endpoint.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-network-routing-endpoints/media/service-endpoint-addresses-a027197f.png)

### Things to consider when using service endpoints

There are several scenarios where using service endpoints can be advantageous. Review the following points and think about how you can implement service endpoints in your configuration.

- **Consider improved security for resources**. Implement service endpoints to improve the security of your Azure service resources. When service endpoints are enabled in your virtual network, you secure Azure service resources to your virtual network with virtual network rules. The rule improves security by fully removing public internet access to resources, and allowing traffic only from your virtual network.
    
- **Consider optimal routing for service traffic**. Routes in your virtual network that force internet traffic to your on-premises or network virtual appliances also typically force Azure service traffic to take the same route as the internet traffic. This traffic control process is known as _forced-tunneling_. Service endpoints provide optimal routing for Azure service traffic to allow you to circumvent forced tunneling.
    
- **Consider direct traffic to the Microsoft network**. Use service endpoints to keep traffic on the Azure backbone network. This approach allows you to continue auditing and monitoring outbound internet traffic from your virtual networks, through forced-tunneling, without impacting service traffic. Learn more about [user-defined routes and forced-tunneling](https://learn.microsoft.com/en-us/azure/firewall/forced-tunneling).
    
- **Consider easy configuration and maintenance**. Configure service endpoints in your subnets for simple setup and low maintenance. You no longer need reserved public IP addresses in your virtual networks to secure Azure resources through an IP firewall. There are no NAT or gateway devices required to set up the service endpoints.
    

> Note
>
>With service endpoints, the virtual machine IP addresses switch from public to private IPv4 addresses. Existing Azure service firewall rules that use Azure public IP addresses stop working after the switch. Ensure Azure service firewall rules allow for this switch before you set up service endpoints. You might also experience temporary interruption to service traffic from this subnet while configuring service endpoints.

# Determine service endpoint services

It's easy to add a service endpoint to the virtual network. In the Azure portal, you select the Azure service for which to create the endpoint. In this unit, we examine several services, including Azure Cosmos DB, Event Hubs, Key Vault, and SQL Database.

![Screenshot of the Service endpoints page in the Azure portal.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-network-routing-endpoints/media/add-service-endpoints-5df9ecfc.png)

 Note

Adding service endpoints can take up to 15 minutes to complete. Each service endpoint integration has its own Azure documentation page.

Expand table

|Service|Availability|Description|
|---|---|---|
|**Azure Storage**|Generally available in all Azure regions|This endpoint gives traffic an optimal route to the Azure Storage service. Each Storage account supports up to 100 virtual network rules.|
|**Azure SQL Database and Azure SQL Data Warehouse**|Generally available in all Azure regions|A firewall security feature controls whether your database accepts communication from particular subnets in virtual networks. This feature applies to the database server for your single databases and elastic pool in SQL Database or your databases in SQL Data Warehouse.|
|**Azure Database for PostgreSQL and Azure Database for MySQL**|Generally available in Azure regions where database service is available|Virtual network service endpoints and rules extend the private address space of a virtual network to your Azure Database for PostgreSQL server and Azure Database for MySQL server.|
|**Azure Cosmos DB**|Generally available in all Azure regions|You can configure the Azure Cosmos DB account to allow access only from a specific subnet of virtual network. Enable service endpoints to access Azure Cosmos DB on the subnet within a virtual network. Traffic from the subnet is sent to Azure Cosmos DB with the identity of the subnet and virtual network. After the Azure Cosmos DB service endpoint is enabled, you can limit access to the subnet by adding it to your Azure Cosmos DB account.|
|**Azure Key Vault**|Generally available in all Azure regions|The virtual network service endpoints for Key Vault allow you to restrict access to a specified virtual network. The endpoints also allow you to restrict access to a list of IPv4 (internet protocol version 4) address ranges. Any user connecting to your key vault from outside those sources is denied access.|
|**Azure Service Bus and Azure Event Hubs**|Generally available in all Azure regions|The integration of Service Bus with virtual network service endpoints enables secure access to messaging capabilities from workloads like virtual machines that are bound to virtual networks. The network traffic path is secured on both ends.|

# Identify private link uses

Azure Private Link provides private connectivity from a virtual network to Azure platform as a service (PaaS), customer-owned, or Microsoft partner services. It simplifies the network architecture and secures the connection between endpoints in Azure by eliminating data exposure to the public internet.

### Things to know about Azure Private Link

Let's examine the characteristics of Azure Private Link and network routing configurations.

- Azure Private Link keeps all traffic on the Microsoft global network. There's no public internet access.
    
- Private Link is global and there are no regional restrictions. You can connect privately to services running in other Azure regions.
    
- Services delivered on Azure can be brought into your private virtual network by mapping your network to a private endpoint.
    
- Private Link can privately deliver your own services in your customer's virtual networks.
    
- All traffic to the service can be routed through the private endpoint. No gateways, NAT devices, Azure ExpressRoute or VPN connections, or public IP addresses are required.
    

The following Illustration demonstrates a network routing configuration with Azure Private Link. The service connects to a network security group (NSG) private endpoint by using Azure SQL Database. This configuration prevents a direct connection.

![Diagram that shows a network routing configuration with Azure Private Link as described in the text.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-network-routing-endpoints/media/private-links-602b4a62.png)

### Things to consider when using Azure Private Link

There are many benefits to working with Azure Private Link. Review the following points and consider how you can implement the service for your scenarios.

- **Consider private connectivity to services on Azure**. Connect privately to services running in other Azure regions. Traffic remains on the Microsoft network with no public internet access.
    
- **Consider integration with on-premises and peered networks**. Access private endpoints over private peering or VPN tunnels from on-premises or peered virtual networks. Microsoft hosts the traffic, so you don't need to set up public peering or use the internet to migrate your workloads to the cloud.
    
- **Consider protection against data exfiltration for Azure resources**. Map private endpoints to Azure PaaS resources. When there's a security incident within your network, only the mapped resources are accessible. This implementation eliminates the threat of data exfiltration.
    
- **Consider services delivered directly to customer virtual networks**. Privately consume Azure PaaS, Microsoft partner, and your own services in your virtual networks on Azure. Private Link works across tenants to help unify your experience across services. Send, approve, or reject requests directly without permissions or role-based access controls.

# Interactive lab simulation

## Lab scenario

Your organization is exploring Azure virtual networking capabilities. As the Azure Administrator you've been tasked to implement the following requirements:

- Create and configure a virtual network in Azure.
- Deploy two virtual machines into different subnets of the virtual network.
- Ensure the virtual machines have public IP addresses that won't change over time.
- Protect the virtual machine public endpoints from being accessible from the internet.
- Ensure internal Azure virtual machines names and IP addresses can be resolved.
- Ensure a publicly available domain name can be resolved by external queries.

## Architecture diagram

![Architecture diagram as explained in the text.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-network-routing-endpoints/media/lab-04.png)

 Note

Tasks 1 - 4 focus on IP addresses and access.

## Objectives

 Note

You may find slight differences between the interactive simulation and the Azure environment, but the core concepts and ideas being demonstrated are the same.

- **Task 1**: Create and configure a virtual network in Azure.
    - Create a virtual network, **az104-04-vnet1**.
    - Add two subnets, **Subnet0** and **Subnet1**, to the virtual network.
- **Task 2**: Deploy virtual machines into different subnets of the virtual network.
    - Review a JSON template that will deploy two virtual machines, **VM0** and **VM1**.
    - Use Azure PowerShell to deploy the template.
- **Task 3**: Configure private and public IP addresses of Azure virtual machines. Ensure the IP addresses don't change over time.
    - Associate the VM0 NIC with a static public IP address, **az104-04-pip0**.
    - Associate the VM1 NIC with a static public IP address, **az104-04-pip1**.
- **Task 4**: Configure network security groups. Protect the virtual machine public endpoints from being accessible from the internet.
    - Verify you can't use RDP to connect to a virtual machine.
    - Create a network security group.
    - Configure inbound security rules to allow RDP.
    - Associate the network security group with the virtual machine NICs.
    - Confirm that you can now use RDP to connect to a virtual machine.
- **Task 5**: Configure Azure DNS for internal name resolution. Ensure internal Azure virtual machines names and IP addresses can be resolved.
    - Create a private DNS zone for your organization.
    - Add a virtual network link to the virtual network.
    - Verify the virtual machines DNS records are registered.
    - Verify internal DNS name resolution is working.
- **Task 6**: Configure Azure DNS for external name resolution. Ensure a publicly available domain name can be resolved by external queries.
    - Create a DNS zone for a publicly available domain name.
    - Add a DNS record for each virtual machine.
    - Verify external DNS name resolution is working.

 Note

Select the thumbnail image to start the lab simulation. When you're done, be sure to return to this page so you can continue learning.

[![Screenshot of the simulation page.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-network-routing-endpoints/media/simulation-networks-thumbnail.jpg)](https://mslabs.cloudguides.com/guides/AZ-104%20Exam%20Guide%20-%20Microsoft%20Azure%20Administrator%20Exercise%208)
# Summary and resources

Network routes control the flow of traffic through your network. You can customize these routes, implement service endpoints, and work with private links.

In this module, you learned how to implement system routes and user-defined routes. You identified features and usage cases for Azure Private Link and endpoint services. You explored how to configure a custom route, and discovered how to work with service endpoints.

## Learn more

- Peruse [virtual network traffic routing documentation](https://learn.microsoft.com/en-us/azure/virtual-network/virtual-networks-udr-overview).
    
- Read about [Virtual network traffic routing](https://learn.microsoft.com/en-us/azure/virtual-network/virtual-networks-udr-overview).
    
- Route [network traffic with a route table by using the Azure portal](https://learn.microsoft.com/en-us/azure/virtual-network/tutorial-create-route-table-portal).
    
- Configure [BGP for Azure VPN Gateway by using PowerShell](https://learn.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-bgp-resource-manager-ps).
    
- Create [custom routes](https://learn.microsoft.com/en-us/azure/virtual-network/manage-route-table#create-a-route).
    
- View [all routes for a subnet and diagnose virtual machine routing problems](https://learn.microsoft.com/en-us/azure/virtual-network/diagnose-network-routing-problem).
    
- Determine [the next hop type between a virtual machine and a destination IP address](https://learn.microsoft.com/en-us/azure/network-watcher/diagnose-vm-network-routing-problem#use-next-hop).
    
- Explore [user-defined routes and forced-tunneling in Azure Firewall](https://learn.microsoft.com/en-us/azure/firewall/forced-tunneling).
    

## Learn more with self-paced training

- Complete an [introduction to Azure Private Link](https://learn.microsoft.com/en-us/training/modules/introduction-azure-private-link/).

## Learn more with optional hands-on exercises

- Manage and control [traffic flow in your Azure deployment with routes (sandbox)](https://learn.microsoft.com/en-us/training/modules/control-network-traffic-flow-with-routes/).

---

# Configure Azure Load Balancer

# Introduction

Many applications need to be resilient to failure and scale easily when demand increases. Administrators can address these requirements by using Azure Load Balancer.

Suppose your healthcare organization is launching a new portal application for patients to schedule appointments. The application has a patient portal, web application frontend, and business tier database. The database is used by the frontend to retrieve and save patient information.

The new portal needs to be available around the clock to handle failures. The portal must adjust to fluctuations in load by adding and removing resources to match the load. You need a solution to distribute work to virtual machines across the system as virtual machines are added. The solution should detect failures and reroute jobs to virtual machines as needed. Improved resiliency and scalability are required to help ensure patients can schedule appointments from any location.

You're responsible for configuring the load balancers to distribute incoming network traffic across a group of back-end servers. You need to scale your applications while maintaining throughput and keeping response times low.

The goal of this module is to equip you to implement an Azure load balancer.

## Learning objectives

In this module, you learn how to:

- Identify features and usage cases for Azure Load Balancer.
- Implement public and internal Azure load balancers.
- Compare features of load balancer SKUs and configuration differences.
- Configure back-end pools, load-balancing rules, session persistence, and health probes.

## Skills measured

The content in the module helps you prepare for [Exam AZ-104: Microsoft Azure Administrator](https://learn.microsoft.com/en-us/certifications/exams/az-104).

## Prerequisites

- Basic knowledge of virtual networks and routing.
- Familiarity with the Azure portal so you can configure the load balancer.

# Determine Azure Load Balancer uses

Azure Load Balancer delivers high availability and network performance to your applications. Administrators use load balancing to efficiently distribute incoming network traffic across back-end servers and resources. A load balancer is implemented by using load-balancing rules and health probes.

The following diagram shows how Azure Load Balancer works. The frontend exchanges information with a load balancer. The load balancer uses rules and health probes to communicate with the backend.

![Diagram that shows how a load balancer works as described in the text.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-azure-load-balancer/media/load-balancer-4caf947b.png)

### Things to know about Azure Load Balancer

Let's take a closer look at how Azure Load Balancer operates.

- Azure Load Balancer can be used for inbound and outbound scenarios.
    
- You can implement a **public** or **internal** load balancer, or use both types in a combination configuration.
    
- To implement a load balancer, you configure four components:
    
    - Front-end IP configuration
    - Back-end pools
    - Health probes
    - Load-balancing rules
- The front-end configuration specifies the public IP or internal IP that your load balancer responds to.
    
- The back-end pools are your services and resources, including Azure Virtual Machines or instances in Azure Virtual Machine Scale Sets.
    
- Load-balancing rules determine how traffic is distributed to back-end resources.
    
- Health probes ensure the resources in the backend are healthy.
    
- Load Balancer scales up to millions of TCP and UDP application flows.

# Implement a public load balancer

Administrators use public load balancers to map the public IP addresses and port numbers of incoming traffic to the private IP addresses and port numbers of virtual machines. The mapping can also be configured for response traffic from the virtual machines.

Load-balancing rules are used to specify how to distribute specific types of traffic across multiple virtual machines or services. You can use this approach to share the load of incoming web request traffic across multiple web servers.

#### Business scenario

Consider a scenario where internet traffic attempts to reach virtual machines in a web tier subnet that implements a public load balancer. Internet clients send webpage requests to the public IP address of a web app on TCP port 80. Azure Load Balancer intercepts the traffic and distributes the requests across the virtual machines in the load-balanced set according to the defined load-balancing rules. The following illustration highlights this scenario:

![Diagram showing how a public load balancer works as described in the text.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-azure-load-balancer/media/public-load-balancer-46d5d9fe.png)

# Implement an internal load balancer

Administrators use internal load balancers to direct traffic to resources that reside in a virtual network, or to resources that use a VPN to access Azure infrastructure. In this configuration, front-end IP addresses and virtual networks are never directly exposed to an internet endpoint. Internal line-of-business applications run in Azure and are accessed from within Azure or from on-premises resources.

#### Business scenario

Suppose you have an Azure SQL Database tier subnet with several virtual machines, and you implement an internal load balancer. Database requests need to be distributed to the backend. The internal load balancer receives the database requests and uses the load-balancing rules to determine how to distribute the requests to the back-end SQL servers. The SQL servers respond on port 1433. The following illustration highlights this scenario:

![Diagram showing how an internal load balancer works as described in the text.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-azure-load-balancer/media/internal-load-balancer-5ae85589.png)

### Things to consider when using an internal load balancer

You can implement an internal load balancer to achieve several types of load balancing.

- **Within virtual network**: Establish load balancing from your virtual machines in the virtual network to a set of virtual machines that reside within the same virtual network.
    
- **For cross-premises virtual network**: Apply load balancing from your on-premises computers to a set of virtual machines that reside within the same virtual network.
    
- **For multi-tier applications**: Implement load balancing for your internet-facing multi-tier applications when the back-end tiers aren't internet-facing. The back-end tiers require traffic load-balancing from the internet-facing tier.
    
- **For line-of-business applications**: Add load balancing for your line-of-business applications hosted in Azure without having to add other load balancer hardware or software. This scenario includes on-premises servers that are in the set of computers whose traffic is load-balanced.
    
- **With public load balancer**: Configure a public load balancer in front of your internal load balancer to create a multi-tier application.

# Determine load balancer SKUs

When you create an Azure load balancer in the Azure portal, you select the type of load balancer to create (internal or public) and the Stock Keeping Unit (SKU). Azure Load Balancer supports three SKU options: Basic, Standard, and Gateway. Each SKU provides different features, scenario scaling, and pricing.

![Screenshot that shows how to create an Azure load balancer in the Azure portal.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-azure-load-balancer/media/load-balancer-types-a4c0eceb.png)

### Things to know about Azure Load Balancer SKUs

Let's review some points to consider when choosing the SKU type for your load balancer.

- Standard Load Balancer is the newest product. It's essentially a superset of Basic Load Balancer.
    
- The Standard SKU offers an expanded and more granular feature set than the Basic SKU.
    
- The Basic SKU can be upgraded to the Standard SKU. But, new designs and architectures should use the Standard SKU.
    
- The Gateway SKU supports high performance and high availability scenarios with third-party network virtual appliances (NVAs).
    

## Compare Basic and Standard SKU features

The following table provides a brief comparison of how features are implemented in the Standard and Basic SKUs.

Expand table

|Feature|Basic SKU|Standard SKU|
|---|---|---|
|**Health probes**|HTTP, TCP|HTTPS, HTTP, TCP|
|**Availability zones**|Not available|Zone-redundant and zonal frontends for inbound and outbound traffic|
|**Multiple frontends**|Inbound only|Inbound and outbound|
|**Security**|- Open by default  <br>- (Optional) Control through network security groups (NSGs)|- Closed to inbound flows unless allowed by an NSG  <br>- Internal traffic from the virtual network to the internal load balancer is allowed|

# Create back-end pools

Each load balancer has one or more back-end pools that are used for distributing traffic. The back-end pools contain the IP addresses of the virtual NICs that are connected to your load balancer. You configure these pool settings in the Azure portal.

![Screenshot that shows how to configure back-end pools in the Azure portal.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-azure-load-balancer/media/backend-pools-1984adb4.png)

### Things to know about back-end pools

The SKU type that you select determines which endpoint configurations are supported for the pool along with the number of pool instances allowed.

- The Basic SKU allows up to 300 pools, and the Standard SKU allows up to 1,000 pools.
    
- When you configure the back-end pools, you can connect to availability sets, virtual machines, or Azure Virtual Machine Scale Sets.
    
- For the Basic SKU, you can select virtual machines in a single availability set or virtual machines in an instance of Azure Virtual Machine Scale Sets.
    
- For the Standard SKU, you can select virtual machines or Virtual Machine Scale Sets in a single virtual network. Your configuration can include a combination of virtual machines, availability sets, and Virtual Machine Scale Sets.

# Create health probes

A health probe allows your load balancer to monitor the status of your application. The probe dynamically adds or removes virtual machines from your load balancer rotation based on the machine response to health checks. When a probe fails to respond, the load balancer stops sending new connections to the unhealthy instance.

The following image shows how to create a health probe in the Azure portal. A custom HTTP health probe is configured to run on TCP port 80. The probe is defined to check the health of the virtual machine instances at 5-second intervals.

![Screenshot that shows how to create a health probe in the Azure portal.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-azure-load-balancer/media/add-health-probe-1d86fb2b.png)

### Things to know about health probes

There are two main ways to configure a custom health probe: **HTTP** and **TCP**.

- In an **HTTP probe**, the load balancer probes your back-end pool endpoints every 15 seconds. A virtual machine instance is considered _healthy_ if it responds with an HTTP 200 message within the specified timeout period (default is 31 seconds). If any status other than HTTP 200 is returned, the instance is considered _unhealthy_, and the probe fails.
    
- A **TCP probe** relies on establishing a successful TCP session to a defined probe port. If the specified listener on the virtual machine exists, the probe succeeds. If the connection is refused, the probe fails.
    
- To configure a probe, you specify values for the following settings:
    
    - **Port**: Back-end port
    - **URI**: URI for requesting the health status from the backend
    - **Interval**: Amount of time between probe attempts (default is 15 seconds)
    - **Unhealthy threshold**: Number of failures that must occur for the instance to be considered unhealthy
- A **Guest agent probe** is a third option that uses the guest agent inside the virtual machine. This option isn't recommended when an HTTP or TCP custom probe configuration is possible.

# Create load balancer rules

You can define load-balancing rules to specify how traffic is distributed to your back-end pools. Each rule maps a front-end IP address and port combination to a set of back-end IP address and port combinations.

![Screenshot that shows how to create load-balancing rules in the Azure portal.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-azure-load-balancer/media/add-load-balancer-rules-f4d9b188.png)

### Things to know about load-balancing rules

Let's take a closer look at how to configure load-balancing rules for your back-end pools.

- To configure a load-balancing rule, you need to have a frontend, backend, and health probe for your load balancer.
    
- To define a rule in the Azure portal, you configure several settings:
    
    - **IP version** (IPv4 or IPv6)
    - **Front-end IP address**, *_Port_, and **Protocol** (TCP or UDP)
    - **Back-end pool** and **Back-end port**
    - **Health probe**
    - **Session persistence**
- By default, Azure Load Balancer distributes network traffic equally among multiple virtual machines.
    
    Azure Load Balancer uses a five-tuple hash to map traffic to available servers. The tuple consists of the source IP address, source port, destination IP address, destination port, and protocol type. The load balancer provides stickiness only within a transport session.
    
- **Session persistence** specifies how to handle traffic from a client. By default, successive requests from a client go to any virtual machine in your pool.
    
    You can modify the session persistence behavior as follows:
    
    - **None (default)**: Any virtual machine can handle the request.
    - **Client IP**: Successive requests from the same client IP address go to the same virtual machine.
    - **Client IP and protocol**: Successive requests from the same client IP address and protocol combination go to the same virtual machine.
    
     Note
    
    Maintaining session persistence information is important for applications that implement a shopping cart. Can you think of other applications that might benefit from session persistence?
    
- Load-balancing rules can be used in combination with NAT rules.
    
    Consider a scenario where you use NAT from a load balancer's public address to TCP port 3389 on a specific virtual machine. By combining your NAT rule with load-balancing rules, you can enable remote desktop access from outside of Azure.

# Interactive lab simulation

## Lab scenario

Your organization is migrating hub and spoke network topologies to Azure. As the Azure Administrator you need to:

- Replicate the on-premises functionality in Azure.
- Configure virtual network peering and traffic routing.
- Implement load balancer and application gateway functionality.
- Test to ensure traffic management is flowing as intended.

## Architecture diagram

![Architecture diagram as explained in the text.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-azure-load-balancer/media/lab-06.png)

## Objectives

- **Task 1: Provision the lab environment.** In this task, you deploy four virtual machines into the same Azure region. The first two reside in a hub virtual network, while the remaining two reside in a separate spoke virtual network.
    - Review an [Azure Resource Manager template](https://github.com/MicrosoftLearning/AZ-104-MicrosoftAzureAdministrator/tree/master/Allfiles/Interactive%20Lab%20Simulation%20Files/06).
    - This template includes the virtual machines and virtual networks in the underlying architecture.
    - Use Azure PowerShell to install the Network Watcher extension on the Azure virtual machines.
- **Task 2: Configure the hub and spoke network topology.** In this task, you configure local peering between the virtual networks you deployed in the previous tasks in order to create a hub and spoke network topology.
    - Configure virtual network peering between the virtual networks.
    - Ensure forwarded traffic is allowed to facilitate routing between spoke virtual networks.
- **Task 3: Test transitivity of virtual network peering.** In this task, you test transitivity of virtual network peering by using Network Watcher.
    - Use Network Watcher to verify peered networks are reachable.
    - Use Network Watcher to verify unpeered networks are unreachable.
- **Task 4: Configure routing in the hub and spoke topology**. In this task, you configure and test routing between the two spoke virtual networks.
    - Enable IP forwarding on a virtual machine.
    - Install the remote access Windows feature with associated tools.
    - Create routing tables and associate them with the appropriate subnets.
    - Use Network Watcher to verify traffic routed through the virtual machine.
- **Task 5: Implement Azure Load Balancer**. In this task, you implement an Azure load balancer in front of the two Azure virtual machines in the hub virtual network.
    - Create a load balancer with a public IP address.
    - Create a back-end pool that includes the virtual machines.
    - Add a load balancing rule to alternate between virtual machines in the back-end pool.
    - Test to confirm that the load balancer is working correctly.
- **Task 6: Implement Azure Application Gateway**. In this task, you implement an Azure application gateway in front of the two Azure virtual machines in the spoke virtual networks.
    - Create a dedicated subnet for the application gateway.
    - Create an application gateway with a public IP address.
    - Configure the application gateway back-end pool to include the virtual machines.
    - Test to ensure traffic is balanced across the back-end virtual machines.

 Note

Select the thumbnail image to start the lab simulation. When you're done, be sure to return to this page so you can continue learning.

[![Screenshot of the simulation page.](https://learn.microsoft.com/en-us/training/wwl-azure/configure-azure-load-balancer/media/simulation-traffic-thumbnail.jpg)](https://mslabs.cloudguides.com/guides/AZ-104%20Exam%20Guide%20-%20Microsoft%20Azure%20Administrator%20Exercise%2010)

# Summary and resources

In this module, you learned about Azure Load Balancer and its features. Azure Load Balancer distributed workloads and network traffic across virtual machines, making applications more resilient and scalable. You learned about load balancer SKUs, back-end pools, load-balancing rules, session persistence, and health probes.

The main takeaways from this module are:

- Azure Load Balancer helps distribute network traffic across servers and resources.
    
- Load balancing can be used for inbound and outbound scenarios.
    
- There are public and internal load balancers.
    
- Load-balancing rules specify how traffic is distributed to your back-end pools.
    
- Back-end pools contain the IP addresses of the virtual NICs that are connected to your load balancer.
    
- Health probes dynamically add or remove virtual machines based on virtual machine health checks.
    

## Learn more with documentation

- [Azure Load Balancer documentation](https://learn.microsoft.com/en-us/azure/load-balancer/). This collection of articles is your starting point for all things load balancer.
    
- [Create a public load balancer for virtual machines in the Azure portal](https://learn.microsoft.com/en-us/azure/load-balancer/quickstart-load-balancer-standard-public-portal). This article reviews creating a public load balancer for a backend pool with two virtual machines.
    

## Learn more with self-paced training

- [Introduction to Azure Load Balancer](https://learn.microsoft.com/en-us/training/modules/intro-to-azure-load-balancer/). Learn what Azure Load Balancer does, how it works, and when you should choose to use Load Balancer as a solution
    
- [Improve application scalability and resiliency by using Azure Load Balancer (sandbox)](https://learn.microsoft.com/en-us/training/modules/improve-app-scalability-resiliency-with-load-balancer/). Learn about the different load balancers in Azure and how to choose the right Azure load balancer solution.
    
- [Load balance non-HTTP(S) traffic in Azure](https://learn.microsoft.com/en-us/training/modules/load-balancing-non-https-traffic-azure/). Learn the different load balancer options in Azure and how to choose and implement the right Azure solution for non-HTTP(S) traffic.

