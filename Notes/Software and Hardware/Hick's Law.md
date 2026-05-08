---
title: Hick's Law
aliases:
  - Hick-Hyman Law
  - Hick'sches Gesetz
tags:
  - hci
  - decision-making
  - interaction-design
description: "A law stating that decision time increases logarithmically with the number of choices"
draft: false
---

Hick's Law (William Hick, 1952; Ray Hyman, 1953) states that the time it takes a person to make a decision increases logarithmically with the number of available choices. In HCI, it is used to predict how long users take to select an option from a set — menus, toolbars, settings panels, etc.

## The Model

$$RT = a + b \cdot \log_2(n + 1)$$

where:
- $RT$ = reaction (decision) time
- $n$ = number of equally probable alternatives
- $a$ = base reaction time (independent of choices)
- $b$ = empirically determined constant (processing time per bit of information)
- The $+1$ accounts for the option of "no response" / uncertainty

For non-equiprobable choices, the general form uses information entropy:

$$RT = a + b \cdot H \quad \text{where} \quad H = -\sum_{i=1}^{n} p_i \log_2 p_i$$

## Key Implications for Design

1. **Reduce the number of options per step** — 8 items in a flat menu are slower to decide from than 2 levels of 3 items each (but navigation cost must be balanced)
2. **Highlight probable choices** — if some options are far more likely, visually distinguish them to reduce effective entropy
3. **Progressive disclosure** — show basic options first, reveal advanced ones on demand
4. **Search as an alternative** — for very large option sets (100+), a search field bypasses Hick's Law entirely

## Example

A dropdown menu with 4 options: $RT = a + b \cdot \log_2(5) \approx a + 2.3b$. Expanding to 16 options: $RT = a + b \cdot \log_2(17) \approx a + 4.1b$. Quadrupling choices less than doubles decision time — but the increase is still noticeable.

## Limitations

- Assumes choices are **known and visible** — doesn't apply when users must search or recall options
- Works best for **simple, practiced choices** — complex decisions involve cognitive processes beyond simple selection
- Does not account for **motor time** to execute the choice (see [[Fitts's Law]])

## Related Concepts

- [[Fitts's Law]]: models the motor execution time *after* the decision Hick's Law describes
- [[Cognitive Load Theory]]: too many choices increase cognitive load beyond just decision time
- [[Mental Models]]: familiar categorization of options can reduce effective choice complexity
