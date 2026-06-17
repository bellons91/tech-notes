---
title: "Actor Model"
tags:
  - architecture
  - software-architecture
  - concurrency
  - distributed-systems
  - fault-tolerance
  - actor-model
aliases:
  - Actor model
  - Actors
---

The **actor model** is a mathematical model of concurrent computation that treats **actors** as the basic unit of work. It targets **high concurrency**, **scalability**, and **fault tolerance**. Languages such as Erlang and Elixir are built around this model; most other ecosystems expose it through frameworks.

## Summary

- Created in **1973** for highly parallel machines: many independent processors with local memory, communicating over a network.
- Like OOP treats everything as objects, the actor model treats everything as **actors** that communicate only by **messages**.
- An actor reacts to a message by updating **state**, choosing the next **behaviour**, and sending more messages.
- Messages are serializable units of communication; they can cross process or machine boundaries.
- Each actor has a **mailbox** (typically FIFO) where incoming messages queue until processed.
- Only the actor itself may change its state; other actors address it through a **PID** or **actor reference** (local or remote).
- **Supervision** coordinates failure handling: failed actors signal a supervisor, which decides how to recover.
- **Virtual actors** (grains) add identity-based activation: the runtime finds or creates the actor for a stable ID - see [[Microsoft Orleans]].
- The model pairs well with [[Event-Driven Architecture]], domain-driven design, [[Event Sourcing]], and CQRS for high-scale systems.
- On .NET, common implementations include [[Microsoft Orleans]], [[Akka.NET]], and [[Proto.Actor]]; Erlang/Elixir run on the BEAM VM without a separate actor framework.

## Core concepts

### Actor

An actor is the basic block of concurrency. When it receives a message, it may:

- Send a **finite** number of messages to other actors
- Create a **finite** number of new actors
- **Designate the behaviour** used for the next message it receives

Processing is message-driven: the actor reacts by changing state, switching behaviour, and emitting further messages.

### Message

A **message** is the unit of communication between actors. Messages should be **serializable** so they can traverse networks.

### Mailbox

The **mailbox** is where an actor receives messages. Actor systems typically dequeue in **FIFO** (first-in, first-out) order. Some implementations allow custom ordering—for example, prioritizing certain message types.

### State

**State** belongs to a single actor. Other actors may read it only indirectly (for example, by sending a message and receiving a reply). **Only the owning actor may modify its state.**

### Behaviours

A **behaviour** defines how an actor handles a given message—effectively its handler or reaction logic for that turn of processing.

### PID / actor reference

A **process ID (PID)** or **actor reference** is the address used to send messages to an actor. The reference may point to a local process or a remote node.

## Supervision

**Supervision** is how actor systems coordinate work and stay resilient when something fails.

When an actor cannot complete an action, it **emits a signal to its supervisor**. The supervisor—not the failed child alone—chooses the recovery policy. Typical options described in classical actor literature include:

- **Stop only the failed actor** (isolate the fault)
- **Stop all supervised actors** (tear down a subtree when the failure is systemic)
- **Escalate** the failure signal to a **parent supervisor**, letting a higher layer decide

In a hierarchy, **all actors are supervisors** of their children: every actor that creates other actors is responsible for handling their failures according to the configured strategy.

Supervision is distinct from ordinary message handling. Creating child actors is a normal capability when processing messages; **failure policy** is what the supervisor applies after a crash or unhandled error.

## Virtual actors (grains)

A **virtual actor** (also called a **grain** in Orleans) is addressed by a **stable unique identifier** rather than by manually creating and tracking a PID. The runtime **locates an existing activation** or **creates one on demand**.

That pattern fits domain-centric designs: the grain ID can align with a domain entity ID, and incoming messages can be persisted (for example, in [[Event Sourcing]]) so state can be rebuilt by replay.

See [[Microsoft Orleans]] for the .NET virtual-actor implementation and terminology (**grain**, **silo**).

## .NET and BEAM implementations

| Implementation | Notes |
| --- | --- |
| [[Microsoft Orleans]] | Virtual actors (grains); minimal setup; does not implement classical supervision as in the original model |
| [[Akka.NET]] | Port of Akka (JVM); broad classical actor features; no built-in virtual actors |
| [[Proto.Actor]] | Classical actor model plus virtual-actor support; usable from .NET and Go |
| Erlang / Elixir (BEAM) | Runtime is actor-based; virtual actors require external libraries |

## Related

- [[Event-Driven Architecture]]
- [[Event Sourcing]]
- [[Dapr]] — exposes an actor API for message-driven, single-threaded units of work
- [[Microsoft Orleans]]
- [[Akka.NET]]
- [[Proto.Actor]]

## Sources

- [Actor Model Overview](https://medium.com/@actor-swe/actor-model-overview-da21779545af) — fundamentals, supervision, virtual actors, and .NET framework comparison (Rafael Andrade, Medium, Feb 2025)
- [Actor model — Wikipedia](https://en.wikipedia.org/wiki/Actor_model)
