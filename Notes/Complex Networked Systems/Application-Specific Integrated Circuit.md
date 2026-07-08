---
title: Application-Specific Integrated Circuit
aliases:
  - ASIC
  - Dedicated Hardware
tags:
  - hardware
  - performance
description: "A chip fabricated with fixed circuitry designed for exactly one workload, offering the highest possible energy efficiency at the cost of all flexibility"
draft: false
---

> [!NOTE] Definition
> An Application-Specific Integrated Circuit (ASIC) is a chip whose logic is fixed permanently at fabrication time for a single, specific task, trading away all reconfigurability for maximum energy efficiency and performance density.

## Position on the Specialization Spectrum

ASICs sit at the extreme "dedicated hardware" end of the [[Hardware Specialization Spectrum]], achieving roughly 100x the energy efficiency (MOPS/mW) of general-purpose microprocessors, compared to about 10x for DSPs. This efficiency comes directly from removing everything a general-purpose chip needs but a fixed workload does not: instruction decoding, branch prediction, and large general caches.

## Trade-offs

| Advantage | Disadvantage |
|---|---|
| Highest possible performance-per-watt | Zero flexibility - fixed at fabrication |
| No wasted die area on general-purpose control logic | Extremely expensive and slow to design/fabricate (months to years) |
| Ideal for extremely high-volume, stable workloads | A design mistake or workload change cannot be fixed in hardware |

## Design Flow

The ASIC design flow mirrors [[Field-Programmable Gate Array|FPGA]] programming - code is synthesized into a logic-gate-level representation, then placed and routed - but the final circuit is mapped onto dedicated **silicon** at fabrication rather than onto reconfigurable FPGA resources, removing the reconfiguration overhead entirely.

## Example

Google's [[Tensor Processing Unit]] is a production ASIC built specifically for neural network inference, justified because the target workload (voice search using DNNs) was both extremely high-volume and compute-intensive enough that a 10x cost-performance improvement over GPUs was worth the fixed, non-reconfigurable design.

## Related Concepts

- [[Tensor Processing Unit]]: a concrete, production ASIC example
- [[Field-Programmable Gate Array]]: the reconfigurable alternative one step less specialized than an ASIC
- [[Hardware Specialization Spectrum]]: the general efficiency-vs-flexibility tradeoff ASICs sit at the extreme of
