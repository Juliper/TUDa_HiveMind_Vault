---
title: Delta Encoding
aliases:
  - Delta Compression
  - Differenzkodierung
tags:
  - databases
  - compression
  - in-memory
description: "A compression technique that stores differences between consecutive values rather than absolute values"
draft: false
---

> [!NOTE] Definition
> Delta encoding stores each value as the difference (delta) from the previous value. For sorted or slowly-changing data, these deltas are small and can be compressed further with [[Bit-Packing Encoding]] or [[Frame of Reference Encoding]].

## How It Works

Given sorted values $[v_1, v_2, \ldots, v_n]$, store:

$$[\delta_1 = v_1, \delta_2 = v_2 - v_1, \delta_3 = v_3 - v_2, \ldots, \delta_n = v_n - v_{n-1}]$$

**Example:** `[100, 102, 105, 106, 110]` becomes `[100, 2, 3, 1, 4]`

The deltas are much smaller than the original values and require fewer bits.

## When It Works Best

- **Sorted columns** - deltas are small and non-negative
- **Time series data** - timestamps increase monotonically
- **Incrementing IDs** - deltas are often 1

> [!IMPORTANT]
> Delta encoding requires sequential decoding - to access value $v_k$, you must sum all deltas $\delta_1 + \delta_2 + \ldots + \delta_k$. This makes random access expensive. In practice, deltas are stored in blocks with periodic checkpoints (prefix sums) to enable partial decoding.

## Combination with Other Techniques

Delta encoding is often combined with other compression:
1. Apply delta encoding to reduce value magnitudes
2. Apply [[Frame of Reference Encoding]] or [[Bit-Packing Encoding]] to compress the small deltas

## Related Concepts

- [[Frame of Reference Encoding]]: alternative approach that uses a per-block reference
- [[Bit-Packing Encoding]]: used to compress the small delta values
- [[Null Suppression]]: removes leading zeros from delta values
- [[Lightweight Compression]]: delta encoding is a core lightweight compression technique
