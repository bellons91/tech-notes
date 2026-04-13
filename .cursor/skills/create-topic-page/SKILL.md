---
name: create-topic-page
description: Researches trustworthy web sources, writes a new Obsidian/Quartz markdown note with frontmatter (title, tags, aliases), an in-note summary, wikilinks where helpful, and a Sources section with full URLs. Use when the user asks to create a new page or note about a specific topic, to document a concept from authoritative references, or to add a research-backed vault article.
---

# Create topic page (vault)

## When this applies

The user wants a **new** markdown page about a **named topic** (not a light edit to an existing note). Execute the full workflow below unless they explicitly narrow the scope (e.g. “outline only” or “no web search”).

## Workflow

### 1. Research (trustworthy sources)

Before drafting, use **web search** and, when useful, **fetch** primary pages.

**Prefer, in order:**

- Vendor or product **official documentation** (e.g. Microsoft Learn, AWS docs, RFC publishers).
- **Standards and specifications** (IETF, W3C, NIST, ISO summaries where full text is paywalled).
- **Open-source project** docs and repos (README, ADRs) for tools and libraries.
- Established reference sites (e.g. MDN for web platform behavior).

**Deprioritize:** anonymous blogs, SEO aggregators, uncited social posts, and duplicated Medium content for factual or security-sensitive claims. If only weak sources exist, say so briefly in the note and qualify statements.

Collect **3–8** distinct URLs where reasonable; fewer is fine for narrow topics if sources are authoritative.

### 2. Choose location and filename

- **Vault root:** `source/content/` (or the folder the user names).
- **Folder:** Infer from topic (`azure/`, `general/`, `how-to/`, etc.). If ambiguous, pick the closest sibling notes and match their folder; one short sentence in chat is enough to explain the choice.
- **Filename:** Match **existing notes in that folder** (this vault often uses descriptive **Title Case with spaces** and `.md`). Do not rename the whole vault to kebab-case as part of this task unless the user asks.

### 3. Write the markdown file

Create the file with:

1. **YAML frontmatter** (same shape as neighbors, e.g. `Cloud Models.md`):

   - `title:` — Title Case string; the human name of the topic.
   - `tags:` — YAML list, **lowercase**, **hyphenated** multi-word tags; **3–8** tags grounded in content (domain, artifact type, product/exam stream if clear). Do not pad with generic tags like `notes` or `misc`.
   - `aliases:` — YAML list of **alternate wikilink targets** readers might type: abbreviations, former names, common synonyms, and shortened forms **without** duplicating the exact `title` unless it helps linking.

2. **Body structure**

   - Opening **1–3 sentences** stating what the page covers and who it is for.
   - **`## Summary`** (or `## TL;DR`) — **5–12 bullet points** or a tight short paragraph capturing the main ideas **from the sources**, not generic filler. Mark uncertainty where sources disagree.
   - **`## Details`** (or multiple `##` sections) — deeper explanation, tables, or lists as appropriate; prefer accurate paraphrase over long quotes.
   - **`## Related`** (optional) — `[[Wikilinks]]` to existing vault notes that genuinely connect; run a quick search in the vault for real note titles/paths. Omit if nothing fits.
   - **`## Sources`** — **Required.** Bulleted list of **markdown links** with meaningful link text; use the **full URL** string (no shortened or elided URLs). Order roughly follows importance or reading order. Optionally add one line per source on what it was used for (factual scope only).

3. **Accuracy and voice**

   - Do not invent APIs, flags, version numbers, or dates; tie claims to what the sources support.
   - Prefer **regional spelling** consistent with the surrounding vault when obvious; otherwise default to clear technical English.

### 4. After saving

In the chat message (in addition to the file):

- **Short summary** of what the page contains (mirror the Summary section in prose).
- **List of sources** (titles + URLs) so the user can skim without opening the file.
- Mention **folder path** and **filename** of the new note.

## Checklist (agent)

- [ ] Web research completed; sources are appropriate for the topic type
- [ ] New `.md` file created under the chosen vault folder
- [ ] Frontmatter: `title`, `tags`, `aliases` present and consistent with neighbors
- [ ] In-note **Summary** section reflects the sources
- [ ] **Sources** section lists every URL used meaningfully, as markdown links with full URLs
- [ ] Optional **Related** wikilinks only to notes that exist

## Anti-patterns

- Creating the page **without** checking the web when the topic is factual, product-specific, or time-sensitive.
- Empty `aliases:` or tags copied from unrelated notes.
- Dropping sources because they were “only used a little” — if a URL informed the text, include it (or remove the claim it supported).
