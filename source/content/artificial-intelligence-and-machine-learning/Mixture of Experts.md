---
title: "Mixture of Experts"
tags:
  - ai
  - machine-learning
  - deep-learning
  - transformers
  - sparse-models
  - moe
aliases:
  - MoE
  - Mixture-of-Experts
  - Expert Models
---

Mixture of Experts (MoE) is a sparse neural-network architecture where only a subset of model components is activated for each token or input.  
This note is a quick reference for understanding why MoE is used in large AI models and what trade-offs it introduces.

## Summary

- MoE replaces part of a dense layer (commonly the FFN/MLP block) with multiple expert sub-networks plus a router.
- For each token, the router selects one or a few experts instead of activating every expert.
- This keeps **active parameters per token** low while allowing a high **total parameter count**.
- MoE is widely used in scalable transformer systems to improve quality at a given compute budget.
- Routing quality and load balancing are critical; poor routing can overload a few experts and hurt training stability.
- Capacity constraints and dropped/overflow tokens are practical concerns in training and inference implementations.
- MoE can reduce compute relative to equally large dense models, but it increases system complexity and communication cost.
- Expert parallelism is a common distributed strategy for running MoE models across multiple GPUs.

## Details

## Core idea

An MoE layer typically contains:

1. A **router/gating function** that scores experts for each token.
2. Multiple **experts** (usually dense MLP blocks).
3. A dispatch/combine mechanism that sends token representations to selected experts and merges outputs.

In many transformer implementations, the attention block remains dense while the feed-forward block becomes sparse via experts.

## Why it scales

In dense models, every token uses the same full stack of parameters in each layer.  
In MoE models, each token uses only the routed experts, so the model can increase total capacity without proportional per-token compute.

This is why model cards often report both:

- **Total parameters** (all experts + shared components)
- **Active parameters** per token

## Common trade-offs

| Benefit | Cost / Risk |
| --- | --- |
| Higher capacity at similar compute | More complex routing logic |
| Better scaling for large models | Communication overhead between devices |
| Flexible expert specialization | Expert imbalance and instability if routing is poor |
| Potential quality gains | Additional tuning needed (capacity, routing, auxiliary losses) |

## Where it appears

- Research and production transformer systems (for example, Switch Transformer-style models)
- Distributed training stacks that support expert parallelism and sparse dispatch

## Related

- [[Parameters]]
- [[Model Weights]]
- [[Transformer Architecture]]
- [[Inference Optimization]]
- [[Hyperparameters]]

## Sources

- [Shazeer et al. — Outrageously Large Neural Networks: The Sparsely-Gated Mixture-of-Experts Layer](https://arxiv.org/abs/1701.06538)
- [Fedus et al. — Switch Transformers: Scaling to Trillion Parameter Models with Simple and Efficient Sparsity](https://arxiv.org/abs/2101.03961)
- [DeepSpeed Tutorial — Mixture of Experts (DeepSpeed MoE)](https://www.deepspeed.ai/tutorials/mixture-of-experts/)
- [Hugging Face Transformers Docs — Switch Transformers](https://github.com/huggingface/transformers/blob/main/docs/source/en/model_doc/switch_transformers.md)
