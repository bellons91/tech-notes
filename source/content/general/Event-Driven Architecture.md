---
tags:
  - architecture
  - software-architecture
  - event-driven
  - ddd
aliases:
  - EDA
---
EDA is a software architecture paradigm concerning the production and detection of events, enabling #scalability, #fault-tolerance, and #loose-coupling. 

Events represent significant state changes (e.g., `OrderPaid`) and propagate through event channels (message brokers like #RabbitMQ or #Kafka).

Every event can have one or more independent consumers.


## Event types

- **Domain Events**: Business-critical events within a bounded context (e.g., `OrderPaid`).
- **Integration Events**: Cross-context events for propagating changes (e.g., `InventoryUpdated`).

## Topologies

- **Broker Topology**: Simple, decentralized event broadcasting (high performance, no central control).
- **Mediator Topology** : Central #orchestrator for complex workflows (better error handling, lower scalability).