---
title: Late Materialization
aliases:
  - Lazy Materialization
  - Deferred Materialization
tags:
  - databases
  - query-processing
  - in-memory
description: "A query processing strategy in column stores that delays tuple reconstruction until the final result, operating on position lists instead"
draft: false
---

> [!NOTE] Definition
> Late materialization is a query execution strategy in [[Column Store]] systems that delays the reconstruction of full tuples as long as possible. Instead of immediately combining columns into rows, it passes **position lists** (arrays of qualifying row positions) between operators.

## Early vs Late Materialization

```mermaid
graph TD
    subgraph "Early Materialization"
        E1["Scan col A"] --> E2["Reconstruct tuples"]
        E3["Scan col B"] --> E2
        E2 --> E4["Apply remaining predicates"]
        E4 --> E5["Project result"]
    end
    subgraph "Late Materialization"
        L1["Scan col A - get positions"] --> L3["Intersect positions"]
        L2["Scan col B - get positions"] --> L3
        L3 --> L4["Fetch only needed columns at final positions"]
        L4 --> L5["Project result"]
    end
```

| Strategy | Tuple Construction | Data Moved |
|---|---|---|
| **Early** | Before filtering | All columns for all candidates |
| **Late** | After all filtering | Only result columns for final matches |

## Benefits

1. **Reduced memory bandwidth** - only qualifying columns are read at the end
2. **Better compression** - columns stay compressed longer, enabling [[Query Processing on Compressed Data]]
3. **SIMD-friendly** - position lists and column arrays enable [[SIMD Processing]]
4. **Cache efficiency** - less data moved through [[Memory Hierarchy]]

> [!IMPORTANT]
> Late materialization is one of the key reasons [[Column Store]] systems outperform [[Row Store]] systems for analytical queries. By avoiding premature tuple reconstruction, they minimize the amount of data that flows through the query pipeline.

## Position Lists

A position list is a sorted array of row indices where a predicate is satisfied:

$$P = \{i \mid \text{predicate}(A[i]) = \text{true}\}$$

Multiple predicates produce multiple position lists that are intersected (AND) or unioned (OR) using fast merge operations or [[Bit-Packing Encoding|bit-vector]] operations.

## Related Concepts

- [[Column Store]]: the storage model that enables late materialization
- [[Query Processing on Compressed Data]]: late materialization keeps data compressed longer
- [[Predicate Evaluation]]: determines the position lists
- [[SIMD Processing]]: accelerates both predicate evaluation and position list operations
