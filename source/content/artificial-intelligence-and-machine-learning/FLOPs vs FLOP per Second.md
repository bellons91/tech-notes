---
title: "FLOPs vs FLOP per Second"
tags:
  - artificial-intelligence
  - machine-learning
  - performance
  - high-performance-computing
  - terminology
aliases:
  - FLOPs vs FLOP/s
  - FLOPs versus FLOP/s
  - FLOPs vs FLOPS
---

This note compares **FLOPs** and **FLOP/s** because the two terms are closely related but describe different things. It is mainly for avoiding terminology mistakes when reading AI papers, profiler output, and hardware marketing material.

## Summary

- [[FLOPs|FLOPs]] are a **count of work**.
- [[FLOP per Second|FLOP/s]] is a **rate of work over time**.
- A workload can have a fixed FLOP count but achieve very different FLOP/s on different hardware or runtimes.
- FLOPs are useful for estimating computational demand; FLOP/s is useful for evaluating performance and utilization.
- Peak FLOP/s is a hardware property under stated assumptions; achieved FLOP/s is workload-dependent.
- Confusing the two makes benchmark claims sound stronger or more precise than they really are.

## Side-by-Side Comparison

| Aspect                                 | FLOPs                                       | FLOP/s                                            |
| -------------------------------------- | ------------------------------------------- | ------------------------------------------------- |
| Core meaning                           | Total floating-point operations             | Floating-point operations executed per second     |
| Answers                                | How much compute is required?               | How fast is the compute executed?                 |
| Depends on time                        | No                                          | Yes                                               |
| Typical use                            | Model cost estimation, algorithm analysis   | Hardware specs, benchmark throughput, utilization |
| Common units                           | raw count, MFLOPs, GFLOPs as a total amount | GFLOPS, TFLOPS, PFLOPS as rates                   |
| Can vary by hardware for same workload | No, if counted the same way                 | Yes                                               |

## Simple Intuition

If a model inference step requires a certain number of [[FLOPs|FLOPs]], that is the size of the arithmetic job. If one accelerator sustains higher [[FLOP per Second|FLOP/s]], it finishes that same arithmetic job faster.

So the relationship is roughly:

- **runtime ≈ FLOPs / achieved FLOP/s**

That simplification is useful, but it still hides memory overhead, communication, compiler effects, and non-floating-point work.

## In AI Practice

You will usually see the distinction in three places:

1. **Papers and architecture discussions** use FLOPs to compare training or inference cost.
2. **Hardware datasheets** use FLOP/s to advertise peak arithmetic throughput.
3. **Profilers and tuning tools** compare expected FLOPs with achieved FLOP/s to reason about utilization and bottlenecks.

## Rule of Thumb

When you read “the model needs X FLOPs,” think **workload size**.

When you read “the device delivers Y TFLOPS,” think **throughput limit under some assumptions**.

## Related

- [[FLOPs]]
- [[FLOP per Second]]
- [[Inference Optimization]]
- [[TPU]]

## Sources

- [PyTorch `torch/utils/_runtime_estimation.py` — example of using a FLOPs count separately from peak GPU FLOPS](https://github.com/pytorch/pytorch/blob/main/torch/utils/_runtime_estimation.py)
- [TensorFlow `stream_executor.h` — device-side average floating point operations per second terminology](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/c/experimental/stream_executor/stream_executor.h)
- [LLVM MLIR tutorial — contrasts total floating-point operations with achieved GFlops and theoretical peak](https://github.com/llvm/llvm-project/blob/main/mlir/docs/Tutorials/transform/ChH.md)
- [ROCm HIP glossary — defines arithmetic intensity in FLOPs/byte and arithmetic bandwidth in FLOPS](https://github.com/ROCm/hip/blob/develop/docs/understand/glossary.md)
