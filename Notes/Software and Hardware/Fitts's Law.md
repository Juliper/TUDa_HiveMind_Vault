---
title: Fitts's Law
aliases:
  - Fitts' Law
  - Fitts'sches Gesetz
tags:
  - hci
  - motor-performance
  - interaction-design
description: "A predictive model relating the time to acquire a target to its distance and size"
draft: false
---

Fitts's Law (Paul Fitts, 1954) is a predictive model of human motor performance that quantifies the time required to move to and select a target. It is one of the most validated and widely applied laws in HCI, used to evaluate pointing tasks, button sizing, and layout design.

## The Model

The movement time $MT$ to reach a target is:

$$MT = a + b \cdot \log_2\!\left(\frac{D}{W} + 1\right)$$

where:
- $D$ = distance from the starting point to the center of the target
- $W$ = width (size) of the target along the axis of movement
- $a$, $b$ = empirically determined constants (depend on device, user, context)
- $\log_2\!\left(\frac{D}{W} + 1\right)$ is the **Index of Difficulty** ($ID$), measured in bits

The **throughput** (Index of Performance) is $IP = \frac{ID}{MT}$, measured in bits/s.

## Key Implications for Design

1. **Larger targets are faster to hit** — make frequently used buttons bigger
2. **Closer targets are faster to reach** — place related actions near each other
3. **Screen edges and corners have effectively infinite width** — the cursor cannot overshoot, making edge-placed elements (taskbars, menus) very fast to reach
4. **Pie menus outperform linear menus** — all items are equidistant from the center, with large angular widths

## Example

A 10×10 px button that is 500 px away from the cursor has $ID = \log_2(500/10 + 1) \approx 5.67$ bits. Doubling the button to 20×20 px reduces the ID to $\log_2(500/20 + 1) \approx 4.7$ bits — a meaningful reduction in pointing time.

## Extension to 2D Targets

For a target in a 2D interface (not just a 1D strip), $D$ is measured as the distance to the **center** of the target, and $W$ is measured as the width of the target along a straight line in the direction of movement (not simply the target's on-screen width or height, and not its area). This means the effective width of a target can differ depending on the direction of approach, and for round targets $W$ corresponds to a diameter through the center.

## Model-Based Evaluation Context

Fitts's Law is one of the classic **model-based evaluation** techniques (alongside [[GOMS and Keystroke Level Model|GOMS and the Keystroke Level Model]]) that predicts user performance analytically, without running a study with real users. Measured throughput values for common devices illustrate how the model is used to compare input techniques:

| Input Technique | Throughput (bits/s) |
|---|---|
| FaceTouch (VR touch-on-face) | ~2.16 |
| Mouse | 3.7 - 4.9 |
| Touchscreen | ~6.95 |

## Limitations

- Fitts's Law is **only a model** - it neglects many real factors influencing pointing, such as tremor, mood, nervousness, and eyesight
- The constants $a$ and $b$ must be determined **empirically** for each device and context, not derived theoretically
- The result is a single predicted number, not direct feedback from real users - it complements but does not replace user testing
- Applies to **aimed movements** in 1D and 2D; less directly applicable to 3D or gesture input without extension
- Assumes a single, unambiguous target
- Does not account for cognitive decision time (see [[Hick's Law]] for that)

## Related Concepts

- [[Hick's Law]]: models the cognitive decision time *before* the motor action Fitts's Law describes
- [[Direct Manipulation]]: Fitts's Law governs the efficiency of pointing in direct manipulation interfaces
- [[Signal Detection Theory]]: both model human performance with tradeoffs (speed-accuracy for Fitts)
- [[GOMS and Keystroke Level Model]]: another model-based evaluation technique, often combined with Fitts's Law to predict pointing operator time within a task
- [[Heuristic Evaluation]]: a qualitative analytical evaluation method, contrasted with Fitts's Law's quantitative model-based approach
