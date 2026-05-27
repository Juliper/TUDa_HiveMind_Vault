---
title: IMP Language Semantics
aliases:
  - Syntax und Semantik von Programmen
  - IMP
  - While-Sprache
tags:
  - formal-methods
  - moses
  - semantics
description: "Syntax and semantics of the IMP imperative language used for formal reasoning about programs"
draft: false
---

> [!NOTE] Definition
> IMP is a minimal imperative programming language used in formal semantics to study program behavior. It has arithmetic expressions, boolean expressions, and commands including assignment, sequencing, conditionals, and while loops.

## Domains

| Domain | Definition |
|--------|-----------|
| $Num$ | $:= \mathbb{Z}$, elements $n, m$ |
| $Bool$ | $:= \{true, false\}$, element $t$ |
| $Var$ | Set of variables, elements $X, Y$ |

## Syntax (Grammar)

```
aexpr ::= n | X | (aexpr + aexpr) | (aexpr - aexpr) | (aexpr * aexpr)
bexpr ::= true | false | (aexpr eq aexpr) | (aexpr leq aexpr) |
          not bexpr | (bexpr and bexpr) | (bexpr or bexpr)
c     ::= skip | X := aexpr | c; c |
          if bexpr then c else c fi | while bexpr do c od
```

A word $w$ is a syntactically correct program iff it is derivable from $Com$ in the grammar, i.e., $w \in L(Com)$.

## States and Evaluation

**State**: a function $\sigma : Var \rightarrow Num$ mapping variables to values.

**Set of all states**: $\Sigma_Z$

### Evaluation Relations

| Expression type | Relation |
|----------------|----------|
| Arithmetic | $\langle aexpr, \sigma \rangle \Downarrow n$ |
| Boolean | $\langle bexpr, \sigma \rangle \Downarrow t$ |
| Command | $\langle c, \sigma \rangle \longrightarrow \sigma'$ |

## Substitution

Replaces variables with values in an expression:

$$((2 + X) * (Y - X))[X \rightarrow 1, Y \rightarrow 0] = ((2 + 1) * (0 - 1))$$

### State Update

$$\sigma[X \backslash n](Y') := \begin{cases} n & \text{if } Y' = X \\ \sigma(Y') & \text{otherwise} \end{cases}$$

## Related Concepts

- [[Semantic Calculi]]: the rules for evaluating IMP programs
- [[Proof Techniques in MOSES]]: proving properties of IMP programs
- [[Formal Modeling Steps]]: IMP as a formalized programming language
