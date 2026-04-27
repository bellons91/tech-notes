---
title: How to use Hugging Face models in Ollama
tags:
  - ollama
  - hugging-face
  - gguf
  - llm
  - artificial-intelligence
  - ai
aliases:
  - Ollama Hugging Face
  - Run HuggingFace models locally
---

A guide to pulling and running models from Hugging Face inside [[Ollama]] when the model you need is not listed on `ollama.com`. Ollama only supports models in [[GGUF]] format.

## Summary

- Hugging Face hosts thousands of open-weight models, many available as [[GGUF]] files ready for local inference.
- Ollama accepts Hugging Face model IDs directly if the repository contains GGUF files; prefix the name with `huggingface.co/`.
- If the model is not already in GGUF format, download it via the `transformers` Python library and convert it with `llama.cpp`.
- A Modelfile lets you import a locally stored `.gguf` file and customise model behavior (system prompt, temperature) before creating a named Ollama model.

## Method 1 — Run a model directly from Hugging Face

1. Browse [huggingface.co](https://huggingface.co) and apply the **GGUF** filter to find a compatible model.
2. Pull and run the model by prefixing its path with `huggingface.co/`:

```bash
ollama run huggingface.co/unsloth/QwQ-32B-GGUF
```

To run a specific [[quantized]] variant, append the variant tag:

```bash
ollama run huggingface.co/unsloth/QwQ-32B-GGUF:Q4_K_M
```

> If you see `400: Repository is not GGUF or is not compatible with llama.cpp`, the repository does not contain GGUF files. Use Method 2 or convert the model first (see below).

Quantized variants (e.g. `Q4_K_M`, `Q8_0`) trade a small amount of accuracy for lower memory use and faster inference — useful on CPUs and low-VRAM GPUs.

## Method 2 — Import a locally downloaded model with a Modelfile

Use this approach when you have already downloaded a `.gguf` file to disk, or when you need to set custom model parameters.

1. Download the GGUF file from the model's **Files** tab on Hugging Face (e.g. `QwQ-32B-Q4_K_M.gguf`).

2. Create a plain text file named `Modelfile` (no extension) in the same directory:

```
FROM ./downloads/QwQ-32B-Q4_K_M.gguf
SYSTEM "You are a helpful AI assistant."
PARAMETER temperature 0.7
```

3. Build a named Ollama model from the Modelfile:

```bash
ollama create my-model -f Modelfile
```

4. Verify it appears in the local model list:

```bash
ollama list
```

5. Run the model:

```bash
ollama run my-model
```

## Converting a Hugging Face model to GGUF

When a GGUF version of the model is not available on Hugging Face, convert it yourself using `llama.cpp`.

**Prerequisites:** `llama.cpp` installed ([github.com/ggml-org/llama.cpp](https://github.com/ggml-org/llama.cpp)) and the `transformers` Python package.

### Step 1 — Download the model

```python
from transformers import AutoModelForCausalLM, AutoTokenizer

model_id = "meta-llama/Llama-3.2-3B-Instruct"

tokenizer = AutoTokenizer.from_pretrained(model_id)
model = AutoModelForCausalLM.from_pretrained(model_id)
```

The model is saved to `~/.cache/huggingface/hub/` (macOS/Linux) or `C:\users\<username>\.cache\huggingface\hub\` (Windows).

### Step 2 — Convert to GGUF

Run the conversion script bundled with `llama.cpp`, pointing it at the downloaded snapshot directory:

```bash
cd ~/llama.cpp
python convert_hf_to_gguf.py \
  ~/.cache/huggingface/hub/models--meta-llama--Llama-3.2-3B-Instruct/snapshots/<snapshot-hash> \
  --outfile /path/to/Llama-3.2-3B-Instruct.gguf
```

Replace `<snapshot-hash>` with the actual hash folder name created by the `transformers` download.

Once the `.gguf` file is produced, import it into Ollama with a Modelfile as described in Method 2.

## Related

- [[Ollama]] — overview of local LLM deployment, CLI usage, and Modelfile syntax.
- [[GGUF]] — binary model format used by Ollama and llama.cpp; covers quantization levels.

## Sources

- [Running Large Language Models Locally Using Ollama — CODE Magazine](https://www.codemag.com/Article/264031/Running-Large-Language-Models-Locally-Using-Ollama)
