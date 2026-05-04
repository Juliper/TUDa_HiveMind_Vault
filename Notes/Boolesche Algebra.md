---
title: Boolesche Algebra
aliases:
  - Boolean Algebra
  - Schaltalgebra
  - Boolean Laws
  - De Morgan
tags:
  - digitaltechnik
  - logic
description: "The algebraic system for binary variables and logic operations — the mathematical foundation of all digital circuits."
---

**Boolesche Algebra** (Boolean / switching algebra) is the algebra of binary variables that can take only two values: **0** and **1**. It provides the mathematical foundation for designing and simplifying digital logic circuits.

## Grundoperationen (Basic Operations)

| Operation | Symbol | Name |
|---|---|---|
| AND | $A \cdot B$ | Konjunktion |
| OR | $A + B$ | Disjunktion |
| NOT | $\overline{A}$ | Negation / Komplement |

## Gesetze der Booleschen Algebra

### Kommutativgesetz (Commutativity)
$$A \cdot B = B \cdot A \qquad A + B = B + A$$

### Assoziativgesetz (Associativity)
$$(A \cdot B) \cdot C = A \cdot (B \cdot C) \qquad (A + B) + C = A + (B + C)$$

### Distributivgesetz (Distributivity)
$$A \cdot (B + C) = A \cdot B + A \cdot C$$
$$A + (B \cdot C) = (A + B) \cdot (A + C)$$

> [!NOTE]
> The second distributive law (OR distributes over AND) has no analogue in ordinary algebra — it is specific to Boolean algebra.

### Idempotenz (Idempotency)
$$A \cdot A = A \qquad A + A = A$$

### Neutralelement (Identity)
$$A \cdot 1 = A \qquad A + 0 = A$$

### Absorptionsgesetz (Absorption)
$$A \cdot (A + B) = A \qquad A + (A \cdot B) = A$$

### Komplementgesetz (Complement)
$$A \cdot \overline{A} = 0 \qquad A + \overline{A} = 1$$

### Doppelte Negation (Double Negation)
$$\overline{\overline{A}} = A$$

## De Morgansche Gesetze

De Morgan's theorems connect AND/OR through negation:

$$\overline{A \cdot B} = \overline{A} + \overline{B}$$
$$\overline{A + B} = \overline{A} \cdot \overline{B}$$

**Mnemonic**: *break the bar, change the operator*.

De Morgan is essential for:
- Implementing AND gates using only NOR/NAND gates
- Transforming between [[Normalformen|DNF and KNF]]
- Simplifying logic expressions

## Dualitätsprinzip (Duality)

Every Boolean identity has a **dual**: swap AND↔OR and 0↔1. Both forms are equally valid. This is why most laws come in pairs.

## Praktische Vereinfachung (Simplification)

Boolean algebra is used to minimize logic expressions before implementing them in hardware:

$$F = A \cdot B + A \cdot \overline{B} = A \cdot (B + \overline{B}) = A \cdot 1 = A$$

Systematic minimization is done with [[Normalformen]] (DNF/KNF) and [[Karnaugh-Veitch-Diagramme]].

## Related Concepts

- [[Normalformen]]: canonical forms (DNF/KNF) derived from Boolean algebra
- [[Karnaugh-Veitch-Diagramme]]: graphical method for applying Boolean simplification
- [[Zahlensysteme]]: the binary number system that Boolean variables operate over
