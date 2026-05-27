---
title: Pointer Swizzling
aliases:
  - Swizzling
tags:
  - databases
  - indexing
  - storage
description: "A technique that replaces page IDs in buffer-resident index nodes with direct memory pointers, avoiding repeated page table lookups"
draft: false
---

> [!NOTE] Definition
> Pointer swizzling is a technique used in SSD-based database systems where page ID references in index nodes (like B+ trees) are replaced with direct memory pointers once the referenced page is loaded into the buffer pool. This avoids the overhead of translating page IDs to memory addresses on every access.

## The Problem

In a disk/SSD-based B+ tree, each node references children via **page IDs**. Every traversal step requires:
1. Read the page ID from the current node
2. Look up the page ID in the **page table** (hash table mapping page ID to memory address)
3. If not in buffer: load from SSD, find a buffer frame, update page table
4. Access the node at the resolved memory address

Step 2 happens on **every access**, even when the page is already in memory - this is pure overhead.

## How Swizzling Works

When a page is loaded into the buffer pool:
1. Read the disk page (contains page IDs as child references)
2. Look up where those child pages are in memory (if already loaded)
3. **Rewrite** ("swizzle") the page ID references into direct memory pointers

**Before swizzling**: child reference = page ID 42
**After swizzling**: child reference = memory pointer `0x7fff5a2b3000`

Subsequent accesses to children follow pointers directly - no page table lookup needed.

## Swizzling Strategies

| Strategy | When to swizzle | Trade-off |
|---|---|---|
| **Eager** | When page is loaded | Higher load cost, faster subsequent access |
| **Lazy** | On first child access | Lower load cost, first access still needs lookup |

## Unswizzling

When a page must be evicted from the buffer pool:
1. Find all pages that point to the evicted page
2. Replace the swizzled pointers back with page IDs
3. Evict the page

> [!IMPORTANT]
> Pointer swizzling is critical for SSD-based DBMS performance. Without it, every B+ tree traversal step incurs an extra hash table lookup in the page table, which can dominate the cost of index operations when most data fits in the buffer pool.

## Related Concepts

- [[B+ Tree Latch Coupling]]: concurrency control for the B+ tree that uses swizzling
- [[LeanStore]]: NVMe-optimized storage engine that uses pointer swizzling
- [[Flash Translation Layer]]: similar concept of address indirection, but at the SSD firmware level
