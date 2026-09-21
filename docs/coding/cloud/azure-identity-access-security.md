---
title: Azure Identity, Access, and Security
---

# Azure Identity, Access, and Security

## Azure directory services

Azure directory services help manage identities (users, devices) and access to resources in the cloud and on-premises. The main services are **Microsoft Entra ID** (formerly Azure Active Directory) and **Microsoft Entra Domain Services**.

### Microsoft Entra ID

- **What is it?** Microsoft's cloud-based identity and access management service. It lets users sign in to Microsoft cloud apps (like Office 365 and Azure) and custom apps.
- **Who uses it?**
    - IT administrators (manage access to apps and resources)
    - App developers (add login and SSO to apps)
    - Users (manage their identity, reset passwords)
    - Anyone using Microsoft cloud services
- **What does it do?**
    - **Authentication:** verifies identity, supports password reset, multifactor authentication, smart lockouts.
    - **Single Sign-On (SSO):** use one account for many apps.
    - **Application management:** manage access to cloud and on-premises apps.
    - **Device management:** register and manage devices, enforce security policies.
- **Integration with on-premises AD:** you can connect your local Active Directory to Microsoft Entra ID using Microsoft Entra Connect. This syncs users between both systems for a seamless experience.

### Microsoft Entra Domain Services

- **What is it?** Provides managed domain services (domain join, group policy, LDAP, Kerberos/NTLM) in Azure, with no need to run your own domain controllers. Great for running legacy apps in the cloud.
- **How does it work?**
    - You create a managed domain with a unique name.
    - Azure deploys and manages 2 domain controllers for you, with no setup or patching needed.
    - One-way sync from Microsoft Entra ID to Domain Services (not back to Entra ID).
- **Integration:** works with your existing Microsoft Entra tenant. Users can sign into services and apps using their usual credentials. Lets you move older on-premises apps to the cloud easily.

## Azure authentication methods

Authentication is how Azure checks who you are before letting you access resources.

1. **Passwords:** the most basic method. Easy but less secure if used alone.
2. **Single Sign-On (SSO):** sign in once and get access to multiple apps and resources. Makes things easier for users and IT, since you only manage one identity. Security depends on the initial login.
3. **Multifactor Authentication (MFA):** adds another step after the password, like entering a code sent to your phone or using a fingerprint. Requires two or more of:
    - something you know (password, PIN),
    - something you have (phone, security key),
    - something you are (biometrics).

   Makes accounts much harder to hack.
4. **Passwordless authentication:** no passwords needed. Uses biometrics, devices, or security keys. More secure and more convenient. Options in Azure:
    - **Windows Hello for Business:** your PC plus PIN or biometrics.
    - **Microsoft Authenticator app:** your phone, with a notification and biometric or PIN.
    - **FIDO2 security keys:** hardware USB, Bluetooth, or NFC keys. No password to steal or guess.

## Azure external identities

External identities are people (like partners, customers, or vendors), devices, or services outside your organization. Azure lets you securely interact with these external users using Microsoft Entra External ID.

**What does it do?**

- Lets external users "bring their own identity": they sign in with their own accounts (like Google, Facebook, or their company login).
- You control what they can access, keeping your resources safe.

**Main capabilities**

1. **B2B collaboration:** invite partners, suppliers, or vendors to use your apps. They sign in with their own credentials and appear in your directory as guest users.
2. **B2B direct connect:** set up a two-way trust with another organization. Enables seamless collaboration (like shared Teams channels) without adding users to your directory.
3. **B2C (business to customer):** manage customer identities for your consumer-facing apps. Supports social logins (Google, Facebook, etc.). Use Azure AD B2C to handle sign-up, sign-in, and access for your customers.

**How does it work?** Invite external users as guests or allow them to sign up via social accounts. Control and review what guests can access. Remove access when it is no longer needed.

## Azure Conditional Access

Conditional Access is a security tool in Microsoft Entra ID that decides whether someone can access your resources based on specific conditions or "signals", such as who the user is, where they are signing in from, and what device they are using.

**How does it work?**

1. **Collect signals:** when someone tries to sign in, Azure looks at details like location, device, and app.
2. **Make a decision:** based on these signals, Azure decides if access should be allowed, blocked, or if extra steps (like MFA) are needed.
3. **Enforce:** the decision is put into action. Access is granted, blocked, or challenged with multifactor authentication.

**Examples**

- Allow access if the user is on a trusted device or location.
- Challenge for MFA if the user is in an unusual location.
- Block access if the device doesn't meet security standards.

**Why use Conditional Access?**

- **Flexible security:** set rules based on user roles, locations, devices, and apps.
- **Granular control:** choose when MFA is needed, which apps can be used, and which devices are allowed.
- **Protection:** block risky sign-ins, require secure devices, and keep your data safe.

## Azure role-based access control (RBAC)

Azure RBAC controls who can do what in your Azure environment by giving people only the access they need, no more and no less (the principle of **least privilege**).

**How does it work?**

- **Roles:** Azure provides built-in roles (like Reader, Contributor, Owner) and lets you create custom roles. Each role has specific permissions.
- **Assignments:** you assign people or groups to roles, and they get the permissions of that role.
- **Groups:** add users to a group with a specific role, and everyone in the group gets the same access.

**What can you control?**

