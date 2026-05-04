---
title: Normalformen
aliases:
  - Normal Forms
  - DNF
  - KNF
  - Disjunktive Normalform
  - Konjunktive Normalform
  - Minterms
  - Maxterms
  - Canonical Form
tags:
  - digitaltechnik
  - logic
description: "The two canonical representations of Boolean functions — DNF (sum of minterms) and KNF (product of maxterms) — used as a systematic starting point for logic minimization."
---

**Normalformen** are standardized representations of Boolean functions. Every Boolean function can be expressed in exactly one **DNF** and one **KNF** (up to ordering). They serve as the canonical starting point before minimization with [[Karnaugh-Veitch-Diagramme]].

## Minterm und Maxterm

For a function of $n$ variables, each input combination $i$ (0 to $2^n - 1$) defines:

| | Minterm $m_i$ | Maxterm $M_i$ |
|---|---|---|
| **Form** | AND of all variables (non-inverted if bit = 1, inverted if bit = 0) | OR of all variables (non-inverted if bit = 0, inverted if bit = 1) |
| **Value** | 1 for exactly one input combination | 0 for exactly one input combination |
| **Used when** | Function output is **1** | Function output is **0** |

**Example** for $n = 2$ variables $A, B$:

| $i$ | $A$ | $B$ | Minterm $m_i$ | Maxterm $M_i$ |
|---|---|---|---|---|
| 0 | 0 | 0 | $\overline{A} \cdot \overline{B}$ | $A + B$ |
| 1 | 0 | 1 | $\overline{A} \cdot B$ | $A + \overline{B}$ |
| 2 | 1 | 0 | $A \cdot \overline{B}$ | $\overline{A} + B$ |
| 3 | 1 | 1 | $A \cdot B$ | $\overline{A} + \overline{B}$ |

## Disjunktive Normalform (DNF)

The DNF is a **sum (OR) of minterms** — one minterm for each row where the function output is **1**:

$$F_{DNF} = \sum m_i \quad \text{for all } i \text{ where } F(i) = 1$$

The DNF is read directly from the **1-rows** of the truth table.

**Example**: $F(A,B,C)$ is 1 for inputs $\{1, 3, 5, 7\}$:
$$F = m_1 + m_3 + m_5 + m_7 = \overline{A}\,\overline{B}\,C + \overline{A}\,B\,C + A\,\overline{B}\,C + A\,B\,C$$

> [!NOTE]
> This simplifies to $F = C$ — but the DNF captures all the information before minimization.

## Konjunktive Normalform (KNF)

The KNF is a **product (AND) of maxterms** — one maxterm for each row where the function output is **0**:

$$F_{KNF} = \prod M_i \quad \text{for all } i \text{ where } F(i) = 0$$

The KNF is read from the **0-rows** of the truth table.

## DNF ↔ KNF Zusammenhang

$$F_{DNF} \text{ uses minterms of } F=1 \qquad F_{KNF} \text{ uses maxterms of } F=0$$

The missing indices in one form are exactly the indices used in the other:
$$F = \sum m(1,3,5,7) \equiv F = \prod M(0,2,4,6)$$

## Von der Wahrheitstabelle zur Normalform

1. Write out the truth table for all $2^n$ input combinations
2. For **DNF**: collect all rows where $F = 1$, write their minterms, OR them together
3. For **KNF**: collect all rows where $F = 0$, write their maxterms, AND them together
4. Minimize using [[Boolesche Algebra|Boolean algebra]] or [[Karnaugh-Veitch-Diagramme]]

## Related Concepts

- [[Boolesche Algebra]]: the algebraic laws used to simplify normalized expressions
- [[Karnaugh-Veitch-Diagramme]]: graphical minimization directly from DNF/KNF
