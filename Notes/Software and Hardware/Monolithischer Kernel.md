---
title: Monolithic Kernel
aliases:
  - Monolithischer Kernel
tags:
  - operating-systems
  - kernel
description: "Kernel architecture where all OS services run in a single address space in kernel mode"
draft: false
---

> [!NOTE] Definition
> A monolithic kernel runs all operating system services (file systems, drivers, networking, scheduling) in a single large process in kernel mode (Ring 0).

## Characteristics

- All services share the same address space
- Internal function calls between components (no IPC overhead)
- A bug in any component can crash the entire system

## Trade-offs

| Advantage | Disadvantage |
|-----------|-------------|
| Better performance (no IPC overhead) | Lower reliability (single fault crashes all) |
| Simpler internal communication | Harder to maintain and extend |
| Direct hardware access for all components | Larger attack surface |

## Examples

- Linux, FreeBSD, classic UNIX

## Related Concepts

- [[Microkernel]]: the alternative approach that moves services to user space
- [[x86 Schutzringe]]: the hardware privilege model that kernels rely on
