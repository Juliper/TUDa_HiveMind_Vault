---
title: Karnaugh-Veitch-Diagramme
aliases:
  - KV-Diagramm
  - Karnaugh Map
  - KV Map
  - KV-Karte
tags:
  - digitaltechnik
  - logic
description: "A graphical method for minimizing Boolean functions by identifying adjacent minterms that can be grouped and simplified."
---

**Karnaugh-Veitch-Diagramme** (KV maps / Karnaugh maps) provide a systematic, visual method for minimizing Boolean functions. They exploit the fact that geometrically adjacent cells differ in exactly one variable — making simplification intuitive.

## Aufbau (Structure)

A KV map is a 2D grid where:
- Each cell corresponds to one **minterm** (one row of the truth table)
- Adjacent cells differ in **exactly one variable** (Gray code ordering)
- The map **wraps around**: top↔bottom and left↔right edges are adjacent

### 2-Variable KV Map ($n=2$)

$$\begin{array}{c|cc}
 & B=0 & B=1 \\ \hline
A=0 & m_0 & m_1 \\
A=1 & m_2 & m_3
\end{array}$$

### 3-Variable KV Map ($n=3$)

$$\begin{array}{c|cccc}
 & \overline{B}\overline{C} & \overline{B}C & BC & B\overline{C} \\ \hline
A=0 & m_0 & m_1 & m_3 & m_2 \\
A=1 & m_4 & m_5 & m_7 & m_6
\end{array}$$

> [!NOTE]
> The column order follows **Gray code** (00, 01, 11, 10) to ensure adjacency. This is the most common source of errors — do not use binary order (00, 01, 10, 11).

### 4-Variable KV Map ($n=4$)

Rows use Gray code for $AB$, columns for $CD$ — gives a 4×4 grid of 16 cells.

## Minimierungsregeln (Grouping Rules)

1. **Mark all cells** where $F = 1$ (ones in the truth table)
2. **Group** ones into rectangles of size $2^k$ ($1, 2, 4, 8, 16, \ldots$) — only powers of two
3. **Maximize group size**: larger groups eliminate more variables
4. **Every 1 must be covered** by at least one group; groups may overlap
5. **No zeros** may be included in a group
6. **Wrap-around is allowed**: the map is a torus — top/bottom and left/right wrap

### Reading a Group

A group of size $2^k$ eliminates $k$ variables — the $k$ variables that change within the group are eliminated; the remaining variables form the product term.

**Example** (3-variable): Group $\{m_1, m_3, m_5, m_7\}$ — $C=1$ in all, $A$ and $B$ vary → simplifies to $C$.

## Don't-Care-Zustände

Certain input combinations may be:
- **Physically impossible** (e.g. BCD codes 10–15)
- **Irrelevant** (output doesn't matter)

These **don't cares** are marked as `X` in the truth table and map. They can be treated as either 0 or 1, whichever allows a larger group — but they do **not** need to be covered.

## Minimierungsablauf

1. Derive the [[Normalformen|DNF]] from the truth table (mark the 1-cells)
2. Enter values into the KV map
3. Identify largest possible groups (cover all 1s, use don't cares opportunistically)
4. Read off one product term per group
5. OR all product terms → minimized expression

## Vor- und Nachteile

| | KV Map | Boolean Algebra |
|---|---|---|
| **Best for** | Up to 4–6 variables | Algebraic manipulation / proof |
| **Scales to** | ~6 variables (5×5 hard to visualize) | Arbitrary |
| **Method** | Visual, systematic | Equation-based, requires insight |

## Related Concepts

- [[Normalformen]]: DNF/KNF are the starting point for KV minimization
- [[Boolesche Algebra]]: algebraic alternative and verification method
