---
title: Bitvector Encoding
aliases:
  - Bitmap Encoding
  - Bit-Vector Encoding
tags:
  - databases
  - compression
  - in-memory
description: "A compression scheme that creates one bitvector per unique value in a column, enabling fast bitwise query evaluation"
draft: false
---

> [!NOTE] Definition
> Bitvector encoding creates a separate bit-vector for each unique value $v$ in a column $c$. For a column with $n$ rows and $d$ distinct values, it produces $d$ bitvectors each of length $n$, where $b_v[i] = 1$ if $c[i] = v$.

## How It Works

For each unique value $v$ in column $c$:
$$b_v[i] = \begin{cases} 1 & \text{if } c[i] = v \\ 0 & \text{otherwise} \end{cases}$$

| Property | Value |
|---|---|
| Space per bitvector | $n$ bits |
| Total space | $d \times n$ bits |
| Best for | Columns with few unique values |

## Example

A `ProductID` column with values $\{1, 2, 3\}$:

| Row | ProductID | BV(1) | BV(2) | BV(3) |
|---|---|---|---|---|
| 0 | 1 | 1 | 0 | 0 |
| 1 | 1 | 1 | 0 | 0 |
| 2 | 2 | 0 | 1 | 0 |
| 3 | 2 | 0 | 1 | 0 |
| 4 | 1 | 1 | 0 | 0 |
| 5 | 3 | 0 | 0 | 1 |

## Query Evaluation

Bitvectors enable fast predicate evaluation using bitwise operations:

- **Equality**: `WHERE ProductID = 2` - just read bitvector BV(2)
- **OR**: `WHERE ProductID = 1 OR ProductID = 3` - BV(1) OR BV(3)
- **COUNT**: `popcount(bitvector)` counts matching rows efficiently

> [!IMPORTANT]
> Bitvector encoding is especially powerful for [[Late Materialization]]. Operations like COUNT and GROUP BY can be computed directly on bitvectors without ever decompressing the original values.

## Related Concepts

- [[Bit-Packing Encoding]]: encodes values with minimal bits per value
- [[Run-Length Encoding]]: can compress sparse bitvectors further
- [[Late Materialization]]: bitvectors enable position-based query evaluation
- [[Query Processing on Compressed Data]]: bitwise operations avoid decompression
- [[Column Imprints]]: a related bitmap-based technique for range filtering
