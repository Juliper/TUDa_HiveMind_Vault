---
title: Zweierkomplement
aliases:
  - Two's Complement
  - Signed Numbers
  - Vorzeichendarstellung
  - Einerkomplement
  - Vorzeichen-Betrag
tags:
  - digitaltechnik
  - number-systems
description: "The three binary representations for signed integers — sign-magnitude, one's complement, and two's complement — and why two's complement dominates hardware design."
---

To represent **negative integers** in binary, hardware needs a convention. Three representations exist, each with different trade-offs.

## 1. Vorzeichen-Betrag (Sign-Magnitude)

The **MSB** is the sign bit ($0$ = positive, $1$ = negative); the remaining bits hold the magnitude.

| Bits | Value |
|---|---|
| `0 101` | +5 |
| `1 101` | −5 |

**Problems**: two representations of zero (`+0` and `−0`); addition requires sign-checking logic — not suitable for simple hardware adders.

## 2. Einerkomplement (One's Complement)

Negate by **flipping all bits** (bitwise NOT).

$$-5_{10}: \quad 0101_2 \xrightarrow{\text{flip}} 1010_2$$

**Problems**: still has two zeros (`0000` and `1111`); end-around carry needed in addition.

## 3. Zweierkomplement (Two's Complement)

Negate by **flipping all bits and adding 1**:

$$-N = \overline{N} + 1$$

$$-5_{10}: \quad 0101 \xrightarrow{\text{flip}} 1010 \xrightarrow{+1} 1011$$

**Check**: $1011_2 = -8 + 0 + 2 + 1 = -5$ ✓ (using the MSB weight $-2^{n-1}$)

### Warum Zweierkomplement?

- **Unique zero**: only one representation of 0
- **Standard addition works unchanged**: no special hardware needed; overflow is simply ignored
- **Asymmetric range**: for $n$ bits: $-2^{n-1}$ to $+2^{n-1}-1$ (e.g. 8-bit: −128 to +127)

### Value Formula

For an $n$-bit two's complement number $b_{n-1} b_{n-2} \ldots b_0$:

$$N = -b_{n-1} \cdot 2^{n-1} + \sum_{i=0}^{n-2} b_i \cdot 2^i$$

## Range-Übersicht (4-Bit)

| Representation | Min | Max | Zeros |
|---|---|---|---|
| Vorzeichen-Betrag | −7 | +7 | 2 |
| Einerkomplement | −7 | +7 | 2 |
| **Zweierkomplement** | **−8** | **+7** | **1** |

## Weitere Codes

### BCD (Binary-Coded Decimal)

Each decimal digit is encoded separately in 4 bits ($0000$–$1001$). Used in displays and financial calculations where decimal accuracy matters. Wastes 6 of 16 possible 4-bit patterns.

### Gray Code

Consecutive values differ in **exactly one bit** (unit distance code). Used in rotary encoders and analog-to-digital converters to avoid ambiguous intermediate states during transitions.

```
Decimal:  0   1   2   3   4   5   6   7
Binary:  000 001 010 011 100 101 110 111
Gray:    000 001 011 010 110 111 101 100
```

## Related Concepts

- [[Zahlensysteme]]: positional number systems that two's complement is built on
- [[Boolesche Algebra]]: the algebraic basis for bitwise NOT (used in complement operations)
