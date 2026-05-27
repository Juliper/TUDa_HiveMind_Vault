---
title: Transition Systems
aliases:
  - Transitionssysteme
  - LTS
  - Labeled Transition System
tags:
  - formal-methods
  - moses
  - concurrency
description: "Formal model of system behavior as states connected by labeled transitions, with traces and histories"
draft: false
---

> [!NOTE] Definition
> A transition system models the behavior of a system as a set of states $S$, events $E$, initial states $S_0$, and a transition relation $\rightarrow \subseteq S \times E \times S$. It forms the foundation for behavioral modeling and verification.

## Core Definitions

### Traces

A **trace** $t \in (S \cup E)^*$ is a sequence of alternating states and events:

$$Traces(TS) := \begin{cases} (s) \in Traces(TS) & \text{if } s \in S_0 \\ t.(s, e, s') \in Traces(TS) & \text{if } t.(s) \in Traces(TS) \wedge s \xrightarrow{e} s' \end{cases}$$

### Trace Operations

| Operation | Notation | Description |
|-----------|----------|-------------|
| Concatenation | $t_1.t_2$ | Append $t_2$ to $t_1$ |
| Prefix | $t' \leq t$ | $\exists t'' : t = t'.t''$ |
| Projection | $t \upharpoonright Q$ | Filter trace to only include elements in $Q$ |

### Derived Trace Types

| Type | Definition |
|------|-----------|
| **State traces** (S-Traces) | $\{t \upharpoonright S \mid t \in Traces(TS)\}$ |
| **Event traces** (E-Traces) | $\{t \upharpoonright E \mid t \in Traces(TS)\}$ |

### Histories

$$Hist(TS) := \{h : \mathbb{N}^+ \rightarrow (S \cup E) \mid h(1) \in S_0 \wedge \forall n \in \mathbb{N}^+ : h(2n-1) \xrightarrow{h(2n)} h(2n+1)\}$$

| Type | Definition |
|------|-----------|
| **State histories** | $S\text{-}Hist(TS) := \{h : \mathbb{N}^+ \rightarrow S \mid \exists h' \in Hist(TS) : \forall n \in \mathbb{N}^+ : h(n) = h'(2n-1)\}$ |
| **Event histories** | $E\text{-}Hist(TS) := \{h : \mathbb{N}^+ \rightarrow E \mid \exists h' \in Hist(TS) : \forall n \in \mathbb{N}^+ : h(n) = h'(2n)\}$ |

## Related Concepts

- [[Transition System Composition]]: combining multiple transition systems
- [[Process Algebra]]: an alternative formalism for specifying concurrent behavior
- [[Proof Techniques in MOSES]]: proving properties of transition systems
