---
title: "Sidecar Pattern"
tags:
  - architecture
  - microservices
  - kubernetes
  - sidecar
---

The **sidecar** pattern pairs a main application with a **collocated helper process** (often in the same pod on Kubernetes) that handles cross-cutting concerns such as proxies, telemetry, secrets, or sync, so the primary service stays focused on business logic.

Examples of sidecar containers include:

- An agent that reads logs from the primary app container on a shared volume and forwards them to a logging service.
- A background process that refreshes a cache used by the primary app container in a shared volume.
