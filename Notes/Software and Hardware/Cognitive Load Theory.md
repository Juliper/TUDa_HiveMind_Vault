---
title: Cognitive Load Theory
aliases:
  - CLT
  - Kognitive Belastungstheorie
tags:
  - hci
  - cognition
  - usability
description: "A framework describing the three types of mental effort imposed on working memory during information processing"
draft: false
---

Cognitive Load Theory (John Sweller, 1988) describes the mental effort imposed on working memory during learning and task performance. Since working memory has severe capacity limits (~4±1 chunks, per Cowan, 2001), managing cognitive load is essential for usable interface design.

## Three Types of Cognitive Load

| Type | Source | Controllable? |
|---|---|---|
| **Intrinsic** | Inherent complexity of the task itself (element interactivity) | No — determined by task and user expertise |
| **Extraneous** | Poor design, irrelevant information, unnecessary steps | Yes — the primary target for optimization |
| **Germane** | Effort spent building mental schemas and understanding | Yes — should be maximized |

The goal in HCI design: **minimize extraneous load** so that limited working memory capacity can be devoted to intrinsic and germane processing.

## Working Memory Constraints

- **Capacity:** ~4 chunks (fewer for novel/complex items)
- **Duration:** Information decays from working memory within ~20 seconds without rehearsal
- **Modality:** Visual and auditory channels are partially independent (Baddeley's model) — multimodal presentation can increase effective capacity

## Design Strategies to Reduce Extraneous Load

1. **Eliminate redundancy** — don't present the same information in text and narration simultaneously (redundancy effect)
2. **Spatial contiguity** — place related information close together (e.g., labels next to their fields, not in a separate legend)
3. **Temporal contiguity** — present related information simultaneously rather than sequentially
4. **Segmenting** — break complex tasks into manageable steps (wizards, progressive disclosure)
5. **Signaling** — highlight essential information to guide attention (bold, color, callouts)

## Example

A poorly designed form that shows all 30 fields at once with instructions in a separate sidebar imposes high extraneous load. Redesigning it as a multi-step wizard with 5 fields per step, inline validation, and contextual help text reduces extraneous load while preserving the intrinsic complexity of the task.

## Related Concepts

- [[Mental Models]]: germane load is the effort of building and refining mental models
- [[Hick's Law]]: more choices increase cognitive load during decision-making
- [[Gestalt Principles]]: good visual grouping reduces the extraneous load of parsing a layout
- [[Gulf of Execution and Evaluation]]: high extraneous load widens both gulfs
