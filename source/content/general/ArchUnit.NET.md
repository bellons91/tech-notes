---
title: "ArchUnit.NET"
tags:
  - dotnet
  - csharp
  - software-architecture
  - testing
  - archunitnet
aliases:
  - ArchUnitNET
  - ArchUnit NET
---

**ArchUnit.NET** is a .NET port of the Java [ArchUnit](https://github.com/TNG/ArchUnit) library. You describe architectural rules with a **fluent API** and evaluate them against a loaded **architecture** (your assemblies). Rules run inside your usual test runner (for example **xUnit**), like any other test.

## Example: services must not depend on controllers

The following pattern matches the example in [Architectural Tests in .NET](https://mareks-082.medium.com/architectural-tests-in-net-1bd5d19b0ba8): pick types in two namespaces, state a dependency rule, evaluate it, and assert there are no violations.

```csharp
[Fact]
public void ServicesShouldNotDependOnControllers()
{
    var services = Types()
        .That()
        .ResideInNamespace("SampleApp.Services");

    var controllers = Types()
        .That()
        .ResideInNamespace("SampleApp.Controllers");

    var rule = services
        .Should()
        .NotDependOnAny(controllers);

    var failures = rule.Evaluate(Architecture)
        .Where(result => !result.Passed)
        .Select(result => result.Description)
        .Where(description => !string.IsNullOrWhiteSpace(description))
        .ToArray();

    Assert.True(
        failures.Length == 0,
        "These types violate the rule: " +
        string.Join(Environment.NewLine, failures));
}
```

In a real project you build `Architecture` with ArchUnit.NET’s loader (for example `ArchLoader` over your assemblies); `Types()` is part of the fluent entry API used together with that architecture instance—see the official docs for the exact setup for your solution layout.

## What you can express

The same article highlights that ArchUnit.NET can help you check **dependencies between layers, namespaces, and classes**, enforce **naming and structural conventions**, validate **attributes**, and similar rules—all as ordinary test code rather than a separate proprietary DSL.

## Limitations

Because of how .NET compilation and metadata work, ArchUnit.NET has documented **edge cases** (for example around constant fields). Review the upstream limitations page before relying on subtle rules.

## Related

- [[Architectural Tests]]
- [[Source Generator]] (Roslyn pipeline; complementary to assembly-based rules)

## Sources

- [Architectural Tests in .NET](https://mareks-082.medium.com/architectural-tests-in-net-1bd5d19b0ba8) (Marek Sirkovský, Medium, 2026) — examples and ecosystem context.
- [ArchUnitNET on GitHub](https://github.com/TNG/ArchUnitNET) — source and issue tracker.
- [ArchUnit.NET limitations](https://archunitnet.readthedocs.io/en/stable/limitations/constant_fields/) — official documentation on known constraints.
