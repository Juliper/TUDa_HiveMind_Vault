---
title: Paging and Swapping
aliases:
  - Paging und Swapping
  - Virtual Memory Paging
tags:
  - operating-systems
  - memory-management
  - paging
description: "Mechanisms for managing memory by dividing it into fixed-size pages and swapping processes to disk"
draft: false
---

> [!NOTE] Definition
> **Swapping** moves an entire process's memory to secondary storage when RAM is full. **Paging** divides memory into fixed-size blocks (pages) and can move individual pages instead.

## Swapping

- When main memory is full, the OS copies an inactive process's entire memory to disk
- The process is later swapped back in when it needs to run
- Simple but coarse-grained: moves everything, even pages that aren't needed

## Paging

- Memory is divided into equal-sized **pages** (virtual) and **frames** (physical)
- Each virtual page maps to a physical frame via a **page table**
- Address translation: page number gives the frame number, offset stays the same

### Advantages over Swapping

- Only unused pages are swapped out, not the entire process
- Process can continue running even with some pages on disk
- Page sharing: multiple virtual pages can point to the same physical frame
- Process memory doesn't need to be contiguous

### Problem

Page tables can become very large - solved by [[Multilevel Page Tables]] and [[Translation Lookaside Buffer|TLBs]].

## Related Concepts

- [[Demand Paging vs Pre-Paging]]: when to load pages into memory
- [[Page Replacement Algorithmen]]: which page to evict when memory is full
- [[Translation Lookaside Buffer]]: caching page table lookups
- [[Thrashing]]: what happens when paging goes wrong
