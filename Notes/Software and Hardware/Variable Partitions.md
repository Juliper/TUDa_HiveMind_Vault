---
title: Variable Partitions
aliases:
  - Variable Partitionierung
tags:
  - operating-systems
  - memory-management
description: "Memory partitioning scheme where partition sizes adapt to process requirements"
draft: false
---

> [!NOTE] Definition
> Variable partitioning assigns memory regions sized to match each process's actual needs, using a base address and a limit register.

## Address Calculation

$$\text{Physical Address} = \text{Base} + \text{Offset}$$

The hardware checks: $\text{Offset} \leq \text{Limit}$ before allowing access.

## Trade-offs

| Advantage | Disadvantage |
|-----------|-------------|
| No internal fragmentation | [[Interne und Externe Fragmentierung|External fragmentation]] |
| Efficient memory use | Compaction may be needed |
| Flexible partition sizes | More complex management |

> [!WARNING]
> External fragmentation: after repeated loading and unloading of processes, small unusable gaps appear between partitions. These holes may be too small individually for any new process.

## Related Concepts

- [[Fixed Partitions]]: the simpler but less efficient alternative
- [[Allocation-Strategien]]: how to choose which hole to fill
- [[Interne und Externe Fragmentierung]]: the fragmentation trade-off
