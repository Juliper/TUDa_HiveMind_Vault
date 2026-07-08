---
title: Instruction-Level Parallelism
aliases:
  - Superscalar CPU
  - Subscalar CPU
  - ILP
tags:
  - hardware
  - computer-architecture
  - performance
description: "How CPUs overlap and issue multiple instructions per clock cycle to extract parallelism from a sequential instruction stream"
draft: false
---

> [!NOTE] Definition
> Instruction-Level Parallelism (ILP) is the degree to which a CPU can execute multiple instructions simultaneously, moving beyond a purely sequential ("subscalar") execution model.

## Subscalar CPU

A subscalar CPU has **no implicit parallelism**: it executes one instruction at a time, taking one instruction through fetch, decode, execute, memory, and write-back stages before starting the next.

```
instr1: fetch decode execute mem write
instr2:                          fetch decode execute mem write
```

Several cycles are needed to complete even two instructions, assuming no long-latency memory accesses.

## Superscalar CPU

A superscalar CPU issues **multiple instructions per clock cycle** by duplicating execution resources and pipelining instruction stages, so several instructions are in different stages simultaneously.

```
instr1: fetch decode execute mem write
instr2: fetch decode execute mem write
instr3: fetch decode execute mem write
instr4: fetch decode execute mem write
```

A "4-way superscalar" CPU can have up to 4 instructions in flight concurrently across its pipeline stages.

> [!IMPORTANT]
> Modern processors' **Hyper-Threading** feature relies on superscalar execution at its core: by interleaving instructions from two logical threads, it fills execution slots that a single thread would otherwise leave idle.

## Where the Silicon Goes

Examining a real CPU die (e.g., AMD Ryzen 5 2600) shows that a large fraction of the chip is dedicated to caches (L1, L2), decode logic, the scheduler, and branch prediction (BPU) - with the actual compute units (FPU, ALU) occupying comparatively little area. This reflects the CPU's design goal of working well for **any** application rather than maximizing raw throughput for one workload, which is why [[Hardware Specialization Spectrum|specialized hardware]] can achieve much higher efficiency for narrower workloads.

## Related Concepts

- [[Von Neumann Architecture]]: the sequential instruction model ILP techniques work around
- [[Hardware Specialization Spectrum]]: CPUs trade raw compute density for this general-purpose flexibility
- [[Pipelining]]: the underlying circuit-level technique (temporal parallelism) superscalar execution builds on
