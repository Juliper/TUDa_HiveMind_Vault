---
title: Query Processing on Compressed Data
aliases:
  - Operating on Compressed Data
tags:
  - databases
  - compression
  - in-memory
  - query-processing
description: "Techniques for executing queries directly on compressed column data without full decompression, improving both memory and compute efficiency"
draft: false
---

> [!NOTE] Definition
> Query processing on compressed data executes operations (comparisons, aggregations, joins) directly on compressed representations without decompressing first. This reduces memory bandwidth usage and can even speed up computation by processing more values per cache line and SIMD register.

## Why It Matters

Decompressing before processing wastes:
- **Memory bandwidth** - moving decompressed data through the [[Memory Hierarchy]]
- **Cache space** - decompressed data is larger and evicts other useful data
- **CPU cycles** - decompression overhead added to every query

## Techniques by Compression Scheme

| Compression | Direct Operation |
|---|---|
| [[Dictionary Encoding]] | Compare encoded codes instead of strings |
| [[Run-Length Encoding]] | Aggregate over runs without expanding |
| [[Bit-Packing Encoding]] | SIMD comparisons on packed values |
| [[Frame of Reference Encoding]] | Adjust predicate constant instead of decoding values |

### Dictionary-Encoded Predicates

For a predicate `WHERE city = 'Berlin'`:
1. Look up `'Berlin'` in the dictionary to get code $c$
2. Scan the encoded column comparing against $c$ (integer comparison)

With [[Dictionary Encoding|order-preserving dictionaries]], even range predicates work:
- `WHERE city BETWEEN 'A' AND 'D'` becomes `WHERE code BETWEEN 0 AND 2`

### FOR-Encoded Predicates

For a predicate `WHERE x > 100` on a FOR block with reference $\text{min} = 95$:
- Transform to `WHERE (x - 95) > 5`, i.e., compare residuals against $100 - 95 = 5$

> [!IMPORTANT]
> The key insight is that lightweight compression schemes are designed to allow predicate transformation rather than data transformation. This is what distinguishes [[Lightweight Compression]] from heavyweight compression like LZ4 or Snappy.

## Related Concepts

- [[Dictionary Encoding]]: enables string predicates as integer comparisons
- [[Lightweight Compression]]: designed specifically to enable direct query processing
- [[Late Materialization]]: delays decompression until tuple reconstruction
- [[SIMD Processing]]: processes compressed values in parallel
