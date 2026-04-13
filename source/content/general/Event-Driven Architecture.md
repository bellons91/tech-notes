---
title: "Event-Driven Architecture"
tags:
  - architecture
  - software-architecture
  - event-driven
  - ddd
  - messaging
aliases:
  - EDA
---

Event-driven architecture (EDA) is a paradigm built around the production, detection, and consumption of **events**, enabling scalability, fault tolerance, and loose coupling between producers and consumers.

Events represent significant state changes (for example `OrderPaid`) and propagate through event channels such as message brokers (for example RabbitMQ or Kafka).

Every event can have one or more independent consumers.


## Event types

- **Domain Events**: Business-critical events within a bounded context (e.g., `OrderPaid`).
- **Integration Events**: Cross-context events for propagating changes (e.g., `InventoryUpdated`).

## Topologies

- **Broker Topology**: Simple, decentralized event broadcasting (high performance, no central control).
- **Mediator topology**: Central orchestrator for complex workflows (often stronger error handling, more coordination overhead).