---
name: optimizing-obsidian-notes
description: Use when the user is refining existing Obsidian or Quartz vault notes and mentions frontmatter, tags, note structure, wikilinks or crosslinks, broken links, kebab-case filenames, or inbound references after a rename.
---

# Optimizing Obsidian / Quartz notes

## Goal

Take one note from “drafty” to **consistent, discoverable, and link-safe** without changing the author’s meaning. Prefer small, reversible edits; batch risky renames with a repo-wide search plan.

## Before you touch files

1. Identify the **vault root** (often `content/`, `source/content/`, or the folder that contains the note tree). **In this repository, notes live under `source/content/`.**
2. Sample **2–3 nearby notes** for conventions: frontmatter keys (`title`, `tags`, `draft`, `aliases`), tag style (YAML list vs comma-separated), heading level for page title, link style (`[[wikilinks]]` vs relative Markdown).
3. Match those conventions unless the user asked to migrate the whole vault.

## Workflow (checklist)

Copy into todos when optimizing multiple notes:

- [ ] Frontmatter complete (`title`, `tags`, plus any project-required keys)
- [ ] Body edited for clarity and structure (minimal rewrite)
- [ ] Suggestions delivered (structure, inline tags, crosslinks)
- [ ] Filename kebab-case (if renaming)
- [ ] Content correctness, ensuring info is up to date

---

## 1. Frontmatter

**If frontmatter is missing**, insert YAML at the top:

```yaml
---
title: "Human Readable Title In Title Case"
tags: 
  - topic
  - tool
  - optional-subtopic
---
```

Adjust to vault style:

- **Tags**: use the same shape as sibling files (bullet list. Comma-separated `a, b, c` arrays are NOT supported.). Keep tags **lowercase**, **hyphenated multi-words** unless the vault already uses another rule.
- **`title`**: Title Case string. It should match the **intended page title**, usually aligned with the first `#` heading after optimization.
- **Do not** invent dates or `lastmod` unless the project already tracks them.

**Derive tags from content** (3–8 tags typical):

- Primary domain (e.g. `azure`, `kubernetes`)
- Artifact type (`cli`, `script`, `architecture`, `cheatsheet`)
- Exam/cert/workstream if clearly the focus (`az-204`)
- Add **new** tags when they improve browse/search and appear justified by the text—not generic filler (`notes`, `misc`).

---

## 2. Optimize the body (light touch)

- One clear **H1** (or follow vault rule if H1 is reserved for Quartz layout).
- Logical **H2/H3** sections; move long command blocks under “Commands” or “Examples”.
- Fix **obvious** formatting: fenced languages on code blocks, spacing around lists, broken fences.
- Preserve tone and technical intent; do not paste unverified facts.

---

## 3. Suggestions block (required output)

After edits (or in the PR/chat message), provide a compact **Suggestions** section:

1. **Structure** — e.g. “Add a Prerequisites H2”, “Split JSON dump into Details”, “Promote repeated flags to a table”.
2. **Missing tags (in content or frontmatter)** — list tag names that would help; include **new** tags if they map to real themes in the note.
3. **Crosslinks** — list existing vault notes that should be linked (with `[[Note Title]]` or relative paths per convention). To find candidates, search the vault for shared keywords, product names, or prior notes on the same topic.

---


## 4. Rename file to kebab-case

- **Filename**: lower case, words separated by `-`, only safe characters (`[a-z0-9-]` plus allowed Unicode if the vault already uses it—default ASCII kebab).
- **Page title**: stays **Title Case** in `title:` and typically the H1.
- **Do not** change the displayed title to kebab-case.

**Example**

- From: `Azure Storage Scripts.md`
- To: `azure-storage-scripts.md`
- Frontmatter: `title: "Azure Storage Scripts"`

---

## Common mistakes

| Mistake | Fix |
|--------|-----|
| `title` matches filename slug | Set `title` to Title Case; keep slug in filename only |
| Tags duplicate the folder name only | Add content-specific tags (commands, services, scenarios) |
| Wikilink updated but embed `![[...]]` missed | Search `![[` separately |
| Quartz permalink/slug fields ignored | If the project uses `permalink` or `aliases`, update per existing notes |
| Rename without vault-wide search | Always grep for old basename and old title variants |

---

## Quick reference

| Item | Rule |
|------|------|
| Frontmatter | Required keys per vault; always include `title` + `tags` when missing |
| Tags | From content; lowercase; hyphenated; 3–8 typical |
| Suggestions | Structure + tags + crosslinks |
| Links | Wikilink + Markdown; list unfixed |
| Filename | kebab-case |
| Display title | Title Case in `title` / H1 |
| Rename follow-up | Update all inbound references; re-validate links |
