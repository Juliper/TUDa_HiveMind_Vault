---
title: Mapping and Analogy in HCI
aliases:
  - Interface Mappings
  - Naturally Mapping
tags:
  - hci
  - interaction-design
description: "The relationship between controls and their effects, and how well that relationship matches user expectations"
draft: false
---

> [!NOTE] Definition
> A mapping is the relationship between a control and its effect on a system. A "natural" mapping exploits spatial, physical, cultural, or perceptual analogies so that the relationship is understood immediately, without instructions.

## Types of Mapping

| Type | Basis | Example |
|---|---|---|
| **Spatial** | Physical arrangement matches expected effect | Stove knobs arranged in the same layout as the burners they control |
| **Physical** | The control's motion resembles the effect | Turning a steering wheel right to turn the car right |
| **Cultural** | Shared convention, not inherent logic | Turning a knob clockwise to increase volume |
| **Perceptual** | Sensory cues suggest the relationship | A larger, heavier-feeling slider suggests a larger range of effect |

## Why Natural Mappings Matter

Good mappings reduce reliance on labels, memorization, or trial and error - they let users predict outcomes instantly by analogy to real-world experience. Poor mappings force users to memorize arbitrary control-effect relationships, increasing [[Cognitive Load Theory|cognitive load]] and error rates.

## Example

A classic bad mapping: four identical stove knobs arranged in a single row controlling four burners arranged in a square. Users cannot predict which knob controls which burner without labels, because there is no spatial correspondence between the layout of controls and the layout of effects. Rearranging the knobs to mirror the burner layout fixes the mapping without adding any new labels.

> [!IMPORTANT]
> Mapping is closely related to but distinct from a [[Metaphors in HCI|metaphor]]: a metaphor borrows an entire familiar concept, while a mapping is specifically about the geometric or perceptual correspondence between a control and its effect.

## Related Concepts

- [[Affordances]]: affordances suggest an action is possible; mapping determines whether its effect is predictable
- [[Constraints in HCI]]: logical constraints often rely on natural mappings to be interpretable
- [[Gulf of Execution and Evaluation]]: poor mappings widen the Gulf of Execution by making the correct action unclear
