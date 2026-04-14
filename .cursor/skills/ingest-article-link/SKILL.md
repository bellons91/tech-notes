---
name: ingest-article-link
description: Fetches an article from a user-supplied URL, extracts key topics and terms, searches the vault for related notes, then creates or enriches notes with Sources and wikilinks. When a post mixes concepts and tools, prefers a concept note plus tool note(s) with examples from the article, and upgrades index.md glossary stubs to [[wikilinks]]. Use when the user pastes a link to an online article or blog post they want captured in Obsidian/Quartz notes, or asks to summarize or merge external reading into the vault.
---

# Ingest article link into the vault

## When this applies

The user provides **one or more URLs** to online articles or posts they want turned into durable notes: extract substance, map to the vault, **create** or **enrich**, and **cross-link**.

## Repository rules (this project)

- Notes live only under `source/content/`. Do not add narrative content under `source/raw_html`.
- Follow `AGENTS.md`: American English, no secrets or identifying names, treat committed paths as public.
- Match **neighboring notes** for filename style, frontmatter shape, headings, and link style (`[[wikilinks]]` vs paths).

## Workflow

### 1. Fetch and understand the article

1. Retrieve the page (prefer a **fetch** tool that returns readable markdown or HTML converted to text).
2. If access fails (paywall, bot block, empty body): say so briefly, use any still-readable abstract or lede, and **do not invent** missing body details.
3. Produce a short internal picture: **main thesis**, **audience**, **3–8 key concepts or terms**, and anything **actionable** (commands, steps, APIs) only if explicitly present in the fetched text.

### 2. Discover related vault content

Before writing files:

1. Run **semantic search** across `source/content/` for the article’s core concepts and product names.
2. Supplement with **keyword grep** on distinctive terms and existing note titles.
3. List **0–5** plausible related notes with one line each on why they match.

### 3. Decide create vs enrich

| Outcome | Condition |
| --- | --- |
| **Enrich existing** | A note clearly covers the **same topic** as the article (same product feature, same pattern, same glossary entry). Prefer updating one strong hub over scattering duplicates. |
| **Create new** | No note is a close topical match, or the article introduces a **distinct** angle that deserves its own page (then cross-link to partial overlaps). |

If unsure, **create** a focused new note and **link** to nearby notes rather than overloading a weak match.

### 3a. Articles that mix a **concept** with **named tools** (this vault)

Some posts spend meaningful space on **what something means** (definitions, motivation, comparisons) *and* on **specific products or libraries** with **examples** (code, config, CLI). Unless the user asks for a **single** combined page, prefer **splitting** so the graph stays navigable:

| Note | Holds |
| --- | --- |
| **Concept** | Meaning, how it differs from adjacent ideas, when it matters, trade-offs. Keep code minimal or absent. |
| **Tool / product** | What the tool is, how it fits the concept, and **concrete examples from the article** when the article provides them—reformat for readability (syntax highlighting, line breaks); avoid dumping the whole article as an unbroken quote block. |

- Link **both ways**: concept note → `[[Tool]]`; tool note → `[[Concept]]` (often under `## Related`).
- If the article surveys **many** tools in passing, you may add one **overview** note *or* short per-tool stubs; still give a **dedicated** tool note (with examples) for anything that already appears as a **glossary line** in `index.md` or that you expect to link often.

**`source/content/index.md` (glossary-style bullets):** When a stub line uses a **bold product or term** (e.g. `- **ArchUnitNET**: …`) and you created a note for it, **replace the bold name with a `[[wikilink]]`** to that note’s title (match the actual filename / link target used in this vault). Optionally append “see also `[[Concept note]]`” when one short phrase improves discoverability—do not duplicate a full second definition on the index line.

### 4a. Create a new note

1. Pick folder using `AGENTS.md` categories (`azure/`, `Azure CLI/`, `How-to/`, `Cheatsheet/`, etc.) and sibling patterns.
2. For **structure, frontmatter, tags, and Sources formatting**, follow [.cursor/skills/create-topic-page/SKILL.md](../create-topic-page/SKILL.md) with this adjustment: **primary evidence is the single article**—still include a **`## Sources`** section with a markdown link using the **full URL**; add other URLs only if you actually used them.
3. Opening + **`## Summary`**: distill the article; mark uncertainty if the source is opinionated or thin.
4. **`## Related`**: `[[wikilinks]]` to the notes identified in step 2 that genuinely help navigation.

### 4b. Enrich an existing note

1. Read the full target note; preserve the author’s voice; **minimal rewrite** of existing text.
2. Add a dedicated subsection (e.g. **`## Notes from external reading`** or **`## Updates from [Article title](full-url)`**) with bullets or a short paragraph **grounded in the article**—no new factual claims without source support.
3. Append the article to **`## Sources`** if that section exists; otherwise add it with full URL.
4. Update **`tags`** / **`aliases`** only when the new material justifies it (same rules as [optimizing-obsidian-notes](../optimizing-obsidian-notes/SKILL.md)).
5. Add **outbound** `[[wikilinks]]` in the enriched note to any **new** note you created, and add **inbound** links from other strong neighbors if it improves the graph without noise.

### 5. Cross-link and consistency

- **New note** → link to related existing notes in `## Related` or inline where natural.
- **Enriched note** → link to new siblings if you created any.
- **`index.md`**: when the ingested material replaces or clarifies a glossary bullet, prefer **`[[wikilinks]]`** for the main term (see §3a).
- Optionally add a single **“See also”** line in **1–2** highly related hub notes pointing to the new or updated page—avoid spamming many files with marginal mentions.
- After edits, quick-check that new `[[wikilinks]]` targets **exist** under `source/content/` (match actual titles/paths used in this vault).

## Chat response (after edits)

- State **create vs enrich** and list **files touched** with paths.
- Give a **3–6 bullet** takeaway from the article (substance, not metadata).
- Paste the **canonical URL** again for easy copy.

## Checklist (agent)

- [ ] Article fetched or fetch failure explained without fabrication
- [ ] Vault searched; related notes named with rationale
- [ ] Correct branch: new file and/or targeted enrichment
- [ ] If the article mixes **concept + tools**: concept note + tool note(s) per §3a, or a short justification in chat when you intentionally use one combined note
- [ ] Tool notes include **article-grounded examples** (code/config/CLI) when the source supplies them
- [ ] **`index.md`** glossary lines for ingested terms updated to **`[[wikilinks]]`** where a dedicated note exists
- [ ] Full article URL in **Sources** (markdown link, full string)
- [ ] Wikilinks added where they aid navigation; no obvious orphans

## Anti-patterns

- Creating a second full page when an existing hub is clearly the right home.
- **One catch-all note** that merges a broad **concept** and a **primary tool** when the article supports two pages and the vault already surfaces the tool on `index.md`—split instead (§3a).
- Leaving **`index.md`** glossary entries as **bold-only** names when a matching note was created for that term.
- Dumping long quotes instead of a tight summary with a pointer to the URL.
- Adding many tangential wikilinks that do not reflect real topical overlap.
