---
title: Bit-Packing Encoding
aliases:
  - Bit-Packing
  - Bit-Vector Encoding
tags:
  - databases
  - compression
  - in-memory
description: "A compression technique that stores integer values using only the minimum number of bits required"
draft: false
---

> [!NOTE] Definition
> Bit-packing encoding stores integer values using only the minimum number of bits needed to represent the largest value, rather than using a full machine word (32 or 64 bits). This is especially effective after [[Dictionary Encoding]] when the number of distinct values is small.

## How It Works

Given values in range $[0, max]$, each value needs $b = \lceil \log_2(max + 1) \rceil$ bits.

**Example:** A column with values in $[0, 7]$ needs only 3 bits per value instead of 32. This allows to load multiple Values instead of just one value per load operation:

| Value | 32-bit | 3-bit |
|---|---|---|
| 5 | `00000000...00000101` | `101` |
| 3 | `00000000...00000011` | `011` |
| 7 | `00000000...00000111` | `111` |

## Integration with SIMD

Bit-packed data is well-suited for [[SIMD Processing]]:
- Multiple packed values fit in a single SIMD register (128/256/512 bits)
- Parallel comparison and extraction operations
- Up to $\lfloor 512 / b \rfloor$ values processed simultaneously with AVX-512

## Related Concepts
* [[Bit-Packing Encoding|Bit-Vector Encoding]]: An alternative form creates one bit-vector per distinct value
- [[Dictionary Encoding]]: produces the integer codes that are then bit-packed
- [[Frame of Reference Encoding]]: reduces value range before bit-packing
- [[SIMD Processing]]: processes multiple bit-packed values in parallel
- [[Predicate Evaluation]]: uses bit-vectors for efficient multi-predicate scans
- [[Lightweight Compression]]: bit-packing is a core lightweight compression technique
