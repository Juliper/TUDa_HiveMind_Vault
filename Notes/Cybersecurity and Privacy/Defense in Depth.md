---
title: Defense in Depth
aliases:
tags:
description: "Layered security strategy: if one layer fails, the others remain in place."
---

**Defense in Depth** is a layered security strategy that employs multiple defensive mechanisms across different levels of a system, so that if one defense fails, others remain to mitigate the threat. It significantly raises the cost and complexity of a successful attack.

It is one of the core principles of [[Secure by Design]].

## Layers

| Layer | Enforcement |
|---|---|
| **Application** | Input validation, secure coding |
| **Network** | Firewalls, IDS, honeypots |
| **Host** | Antivirus, OS hardening |
| **Data** | Encryption |
| **Physical** | Biometric scanners, security cameras |

## Related Concepts

- [[Secure by Design]]: Defense in Depth is one of the SbD principles
- [[Zero Trust Architecture]]: complementary, trusts no layer implicitly
- [[Indicator of Compromise]]: detection when a layer has already been breached
