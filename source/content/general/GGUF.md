---
aliases:
  - GPT-Generated Unified Format
tags:
  - AI
  - artificial-intelligence
  - file-format
  - ai-model
---

**GGUF (GPT-Generated Unified Format)**: a binary file format for [[LLMs]] that is designed to make [[LLM model|model]] efficient, portable, and easy to run locally, especially on consumer hardware. It is most commonly used with [[inference engine|inference engines]] like [[llama.cpp]], [[Ollama]], [[LMStudio]] and similar.

GGUF is a way to package a [[language model weight|language model's weight]] and [[language model metadata|metadata]] so that it can be loaded quickly, use less memory, and support features like [[quantization]] (eg: 4-bit, 5-bit or 8-bit weights) to reduce model size while still retaining good performance.

Unlike older formats, such as [[GGML]], GGUF stores rich metadata inside the file itself, including [[tokenizer]] info, architecture details, and special tokens, making models more self-contained and less error-prone to load.