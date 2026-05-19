---
title: Wear Leveling
aliases:
  - Wear Management
tags:
  - databases
  - hardware
  - storage
description: "An SSD firmware technique that distributes writes evenly across all flash blocks to prevent premature cell failure"
draft: false
---

> [!NOTE] Definition
> Wear leveling is a technique used by the [[Flash Translation Layer]] to distribute write and erase operations evenly across all flash blocks. Without it, frequently-written blocks would wear out while others remain unused, causing premature SSD failure.

## Why It's Needed

Each flash cell supports a limited number of program/erase (P/E) cycles:

| Flash Type | Endurance |
|---|---|
| SLC | ~100,000 P/E cycles |
| MLC | ~10,000 P/E cycles |
| TLC | ~3,000 P/E cycles |

If writes concentrate on a few blocks, those blocks fail early even though the rest of the SSD is healthy.

## Types

### Dynamic Wear Leveling

Only redistributes writes among **free** blocks. When writing new data, the FTL selects the free block with the lowest erase count.

- Simple to implement
- Does not address cold data sitting on low-wear blocks indefinitely

### Static Wear Leveling

Periodically moves **cold (rarely written) data** from low-wear blocks to high-wear blocks, freeing the low-wear blocks for new writes.

- More complex, causes additional [[Write Amplification]]
- But achieves much more uniform wear across all blocks

> [!IMPORTANT]
> Static wear leveling is essential for long SSD lifetime but increases write amplification. The FTL must balance between wear uniformity and write amplification overhead.

## Related Concepts

- [[Flash Translation Layer]]: implements wear leveling as part of page mapping
- [[Write Amplification]]: wear leveling contributes to write amplification
- [[SSD Architecture]]: the hardware whose lifetime wear leveling extends
