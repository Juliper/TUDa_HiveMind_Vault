---
title: Sets and Functions in MOSES
aliases:
  - Mengen und Funktionen
tags:
  - formal-methods
  - moses
description: "Set definitions, tuple constructions, disjoint union, and function notation used in formal modeling"
draft: false
---

> [!NOTE] Definition
> Formal modeling relies on precise set and function notation. Sets can be defined extensionally, intensionally, or inductively, and functions can be partial or total.

## Set Definition Types

| Type | Example |
|------|---------|
| **Extensional** | $M := \{1, 2, 3, 4, 5, 6, 7, 8, 9, 10\}$ |
| **Intensional** | $M := \{i \in \mathbb{N} \mid i \leq 10\}$ |
| **Inductive** | $M(1) := 1;\; \forall i \in \mathbb{N} : M(i) := \begin{cases} M(i-1)+1 & i \leq 10 \\ \text{undefined} & \text{otherwise} \end{cases}$ |

## Tuple Constructions

| Construction | Notation |
|-------------|----------|
| Pairs from two sets | $O := M \times N$ |
| Subsets of a set | $O := \mathcal{P}(M)$ |
| Tuples of length $n$ to $m$ | $O := \bigcup_{n \leq i \leq m} M^i$ |

## Disjoint Union

$$A \dot{\cup} B := \{(i, x) \in \{1, 2\} \times (A \cup B) \mid i = 1 \wedge x \in A \;\vee\; i = 2 \wedge x \in B\}$$

## Functions

| Concept | Notation |
|---------|----------|
| Partial function | $f : D \rightharpoonup B$ |
| Total function | $f : D \rightarrow B$ |
| Undefined | $f(d) \uparrow := \neg\exists b \in B : (d, b) \in f$ |
| Cardinality | $\|D \rightharpoonup B\| = (\|B\| + 1)^{\|D\|}$ |

**Predicates** are functions $D \mapsto \mathbb{B}$, where $\mathbb{B} := \{\mathbf{w}, \mathbf{f}\}$.

**Recursive notation**: e.g., $f(()) := 0;\; f((x, x_s)) := f((x_s)) + 1$

## Related Concepts

- [[Relations and Orderings]]: relations built on set-theoretic foundations
- [[Formal Modeling Steps]]: sets structure the symbol space in modeling
