---
title: B+ Tree Latch Coupling
aliases:
  - Lock Coupling
  - Latch Coupling
  - B+ Tree Concurrency
tags:
  - databases
  - indexing
  - concurrency
  - in-memory
description: "A concurrency protocol for B+ trees that acquires and releases latches level-by-level during traversal, with safe-child optimization"
draft: false
---

> [!NOTE] Definition
> Latch coupling (also called lock coupling) is a concurrency protocol for B+ tree operations. A thread holds a latch on at most two adjacent levels at a time: it acquires the child's latch before releasing the parent's, ensuring structural consistency during concurrent access.

## Locks vs Latches

| Property | Locks | Latches |
|---|---|---|
| Purpose | Transaction isolation (serializability) | Protect internal data structures |
| Managed by | Lock manager | Index implementation directly |
| Duration | Transaction lifetime | Brief (during node access) |
| Deadlock handling | Detection/timeout | Must be avoided by protocol |
| Modes | Shared, Exclusive, ... | Read (R), Write (W) |

## Latch Coupling Protocol

### Search (Read)

1. Acquire **R latch** on root, search the node
2. Acquire **R latch** on child
3. **Release parent's R latch** (child is safe for reads)
4. Repeat down to the leaf

> [!NOTE] Example
> Searching for key 23: R-latch A (root) -> R-latch C (child, release A) -> R-latch F (leaf, release C) -> read value, release F.

### Insert/Delete (Write)

1. Acquire **W latch** on root, search the node
2. Acquire **W latch** on child
3. Check if child is **safe** - if yes, release **all ancestor latches**
4. Repeat down to the leaf, then perform the modification

## Safe Child Optimization

A child node is considered **safe** if the current operation will not cause a structural modification (split or merge) that propagates to the parent:

| Operation | Child is safe if... |
|---|---|
| **Insert** | Child is **not full** (has room for new key) |
| **Delete** | Child is **more than half-full** (won't trigger merge) |

When the child is safe, all latches held on ancestor nodes can be released immediately, because any structural change will be contained within the subtree below.

> [!IMPORTANT]
> For deletes: if a child might need to merge with a sibling, the parent latch must be held because the parent's separator key may need updating. This is why delete latching is more conservative than insert latching.

## Optimistic Lock Coupling (OLC)

Traditional latch coupling still limits concurrency because write operations hold latches top-down. Optimistic Lock Coupling replaces latches with **version counters**:

1. **Read operations**: read the version, access the node, validate the version hasn't changed
2. **Write operations**: increment the version before and after modification
3. If validation fails: **restart** the operation from the root

| Property | Latch Coupling | Optimistic Lock Coupling |
|---|---|---|
| Read overhead | Acquire/release latch | Read version counter |
| Write overhead | Acquire/release latch | Increment version |
| Contention | Readers block writers | Readers never block |
| Wasted work | None | Restarts on conflicts |

OLC scales much better for read-heavy workloads because readers never acquire any latches and therefore never block writers.

> [!WARNING]
> OLC can be worse than latch coupling under very high write contention, because frequent version changes cause many restarts, wasting work.

## Related Concepts

- [[CSB+ Tree]]: cache-sensitive B+ tree that needs concurrency control
- [[CSS-Tree]]: read-only tree that doesn't need latching
- [[Pointer Swizzling]]: another B+ tree optimization for SSD-based indexes
