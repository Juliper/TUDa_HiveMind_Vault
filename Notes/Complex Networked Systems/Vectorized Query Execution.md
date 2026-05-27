---
title: Vectorized Query Execution
aliases:
  - Vector-at-a-Time Processing
  - Vectorized Execution
  - Batch Processing
tags:
  - databases
  - query-processing
  - in-memory
  - performance
description: "A query execution model that processes data in batches of vectors rather than one tuple or one column at a time, balancing interpretation overhead with materialization cost"
draft: false
---

> [!NOTE] Definition
> Vectorized query execution processes data in batches (vectors).

## Related Concepts

- [[SIMD Processing]]: vectorized execution enables effective SIMD usage
- [[Vectorized Scan]]: the scan operator in a vectorized execution engine
- [[Column Store]]: provides the columnar data that vectorized execution processes
- [[Late Materialization]]: vectors carry column segments, not reconstructed tuples
