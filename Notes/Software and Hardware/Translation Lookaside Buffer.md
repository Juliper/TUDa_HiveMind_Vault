---
title: Translation Lookaside Buffer
aliases:
  - TLB
tags:
  - operating-systems
  - memory-management
  - paging
description: "Hardware cache in the MMU that stores recent virtual-to-physical address mappings for fast lookup"
draft: false
---

> [!NOTE] Definition
> The TLB is a small, fast cache inside the Memory Management Unit (MMU) that stores recently used page table entries to speed up address translation.

## Why It's Needed

Without a TLB, every memory access requires at least one additional memory access to read the page table. With [[Multilevel Page Tables]], this could mean 2-4 extra accesses per lookup.

## How It Works

1. CPU generates a virtual address
2. MMU checks the TLB for a matching entry
3. **TLB Hit**: physical frame number is returned immediately
4. **TLB Miss**: page table is consulted, and the result is cached in the TLB

> [!IMPORTANT]
> During a [[Context Switch]], the TLB typically needs to be flushed since the new process has a different page table, which contributes to the cost of context switching.

## Related Concepts

- [[Paging und Swapping]]: the page table the TLB caches
- [[Multilevel Page Tables]]: multi-level lookups that make the TLB even more critical
- [[Context Switch]]: invalidates TLB entries
