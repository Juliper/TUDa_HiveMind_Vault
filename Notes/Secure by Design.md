---
title: Secure by Design
aliases:
  - SbD
  - Secure-by-Design
tags:
  - cybersecurity
  - fundamentals
  - software-engineering
description: "Principle: build security in from the start instead of adding it later."
---

**Secure by Design** is the principle that security is built into a system from the earliest stages of design, not added as an afterthought, patch, or perimeter control after implementation.

> Retrofitted security is **more expensive** and **less efficient**.

**Goal:** Reduce the number of vulnerabilities early in the development process so that there are fewer incidents during deployment.

## Current Problem: Retrofit Security

Existing systems get security added retroactively:

- Codebase is changed and security features (e.g. cryptography) are added
- Add-ons and wrappers feed systems with additional security parameters
- Issues: new vulnerabilities are introduced, attack surface grows
- **Downgrade attacks** can wipe out the benefits of added security wrappers

## Principles

| Principle | Meaning |
|---|---|
| **Least Privilege** | Every component, user, and process gets only the minimum access needed |
| **[[Defense in Depth]]** | Multiple independent layers of protection |
| **Fail Secure** | On error or unexpected state, default to the most recent safe state |
| **Compartmentalization/Segmentation** | Expose only what is necessary; component isolation (data, networks) |
| **Separation of Duties** | Risk spreading; require multiple conditions to be met before completing a task |
| **No Security through Obscurity** | Security must not depend on keeping the design secret (Kerckhoffs' principle) |

## Compartmentalization

Security by Design requires moving away from "flat" networks where everything can talk to everything.

- **Concept:** divide a network into smaller distinct segments (subnets) based on function, risk profile, or data sensitivity
- **Goal:** minimize the "blast radius" if hosts or segments get compromised
- **Segment Boundaries:** physical and logical checkpoints where strict security policies (firewalls, [[Zero Trust Architecture]]) are applied

## Related Concepts

- [[Defense in Depth]]: one of the SbD principles, explained in detail
- [[Zero Trust Architecture]]: complementary security model for new systems
- [[CIA Triad]]: the security goals SbD protects
