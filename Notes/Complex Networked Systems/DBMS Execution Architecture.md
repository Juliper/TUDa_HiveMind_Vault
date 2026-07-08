---
title: DBMS Execution Architecture
aliases:
  - Multi-Threaded vs Multi-Process DBMS
tags:
  - databases
  - parallelism
  - performance
description: "The choice between a multi-threaded and a multi-process architecture for executing parallel work inside a DBMS"
draft: false
---

> [!NOTE] Definition
> A DBMS must choose between a **multi-threaded architecture**, where workers share one process's memory space, and a **multi-process architecture**, where each worker is a separate OS process.

## Comparison

| | Multi-Threaded | Multi-Process |
|---|---|---|
| **Memory** | Shared address space between threads | Separate address space per process |
| **Context switch overhead** | Lower | Higher |
| **Communication** | Direct via shared memory | Requires IPC (pipes, shared memory segments) |
| **Fault isolation** | Poor - a single thread crash can bring down the whole DBMS process | Good - one process crashing does not affect others |
| **Typical use** | Single-node DBMSs | One process per node in a distributed DBMS |

## Per-Process vs. Per-Thread State

| Per-Process Items | Per-Thread Items |
|---|---|
| Address space | Program counter |
| Global variables | Registers |
| Open files | Stack |
| Child processes | State |
| Pending alarms | |
| Signals and signal handlers | |
| Accounting information | |

## Why This Matters

Because threads share the same address space, most single-node, in-memory DBMSs (e.g., IBM DB2, MS SQL, MySQL, Oracle, SAP HANA) use a multi-threaded architecture for lower overhead per task. Distributed DBMSs typically combine both: one process per node (multi-process), with each node internally using a multi-threaded architecture to parallelize work across its local cores.

## Related Concepts

- [[Query Parallelism]]: the workload this architecture must support
- [[DBMS Task Scheduling]]: how work is distributed to threads within this architecture
- [[Context Switch]]: the overhead difference between threads and processes stems from this
