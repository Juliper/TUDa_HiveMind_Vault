---
title: Demand Paging vs Pre-Paging
aliases:
  - Demand-Paging
  - Lazy Loading
tags:
  - operating-systems
  - memory-management
  - paging
description: "Two strategies for loading pages into memory - on access or predictively"
draft: false
---

> [!NOTE] Definition
> **Demand paging** loads pages only when accessed (triggering a page fault). **Pre-paging** predicts which pages will be needed and loads them in advance.

## Demand Paging (Lazy Loading)

- Pages are loaded into main memory only when the process tries to access them
- First access triggers a [[Page Replacement Algorithmen|page fault]]
- Saves memory by not loading unused pages
- Increases latency for first access to each page

## Pre-Paging

- The OS predicts which pages a process will need and loads them before access
- Reduces page faults and latency
- Risk: wrong predictions waste memory and I/O bandwidth

## Page Fault Types

| Type | Description | Cost |
|------|-------------|------|
| **Minor** | Page is in RAM but not linked to the process - just needs remapping | Low |
| **Major** | Page is on disk (secondary storage) and must be loaded into RAM | High latency |
| **Segmentation Fault** | Process tries to access an invalid address (e.g., kernel space) - process is typically killed | Fatal |

## Related Concepts

- [[Paging und Swapping]]: the paging mechanism these strategies apply to
- [[Page Replacement Algorithmen]]: what happens when a page must be evicted to make room
- [[Thrashing]]: the result of too many page faults
