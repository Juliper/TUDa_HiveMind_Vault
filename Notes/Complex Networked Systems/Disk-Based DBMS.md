---
title:
aliases:
tags:
description: Traditional DBMS systems assume that the primary storage medium is a disk (HDD or SSD). Data is stored on disk pages and cached in a memory buffer pool.
draft: false
---
> [!NOTE] Definition
> Traditional DBMS systems assume that the primary storage medium is a disk (HDD or SSD). Data is stored on disk pages and cached in a memory buffer pool.
## Data Access
TODO

## Overhead
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
> Data access via Buffer pool causes highest overhead