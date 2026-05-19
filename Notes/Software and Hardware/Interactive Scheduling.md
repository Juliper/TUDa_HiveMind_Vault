---
title: Interactive Scheduling Algorithms
aliases:
  - Interactive Scheduling
tags:
  - operating-systems
  - scheduling
description: "Preemptive scheduling algorithms designed for systems with users waiting for responses"
draft: false
---

> [!NOTE] Definition
> Interactive scheduling algorithms prioritize response time and fairness, using time slices to ensure all processes get CPU access.

## Algorithms

### Round Robin
- Each process gets a fixed time slice (**quantum**)
- After the quantum expires, the process goes to the back of the queue
- Fair but quantum size is critical: too small = too much context switching, too large = poor responsiveness

### Priority Scheduling
- Processes with higher priority run first
- Variant: each priority class gets a time slice proportional to its priority
- Aging: increase priority of processes that haven't run for a long time to prevent starvation

### Multiple Queues
- Multiple priority queues with decreasing time quanta
- Processes start in the highest queue and are **demoted** after running once
- Ensures short interactive jobs finish quickly

### Lottery Scheduling
- Each process gets tickets; a random ticket is drawn to select the next process
- More tickets = higher chance of being selected
- Processes that don't get scheduled accumulate more tickets

### Fair-Share Scheduling
- Each user gets a guaranteed fraction of CPU time, regardless of how many processes they have
- Ensures fairness across users, not just processes

## Related Concepts

- [[Batch Scheduling]]: algorithms for non-interactive systems
- [[Scheduling-Metriken]]: response time is the key metric here
- [[Context Switch]]: happens at every quantum expiry in Round Robin
