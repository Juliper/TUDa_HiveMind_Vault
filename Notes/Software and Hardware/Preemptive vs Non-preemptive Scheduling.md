---
title: Preemptive vs Non-preemptive Scheduling
aliases:
  - Scheduling Types
tags:
  - operating-systems
  - scheduling
description: "The two fundamental approaches to CPU scheduling - letting processes run to completion or interrupting them"
draft: false
---

> [!NOTE] Definition
> **Non-preemptive** scheduling lets a process run until it blocks, terminates, or voluntarily yields. **Preemptive** scheduling can interrupt a running process via clock interrupts to give the CPU to another process.

## Comparison

| Aspect | Non-preemptive | Preemptive |
|--------|---------------|------------|
| Interruption | Process runs until done/blocked | Process can be interrupted at any time |
| Fairness | Low (long processes monopolize CPU) | High (time slices ensure sharing) |
| Overhead | Low (fewer context switches) | Higher (frequent context switches) |
| Responsiveness | Poor | Good |
| Use case | [[Batch Scheduling]] | [[Interactive Scheduling]] |

## When Is Scheduling Needed?

- `fork()`: should parent or child run first?
- Process terminates: which process runs next?
- Process blocks (I/O wait): switch to which process?
- Interrupt occurs: continue current process or switch?

## Related Concepts

- [[Context Switch]]: the mechanism that enables preemption
- [[Interrupts]]: clock interrupts trigger preemptive scheduling
- [[Scheduling-Metriken]]: how to evaluate each approach
