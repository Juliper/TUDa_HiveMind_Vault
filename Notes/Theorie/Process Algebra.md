---
title: Process Algebra
aliases:
  - Prozesse
  - CSP Processes
  - Prozessalgebra
tags:
  - formal-methods
  - moses
  - concurrency
description: "Algebraic framework for specifying concurrent systems using processes, alphabets, traces, and composition operators"
draft: false
---

> [!NOTE] Definition
> Process algebra provides a compositional framework for describing concurrent systems. A process $P := (E, Tr)$ is defined by its alphabet $E$ (the set of events it can perform) and its traces $Tr \subseteq E^*$.

## Core Definitions

| Concept | Definition |
|---------|-----------|
| Process | $P := (E, Tr)$ where $Tr \subseteq E^*$ |
| Alphabet | $\alpha(P) := E$ |
| Traces | $traces(P) := Tr$ |

## Process Expressions

| Expression | Meaning |
|-----------|---------|
| $STOP_E$ | Deadlocked process - performs no events |
| $SKIP_{E \setminus \{\checkmark\}}$ | Successfully terminating process |
| $(x \rightarrow P)$ | Prefix - perform event $x$, then behave as $P$ |
| $P \sqcap Q$ | Alternative (choice) - behave as $P$ or $Q$ |

### Process Function

$$process(E, t) := \begin{cases} STOP_E & \text{if } t = () \\ SKIP_{E \setminus \{\checkmark\}} & \text{if } t = (\checkmark) \\ (x \rightarrow process(E, t')) & \text{if } t = (x).t' \wedge \neg x = \checkmark \end{cases}$$

Recursive definitions use equation systems, e.g.:
$P := P_0$ with $P_0 =_E (x \rightarrow P_1)$, $P_1 =_E (y \rightarrow P_0)$

## Composition Operators

### Sequential Composition $(P; Q)$

$\alpha((P; Q)) = \alpha(P) = \alpha(Q)$

$$traces((P; Q)) = \{t \mid t \in traces(P) \wedge t \upharpoonright \{\checkmark\} = () \;\vee\; \exists t'.(\checkmark) \in traces(P) : \exists t'' \in traces(Q) : t = t'.t''\}$$

If $P$ does not terminate, only the traces of $P$ are included.

### Interleaving $(P \mid\mid\mid Q)$

$\alpha((P \mid\mid\mid Q)) := \alpha(P) = \alpha(Q)$

Traces are all possible interleavings of traces from $P$ and $Q$, preserving the internal order of each process.

$$Interleaving(t, u) := \begin{cases} \{t\} & \text{if } u = () \\ \{u\} & \text{if } t = () \\ \{(x).s \mid t = (x).t' \wedge s \in Interleaving(t', u) \;\vee\; u = (x).u' \wedge s \in Interleaving(t, u')\} & \text{otherwise} \end{cases}$$

> [!NOTE] Example
> $t = (2, 3), u = (4, 5)$:
> $Interleaving(t, u) = \{(2,3,4,5), (2,4,3,5), (2,4,5,3), (4,2,3,5), (4,2,5,3), (4,5,2,3)\}$

### Parallel Composition $(P \mid\mid Q)$

$\alpha((P \mid\mid Q)) := \alpha(P) \cup \alpha(Q)$

$$traces((P \mid\mid Q)) = \{t \in (\alpha(P) \cup \alpha(Q))^* \mid t \upharpoonright \alpha(P) \in traces(P) \wedge t \upharpoonright \alpha(Q) \in traces(Q)\}$$

Each process sees only its own events - the combined trace must project correctly onto both.

> [!IMPORTANT]
> Key differences between composition operators:
> - **Sequential** $(P; Q)$: $Q$ starts only after $P$ terminates ($\checkmark$)
> - **Interleaving** $(P \mid\mid\mid Q)$: same alphabet, arbitrary interleaving
> - **Parallel** $(P \mid\mid Q)$: alphabets may differ, shared events synchronize

## Related Concepts

- [[Transition Systems]]: lower-level behavioral model
- [[Transition System Composition]]: composition at the transition system level
