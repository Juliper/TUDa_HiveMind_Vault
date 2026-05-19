---
title: Column Store
aliases:
  - DSM
  - Decomposition Storage Model
  - Column-Oriented Storage
  - Columnar Storage
tags:
  - databases
  - storage-model
  - in-memory
description: "A storage layout that stores each column contiguously in memory, optimized for analytical scans and compression"
draft: false
---

> [!NOTE] Definition
> A column store (Decomposition Storage Model, DSM) stores all values of a single column contiguously in memory. Each attribute becomes its own array, enabling efficient scans, compression, and SIMD processing for analytical workloads.

## Layout

In DSM, a table with columns $(A_1, A_2, \ldots, A_n)$ and $m$ rows stores data as separate arrays:

$$A_1: [r_1.A_1, r_2.A_1, \ldots, r_m.A_1]$$
$$A_2: [r_1.A_2, r_2.A_2, \ldots, r_m.A_2]$$

Each column is stored independently.

## Strengths and Weaknesses

| Aspect | Column Store |
|---|---|
| Column scan | Excellent - sequential memory access |
| Cache utilization (OLAP) | High - cache lines contain only relevant data |
| Compression | Excellent - same data type, high value locality |
| [[SIMD Processing]] | Natural fit - apply one operation to value arrays |
| Full-row access | Expensive - must gather from $n$ separate arrays |
| Tuple reconstruction | Requires position-based joins across columns |

> [!IMPORTANT]
> Column stores achieve high scan performance because sequential access over a single column maximizes cache line utilization and enables hardware prefetching. A scan over column $A_1$ uses 100% of every cache line.

## Tuple Reconstruction

To reconstruct full tuples, column stores rely on **positional alignment** - the $i$-th element in every column array belongs to the same tuple. This is called **virtual OIDs** (no explicit row identifiers needed).

## String Handling

Variable-length strings break the fixed-width assumption. Solutions:
1. **Padding** to maximum length (wastes space)
2. **Dictionary encoding** - replace strings with fixed-width integer codes
3. **Separate string pool** with offset arrays

[[Dictionary Encoding]] is the preferred approach as it also enables compression and faster comparisons.

## Related Concepts

- [[Row Store]]: the alternative layout optimized for full-row access
- [[PAX]]: hybrid layout combining row and column benefits
- [[Late Materialization]]: strategy that delays tuple reconstruction in column stores
- [[Dictionary Encoding]]: key compression technique for column stores
- [[SIMD Processing]]: hardware acceleration that benefits from columnar layout
- [[Lightweight Compression]]: compression techniques designed for column stores
