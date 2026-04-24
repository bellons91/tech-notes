---
title: "Microsoft Presidio"
tags:
  - data-privacy
  - de-identification
  - microsoft-presidio
  - named-entity-recognition
  - open-source
  - pii
  - python
aliases:
  - Presidio
---

**Microsoft Presidio** is an open-source SDK for **identifying** and **anonymizing** sensitive entities in text, images, and structured or semi-structured data. The upstream project documents analyzer and anonymizer pipelines, optional image redaction, structured modules, and deployment patterns from Python through containers ([Presidio documentation](https://microsoft.github.io/presidio/)).

For **why and how** to scrub prompts before calling external [[LLM]] APIs (reversible tokens, system prompts, thresholds, when not to substitute), see [[PII redaction before LLM prompts]].

## Summary

- **Analyzer** returns entity types, spans, and confidence scores using **NER**, **regex**, **rules**, **checksums** (including Luhn-style validation for card-like digit patterns), and context; **Anonymizer** applies operators (mask, replace, hash, encrypt, custom lambdas).
- Extra modules (per official docs): **image redactor** (OCR + detection), **structured** paths for tabular or semi-structured data, samples for **HTTP**, **Kubernetes**, **Spark**, and cloud factories ([Presidio home](https://microsoft.github.io/presidio/)).
- Microsoft warns that automation **does not guarantee** complete detection; pair with monitoring, review, and policy code outside the library ([same](https://microsoft.github.io/presidio/)).
- Typical Python install pairs `presidio-analyzer` and `presidio-anonymizer` with a **spaCy** English pipeline; larger English models improve name recall versus small pipelines at higher download cost.
- Default anonymization can collapse multiple people into one label; **custom operators** emitting numbered placeholders support multi-entity prompts and round-trip restore when combined with a server-side map.
- **`score_threshold`** on `analyze()` reduces noise from weak [[NER]] hits; effective values are workload-specific and should be calibrated on samples.
- **Custom `PatternRecognizer` instances** extend the registry for national IDs, ticket numbers, or other formats; ambiguous regexes benefit from **lower scores plus context words** to limit false positives.

## Details

### Components (official)

From [Microsoft Presidio — home](https://microsoft.github.io/presidio/):

1. Presidio Analyzer — PII identification in text.  
2. Presidio Anonymizer — de-identify detected spans.  
3. Presidio Image Redactor — redact text-bearing PII in images.  
4. Presidio Structured — structured and semi-structured workflows.

### Installation

```bash
pip install presidio-analyzer presidio-anonymizer
python -m spacy download en_core_web_lg
```

The large English model is heavier on disk but generally improves recall on person-like entities compared to `en_core_web_sm`.

### Minimal analyze → anonymize

```python
from presidio_analyzer import AnalyzerEngine
from presidio_anonymizer import AnonymizerEngine

analyzer = AnalyzerEngine()
anonymizer = AnonymizerEngine()
text = "Hi, I'm Alex. Email me at user@example.com or call +1-555-0100."
results = analyzer.analyze(text=text, language="en")
anonymized = anonymizer.anonymize(text=text, analyzer_results=results)
print(anonymized.text)
# Typical default output shape (labels depend on built-in operators):
# Hi, I'm <PERSON>. Email me at <EMAIL_ADDRESS> or call <PHONE_NUMBER>.
```

Default operators tend to reuse the same placeholder per type, which is easy to read but **not** ideal when the model must distinguish two people or two emails; see the numbered-token pattern below.

### Numbered placeholders and restore

Using a **custom** anonymization operator keeps a `token → original` map server-side only:

```python
from presidio_analyzer import AnalyzerEngine
from presidio_anonymizer import AnonymizerEngine
from presidio_anonymizer.entities import OperatorConfig


class PromptCleaner:
    def __init__(self):
        self.analyzer = AnalyzerEngine()
        self.anonymizer = AnonymizerEngine()

    def clean(self, text: str):
        results = self.analyzer.analyze(text=text, language="en")
        mapping = {}
        counter = {}

        def tokenize(original, params):
            entity_type = params["entity_type"]
            counter[entity_type] = counter.get(entity_type, 0) + 1
            token = f"<{entity_type}_{counter[entity_type]}>"
            mapping[token] = original
            return token

        anonymized = self.anonymizer.anonymize(
            text=text,
            analyzer_results=results,
            operators={"DEFAULT": OperatorConfig("custom", {"lambda": tokenize})},
        )
        return anonymized.text, mapping

    def restore(self, text: str, mapping: dict) -> str:
        for token, original in mapping.items():
            text = text.replace(token, original)
        return text
```

Example usage:

```python
cleaner = PromptCleaner()
prompt = "Email Alex at user@example.com and CC Blake at blake@example.com"
cleaned, mapping = cleaner.clean(prompt)
# cleaned might read: Email <PERSON_1> at <EMAIL_ADDRESS_1> and CC <PERSON_2> at <EMAIL_ADDRESS_2>
# Send `cleaned` to the model API, then `cleaner.restore(model_reply, mapping)` for allowed surfaces.
```

Models should be instructed to **copy placeholders exactly**; otherwise restoration by string replace becomes unreliable.

### Analyzer threshold

```python
results = analyzer.analyze(text=text, language="en", score_threshold=0.5)
```

Interpret bands (rough guidance from practitioner calibration, not universal constants): lower thresholds catch more spans but increase false positives; very high thresholds miss sensitive content. Validate against your own traffic.

### Custom pattern recognizer

Register regex-based entities when built-ins omit a jurisdiction- or product-specific format:

```python
from presidio_analyzer import Pattern, PatternRecognizer

doc_id_recognizer = PatternRecognizer(
    supported_entity="REGIONAL_DOC_ID",
    patterns=[
        Pattern(name="format_a", regex=r"\b\d{9}[VvXx]\b", score=0.9),
        Pattern(name="format_b", regex=r"\b\d{12}\b", score=0.4),
    ],
    context=["identity", "national", "document", "id"],
)

analyzer = AnalyzerEngine()
analyzer.registry.add_recognizer(doc_id_recognizer)
```

Ambiguous patterns (e.g. long digit runs) are safer with **moderate scores** and **context** so they fire near qualifying words, not on arbitrary numbers.

## Related

- [[PII redaction before LLM prompts]] — gateway architecture, policy, and model-instruction considerations.
- [[Ollama]] — local inference when literals cannot go to a vendor.
- [[Microsoft Purview]] — broader Microsoft data governance (separate product, overlapping goals).
- [[Defense-in-depth strategy]] — Presidio as one control among many.

## Sources

- [Niraj Ranasinghe — “Redacting PII Before It Hits the LLM”](https://nirajranasinghe.medium.com/redacting-pii-before-it-hits-the-llm-0fe9507f05e0) — Python patterns, thresholds, system-prompt guidance, layered operations, and [companion sample code](https://github.com/nirajshiwantha/Presidio-PII)
- [Microsoft Presidio — documentation](https://microsoft.github.io/presidio/)
- [microsoft/presidio — GitHub](https://github.com/microsoft/presidio)
