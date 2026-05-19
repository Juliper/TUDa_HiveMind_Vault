---
title: Operating System Functions
aliases:
  - Aufgaben eines Betriebssystems
  - OS Functions
tags:
  - operating-systems
description: "Core responsibilities of an operating system - abstraction, resource management, and hardware access control"
draft: false
---

> [!NOTE] Definition
> An operating system is software that manages other programs and provides them with simplified access to hardware. It acts as the interface between software and hardware.

## Why Do We Need an Operating System?

- **Abstraction**: Simplifies hardware access into uniform requests, enabling programs to run on different machines
- **Access Control**: Secures hardware access against critical interference (e.g., disk scans)
- **Resource Management**: Ensures running programs are treated fairly or prioritized according to policy, and prevents conflicts like simultaneous writes to the same address

## Fundamental Concepts

An OS is built around three pillars:

| Pillar | Examples |
|--------|----------|
| **Abstractions** | Files, processes, devices, virtual memory |
| **Mechanisms** | Open, close, create, execute, fork |
| **Policies** | Execution order, memory allocation strategy |

## Memory Hierarchy

The OS must manage multiple storage tiers. Higher tiers are faster but smaller and more expensive:

1. **Registers** - fastest, smallest
2. **Cache** - L1/L2/L3
3. **Main Memory (RAM)**
4. **Secondary Storage** (HDD/SSD)

## Related Concepts

- [[x86 Schutzringe]]: how the CPU enforces privilege levels
- [[System Calls]]: how user programs request OS services
- [[Monolithischer Kernel]]: one approach to OS architecture
- [[Microkernel]]: the alternative modular approach
