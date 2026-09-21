---
title: Azure Compute and Networking Services
---

# Azure Compute and Networking Services

## Azure Virtual Machines

VMs are computers that exist in the cloud. Just like a physical computer, you can customize all of the software running on your VM.

**Benefits**

- **Control:** full control over the operating system and software.
- **Flexibility:** you can easily create, delete, or change VMs as needed.
- **Cost-effective:** you only pay for what you use, which is great for businesses with varying workloads.

### Scale VMs in Azure

VMs can be grouped together for better performance and reliability.

**Scale sets** let you create and manage a group of identical, load-balanced VMs (which automatically adjust the number of VMs based on demand or schedule). With virtual machine scale sets, you can build large-scale services for areas such as compute, big data, and container workloads.

**Availability sets** ensure that VMs stagger updates and have **varied power and network connectivity**, preventing you from losing all your VMs with a single network or power failure. You create an availability set and put multiple VMs into it, and Azure's placement algorithm spreads them across fault domains and update domains automatically.

1. **Update domain:** VMs are split into groups called update domains. Only one update domain is updated or rebooted at a time during maintenance, so your other VMs keep running.
2. **Fault domain:** VMs are also split into fault domains, meaning each group is connected to different power sources and network switches. If there is a hardware or power failure, only the VMs in one fault domain are affected.

!!! tip
    By default, an availability set splits your VMs across up to three **fault domains**.

**What an availability set is NOT.** It is not a cross-datacenter or cross-zone solution. Availability sets operate within a single Azure datacenter or region and do not protect against an entire datacenter outage. For that you need availability zones or cross-region replication and disaster recovery.

### VM use cases

- During **software development and testing**.
- When you need to run applications without investing in physical servers.
- For **disaster recovery**, allowing you to quickly switch to cloud resources if something goes wrong with your main systems.

### Resource requirements

- Virtual disk
- Virtual network
- Network interface (virtual NIC)
- Network security group
- Public IP address

## Azure Virtual Desktop (AVD)

A desktop and app virtualization service that runs in Microsoft Azure. It lets you use a cloud-hosted version of Windows from any location.

**Key features**

- **Security:**
    - Centralized security management using Microsoft Entra ID.
    - Can use multifactor authentication to protect sign-ins.
    - You control who can access what using role-based access (RBAC).
    - Since data and apps stay in the cloud, there is less risk if a device gets lost or stolen.
- **Multi-user support:**
    - Lets several people use the same Windows 10 or 11 virtual machine at once (multi-session).
    - Gives a consistent Windows experience and supports more applications than some server-based options.

**Quick analogies**

- VM = your own private laptop in the cloud.
- AVD = an office building where many people can come in and use identical workstations, and the building manager handles who sits where, maintenance, and scaling.

## Azure Containers

- If you want to **run multiple instances of an application on a single host machine**, containers are an excellent choice.
- Unlike virtual machines, **containers do not require a full operating system** for each instance. They share the host OS kernel, making them lightweight and faster to start, stop, and restart.

### Compare virtual machines to containers

- A VM **virtualizes the hardware**, while containers **virtualize the OS**.
- If you need complete control of the environment, choose a VM. If you need portability and performance, choose containers.

### Azure Container Instances (PaaS)

Lets you upload your containers and then the service runs the containers for you.

### Azure Container Apps (PaaS)

Similar to Container Instances, but with more features for apps that need scaling and flexibility:

- **Load balancing** (spreads incoming traffic across instances).
- **Auto-scaling:** can automatically increase or decrease the number of running containers as needed.
- Great for microservices, APIs, and event-driven apps.

!!! tip
    Best for: when you need fast deployment **plus** the ability to handle varying traffic or workloads.

### Azure Kubernetes Service (AKS)

- **What is it?** A managed Kubernetes service for advanced container orchestration.
- **Key features:**
    - Manages the full lifecycle of many containers (scheduling, scaling, networking, updates).
    - Handles complex applications made of many containers (a fleet).
    - More control and flexibility, but requires more setup and understanding of Kubernetes.

!!! tip
    Best for: large, complex, or production-grade applications that need advanced management and orchestration.

### Using containers in your solutions: microservice architecture

Microservice architecture means breaking your solution into small, independent components (microservices), and each microservice can run in its own container. For example, a website might have a container for the front end (UI), one for the back end (API or business logic), and one for the storage or database service.

**Benefits (key points for AZ-900)**

1. **Independence:** each part is isolated. You can update, maintain, or replace one part without affecting the others.
2. **Scalability:** you can scale just the part that needs it. If the back end is getting a lot of requests, add more back-end containers without changing the front end or storage.
3. **Flexibility:** you can change or upgrade one component (like switching databases or updating the UI) without disrupting the whole solution.
4. **Agility:** teams can work on different parts independently, making development, testing, and deployment faster and safer.

See also [Monoliths and Microservices](../../chapter-3/monoliths-and-microservices.md) and [Virtual Machines (VMs) and Containers](../../chapter-4/virtual-machines-vms-and-containers.md).

