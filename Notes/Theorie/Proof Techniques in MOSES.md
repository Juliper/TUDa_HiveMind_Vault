---
title: Proof Techniques in MOSES
aliases:
  - Beweistechniken
tags:
  - formal-methods
  - moses
description: "Proof methods for formal semantics including case distinction, contradiction, structural and rule induction"
draft: false
---

> [!NOTE] Definition
> Formal semantics requires rigorous proof techniques to establish properties of programs and transition systems. The main techniques are case distinction, contradiction, structural induction, induction over derivations, and rule induction.

## Case Distinction (Fallunterscheidung)

**Use case**: proving semantic equivalence of two programs.

**Schema**:
1. Assume Program 1 holds $\Rightarrow$ prove Program 2 holds (via derivation of Program 1)
2. Prove the reverse direction

## Proof by Contradiction (Widerspruchsbeweis)

**Use case**: proving non-termination.

**Schema**:
1. Assume $H$ is the shortest derivation
2. Find a contradiction, e.g., by showing a recursion that would yield a shorter derivation

## Structural Induction (Strukturelle Induktion)

Induction over the syntactic structure of expressions or programs. The induction hypothesis applies to all subexpressions.

## Induction over Derivations (Induktion uber Herleitung)

Induction over the height/structure of derivation trees in a semantic calculus.

## Rule Induction (Regelinduktion)

Induction over the rules of a calculus - prove a property holds for every rule's conclusion, assuming it holds for the premises.

> [!IMPORTANT]
> Choose the right technique based on what you're proving:
> - **Equivalence** $\rightarrow$ case distinction
> - **Non-termination** $\rightarrow$ contradiction
> - **Properties of all expressions** $\rightarrow$ structural induction
> - **Properties of all derivations** $\rightarrow$ rule induction

## Related Concepts

- [[Semantic Calculi]]: the calculi whose properties are proven
- [[IMP Language Semantics]]: the language about which proofs are constructed
- [[Transition Systems]]: proofs about system behavior
