---
title: Direct Manipulation
aliases:
  - Direkte Manipulation
tags:
  - hci
  - interaction-paradigm
description: "An interaction style where users act on visible objects through physical actions rather than typed commands"
draft: false
---

Direct Manipulation is an interaction paradigm introduced by Ben Shneiderman (1983) in which users interact with on-screen objects using physical actions (clicking, dragging, resizing) rather than issuing textual commands. It is one of the foundational principles behind modern graphical user interfaces.

## Core Properties

Shneiderman defined three key properties of direct manipulation interfaces:

1. **Continuous representation** of the objects of interest — users always see what they're working with
2. **Physical actions or labeled button presses** instead of complex syntax — dragging a file icon to a trash can rather than typing `rm filename`
3. **Rapid, incremental, reversible operations** — actions have immediate visible effects and can be undone

## Why It Works

Direct manipulation leverages human spatial and motor skills rather than requiring memorization of command syntax. This leads to:

- **Faster learning** — novices can explore by trial and error
- **Lower error rates** — visible state makes mistakes obvious
- **Higher user satisfaction** — feeling of control and engagement
- **Easier error recovery** — undo is natural when actions are visible

## Example

Dragging a file from one folder to another on a desktop OS is direct manipulation: the file is continuously visible, the user physically moves it, and the result is immediately apparent. Compare this with the command-line equivalent `mv ~/Documents/report.pdf ~/Desktop/` — same operation, but requires knowing syntax and paths.

## Limitations

- **Repetitive tasks** are tedious — dragging 500 files one by one is far slower than a batch command
- **Not all operations map well** to physical metaphors (e.g., changing file permissions)
- **Accessibility** challenges for users who cannot perform fine motor actions

## Related Concepts

- [[WIMP Paradigm]]: the dominant interface model built on direct manipulation principles
- [[Gulf of Execution and Evaluation]]: direct manipulation narrows both gulfs
- [[Fitts's Law]]: predicts the time cost of pointing at on-screen targets in direct manipulation interfaces
