---
title: Multiplexer
aliases:
  - MUX
  - MUX2
  - MUX4
  - Decoder
  - Dekodierer
  - Look-Up Table
  - LUT
tags:
  - digitaltechnik
  - logic
description: "Multiplexer (data selector), Decoder (one-hot output generator), and Look-Up Table — key combinational building blocks in digital design."
---

## Multiplexer (MUX)

A **Multiplexer** is a data selector: it passes one of its $2^n$ data inputs to the output, selected by $n$ **select bits** (also called control lines).

### MUX2 (2-to-1 Multiplexer)

One select bit $S$ chooses between inputs $D_0$ and $D_1$:

| $S$ | $Y$ |
|---|---|
| 0 | $D_0$ |
| 1 | $D_1$ |

$$Y = \overline{S} \cdot D_0 + S \cdot D_1$$

Gate realization: two AND gates (one with $\overline{S}$, one with $S$) feeding one OR gate.

### MUX4 (4-to-1 Multiplexer)

Two select bits $S_1 S_0$ choose among $D_0, D_1, D_2, D_3$:

| $S_1$ | $S_0$ | $Y$ |
|---|---|---|
| 0 | 0 | $D_0$ |
| 0 | 1 | $D_1$ |
| 1 | 0 | $D_2$ |
| 1 | 1 | $D_3$ |

$$Y = \overline{S_1}\,\overline{S_0}\,D_0 + \overline{S_1}\,S_0\,D_1 + S_1\,\overline{S_0}\,D_2 + S_1\,S_0\,D_3$$

A MUX4 can be built from three MUX2 units in a two-level tree.

### MUX as Look-Up Table (LUT)

By fixing the select bits as **function inputs** and wiring the data inputs to constants (0 or 1), a $2^n$-to-1 MUX implements **any Boolean function of $n$ variables**:

- Each data input corresponds to one row of the truth table
- The constant wired to $D_i$ sets $F(i)$

This is the **Look-Up Table (LUT)** principle used in FPGAs: an $n$-input LUT is simply a MUX with $2^n$ data inputs loaded from configuration memory.

> [!NOTE]
> A 4-input LUT can implement any of the $2^{16}$ possible 4-variable Boolean functions by changing only the 16 stored bits — no rewiring needed. This is why FPGAs are reconfigurable.

## Decoder (Dekodierer)

A **Decoder** converts an $n$-bit binary input into $2^n$ **one-hot** outputs — exactly one output is active for each input combination.

### 2-to-4 Decoder

| $A_1$ | $A_0$ | $Y_3$ | $Y_2$ | $Y_1$ | $Y_0$ |
|---|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 0 | 1 |
| 0 | 1 | 0 | 0 | 1 | 0 |
| 1 | 0 | 0 | 1 | 0 | 0 |
| 1 | 1 | 1 | 0 | 0 | 0 |

Each output $Y_i$ is the minterm $m_i$:

$$Y_0 = \overline{A_1}\,\overline{A_0}, \quad Y_1 = \overline{A_1}\,A_0, \quad Y_2 = A_1\,\overline{A_0}, \quad Y_3 = A_1\,A_0$$

### Applications of Decoders

- **Memory address decoding**: select one of $2^n$ memory chips/rows
- **Function generation**: any Boolean function $F = \sum m_i$ is realized by ORing the selected decoder outputs — decoder generates all minterms simultaneously
- **Seven-segment display**: 4-to-16 decoder stage in multi-digit designs

### Decoder vs. MUX

| | Decoder | MUX |
|---|---|---|
| **Inputs** | $n$ address bits | $n$ select bits + $2^n$ data bits |
| **Outputs** | $2^n$ one-hot lines | 1 selected output |
| **Generates** | All minterms | One function value |

## Related Concepts

- [[Kombinatorische Logik]]: MUX and Decoder are combinational building blocks
- [[Normalformen]]: Decoder outputs are exactly the minterms of the address variables
- [[Logikgatter]]: gate-level realization of MUX and Decoder
- [[Zeitverhalten]]: MUX delay depends on select-to-output path
