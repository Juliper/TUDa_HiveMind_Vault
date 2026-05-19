---
title: Remote Procedure Call
aliases:
  - RPC
tags:
  - operating-systems
  - ipc
  - networking
description: "Protocol that allows a process to call procedures on a remote system as if they were local"
draft: false
---

> [!NOTE] Definition
> A Remote Procedure Call (RPC) is a protocol for requesting services from a program on another system over the network, making remote calls look like local function calls.

## How It Works

- Uses **stubs** (proxies) on both client and server side
- The client stub marshals parameters and sends them over the network
- The server stub unmarshals parameters and calls the actual procedure
- The result is sent back the same way

## Challenges

- RPCs can fail (network issues, server crashes)
- Duplicate requests must be detected and prevented
- ACKs are required for reliability
- Client must resend unacknowledged RPCs

## Related Concepts

- [[Message Passing IPC]]: the underlying communication model
- [[Shared Memory IPC]]: local-only alternative that doesn't need network
