---
title: Frame of Reference Encoding
aliases:
  - FOR Encoding
  - FOR
  - Frame of Reference
tags:
  - databases
  - compression
  - in-memory
description: "A compression technique that stores values as small offsets from a reference value, reducing the number of bits needed"
draft: false
---

> [!NOTE] Definition
> Frame of Reference (FOR) encoding compresses a block of values by representing the values as difference from some reference value.

## How It Works

1. Divide the column into blocks of $B$ values
2. For each block, find refernence value
3. Only store for each value the difference to the reference value

**Example:** Block `[1001, 1005, 1003, 1002, 1007]`
- Reference: $1003$
- Residuals: $[-2, 2, 0, -1, 4]$
## Related Concepts

- [[Bit-Packing Encoding]]: FOR reduces the range before bit-packing
- [[Delta Encoding]]: alternative approach that stores differences between consecutive values
- [[Lightweight Compression]]: FOR is a core lightweight compression technique
