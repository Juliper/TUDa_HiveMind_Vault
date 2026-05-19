---
title: Zombie and Orphan Processes
aliases:
  - Zombie und Orphan Prozesse
  - Zombie Process
  - Orphan Process
tags:
  - operating-systems
  - processes
description: "Special process states where a process has terminated without cleanup or lost its parent"
draft: false
---

> [!NOTE] Definition
> A **zombie process** has finished execution but still occupies an entry in the process table. An **orphan process** continues running after its parent has terminated.

## Zombie Process

- Process has called `exit()` or finished, but the parent has not yet called `wait()`
- The PCB entry remains in the process table, wasting resources
- The OS retains the exit status so the parent can retrieve it later
- Fix: parent must call `wait()` to reap the zombie

## Orphan Process

- The parent process has terminated before the child
- The orphan is typically adopted by the `init` process (PID 1)
- `init` periodically calls `wait()` to clean up adopted children

## Related Concepts

- [[Prozesszustände]]: the terminated state that leads to zombies
- [[POSIX Prozessverwaltung]]: `fork()`, `wait()`, and `exit()` that govern these states
