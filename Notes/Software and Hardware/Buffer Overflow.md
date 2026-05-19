---
title: Buffer Overflow
aliases:
  - Buffer-Overflow
tags:
  - operating-systems
  - security
description: "A vulnerability where data written beyond a buffer's boundary overwrites adjacent memory"
draft: false
---

> [!NOTE] Definition
> A buffer overflow occurs when a program writes data past the end of a buffer, overwriting adjacent memory. Attackers can exploit this to inject code or redirect execution flow.

## How It Works

1. A vulnerable function allocates a fixed-size buffer on the [[Prozessspeicher und Stackframe|stack]]
2. Input exceeding the buffer size overwrites the **return address** on the stack
3. When the function returns, the CPU jumps to the attacker-controlled address
4. This can execute injected shellcode or redirect to existing code (ROP)

## Defenses

| Defense | Description |
|---------|-------------|
| **Stack canaries** | Random value placed before return address; checked on function return |
| **ASLR** | Randomize memory layout to make address prediction harder |
| **DEP/NX** | Mark stack as non-executable |
| **Bounds checking** | Validate buffer sizes before writing |

## Related Concepts

- [[Runtime-Angriffe]]: buffer overflow is a type of runtime attack
- [[Prozessspeicher und Stackframe]]: the stack layout that makes this possible
