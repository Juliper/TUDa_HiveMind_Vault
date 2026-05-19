---
title: Null Suppression
aliases:
  - Leading Zero Suppression
  - Prefix Suppression
tags:
  - databases
  - compression
  - in-memory
description: "A compression technique that removes leading zeros or null bytes from values to reduce storage"
draft: false
---

> [!NOTE] Definition
> Null suppression removes leading zero bytes from integer values, storing only the significant bytes along with a small length indicator. This is effective when most values are much smaller than the maximum value in the column.

## How It Works

A 32-bit integer `0x00000042` (= 66) has 3 leading zero bytes. Null suppression stores only `0x42` plus a 2-bit length code indicating 1 byte.

| Original (4 bytes) | Compressed | Savings |
|---|---|---|
| `0x00000042` | `01` + `0x42` | 3 bytes |
| `0x0000ABCD` | `10` + `0xABCD` | 2 bytes |
| `0x12345678` | `11` + `0x12345678` | 0 bytes |

The 2-bit prefix encodes the number of significant bytes (1, 2, 3, or 4).

## Prefix Suppression

A related technique for strings: if values share a common prefix, store the prefix once and only the differing suffixes.

**Example:** URLs `["https://tu-darmstadt.de/a", "https://tu-darmstadt.de/b"]`
- Shared prefix: `"https://tu-darmstadt.de/"`
- Store only suffixes: `["a", "b"]`

> [!IMPORTANT]
> Null suppression works well after [[Delta Encoding]] or [[Frame of Reference Encoding]], where residuals are small values with many leading zeros.

## Related Concepts

- [[Delta Encoding]]: produces small values ideal for null suppression
- [[Frame of Reference Encoding]]: produces small residuals ideal for null suppression
- [[Lightweight Compression]]: null suppression is a core lightweight compression technique
