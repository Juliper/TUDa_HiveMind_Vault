---
title: Parallel Sort-Merge Join
aliases:
  - Sort-Merge Join
  - M-WAY
  - MPSM
  - Massively Parallel Sort-Merge
tags:
  - databases
  - parallelism
  - joins
  - performance
description: "A join algorithm that sorts both input relations on the join key and then merges them in a single scan, parallelized via multi-way merge or massively parallel variants"
draft: false
---

> [!NOTE] Definition
> A sort-merge join sorts both input relations R and S on the join key, then merges the sorted results in a single linear scan, comparing tuples as it advances through both sorted sequences.

## Two Phases

### Phase 1: Sort
Sort the tuples of R and S based on the join key.

### Phase 2: Merge
Scan the sorted relations and compare tuples; the outer relation R only needs to be scanned once during the merge.

## Parallel Variants

### Multi-Way Sort-Merge (M-WAY)

1. Each thread NUMA-locally partitions and sorts its chunk of the input ("local sort")
2. A **multi-way merge** combines the locally sorted runs into a single globally sorted sequence per relation
3. A **parallel merge join** is then performed on the two globally sorted relations

### Massively Parallel Sort-Merge (MPSM)

1. First, only **one** of the two inputs is partitioned across NUMA nodes and globally sorted
2. The other input is sorted **locally per partition** (not globally)
3. Each locally sorted partition of the second input is joined against the single globally sorted first input via a parallel cross-partition merge join

> [!IMPORTANT]
> The key benefit of MPSM is that it **avoids the expensive global merge phase for one of the two inputs**, which is often the scalability bottleneck of a standard parallel sort-merge join (M-WAY).

## Fast Single-Threaded Sorting

Sorting a partition is the most expensive part of a sort-merge join, so per-thread sort speed matters:

1. **Run generation**: fixed-size sorted runs are generated using a **sorting network** - a data-independent, fixed sequence of compare-and-swap steps with no branches, making it highly efficient on modern CPUs and implementable with [[SIMD Processing|SIMD]] instructions
2. **Merging**: sorted runs are combined into larger sorted blocks in two levels - **bitonic merge** (within-cache, SIMD-friendly) followed by **multi-way merge** (out-of-cache, merges many runs at once)

## Hash Join vs. Sort-Merge Join

Which approach wins has shifted repeatedly across published research as hardware evolved (wider SIMD, more cores, NUMA effects): some studies find hashing faster, others find sort-merge faster once SIMD is fully exploited, and later work argues the "best" choice is workload- and hardware-dependent rather than universal.

## Related Concepts

- [[Partition-Based Hash Join]]: the main alternative parallel join strategy
- [[SIMD Processing]]: accelerates both sorting networks and bitonic merge
- [[Data Partitioning and Placement]]: NUMA-local partitioning underlies both M-WAY and MPSM
- [[NUMA Architecture]]: the hardware property both variants are explicitly designed around
