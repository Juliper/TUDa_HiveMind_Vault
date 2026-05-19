---
title: Multithreading Models
aliases:
  - Multithreading-Modelle
  - Thread Mapping Models
tags:
  - operating-systems
  - threads
description: "The three models for mapping user-level threads to kernel-level threads"
draft: false
---

> [!NOTE] Definition
> Multithreading models define how user-level threads are mapped to kernel-level threads.

## The Three Models

### Many-to-One
- Many user threads map to **one** kernel thread
- Thread management is efficient (done in user space)
- One blocking call blocks all threads
- Cannot use multiple CPUs

### One-to-One
- Each user thread maps to **one** kernel thread
- True parallelism on multi-core systems
- Blocking one thread doesn't affect others
- Creating threads is more expensive (kernel involvement)
- Used by Linux and Windows

### Many-to-Many
- Many user threads map to **many** kernel threads (multiplexing)
- Flexible: OS can create enough kernel threads for the hardware
- Most complex to implement

```mermaid
graph TD
    subgraph "Many-to-One"
        U1[User Thread] --> K1[Kernel Thread]
        U2[User Thread] --> K1
        U3[User Thread] --> K1
    end
```

## Related Concepts

- [[User-Level vs Kernel-Level Threads]]: the building blocks of these models
- [[Linux vs Windows Prozessmodell]]: how real OSes implement threading
