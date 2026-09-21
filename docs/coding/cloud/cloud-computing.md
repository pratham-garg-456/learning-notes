---
title: Cloud Computing
---

# Describe Cloud Computing

## Define cloud computing

Cloud computing is the delivery of computing services over the internet. These services can be rapidly provisioned and released with minimal management effort.

### Economies of scale

The cloud service provider's ability to do things efficiently, at a **lower cost per unit**, when operating at a large scale.

### Serverless architecture

The cloud provider dynamically **manages the allocation and provisioning** of servers, billed with a pay-as-you-go (PAYG) model. Resources are **stateless**, **ephemeral**, and often capable of being **triggered**.

It is more of a design pattern or execution model that can exist within PaaS.

Examples: Function-as-a-Service (Azure Functions), Azure Logic Apps, Azure Event Grid.

- **Azure Functions**
    - What it is: a tiny, purpose-built piece of code that runs only when you need it, with no servers to babysit.
    - Analogy: a motion-sensor light in your hallway. When you walk by, the light snaps on and then goes off again.
    - Example: you drop a photo into a "Photos" folder in Azure Blob Storage. Azure Functions sees the new file and instantly creates a thumbnail image for your website.
- **Azure Logic Apps**
    - What it is: a drag-and-drop workflow builder that links services together, with no coding required.
    - Analogy: a mailroom clerk with a checklist. When a letter arrives, they follow each step: stamp it, scan it, forward it to the right person, then log it in a spreadsheet.
    - Example: a new order comes into your online store. Logic Apps automatically sends an order-confirmation email to the customer, creates an invoice in your accounting system, and posts a notification in your Slack channel.
- **Azure Event Grid**
    - What it is: a super-fast event router that takes a single event and delivers it to one or many handlers.
    - Analogy: a post office that sorts incoming mail and drops copies into multiple mailboxes at once, so you and your teammates all get notified.
    - Example: someone uploads a PDF to Azure Storage. Event Grid grabs that "file-uploaded" event and delivers it to an Azure Function (to generate a preview image) and a Logic App (to update your CRM and send an alert email).

### Difference between PaaS and serverless

1. **Shared goals.** Both aim to eliminate the need to manage servers, provide scalability and high availability, and speed up development and deployment.
2. **PaaS in Azure.** Azure App Service, Azure SQL Database, and Azure Kubernetes Service (AKS) are examples of PaaS. You still define the app environment (like runtime and scaling rules), but Azure handles the OS, patching, and infrastructure.
3. **Serverless in Azure.** Serverless goes a step further. With services like Azure Functions and Azure Logic Apps, you don't even manage the app runtime. You just write code that responds to events, and Azure handles everything else, including auto-scaling from zero.

## Describe the shared responsibility model

When using a cloud provider, you are always responsible for:

- the information and data stored in the cloud,
- devices that are allowed to connect to your cloud (cell phones, computers, and so on),
- the accounts and identities of the people, services, and devices within your organization.

The cloud provider is always responsible for:

- the physical datacenter,
- the physical network,
- the physical hosts.

Your service model determines responsibility for things like operating systems, network controls, applications, and identity and infrastructure.

## Define cloud models

### Private

A cloud environment in your own datacenter, where the customer is responsible for the entire stack all the way down to the wire.

- Advantages: legacy support, control, and compliance.
- Disadvantages: greater cost and fewer of the benefits of a public cloud deployment. You are responsible for everything.

### Public

Everything runs on the cloud provider's hardware. Available to anyone who can purchase it.

- Advantages: scalability, agility, pay-as-you-go, no maintenance, and low skills needed.
- Disadvantage: not complete control over resources and security.

### Hybrid cloud

- Advantage: the benefits of both. Users can flexibly choose which services to keep in the public cloud and which to deploy to their private cloud infrastructure.

### Multi-cloud

Dealing with two (or more) public cloud providers and managing resources and security in both environments.

### Azure Arc

Azure Arc is a set of technologies designed to help manage cloud environments effectively. It is particularly beneficial for organizations that operate across public clouds, private clouds, hybrid configurations, and multi-cloud environments. With Azure Arc, users can manage their resources and security across different cloud providers, and extend Azure management capabilities to any infrastructure (on-premises, at the edge, or in other clouds). This unified management simplifies governance and compliance across diverse environments.

### Azure VMware Solution

Azure VMware Solution is for organizations that already run workloads on VMware in a private cloud. It allows them to migrate those workloads to Azure with seamless integration with Azure's services, using their existing VMware tools and processes. This supports a hybrid approach, running workloads both on-premises and in the cloud, and lets them add cloud features like advanced analytics and machine learning without re-architecting.

## Describe the consumption-based model

### Capital expenditure (CapEx)

Spending money upfront, typically one time, on physical infrastructure.

### Operational expenditure (OpEx)

Spending money on services or products over time. You are billed as you go.

### Compare pricing models

- **Pay-as-you-go:** pay for what you use.
- **Fixed price:** you provision resources and pay for those instances whether you use them or not. Benefit: predictable cost.

## Practice Questions

??? question "1. What is cloud computing?"

    The delivery of computing services over the internet, which can be rapidly provisioned and released with minimal management effort.

??? question "2. What are economies of scale?"

    The provider's ability to operate efficiently at a lower cost per unit when operating at a large scale.

??? question "3. What is serverless, and how does it differ from PaaS?"

    The provider dynamically manages allocation and provisioning of servers, billed pay-as-you-go, with stateless, ephemeral, event-triggered resources. With PaaS you still define the app environment (runtime, scaling rules). With serverless (Azure Functions, Logic Apps) you don't manage the runtime at all, and it can scale from zero.

??? question "4. What are you always responsible for in the shared responsibility model, and what is the provider always responsible for?"

    You: your data, the devices that connect, and the accounts and identities. Provider: the physical datacenter, physical network, and physical hosts. The service model determines the rest (operating systems, network controls, applications, identity and infrastructure).

??? question "5. Compare private, public, hybrid, and multi-cloud."

    Private: your own datacenter, full control but greater cost and you manage everything. Public: the provider's hardware, scalable and pay-as-you-go but less control. Hybrid: a mix of both. Multi-cloud: two or more public cloud providers.

??? question "6. What is the difference between CapEx and OpEx?"

    CapEx is upfront, typically one-time spending on physical infrastructure. OpEx is spending on services over time, billed as you go.
