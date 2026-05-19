---
title: Runtime Attacks
aliases:
  - Runtime-Angriffe
  - Laufzeitangriffe
tags:
  - operating-systems
  - security
description: "Attacks that exploit running programs without modifying their binaries on disk"
draft: false
---

> [!NOTE] Definition
> Runtime attacks exploit vulnerabilities in programs during execution. The binaries on disk remain unchanged - only the in-memory execution is manipulated.

## Attack Types

| Attack | Description |
|--------|-------------|
| **Denial of Service (DoS)** | Overwhelm a system to make it unavailable |
| **Remote Code Execution** | Execute arbitrary code on a target system |
| **Privilege Escalation** | Gain higher privileges than authorized |
| **[[Buffer Overflow]]** | Write beyond buffer boundaries to corrupt memory |

## Related Concepts

- [[Buffer Overflow]]: the most common runtime attack vector
- [[Prozessspeicher und Stackframe]]: understanding the memory layout is key to these attacks
- [[User Mode und Kernel Mode]]: privilege escalation crosses this boundary
