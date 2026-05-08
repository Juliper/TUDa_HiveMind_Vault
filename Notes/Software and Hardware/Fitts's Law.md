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

## Limitations

- Applies to **aimed movements** in 1D and 2D; less directly applicable to 3D or gesture input
- Assumes a single, unambiguous target — not directly applicable to dense target arrays without extensions
- Does not account for cognitive decision time (see [[Hick's Law]] for that)

## Related Concepts

- [[Hick's Law]]: models the cognitive decision time *before* the motor action Fitts's Law describes
- [[Direct Manipulation]]: Fitts's Law governs the efficiency of pointing in direct manipulation interfaces
- [[Signal Detection Theory]]: both model human performance with tradeoffs (speed-accuracy for Fitts)
