---
title: Process Memory Layout
aliases:
  - Prozessspeicher und Stackframe
  - Process Memory
  - Stack Frame
tags:
  - operating-systems
  - processes
  - memory
description: "How a process's virtual memory is organized into text, data, heap, and stack segments"
draft: false
---

> [!NOTE] Definition
> Each process has its own virtual address space divided into distinct segments with different purposes and growth directions.

## Memory Layout

```
High Address
+---------------------------+
|        Stack              |  <- grows downward
|    (dynamic size)         |
+---------------------------+
|           |               |
|           v               |
|                           |
|           ^               |
|           |               |
+---------------------------+
|        Heap               |  <- grows upward
|    (dynamic size)         |
+---------------------------+
|        BSS                |  <- uninitialized globals
+---------------------------+
|        Data               |  <- initialized globals, constants
+---------------------------+
|        Text               |  <- program code (read-only)
+---------------------------+
Low Address
```

| Segment | Contents | Growth |
|---------|----------|--------|
| **Text** | Program code (instructions) | Fixed |
| **Data** | Initialized global variables, constants | Fixed |
| **BSS** | Uninitialized global variables | Fixed |
| **Heap** | Dynamically allocated memory (objects, `malloc`) | Upward |
| **Stack** | Local variables, return addresses, function parameters | Downward |

## Stack Frames

The stack is divided into **frames**, one per function call. Each frame contains:
- Function arguments
- Return address
- Base pointer (frame pointer to the calling function)
- Local variables

> [!IMPORTANT]
> Processes use virtual addresses that must be translated to physical addresses by the MMU. This is done via [[Paging und Swapping|paging]].

## Related Concepts

- [[Process Control Block]]: stores the stack pointer and memory info
- [[Paging und Swapping]]: how virtual addresses map to physical memory
