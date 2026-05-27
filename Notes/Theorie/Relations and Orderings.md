---
title: Relations and Orderings
aliases:
  - Relationen und Ordnungen
  - Partial Order
  - Partielle Ordnung
  - Lattice
  - Verband
tags:
  - formal-methods
  - moses
description: "Properties of relations (reflexive, transitive, etc.) and ordering structures including partial orders and lattices"
draft: false
---

> [!NOTE] Definition
> Relations on a set $M$ can satisfy various properties that determine the type of ordering they impose. Combinations of these properties yield well-known structures like partial orders and lattices.

## Relation Properties

| Property | Formal Definition |
|----------|-------------------|
| Reflexive | $\forall x \in M : (x, x) \in R$ |
| Symmetric | $\forall x, y \in M : (x, y) \in R \Rightarrow (y, x) \in R$ |
| Asymmetric | $\forall x, y \in M : (x, y) \in R \Rightarrow (y, x) \notin R$ |
| Antisymmetric | $\forall x, y \in M : ((x, y) \in R \wedge (y, x) \in R) \Rightarrow (x, y) = (y, x)$ |
| Transitive | $\forall x, y, z \in M : ((x, y) \in R \wedge (y, z) \in R) \Rightarrow (x, z) \in R$ |
| Alternative | $\forall x, y \in M : (x, y) \in R \vee (y, x) \in R$ |

## Ordering Types

| Ordering | Properties |
|----------|-----------|
| **Quasi-order** | reflexive $\wedge$ transitive |
| **Partial order** | reflexive $\wedge$ antisymmetric $\wedge$ transitive |
| **Strict order** | irreflexive $\wedge$ asymmetric $\wedge$ transitive |
| **Total / Linear order** | reflexive $\wedge$ antisymmetric $\wedge$ transitive $\wedge$ alternative |

## Lattice Operators

Given an ordered set $(M, \leq)$:

| Operator | Name | Definition |
|----------|------|-----------|
| $m_1 \sqcup m_2$ | Join (upper bound) | $\{m \in M \mid m_1 \leq m \wedge m_2 \leq m \wedge \forall n \in M : (m_1 \leq n \wedge m_2 \leq n) \Rightarrow m \leq n\}$ |
| $m_1 \sqcap m_2$ | Meet (lower bound) | $\{m \in M \mid m_1 \geq m \wedge m_2 \geq m \wedge \forall n \in M : (m_1 \geq n \wedge m_2 \geq n) \Rightarrow m \geq n\}$ |

A **lattice** (Verband) is an ordered set $(M, \leq)$ where both $\sqcup$ and $\sqcap$ are defined for all pairs.

## Related Concepts

- [[Sets and Functions in MOSES]]: foundational set operations used with relations
- [[Formal Modeling Steps]]: relations are used to model relationships between entities
