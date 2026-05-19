---
title: Internal and External Fragmentation
aliases:
  - Interne und Externe Fragmentierung
  - Memory Fragmentation
tags:
  - operating-systems
  - memory-management
description: "Two types of memory waste that occur with different memory partitioning schemes"
draft: false
---

> [!NOTE] Definition
> **Internal fragmentation** wastes space inside allocated partitions. **External fragmentation** wastes space between allocated partitions.

## Internal Fragmentation

- A partition is assigned to a process, but the process doesn't use all of it
- The unused space within the partition is unavailable to other processes
- Occurs with: [[Fixed Partitions]], any fixed-size allocation

## External Fragmentation

- After repeated allocation and deallocation, scattered free holes appear in memory
- Individual holes are too small for new processes, even though total free memory might be sufficient
- Occurs with: [[Variable Partitions]], [[Segmentierung]]
- Solution: **compaction** (moving processes to consolidate free space) - expensive

## Which Scheme Has Which Problem?

| Scheme | Internal | External |
|--------|----------|----------|
| [[Fixed Partitions]] | Yes | No |
| [[Variable Partitions]] | No | Yes |
| [[Segmentierung]] | No | Yes |
| [[Paging und Swapping\|Paging]] | Minimal (last page only) | No |

## Related Concepts

- [[Allocation-Strategien]]: strategies to minimize external fragmentation
- [[Paging und Swapping]]: largely eliminates both types of fragmentation
