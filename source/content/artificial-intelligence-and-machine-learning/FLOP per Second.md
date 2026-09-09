---
title: "FLOP per Second"
tags:
  - artificial-intelligence
  - machine-learning
  - high-performance-computing
  - performance
  - hardware-accelerators
aliases:
  - FLOP/s
  - FLOPS
  - Floating-Point Operations per Second
  - Floating Point Operations per Second
---

**FLOP/s** is a throughput metric that describes how many floating-point operations a system can execute in one second. This note focuses on the performance meaning of the term, which is often written as **FLOPS** in hardware and benchmarking material.

## Summary

- **FLOP/s** measures arithmetic **rate**, not workload size.
- It is commonly written as **FLOPS** in benchmarks, device specifications, and profiler output.
- Units such as **GFLOPS**, **TFLOPS**, and **PFLOPS** scale the same idea by powers of ten.
- FLOP/s depends on hardware, precision, kernel quality, runtime overhead, and data movement.
- Published peak FLOP/s numbers are usually **theoretical maxima**, not guaranteed application performance.
- Achieved FLOP/s is useful for understanding utilization, especially for compute-bound workloads.
- FLOP/s should be read together with memory bandwidth, latency, and workload shape.

## What FLOP/s Measures

FLOP/s answers the question: **how quickly can the system perform floating-point arithmetic?**

Examples:

- a GPU datasheet listing theoretical TFLOPS
- a benchmark reporting achieved GFLOPS for matrix multiplication
- a profiler estimating whether a kernel is close to peak arithmetic throughput

This makes FLOP/s a **performance rate**, similar in spirit to requests per second or tokens per second, but scoped specifically to floating-point arithmetic.

## Theoretical vs Achieved FLOP/s

| Type | Meaning |
| --- | --- |
| **Theoretical peak** | Maximum arithmetic throughput implied by the hardware design and precision mode. |
| **Achieved FLOP/s** | Throughput actually observed for a specific workload, kernel, and runtime setup. |

Real workloads usually achieve less than peak because of:

- memory stalls
- instruction mix differences
- synchronization or communication overhead
- small batch sizes or poor occupancy
- framework/runtime inefficiencies

## Why FLOP/s Matters in AI Systems

FLOP/s is useful when comparing accelerators such as GPUs and [[TPU|TPUs]], or when checking whether a workload is compute-bound.

In roofline-style performance analysis, arithmetic throughput is read together with arithmetic intensity and memory bandwidth. A workload may have a large [[FLOPs|FLOP count]] but still deliver poor achieved FLOP/s if data movement is the real bottleneck.

## Naming Ambiguity

A common source of confusion is that many people say “FLOPs” when they actually mean **FLOP/s**. In strict usage:

- [[FLOPs|FLOPs]] = amount of floating-point work
- **FLOP/s** or **FLOPS** = rate of floating-point work per second

## Related

- [[FLOPs]]
- [[FLOPs vs FLOP per Second]]
- [[Inference Optimization]]
- [[TPU]]

## Sources

- [TensorFlow `stream_executor.h` — device API comment for average floating point operations per second (`get_gflops`)](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/c/experimental/stream_executor/stream_executor.h)
- [ROCm HIP glossary — defines arithmetic bandwidth as FLOPS, or floating-point operations per second](https://github.com/ROCm/hip/blob/develop/docs/understand/glossary.md)
- [BLIS performance docs — GFLOPS reported as billions of floating-point operations per second](https://github.com/flame/blis/blob/master/docs/Performance.md)
