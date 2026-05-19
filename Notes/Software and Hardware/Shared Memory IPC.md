---
title: Shared Memory IPC
aliases:
  - Shared Memory
tags:
  - operating-systems
  - ipc
description: "Inter-process communication method where processes share a region of virtual memory"
draft: false
---

> [!NOTE] Definition
> Shared memory IPC allows processes to communicate by reading and writing to a shared region of virtual memory, without involving the OS for each transfer.

## How It Works

- The OS sets up a shared memory region accessible by multiple processes
- After setup, processes communicate directly without syscalls
- Processes must handle synchronization themselves (e.g., using [[Semaphore und Mutexes]])

## Trade-offs

| Advantage | Disadvantage |
|-----------|-------------|
| Very fast (no OS involvement after setup) | Requires synchronization |
| No data copying needed | Only works on the same machine |
| Efficient for large data transfers | Risk of [[Race Conditions]] |

## Related Concepts

- [[Message Passing IPC]]: the OS-managed alternative
- [[Race Conditions]]: the primary risk with shared memory
- [[Critical Regions]]: code sections that access shared memory
