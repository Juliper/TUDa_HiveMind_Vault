---
title: Real-Time Scheduling
aliases:
  - Realtime Scheduling
tags:
  - operating-systems
  - scheduling
description: "Scheduling for systems with strict timing constraints where predictability is critical"
draft: false
---

> [!NOTE] Definition
> Real-time scheduling is used in systems where meeting deadlines is critical (e.g., multimedia, industrial control). The scheduler must guarantee predictable timing behavior.

## Types

| Type | Constraint |
|------|-----------|
| **Hard real-time** | Missing a deadline is a system failure (e.g., airbag, pacemaker) |
| **Soft real-time** | Missing a deadline degrades quality but isn't fatal (e.g., video streaming) |

## Key Requirements

- Deterministic execution times
- Predictable scheduling behavior
- Low interrupt latency
- Guaranteed response times

## Related Concepts

- [[Batch Scheduling]]: optimizes throughput, not deadlines
- [[Interactive Scheduling]]: optimizes response time but without hard guarantees
- [[Interrupts]]: real-time systems need precise interrupt handling
