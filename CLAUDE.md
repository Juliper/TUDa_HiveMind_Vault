# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repository Is

**TUDa HiveMind Vault** is a collaborative Obsidian knowledge base for TU Darmstadt computer science students. Notes are published as a static website via [Quartz](https://juliper.github.io/TUDa_HiveMind_Quartz/). There are no build, lint, or test commands — this is a content vault, not a software project.

Every push to `main` triggers `.github/workflows/dispatch-to-main.yml`, which fires a `repository_dispatch` event in the separate Quartz repo to rebuild the site.

## Vault Structure

```
<numbered subject folder>/   # e.g. "1 - Software and Hardware", "4 - Artifical Intelligence"
    <module note>.md         # one file per lecture/module
Notes/                       # flat collection of atomic notes (Zettelkasten-style) with subject folder e.g. "1 - Software and Hardware", "4 - Artifical Intelligence"
_templates/
    module.md                # template for module notes
    note.md                  # template + syntax reference for atomic notes
index.md                     # vault landing page
```

Module notes link *to* atomic notes in `Notes/`; they do not contain the concepts themselves. This enables the same atomic note to be linked from multiple modules without duplication.

## Note Conventions

### Frontmatter (required fields)

All notes must have a YAML frontmatter block. Quartz uses these for hover-preview, search, and the graph view.

**Atomic notes** (`Notes/`):
```yaml
---
title: Concept Name
aliases:
  - Alternative Name
tags:
  - topic-tag        # lowercase, hyphen-separated (e.g. cybersecurity, network-security)
description: "One-sentence summary shown in hover previews and search."
draft: false
---
```

**Module notes** (subject folders):
```yaml
---
title: Module Abbreviation
aliases:
  - Full Module Name
tags:
  - fb20             # TU Darmstadt department (always fb20 for CS)
description: ""
draft: false
---
```

### Linking

Use Obsidian `[[WikiLinks]]` for all internal references. Aliases defined in frontmatter are valid link targets. Example: `[[Digital Perimeter Security|defense perimeter]]`.

### Markdown Features

Quartz supports full Obsidian-flavored markdown. Useful syntax (see `_templates/note.md` for examples):
- **Callouts**: `> [!NOTE]`, `> [!IMPORTANT]`, `> [!WARNING]`
- **LaTeX**: inline `$...$` and block `$$...$$`
- **Mermaid diagrams**: fenced code blocks with ` ```mermaid `
- **HTML comments**: `<!-- hidden -->` — not rendered in output
