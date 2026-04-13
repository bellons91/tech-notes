---
title: "Shared Responsibility Model"
tags:
  - azure
  - cloud
  - az-900
  - security
aliases:
  - SRM
---

When you run workloads **on your own hardware**, you own the full stack—from physical facilities to applications—for example:

- Physical space (buildings, power, hardware)
- Maintenance and component replacement
- Physical security and network connectivity

The **shared responsibility model** describes how those duties are divided between **you** and the **cloud provider** after you adopt cloud services.

Cloud providers are responsible for the infrastructure of the datacenter: physical security, cooling, building access, and maintenance.

Clients are responsible for the data (both the security and the correctness).

Depending on the **cloud service model**, responsibilities are shared in a different way between cloud vendor and client:

![Shared Responsibility](shared-responsibility-model.svg)

- [[Infrastructure-as-a-Service]] places most of the responsibility on the consumer; the cloud vendor is only responsible for physical security and connectivity;
- [[Software-as-a-Service]] places most of the responsibilities on the cloud vendor;
- [[Platform-as-a-Service]] sits in the middle.
