---
tags:
  - artificial-intelligence
  - AI
  - ai-model
  - ollama-cli
---

Platform that provides local deployment and management of [[LLMs]].
It allows you to run models locally, which means your data never leave the device.

It comes with a desktop application and a CLI.

## Modelfile

You can customize a model by creating a modelfile (type of format with no file extension). A modelfile allows you to add additional instructions to a [[LLM model]],

Example of *C:/_whatever_/joyfulmodel*:

```file
FROM llama 3.2
SYSTEM "You are an IT assistant that helps users with sparkling joy"
```

To use it, you first generate the related model, using that file as a source

```cmd
ollama create my-custom-model -f joyfulmodel
```

This CLI command will create a new model locally, so that you can run

```cmd
ollama run my-custom-model 
```
to start conversating with it.

## Related

- [[How to use Hugging Face models in Ollama]] — pull GGUF models from Hugging Face or convert and import them with a Modelfile.
- [[GGUF]] — the binary model format Ollama uses for local inference.