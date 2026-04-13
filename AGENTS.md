# Agent instructions — personal tech notes (Quartz + Obsidian)

## What this repository is

This repo holds **technical notes** distilled from articles, videos, and courses. The goal is to **organize ideas** in a durable, linkable form. The author is the primary consumer of the content.

## Audience and visibility

- **GitHub repository:** public.
- **Published site:** publicly reachable, but **intended readership is the author only** (a personal reference / digital garden, not a product or blog for a general audience).
- Treat every committed path as **eventually public**: avoid sensitive or identifying information (see below).

## Where to edit

- **Notes and Markdown live under** `source/content/` **only.** Do not rely on or add content under `source/raw_html` for this project.

## Language and style

- Write primarily in **English**, using **American English** spelling and conventions.
- Optimize for **clarity and correctness** over flourish.
- Prefer **Mermaid** diagrams when a visual structure helps (flows, relationships, sequences).

## Information architecture (folders)

Use folders consistently as **high-level categories** (examples already in use):

| Area | Purpose |
|------|--------|
| **Azure** | Broad notes on Azure services and concepts. |
| **Azure CLI** | Command-line usage, scripts, and CLI-oriented workflows. |
| **Cheatsheet** | Quick references for scripts, languages, and compact lookups. |
| **How-to** | Short guides for **repetitive operations** that are easy to forget. |

**`index.md`:** Use for **quick facts** or stubs on topics that do **not** warrant a full page yet (too little information to justify a dedicated note).

When creating or moving notes, place them under the folder that best matches this intent; prefer **cross-links** between related notes over duplicating content.

## Files, titles, and frontmatter

- **File names:** `kebab-case.md` (e.g. `azure-storage-account-scripts.md`). Established entry points such as `index.md` may stay as-is.
- **Human-facing title:** **Title Case** in the document (heading or frontmatter `title`), aligned with the note’s subject.
- **Frontmatter:** All fields are **optional** today, but the direction is to **standardize** usage. When adding or editing frontmatter, prefer consistent keys:
  - `title` — Title Case; matches or clarifies the in-note heading.
  - `tags` — meaningful, searchable labels (Azure area, tool, language, pattern, etc.).
  - `aliases` — alternate titles or spellings readers (or the author) might search for.

## Linking and discoverability (priority for assistants)

When editing or authoring notes, optimize for **searchability and navigation**:

- Use **meaningful tags** and keep them consistent with existing notes where possible.
- Add **wikilinks or paths** to related notes and to the **right category** (folder + links), so the graph and search stay useful.
- Prefer short **How-to** and **Cheatsheet** entries that link out to deeper **Azure** / topic pages instead of one oversized page.

## Privacy and safety

- **Do not** include **personal names** or **client / customer names** in committed content.
- Do not store secrets (passwords, API keys, tokens, connection strings with credentials). Use placeholders and describe where secrets live (e.g. environment variables, vault), not the values.

## Quartz / build context (reference)

- Site is generated with **Quartz** from `source/content`. Configuration lives under `source/` (e.g. `quartz.config.ts`, `quartz.layout.ts`).
- Local preview (from repo docs): run `npx quartz build --serve` in `./source/`.

When unsure about Quartz-specific behavior, prefer the official Quartz documentation over guessing.
