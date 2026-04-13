---
title: "I/O-Bound Operations"
tags:
  - csharp
  - async
  - performance
  - io
  - dotnet
---

**I/O-bound** work spends most of its time waiting on external systems: the network, a database, or the file system. In .NET you typically express that with **`async`/`await`** on APIs that return `Task` / `Task<T>`.

For I/O-bound code, you await an operation that returns a `Task` or `Task<T>` inside of an async method.

If the work you have is I/O-bound, use `async` and `await` without `Task.Run`. 

You should **not** use the Task Parallel Library.
