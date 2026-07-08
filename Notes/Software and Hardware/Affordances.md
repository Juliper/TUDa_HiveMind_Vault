---
title: Affordances
aliases:
  - Affordanzen
tags:
  - hci
  - interaction-design
description: "Perceived properties of an object that suggest how it can be used"
draft: false
---

> [!NOTE] Definition
> An affordance is a property of an object or environment that suggests how it can be used. James Gibson (1977) originally defined affordances as objective, actor-relative possibilities for action; Donald Norman (1988) adapted the term for design to mean the perceived, communicated possibilities for action.

## Gibson vs. Norman

| | Gibson's Affordance | Norman's (Perceived) Affordance |
|---|---|---|
| **Nature** | An actual, objective relationship between an object and an actor's capabilities | What the user perceives as possible, whether or not it truly is |
| **Existence** | Exists independent of whether it is perceived | Exists only in the user's perception |
| **Design relevance** | Explains what actions are physically possible | Explains what actions the user believes are possible - the design target |

In interface design, Norman's sense is the practical one: a button should be *perceived* as clickable, regardless of the underlying technical possibility.

## Signifiers

Norman later introduced **signifiers** as a refinement: explicit signals (labels, icons, shadows, borders) that communicate where an action is possible, since digital interfaces often lack the physical cues that make real-world affordances legible.

## Example

A raised, shadowed rectangle with text inside is perceived as a clickable button because its visual styling signals "this can be pressed," even though nothing about pixels on a screen inherently affords pressing - the affordance is entirely communicated through visual signifiers.

> [!IMPORTANT]
> A flat interface element with no visual signifier (a "ghost button") may still be clickable, but if it does not look clickable, it has no *perceived* affordance - users will not discover it.

## Related Concepts

- [[Constraints in HCI]]: constraints limit which affordances are available at a given time
- [[Metaphors in HCI]]: metaphors and affordances jointly communicate how to interact with an object
- [[Mental Models]]: affordances are one of the cues users use to build their mental model
- [[Direct Manipulation]]: relies heavily on strong, visible affordances for on-screen objects
