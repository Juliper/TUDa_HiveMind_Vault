---
title: User-Level vs Kernel-Level Threads
aliases:
  - Thread Types
tags:
  - operating-systems
  - threads
description: "Comparison of threads managed in user space versus threads managed by the OS kernel"
draft: false
---

> [!NOTE] Definition
> Threads can be managed either entirely in user space (invisible to the OS) or by the kernel itself, each with different trade-offs.

## Comparison

| Aspect | User-Level Threads | Kernel-Level Threads |
|--------|-------------------|---------------------|
| Management | Thread library in user space | OS kernel |
| Thread table | One per process | One global table in kernel |
| Switching speed | Very fast (no kernel involvement) | Slower (requires kernel mode switch) |
| OS awareness | OS sees only the process | OS can schedule individual threads |
| Blocking syscalls | Block the entire process | Only block the calling thread |
| Portability | OS-independent | OS-dependent |

## Thread Properties

Threads within the same process share:
- Address space (code, data, heap)
- Open files and resources

Each thread has its own:
- Program counter
- Register values
- Stack

> [!IMPORTANT]
> User-level threads cannot take advantage of multiple CPUs since the OS doesn't know about them. If one thread makes a blocking syscall, all threads in that process are blocked.

## Related Concepts

- [[Multithreading-Modelle]]: how user and kernel threads are mapped
- [[Context Switch]]: cheaper for threads than for processes
