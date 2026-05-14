# PDF Lecture Ingest for TUDa HiveMind Vault

You are ingesting lecture PDFs into an Obsidian Zettelkasten vault for TU Darmstadt CS students. Your job: extract concepts from PDF slides, create atomic notes, and wire them into the module note.

The user will attach one or more PDFs and provide context (module name, lecture number, topic tags, etc.) in their prompt: $ARGUMENTS

## Vault Constants

**Vault root:** `/Users/juliper/Projects/Obsidian/Hive Mind/TUDa_HiveMind_Vault`

### Subject Folders (contain module notes)

| Folder | Topics |
|---|---|
| `1 - Software and Hardware` | Systems programming, hardware design, digital logic |
| `2 - Cybersecurity and Privacy` | Security, cryptography, network defense |
| `3 - Complex Networked Systems` | Networking, distributed systems, databases |
| `4 - Artifical Intelligence` | ML, AI, data science |
| `5 - Theorie` | Formal languages, automata, logic |
| `6 - Mathmatics` | Math courses |
| `7 - Language courses` | Natural language courses (Chinese, etc.) |

### Notes Subfolders (contain atomic notes)

Map your content to the best-matching subfolder:

| Subfolder | Use for |
|---|---|
| `Notes/Software and Hardware/` | Hardware, OS, low-level systems |
| `Notes/Cybersecurity and Privacy/` | Security, crypto, privacy |
| `Notes/Complex Networked Systems/` | Networking, databases, distributed systems |
| `Notes/Artifical Intelligence/` | ML, AI, NLP |
| `Notes/Theorie/` | Formal methods, logic, automata |
| `Notes/Mathmatics/` | Pure math, linear algebra, statistics |
| `Notes/Language Courses/` | Natural language learning |

### Module Note Template

When creating a new module note, use this structure:

```markdown
---
title: Module Abbreviation
aliases:
  - Full Module Name
tags:
  - fb20
description: "One-line module summary."
draft: false
---

# Syllabus

| Moodle      | [Link](url) |
| ----------- | ----------- |
| Dozent      | Name        |
| Prüfungsform | Type |

# Vorlesungen

## Lecture N - Topic

### Subtopic A
- [[Concept A]]
- [[Concept B]]

### Subtopic B
- [[Concept C]]

# Klausurvorbereitung

> [!IMPORTANT] Prüfungsrelevant
> TBD
```

### Atomic Note Template

```markdown
---
title: Concept Name in English
aliases:
  - German Alias (if common)
  - Abbreviation
tags:
  - topic-tag
description: "One-sentence summary - shown in hover previews and search"
draft: false
---

Clear explanation. Start with what it IS, then why it matters.

## How It Works

Details, algorithms, formulas ($n = \lceil \log_2 m \rceil$), tables.

## Example

Concrete example.

## Related Concepts

- [[Other Note]]: brief reason for link
```

## Step-by-Step Process

### Phase 1: Read the PDF(s)

1. Read the PDF in chunks of 20 pages. Start with pages 1-20, then 21-40, etc.
2. Read ALL pages before proceeding - don't start writing notes after reading only part of the PDF.
3. While reading, mentally catalog: what are the distinct concepts covered? What's the lecture structure?

### Phase 2: Find the Module Note

1. Identify the module note from the user's prompt (they'll name the module).
2. Read the existing module note to understand what's already documented.
3. If the module note doesn't exist, ask the user which subject folder it belongs in, then create it following `_templates/module.md`.

### Phase 3: Plan Atomic Notes

Create an atomic note for **every** concept from the lecture. Every concept gets its own `.md` file - never write explanations inline in the module note. A good atomic note:
- Covers **one self-contained concept** (not a whole lecture topic)
- Is **reusable** - could be linked from multiple modules
- Examples: "Dictionary Encoding", "SIMD", "Run-Length Encoding" - not "Lecture 3 Summary"
- Even small concepts (a single definition or principle) get their own note

