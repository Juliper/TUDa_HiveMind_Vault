---
title: GOMS and Keystroke Level Model
aliases:
  - GOMS
  - KLM
  - Keystroke Level Model
tags:
  - hci
  - evaluation
description: "Model-based evaluation techniques that predict expert, error-free task execution time without needing real users"
draft: false
---

> [!NOTE] Definition
> GOMS (Goals, Operators, Methods, Selection rules) is a model of the knowledge a user needs to execute a task; the Keystroke Level Model (KLM) is a quantitative extension of GOMS that predicts how long an expert user takes to perform a task, both without requiring any user testing.

## GOMS

Introduced by Card, Moran, and Newell in *The Psychology of Human-Computer Interaction* (1983). GOMS decomposes a task into:

| Component | Meaning |
|---|---|
| **Goals** | What the user wants to accomplish |
| **Operators** | The elementary actions available (keystrokes, mouse moves, mental steps) |
| **Methods** | Sequences of operators that achieve a goal |
| **Selection rules** | Rules for choosing between multiple methods when more than one is applicable |

GOMS lets an evaluator test an interface **without users**, even before the system is built, by reasoning through the operator sequence required for a task. It works well for routine, well-learned tasks but is less suitable for creative or open-ended problem-solving tasks.

## Keystroke Level Model (KLM)

An extension of GOMS focused purely on quantitative predictions of **execution time** for an expert user performing a task, by summing the time of each elementary operator (keystroke, pointing, homing between devices, mental preparation, system response time).

## Related Concepts

- [[Fitts's Law]]: another model-based technique, used specifically to predict the time of pointing operators within a KLM analysis
- [[Heuristic Evaluation]]: a complementary analytical evaluation method that does not require users either, but relies on expert judgment against usability principles rather than a formal execution-time model
