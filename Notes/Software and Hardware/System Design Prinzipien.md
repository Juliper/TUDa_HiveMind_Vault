---
title: OS Design Principles
aliases:
  - System Design Prinzipien
tags:
  - operating-systems
description: "The three pillars of operating system design - abstractions, mechanisms, and policies"
draft: false
---

> [!NOTE] Definition
> Operating system design is structured around three layers: abstractions that hide complexity, mechanisms that implement operations, and policies that govern decisions.

## The Three Pillars

### Abstractions
Hide hardware complexity behind uniform interfaces:
- Processes, Threads
- Files, Directories
- Virtual Memory
- Devices

### Mechanisms
Concrete operations the OS provides:
- `open()`, `close()`, `read()`, `write()`
- `fork()`, `exec()`, `kill()`
- `create()`, `delete()`

### Policies
Rules that govern how mechanisms are applied:
- Scheduling order (which process runs next?)
- Memory allocation strategy (how is RAM divided?)
- I/O prioritization

> [!IMPORTANT]
> The separation of mechanism and policy is a key design principle. Mechanisms should be general-purpose; policies should be configurable without changing mechanisms.

## Related Concepts

- [[Aufgaben eines Betriebssystems]]: what the OS must accomplish
- [[Allocation-Strategien]]: an example of memory policies
