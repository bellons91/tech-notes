---
title: "Tensor Processing Unit"
tags:
  - ai
  - machine-learning
  - hardware-accelerators
  - tpu
  - model-training
  - inference
aliases:
  - TPU
  - Google TPU
  - Cloud TPU
---

A **TPU (Tensor Processing Unit)** is a custom accelerator designed for tensor-heavy machine-learning workloads, especially deep learning training and inference at scale.  
This note is a quick reference for what TPUs are, where they fit, and how they differ from GPUs and CPUs.

## Summary

- TPUs are specialized AI accelerators optimized for large matrix/tensor operations used in modern ML models.
- They are commonly used through Google Cloud TPU environments and support frameworks such as TensorFlow, JAX, and PyTorch/XLA.
- TPUs are designed for high-throughput training and inference rather than broad general-purpose computing.
- Compared with CPUs, TPUs usually offer much higher parallel compute for large ML batches.
- Compared with GPUs, TPUs can provide strong performance/cost for specific large-scale ML pipelines, but ecosystem and workflow choices matter.
- Hardware choice should be made by measuring model quality, throughput, latency, memory limits, and total operating cost.
- In practice, teams often use a mix: CPU for orchestration/data prep, GPU or TPU for model training/inference.

## TPU vs GPU vs CPU

| Dimension | CPU | GPU | TPU |
| --- | --- | --- | --- |
| Primary design goal | General-purpose compute | Highly parallel numeric compute | ML tensor compute specialization |
| Typical strengths | Control flow, preprocessing, orchestration, broad compatibility | Flexible acceleration across many AI/HPC workloads | Large-scale training/inference for supported ML stacks |
| Parallelism profile | Lower data parallelism per chip | Massive SIMD/SIMT parallelism | Massive tensor-oriented parallelism |
| Ecosystem | Universal | Very broad ML tooling and runtimes | Strongest in Google Cloud + TPU-enabled frameworks |
| Best fit examples | Data pipelines, feature engineering, service logic | Research/prototyping and production ML across vendors | Large production training jobs and high-throughput inference on TPU stacks |

## Where TPUs usually fit

- **Training:** large transformer or multimodal workloads where accelerator utilization and scaling are key.
- **Inference:** high-throughput serving when the deployment stack is TPU-compatible.
- **Distributed jobs:** multi-accelerator training with framework support (for example, PyTorch/XLA or JAX on TPU backends).

## Practical notes

- “Best hardware” is workload-dependent; benchmark the same model and batch strategy across devices when possible.
- Device choice interacts with software stack, compiler/runtime maturity, and team expertise.
- Some workloads are bottlenecked by input pipelines or memory bandwidth, not only raw compute.
- For production decisions, compare **end-to-end** metrics (time-to-train, cost/run, latency SLOs, and reliability).

## Related

- [[Inference Optimization]]
- [[Transformer Architecture]]
- [[Parameters]]
- [[Model Weights]]

## Sources

- [PyTorch/XLA Docs — Learn about TPUs](https://github.com/pytorch/xla/blob/master/docs/source/accelerators/tpu.md)
- [Google Cloud TPU Docs — Introduction to Cloud TPUs](https://cloud.google.com/tpu/docs/intro-to-tpu)
- [Google Cloud TPU Docs — TPU VM system architecture](https://cloud.google.com/tpu/docs/system-architecture-tpu-vm)
- [JAX README — XLA compilation and TPU/GPU accelerator support](https://github.com/jax-ml/jax/blob/main/README.md)
- [TensorFlow source (`tensorflow/python/tpu/__init__.py`) — TPU module context](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/python/tpu/__init__.py)
