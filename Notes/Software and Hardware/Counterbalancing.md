---
title: Counterbalancing
aliases:
  - Balanced Latin Square
  - Gegenausgleich
tags:
  - hci
  - evaluation
  - research-methods
description: "A technique for varying the order of conditions across participants in a within-subject design to cancel out learning and carry-over effects"
draft: false
---

> [!NOTE] Definition
> Counterbalancing is the practice of systematically varying the order in which experimental conditions are presented to different participants, so that any effect of order (learning, fatigue, carry-over) is distributed evenly across all conditions rather than biasing one of them.

## Why It Is Needed

In a [[Between-Subjects and Within-Subjects Design|within-subject design]], every participant sees every condition. Without counterbalancing, presenting conditions in the same fixed order to everyone would confound the condition itself with its position in the sequence (e.g., the last condition might look best purely because participants had practiced by then).

## Balanced Latin Square

A common counterbalancing method that arranges conditions into an $n \times n$ grid such that each condition appears exactly once in each position (first, second, third, ...) across the set of participants, and each condition is immediately preceded by every other condition an equal number of times.

**Example** with conditions A, B, C, D, a balanced Latin square assigns different participants the orders:

| Participant | Order |
|---|---|
| 1 | A, B, D, C |
| 2 | B, C, A, D |
| 3 | C, D, B, A |
| 4 | D, A, C, B |

## Related Concepts

- [[Between-Subjects and Within-Subjects Design]]: counterbalancing is specifically a within-subject design technique
- [[Controlled Experiment]]: part of overall study design planning
- [[Validity and Reliability]]: proper counterbalancing protects internal validity against order-related confounds
