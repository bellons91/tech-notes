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
- [ ] Broken links checked and fixed or listed
- [ ] Filename kebab-case (if renaming)
- [ ] Inbound links updated (wikilinks + Markdown + embeds)
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
- Short **intro sentence** stating what the reader will do.
- Fix **obvious** formatting: fenced languages on code blocks, spacing around lists, broken fences.
- Preserve tone and technical intent; do not paste unverified facts.

---

## 3. Suggestions block (required output)

After edits (or in the PR/chat message), provide a compact **Suggestions** section:

1. **Structure** — e.g. “Add a Prerequisites H2”, “Split JSON dump into Details”, “Promote repeated flags to a table”.
2. **Missing tags (in content or frontmatter)** — list tag names that would help; include **new** tags if they map to real themes in the note.
3. **Crosslinks** — list existing vault notes that should be linked (with `[[Note Title]]` or relative paths per convention). To find candidates, search the vault for shared keywords, product names, or prior notes on the same topic.

---

## 4. Broken links

Check both **wikilinks** and **Markdown** links:

- `[[Some Note]]`, `[[folder/Some Note.md|alias]]`, `![[embed]]`
- `[text](../path/file.md)` and site-relative `/` links if used

**Method (pick what fits the environment):**

- Search the vault for each distinct link target; confirm a matching `.md` (or configured extension) exists after applying Quartz/Obsidian path rules.
- Flag **ambiguous** targets (multiple matches); prefer explicit paths if the vault allows.

Output: **fixed** links inline, or a **Broken links** list with recommended target.

If the broken link is a wikilink, then ask if you have to create a page for that element. If the user confirms the action, then create a new note with that name a populate it with a brief description taken from the Internet. It may happen that the page actually exists, but you did not notice. Check with the user what they want to do with the broken wikilink (but do it at the end of the optimization).

---

## 5. Rename file to kebab-case

- **Filename**: lower case, words separated by `-`, only safe characters (`[a-z0-9-]` plus allowed Unicode if the vault already uses it—default ASCII kebab).
- **Page title**: stays **Title Case** in `title:` and typically the H1.
- **Do not** change the displayed title to kebab-case.

**Example**

- From: `Azure Storage Scripts.md`
- To: `azure-storage-scripts.md`
- Frontmatter: `title: "Azure Storage Scripts"`

---

## 6. Update inbound references after rename

When the filename or path changes, search the **entire vault root** for references to the old name:

- Old basename without extension in wikilinks: `[[Azure Storage Scripts]]`
- Old path segments in Markdown links
- Query params or anchors if present

Replace with the **new** wikilink or path. Re-run the **broken links** pass on edited files.

Use ripgrep-style patterns (adapt for Windows paths):

```bash
rg -n "Old Filename|old-slug|old-folder/old-file" path/to/vault
```

For this repo, default vault path in commands: `source/content`.

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
