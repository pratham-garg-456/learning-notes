---
title: Azure Cost Management
---

# Cost Management in Azure

Official module: [Describe cost management in Azure](https://learn.microsoft.com/en-us/training/modules/describe-cost-management-azure/).

## Factors that can affect costs in Azure

Azure charges you based on how you use its cloud resources. Several factors can change how much you pay:

1. **Resource type.** Different resources (VMs, storage, databases, etc.) have different prices. Settings like performance tier, redundancy, and region affect the cost.
2. **Consumption (usage).**
    - Pay-as-you-go: you pay for what you use each billing cycle.
    - Reserved capacity: commit to use resources for 1 or 3 years to get discounts.
    - More usage means higher cost. Less usage means lower cost.
3. **Maintenance.** Unused resources can still cost money. Extra resources (storage, networking) may stay after deleting a VM, so clean up regularly to avoid paying for things you don't need.
4. **Geography.** Azure resources are priced differently in different regions due to local factors (power, labor, taxes). Network traffic costs also depend on regions: moving data between far apart regions costs more.
5. **Network traffic.** Some inbound data is free. Outbound data (leaving Azure) has costs based on zones (groups of regions). Moving data between continents is more expensive.
6. **Subscription type.** Free trials and certain subscription types include free usage or credits. Some subscriptions have usage allowances that lower costs.
7. **Azure Marketplace.** Buying third-party solutions or services may include extra fees set by vendors, on top of normal Azure costs.

## Pricing calculator vs Total Cost of Ownership (TCO) calculator

### Pricing calculator

- **Purpose:** estimate the cost of provisioning Azure resources.
- **Use:** build a solution or scenario, select resources (VMs, storage, networking, etc.), and get a price estimate.
- **Focus:** cost of Azure resources only.
- **Note:** for planning only. You won't be charged and nothing is actually created.

### TCO calculator

- **Purpose:** compare the costs of running your infrastructure on-premises vs in Azure.
- **Use:** enter details about your current setup (servers, databases, storage, network traffic) and assumptions (power, IT labor).
- **Focus:** shows cost differences between your own datacenter and Azure for the same workload.
- **Note:** helps you see savings or changes if you move to the cloud.

**In short:** the pricing calculator estimates Azure resource costs for new or planned deployments. The TCO calculator compares your current on-premises costs to what it would cost to run the same setup in Azure.

## Microsoft Cost Management tool

Microsoft Cost Management helps you track, manage, and control your spending in Azure. It makes sure you know where your money is going and helps avoid surprises on your bill.

**What does it do?**

- **Cost analysis:** gives you visual reports of your Azure costs by billing cycle, region, resource, and so on. Lets you see cost trends over time (monthly, quarterly, yearly).
- **Cost alerts:** notifies you when your spending reaches certain limits. Types of alerts:
    - **Budget alerts:** warn you when you hit your spending or usage limits.
    - **Credit alerts:** notify you when you use up your Azure credit (for Enterprise Agreements).
    - **Department spending quota alerts:** let departments know when they reach preset spending amounts.
- **Budgets:** lets you set spending limits for subscriptions, resource groups, or services. Triggers alerts and can even automate actions (like suspending resources) when limits are reached.

## Purpose of tags

Tags are labels (metadata) you add to your Azure resources to help keep things organized as your cloud usage grows. Each tag is a name-value pair (like `Owner: John` or `Environment: Prod`), and you can add multiple tags to each resource.

**Why use tags?**

- **Resource management:** easily find, group, and manage resources by workload, environment, owner, and so on.
- **Cost management:** track spending by groups (like departments or projects), report costs, and optimize budgets.
- **Operations management:** group resources by how critical they are to the business, helping you set service-level agreements (SLAs).
- **Security:** classify data by security level (for example public, confidential).
- **Governance and compliance:** identify resources that meet regulatory requirements (like ISO 27001) and enforce standards (for example require Owner tags).
- **Workload optimization and automation:** tag resources by application or workload for easier automation and visualization in tools like Azure DevOps.

**Managing tags**

- You can add, edit, or delete tags using the Azure portal, PowerShell, CLI, templates, or the API.
- Use Azure Policy to enforce tagging rules (for example require tags on new resources).
- Tags don't inherit between resource groups, subscriptions, and resources. You control where tags are applied.

## Practice Questions

??? question "1. Name factors that affect Azure costs."

    Resource type, consumption (pay-as-you-go or reserved capacity), maintenance (unused resources still cost money), geography, network traffic, subscription type, and Azure Marketplace purchases.

??? question "2. What is the difference between the pricing calculator and the TCO calculator?"

    The pricing calculator estimates the cost of Azure resources you plan to provision. The TCO calculator compares the cost of running your current on-premises infrastructure with running the same workload in Azure.

??? question "3. What can Microsoft Cost Management do?"

    Cost analysis reports, cost alerts (budget, credit, and department spending quota alerts), and budgets that can trigger alerts or automated actions when limits are reached.

??? question "4. What is a tag, and why use one?"

    A name-value label (like `Owner: John`) on a resource. Tags help with resource management, cost tracking, operations, security classification, governance and compliance, and automation.

??? question "5. Do tags inherit?"

    No. Tags don't inherit between resource groups, subscriptions, and resources. You control where they are applied, and Azure Policy can enforce tagging rules.
