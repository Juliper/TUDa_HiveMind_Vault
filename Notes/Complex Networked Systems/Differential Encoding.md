---
title: Differential Encoding
aliases:
tags:
  - databases
  - compression
  - in-memory
description: A compression technique that stores differences between consecutive values rather than absolute values
draft: false
---

> [!NOTE] Definition
> Differential encoding stores each value as the difference (delta) from the previous value. For sorted or slowly-changing data, these deltas are small and can be compressed further with [[Bit-Packing Encoding]] or [[Frame of Reference Encoding]].

## How It Works

**Example:** `[100, 102, 105, 106, 110]` becomes `[100, 2, 3, 1, 4]`

The deltas are much smaller than the original values and require fewer bits.

## When It Works Best

- **Sorted columns** - deltas are small and non-negative
- **Time series data** - timestamps increase monotonically
- **Incrementing IDs** - deltas are often 1
## Related Concepts

- [[Frame of Reference Encoding]]: alternative approach that uses a per-block reference
- [[Bit-Packing Encoding]]: used to compress the small delta values
- [[Null Suppression]]: removes leading zeros from delta values
- [[Lightweight Compression]]: delta encoding is a core lightweight compression technique