- **Scope:** RBAC applies at different levels: management group (collection of subscriptions), subscription, resource group, or a specific resource.
- **Inheritance:** permissions given at a higher scope (like subscription) are inherited by lower scopes (resource groups, resources).

**Enforcement**

- RBAC is enforced by Azure Resource Manager when users interact with resources via the portal, CLI, PowerShell, and so on.
- RBAC controls access to Azure resources, not to the data inside your apps.

**Example:** you want one engineer to have Reader access to a storage blob, and another to have Owner access to a resource group. Assign the right roles, and Azure automatically gives them the permissions they need.

## Zero Trust model

Zero Trust is a cybersecurity approach that assumes no one and nothing is trusted by default, not even people or devices inside your company's network. Every access request is treated as if it could be coming from a potentially risky source.

**Key principles**

1. **Verify explicitly:** always check and confirm every user and device's identity, using all available data (like location, device health, and user behavior).
2. **Use least privilege access:** give users only the minimum access they need to do their job, and only for as long as needed.
3. **Assume breach:** expect that attackers may already be inside your network. Segment access, limit damage, and use analytics to detect threats and improve security.

**How is Zero Trust different?**

- **Old way:** trusted everything inside the company network.
- **Zero Trust:** treats everyone and every device as untrusted and requires authentication and authorization for every access, no matter where they are.

## Defense-in-depth

A security strategy that uses multiple layers of protection to keep your data safe. If one layer fails, the next layer is there to stop or slow down an attack.

1. **Physical security:** protects datacenters and hardware from physical threats (theft, unauthorized entry).
2. **Identity and access:** controls who can access resources, using tools like SSO and MFA, and logs changes and sign-ins.
3. **Perimeter:** protects against large-scale network attacks (like DDoS) using firewalls and attack detection.
4. **Network:** limits and secures connections between resources, blocks unnecessary traffic, and restricts internet access.
5. **Compute:** secures servers and virtual machines, keeps systems patched, installs malware protection, and controls who can access them.
6. **Application:** makes sure software is built securely, fixes vulnerabilities, protects secrets, and includes security in the design.
7. **Data:** protects business and customer data, controls access, and follows regulations to keep data confidential, accurate, and available.

## Microsoft Defender for Cloud

A security tool built into Azure that helps you protect your cloud, on-premises, hybrid, and multicloud environments. It gives you guidance, alerts, and tools to keep your resources safe.

**What does it do?**

- **Monitors** your environment for security issues and threats.
- **Assesses** your security posture and shows where you are vulnerable.
- **Secures** your resources with recommendations to fix weaknesses.
- **Defends** against attacks and sends alerts if something suspicious happens.

**Where does it work?**

- **Azure-native:** automatically protects many Azure services.
- **Hybrid and multicloud:** can also protect on-premises servers and resources in AWS or GCP (using Azure Arc and Defender plans).

**Key features**

- **Threat detection:** finds and alerts you to suspicious activity, attacks, and vulnerabilities across VMs, databases, containers, and more.
- **Security recommendations:** suggests how to fix and harden your resources, based on the Azure Security Benchmark.
- **Secure Score:** shows your overall security health at a glance and helps you improve it.
- **Policy management:** lets you set and enforce security policies across your organization.
- **Advanced protections:** includes things like just-in-time VM access, application allowlists, and adaptive controls.

**How does it protect?**

- **Continuously assesses** your environment with vulnerability scans for VMs, containers, and databases.
- **Groups recommendations** into controls, with a secure score to help you prioritize fixes.
- **Alerts and advanced threat protection** when attacks or suspicious activity are detected, with details and steps to respond.

## Practice Questions

??? question "1. What are Microsoft Entra ID and Entra Domain Services?"

    Entra ID is Microsoft's cloud identity and access management service (authentication, SSO, application and device management), formerly Azure Active Directory. Entra Domain Services provides managed domain services (domain join, group policy, LDAP, Kerberos/NTLM) without running your own domain controllers, useful for legacy apps.

??? question "2. What are the Azure authentication methods?"

    Passwords, single sign-on (SSO), multifactor authentication (MFA), and passwordless authentication (Windows Hello for Business, Microsoft Authenticator, FIDO2 security keys).

??? question "3. What three kinds of factors can MFA combine?"

    Something you know (password, PIN), something you have (phone, security key), and something you are (biometrics).

??? question "4. What is the difference between B2B collaboration, B2B direct connect, and B2C?"

    B2B collaboration invites partners as guest users who sign in with their own credentials. B2B direct connect sets up a two-way trust with another organization without adding users to your directory. B2C manages customer identities for consumer-facing apps, including social logins.

??? question "5. How does Conditional Access work?"

    It collects signals (user, location, device, app), decides whether to allow, block, or require extra steps like MFA, and then enforces that decision.

??? question "6. What are the scopes of Azure RBAC, and how does inheritance work?"

    Management group, subscription, resource group, and specific resource. Permissions given at a higher scope are inherited by lower scopes. RBAC controls access to Azure resources, not the data inside your apps.

??? question "7. What are the three principles of Zero Trust?"

    Verify explicitly, use least privilege access, and assume breach.

??? question "8. List the seven layers of defense-in-depth."

    Physical security, identity and access, perimeter, network, compute, application, and data.

??? question "9. What does Microsoft Defender for Cloud do?"

    It monitors for threats, assesses your security posture (Secure Score), recommends fixes, and defends with alerts across Azure, on-premises, and other clouds (AWS, GCP via Azure Arc).
