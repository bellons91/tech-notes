---
title: "Proto.Actor"
tags:
  - dotnet
  - golang
  - distributed-systems
  - concurrency
  - actor-model
  - proto-actor
aliases:
  - Proto Actor
  - Proto.Actor Go
---

**Proto.Actor** is an actor framework usable from **.NET** and **Go**. Among the options discussed for C#, it is positioned as combining **classical actor-model semantics** with **virtual-actor** support.

## Summary

- Implements the [[Actor Model]] **by the book** (similar breadth to [[Akka.NET]] for classical concepts).
- Also supports the **virtual actor** pattern (like [[Microsoft Orleans]] grains).
- Useful when you want both supervision-style classical actors and identity-based virtual activations in one stack.
- The author of the source article recommends evaluating Proto.Actor when choosing a .NET actor library.

## Related

- [[Actor Model]]
- [[Microsoft Orleans]]
- [[Akka.NET]]

## Sources

- [Actor Model Overview](https://medium.com/@actor-swe/actor-model-overview-da21779545af) — Proto.Actor as full model plus virtual actors (Rafael Andrade, Medium, Feb 2025)
- [Proto.Actor](https://proto.actor/)
