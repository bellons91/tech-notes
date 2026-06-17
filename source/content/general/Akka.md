---
title: "Akka"
tags:
  - akka
  - jvm
  - scala
  - java
  - distributed-systems
  - concurrency
  - actor-model
  - fault-tolerance
aliases:
  - Akka JVM
  - Akka core
---

**Akka** is a JVM toolkit for building concurrent and distributed applications with the [[Actor Model]]. It is the reference implementation behind [[Akka.NET]] on .NET. Documentation and APIs target **Scala** and **Java** (typed and classic actor APIs, plus modules for cluster, persistence, streams, and HTTP).

## Summary

- Actors send **messages** instead of sharing mutable state; senders do not block waiting for the receiver’s thread.
- Each actor has a **mailbox**, **behaviour**, and **address**; an **execution environment** schedules actors onto a shared thread pool.
- **Encapsulation** is preserved because only the actor processes its mailbox **sequentially**—no locks required to protect invariants.
- **Supervision** is central: actors form a **tree** (creator = parent). Parents define a **supervisor strategy** when spawning children—restart on some failures, stop on others.
- **Domain errors** are normal reply messages; **internal faults** trigger supervisory action. Restarts can be **transparent** to actors still messaging the same target.
- Stopping a parent **recursively stops** all descendants, similar to process trees in operating systems.
- The same local-message mental model extends to **remote** actors: state stays on a node; data moves as serialized packets.

## Supervision in Akka

When a child actor fails with an unhandled error, the **parent**—not the sender of the failing message—decides recovery:

- **Restart** the child (fresh behaviour/state according to strategy)
- **Stop** the child (interested parties can be notified)
- **Escalate** to the parent’s supervisor

Supervisor policies are typically declared at **child creation** time. Collaborators can keep sending messages while a supervised actor restarts; external observers should not need to track restart events for basic messaging.

Children should not disappear without supervisory action (aside from edge cases such as an infinite loop). There is always a **responsible parent** in the hierarchy.

## Ecosystem

Akka ships as a family of libraries (core actors, cluster, event sourcing persistence, streams, gRPC integrations, and more). New projects may also evaluate the **Akka SDK** as a higher-level entry point—see current [Akka documentation](https://doc.akka.io/) for supported paths.

## Related

- [[Actor Model]] — concepts: message passing, mailboxes, domain errors versus faults
- [[Akka.NET]] — .NET port of Akka
- [[Proto.Actor]] — classical actors on .NET/Go with optional virtual actors
- [[Microsoft Orleans]] — virtual-actor alternative on .NET without classical supervision trees

## Sources

- [How the Actor Model Meets the Needs of Modern, Distributed Systems](https://doc.akka.io/libraries/akka-core/current/typed/guide/actors-intro.html) — Akka’s actor-model motivation, message lifecycle, and supervision (Akka core documentation)
