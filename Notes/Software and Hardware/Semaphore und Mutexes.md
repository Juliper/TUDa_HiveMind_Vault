---
title: Semaphores and Mutexes
aliases:
  - Semaphore und Mutexes
tags:
  - operating-systems
  - synchronization
description: "OS-managed synchronization primitives that solve the critical section problem without busy-waiting"
draft: false
---

> [!NOTE] Definition
> Semaphores and mutexes are OS-managed synchronization tools that block waiting processes (putting them to sleep) instead of busy-waiting, making them more efficient than [[Atomare Instruktionen|hardware-level spinning]].

## Semaphore

An integer variable with two atomic operations:
- **down(S)** (P/wait): if $S > 0$, decrement and continue; if $S = 0$, block the calling process
- **up(S)** (V/signal): increment $S$; if blocked processes are waiting, wake one up

A semaphore initialized to 1 acts as a mutual exclusion lock (binary semaphore).

## Mutex

A simplified binary semaphore with only two states: **locked** and **unlocked**. Only the process that locked it can unlock it.

## Condition Variables

Used together with mutexes to wait for a specific condition:
- `wait(cv, mutex)`: release mutex and block until signaled
- `signal(cv)`: wake one waiting process

## Monitor

A higher-level abstraction: a module where only one process can be active at a time. Contains procedures, variables, and condition variables. The compiler enforces mutual exclusion.

## Related Concepts

- [[Critical Regions]]: the problem these primitives solve
- [[Atomare Instruktionen]]: lower-level approach with busy-waiting
- [[Resource Deadlock Conditions]]: improper use of locks can cause deadlocks
