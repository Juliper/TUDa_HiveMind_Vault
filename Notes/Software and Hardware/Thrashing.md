---
title: Thrashing
aliases:
  - Seitenflattern
tags:
  - operating-systems
  - memory-management
  - paging
description: "A pathological state where the system spends more time paging than doing useful work"
draft: false
---

> [!NOTE] Definition
> Thrashing occurs when a process's working set is larger than the available physical page frames, causing constant page faults as evicted pages are immediately needed again.

## What Happens

1. Working set exceeds available memory
2. Pages that are evicted are needed again almost immediately
3. This triggers more page faults, evicting other needed pages
4. The cycle continues indefinitely - the CPU is busy handling page faults instead of running processes

## Load Control

When the combined working sets of all processes exceed total main memory, thrashing affects the entire system.

**Solutions:**
- Add more physical memory
- Swap out entire processes until thrashing stops
- Reduce the degree of multiprogramming

> [!WARNING]
> Thrashing can bring a system to a near-halt. The only real solution is to ensure processes have enough physical memory for their working sets.

## Related Concepts

- [[Page Replacement Algorithmen]]: working set algorithms try to prevent thrashing
- [[Paging und Swapping]]: the mechanism that fails under thrashing
