---
title: "Chinchilla Scaling Law"
tags:
  - artificial-intelligence
  - machine-learning
  - llm
  - scaling-laws
  - model-training
  - transformers
aliases:
  - Chinchilla Law
  - Chinchilla Scaling Laws
  - Compute-Optimal Scaling
---

The **Chinchilla scaling law** is the compute-optimal training result popularized by DeepMind's *Training Compute-Optimal Large Language Models* paper. It is a useful mental model for understanding how to balance model size and training data when the training compute budget is fixed.

## Summary

- Chinchilla argues that many large language models of its era were **too large for the amount of data they were trained on**.
- For a fixed training compute budget, better results can come from **smaller models trained on more tokens** rather than from making the model as large as possible.
- The paper's headline example is **Chinchilla**, a 70B-parameter model trained on **1.4T tokens**.
- The result is often summarized as a rough rule of thumb near **20 training tokens per parameter** in the original regime studied.
- Chinchilla revised the earlier intuition from Kaplan-style scaling that favored relatively larger models trained on fewer tokens.
- The law is about **training-loss efficiency under a compute budget**, not a universal rule for every downstream objective.
- In practice, later model families adapted or relaxed the heuristic depending on data quality, repeated tokens, inference cost, and product constraints.

## Core Idea

Chinchilla focuses on **compute-optimal allocation**:

- one part of the budget goes into model size
- another part goes into the number of training tokens
- the best loss for a fixed compute budget comes from balancing those choices more evenly than many earlier models did

This matters because a larger model is more expensive per training step, while a larger dataset requires more steps or more tokens processed. The paper argues that the best trade-off is not “largest possible model,” but a model-data balance that uses the available compute more efficiently.

## Why It Changed the Discussion

Earlier scaling conversations often emphasized growing parameter count aggressively. Chinchilla shifted the center of gravity toward **data-token scaling** and undertraining risk.

A simplified comparison:

| View | Main emphasis |
| --- | --- |
| Pre-Chinchilla reading of scaling | Grow model size strongly under a fixed compute budget |
| Chinchilla | Use smaller models than that earlier practice and train them on much more data |

That shift influenced later open and closed model programs, including smaller-but-better-trained model families.

## Scope and Limits

Chinchilla is important, but it is not a law of nature:

- it was derived from a specific training setup and loss objective
- it does not directly optimize **inference cost**, latency, or memory footprint
- it assumes access to enough useful training data
- later work explored repeated-data regimes, data-constrained settings, and cases where the original token-to-parameter ratio is not ideal

For operational decisions, it is better treated as a strong baseline heuristic than as an invariant.

## Relationship to Other Notes

- It relates to [[Parameters]] because parameter count is one side of the scaling trade-off.
- It relates to [[Transformer Architecture]] because the original result is framed around transformer language models.
- It relates to [[Inference Optimization]] because a compute-optimal training choice is not automatically an inference-optimal deployment choice.

## Related

- [[Parameters]]
- [[Hyperparameters]]
- [[Transformer Architecture]]
- [[Inference Optimization]]

## Sources

- [Hoffmann et al. — Training Compute-Optimal Large Language Models](https://arxiv.org/abs/2203.15556)
- [Kaplan et al. — Scaling Laws for Neural Language Models](https://arxiv.org/abs/2001.08361)
- [Hugging Face blog — 2023, year of open LLMs](https://github.com/huggingface/blog/blob/main/2023-in-llms.md)
- [theLMbook scaling notes — points to Chinchilla as a core neural scaling-law reference](https://github.com/aburkov/theLMbook/blob/main/wiki/scaling.md)
