---
title: Atomic Instructions
aliases:
  - Atomare Instruktionen
  - Test-and-Set
tags:
  - operating-systems
  - synchronization
  - hardware
description: "Hardware-level instructions that perform read-modify-write operations atomically for mutual exclusion"
draft: false
---

> [!NOTE] Definition
> Atomic instructions are CPU instructions that perform a read-modify-write operation in a single, uninterruptible step, enabling correct mutual exclusion without software-only algorithms.

## Common Atomic Instructions

| Instruction | Description |
|-------------|-------------|
| **Test-and-Set** | Reads a memory location, returns the old value, and sets it to 1 - all atomically |
| **Compare-and-Swap (CAS)** | Compares memory with expected value; if equal, swaps in the new value |
| **Fetch-and-Add** | Atomically adds a value and returns the previous value |

## Usage for Mutual Exclusion

```
while (test_and_set(&lock) == 1) {
    // busy wait (spin)
}
// critical region
lock = 0;
```

## Trade-offs

| Advantage | Disadvantage |
|-----------|-------------|
| Correct and simple | Still uses busy-waiting |
| Works for any number of processes | Wastes CPU cycles while spinning |
| Hardware-guaranteed atomicity | Priority inversion possible |

## Related Concepts

- [[Petersons Solution]]: software-only approach for two processes
- [[Semaphore und Mutexes]]: OS-managed approach that avoids busy-waiting
- [[Critical Regions]]: what these instructions protect
