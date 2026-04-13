---
title: "Cloud Models"
tags:
  - azure
  - cloud
  - az-900
  - architecture
  - hybrid-cloud
---

Cloud **deployment** models describe where infrastructure runs and how it is isolated or shared. They sit alongside **service** models ([[Infrastructure-as-a-Service]], [[Platform-as-a-Service]], [[Software-as-a-Service]]), which describe what the provider manages for you. Responsibility and control trade-offs are summarized in the [[Shared Responsibility Model]].

## Private cloud

A cloud used by a single organization.

The IT team has almost full control; capacity is not shared with other customers. Total cost of ownership is often higher than in public cloud because you fund hardware, facilities, and operations.

It can run in an on-site datacenter or be operated for you by a third party (dedicated hosted environment).

- Complete control over resources and security posture
- Data and workloads are not mixed with other tenants
- Up-front hardware purchase and ongoing maintenance are your responsibility
- You own patching, capacity planning, and lifecycle of the physical layer

## Public cloud

Built, operated, and maintained by a third-party provider.

Any customer can buy services; the provider’s datacenter and underlying hardware are shared across tenants (logically isolated per service design).

- No large capital outlay to scale capacity up or down
- Resources can be provisioned and released quickly
- Pay-as-you-go consumption pricing
- Less direct control over the physical stack and some security boundaries (shared responsibility with the provider)

## Hybrid cloud

Combines private cloud (or on-premises) with public cloud services—for example, burst capacity or specific workloads in the public tier while sensitive data stays private.

You decide which workloads stay private and which use public services.

- High flexibility to match cost, latency, and compliance needs per workload
- You choose where each application runs
- Lets you satisfy strict security, compliance, or legal requirements while still using public-cloud scale where appropriate

## Multi-cloud

Uses services from **more than one** cloud vendor (or more than one public cloud), mixing providers by workload, region, or capability.

- Reduces dependence on a single vendor’s roadmap and outages
- Lets teams pick best-of-breed services per use case
- Adds integration, governance, and operational complexity across providers
