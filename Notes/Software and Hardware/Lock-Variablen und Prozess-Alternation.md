---
title: Lock Variables and Process Alternation
aliases:
  - Lock-Variablen und Prozess-Alternation
  - Strict Alternation
tags:
  - operating-systems
  - synchronization
description: "Simple but flawed approaches to mutual exclusion using shared variables"
draft: false
---

> [!NOTE] Definition
> Lock variables and strict alternation are simple attempts at solving the [[Critical Regions|critical section problem]], but both have fundamental flaws.

## Lock Variables

- A shared variable (e.g., `lock = 0`) indicates whether the critical region is occupied
- Before entering: check if `lock == 0`, then set `lock = 1`
- **Problem**: the check-and-set is not atomic - two processes can both read `lock == 0` before either sets it to 1, creating a [[Race Conditions|race condition]] on the lock itself

## Strict Alternation (Turn Variable)

- A `turn` variable indicates which process may enter the critical region
- Process $i$ waits while `turn != i`, then enters
- After exiting, sets `turn` to the other process
- **Problem**: violates the "no external blocking" requirement - if one process is much slower or doesn't need the critical region, the other is blocked anyway

## Related Concepts

- [[Petersons Solution]]: combines both approaches correctly
- [[Atomare Instruktionen]]: hardware solution to the atomic check-and-set problem
- [[Critical Regions]]: the problem these approaches try to solve
