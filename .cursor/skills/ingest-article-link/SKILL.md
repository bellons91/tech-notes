---
name: ingest-article-link
description: Use when the user pastes a URL to an online article or post they want captured in Obsidian/Quartz notes, asks to summarize or merge external reading into the vault, or wants article content turned into durable linked notes.
---

# Ingest article link into the vault

## When this applies

The user provides **one or more URLs** to online articles or posts they want turned into durable notes: after fetching, they get a **short quiz** on the article (unless they opt out), then answers are graded, then substance is mapped to the vault to **create** or **enrich** and **cross-link**.

## Repository rules (this project)

- Notes live only under `source/content/`. Do not add narrative content under `source/raw_html`.
- Follow `AGENTS.md`: American English, no secrets or identifying names, treat committed paths as public.
- Match **neighboring notes** for filename style, frontmatter shape, headings, and link style (`[[wikilinks]]` vs paths).

## Workflow

**Order matters:** fetch and read the source first, then deliver a **quiz** and **wait for the user’s answers**. Only after grading may you search the vault and create or edit notes. If the user explicitly asks to **skip the quiz**, proceed straight from fetch to vault work (still no fabrication).

### 1. Fetch and understand the article

1. Retrieve the page (prefer a **fetch** tool that returns readable markdown or HTML converted to text).
2. If access fails (paywall, bot block, empty body): say so briefly, use any still-readable abstract or lede, and **do not invent** missing body details.
3. Produce a short internal picture: **main thesis**, **audience**, **3–8 key concepts or terms**, and anything **actionable** (commands, steps, APIs) only if explicitly present in the fetched text.

### 2. Pre-ingest quiz (first user-facing step after fetch)

**Before** semantic search, file reads for enrichment, or any writes under `source/content/`:

1. Follow **[.cursor/skills/knowledge-quiz/SKILL.md](../knowledge-quiz/SKILL.md)** for quiz shape and grading later: **3–5** single-choice items (A–D, exactly one correct each), **1–2** short open questions, answer-sheet reply line, and **do not** publish the answer key until the user has answered.
2. Base every question on the **fetched article only** (plus standard definitions that the article clearly assumes). If the body is too thin for a fair quiz, say so, ask **1–2** open questions on what is readable, still wait for a reply, then continue—**do not** invent article specifics to pad a quiz.
3. **Stop** after posting the quiz: do not create or edit notes until the user submits answers in a follow-up message.
4. If multiple URLs were given, one quiz may cover the combined reading; if sources are unrelated, split into short labeled sections (Source A / Source B) within the same quiz block.

### 3. Grade answers and collect reinforcement topics

When the user replies with answers:

1. Grade per **knowledge-quiz**: MCQ right/wrong with brief corrections; open questions for accuracy and completeness; short summary of strengths and gaps.
2. Maintain an internal list of **reinforcement topics**: each **incorrect** MCQ choice and each **wrong or incomplete** open-answer theme (the underlying idea they need to understand, not chat meta-commentary).

### 4. Discover related vault content

Before writing files:

1. Run **semantic search** across `source/content/` for the article’s core concepts and product names.
2. Supplement with **keyword grep** on distinctive terms and existing note titles.
3. List **0–5** plausible related notes with one line each on why they match.

### 5. Decide create vs enrich

| Outcome | Condition |
| --- | --- |
| **Enrich existing** | A note clearly covers the **same topic** as the article (same product feature, same pattern, same glossary entry). Prefer updating one strong hub over scattering duplicates. |
| **Create new** | No note is a close topical match, or the article introduces a **distinct** angle that deserves its own page (then cross-link to partial overlaps). |

If unsure, **create** a focused new note and **link** to nearby notes rather than overloading a weak match.

### 5a. Articles that mix a **concept** with **named tools** (this vault)

Some posts spend meaningful space on **what something means** (definitions, motivation, comparisons) *and* on **specific products or libraries** with **examples** (code, config, CLI). Unless the user asks for a **single** combined page, prefer **splitting** so the graph stays navigable:

| Note | Holds |
| --- | --- |
| **Concept** | Meaning, how it differs from adjacent ideas, when it matters, trade-offs. Keep code minimal or absent. |
| **Tool / product** | What the tool is, how it fits the concept, and **concrete examples from the article** when the article provides them—reformat for readability (syntax highlighting, line breaks); avoid dumping the whole article as an unbroken quote block. |

- Link **both ways**: concept note → `[[Tool]]`; tool note → `[[Concept]]` (often under `## Related`).
- If the article surveys **many** tools in passing, you may add one **overview** note *or* short per-tool stubs; still give a **dedicated** tool note (with examples) for anything that already appears as a **glossary line** in `index.md` or that you expect to link often.

**`source/content/index.md` (glossary-style bullets):** When a stub line uses a **bold product or term** (e.g. `- **ArchUnitNET**: …`) and you created a note for it, **replace the bold name with a `[[wikilink]]`** to that note’s title (match the actual filename / link target used in this vault). Optionally append “see also `[[Concept note]]`” when one short phrase improves discoverability—do not duplicate a full second definition on the index line.

