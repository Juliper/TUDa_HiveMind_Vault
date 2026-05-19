---
title: POSIX Process Management
aliases:
  - POSIX Prozessverwaltung
tags:
  - operating-systems
  - processes
  - unix
description: "UNIX system calls for creating, executing, and managing processes"
draft: false
---

> [!NOTE] Definition
> POSIX defines a standard set of system calls for process management in UNIX-like systems.

## Core System Calls

| Syscall | Description |
|---------|-------------|
| `fork()` | Creates a copy of the calling process. Returns 0 in the child, the child's PID in the parent, negative on error |
| `exec()` | Loads a new program into the current process and starts executing it |
| `exit()` | Terminates the current process |
| `wait()` | Parent blocks until a child process terminates |
| `kill()` | Sends a signal to a process (can cause termination) |

## Typical Process Creation Flow

```mermaid
sequenceDiagram
    participant P as Parent
    participant C as Child
    P->>P: fork()
    P->>C: Child created (copy of parent)
    C->>C: exec() - load new program
    P->>P: wait() - block until child exits
    C->>C: exit() - child terminates
    C->>P: Parent unblocked
```

## Related Concepts

- [[System Calls]]: the general mechanism these calls use
- [[Prozesszustände]]: the states processes transition through
- [[Zombie und Orphan Prozesse]]: what happens when `wait()` is not called
