---
title: Deadlock Strategies
aliases:
  - Deadlock-Strategien
tags:
  - operating-systems
  - synchronization
  - deadlocks
description: "Approaches to handling deadlocks - ignoring, detecting, preventing, and recovering"
draft: false
---

> [!NOTE] Definition
> There are four fundamental strategies for dealing with deadlocks, ranging from ignoring them to actively preventing them.

## Strategies

### 1. Ignore (Ostrich Algorithm)
- If deadlocks are rare and the cost of prevention is high, simply ignore them
- Pragmatic approach used by many real systems

### 2. Detection
- Allow deadlocks to occur, then detect and resolve them
- Detection via **resource allocation graph**: if the graph contains a cycle, a deadlock exists
- After detection, apply recovery

### 3. Prevention
Break one of the [[Resource Deadlock Conditions|four Coffman conditions]]:
- **Break mutual exclusion**: make resources shareable (often not possible)
- **Break hold-and-wait**: require processes to request all resources at once
- **Break no-preemption**: allow resources to be forcibly taken
- **Break circular wait**: impose an ordering on resource acquisition

### 4. Avoidance
- System grants resources only if the resulting state is **safe**
- A state is safe if there exists a sequence in which all processes can complete without deadlock
- [[Bankers Algorithmus]]: checks if granting a request keeps the state safe

## Recovery Methods

| Method | Description |
|--------|-------------|
| **Pre-emption** | Take resources from one process and give to another |
| **Kill process** | Terminate one or more processes to free resources |
| **Rollback** | Restore processes to a saved checkpoint state |

## Related Concepts

- [[Resource Deadlock Conditions]]: the conditions these strategies target
- [[Bankers Algorithmus]]: the classic avoidance algorithm
