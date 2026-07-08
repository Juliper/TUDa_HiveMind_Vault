---
title: Tensor Processing Unit
aliases:
  - TPU
tags:
  - hardware
  - machine-learning
  - performance
description: "Google's custom ASIC accelerator for neural network inference and training, built around a systolic array matrix-multiply unit"
draft: false
---

> [!NOTE] Definition
> The Tensor Processing Unit (TPU) is a custom [[Application-Specific Integrated Circuit|ASIC]] developed by Google specifically to accelerate neural network training and inference, using a [[Systolic Array]] as its core matrix-multiplication unit.

## Motivation

Google built the TPU after projecting that serving voice search to users for just 3 minutes a day using speech-recognition deep neural networks (DNNs) would require doubling their datacenter capacity - prohibitively expensive with conventional CPUs. The goal was a 10x improvement in cost-performance over GPUs for inference workloads (GPUs were kept for training).

## Die Layout: TPU vs. General-Purpose Processor

| Component | CPU/GPU | TPU |
|---|---|---|
| **Compute** | Small fraction | ~30% |
| **Data buffers/cache** | Large fraction, dominant | ~37% |
| **Control** | Large and complex (branch prediction, scheduling) | Only ~2%, much simpler |
| **I/O** | Moderate | ~10% |

Because control logic is both smaller and much easier to design in the TPU, more of the chip area and power budget goes directly to compute and data movement - the same insight that motivates [[Hardware Specialization Spectrum|specialization]] in general.

## Measured Efficiency

| Hardware | Performance/Watt (relative) |
|---|---|
| CPU | 1x (baseline) |
| GPU | 2.9x |
| TPU | 83x |

The TPU beats CPUs by 83x and GPUs by roughly 28x in performance-per-watt for its target workload.

## Programming Model

TPUs are programmed through the TensorFlow library, with the entire management stack (scheduling, memory management, low-level kernel drivers) hidden from the application developer behind a `StreamExecutor API`.

> [!IMPORTANT]
> Specialized hardware does not exist in a vacuum - it must be integrated with the rest of the software stack (compilers, drivers, frameworks) to be usable. This integration burden is often called the "Achilles heel" of research accelerator projects that never reach production use, since a fast chip without a usable software stack has limited real-world impact.

## Related Concepts

- [[Systolic Array]]: the core computational structure inside the TPU's matrix-multiply unit
- [[Application-Specific Integrated Circuit]]: the general category the TPU belongs to
- [[Hardware Specialization Spectrum]]: the TPU sits at the highest-efficiency, lowest-flexibility end of this spectrum
