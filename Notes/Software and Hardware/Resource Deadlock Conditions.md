---
title: Resource Deadlock Conditions
aliases:
  - Coffman Conditions
  - Deadlock-Bedingungen
tags:
  - operating-systems
  - synchronization
  - deadlocks
description: "The four conditions that must hold simultaneously for a resource deadlock to occur"
draft: false
---

> [!NOTE] Definition
> A resource deadlock occurs when concurrent processes block each other indefinitely, each waiting for a resource held by another. All four Coffman conditions must hold simultaneously.

## The Four Conditions

1. **Mutual Exclusion**: Each resource is either assigned to exactly one process or is free
2. **Hold and Wait**: Processes holding resources can request additional ones
3. **No Pre-emption**: Resources cannot be forcibly taken from a process
4. **Circular Wait**: A circular chain of processes exists, each waiting for a resource held by the next

## Resource Types

| Type | Description | Example |
|------|-------------|---------|
| **Preemptable** | Can be taken from a process without negative consequences | Memory (can be swapped) |
| **Non-preemptable** | Cannot be taken without causing problems | Printer, CD burner |

> [!IMPORTANT]
> Breaking any one of the four conditions prevents deadlocks. This is the basis for all [[Deadlock-Strategien|deadlock prevention and avoidance strategies]].

## Related Concepts

- [[Deadlock-Strategien]]: how to prevent, avoid, detect, and recover from deadlocks
- [[Bankers Algorithmus]]: algorithm for deadlock avoidance
- [[Semaphore und Mutexes]]: improper use can create deadlocks
