---
title: "FLOPs"
tags:
  - artificial-intelligence
  - machine-learning
  - high-performance-computing
  - performance
  - floating-point
aliases:
  - FLOP
  - Floating-Point Operations
  - Floating Point Operations
---

**FLOPs** in the strict sense are a **count of floating-point operations** such as adds, multiplies, and fused multiply-add work used to describe how much numeric computation a workload performs. This note is a quick reference for reading FLOPs as a workload-size metric instead of a hardware speed metric.

## Summary

- A **FLOP** is one floating-point operation; **FLOPs** is the plural form or a total count.
- FLOPs describe **how much arithmetic work** a model, layer, kernel, or benchmark performs.
- FLOPs are separate from elapsed time; the same FLOP count can run faster or slower on different hardware or runtimes.
- In ML tooling, FLOPs are often estimated from operator shapes rather than measured directly in hardware.
- A fused multiply-add is commonly counted as **two** floating-point operations in performance analysis.
- FLOP counts help compare algorithms, layers, and model variants, but they do not capture memory traffic, synchronization, or control-flow overhead.
- People often use “FLOPs” loosely when they really mean [[FLOP per Second|FLOP/s]], which causes confusion.

## What FLOPs Measure

FLOPs answer the question: **how many floating-point arithmetic operations does this computation require?**

Typical examples:

- matrix multiplication workload size
- forward-pass or training-step compute for a neural network
- kernel-level arithmetic count in a profiler or compiler

In practice, ML tools may derive this number from tensor shapes and known formulas. For example, PyTorch includes utilities that treat FLOPs as a **count** and convert that count into an estimated execution time only after combining it with hardware throughput assumptions.

## FLOPs Are Not Runtime

A FLOP count by itself does **not** tell you how fast something runs.

Two workloads with similar FLOP counts can have very different wall-clock time because of:

- memory bandwidth limits
- cache behavior
- kernel launch overhead
- communication across devices
- poor hardware utilization
- different precision modes

That is why performance discussions often pair FLOPs with [[FLOP per Second|FLOP/s]] or with roofline-style analysis.

## Why FLOPs Matter in AI

For AI and ML notes, FLOPs are useful because they provide a rough hardware-independent way to talk about compute demand:

- larger models often require more FLOPs per token or per batch
- training cost grows with model size, sequence length, and token count
- architecture choices can trade [[Parameters|parameters]], memory use, and FLOPs differently
- optimization work often tries to reduce effective FLOPs or make the same FLOPs execute more efficiently

## Common Caveats

| Caveat | Why it matters |
| --- | --- |
| FLOPs are often estimated | Different tools may count the same operation slightly differently. |
| FLOPs ignore non-arithmetic costs | Memory movement and orchestration can dominate runtime. |
| Precision changes the story | FP32, BF16, FP16, and tensor-core paths can have different effective throughput. |
| Sparse execution complicates comparisons | Total model size and active compute per token are not always the same. |

## Related

- [[FLOP per Second]]
- [[FLOPs vs FLOP per Second]]
- [[Inference Optimization]]
- [[TPU]]
- [[Parameters]]

## Sources

- [PyTorch `torch/utils/_runtime_estimation.py` — treats FLOPs as a count before converting to estimated time](https://github.com/pytorch/pytorch/blob/main/torch/utils/_runtime_estimation.py)
- [LLVM MLIR tutorial — example that counts floating-point operations separately from achieved GFlops](https://github.com/llvm/llvm-project/blob/main/mlir/docs/Tutorials/transform/ChH.md)
- [corsix/amx `fma.md` — notes that one fused multiply-add is counted as two floating-point operations](https://github.com/corsix/amx/blob/main/fma.md)
