---
title: Transition System Composition
aliases:
  - Produktkomposition
  - TS Composition
tags:
  - formal-methods
  - moses
  - concurrency
description: "Four composition modes for transition systems - synchronous, asynchronous, shared-memory, and message-passing"
draft: false
---

> [!NOTE] Definition
> Transition systems can be composed in four ways to model different interaction patterns between concurrent components.

## Synchronous Product Composition

Both systems must take a step simultaneously with matching events.

$$S := S^1 \times S^2, \quad S_0 := S_0^1 \times S_0^2, \quad E := E^1 \times E^2$$

$$\rightarrow := \{((s_1, s_2), (e_1, e_2), (s_1', s_2')) \mid s_1 \xrightarrow{e_1} s_1' \wedge s_2 \xrightarrow{e_2} s_2'\}$$

## Asynchronous Product Composition

Either system takes a step while the other remains unchanged.

$$S := S^1 \times S^2, \quad S_0 := S_0^1 \times S_0^2, \quad E := E^1 \cup E^2$$

$$\rightarrow := \{((s_1, s_2), e, (s_1', s_2')) \mid s_1 \xrightarrow{e} s_1' \wedge s_2 = s_2' \;\vee\; s_2 \xrightarrow{e} s_2' \wedge s_1 = s_1'\}$$

## Shared-Memory Composition (Asynchronous)

Two local systems share global state. Either system steps, reading/writing shared state.

$$S := SL_1 \times SL_2 \times SG$$

$$S_0 := \{(sl_1, sl_2, sg) \mid (sl_1, sg) \in S_0^1 \wedge (sl_2, sg) \in S_0^2\}$$

$$E := E_1 \cup E_2$$

A transition fires for one system while the other's local state is unchanged:
- If $e \in E^1$: system 1 steps with $(sl_1, sg) \xrightarrow{e} (sl_1', sg')$, and $sl_2' = sl_2$
- If $e \in E^2$: system 2 steps with $(sl_2, sg) \xrightarrow{e} (sl_2', sg')$, and $sl_1' = sl_1$

## Message-Passing Composition (Asynchronous)

Systems have private events and shared (synchronizing) events $E^1 \cap E^2$.

$$S := S^1 \times S^2, \quad E := E^1 \cup E^2$$

- **Private event** ($e \in E^1 \setminus E^2$): only system 1 steps, system 2 unchanged
- **Private event** ($e \in E^2 \setminus E^1$): only system 2 steps, system 1 unchanged
- **Shared event** ($e \in E^1 \cap E^2$): both systems must step simultaneously (handshake)

> [!IMPORTANT]
> The key distinction:
> - **Synchronous**: both always step together
> - **Asynchronous**: interleaved, independent steps
> - **Shared-memory**: interleaved with shared global state
> - **Message-passing**: interleaved with synchronization on shared events

## Related Concepts

- [[Transition Systems]]: the systems being composed
- [[Process Algebra]]: alternative formalism for composition
