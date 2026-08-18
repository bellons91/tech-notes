---
title: "Masked vs Autoregressive Language Models"
tags:
  - artificial-intelligence
  - language-models
  - natural-language-processing
  - transformers
  - machine-learning
  - ai
aliases:
  - MLM vs ALM
  - Masked vs Causal Language Models
  - Bidirectional vs Autoregressive Language Models
---

Masked language models and autoregressive language models learn from text using different prediction objectives. The key distinction is whether a token can be predicted from context on **both sides** or only from the tokens that come **before it**.

## Summary

- A **masked language model (MLM)** predicts deliberately hidden tokens using both their left and right context.
- An **autoregressive language model (ALM)** predicts the next token using only preceding tokens; it is also called a **causal language model**.
- MLMs usually use bidirectional attention and are well suited to understanding or representation tasks.
- Autoregressive models use causal attention and are naturally suited to generating text from left to right.
- BERT is the best-known masked language model; GPT-2 is a representative autoregressive language model.
- These terms describe training objectives and attention patterns, not merely model size or whether the architecture uses Transformers.

## Masked Language Models

A masked language model learns by hiding selected tokens in an input sequence and predicting their original values. Because the rest of the sequence is visible, the model can use context from both before and after each hidden token.

BERT's original training procedure selected 15% of its WordPiece tokens for prediction. Most selected tokens were replaced by `[MASK]`, while some were replaced by a random token or left unchanged to reduce the mismatch between pre-training and later use.

### Example

Given:

> The cat `[MASK]` on the mat.

The model sees **"The cat"** on the left and **"on the mat"** on the right. It may assign the highest probability to **"sat"**:

> The cat **sat** on the mat.

This objective teaches a rich representation of the entire input. MLMs are commonly adapted to tasks such as classification, sentiment analysis, named-entity recognition, and extractive question answering. They are not naturally open-ended generators because ordinary generation does not provide future tokens or `[MASK]` positions.

MLM are also used for debugging, as they can look at the preceding and following code to identify errors.


## Autoregressive Language Models

An autoregressive language model factorizes the probability of a sequence into a chain of next-token predictions.

At each position, a **causal attention mask** prevents the model from looking at later tokens. During generation, the model predicts one token, appends it to the context, and repeats the process.

### Example

Starting with:

> The cat

The model might generate the sentence one token at a time:

1. `The cat` → predicts `sat`
2. `The cat sat` → predicts `on`
3. `The cat sat on` → predicts `the`
4. `The cat sat on the` → predicts `mat`

Unlike the masked model, it never sees the future words while making a prediction. This matches how text is generated at inference time, making autoregressive models a natural fit for completion, dialogue, summarization, and code generation.

## Comparison

| Aspect | Masked language model | Autoregressive language model |
| --- | --- | --- |
| Training objective | Recover selected hidden tokens | Predict each next token |
| Context available for a prediction | Left and right | Left only |
| Typical attention pattern | Bidirectional | Causal |
| Natural strength | Understanding and contextual representations | Sequential text generation |
| Representative model | BERT | GPT-2 |
| Example input | `The cat [MASK] on the mat.` | `The cat` |
| Example prediction | `sat` at the masked position | `sat`, then `on`, then `the`, and so on |

The distinction is not absolute at the application level: either family can be fine-tuned for many tasks. The training objective nevertheless creates a useful practical bias—MLMs encode complete inputs efficiently, while autoregressive models produce variable-length outputs directly.

## Related

- [[How to use Hugging Face models in Ollama]] — shows `AutoModelForCausalLM`, the Hugging Face class for autoregressive language models.

## Sources

- [Devlin et al. — *BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding*](https://arxiv.org/abs/1810.04805v2)
- [Radford et al. — *Language Models are Unsupervised Multitask Learners*](https://cdn.openai.com/better-language-models/language_models_are_unsupervised_multitask_learners.pdf)
- [OpenAI — *Better Language Models and Their Implications*](https://openai.com/index/better-language-models/)
- [Hugging Face Transformers — *Language Modeling*](https://huggingface.co/docs/transformers/v4.26.0/en/tasks/language_modeling)
