---
title: GOLAP
aliases:
  - GPU-in-Data-Path Architecture
tags:
  - databases
  - hardware
  - performance
description: "A GPU-in-data-path OLAP architecture that combines GPU-Direct Storage, on-GPU decompression, and GPU-accelerated pruning to exceed raw SSD bandwidth"
draft: false
---

> [!NOTE] Definition
> GOLAP is a research architecture (Boeschen, Ziegler, Binnig - TU Darmstadt/DFKI) that places the GPU directly "in the data path" between SSD storage and query execution, using [[GPU-Direct Storage]] combined with GPU-side decompression and pruning to reach effective analytical query bandwidths far above the raw SSD's read bandwidth.

## The Core Insight: Compressed Scan on GPU

Storing data compressed on the SSD and decompressing on the GPU (rather than storing it uncompressed) lets the *effective* bandwidth exceed the SSD's raw bandwidth, because less data has to physically travel over the storage interface:

| Configuration | Effective Bandwidth |
|---|---|
| SSD uncompressed (CPU or GPU) | ~19 GiB/s (SSD-bound) |
| SSD + GPU decompression | ~52 GiB/s |
| SSD + CPU decompression | ~25 GiB/s |

The CPU lacks sufficient compute to decompress at line rate without slowdown; the GPU can decompress and execute the query in an overlapped fashion.

## Compressed GPU Table Scan Pipeline

1. Store column chunks on SSD in a heavy-weight compressed format (e.g., LZ4, Deflate) once
2. At query time, load the compressed (smaller) chunks directly into GPU memory via GDS
3. Decompress and materialize the chunk in GPU memory using a decompression kernel
4. Execute the query kernel on the decompressed data

Multiple columns and multiple chunks are read, decompressed, and computed on with pipelined overlap: while one chunk's kernel executes, the next chunks' reads and decompressions are already in flight, hiding I/O and decompression latency behind compute (see [[GPU Query Execution Models]] for the general overlap technique).

## Opportunistic Pruning

GOLAP layers **fine-grained histogram metadata** per chunk (more informative than a simple min/max per column) combined with **GPU-accelerated metadata checks**, letting entire chunks be skipped before they are even read from the SSD.

> [!IMPORTANT]
> Pruning adds no slowdown in the low-selectivity case and prunes tens of percent more data than coarse min/max metadata, especially for large chunks and workloads with many-column sort orders.

## Results

Evaluated on SSB, TPC-H, and NYC Taxi query workloads, effective bandwidth improved progressively by layering optimizations:

| Configuration | Effective BW (relative to SSD-only baseline) |
|---|---|
| No pruning, no compression | ~baseline (SSD-bound) |
| Pruning only | up to ~7x |
| Compression only | moderate improvement, below pruning alone in some queries |
| Pruning + compression combined | up to ~13x, robust across all tested queries |

Combining pruning and compression together gives the largest and most consistent speedups across query types, since the two optimizations attack different bottlenecks (data volume read vs. data volume transferred).

## Industry Context

Similar GPU-accelerated query engine efforts are emerging in industry: Microsoft's "GPU Accelerated Fabric DW" and "CoddSpeed" project (Microsoft Fabric), and NVIDIA's GQE (GPU Query Engine), both pursuing overlapped decompression/transfer/execution pipelines analogous to GOLAP's design.

## Related Concepts

- [[GPU-Direct Storage]]: the underlying data path GOLAP is built on
- [[GPU Query Execution Models]]: the overlap-based execution strategy GOLAP's pipeline implements
- [[Data Partitioning and Placement]]: pruning is conceptually related to skipping irrelevant partitions early
