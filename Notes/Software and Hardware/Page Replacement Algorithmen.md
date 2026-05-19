---
title: Page Replacement Algorithms
aliases:
  - Page Replacement Algorithmen
  - Seitenersetzungsalgorithmen
tags:
  - operating-systems
  - memory-management
  - paging
description: "Algorithms that decide which page to evict from memory when a new page must be loaded"
draft: false
---

> [!NOTE] Definition
> When all page frames are occupied and a new page must be loaded, a page replacement algorithm decides which existing page to evict.

## Algorithms

### Optimal
- Evict the page that will not be used for the longest time in the future
- Theoretically best but impossible to implement (requires future knowledge)
- Used as a benchmark for comparison

### Not Recently Used (NRU)
Classifies pages using R (Referenced) and M (Modified) bits into four classes. Evicts a page from the lowest class:

| Class | R | M | Priority |
|-------|---|---|----------|
| 0 | 0 | 0 | Evict first |
| 1 | 0 | 1 | |
| 2 | 1 | 0 | |
| 3 | 1 | 1 | Evict last |

### FIFO (First-In, First-Out)
- Evict the page that has been in memory the longest
- Simple but ignores how frequently a page is used

### Second Chance
- FIFO variant: if the oldest page has R=1, set R=0 and move it to the end of the list (as if it were newly loaded)
- Only evicts pages with R=0

### Clock
- Circular list version of Second Chance
- A pointer advances around the circle; pages with R=1 get their bit cleared and are skipped, pages with R=0 are evicted

### Least Recently Used (LRU)
- Evict the page that has been unused for the longest time
- Good approximation of optimal, but expensive: requires updating a list on every memory access

### Not Frequently Used (NFU)
- Each page has a counter incremented on every clock interrupt if referenced
- Evict the page with the lowest counter
- Problem: pages heavily used early on retain high counters forever

### Aging
- Improvement on NFU: each clock tick, right-shift all counters and add the R bit as the highest bit
- Example: $R = (1,0,1,0)$ over four ticks results in counter value `0101000`
- Naturally "forgets" old references

### Working Set
- The working set is the set of pages a process is currently using
- Pages track when they were last referenced
- On page fault: if R=1, update timestamp; if R=0 and age $> \tau$, evict it
- If no evictable page is found, evict the oldest page

### WSClock
- Combines Working Set with Clock algorithm
- Circular list; on page fault: R=1 pages get timestamp updated; R=0 pages with age $> \tau$ are evicted (dirty pages get a write scheduled and the pointer moves on)

## Local vs Global Replacement

| Strategy | Description |
|----------|-------------|
| **Local** | Only replace pages within the same process - simple and fast |
| **Global** | Replace pages across all processes - flexible working set size |

> [!IMPORTANT]
> Best practice is to switch between local and global replacement based on page fault frequency.

## Related Concepts

- [[Page Table Entries]]: the R and M bits used by these algorithms
- [[Thrashing]]: what happens when the working set exceeds available frames
- [[Demand Paging vs Pre-Paging]]: when page faults trigger these algorithms
