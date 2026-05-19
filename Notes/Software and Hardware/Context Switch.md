---
title: Context Switch
aliases:
  - Kontextwechsel
tags:
  - operating-systems
  - scheduling
description: "The mechanism by which the CPU switches from executing one process to another"
draft: false
---

> [!NOTE] Definition
> A context switch is the process of saving the state of the currently running process and loading the state of the next process to be executed.

## Steps

1. **Save** the [[Process Control Block|PCB]] of the current process (registers, program counter, stack pointer)
2. **Load** the PCB of the next process into the CPU

## When Does It Happen?

- After a clock interrupt (time slice expired)
- When a process blocks (e.g., waiting for I/O)
- When a process terminates
- When a higher-priority process becomes ready (preemption)

## Trade-offs

| Advantage | Disadvantage |
|-----------|-------------|
| Enables [[Scheduling-Metriken|multiprogramming]] | Pure overhead - no useful work during switch |
| Allows pseudo-parallelism | Too many switches degrade performance |
| Fair CPU sharing | Cache and TLB are invalidated |

> [!WARNING]
> Context switches are expensive. The CPU must flush caches and TLB entries, and no useful computation happens during the switch. The OS must balance responsiveness against switching overhead.

## Related Concepts

- [[Process Control Block]]: what gets saved and restored
- [[Preemptive vs Non-preemptive Scheduling]]: determines when switches occur
- [[Interrupts]]: often trigger context switches
