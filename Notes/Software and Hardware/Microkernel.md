---
title: Microkernel
aliases:
  - Mikrokernel
tags:
  - operating-systems
  - kernel
description: "Kernel architecture that runs most services in user space, keeping only essential functions in the kernel"
draft: false
---

> [!NOTE] Definition
> A microkernel keeps only the most essential services (IPC, basic scheduling, memory management) in kernel mode and moves everything else (drivers, file systems, networking) into user-space processes.

## Characteristics

- Minimal kernel with only core functionality
- Services communicate via Inter-Process Communication (IPC)
- Each service runs in its own isolated address space

## Trade-offs

| Advantage | Disadvantage |
|-----------|-------------|
| Better modularity and isolation | More IPC overhead |
| Higher reliability (faulty service doesn't crash kernel) | More complex communication |
| Easier to extend and maintain | Generally slower than monolithic |
| Better security (smaller attack surface) | |

## Examples

- MINIX, QNX, L4, Mach

## Related Concepts

- [[Monolithischer Kernel]]: the alternative approach running everything in kernel space
- [[Message Passing IPC]]: the communication model microkernels rely on
