---
title: Linux vs Windows Process Model
aliases:
  - Linux vs Windows Prozessmodell
tags:
  - operating-systems
  - processes
  - threads
description: "How Linux and Windows differ in their implementation of processes and threads"
draft: false
---

> [!NOTE] Definition
> Windows explicitly separates processes and threads, while Linux unifies them as tasks with configurable resource sharing.

## Comparison

| Aspect | Linux | Windows |
|--------|-------|---------|
| Basic unit | Task | Process + Thread |
| Thread concept | Implicit via `clone()` flags | Explicit thread objects |
| Creation syscall | `clone()` with sharing flags | `CreateProcess()` / `CreateThread()` |
| Thread mapping | One-to-one | One-to-one |

## Linux Tasks

In Linux, `clone()` creates a new task. The flags passed to `clone()` determine which resources are shared:
- Share address space = thread-like behavior
- Separate address space = process-like behavior

This means Linux doesn't have a formal thread abstraction at the kernel level - threads are simply tasks that share resources.

## Related Concepts

- [[Multithreading-Modelle]]: both use one-to-one mapping
- [[POSIX Prozessverwaltung]]: the POSIX API used on Linux
