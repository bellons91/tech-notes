---
title: "Microsoft Orleans"
tags:
  - dotnet
  - csharp
  - distributed-systems
  - concurrency
  - actor-model
  - orleans
aliases:
  - Orleans
---

**Microsoft Orleans** is a .NET framework for building distributed applications using the **virtual actor** model. It does **not** implement the full classical [[Actor Model]] from the literature—it focuses on **grains** (virtual actors) rather than general-purpose actor hierarchies with book-style supervision.

## Summary

- Orleans implements **virtual actors**: you address a **grain** by a stable ID; the runtime activates, locates, or creates the instance.
- Microsoft terminology maps **grain** → virtual actor and **silo** → node (cluster member).
- Strengths: **low ceremony**, **minimal setup**, approachable for .NET teams.
- Trade-off: **supervision** as described in classical actor texts is **not** implemented, so failure-handling flexibility is more limited than in [[Akka.NET]] or [[Proto.Actor]].
- Virtual grains align well with **domain IDs**, [[Event Sourcing]], and CQRS: messages tied to an entity ID can be stored and replayed to reconstruct state (or snapshots can be saved alongside the event log).

## When to consider Orleans

Choose Orleans when you want identity-based, location-transparent actors with simple cluster hosting and can accept Orleans’s opinionated subset of actor concepts. Prefer [[Akka.NET]] or [[Proto.Actor]] when you need full classical supervision trees or a closer match to textbook actor semantics.

## Related

- [[Actor Model]]
- [[Event Sourcing]]
- [[Akka.NET]]
- [[Proto.Actor]]

## Sources

- [Actor Model Overview](https://medium.com/@actor-swe/actor-model-overview-da21779545af) — Orleans as a C# virtual-actor framework; grains, silos, and supervision limitations (Rafael Andrade, Medium, Feb 2025)
