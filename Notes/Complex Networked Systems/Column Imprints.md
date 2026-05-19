---
title: Column Imprints
aliases:
  - Imprints
  - Cache-Conscious Column Index
tags:
  - databases
  - indexing
  - in-memory
  - performance
description: "A lightweight, cache-conscious secondary index structure that uses bit-vectors to quickly skip cache-line-sized blocks during column scans"
draft: false
---

> [!NOTE] Definition
> Column imprints are a secondary index structure for [[Column Store]] systems. For each cache-line-sized block of a column, an imprint stores a small bit-vector indicating which value ranges are present in that block. During a scan, blocks whose imprint does not overlap with the query range are skipped entirely.

## How It Works

1. **Divide** the value domain into $b$ equal-width buckets (typically $b = 64$, one per bit)
2. **For each cache line** of the column, set bit $j = 1$ if any value in the cache line falls into bucket $j$
3. **At query time**, create a query bitmask with bits set for buckets that overlap the predicate range
4. **AND** the query bitmask with each imprint - if the result is zero, skip that cache line

```mermaid
graph TD
    subgraph "Column (4 cache lines)"
        CL1["CL1: 3, 5, 2, 8"]
        CL2["CL2: 45, 47, 46, 44"]
        CL3["CL3: 12, 15, 11, 14"]
        CL4["CL4: 3, 4, 5, 6"]
    end
    subgraph "Imprints (bits for ranges 0-9, 10-19, 40-49, ...)"
        I1["CL1: 10000000"]
        I2["CL2: 00001000"]
        I3["CL3: 01000000"]
        I4["CL4: 10000000"]
    end
    Q["Query: col > 40"] --> QM["Query mask: 00001111"]
    QM --> AND1["AND with I1 = 0 - SKIP"]
    QM --> AND2["AND with I2 != 0 - SCAN"]
    QM --> AND3["AND with I3 = 0 - SKIP"]
    QM --> AND4["AND with I4 = 0 - SKIP"]
```

## Properties

| Property | Value |
|---|---|
| Space overhead | ~1 bit per value (with 64 buckets per cache line of 16 int32 values = 64/16 = 4 bits, but compressed) |
| Granularity | Cache-line level |
| Update cost | Cheap (set additional bits, never unset) |
| False positives | Possible (bit set but no qualifying value) |
| False negatives | Never |

> [!IMPORTANT]
> Column imprints are designed to be **cache-resident** themselves. The imprint index for a column is much smaller than the column itself (roughly 1/8th to 1/64th the size), so it fits in cache even when the column does not.

## Compression of Imprints

Consecutive cache lines often have similar imprints (especially in sorted or clustered data). Run-length compression on the imprint bit-vectors further reduces their size.

## Comparison with Zone Maps

| Feature | Column Imprints | [[Zone Maps]] |
|---|---|---|
| Granularity | Cache line (~64 bytes) | Page/block (~4 KB+) |
| Information | Which ranges present | Min/max only |
| Space | Larger | Very small |
| Precision | Higher | Lower |

## Related Concepts

- [[Zone Maps]]: coarser-grained alternative using min/max per block
- [[Vectorized Scan]]: imprints determine which blocks to scan
- [[Column Store]]: the storage model imprints are designed for
- [[Predicate Evaluation]]: imprints accelerate predicate evaluation by skipping blocks
