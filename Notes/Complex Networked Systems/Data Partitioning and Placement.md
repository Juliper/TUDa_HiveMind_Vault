---
title: Data Partitioning and Placement
aliases:
  - Table Partitioning Schemes
tags:
  - databases
  - parallelism
  - numa
  - performance
description: "How a DBMS splits tables into partitions and decides which NUMA node each partition should physically reside on"
draft: false
---

> [!NOTE] Definition
> A **partitioning scheme** splits a table into disjoint chunks based on some policy, while a **placement scheme** decides which physical memory region (NUMA node) each partition should be stored in.

## Partitioning Schemes

| Scheme | Description |
|---|---|
| **Round-robin / Random** | Tuples distributed cyclically or randomly across partitions, no ordering guarantee |
| **Range-partitioning** | Tuples split by value ranges of the partitioning key |
| **Hash-partitioning** | Tuples split by a hash function on the partitioning key |

## Partition Granularity

| Granularity | Trade-off |
|---|---|
| **Coarse-grained** (few, large partitions) | Lower scheduling overhead |
| **Fine-grained** (many, small partitions) | Better load-balancing across workers |

By tracking the location of each partition, the DBMS's scheduler can execute operators on the worker whose CPU core is physically closest to that partition's memory, minimizing [[NUMA Architecture|NUMA]]-remote accesses.

## Memory Allocation on NUMA Systems

When a DBMS calls `malloc`, the allocator typically just extends the process's virtual data segment - physical memory is only allocated by the OS when a page fault first occurs. On a NUMA system, the OS then has to decide **where** to place that physical page:

| Strategy | Behavior |
|---|---|
| **Interleaving** | Distribute allocated memory uniformly across all NUMA nodes |
| **First-Touch** | Allocate physical memory on the NUMA node of the CPU that first touched (wrote to) that memory location |
| **NUMA-aware pre-allocation** | The DBMS explicitly controls placement via APIs like `numa_alloc()`, or moves existing pages with Linux's `move_pages` |

> [!IMPORTANT]
> Measurements on a sequential scan workload (8 sockets, 10 cores/node) show that combining NUMA-aware allocation with thread pinning roughly **doubles** throughput compared to random partition placement, and the gain plateaus once thread count exceeds the number of physical cores.

## Related Concepts

- [[NUMA Architecture]]: the hardware property this scheme is designed around
- [[DBMS Task Scheduling]]: worker-to-core assignment must align with partition placement
- [[Partition-Based Hash Join]]: a concrete algorithm that relies on NUMA-local partitioning
