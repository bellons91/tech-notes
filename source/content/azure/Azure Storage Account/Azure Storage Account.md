---
tags:
  - azure
  - cloud
  - az-900
  - az-204
  - storage
  - azure-storage-account
  - iaas
---

Cloud storage solution, **IaaS**. It's an entry point to access data over HTTP or HTTPS.

Using storage accounts, data is secure, highly available, durable, and scalable.

You can even use Azure Storage publish static content (see [[Static website hosting with Azure Storage]]).

You can use it to create a Virtual Machine with consistent disks and storage.

You create a Storage Account in a specific region (to enable redundancy).

Azure Storage Account allows you to use:

- [[Azure Files]]
- [[Azure Blob Storage]]
- [[Azure Table Storage]]
- [[Azure Queue Storage]]

You can also use [[hierarchical-namespaces]].

## Storage Account Tiers

There are several tiers, each of them with specific usage and supported services.

### Standard general-purpose v2

It's the type best for blobs, file shares, queues, and tables.

Recommended for the most basic scenarios.

Supported services:

- [[Azure Blob Storage]]
- [[Azure Queue Storage]]
- [[Azure Table Storage]]
- [[Azure Files]]

It supports all the redundancy options:

- Locally Redundant Storage (LRS) (see :[[Azure Storage Redundancy Types#Locally Redundant Storage (LRS)]])
- Zone-Redundant Storage (ZRS) (see: [[Azure Storage Redundancy Types#Zone-Redundant Storage (ZRS)]])
- Geo-Redundant Storage (GRS) (see: [[Azure Storage Redundancy Types#Geo-Redundant Storage (GRS)]])
- Read-Access Geo-Redundant Storage (RA-GRS) (see: [[Azure Storage Redundancy Types#Read-Access Geo-Redundant Storage (RA-GRS)]])
- Geo-Zone-Redundant Storage (GZRS) (see:[[Azure Storage Redundancy Types#Geo-Zone-Redundant Storage (GZRS)]])
- Read-Access Geo-Zone-Redundant Storage (RA-GZRS) (see: [[Azure Storage Redundancy Types#Read-Access Geo-Zone-Redundant Storage (RA-GZRS)]])

### Premium block blobs

Premium storage for [[Block Blobs]] and [[Append Blobs]].

Recommended for scenarios with **high transaction rates** or that use smaller objects or require consistently low storage latency.

It is available only for [[Azure Blob Storage]].

It supports:

- Locally Redundant Storage (LRS) (see :[[Azure Storage Redundancy Types#Locally Redundant Storage (LRS)]])
- Zone-Redundant Storage (ZRS) (see: [[Azure Storage Redundancy Types#Zone-Redundant Storage (ZRS)]])

### Premium file shares

For file shares only.

Recommended for enterprise or high-performance scale applications.

Is available only for [[Azure Files]].

It supports:

- Locally Redundant Storage (LRS) (see :[[Azure Storage Redundancy Types#Locally Redundant Storage (LRS)]])
- Zone-Redundant Storage (ZRS) (see: [[Azure Storage Redundancy Types#Zone-Redundant Storage (ZRS)]])

### Premium page blobs

For [[Page Blobs]] only.

It supports only Locally Redundant Storage (LRS)
