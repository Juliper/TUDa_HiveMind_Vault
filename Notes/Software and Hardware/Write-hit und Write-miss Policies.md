---
title: Cache Write Policies
aliases:
  - Write-hit und Write-miss Policies
  - Write-through
  - Write-back
tags:
  - operating-systems
  - hardware
  - memory
description: "How CPU caches handle write operations - write-through vs write-back and write-allocate vs no-write-allocate"
draft: false
---

> [!NOTE] Definition
> Write policies determine how the cache handles writes - both when the target is already cached (hit) and when it is not (miss).

## Write-Hit Policies

| Policy | Description |
|--------|-------------|
| **Write-through** | Write to both cache and main memory simultaneously. Simple but slower. |
| **Write-back** | Write only to cache; main memory is updated when the cache line is evicted. Faster but more complex. |

## Write-Miss Policies

| Policy | Description |
|--------|-------------|
| **Write-allocate** | Load the block into cache on a miss, then write to it. Common with write-back. |
| **No-write-allocate** | Write directly to main memory without loading into cache. Common with write-through. |

## Related Concepts

- [[Cache-Eigenschaften]]: overall cache organization
- [[Page Table Entries]]: the dirty bit tracks whether a page has been written (similar concept)
