---
title: Arithmetische Schaltungen
aliases:
  - Arithmetic Circuits
  - Addierer
  - Adder
  - Subtrahierer
  - Multiplizierer
  - Shifter
  - Barrel Shifter
  - CLA
  - Carry Lookahead
tags:
  - digitaltechnik
  - logic
description: "Combinational arithmetic building blocks — shifters, adders (RCA, CLA, CSA), subtractors, comparators, and multipliers."
---

**Arithmetische Schaltungen** implement mathematical operations in hardware. They are purely combinational ([[Kombinatorische Logik|Schaltnetze]]) and form the datapath core of processors and DSPs.

## Shifter

A shifter moves all bits of a word left or right by a specified number of positions.

| Type | Fill bits | Use case |
|---|---|---|
| **Logical shift** | 0 | Unsigned operations |
| **Rotate** | Wrap-around (bits that fall off re-enter on the other side) | Circular permutations |
| **Arithmetic right** | Sign bit (MSB replicated) | Signed division by $2^n$ |
| **Arithmetic left** | 0 (same as logical left) | Signed multiplication by $2^n$ |

### Barrel Shifter

A **Barrel Shifter** uses a cascade of MUX layers to shift by any amount in constant time. For an $n$-bit word, $\log_2 n$ MUX stages are needed — each stage conditionally shifts by $2^0, 2^1, 2^2, \ldots$ positions.

### Multiplikation durch Shifts

Multiplication by a constant can be decomposed into shifts and additions:

$$a \times 6 = a \times (4 + 2) = (a \ll 2) + (a \ll 1)$$

This avoids a full multiplier when the constant is known at design time.

## Addierer (Adders)

### Halbaddierer (Half Adder)

Adds two single-bit inputs $A, B$ — no carry-in:

$$S = A \oplus B \qquad C = A \cdot B$$

### Volladdierer (Full Adder)

Adds three single-bit inputs $A, B, C_{in}$:

$$S = A \oplus B \oplus C_{in} \qquad C_{out} = A \cdot B + A \cdot C_{in} + B \cdot C_{in}$$

Can be built from **two half adders** and one OR gate. See [[Kombinatorische Logik#Volladdierer (Full Adder)|Kombinatorische Logik]] for the full truth table.

### Ripple-Carry-Adder (RCA)

Chain of $n$ full adders, carry propagates serially from LSB to MSB.

- **Einfach** to design
- **Critical path**: $O(n)$ — carry must ripple through all stages
- Too slow for wide words ($n > 16$)

### Conditional Sum Adder (CSA)

Split the word into lower and upper halves. **Precompute** the upper half for both $C_{in}=0$ and $C_{in}=1$, then select the correct result with a [[Multiplexer|MUX]] once the actual carry arrives.

- Faster than RCA: critical path $O(\log n)$ with recursive splitting
- More hardware (two upper-half adders + MUX)

### Carry Lookahead Adder (CLA)

Eliminates serial carry propagation by computing all carries **in parallel** using **Generate** and **Propagate** signals:

$$G_i = A_i \cdot B_i \qquad P_i = A_i + B_i$$

$$C_i = G_i + P_i \cdot C_{i-1}$$

**Block-level** G and P over $k$ columns (e.g. $k=4$):

$$G_{3:0} = G_3 + P_3 \cdot G_2 + P_3 \cdot P_2 \cdot G_1 + P_3 \cdot P_2 \cdot P_1 \cdot G_0$$

| Adder | Critical Path | Hardware |
|---|---|---|
| RCA | $O(n)$ | $O(n)$ |
| CLA ($k$-bit blocks) | $O(n/k)$ | $O(n \cdot k)$ |
| Parallel Prefix | $O(\log n)$ | $O(n \log n)$ |

> [!NOTE]
> CLA with $k=4$ is faster than RCA starting from about $n=8$ bits. **Parallel Prefix Adders** (Brent-Kung, Kogge-Stone) achieve $O(\log n)$ depth using tree structures of G/P computations.

## Subtrahierer (Subtractor)

Uses [[Zweierkomplement]]: $A - B = A + \overline{B} + 1$

Implementation: invert all bits of $B$ (NOT gates), then feed into an adder with $C_0 = 1$.

## Vergleicher (Comparator)

| Operation | Method |
|---|---|
| $A < B$ | Compute $A - B$, check sign bit (MSB of result) |
| $A = B$ | Bitwise XNOR + AND tree: $\prod_{i}(A_i \odot B_i)$ |

## Multiplizierer (Multiplier)

For $n \times m$ bit inputs → $(n+m)$ bit output.

**Partial-product method** (like long multiplication in binary):
1. For each bit $B_j$ of the multiplier: $PP_j = A \cdot B_j$ (AND of all bits of $A$ with $B_j$)
2. Shift $PP_j$ left by $j$ positions
3. Sum all partial products

- **Area**: $O(n^2)$ — one AND gate per partial-product bit
- **Depth**: $O(n)$ — summing $n$ partial products
- **Karatsuba**: $O(n^{\log_2 3}) \approx O(n^{1.58})$ for large $n$

## Related Concepts

- [[Kombinatorische Logik]]: arithmetic circuits are Schaltnetze (acyclic)
- [[Zweierkomplement]]: subtraction and signed operations
- [[Logikgatter]]: gate-level building blocks (XOR for sum, AND for carry/products)
- [[Zeitverhalten]]: critical path determines adder speed
- [[Pipelining]]: pipelined adders/multipliers for higher throughput
