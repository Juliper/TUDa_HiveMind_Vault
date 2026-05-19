---
title: Free Memory Management
aliases:
  - Freispeicherverwaltung
tags:
  - operating-systems
  - memory-management
description: "Data structures for tracking which memory blocks are free or occupied"
draft: false
---

> [!NOTE] Definition
> The OS needs to track which parts of memory are free and which are in use. Two common approaches are bitmaps and linked lists.

## Bitmaps

- Memory is divided into **allocation units**
- Each unit is represented by one bit: `1` = occupied, `0` = free
- Trade-off: smaller units mean more precise tracking but longer bitstrings; larger units reduce bitmap size but increase [[Interne und Externe Fragmentierung|internal fragmentation]]

## Linked Lists

- A linked list of memory segments, each storing:
  - Block ID, start position, size, and whether it's free or occupied
- Neighboring free blocks should be merged to prevent [[Interne und Externe Fragmentierung|external fragmentation]]
- More flexible than bitmaps but slower to search

## Related Concepts

- [[Allocation-Strategien]]: which free block to choose for a new process
- [[Interne und Externe Fragmentierung]]: the problems these structures help manage
