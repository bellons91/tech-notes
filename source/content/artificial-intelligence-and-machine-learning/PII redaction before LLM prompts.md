---
title: "PII Redaction Before LLM Prompts"
tags:
  - artificial-intelligence
  - data-privacy
  - de-identification
  - llm
  - pii
aliases:
  - Reversible tokenization for LLMs
---

Applications that send user-written text to **third-party model APIs** often expose emails, phone numbers, names, and financial tokens to provider logging, retention, and (depending on contract) training pipelines. This page describes the **gateway pattern**: scrub or tokenize sensitive spans **before** the HTTP call, keep secrets in a **trusted server boundary**, and only **restore** literals where policy allows—so the model can still reason about *which* entity is which without seeing real values.

Implementation with Microsoft’s open-source toolkit is covered in [[Microsoft Presidio]].

## Summary

- **Risk**: outbound prompts and retrieved context can carry PII to vendors, backups, and support tooling unless you treat the model boundary like any other egress point.
- **Reversible tokenization**: replace each detected span with a **stable opaque placeholder** (often numbered per type, e.g. distinct persons stay distinct), call the model on scrubbed text, then map placeholders back in the response path inside your infrastructure.
- **Why numbering matters**: a single generic mask for every person or every email collapses referential structure; multi-party instructions need **distinct placeholders** per span so the model can follow “first person vs second person” logic.
- **Model behavior**: without explicit instructions, models may **rewrite** placeholders into paraphrases or invented names, which breaks string-based restore. System prompts should require **verbatim** copy of placeholder tokens when echoing user content.
- **Confidence trade-offs**: detectors emit scores; very low thresholds increase false positives (e.g. common words as names); very high thresholds leak misses. Tune on **representative traffic**, not a single guessed constant.
- **Layered production posture**: pattern-heavy detection for structured PII, optional second pass (e.g. smaller local model) for messy language or formats, plus a **policy layer** that chooses redact vs block vs allow—and **metrics** on counts and types without logging raw values.
- **When tokenization fails**: tasks that require the **literal** secret (format validation, domain extraction, personalization with a real name) need other controls: synthetic fixtures, on-prem inference ([[Ollama]]), or constrained exposure—not blind substitution.
- **Detection is not policy**: tooling surfaces candidate spans; **compliance and product rules** (quarantine, audit, deny) stay in application code.

## Details

### End-to-end flow

1. Accept user text (and optionally RAG snippets) on the server.
2. Run detection; optionally filter by score and entity type.
3. Substitute placeholders; retain an **ephemeral** token→value map in memory (never send the map to the model).
4. Invoke the remote API with scrubbed messages.
5. Validate model output if placeholders must round-trip (especially smaller open models).
6. Restore literals only for channels that are allowed to show them.

### Governance and limits

Automated PII detection is **probabilistic**: expect false positives, misses, and domain-specific gaps (IDs, order numbers vs phone digits). Combine with [[Defense-in-depth strategy]]: contracts, retention, access control, and periodic review of detection quality.

## Related

- [[Microsoft Presidio]] — analyzer, anonymizer, and extension points used in Python pipelines.
- [[Ollama]] — local inference when literals must not leave your environment.

## Sources

- [Niraj Ranasinghe — “Redacting PII Before It Hits the LLM”](https://nirajranasinghe.medium.com/redacting-pii-before-it-hits-the-llm-0fe9507f05e0)
