---
title: Logikgatter
aliases:
  - Logic Gates
  - Bubble Pushing
  - Gatter
  - NAND
  - NOR
  - XOR
  - XNOR
  - Zweistufige Logik
tags:
  - digitaltechnik
  - logic
description: "Gate symbols, XOR/XNOR behavior, two-level AND-OR logic, and Bubble Pushing — the technique for propagating inversions through gate networks."
---

**Logikgatter** are the physical building blocks of combinational circuits. Each gate implements a Boolean operation. Understanding gate symbols, inversion conventions, and the Bubble Pushing technique is essential for reading and drawing schematics.

## Grundgatter (Basic Gates)

| Gate | Symbol notation | Function |
|---|---|---|
| AND | $A \cdot B$ | 1 iff both inputs are 1 |
| OR | $A + B$ | 1 iff at least one input is 1 |
| NOT | $\overline{A}$ | Inversion (bubble on output) |
| NAND | $\overline{A \cdot B}$ | AND followed by inversion |
| NOR | $\overline{A + B}$ | OR followed by inversion |
| XOR | $A \oplus B$ | 1 iff inputs differ (odd parity) |
| XNOR | $\overline{A \oplus B}$ | 1 iff inputs are equal (even parity) |

Inversion is shown graphically as a **bubble** (small circle) on an input or output pin.

## XOR und XNOR

**XOR** (exclusive OR) outputs 1 when an **odd** number of inputs are 1:

$$A \oplus B = A\,\overline{B} + \overline{A}\,B$$

**XNOR** is the complement:

$$\overline{A \oplus B} = A\,B + \overline{A}\,\overline{B}$$

XOR chains compute **parity**: $A \oplus B \oplus C \oplus \ldots = 1$ iff an odd number of inputs are 1. Used in error detection and the [[Kombinatorische Logik|Volladdierer]].

## Zweistufige Logik (Two-Level Logic)

Any Boolean function in **DNF** can be implemented directly as a two-level AND-OR circuit:

- **Level 1**: one AND gate per product term (minterm or implicant)
- **Level 2**: one OR gate combining all product terms

$$F = \overline{A}\,B + A\,\overline{B}\,C \quad \Rightarrow \quad \text{two AND gates feeding one OR gate}$$

Two-level logic has a **bounded delay** (at most 2 gate delays from any input to the output) but may require wide gates (many inputs) for complex functions.

> [!NOTE]
> NAND-NAND networks implement the same AND-OR structure: by De Morgan, a NAND gate with inverted inputs equals an OR gate. NAND gates are preferred in CMOS because they are faster and smaller than NOR gates driving AND loads.

## Bubble Pushing

**Bubble Pushing** is a schematic technique for moving inversion bubbles through a gate network to achieve an equivalent circuit with fewer explicit inverters and gates that match the CMOS implementation style.

### Rules

1. **Push a bubble through a gate**: inversion bubbles on **all** inputs of a gate are equivalent to a bubble on the output — and the gate type flips (AND ↔ OR):

$$\text{AND with all inputs inverted} = \text{NOR (OR with inverted output)}$$
$$\text{OR with all inputs inverted} = \text{NAND (AND with inverted output)}$$

This follows directly from **De Morgan's laws**:
$$\overline{A} \cdot \overline{B} = \overline{A + B} \qquad \overline{A} + \overline{B} = \overline{A \cdot B}$$

2. **Bubbles on a wire cancel**: two bubbles in series on the same wire eliminate each other (double negation).

3. **Direction**: bubbles can be pushed **forward** (toward outputs) or **backward** (toward inputs).

### Goals of Bubble Pushing

- **Reduce inverter count**: a bubble absorbed into a gate pin replaces a standalone NOT gate
- **Match gate types to CMOS**: CMOS naturally produces NAND and NOR functions (not AND/OR); bubble-pushing converts AND-OR schematics into NAND-NAND or NOR-NOR equivalents
- **Improve readability**: complementary signal paths become explicit

### Example

Starting from: AND gate with output inversion (= NAND)

Push the output bubble back to the inputs + flip to OR:

$$\overline{A \cdot B} \;=\; \overline{A} + \overline{B}$$

Both circuits are identical in function; the second matches an OR gate with inverted inputs.

## Schematische Konventionen

- Signals flow **left to right** by convention
- Bubbles indicate **active-low** signals
- Complementary signals are drawn on **parallel paths** (one asserted, one inverted)
- Wire junctions are shown with a **dot**; crossing wires without a dot do not connect

## Related Concepts

- [[Kombinatorische Logik]]: circuit classification and structure
- [[Boolesche Algebra]]: De Morgan's laws underpin Bubble Pushing
- [[Normalformen]]: DNF is the starting point for two-level AND-OR synthesis
- [[Multiplexer]]: complex combinational building blocks built from gates
- [[Zeitverhalten]]: gate delays determine circuit speed
