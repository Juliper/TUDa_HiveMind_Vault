---
title: Batch Scheduling Algorithms
aliases:
  - Batch Scheduling
tags:
  - operating-systems
  - scheduling
description: "Non-preemptive scheduling algorithms optimized for throughput and turnaround time"
draft: false
---

> [!NOTE] Definition
> Batch scheduling algorithms are designed for systems without interactive users. They optimize for throughput, CPU utilization, and turnaround time.

## Algorithms

### First-Come-First-Serve (FCFS)
- Non-preemptive
- Processes execute in arrival order
- Simple but unfair: short processes stuck behind long ones ("convoy effect")

### Shortest Job First (SJF)
- Non-preemptive
- Process with the shortest estimated runtime runs next
- Optimal for minimizing average turnaround time
- Requires knowing or estimating job lengths in advance

### Shortest Remaining Time Next (SRTN)
- Preemptive version of SJF
- If a new process arrives with shorter remaining time than the current one, it preempts
- Best average turnaround time, but requires continuous estimation

## Process Runtime Estimation

Since actual runtimes are unknown in advance, the OS estimates using exponential averaging:

$$T_n = \alpha \cdot T_{n-1} + (1 - \alpha) \cdot T_{prev}$$

Where $\alpha$ weights recent behavior against historical averages.

## Related Concepts

- [[Interactive Scheduling]]: algorithms for systems with users
- [[Scheduling-Metriken]]: the metrics these algorithms optimize
- [[Preemptive vs Non-preemptive Scheduling]]: SRTN is preemptive, others are not
