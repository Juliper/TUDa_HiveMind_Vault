---
title: Race Conditions
aliases:
  - Wettlaufsituation
tags:
  - operating-systems
  - synchronization
description: "A bug where the outcome depends on the timing of concurrent processes accessing shared data"
draft: false
---

> [!NOTE] Definition
> A race condition occurs when two or more processes access shared memory concurrently and the final result depends on the order in which their operations execute.

## Example

Two processes increment a shared counter `x = 0`:
1. Process A reads `x = 0`
2. Process B reads `x = 0`
3. Process A writes `x = 1`
4. Process B writes `x = 1`

Result: `x = 1` instead of expected `x = 2`.

## Prevention

Race conditions are prevented by ensuring [[Critical Regions|mutual exclusion]] - only one process can access the shared resource at a time.

## Related Concepts

- [[Critical Regions]]: code sections that must be protected from concurrent access
- [[Semaphore und Mutexes]]: synchronization primitives to prevent races
- [[Shared Memory IPC]]: communication method prone to race conditions
