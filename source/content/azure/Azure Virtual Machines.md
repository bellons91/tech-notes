---
title: "Azure Virtual Machines"
tags:
  - azure
  - cloud
  - az-900
  - virtual-machines
  - iaas
  - virtualization
aliases:
  - Azure VM
---

# Azure Virtual Machines

Azure Virtual Machines deliver [[Infrastructure-as-a-Service]] as a **virtualized server**. You do not manage physical hardware, but you still configure, patch, and maintain the software on the VM.

## Creating and sizing VMs

You create and provision a VM from a preconfigured **VM image**—a template that may already include an OS and other software (for example development tools or a web stack).

Choose a [[Virtual Machines size]] that matches expected workload, then tune cost and performance using [[Optimize Azure Virtual Machines]].

## When VMs are a good fit

VMs suit scenarios where you need:

1. Full control over the operating system.
2. Custom or specialized software that is not offered as a managed service.
3. Hosting patterns that require a specific machine configuration.

Typical uses:

- Small workloads that map cleanly to a single VM.
- Test and development **environments**.
- **High availability**, **scalability**, and **redundancy** (for example with scale sets).
- Running applications on Azure in an IaaS style.
- Cost control by stopping or deallocating VMs when they are idle.
- **Extending an on-premises network** with cloud-hosted VMs.
- **Lift-and-shift** migration of existing servers.

## Virtual Machines Scale Sets

Virtual machine scale sets let you create and manage a **group of identical, load-balanced VMs**. You can **ensure identical configuration** and **consistent networking rules** across the set.

Scale sets support **monitoring** so you can grow or shrink the number of VMs based on workload or a **schedule**.

## Virtual Machines Availability Sets

Availability sets spread VMs across **update domains** and **fault domains** so maintenance or hardware issues do not take down every instance at once. For example, if every VM received updates in the same window, you could lose availability across the whole tier. Availability sets have **no separate charge**; you pay for the VM instances.

Two dimensions:

- **Update domains**: subsets of VMs that can be rebooted together during platform maintenance. Azure waits about **30 minutes** before moving to VMs in the next update domain.
- **Fault domains**: VMs that share underlying power or network paths. By default, an availability set spreads VMs across up to **three fault domains**.

## Additional resources

Operate on VMs with the Azure CLI: [[Operations on VM with Cloud CLI]]
