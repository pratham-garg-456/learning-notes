---
title: Azure Storage Services
---

# Azure Storage Services

## Azure storage accounts

- A special space in Azure where you can store all kinds of data (files, tables, blobs, and so on).
- Each storage account gets a unique name so your data can be accessed from anywhere in the world using HTTP or HTTPS.

**Security and reliability:** data is safe, always available, durable, and can scale massively.

### Types of storage accounts

- **Standard general-purpose v2:** supports blobs, files, queues, and tables. The most common and recommended for general use.
- **Premium block blobs:** blob storage with high performance needs.
- **Premium file shares:** high-performance file storage (SMB and NFS).
- **Premium page blobs:** page blobs only.

### Redundancy options

These decide how your data is copied for safety:

- LRS: Locally Redundant Storage
- ZRS: Zone-Redundant Storage
- GRS: Geo-Redundant Storage
- RA-GRS: Read-Access Geo-Redundant Storage
- GZRS: Geo-Zone-Redundant Storage
- RA-GZRS: Read-Access Geo-Zone-Redundant Storage

### Naming your storage account

- The name must be 3 to 24 characters, only lowercase letters and numbers.
- It must be unique across all of Azure.

### Endpoints

Each service gets a URL using your account name:

- Blob: `https://<storage-account-name>.blob.core.windows.net`
- Data Lake: `https://<storage-account-name>.dfs.core.windows.net`
- Files: `https://<storage-account-name>.file.core.windows.net`
- Queues: `https://<storage-account-name>.queue.core.windows.net`
- Tables: `https://<storage-account-name>.table.core.windows.net`

## Azure storage redundancy

Azure always keeps multiple copies of your data to protect it from failures or disasters, so your data is safe and available even if something goes wrong with the hardware or network.

1. **Locally Redundant Storage (LRS)**
    - Stores 3 copies of your data in one datacenter, synchronously.
    - The cheapest option; protects against hardware failure.
    - If the whole datacenter is lost (fire, flood), your data may be lost.
2. **Zone-Redundant Storage (ZRS)**
    - Stores copies across 3 different **availability zones** in the same region, synchronously.
    - Higher durability: if one zone fails, your data is still safe and accessible.
    - Good for high availability and keeping data within a region.
3. **Geo-Redundant Storage (GRS)**
    - Copies your data to another region (Azure region pairs, fixed) far away.
    - Protects against disasters that affect an entire region.
    - Your data in the backup region is only available after a failover.
4. **Geo-Zone-Redundant Storage (GZRS)**
    - Combines ZRS (across zones in the primary region) with geo-replication to a secondary region.
    - Maximum durability, performance, and disaster recovery.
5. **Read-Access GRS (RA-GRS) and Read-Access GZRS (RA-GZRS)**
    - Same as GRS/GZRS, but lets you read data from the backup region even if the primary is still working.

**What to consider**

- LRS is cheapest but has less protection.
- ZRS is good for high availability within a region.
- GRS/GZRS protect against big disasters.
- RA-GRS/RA-GZRS let you read from the backup region at any time.

!!! tip
    The interval between the most recent writes to the primary region and the last write to the secondary region is known as the recovery point objective (RPO). The RPO indicates the point in time to which data can be recovered. Azure Storage typically has an RPO of less than 15 minutes, although there is currently no SLA on how long it takes to replicate data to the secondary region.

## Azure storage services (PaaS)

**Benefits of Azure Storage**

- **Durable and highly available:** your data is safe and always accessible, even if hardware fails.
- **Secure:** data is encrypted; you control access.
- **Scalable:** grows with your needs.
- **Managed:** Azure takes care of maintenance and updates.
- **Accessible:** reach your data from anywhere, using various tools and languages.

### 1. Azure Blobs

- Stores any kind of unstructured data (text, binary, images, videos, logs).
- Great for big data and analytics (through Data Lake Storage Gen2).
- Can handle thousands of uploads at once.
- Supports different access tiers:
    - **Hot:** for data you need often (online), higher storage cost.
    - **Cool:** for data you need sometimes (online).
    - **Cold:** for data you rarely need (online).
    - **Archive:** for data you almost never need (**offline**), high access cost.

