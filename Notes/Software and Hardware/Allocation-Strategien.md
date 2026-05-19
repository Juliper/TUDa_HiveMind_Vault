---
title: Memory Allocation Strategies
aliases:
  - Allocation-Strategien
  - Allokationsstrategien
tags:
  - operating-systems
  - memory-management
description: "Strategies for choosing which free memory block to allocate to a new process"
draft: false
---

> [!NOTE] Definition
> When a process needs memory, the OS must decide which free block (hole) to use. Different strategies optimize for speed, utilization, or fragmentation.

## Strategies

| Strategy | Description | Trade-off |
|----------|-------------|-----------|
| **First Fit** | First hole that is large enough | Fast, but may fragment the beginning of memory |
| **Next Fit** | Like First Fit, but starts searching from where the last allocation ended | Distributes allocations more evenly |
| **Best Fit** | Smallest hole that is large enough | Minimizes wasted space, but slow (must scan all holes) |
| **Worst Fit** | Largest available hole | Leaves large remaining holes, but slow |
| **Quick Fit** | Maintains separate lists of holes by size category (e.g., $\leq 64\text{KB}$, $\leq 128\text{KB}$, ...) | Very fast lookup, more complex bookkeeping |

> [!IMPORTANT]
> First Fit and Best Fit generally perform better than Worst Fit in practice. Quick Fit offers the best lookup time but requires maintaining multiple free lists.

## Related Concepts

- [[Interne und Externe Fragmentierung]]: what these strategies try to minimize
- [[Freispeicherverwaltung]]: how free memory is tracked (bitmaps vs linked lists)
- [[Variable Partitions]]: the partitioning scheme that needs these strategies
