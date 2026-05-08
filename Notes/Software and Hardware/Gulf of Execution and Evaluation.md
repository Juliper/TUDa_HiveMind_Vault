---
title: Gulf of Execution and Evaluation
aliases:
  - Norman's Gulfs
  - Ausführungs- und Bewertungskluft
tags:
  - hci
  - usability
  - interaction-design
description: "Norman's framework describing the two gaps users must bridge when interacting with a system"
draft: false
---

The Gulf of Execution and Gulf of Evaluation are two conceptual gaps introduced by Donald Norman (1986) that describe the cognitive distance users must bridge when interacting with any system. Minimizing both gulfs is a central goal of usable interface design.

## The Two Gulfs

### Gulf of Execution

The gap between the user's **intention** (what they want to do) and the **actions** required by the system to achieve it.

- **Wide gulf:** the user knows what they want but can't figure out how to do it (e.g., complex command syntax, hidden features)
- **Narrow gulf:** the available actions clearly map to the user's goals (e.g., a visible "Delete" button for removing an item)

### Gulf of Evaluation

The gap between the **system's state** (what happened) and the user's **interpretation** of that state.

- **Wide gulf:** the user performed an action but can't tell if it worked (e.g., no confirmation, ambiguous feedback)
- **Narrow gulf:** the system clearly communicates its new state (e.g., success message, visual change, undo option)

## Norman's Seven Stages of Action

The gulfs map onto Norman's cyclical model of interaction:

1. **Goal** — form the goal
2. **Plan** — determine what actions to take *(Gulf of Execution)*
3. **Specify** — translate plan into specific interface actions
4. **Perform** — execute the actions
5. **Perceive** — observe the system's response *(Gulf of Evaluation)*
6. **Interpret** — make sense of what happened
7. **Compare** — evaluate whether the goal was achieved

## Design Strategies

**To narrow the Gulf of Execution:**
- Use familiar interaction patterns and metaphors
- Provide clear affordances and signifiers
- Reduce the number of steps to complete common tasks
- Offer multiple paths to the same goal (menu, shortcut, search)

**To narrow the Gulf of Evaluation:**
- Give immediate, visible feedback for every action
- Use clear status indicators (progress bars, state labels)
- Provide meaningful error messages that suggest corrective action
- Make system state visible at all times

## Example

Sending an email: a well-designed mail client narrows the Gulf of Execution with a prominent "Compose" button and narrows the Gulf of Evaluation with a "Message sent" confirmation and the email appearing in the Sent folder.

## Related Concepts

- [[Mental Models]]: mismatched mental models widen both gulfs
- [[Direct Manipulation]]: narrows both gulfs by making objects and actions visible
- [[Cognitive Load Theory]]: wide gulfs increase extraneous cognitive load
- [[Human Error in HCI]]: wide gulfs are a primary source of user errors
