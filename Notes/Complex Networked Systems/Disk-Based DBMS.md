---
title: Disk-Based DBMS
aliases:
  - Traditional DBMS
  - Disk-Oriented Database
tags:
  - databases
  - storage
description: "Traditional DBMS architecture that assumes primary data resides on disk, using a buffer pool to cache pages in memory"
draft: false
---


> [!NOTE] Definition
> A disk-based DBMS assumes that the primary storage medium is a disk (HDD or SSD). Data is organized in fixed-size pages on disk and cached in a memory buffer pool. All data access goes through the buffer pool manager, which handles page loading, eviction, and dirty page write-back.
<img src="https://deepaksood619.github.io/assets/images/Disk-oriented-vs-in-memory-DBs-image2-36160e65857bfe7d5cc811e910059d32.jpg">
## Overhead Breakdown

```mermaid
pie
    "Buffer Pool" : 34
    "Latching" : 14
    "Locking" : 16
    "Logging" : 12
    "B-Tree Keys" : 16
    "Real Work" : 7
```

> [!IMPORTANT]
> Only about 7% of CPU cycles in a disk-based DBMS go to actual data processing. The overwhelming majority is spent on infrastructure to manage the disk-memory boundary. This is the key motivation for [[Main Memory DBMS]] systems.

## Observations
- Overhead comes from “indirections” even if page is already in the buffer
	- lookup cost in page table
	- calculating a memory pointer to the tuple
- There is an increasing gap between CPU & memory speeds leading to I/O wait
## Related Concepts

- [[Main Memory DBMS]]: the alternative architecture assuming data fits in RAM
- [[SSD Performance Characteristics]]: SSDs change the disk access cost model
- [[SSD-Aware Database Design]]: adapting disk-based designs for SSD characteristics
