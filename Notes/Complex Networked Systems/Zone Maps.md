---
title: Zone Maps
aliases:
  - Small Materialized Aggregates
  - SMA
  - Min-Max Index
tags:
  - databases
  - indexing
  - in-memory
  - performance
description: "Lightweight metadata storing min/max values per data block, enabling fast elimination of irrelevant blocks during scans"
draft: false
---

> [!NOTE] Definition
> Zone maps (also called Small Materialized Aggregates) store precomputed min and max values for each block of a column. During a scan, any block whose $[\text{min}, \text{max}]$ range does not overlap the query predicate is skipped entirely without reading the data.

## How It Works

For a column divided into blocks of $B$ values:

| Block | Min | Max |
|---|---|---|
| Block 0 | 3 | 15 |
| Block 1 | 42 | 89 |
| Block 2 | 7 | 23 |
| Block 3 | 100 | 150 |

For predicate `WHERE col > 50`:
- Block 0: max=15 < 50 - **SKIP**
- Block 1: max=89 > 50 - **SCAN** (might contain matches)
- Block 2: max=23 < 50 - **SKIP**
- Block 3: min=100 > 50 - **ALL QUALIFY** (no scan needed)

> [!IMPORTANT]
> Zone maps are extremely cheap in both storage (2 values per block) and maintenance (update min/max on insert). They are most effective on sorted or clustered columns where blocks have narrow value ranges.

## Effectiveness

Zone maps work best when:
- Data is **sorted** or **clustered** by the query column
- Queries are **range predicates** or equality checks
- Block sizes are appropriate (too large = poor selectivity, too small = too many zone maps)

On random data, zone maps provide little benefit because every block spans nearly the full value range.

## Related Concepts

- [[Column Imprints]]: finer-grained alternative with per-cache-line information
- [[Vectorized Scan]]: zone maps determine which blocks need scanning
- [[Predicate Evaluation]]: zone maps are a pre-filtering step before predicate evaluation
- [[Column Store]]: zone maps are a standard feature of column store systems
