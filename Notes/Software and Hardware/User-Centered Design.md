---
title: User-Centered Design
aliases:
  - UCD
  - Interaktionsdesignprozess
tags:
  - visual-computing
  - user-interfaces
description: "Design methodology prioritizing early user focus, continuous evaluation, and iterative refinement"
draft: false
---

> [!NOTE] Definition
> User-Centered Design (UCD) is a design methodology that places the user at the center of the development process, emphasizing learnability and usability through iterative refinement.

## Core Principles

1. **Early focus on the user** from the start of the design process
2. **Continuous evaluation** of learnability and usability
3. **Iterative design** - repeated cycles of design, test, refine

## Interaction Modalities

| Modality | Description |
|----------|-------------|
| Command line | Fast and powerful |
| Menus | Simple, sequential, hierarchical |
| Forms | Structured data input |
| Q&A | Guided interaction |
| Direct manipulation | WYSIWYG interaction with objects |
| 3D environments | Spatial interaction |
| Natural language | Speech-based interaction |
| Gestures | Physical movement-based input |

## 2D Input for 3D Objects

Using 2D input devices for 3D manipulation introduces ambiguity - a single cursor position maps to infinitely many 3D positions. Manipulators (handles/gizmos) solve this by constraining interaction to specific axes.

## User-Centered vs. Human-Centered Design

The terms are related but not identical. ISO 9241 defines **User-Centered Design (UCD)** as an iterative process focused on the *users* and their needs at each phase, while **Human-Centered Design (HCD)** is framed more broadly as making systems usable and useful by focusing on users, their needs and requirements, and applying human factors/ergonomics knowledge.

> [!NOTE]
> The word "user" can strip away the emotional, human side of the people involved. Human-Centered Design deliberately broadens scope to consider *every* human touched by the process - not just the end user, but also those who maintain, sell, or otherwise interact with the system. See [[Human-Centered Design Process]] for the full ISO 9241-210 cycle.

## Related Concepts

- [[Human-Machine Interface]]: the perception-cognition-reaction framework underlying UCD
- [[Human-Centered Design Process]]: the broader ISO 9241-210 process UCD is closely related to
- [[Visual Attention]]: designing for human attention constraints
- [[Uncanny Valley]]: emotional response considerations in design
