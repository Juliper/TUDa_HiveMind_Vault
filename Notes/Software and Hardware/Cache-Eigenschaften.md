---
title: Cache Properties
aliases:
  - Cache-Eigenschaften
tags:
  - operating-systems
  - hardware
  - memory
description: "Classification of CPU caches by organization and data sharing policies"
draft: false
---

> [!NOTE] Definition
> CPU caches are small, fast memory stores between the CPU and main memory. They are classified by how they are organized and how data is shared across cache levels.

## Cache Organization

| Type | Description |
|------|-------------|
| **Split cache** | Separate caches for instructions (I-cache) and data (D-cache) |
| **Unified cache** | Single cache for both instructions and data |

## Data Sharing Policies

| Policy | Description |
|--------|-------------|
| **Inclusive** | Data in a core's private cache is also kept in the shared cache |
| **Exclusive** | Data exists in either the private or shared cache, never both |
| **Non-exclusive** | Data may or may not be duplicated across cache levels |

## Related Concepts

- [[Write-hit und Write-miss Policies]]: how cache handles writes
- [[Translation Lookaside Buffer]]: a specialized cache for page table entries
