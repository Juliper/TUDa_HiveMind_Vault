---
title: Parallel Hash Table Construction
aliases:
  - Lock-Free Hash Table Build
tags:
  - databases
  - parallelism
  - concurrency
  - performance
description: "How DBMSs build and probe hash tables in parallel using lock-free inserts and Bloom-filter-accelerated lookups"
draft: false
---

> [!NOTE] Definition
> A DBMS's join hash table is built and probed in two strictly separated phases - a write-only **build** phase and a read-only **probe** phase - which allows the probe phase to avoid locking entirely and the build phase to use lock-free inserts instead of general-purpose synchronization.

## Why General-Purpose Hash Tables Are a Poor Fit

Standard library hash tables (`std`, boost) are not well suited for database joins because:

- They pay **high overhead for parallel execution**, since DBMS joins execute in two clearly distinct phases (no locking is actually needed during the read-only probe phase)
- **Non-matching rows** are common in real join workloads (most probes find no partner), which general hash tables do not optimize for
- **Skewed key distributions** lead to hash collisions concentrated in a few buckets

## Build Phase: Lock-Free Parallel Insert

Because the number of tuples to insert is known in advance (from the partition size), the hash table can be pre-sized before insertion begins. Each bucket is implemented as a linked list; concurrent threads insert new entries using **compare-and-swap** in a busy loop instead of a lock:

```
Entry* current = slot.load();
do {
    newEntry->next = current->next;
} while (!slot.compare_exchange_weak(current, newEntry));
```

This is a direct application of the [[Atomic Instructions|compare-and-swap (CAS)]] primitive: if another thread modified the slot concurrently, the CAS fails and the loop retries with the updated pointer, avoiding any blocking lock.

## Probe Phase: Read-Only, Bloom-Filter Accelerated

Since the probe phase is strictly read-only (no inserts happen during probing), no synchronization is needed at all. Because most probes are expected to be negative (the tuple has no join partner), a [[Bloom Filter]] embedded in the hash table's directory (using spare lower bits as a filter) lets the probe skip traversing the bucket's linked list entirely when the filter reports "definitely not present."

## Related Concepts

- [[Partition-Based Hash Join]]: the algorithm this build/probe mechanism implements
- [[Atomic Instructions]]: compare-and-swap is the hardware primitive enabling lock-free insert
- [[Bloom Filter]]: accelerates the read-only probe phase
- [[Translation Lookaside Buffer]]: motivates keeping the number of concurrently written pages small during insert