Before writing anything, check if each note already exists:
```bash
find "<vault>/Notes" -iname "<concept-name>*" -type f
```

- **Note exists and PDF adds substantial new info** → append to it (new section or expand existing sections)
- **Note exists and PDF adds nothing new** → skip, just link from module note
- **Note doesn't exist** → create it

### Phase 4: Write Atomic Notes

For each new atomic note, follow this format exactly:

```markdown
---
title: Concept Name in English
aliases:
  - German Alias (if common)
  - Abbreviation or alternative name
tags:
  - topic-tag-1
  - topic-tag-2
description: "One-sentence summary - shown in hover previews and search"
draft: false
---

> [!NOTE] Definition
> Concise definition of the concept.

Clear explanation of the concept. Start with what it IS, then why it matters.

## How It Works

Mechanics, algorithms, or detailed explanation. Use LaTeX for formulas:
$n = \lceil \log_2 m \rceil$

Use tables for comparisons. Use Mermaid diagrams to visualize processes or relationships where helpful.

## Example

A concrete example that makes the concept click.

> [!IMPORTANT]
> Key takeaway or common pitfall worth highlighting.

## Related Concepts

- [[Other Note]]: brief reason for link
```

**Style rules:**
- **All notes in English** - titles, prose, descriptions, everything
- German aliases in frontmatter only if a common German term exists
- **Description in English**, one sentence, no period at end
- **Tags**: lowercase, hyphen-separated, drawn from the lecture topic area
- **No em-dashes or en-dashes** - never use `---` (em-dash) or `--` (en-dash) unicode characters, always use regular hyphens `-` instead
- Use **LaTeX** for any math: inline `$...$`, block `$$...$$`
- Use **tables** for structured comparisons
- Use **callouts** generously to break up text and highlight key points: `> [!NOTE]`, `> [!IMPORTANT]`, `> [!WARNING]`
- Use **Mermaid** diagrams actively to visualize relationships, processes, hierarchies, and comparisons - they make notes more engaging and scannable
- Link generously with `[[WikiLinks]]` to other concepts - both existing and newly created

### Phase 5: Update the Module Note

Add a new lecture section to the module note. Follow the style of `IT-Sicherheit.md` - subtopics with bullet-point links to atomic notes:

```markdown
## Lecture N - Topic Title

### Subtopic A
- [[Concept A]]
- [[Concept B]]

### Subtopic B
- [[Concept C]]
```

Every concept gets its own atomic note - never write explanations inline. The module note only contains `[[WikiLinks]]` organized by subtopic.

### Phase 6: Summary

After everything is written, output a summary:

```
## Ingest Summary

**PDF(s):** filename(s)
**Module:** Module Name
**Lecture:** Vorlesung N - Topic

### Created Notes
- [[Note A]] → Notes/Subfolder/Note A.md
- [[Note B]] → Notes/Subfolder/Note B.md

### Updated Notes
- [[Existing Note]] - added section on X

### Added to Module Note
- Vorlesung N section with links to N atomic notes

### Skipped (already covered)
- Concept X - already in [[Existing Note]]
```

## Quality Checklist

Before finishing, verify:
- [ ] Every atomic note has complete YAML frontmatter (title, aliases, tags, description, draft)
- [ ] Every `[[WikiLink]]` target exists or was just created
- [ ] No orphan notes - every new note is linked from the module note
- [ ] Tags are lowercase and hyphen-separated
- [ ] LaTeX renders correctly (no broken `$` delimiters)
- [ ] Existing notes were appended to, not overwritten

## Efficiency Rules

- Batch all PDF reads first, then plan, then write - don't interleave reading and writing
- Use `find` to check for existing notes in a single command, not one-by-one
- Create multiple atomic notes in rapid succession - don't pause between them
- When appending to an existing note, read it once, plan the edit, apply it
