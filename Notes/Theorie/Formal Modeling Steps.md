---
title: Formal Modeling Steps
aliases:
  - Modellierungsschritte
  - Formale Modellierung
tags:
  - formal-methods
  - moses
description: "The six-step process for creating formal models of systems using symbols, relations, and logic"
draft: false
---

> [!NOTE] Definition
> Formal modeling follows a structured six-step process to translate real-world systems into precise mathematical models.

## The Six Steps

```mermaid
flowchart TD
    A["1. Identify relevant things"] --> B["2. Model things as Symbols"]
    B --> C["3. Structure symbol set via value domains"]
    C --> D["4. Model relationships via Relations"]
    D --> E["5. Model properties via Functions"]
    E --> F["6. Model requirements via Relations"]
```

## Specification with Logic

Models can be specified using different formal languages:

| Formalism | Notation |
|-----------|----------|
| Regular language (semantics) | $L(\ldots) := (\{a\} \circ \{b\}) \circ (\{a\} \circ \{b\})^*$ |
| Regular expression | $E := ((a(a+b)^*))b)$ |
| Regular grammar | $G := (\Sigma, V, X_0, P)$ |
| DFA/NFA | $A := (\Sigma, Q, \delta, q_0, F)$ |

## Related Concepts

- [[Sets and Functions in MOSES]]: the mathematical foundation for modeling
- [[Relations and Orderings]]: step 4 and 6 use relations
- [[Aussagenlogik]]: logic used for specifying properties
- [[Prädikatenlogik]]: first-order logic for richer specifications
