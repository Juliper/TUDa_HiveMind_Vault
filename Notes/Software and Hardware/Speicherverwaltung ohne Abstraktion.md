---
title: Memory Management Without Abstraction
aliases:
  - Speicherverwaltung ohne Abstraktion
  - No Memory Abstraction
tags:
  - operating-systems
  - memory-management
description: "The simplest memory model where processes directly use physical addresses"
draft: false
---

> [!NOTE] Definition
> Without memory abstraction, processes access physical memory directly. Only one process can reside in memory at a time.

## Problems

- Only one process in memory at a time (unless swapping is used)
- Absolute addresses break when multiple processes are loaded at different positions - jumps and references no longer point to the correct locations

## Static Relocation

A provisional solution: before execution, all addresses in the program are rewritten by adding the size of previously loaded processes.

**Drawbacks:**
- Slows down program loading
- Finding and modifying all addresses is error-prone and complex

> [!IMPORTANT]
> This approach is only viable for very simple systems. Modern OSes use [[Fixed Partitions]], [[Variable Partitions]], or [[Paging und Swapping|virtual memory]] instead.

## Related Concepts

- [[Fixed Partitions]]: first step toward memory abstraction
- [[Segmentierung]]: more flexible memory abstraction
- [[Paging und Swapping]]: the modern solution using virtual addresses
