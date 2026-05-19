---
title: Process vs Program
aliases:
  - Prozess vs Programm
tags:
  - operating-systems
  - processes
description: "The distinction between a static program on disk and its active execution as a process"
draft: false
---

> [!NOTE] Definition
> A **program** is static code and data stored on disk. A **process** is the abstraction of a running program - the unit the OS schedules for execution on the CPU.

## Key Differences

| Aspect | Program | Process |
|--------|---------|---------|
| Nature | Passive (stored on disk) | Active (executing in memory) |
| Lifetime | Permanent until deleted | Temporary (created and terminated) |
| Resources | None | CPU time, memory, open files |
| Instances | One copy | Multiple processes from same program |

## From Program to Process

When a program is launched:
1. OS allocates memory for the process
2. Program code and data are loaded into memory
3. A [[Process Control Block]] is created
4. The process enters the `new` state (see [[Prozesszustände]])
5. The process uses virtual addresses, translated by the MMU via [[Paging und Swapping]]

## Related Concepts

- [[Prozesszustände]]: lifecycle of a process
- [[Prozessspeicher und Stackframe]]: how process memory is organized
- [[POSIX Prozessverwaltung]]: how processes are created in UNIX