## Azure Functions

Azure Functions is Microsoft's serverless compute service for running small pieces of code (functions) in response to events. You write the code and Azure runs it when needed without you managing servers.

## Application hosting options: Azure App Service (PaaS)

An HTTP-based service for **building, hosting, and scaling web apps, background jobs, mobile back ends, and RESTful APIs** in any programming language.

**Key features**

- **Automatic scaling** and **high availability** (built-in load balancing).
- Supports continuous deployment (CD) from GitHub, Azure DevOps, or any Git repository.
- **Integrated management:** deployment, security, and scaling are built in.
- **Supports multiple languages:** .NET, .NET Core, Java, Ruby, Node.js, PHP, Python.

**Types of apps you can host**

| App Service type | Description |
| --- | --- |
| **Web Apps** | ASP.NET, ASP.NET Core, Java, Ruby, Node.js, PHP, or Python. You can choose either Windows or Linux as the host operating system. |
| **API Apps** | Host REST-based APIs with full Swagger support and the ability to package and publish your API in Azure Marketplace. APIs can be consumed by any HTTP/HTTPS client. |
| **WebJobs** | Run background tasks (scripts or programs) alongside your app. Can be scheduled or triggered. |
| **Mobile Apps** | Backend for mobile apps (iOS/Android), with features like cloud data storage, authentication (Microsoft, Google, X, Facebook), and push notifications. |

## Azure Virtual Networking

Azure Virtual Networks (VNets) let you connect and isolate your Azure resources (VMs, databases, web apps, etc.) in a secure, scalable, and flexible way, similar to setting up a network in your own datacenter.

### Key capabilities

1. **Isolation and segmentation**
    - You can create multiple, isolated virtual networks in Azure.
    - Each VNet has its own private IP address space (not visible on the internet).
    - You can split a VNet into **subnets** to further organize and secure resources.
    - Name resolution (DNS) can be handled by Azure or by your own DNS servers.
2. **Internet communications**
    - Assign a **public IP** or use a **public load balancer** for internet access.
    - **Public endpoints:** public IP, accessible worldwide.
    - **Private endpoints:** private IP, only accessible inside the VNet.
3. **Communicate between Azure resources**
    - VNets allow secure communication between Azure resources (VMs, databases, App Services).
    - **Service endpoints:** securely connect VNets to Azure services like SQL or Storage for better security and routing.
4. **Communicate with on-premises resources**
    - VNets can connect your on-premises network and Azure.
    - **Point-to-site VPN:** individual computers connect securely to Azure.
    - **Site-to-site VPN:** your entire on-premises network connects to Azure.
    - **ExpressRoute:** a dedicated, private connection (not over the public internet), for higher security and bandwidth.
5. **Route network traffic**
    - Azure automatically routes traffic between subnets, VNets, and the internet.
    - **Custom route tables:** you can control and override routing for advanced scenarios.
    - **BGP (Border Gateway Protocol):** used for advanced routing, especially with VPN and ExpressRoute.
6. **Filter network traffic**
    - **Network security groups (NSGs):** a set of rules to allow or block traffic to and from resources based on IP, port, protocol, and so on.
    - **Network virtual appliances:** special VMs that act as firewalls or WAN optimizers.
7. **Connect virtual networks**
    - **VNet peering:** directly connect two VNets (even in different regions). Traffic is secure and private and never leaves Microsoft's backbone.
    - **User-defined routes (UDRs):** define custom routing between subnets or VNets for more control.

### Summary table

| Feature / term | Description |
| --- | --- |
| Virtual Network (VNet) | Isolated network in Azure. |
| Subnet | Subdivision of a VNet for better organization and security. |
| Public endpoint | Public IP, accessible from the internet. |
| Private endpoint | Private IP, accessible only within the VNet. |
| VNet peering | Connects VNets together privately and securely. |
| Site-to-site VPN | Connects an entire on-premises network to Azure. |
| Point-to-site VPN | Connects an individual device to Azure. |
| ExpressRoute | Dedicated, private connection to Azure (not over the public internet). |
| NSG | Set of rules to filter network traffic. |
| Route table / UDR | Customizes routing of traffic within and between VNets. |
| Service endpoints | Securely connect a VNet to Azure services (for example SQL, Storage). |

## Azure virtual private networks (VPN)

VPNs let you connect different private networks securely over the internet using encrypted tunnels. This keeps your data safe from hackers and snooping.

### VPN gateways

- A VPN gateway is a special device in Azure that manages these secure connections.
- It sits in its own subnet and can:
    - connect your company's network to Azure (site-to-site),
    - connect individual computers to Azure (point-to-site),
    - connect different Azure networks to each other.
- Each virtual network (VNet) can have only one VPN gateway deployed inside it.
- That single gateway can still connect to many different remote endpoints (other VNets or on-premises datacenters). In other words, one gateway can host multiple VPN connections.

In Azure, regardless of the VPN type, the method of authentication employed is a preshared key.

