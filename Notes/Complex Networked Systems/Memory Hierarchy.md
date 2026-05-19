---
title: Memory Hierarchy
aliases:
  - Speicherhierarchie
  - Cache Hierarchy
tags:
  - databases
  - hardware
  - performance
description: "The layered organization of storage from fast registers to slow disk, where each level trades capacity for speed"
draft: false
---

> [!NOTE] Definition
> The memory hierarchy organizes computer storage in layers ordered by speed and capacity. Faster layers (registers, caches) are small and expensive, while slower layers (DRAM, disk) are large and cheap. Database performance depends heavily on how well data access patterns exploit this hierarchy.

## Levels

| Level | Typical Size | Latency | Bandwidth |
|---|---|---|---|
| Registers | ~1 KB | < 1 ns | - |
| L1 Cache | 32-64 KB | ~1 ns | ~100 GB/s |
| L2 Cache | 256 KB - 1 MB | ~3-10 ns | ~50 GB/s |
| L3 Cache | 4-64 MB | ~10-30 ns | ~30 GB/s |
| DRAM | 16-512 GB | ~50-100 ns | ~25 GB/s |
| SSD | 0.5-8 TB | ~10-100 us | ~3 GB/s |
| HDD | 1-20 TB | ~5-10 ms | ~200 MB/s |

> [!IMPORTANT]
> Each level is roughly 10x slower than the one above it. The gap between DRAM and disk is especially dramatic - about 1000x for SSDs and 100,000x for HDDs.

## Cache Lines and Spatial Locality

Data moves between levels in fixed-size blocks called **cache lines** (typically 64 bytes). When the CPU accesses a memory address, the entire cache line containing that address is loaded.

This means:
- **Sequential access** is fast - subsequent elements are already in cache
- **Random access** is slow - each access may trigger a cache miss
- Data structures should be **cache-friendly** (contiguous, compact)

## Relevance for Databases

```mermaid
graph TD
    A[Data Layout Choice] --> B[Row Store - NSM]
    A --> C[Column Store - DSM]
    B --> D[Good for full-row access]
    B --> E[Poor cache utilization for scans]
    C --> F[Good for column scans]
    C --> G[Excellent cache utilization]
```

[[Main Memory DBMS]] systems must be designed with cache behavior in mind. The choice between [[Row Store]] and [[Column Store]] storage models directly impacts how well the system exploits the memory hierarchy.

## Related Concepts

- [[Main Memory DBMS]]: assumes data fits in DRAM, making cache behavior the primary bottleneck
- [[Disk-Based DBMS]]: traditional systems designed around the DRAM-to-disk boundary
- [[Row Store]]: N-ary Storage Model optimized for full-row access
- [[Column Store]]: Decomposition Storage Model optimized for columnar scans
