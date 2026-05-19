---
title: Precise vs Imprecise Interrupts
aliases:
  - Interrupt Precision
tags:
  - operating-systems
  - hardware
description: "Whether an interrupt leaves the CPU in a well-defined state or not"
draft: false
---

> [!NOTE] Definition
> A **precise interrupt** leaves the system in a well-defined state. An **imprecise interrupt** leaves the system in an ambiguous state requiring extra information to recover.

## Precise Interrupts

- The Program Counter is saved
- All instructions before the PC have been fully executed
- No instruction after the PC has been executed
- The execution status of the instruction at the PC is known

## Imprecise Interrupts

- The system is in a non-deterministic state
- Much more information is needed to restore the process state
- Some systems require precise interrupts for correct operation

## Where Process State is Stored

| Location | Problem |
|----------|---------|
| **Internal Registers** | Acknowledgment must be delayed until all states are saved, or they could be overwritten |
| **Process Stack** | Stack pointer might be at the end of a page, causing a page fault |
| **Kernel Stack** | Requires switching to kernel mode (MMU), which invalidates cache and TLB |

## Related Concepts

- [[Interrupts]]: the interrupt mechanism these precision levels apply to
- [[Interrupt-Verarbeitung]]: the full interrupt handling process
