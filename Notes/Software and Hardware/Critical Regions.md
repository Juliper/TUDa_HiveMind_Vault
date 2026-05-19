---
title: Critical Regions
aliases:
  - Critical Section
  - Kritischer Abschnitt
tags:
  - operating-systems
  - synchronization
description: "Code sections that access shared resources and must be executed by only one process at a time"
draft: false
---

> [!NOTE] Definition
> A critical region (critical section) is a segment of code that accesses shared variables, memory, or files. Mutual exclusion must ensure only one process executes its critical region at a time.

## Requirements for a Correct Solution

1. **Mutual exclusion**: No two processes simultaneously in their critical regions
2. **No speed assumptions**: No assumptions about CPU speeds or count
3. **No external blocking**: No process outside its critical region may block others
4. **No starvation**: No process waits forever to enter its critical region

## Solutions (Simplest to Most Sophisticated)

| Approach | Description | Problem |
|----------|-------------|---------|
| Disable interrupts | Prevent context switches inside critical region | Only works on single CPU, dangerous |
| [[Lock-Variablen und Prozess-Alternation\|Lock variables]] | Shared flag indicating occupancy | Race condition on the flag itself |
| [[Lock-Variablen und Prozess-Alternation\|Strict alternation]] | Turn variable alternates access | Violates requirement 3 |
| [[Petersons Solution]] | Turn + interest flags | Correct but busy-waiting |
| [[Atomare Instruktionen]] | Hardware-level atomic operations | Busy-waiting |
| [[Semaphore und Mutexes]] | OS-managed synchronization | Best general solution |

## Related Concepts

- [[Race Conditions]]: what happens without proper critical region protection
- [[Resource Deadlock Conditions]]: what can happen if synchronization is mismanaged
