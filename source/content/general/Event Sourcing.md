---
tags:
  - storage
  - software-architecture
  - data
  - database
---
Event Sourcing focuses on persisting application state by storing every change as an **immutable** event. 

Unlike [[Event-Driven Architecture]], it operates at the application level, not between services.


- **Immutable Event Log** : Every state change is captured as a sequence of events (e.g., `ItemAddedToCart`, `PaymentProcessed`).
- **Replayable History**: Applications can reconstruct state by replaying events, enabling:
	- Temporal Queries: Audit past states (e.g., “What was the order status on 2023–01–01?”).
	- Retroactive Adjustments: Fix errors by reversing incorrect events and replaying corrected ones.