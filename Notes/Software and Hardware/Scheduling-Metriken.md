---
title: Scheduling Metrics
aliases:
  - Scheduling-Metriken
tags:
  - operating-systems
  - scheduling
description: "Key metrics for evaluating CPU scheduling algorithms - turnaround time, response time, and utilization"
draft: false
---

> [!NOTE] Definition
> Scheduling metrics quantify how well a scheduling algorithm performs. The OS aims to optimize different metrics depending on the system type.

## Core Metrics

| Metric | Formula | Goal |
|--------|---------|------|
| **Turnaround Time** | $T_{end} - T_{submit}$ (includes all waiting) | Minimize |
| **Response Time** | $T_{first\_output} - T_{submit}$ | Minimize |
| **Wait Time** | Sum of all time spent in ready queue | Minimize |
| **CPU Utilization** | $u = 1 - p^n$ | Maximize |
| **Throughput** | Completed processes per time unit | Maximize |

Where $p$ = fraction of time a process waits for I/O, $n$ = number of processes.

## Scheduling Goals

| Goal | Description |
|------|-------------|
| Fairness | Every process gets its fair share |
| Policy enforcement | Priorities are respected |
| Proportionality | Small jobs finish quickly, large jobs can wait |

## Process Types

- **CPU-bound**: Most time spent computing (benefits from long time slices)
- **I/O-bound**: Most time spent waiting for I/O (benefits from frequent scheduling)

> [!IMPORTANT]
> Multiprogramming improves CPU utilization because I/O-bound processes can be swapped out while waiting, letting CPU-bound processes run.

## Related Concepts

- [[Batch Scheduling]]: optimizes turnaround time and throughput
- [[Interactive Scheduling]]: optimizes response time
- [[Preemptive vs Non-preemptive Scheduling]]: fundamental scheduling approach
