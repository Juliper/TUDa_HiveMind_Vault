---
title: Fixed Partitions
aliases:
  - Fixe Partitionierung
tags:
  - operating-systems
  - memory-management
description: "Memory partitioning scheme where RAM is divided into fixed-size regions assigned to processes"
draft: false
---

> [!NOTE] Definition
> Fixed partitioning divides physical memory into equally sized partitions. Each process is assigned one partition.

## Address Calculation

$$\text{Physical Address} = \text{Base Address (partition start)} + \text{Offset}$$

## Trade-offs

| Advantage | Disadvantage |
|-----------|-------------|
| Simple to implement | [[Interne und Externe Fragmentierung|Internal fragmentation]] |
| Fast context switch | Fixed partition count limits concurrency |
| Predictable memory allocation | Small processes waste large partitions |

> [!WARNING]
> Internal fragmentation occurs because a process rarely uses all the memory in its assigned partition. The unused space within the partition cannot be used by other processes.

## Related Concepts

- [[Variable Partitions]]: the flexible alternative
- [[Interne und Externe Fragmentierung]]: the fragmentation problem
