---
title: DBMS Task Scheduling
aliases:
  - Query Task Scheduling
tags:
  - databases
  - parallelism
  - performance
description: "How a DBMS decides which thread executes which task, and how many threads are pinned to which CPU cores"
draft: false
---

> [!NOTE] Definition
> Scheduling is the process of distributing query tasks to worker threads. In a DBMS, the scheduler must decide **how many tasks** to split a query plan into, **which CPU cores** the tasks execute on, and **to which memory region** a task should store its output.

DBMSs typically manage scheduling on their own rather than relying purely on the OS scheduler, since the OS has no visibility into query plan structure or NUMA-aware data placement.

## Task Assignment: Push vs. Pull

| Approach | Mechanism | Control |
|---|---|---|
| **Push** | A centralized dispatcher thread assigns tasks to workers and monitors their progress | Global, centralized control |
| **Pull** | Workers pull tasks from a shared queue (filled by a dispatcher), process them, and return for the next task | Decentralized, worker-driven |

> [!IMPORTANT]
> For very small tasks, the pull model tends to scale better since it avoids the dispatcher becoming a bottleneck, while push gives tighter global control useful for load balancing across heterogeneous task sizes.

## Worker Allocation

| Approach | Description | Trade-off |
|---|---|---|
| **One worker per core** | Each physical core is assigned exactly one pinned thread (`sched_setaffinity` / `pthread_setaffinity_np`) | Predictable, low overhead |
| **Multiple workers per core** | Multiple threads assigned per core, leveraging hyper-threading | Better utilization but higher scheduling overhead |

## Example: Dispatcher Thread (Push Model)

A classic example is a multithreaded web server: a dispatcher thread in user space receives incoming network connections and hands them off to a pool of worker threads that access a shared cache, all within the same process. DBMSs like IBM DB2, MS SQL, MySQL, and SAP HANA use an analogous push-based dispatcher model.

## Related Concepts

- [[DBMS Execution Architecture]]: the multi-threaded model scheduling operates within
- [[Query Parallelism]]: the tasks being scheduled originate from splitting a query plan
- [[NUMA Architecture]]: the scheduler must be NUMA-aware to keep workers on local data
