---
title: Message Passing IPC
aliases:
  - Message Passing
tags:
  - operating-systems
  - ipc
description: "Inter-process communication method where processes exchange data through OS-managed send and receive operations"
draft: false
---

> [!NOTE] Definition
> Message passing IPC allows processes to communicate by sending and receiving messages through the OS kernel.

## How It Works

- Processes use `send()` and `receive()` system calls
- The OS manages message buffering and delivery
- No shared memory needed - processes can be on different machines

## Trade-offs

| Advantage | Disadvantage |
|-----------|-------------|
| No shared state to synchronize | Higher overhead (syscalls for every message) |
| Works across network boundaries | OS involvement on every transfer |
| Safer (no direct memory sharing) | Slower than [[Shared Memory IPC]] |

## Related Concepts

- [[Shared Memory IPC]]: the faster alternative using shared address space
- [[Remote Procedure Call]]: message passing abstracted as function calls
- [[Microkernel]]: relies heavily on message passing for internal communication
