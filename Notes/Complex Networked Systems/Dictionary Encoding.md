---
title: Dictionary Encoding
aliases:
  - Dictionary Compression
tags:
  - databases
  - compression
  - in-memory
description: "A compression technique that replaces repeated values with compact integer codes via a lookup dictionary"
draft: false
---

> [!NOTE] Definition
> Dictionary encoding replaces each distinct value in a column with a compact integer code. A separate dictionary maps codes back to original values. This is especially effective for columns with low cardinality (few distinct values) and is the foundation of compression in [[Column Store]] systems.

## How It Works

1. Build a dictionary of all distinct values in the column
2. Assign each value a fixed-width integer code
3. Replace all occurrences with their codes
4. Store the dictionary separately

**Example:**

| Original | Code |
|---|---|
| "Berlin" | 0 |
| "Munich" | 1 |
| "Hamburg" | 2 |

Column `["Berlin", "Munich", "Berlin", "Hamburg"]` becomes `[0, 1, 0, 2]`

## Benefits

- **Fixed-width codes** enable direct array indexing and [[SIMD Processing]]
- **Reduced memory footprint** - integer codes are smaller than strings
- **Faster comparisons** - compare integers instead of strings
- **Enables further compression** - encoded columns can be additionally compressed with [[Run-Length Encoding]], [[Bit-Packing Encoding]], or [[Frame of Reference Encoding]]

## Order-Preserving Dictionary Encoding

If dictionary codes preserve the sort order of original values, comparisons like `<`, `>`, `BETWEEN` can operate directly on codes without decoding:

$$v_1 < v_2 \iff \text{code}(v_1) < \text{code}(v_2)$$

> [!IMPORTANT]
> Order-preserving dictionaries enable range queries and sorting to work entirely on compressed data, avoiding decompression overhead. This is critical for efficient [[Query Processing on Compressed Data]].

## Code Width Optimization

With $d$ distinct values, codes need $\lceil \log_2 d \rceil$ bits. For a column with 1000 distinct values, codes need only 10 bits instead of storing full strings.

## Related Concepts

- [[Column Store]]: primary use case for dictionary encoding
- [[Lightweight Compression]]: dictionary encoding is the most fundamental lightweight compression scheme
- [[Run-Length Encoding]]: can be applied on top of dictionary-encoded columns
- [[Bit-Packing Encoding]]: stores dictionary codes in minimum bits
- [[Query Processing on Compressed Data]]: operating on encoded values without decompression