**Types of VPN gateways**

- **Policy-based:** decides which data to encrypt based on IP addresses. Each packet is checked against a list.
- **Route-based:** uses network routing to decide which packets to send through the tunnel. Preferred for most cases and more flexible.

**High availability and resilience**

- **Active/Standby:** two VPN gateways are set up, but only one is working at a time. If one fails, the other takes over quickly.
- **Active/Active:** both gateways work at the same time for even better reliability.
- **ExpressRoute failover:** if your main private connection (ExpressRoute) fails, a VPN gateway can keep you connected over the internet.
- **Zone-redundant gateways:** in some regions, gateways can be set up across different physical zones for extra protection against outages.

## Azure ExpressRoute

Azure ExpressRoute lets you connect your network straight to Microsoft's cloud with a private, secure, and reliable link, giving you better speed, security, and global reach than a normal internet connection.

**Key points**

- **Private connection:** your data goes through a secure, private line instead of the public internet, making it faster, more reliable, and more secure.
- **ExpressRoute circuit:** each location (like an office or datacenter) gets its own connection, called a circuit.
- **Connects to cloud services:** you can use ExpressRoute to access services like Azure, Office 365, and Dynamics 365 directly.
- **Global reach:** you can link offices in different parts of the world together, allowing them to communicate securely.
- **Dynamic routing:** it uses BGP to automatically find the best path for your data.
- **Redundancy:** built-in backup connections make sure your link stays up even if something fails.

**Connection options**

- **Cloud exchange colocation:** connect from a datacenter located at a cloud exchange (like an ISP).
- **Point-to-point Ethernet:** direct connection between your place and Microsoft.
- **Any-to-any:** connect multiple offices and datacenters to Azure through your wide area network.
- **Direct from ExpressRoute sites:** connect straight into Microsoft's network from special locations, with very high speeds.

**Security**

- Data never touches the public internet, so it is safer from threats.
- Some things (like DNS lookups) may still use the internet.

## Azure DNS

Azure DNS is a service that helps you manage domain names and DNS records using Microsoft Azure's cloud.

**What does Azure DNS do?**

- It hosts your DNS domains and answers requests for your domain names (like `yourcompany.com`).
- You can manage DNS records (like A, CNAME, MX records) for your websites and apps using Azure tools.

**Benefits**

- **Reliable and fast:** uses Microsoft's global network, so your domain gets fast, reliable responses.
- **Secure:** you control who can change DNS settings with Azure's role-based access. You can also track changes and lock resources to prevent mistakes.
- **Easy to use:** manage DNS like your other Azure services, using the Azure portal, PowerShell, CLI, or APIs.
- **Custom networks:** you can use custom domain names inside private virtual networks.
- **Alias records:** you can link DNS records to Azure resources (like public IPs) so if an address changes, DNS updates automatically.

**Important note:** you can't buy a domain name directly from Azure DNS. You need to buy it elsewhere, then use Azure DNS to manage its records.

See also [Domain Name System (DNS)](../../chapter-1/domain-name-system-dns.md).

## Practice Questions

??? question "1. What is the difference between availability sets and scale sets?"

    Scale sets create and manage a group of identical, load-balanced VMs that automatically adjust in number based on demand or schedule. Availability sets spread VMs across fault domains (separate power and network) and update domains (staggered maintenance) so a single failure or update doesn't take them all down.

??? question "2. Why aren't availability sets a datacenter-level solution?"

    They operate within a single datacenter or region, so they don't protect against a whole datacenter outage. For that you need availability zones or cross-region replication.

??? question "3. How do containers differ from VMs, and when do you choose each?"

    A VM virtualizes the hardware, containers virtualize the OS and share the host kernel, so they are lightweight and start fast. Choose a VM for complete control of the environment, and containers for portability and performance.

??? question "4. What are Container Instances, Container Apps, and AKS best for?"

    Container Instances: upload containers and the service runs them. Container Apps: microservices, APIs, and event-driven apps with load balancing and auto-scaling. AKS: large, complex, production-grade apps needing advanced Kubernetes orchestration.

??? question "5. What benefits does a container-based microservice architecture give?"

    Independence, scalability of just the part that needs it, flexibility to change one component without disrupting the rest, and agility for teams working independently.

??? question "6. What are the four App Service app types?"

    Web Apps, API Apps, WebJobs, and Mobile Apps.

??? question "7. What is the difference between a public and a private endpoint?"

    A public endpoint has a public IP and is accessible from anywhere. A private endpoint has a private IP and is accessible only inside the VNet.

??? question "8. Compare site-to-site VPN, point-to-site VPN, and ExpressRoute."

    Site-to-site connects an entire on-premises network to Azure, point-to-site connects an individual computer, both over the internet through encrypted tunnels. ExpressRoute is a dedicated private connection that doesn't use the public internet.

??? question "9. What does Azure DNS do, and what can't it do?"

    It hosts DNS domains and manages DNS records using Azure's global network and role-based access. You can't buy a domain name from Azure DNS.
