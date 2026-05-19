---
title: Peterson's Solution
aliases:
  - Petersons Solution
  - Peterson-Algorithmus
tags:
  - operating-systems
  - synchronization
description: "A correct software-only solution for mutual exclusion between two processes"
draft: false
---

> [!NOTE] Definition
> Peterson's solution uses a `turn` variable and an `interested` array to correctly solve the critical section problem for two processes without hardware support.

## How It Works

Each process $i$ does:
1. Set `interested[i] = true`
2. Set `turn = i` (give the other process priority)
3. Wait while `interested[other] == true AND turn == i`
4. Enter critical region
5. On exit: set `interested[i] = false`

## Why It's Correct

- If both processes try to enter simultaneously, `turn` can only hold one value
- The process whose `turn` value was overwritten gets to enter first
- Satisfies all four [[Critical Regions|requirements]] for mutual exclusion

## Limitation

- Only works for exactly two processes
- Uses busy-waiting (wastes CPU cycles while spinning)
- Modern CPUs may reorder instructions, breaking correctness without memory barriers

## Related Concepts

- [[Lock-Variablen und Prozess-Alternation]]: the flawed predecessors
- [[Atomare Instruktionen]]: hardware approach that avoids busy-waiting issues
- [[Semaphore und Mutexes]]: general solution for any number of processes
