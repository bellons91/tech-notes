---
title: "Source Generators"
tags:
  - dotnet
  - csharp
  - roslyn
  - code-generation
---

A **source generator** in .NET is a feature introduced with **C# 9** and **.NET 5** that lets you emit additional C# source files **at compile time**.

Generators run inside the **Roslyn** compilation pipeline. They can inspect syntax, semantics, and additional files, then contribute generated code into the same compilation. Typical uses include reducing boilerplate, generating DTOs or serializers, and wiring **dependency injection** registrations.

### How Source Generators Work

- They are implemented as **Roslyn analyzers** and plugged into the build process.
- They do **not** modify your existing source code, but add new files **to the compilation**.
- You can use them for tasks like auto-generating DTOs, mapping code, or any repetitive code that follows a pattern.

## Incremental vs. Full Source Generators

### Full Source Generators

- **Full generators** (or "classic" generators) are the original model.
- They execute on **every build**, regardless of what changed.
- Every time anything in the project changes, the generator runs from scratch and produces all its output again.
- This can lead to **performance issues** in large projects, as the generator is not aware of what has changed and always reprocesses everything.

### Incremental Source Generators

- **Incremental generators** are a newer, more efficient model introduced in **.NET 6**.
- They use the **Incremental Generator API**.
- They track which inputs (syntax trees, files, metadata, etc.) have changed and **only re-execute the parts of the generator affected by those changes**.
- This approach **improves performance** during builds, especially in large codebases, because it avoids unnecessary work.
- Incremental generators are preferred for most new projects due to their efficiency and scalability.
