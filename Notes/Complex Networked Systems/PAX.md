---
title: PAX
aliases:
  - Partition Attributes Across
tags:
  - databases
  - storage-model
  - in-memory
description: "A hybrid storage layout that partitions attributes across mini-pages within each page, combining row store locality with column store scan efficiency"
draft: false
---

> [!NOTE] Definition
> PAX (Partition Attributes Across) is a hybrid storage model that divides each database page into mini-pages, one per attribute. Within a page, data is stored column-wise, but across pages, data is organized by rows. This combines the cache efficiency of [[Column Store]] with the page-level locality of [[Row Store]].

## Layout

```mermaid
graph TD
    subgraph "Traditional NSM Page"
        R1["Row 1: A1 A2 A3"]
        R2["Row 2: A1 A2 A3"]
        R3["Row 3: A1 A2 A3"]
    end
    subgraph "PAX Page"
        MP1["Mini-page A1: r1.A1, r2.A1, r3.A1"]
        MP2["Mini-page A2: r1.A2, r2.A2, r3.A2"]
        MP3["Mini-page A3: r1.A3, r2.A3, r3.A3"]
    end
```

Each page contains the same set of tuples, but attributes are stored together in mini-pages rather than interleaved.

## Comparison

| Property | [[Row Store\|NSM]] | [[Column Store\|DSM]] | PAX |
|---|---|---|---|
| Cache behavior (scan) | Poor | Excellent | Good |
| Tuple reconstruction | Free | Expensive | Cheap (within page) |
| Compression potential | Low | High | Medium |
| Page I/O granularity | Row-aligned | Column-aligned | Row-aligned |

> [!IMPORTANT]
> PAX is a compromise: it improves cache utilization for scans compared to NSM without requiring the expensive cross-column tuple reconstruction of full DSM. However, it does not achieve the same compression ratios as a pure column store.

## Related Concepts

- [[Row Store]]: traditional NSM layout that PAX improves upon
- [[Column Store]]: pure columnar layout that PAX partially emulates
- [[Memory Hierarchy]]: PAX is designed to improve cache line utilization
