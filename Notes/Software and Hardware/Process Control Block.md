---
title: Process Control Block
aliases:
  - PCB
tags:
  - operating-systems
  - processes
description: "Data structure containing all information the OS needs to manage a process"
draft: false
---

> [!NOTE] Definition
> The Process Control Block (PCB) stores the current state of a process so that when it is descheduled, it can later resume exactly where it left off.

## Contents

| Field | Purpose |
|-------|---------|
| **Program Counter** | Address of the next instruction to execute |
| **Register Values** | Saved CPU register contents |
| **Process Status** | Current state (ready, running, blocked, etc.) |
| **Stack Pointer** | Points to the top of the process stack |
| **Memory Allocations** | Base address and size of allocated memory |
| **Open Files** | List of files the process has open |
| **Scheduling Info** | Priority, queue placement |
| **Accounting Info** | CPU time used, runtime statistics |

## Role in Context Switching

During a [[Context Switch]]:
1. The PCB of the currently running process is **saved** (registers, PC, etc.)
2. The PCB of the next process is **loaded** into the CPU

This allows the OS to implement [[Prozesszustände|process state transitions]] transparently.

## Related Concepts

- [[Context Switch]]: the operation that saves and restores PCBs
- [[Prozesszustände]]: the states tracked in the PCB
- [[Prozessspeicher und Stackframe]]: what the memory pointers in the PCB reference
