---
title: Kombinatorische Logik
aliases:
  - Schaltnetz
  - Combinational Logic
  - Schaltwerk
  - Sequential Logic
tags:
  - digitaltechnik
  - logic
description: "Circuits classified as Schaltnetz (combinational, acyclic) or Schaltwerk (sequential, with memory); Boolean equations, Volladdierer, and key terminology."
---

A digital circuit is described by its **inputs**, **outputs**, and the **functional/timing relationship** between them. Circuits fall into two fundamental classes based on whether they have memory.

## Schaltungsarten

### Schaltnetz (Combinational Circuit)

A **Schaltnetz** is a circuit whose output depends **only on the current inputs** — no memory.

Properties:
- **Acyclic**: no feedback loops; can be drawn as a directed acyclic graph (DAG)
- Outputs are a pure function of inputs: $Y = f(X_1, X_2, \ldots, X_n)$
- Described completely by a truth table or Boolean expression

### Schaltwerk (Sequential Circuit)

A **Schaltwerk** has **memory**: output depends on current inputs **and past history**.

Properties:
- Contains **feedback loops** (cycles in the circuit graph)
- Stores state in flip-flops or latches
- Requires state diagrams or state tables for full description

> [!NOTE]
> The acyclicity rule is the key distinguishing criterion: a circuit with any feedback path is a Schaltwerk, not a Schaltnetz.

## Grundbegriffe (Terminology)

| Term | Definition |
|---|---|
| **Literal** | A variable or its complement: $A$, $\overline{A}$ |
| **Implikant** | A product term (AND of literals) that is 1 only when the function is 1 |
| **Primimplikant** | An implicant that cannot be combined with another to eliminate a variable |
| **Minterm** | A product term in which every variable appears exactly once |
| **Maxterm** | A sum term in which every variable appears exactly once |
| **Komplement** | The logical inverse of a function or variable |

## Operatorrangfolge (Precedence)

When evaluating Boolean expressions without parentheses:

$$\text{NOT} > \text{AND} > \text{XOR} > \text{OR}$$

Example: $A + B \cdot \overline{C}$ means $A + (B \cdot (\overline{C}))$

## Schaltungsdarstellung

A combinational circuit maps inputs to outputs via Boolean equations. Each output is a separate Boolean function of the inputs. Two representation levels:

1. **Abstract**: Boolean equation $Y = f(A, B, C, \ldots)$
2. **Schematic**: gate-level diagram with wire connections

**Verbindungsknoten** (junction nodes) are points where wires connect — signals at a node have the same value. **Schaltungselemente** (gates) transform signals.

## Volladdierer (Full Adder)

A **Volladdierer** adds three single-bit inputs (A, B, carry-in $C_{in}$) and produces a sum bit S and carry-out $C_{out}$:

$$S = A \oplus B \oplus C_{in}$$
$$C_{out} = A \cdot B + A \cdot C_{in} + B \cdot C_{in}$$

| $A$ | $B$ | $C_{in}$ | $S$ | $C_{out}$ |
|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 1 | 0 |
| 0 | 1 | 0 | 1 | 0 |
| 0 | 1 | 1 | 0 | 1 |
| 1 | 0 | 0 | 1 | 0 |
| 1 | 0 | 1 | 0 | 1 |
| 1 | 1 | 0 | 0 | 1 |
| 1 | 1 | 1 | 1 | 1 |

$C_{out} = 1$ whenever at least two of the three inputs are 1.

Multiple full adders chained together form a **Ripple-Carry-Addierer** for multi-bit addition.

## Related Concepts

- [[Boolesche Algebra]]: the algebraic laws governing Boolean equations
- [[Normalformen]]: DNF/KNF as systematic representations of combinational functions
- [[Karnaugh-Veitch-Diagramme]]: minimization of combinational functions
- [[Logikgatter]]: physical gate implementations of Boolean operators
- [[Zeitverhalten]]: propagation delays in combinational circuits
