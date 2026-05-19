---
title: Multilevel Page Tables
aliases:
  - Mehrstufige Seitentabellen
tags:
  - operating-systems
  - memory-management
  - paging
description: "Hierarchical page table structure that reduces memory overhead for large address spaces"
draft: false
---

> [!NOTE] Definition
> Instead of one large flat page table, multilevel page tables use a hierarchy of smaller tables. Only the tables actually needed are kept in memory.

## Why Multilevel?

A single-level page table for a 32-bit address space with 4KB pages requires $2^{20}$ entries - this wastes memory if most of the address space is unused. Multilevel tables only allocate sub-tables for address ranges actually in use.

## Structure

A virtual address is split into multiple parts, each indexing a level of the hierarchy:

```
|  Page Directory Index  |  Page Table Index  |  Offset  |
```

1. **Page Directory Entry (PDE)** points to a page table
2. **Page Table Entry (PTE)** points to a physical frame
3. **Offset** selects the byte within the frame

## Size Calculations

- PTE size = Page Frame Number (PFN) bits + management bits
- PFN bits = physical address bits - page offset bits

## Related Concepts

- [[Translation Lookaside Buffer]]: caches lookups to avoid walking the hierarchy
- [[Page Table Entries]]: what each entry contains
- [[Paging und Swapping]]: the paging system that uses these tables
