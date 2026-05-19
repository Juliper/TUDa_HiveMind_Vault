---
title: File Allocation Types
aliases:
  - File Allocation-Typen
  - Allokationstypen
tags:
  - operating-systems
  - file-systems
description: "Methods for allocating disk blocks to files - contiguous, linked list, FAT, and i-nodes"
draft: false
---

> [!NOTE] Definition
> File allocation determines how a file's data blocks are arranged on disk. Each method trades off between access speed, fragmentation, and flexibility.

## Allocation Methods

### Contiguous Allocation
- Files occupy consecutive blocks on disk
- **Advantage**: fast sequential and random access
- **Disadvantage**: external fragmentation, maximum file size must be known in advance

### Linked List Allocation
- Each block contains a pointer to the next block
- **Advantage**: no external fragmentation, only first block address needed
- **Disadvantage**: random access is very slow (must follow chain), block size is not a power of 2 (pointer takes space)

### File Allocation Table (FAT)
- The entire chain of block pointers is stored in a table in memory
- Directory entries point to the first block; each FAT entry points to the next block
- **Advantage**: random access via table lookup
- **Disadvantage**: entire table must fit in memory - problematic for large disks

### I-Nodes
- Each file has an i-node containing attributes and addresses of the first $n$ data blocks
- If the file is larger than $n$ blocks, the i-node contains a pointer to an indirect block with more addresses
- This hierarchy can have multiple levels (single, double, triple indirect)
- **Advantage**: only the i-node of open files needs to be in memory
- **Disadvantage**: more complex implementation

## File System Types

| Type | Description |
|------|-------------|
| **Log-Structured** | Writes are collected in a buffer and appended to disk end. Minimizes seeks. I-nodes can fragment; a cleaner thread consolidates valid data. |
| **Journal** | Before modifying data, the operation is logged to a journal. On crash, the journal is replayed to restore consistency. |
| **Virtual (VFS)** | Abstraction layer enabling multiple file systems (ext4, NTFS, FAT) to coexist under one interface. |

## Directory Implementation

| Method | Description |
|--------|-------------|
| Store attributes directly | Attributes are in the directory entry |
| Reference i-node | Directory entry points to an i-node containing the attributes |

## Related Concepts

- [[Disk Partitions]]: the partitions these allocation methods operate within
- [[Dateitypen und Dateistruktur]]: the files being allocated
