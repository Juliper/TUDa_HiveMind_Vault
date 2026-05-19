---
title: Banker's Algorithm
aliases:
  - Bankers Algorithmus
tags:
  - operating-systems
  - synchronization
  - deadlocks
description: "Deadlock avoidance algorithm that only grants resource requests if the system remains in a safe state"
draft: false
---

> [!NOTE] Definition
> The Banker's Algorithm is a deadlock avoidance strategy. Before granting a resource request, it checks whether the resulting state would still be safe - meaning all processes could still complete.

## How It Works

1. A process requests resources
2. The algorithm tentatively grants the request
3. It checks if a safe sequence exists: an ordering of all processes where each can finish with the currently available resources plus those held by previously finished processes
4. If safe: grant the request
5. If unsafe: block the process until the request can be safely granted

## Safe vs Unsafe State

- **Safe state**: there exists at least one execution order where every process can finish
- **Unsafe state**: no such order exists - deadlock is possible (but not guaranteed)

> [!WARNING]
> An unsafe state does not mean a deadlock has occurred - it means one *could* occur. The Banker's Algorithm is conservative and may reject requests that would actually be fine.

## Related Concepts

- [[Resource Deadlock Conditions]]: the conditions the algorithm tries to avoid
- [[Deadlock-Strategien]]: the broader context of deadlock handling
