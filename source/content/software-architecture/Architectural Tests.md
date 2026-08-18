---
title: "Architectural Tests"
tags:
  - software-architecture
  - testing
  - quality
  - maintainability
aliases:
  - architecture tests
  - structural tests
---

**Architectural tests** are automated checks that assert the **intended shape** of a codebase: allowed or forbidden dependencies between layers or namespaces, placement of types, naming or attribute conventions, and similar **structural** rules. They are not primarily about proving that a unit of behavior returns the correct output for a given input.

## How they differ from other tests

| Kind | Main question |
| --- | --- |
| **Unit tests** | Does this component behave correctly in isolation? |
| **Integration tests** | Do these parts work together at runtime (I/O, APIs, DB)? |
| **Architectural tests** | Does the code still respect the boundaries and conventions we agreed on? |

Diagrams and architecture documents describe intent, but they **do not enforce** it when deadlines pressure teams to take shortcuts. Executable rules turn those decisions into failures in CI or the IDE, so drift is visible early.

## Why teams use them

- **Preserve layering** (for example, domain must not depend on UI).
- **Block dependency mistakes** (for example, services must not reference MVC controllers).
- **Encode conventions** (naming, attributes, where certain patterns must appear).
- **Complement people practices** (mentorship, ADRs): tests automate what conversation alone cannot guarantee at scale.

Statically typed stacks such as **.NET** (C#, F#) offer rich metadata and reflection, which makes many architectural rules straightforward to express as ordinary test code or analyzers; see [[ArchUnit.NET]] for one common library in that ecosystem.

## Related

- [[Software Architecture vs Software Design]]
- [[Architectural Risk]]
- [[ArchUnit.NET]]

## Sources

- [Architectural Tests in .NET](https://mareks-082.medium.com/architectural-tests-in-net-1bd5d19b0ba8) (Marek Sirkovský, Medium, 2026) — motivation and comparison to other test types.
