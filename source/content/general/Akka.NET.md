---
title: "Akka.NET"
tags:
  - dotnet
  - csharp
  - distributed-systems
  - concurrency
  - actor-model
  - akka
aliases:
  - Akka NET
  - Akka.net
---

**Akka.NET** is a .NET port of the JVM [[Akka]] framework. It implements most classical [[Actor Model]] concepts—actors, mailboxes, messaging, and **supervision**—with flexible configuration.

## Summary

- Ported from the Java Akka ecosystem; familiar to teams moving actor patterns to .NET.
- Implements **supervision hierarchies** and other textbook actor features more completely than [[Microsoft Orleans]].
- **Does not** provide built-in **virtual actors** (grains). Mimicking Orleans-style identity-based activation on top of Akka.NET is possible but requires extra design.
- Often described as **flexible** and relatively **easy to use** for classical actor programming.
- For DDD-style entity-per-ID activation without custom plumbing, [[Microsoft Orleans]] or [[Proto.Actor]] may be a better fit.

## Related

- [[Actor Model]]
- [[Akka]] — JVM reference implementation this port follows
- [[Microsoft Orleans]]
- [[Proto.Actor]]

## Sources

- [How the Actor Model Meets the Needs of Modern, Distributed Systems](https://doc.akka.io/libraries/akka-core/current/typed/guide/actors-intro.html) — shared actor-model and supervision concepts from Akka core docs
- [Actor Model Overview](https://medium.com/@actor-swe/actor-model-overview-da21779545af) — Akka.NET positioning versus Orleans and Proto.Actor (Rafael Andrade, Medium, Feb 2025)
- [Akka Documentation](https://doc.akka.io/)