### 6a. Create a new note

1. Pick folder using `AGENTS.md` categories (`azure/`, `Azure CLI/`, `How-to/`, `Cheatsheet/`, etc.) and sibling patterns.
2. For **structure, frontmatter, tags, and Sources formatting**, follow [.cursor/skills/create-topic-page/SKILL.md](../create-topic-page/SKILL.md) with this adjustment: **primary evidence is the single article**—still include a **`## Sources`** section with a markdown link using the **full URL**; add other URLs only if you actually used them.
3. Opening + **`## Summary`**: distill the article; mark uncertainty if the source is opinionated or thin.
4. **`## Related`**: `[[wikilinks]]` to the notes identified in step 4 that genuinely help navigation.
5. **Reinforcement from quiz gaps (notes only):** If the **reinforcement topics** list from step 3 is **non-empty**, for each topic add clear explanatory prose (a short subsection or integrated paragraphs) so future readers understand that idea in context of the article. Write it like normal reference material—definitions, contrasts, steps, or boundaries the article supports. If the list is **empty** (everything correct and complete), do not add filler “reinforcement” sections—keep the note to the usual summary and article-grounded content. **Do not** state or imply that text exists because of a quiz, a wrong answer, practice, or a knowledge check (forbidden examples: “after the quiz”, “you missed”, “common mistake on the questions”, “to address your answer”). In chat, summarizing quiz results is fine; in vault files, keep an encyclopedic tone.

### 6b. Enrich an existing note

1. Read the full target note; preserve the author’s voice; **minimal rewrite** of existing text.
2. Add a dedicated subsection (e.g. **`## Notes from external reading`** or **`## Updates from [Article title](full-url)`**) with bullets or a short paragraph **grounded in the article**—no new factual claims without source support.
3. Apply the same **reinforcement** rules as in **6a**: weave in extra explanation for **reinforcement topics** in the same neutral reference voice; never attribute those additions to quiz performance.
4. Append the article to **`## Sources`** if that section exists; otherwise add it with full URL.
5. Update **`tags`** / **`aliases`** only when the new material justifies it (same rules as [optimizing-obsidian-notes](../optimizing-obsidian-notes/SKILL.md)).
6. Add **outbound** `[[wikilinks]]` in the enriched note to any **new** note you created, and add **inbound** links from other strong neighbors if it improves the graph without noise.

### 7. Cross-link and consistency

- **New note** → link to related existing notes in `## Related` or inline where natural.
- **Enriched note** → link to new siblings if you created any.
- **`index.md`**: when the ingested material replaces or clarifies a glossary bullet, prefer **`[[wikilinks]]`** for the main term (see section 5a).
- Optionally add a single **“See also”** line in **1–2** highly related hub notes pointing to the new or updated page—avoid spamming many files with marginal mentions.
- After edits, quick-check that new `[[wikilinks]]` targets **exist** under `source/content/` (match actual titles/paths used in this vault).

## Chat response (after edits)

- Briefly recap **quiz grading** (optional if skipped): what was wrong/right at a high level; full per-question grading already belongs in the grading message.
- State **create vs enrich** and list **files touched** with paths.
- Give a **3–6 bullet** takeaway from the article (substance, not metadata).
- Paste the **canonical URL** again for easy copy.

## Checklist (agent)

- [ ] Article fetched or fetch failure explained without fabrication
- [ ] **Quiz** delivered per **knowledge-quiz** and **step 2**; user answers received and **graded** before vault writes (unless user opted out of quiz)
- [ ] **Reinforcement topics** from wrong/incomplete answers addressed in notes with **neutral** prose (no quiz attribution in files)
- [ ] Vault searched; related notes named with rationale
- [ ] Correct branch: new file and/or targeted enrichment
- [ ] If the article mixes **concept + tools**: concept note + tool note(s) per section 5a, or a short justification in chat when you intentionally use one combined note
- [ ] Tool notes include **article-grounded examples** (code/config/CLI) when the source supplies them
- [ ] **`index.md`** glossary lines for ingested terms updated to **`[[wikilinks]]`** where a dedicated note exists
- [ ] Full article URL in **Sources** (markdown link, full string)
- [ ] Wikilinks added where they aid navigation; no obvious orphans

## Anti-patterns

- **Writing notes before** the user answers the pre-ingest quiz (when a quiz was required).
- **Mentioning the quiz, wrong answers, or “extra explanation because you missed X”** inside `source/content/` markdown.
- Creating a second full page when an existing hub is clearly the right home.
- **One catch-all note** that merges a broad **concept** and a **primary tool** when the article supports two pages and the vault already surfaces the tool on `index.md`—split instead (section 5a).
- Leaving **`index.md`** glossary entries as **bold-only** names when a matching note was created for that term.
- Dumping long quotes instead of a tight summary with a pointer to the URL.
- Adding many tangential wikilinks that do not reflect real topical overlap.
