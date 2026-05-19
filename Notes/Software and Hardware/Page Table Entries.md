---
title: Page Table Entries
aliases:
  - PTE
tags:
  - operating-systems
  - memory-management
  - paging
description: "The data stored in each entry of a page table including frame number and status bits"
draft: false
---

> [!NOTE] Definition
> A Page Table Entry (PTE) maps a virtual page to a physical frame and stores metadata about the page's status and permissions.

## Fields

| Bit | Purpose |
|-----|---------|
| **Present** | Is the page currently in physical memory? (0 = on disk) |
| **Protection** | Access rights: read, write, execute |
| **Modified (Dirty)** | Has the page been written to? (determines if it needs to be written back to disk on eviction) |
| **Referenced** | Has the page been accessed for reading or writing? (used by [[Page Replacement Algorithmen]]) |
| **Caching Disabled** | Page should not be cached (e.g., memory-mapped I/O) |
| **Page Frame Number** | The physical frame this page maps to |

> [!IMPORTANT]
> The Referenced (R) and Modified (M) bits are critical for page replacement algorithms like [[Page Replacement Algorithmen|NRU and Clock]]. The OS periodically resets R bits to track recent usage.

## Related Concepts

- [[Multilevel Page Tables]]: the table structure that contains PTEs
- [[Page Replacement Algorithmen]]: algorithms that read R and M bits to decide which page to evict
