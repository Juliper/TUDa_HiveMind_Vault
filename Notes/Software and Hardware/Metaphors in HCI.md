---
title: Metaphors in HCI
aliases:
  - Interface Metaphors
  - Metaphern im Interfacedesign
tags:
  - hci
  - interaction-design
description: "Design technique that maps a new, unfamiliar system onto a familiar concept to help users predict its behavior"
draft: false
---

> [!NOTE] Definition
> An interface metaphor maps the structure and behavior of an unfamiliar computer system onto a familiar, real-world concept, letting users apply existing knowledge to predict how the system works.

## Models Involved in a Metaphor

Design relies on the relationship between three models, closely related to the models described in [[Mental Models]]:

| Model | Description |
|---|---|
| **Conceptual model** | The designer's intended structure and behavior of the system |
| **Mental model** | The user's actual internal understanding, partly built from the metaphor |
| **Presented / implemented model** | What the interface literally shows and how it actually behaves |

A metaphor succeeds when the presented model reliably evokes a mental model that matches the conceptual model - for example, the "desktop" metaphor evokes files, folders, and a trash can that behave analogously to their physical counterparts.

## Properties of a Good Metaphor

- **Transparency** - the metaphor should make the system's operation obvious rather than requiring extra explanation
- **Flexibility / Accelerators** - the metaphor should not trap expert users in slow, literal interactions; it should allow shortcuts once the user is experienced (e.g., keyboard shortcuts alongside drag-and-drop)
- **Scope** - the metaphor should cover enough of the system's functionality to be useful, without being stretched into situations where it misleads

## Where Metaphors Break Down

A metaphor is never a perfect match - it should highlight useful similarities while the user learns to ignore irrelevant differences. Problems occur when:

- The metaphor implies a capability the system doesn't have (e.g., a "trash can" implying permanent, private disposal when files are actually recoverable or shared)
- The metaphor becomes an accelerator bottleneck - forcing all interaction through a literal, slow physical analogy

> [!IMPORTANT]
> A metaphor is a communication tool between the conceptual model and the user's mental model - it is not the system itself, and overly literal metaphors can limit interface efficiency for experienced users.

## Example

The "shopping cart" metaphor in e-commerce lets users understand adding, removing, and reviewing items before "checkout" without needing to learn a new transactional vocabulary - it borrows an entire familiar script from physical retail.

## Related Concepts

- [[Mental Models]]: the internal representation a metaphor is meant to shape
- [[Affordances]]: metaphors work together with affordances to signal how to interact with an object
- [[WIMP Paradigm]]: the desktop metaphor underlying the dominant GUI paradigm
