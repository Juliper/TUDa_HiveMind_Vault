---
title: Zahlensysteme
aliases:
  - Number Systems
  - Positional Notation
  - Stellenwertsystem
  - Base Conversion
tags:
  - digitaltechnik
  - number-systems
description: "Positional number systems used in digital circuits — binary, octal, decimal, hexadecimal — and the algorithms for converting between them."
---

**Zahlensysteme** (number systems) in digital engineering are based on **positional notation**: the value of a digit depends on both the digit itself and its position (place value).

## Stellenwertsystem (Positional Notation)

A number in base $b$ with digits $d_n d_{n-1} \ldots d_1 d_0$ has value:

$$N = \sum_{i=0}^{n} d_i \cdot b^i$$

The **radix** (Basis) $b$ determines how many distinct digit symbols are used ($0$ to $b-1$).

## Wichtige Zahlensysteme

| System | Basis $b$ | Symbole | Präfix |
|---|---|---|---|
| Binär | 2 | 0, 1 | `0b` |
| Oktal | 8 | 0–7 | `0o` |
| Dezimal | 10 | 0–9 | — |
| Hexadezimal | 16 | 0–9, A–F | `0x` |

**Hexadezimal** is especially practical in digital engineering: one hex digit represents exactly 4 bits (a *nibble*), so two hex digits represent one byte.

## Umrechnung (Base Conversion)

### Dezimal → Basis b (Integer)

Repeated division by $b$; read remainders from bottom to top:

```
137 ÷ 2 = 68 R 1   ← LSB
 68 ÷ 2 = 34 R 0
 34 ÷ 2 = 17 R 0
 17 ÷ 2 =  8 R 1
  8 ÷ 2 =  4 R 0
  4 ÷ 2 =  2 R 0
  2 ÷ 2 =  1 R 0
  1 ÷ 2 =  0 R 1   ← MSB

137₁₀ = 1000 1001₂
```

### Dezimal → Basis b (Fraction)

Repeated multiplication by $b$; collect the integer parts from top to bottom:

```
0.625 × 2 = 1.25  → 1
0.25  × 2 = 0.5   → 0
0.5   × 2 = 1.0   → 1

0.625₁₀ = 0.101₂
```

> [!WARNING]
> Not every decimal fraction has a finite binary representation — just as $1/3$ has no finite decimal expansion, $0.1_{10}$ has no finite binary expansion. This causes floating-point rounding errors in computers.

### Basis b → Dezimal

Evaluate the positional sum directly:

$$1010_2 = 1 \cdot 2^3 + 0 \cdot 2^2 + 1 \cdot 2^1 + 0 \cdot 2^0 = 8 + 2 = 10_{10}$$

### Binär ↔ Oktal / Hexadezimal (Shortcut)

Group bits from the right: groups of **3** for octal, groups of **4** for hex.

```
Binary:  1010 1101
Hex:      A    D    → 0xAD
```

## Related Concepts

- [[Zweierkomplement]]: signed binary representations built on top of these number systems
- [[Boolesche Algebra]]: the algebra of binary (0/1) values that underlies digital logic
