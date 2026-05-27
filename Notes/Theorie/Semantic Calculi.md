---
title: Semantic Calculi
aliases:
  - Kalkule
  - Evaluation Rules
tags:
  - formal-methods
  - moses
  - semantics
description: "Formal rule systems for deriving the meaning of program expressions and commands"
draft: false
---

> [!NOTE] Definition
> Semantic calculi are formal rule systems that define how expressions and commands in a programming language are evaluated. They provide the derivation rules for the evaluation relations of [[IMP Language Semantics]].

## Evaluation Relations

| Relation | Meaning |
|----------|---------|
| $\langle aexpr, \sigma \rangle \Downarrow n$ | Arithmetic expression $aexpr$ evaluates to number $n$ in state $\sigma$ |
| $\langle bexpr, \sigma \rangle \Downarrow t$ | Boolean expression $bexpr$ evaluates to truth value $t$ in state $\sigma$ |
| $\langle c, \sigma \rangle \longrightarrow \sigma'$ | Command $c$ transforms state $\sigma$ into state $\sigma'$ |

## State Update in Calculi

When evaluating an assignment $X := aexpr$, the state is updated:

$$\sigma[X \backslash n](Y') := \begin{cases} n & \text{if } Y' = X \\ \sigma(Y') & \text{otherwise} \end{cases}$$

> [!IMPORTANT]
> A derivation tree built from these rules constitutes a formal proof that a program produces a specific result. The tree structure mirrors the syntactic structure of the program.

## Related Concepts

- [[IMP Language Semantics]]: the language whose semantics these calculi define
- [[Proof Techniques in MOSES]]: techniques for reasoning about derivations
- [[Rule Induction]]: induction principle over derivation rules
