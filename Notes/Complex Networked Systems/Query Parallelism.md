---
title: Query Parallelism
aliases:
  - Inter-Query Parallelism
  - Intra-Query Parallelism
tags:
  - databases
  - parallelism
  - performance
description: "The two forms of parallel query execution in a DBMS, distinguished by whether they parallelize across queries or within a single query"
draft: false
---

> [!NOTE] Definition
> A DBMS can exploit parallel hardware in two distinct ways: **inter-query parallelism** executes multiple queries concurrently, while **intra-query parallelism** splits a single query into parallel tasks.

## Inter-Query vs. Intra-Query

| | Inter-Query Parallelism | Intra-Query Parallelism |
|---|---|---|
| **Unit of parallelism** | Multiple independent queries | Operators/tasks within one query |
| **Goal** | Increase throughput | Decrease response time of a single query |
| **Workload** | Important for **OLTP** (many short queries) | Important for **OLAP** (few large, expensive queries) |

## Intra-Query Parallelism: Intra-Operator vs. Inter-Operator

Intra-query parallelism can further be split by which part of the query plan is parallelized:

- **Intra-operator parallelism** - the same operator (e.g., a scan or join) is executed by multiple threads on different partitions of its input
- **Inter-operator parallelism** - different operators in the query plan execute concurrently, e.g. via pipelining

## General Idea: Tasks

A query plan is decomposed into smaller **tasks** that can be executed in parallel on multiple cores, enabling both inter- and intra-query parallelism simultaneously. For example, `SELECT A.id, B.value FROM A, B WHERE A.id = B.id AND A.value < 99 AND B.value > 100` can be split so that the two `σ` (select) operators on A and B run as independent tasks before the join.

## Related Concepts

- [[DBMS Execution Architecture]]: the threading/process model that executes these tasks
- [[DBMS Task Scheduling]]: how tasks are assigned to workers
- [[Partition-Based Hash Join]]: a concrete example of intra-operator parallelism
