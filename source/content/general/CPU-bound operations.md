---
title: "CPU-Bound Operations"
tags:
  - csharp
  - async
  - cpu
  - performance
  - dotnet
---

**CPU-bound** work keeps a core busy with computation—for example heavy math, compression, or large in-memory transformations.

For CPU-bound code, you await an operation that is started on a background thread with the `Task.Run` method.

For example, you can use

```cs
var damageResult = await Task.Run(() => CalculateDamageDone());
```

If the work you have is CPU-bound and you care about responsiveness, use async and await, but spawn off the work on another thread with Task.Run.

If the work is appropriate for concurrency and parallelism, also consider using the Task Parallel Library.
