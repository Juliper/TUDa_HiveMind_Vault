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
> Frame of Reference (FOR) encoding compresses a block of values by subtracting a common reference value (typically the minimum) and storing only the small residuals. This reduces the bit-width needed per value.

## How It Works

1. Divide the column into blocks of $B$ values
2. For each block, find $\text{min}$ (the reference/frame)
3. Store each value as $v_i - \text{min}$
4. Bit-pack the residuals using $\lceil \log_2(\text{max} - \text{min} + 1) \rceil$ bits

**Example:** Block `[1001, 1005, 1003, 1002, 1007]`
- Reference: $\text{min} = 1001$
- Residuals: $[0, 4, 2, 1, 6]$
- Bits needed: $\lceil \log_2(7) \rceil = 3$ bits per value

Instead of 11 bits per original value, we need only 3 bits plus the reference.

## Comparison with Plain Bit-Packing

| Technique | Bits per value (example) |
|---|---|
| Full integers | 32 bits |
| [[Bit-Packing Encoding]] | $\lceil \log_2(\text{max} + 1) \rceil$ |
| FOR | $\lceil \log_2(\text{max} - \text{min} + 1) \rceil$ |

> [!IMPORTANT]
> FOR is most effective when values in a block are close together (small range). If one outlier has a much larger value, it forces all residuals to use more bits. [[PFOR Encoding]] addresses this problem.

## Related Concepts

- [[Bit-Packing Encoding]]: FOR reduces the range before bit-packing
- [[PFOR Encoding]]: patched FOR that handles outliers separately
- [[Delta Encoding]]: alternative approach that stores differences between consecutive values
- [[Lightweight Compression]]: FOR is a core lightweight compression technique
