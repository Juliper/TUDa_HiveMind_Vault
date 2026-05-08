---
title: Human Error in HCI
aliases:
  - Slips and Mistakes
  - Menschliche Fehler
tags:
  - hci
  - usability
  - error-handling
description: "Classification of human errors into slips (execution failures) and mistakes (planning failures) with design strategies to prevent them"
draft: false
---

Human error in HCI refers to user actions that lead to unintended outcomes. James Reason (1990) and Donald Norman (1983) established the foundational classification: errors are not random — they follow systematic patterns that can be anticipated and designed against.

## Error Classification

### Slips (Execution Errors)

The user has the **correct intention** but the **action goes wrong**. Slips occur during automatic, skilled behavior.

| Type | Description | Example |
|---|---|---|
| **Capture error** | A frequent action "captures" the intended one | Driving to work on a day off because the route is habitual |
| **Description error** | Correct action on the wrong object | Pouring coffee into the sugar bowl instead of the cup |
| **Data-driven error** | External data intrudes into the action | Typing a word you just heard instead of the word you meant |
| **Mode error** | Correct action in the wrong system mode | Typing text when an application is in command mode (e.g., Vim) |

### Mistakes (Planning Errors)

The user's **plan itself is wrong** — the intention doesn't match the goal. Mistakes stem from incorrect [[Mental Models]] or incomplete knowledge.

| Type | Description | Example |
|---|---|---|
| **Rule-based mistake** | Applying the wrong rule to a recognized situation | Using Ctrl+Z to undo in a terminal that interprets it as SIGTSTP |
| **Knowledge-based mistake** | Incorrect reasoning when facing an unfamiliar situation | Assuming "deleting a shortcut" deletes the original file |

## Reason's Swiss Cheese Model

Errors propagate through systems when multiple protective layers have aligned gaps — like holes in slices of Swiss cheese lining up. Good design adds multiple independent barriers:

1. **Prevention** — make errors impossible (constraints, graying out invalid options)
2. **Detection** — make errors visible (validation, confirmation dialogs)
3. **Recovery** — make errors reversible (undo, trash instead of permanent delete)

## Design Strategies

**Preventing slips:**
- Use constraints to prevent invalid inputs (date pickers instead of free text)
- Require confirmation for destructive actions ("Are you sure you want to delete?")
- Provide clear mode indicators when system modes exist
- Design distinct actions to look and feel different

**Preventing mistakes:**
- Provide clear system feedback so users can verify their [[Mental Models]]
- Use familiar conventions and metaphors
- Offer preview/simulation before committing ("This will affect 47 files")
- Write meaningful error messages that explain *what went wrong* and *how to fix it*

## Example

A "Send" button placed directly next to "Delete" in an email client invites capture errors (slips). Moving them apart, making "Delete" red and requiring confirmation are design interventions. A user who replies-all thinking only the sender will see the message commits a mistake — a mental model error about how reply-all works.

## Related Concepts

- [[Mental Models]]: incorrect mental models are the root cause of mistakes
- [[Gulf of Execution and Evaluation]]: wide gulfs increase both slips and mistakes
- [[Signal Detection Theory]]: misses and false alarms are specific error types in detection tasks
- [[Cognitive Load Theory]]: high cognitive load increases error rates
