---
title: Segmentation
aliases:
  - Segmentierung
tags:
  - operating-systems
  - memory-management
description: "Memory management scheme that divides a process's address space into variable-length segments"
draft: false
---

> [!NOTE] Definition
> Segmentation divides a process's memory into logical segments (e.g., one for stack, one for code, one for heap), each with its own base address and limit. These segments are tracked in a segment table.

## Address Calculation

$$\text{Physical Address} = \text{Segment Base} + \text{Offset}$$

The hardware verifies: $\text{Offset} < \text{Segment Limit}$

## Key Registers

- **STBR** (Segment Table Base Register): points to the segment table's location in memory
- **STLR** (Segment Table Length Register): number of segments in the program

## Trade-offs

| Advantage | Disadvantage |
|-----------|-------------|
| No internal fragmentation | External fragmentation possible |
| Multiple independent protected address spaces | Each segment must be contiguous |
| Process memory blocks don't need to be contiguous | More complex than paging |

## Related Concepts

- [[Paging und Swapping]]: the alternative that uses fixed-size pages
- [[Interne und Externe Fragmentierung]]: segmentation trades internal for external fragmentation
- [[Variable Partitions]]: similar concept at a coarser level
