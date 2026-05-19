---
title: Disk Partitions
aliases:
  - Festplattenorganisation
  - Master Boot Record
tags:
  - operating-systems
  - file-systems
description: "How disks are physically structured and logically partitioned for file system use"
draft: false
---

> [!NOTE] Definition
> A disk is divided into partitions, each with its own file system. The partition table and boot code are stored in the Master Boot Record.

## Disk Structure

| Component | Description |
|-----------|-------------|
| **Sector** | Smallest addressable unit on disk |
| **Track** | Circular path on a magnetic platter |
| **Platter (Disk)** | One of the stacked magnetic disks |
| **Cylinder** | The set of tracks at the same position across all platters |

## Access Latency

| Component | Typical Time |
|-----------|-------------|
| Seek time (move head to cylinder) | ~10ms |
| Rotational delay (wait for sector) | ~4ms |
| Read/write time (transfer data) | ~50us |

## Master Boot Record (MBR)

- Stored in sector 0 of every disk
- Required for booting the system
- Contains the partition table at the end
- Exactly one partition is marked **active** for booting

## Partition Layout (K-th Partition)

- All partitions start with a **boot block** (including OS partitions)
- Layout depends on the file system
- Typically starts with a **superblock** containing key parameters (number of blocks, etc.)

## Disk Controller

Abstracts between physical disk geometry and logical block addresses. The OS works with logical blocks; the controller maps them to physical sectors.

## Related Concepts

- [[File Allocation-Typen]]: how files are stored within partitions
- [[Dateitypen und Dateistruktur]]: what files look like at a higher level
