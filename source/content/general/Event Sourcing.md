---
title: "Event Sourcing"
tags:
  - storage
  - software-architecture
  - data
  - database
  - event-sourcing
---

Event Sourcing persists application state by storing every change as an **immutable** event. Unlike [[Event-Driven Architecture]], which often spans services and integration boundaries, event sourcing is primarily an **application-level** state model.

## Core ideas

- **Immutable event log**: Every state change is captured as a sequence of events (for example `ItemAddedToCart`, `PaymentProcessed`).
- **Replayable history**: Applications can reconstruct state by replaying events, enabling:
  - **Temporal queries**: Audit past states (for example “What was the order status on 2023-01-01?”).
  - **Retroactive adjustments**: Correct errors by appending compensating events and replaying with updated logic where appropriate.