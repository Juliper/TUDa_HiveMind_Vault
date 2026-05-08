---
title: Mental Models
aliases:
  - Mentale Modelle
tags:
  - hci
  - cognition
  - usability
description: "Internal representations users build of how a system works, guiding their expectations and actions"
draft: false
---

A mental model is a user's internal representation of how a system works. Users don't understand the actual implementation — they construct a simplified, often incomplete model based on experience, analogy, and interface cues. The quality of this model determines how effectively they can predict system behavior and recover from errors.

## Three Models (Norman's Framework)

Donald Norman (1988) distinguished three related models:

1. **Design Model** — the conceptual model the designer intended to convey
2. **User's Model (Mental Model)** — the model the user actually constructs
3. **System Image** — what the system actually presents (interface, documentation, feedback)

The designer communicates the design model through the system image. If the system image is unclear or inconsistent, the user's mental model will diverge from the intended design model, leading to confusion and errors.

## How Mental Models Form

- **Exploration** — trial and error with the interface
- **Analogy** — mapping from familiar systems ("this works like email")
- **Instruction** — tutorials, tooltips, onboarding flows
- **Observation** — watching others use the system

Mental models are:
- **Incomplete** — users don't model every feature
- **Unstable** — they evolve and can regress without use
- **Unscientific** — may include "superstitious" beliefs about causation
- **Parsimonious** — users prefer simpler models even if less accurate

## Design Implications

1. **Match existing mental models** — leverage familiar patterns and metaphors (e.g., shopping cart, folder hierarchy)
2. **Provide clear feedback** — every action should produce visible results that reinforce the correct model
3. **Use progressive disclosure** — reveal complexity gradually to avoid overwhelming the initial model
4. **Offer affordances** — visual cues that suggest how an element can be used (buttons look pressable, sliders look draggable)
5. **Consistent behavior** — identical elements should always work the same way

## Example

Users expect the "back" button in a browser to return to the previous page. A web application that uses client-side routing but doesn't update browser history breaks this mental model — pressing back might exit the application entirely instead of going to the previous view.

## Related Concepts

- [[Gulf of Execution and Evaluation]]: mental model mismatches widen both gulfs
- [[Cognitive Load Theory]]: building a mental model consumes germane cognitive load
- [[Direct Manipulation]]: effective because it aligns the interface with spatial/physical mental models
- [[Human Error in HCI]]: mental model mismatches are a primary cause of mistakes
