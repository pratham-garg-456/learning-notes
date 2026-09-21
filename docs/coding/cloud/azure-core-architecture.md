---
title: Core Architectural Components of Azure
---

# Core Architectural Components of Azure

## Azure physical infrastructure

### Regions

A region contains at least one, but potentially multiple, datacenters that are nearby and networked together with a low-latency network.

### Availability zones

Availability zones are **physically separate datacenters** within an Azure region. Each availability zone is made up of one or more datacenters equipped with **independent power, cooling, and networking**. An availability zone is set up to be an isolation boundary: if one zone goes down, the other continues working. Availability zones are connected through high-speed, **private fiber-optic networks**.

!!! tip
    To ensure resiliency, a minimum of three separate availability zones are present in all availability zone-enabled regions. However, not all Azure regions currently support availability zones.

### Region pairs

A relationship between **two Azure regions** within the same geographical region for disaster recovery purposes.

- At least 300 miles apart
- Chosen by Microsoft

**Advantages**

- If an extensive Azure outage occurs, one region out of every pair is prioritized to restore.
- Planned Azure updates are rolled out to paired regions one region at a time to minimize downtime and risk of application outage.
- Data continues to reside within the same geography as its pair (except for Brazil South) for tax and law-enforcement jurisdiction purposes.

!!! tip
    Most regions are paired in two directions (each is the backup for the region that provides a backup for it). However, some regions, such as West India and Brazil South, are paired in only one direction.

### Sovereign regions

Physical and logical network-isolated instances of Azure. Sovereign regions are instances of Azure that are isolated from the main instance of Azure. You may need to use a sovereign region for **compliance or legal purposes**.

## Azure management infrastructure

The management infrastructure includes Azure resources and resource groups, subscriptions, and accounts.

### Management groups

Management groups are a way to manage many Azure subscriptions together, so you can set rules and permissions once and have them apply everywhere you need. You can organize management groups in layers (nested) for even more control.

**Use cases**

1. **Apply rules and policies easily.** Say you want to make sure all virtual machines are only set up in the US West region. You can set this rule (policy) at the management group level.
2. **Give access to many things at once.** Suppose you have several subscriptions. Instead of giving someone permission for each subscription separately, you can move them all under a management group and give permissions once at the management group level. Everyone under that group (including all resources and subscriptions) automatically gets the access.

**Facts**

- You can have up to **10,000 management groups** in a single Azure directory (tenant).
- You can nest management groups up to **six levels deep** (not counting the root or subscription level).
- Each management group and each subscription can have **only one parent**.

### Azure subscriptions

- A container that holds resource groups and resources.
- Used to organize, manage, and pay for your use.

An Azure subscription is a way to **organize, manage, and pay for Azure resources, and control who can access them**. You can have one or many subscriptions, depending on your needs.

**Why create more than one subscription?**

1. **Environments:** separate environments (development, testing, production) to isolate resources.
2. **Organizational structures:** different teams or departments.
3. **Billing:** to track costs separately.
4. The subscription limit is reached.

### Resource groups

- A resource group is a container that holds a set of **related resources**.
- When you provision something in Azure, you must put it into a resource group.
- A resource group can have many resources, but each resource can only be in one resource group at a time.
- You can move some resources to another group, but once you do, they leave the old group.
- You **cannot** put one resource group inside another (no nesting).

**How should you use them?** Group resources in ways that make management easier for you.

- Put all resources for a temporary project in one group so you can delete them all at once when you are done.
- Group resources by who needs access, so you can easily set permissions.

### Resources

Resources are the things you create and use in Azure, like virtual machines, databases, networks, and apps.

## Practice Questions

??? question "1. What is an availability zone, and how many are in an enabled region?"

    A physically separate datacenter (or group of datacenters) within an Azure region, with independent power, cooling, and networking, connected by high-speed private fiber. If one zone goes down the others continue working. A minimum of three zones exist in every availability-zone-enabled region, but not all regions support them.

??? question "2. What is a region pair and why does it matter?"

    Two Azure regions within the same geography (at least 300 miles apart, chosen by Microsoft) for disaster recovery. Updates roll out one region at a time, and data stays within the same geography for tax and law-enforcement jurisdiction.

??? question "3. What is a sovereign region?"

    A physically and logically network-isolated instance of Azure, used for compliance or legal purposes.

??? question "4. What are management groups used for, and what are their limits?"

    Managing many subscriptions together so policies and permissions are set once. Up to 10,000 per tenant, nested up to six levels deep, and each group or subscription has only one parent.

??? question "5. Why create more than one Azure subscription?"

    To separate environments, organizational structures, or billing, or when a subscription limit is reached.

??? question "6. What are the rules for resource groups?"

    Every resource must be in a resource group, each resource can be in only one group at a time, you can move some resources between groups, and you cannot nest resource groups.
