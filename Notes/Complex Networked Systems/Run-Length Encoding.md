---
title: Run-Length Encoding
aliases:
  - RLE
  - Lauflangenkodierung
tags:
  - databases
  - compression
  - in-memory
description: "A compression technique that replaces consecutive repeated values with (value, count) pairs"
draft: false
---

> [!NOTE] Definition
> Run-Length Encoding (RLE) compresses data by replacing consecutive sequences of the same value (runs) with a pair of (value, run length). It is highly effective on sorted columns where identical values cluster together.

## How It Works

A column `[A, A, A, B, B, C, C, C, C]` is encoded as:

| Value | Run Length |
|---|---|
| A | 3 |
| B | 2 |
| C | 4 |

Storage shrinks from 9 values to 3 pairs.

## Compression Ratio

For a column of $n$ values with $r$ runs:

$$\text{Compression ratio} = \frac{n}{2r}$$

RLE is most effective when:
- The column is **sorted** (maximizes run lengths)
- The column has **low cardinality** (few distinct values)
- Values appear in **clusters**

> [!IMPORTANT]
> On unsorted columns with high cardinality, RLE can actually **increase** storage (each value becomes a pair). RLE should only be applied to sorted or clustered data.

## Use in Databases

RLE is often combined with [[Dictionary Encoding]]:
1. First encode strings as integer codes
2. Sort the column (or use a sorted index)
3. Apply RLE on the sorted codes

This two-stage approach is common in [[Column Store]] systems.

## Related Concepts

- [[Dictionary Encoding]]: often applied before RLE
- [[Bit-Packing Encoding]]: alternative compression for integer codes
- [[Lightweight Compression]]: RLE is a core lightweight compression technique
- [[Column Store]]: RLE works best on columnar data
