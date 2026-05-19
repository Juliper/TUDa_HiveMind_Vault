---
title: x86 Protection Rings
aliases:
  - x86 Schutzringe
  - Ring Architecture
  - Protection Rings
tags:
  - operating-systems
  - cpu-architecture
description: "Privilege levels in x86 architecture that control access to hardware resources"
draft: false
---

> [!NOTE] Definition
> The x86 architecture uses four privilege rings (0-3) to categorize access permissions. Lower ring numbers grant more privileges.

## Ring Levels

```mermaid
graph LR
    R0[Ring 0 - Kernel] --> R1[Ring 1 - Drivers]
    R1 --> R2[Ring 2 - Drivers]
    R2 --> R3[Ring 3 - Applications]
```

| Ring | Purpose | Privilege Level |
|------|---------|----------------|
| **Ring 0** | OS Kernel | Full hardware access |
| **Ring 1** | Device drivers | Elevated (rarely used) |
| **Ring 2** | Device drivers | Elevated (rarely used) |
| **Ring 3** | User applications | Restricted |

> [!IMPORTANT]
> Rings 1 and 2 are rarely used in modern operating systems. Most systems only distinguish between Ring 0 (kernel mode) and Ring 3 (user mode).

## How It Works

When a program in a higher ring (e.g., Ring 3) needs to access resources managed by a lower ring, it must request access through the lower ring's interfaces - typically via [[System Calls]].

## Related Concepts

- [[User Mode und Kernel Mode]]: the practical two-ring model used by modern OSes
- [[System Calls]]: the mechanism for crossing ring boundaries