### 2. Azure Files

- Managed file shares you can access from anywhere, like a network drive.
- Works with Windows, Linux, and macOS.
- Uses SMB and NFS protocols.
- No need to manage hardware or servers.

### 3. Azure Queues

- Stores messages for communication between app parts.
- Useful for handling tasks in the background or asynchronously.
- Can work with millions of messages.

### 4. Azure Disks

- Block storage for Azure virtual machines (VMs).
- Like a virtual hard drive, but managed and more reliable.

### 5. Azure Tables

- Stores structured, non-relational (NoSQL) data.
- Great for large amounts of simple data.

## Azure data migration options

Options that help you move your data, apps, and infrastructure to Azure.

### 1. Azure Migrate

- A service that helps you move your servers, databases, and apps from your own datacenter to Azure.
- It has tools for:
    - **Discovery and assessment:** checks what you have and helps plan the move.
    - **Server migration:** moves virtual machines, physical servers, and public cloud VMs to Azure.
    - **Database migration:** helps move databases to Azure SQL or managed instances.
    - **App migration:** moves web apps (like .NET or PHP) to Azure App Service.
- It is a single portal to start, track, and manage your migration.

### 2. Azure Data Box

- A physical device sent to you to move large amounts of data (up to 80 TB) quickly and securely, especially if your internet is slow or unavailable.
- You copy your data onto the Data Box, send it back, and Microsoft uploads it to Azure for you.
- Good for: one-time big migrations, moving offline media libraries, bulk transfers followed by online updates, and disaster recovery and exporting data out of Azure if needed.

## Azure file movement options

Tools that help you move or manage individual files or small groups of files in Azure, not just large migrations.

### 1. AzCopy

- A command-line tool for copying files to and from Azure Storage.
- You can upload, download, and sync files between storage accounts.
- Sync is one-way (from source to destination), not two-way.

### 2. Azure Storage Explorer

- A desktop app (Windows, Mac, Linux) with a graphical interface.
- Lets you upload, download, and manage files in Azure Storage.
- Uses AzCopy behind the scenes for file operations.

### 3. Azure File Sync

- Keeps your on-premises Windows file server and Azure Files in sync.
- Bi-directional sync: changes in either location are updated in both places.
- Works with standard Windows file protocols (SMB, NFS, FTPS).
- Supports cloud tiering: keeps frequently used files local, stores others in the cloud.

## Practice Questions

??? question "1. What are the rules for naming a storage account?"

    3 to 24 characters, only lowercase letters and numbers, and unique across all of Azure.

??? question "2. Compare LRS, ZRS, GRS, and GZRS."

    LRS: 3 copies in one datacenter, cheapest, but a datacenter loss can lose data. ZRS: copies across 3 availability zones in one region. GRS: copies to a paired region far away, available after a failover. GZRS: ZRS in the primary region plus geo-replication to a secondary region, for maximum durability.

??? question "3. What do the RA versions add?"

    RA-GRS and RA-GZRS let you read data from the backup region even while the primary is still working.

??? question "4. What are the blob access tiers?"

    Hot (often used, online), Cool (sometimes), Cold (rarely), and Archive (almost never, offline, with high access cost).

??? question "5. What are the five Azure storage services?"

    Blobs (unstructured data), Files (managed file shares over SMB/NFS), Queues (messages between app parts), Disks (block storage for VMs), and Tables (NoSQL structured data).

??? question "6. When do you use Azure Migrate versus Azure Data Box?"

    Azure Migrate moves servers, databases, and apps from your datacenter to Azure with discovery, assessment, and migration tools. Data Box is a physical device (up to 80 TB) for moving large amounts of data when the internet is slow or unavailable.

??? question "7. How do AzCopy, Storage Explorer, and File Sync differ?"

    AzCopy is a command-line tool with one-way sync. Storage Explorer is a graphical desktop app that uses AzCopy behind the scenes. File Sync keeps an on-premises Windows file server and Azure Files in sync in both directions, with cloud tiering.
