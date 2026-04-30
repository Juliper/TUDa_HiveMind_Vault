---
title: Zero Trust Architecture
aliases:
  - ZTA
  - Zero Trust
tags:
  - cybersecurity
  - fundamentals
  - network-security
description: "Security model: trust nothing by default, verify everything explicitly."
---

**Zero Trust Architecture (ZTA)** is a security model built on the premise of *"trust nothing by default, verify everything explicitly"*, regardless of where a request originates.

**Goal:** Eliminate implicit trust. Always assume the system has already been compromised.

## Core Principles (NIST SP 800-207)

- All data sources and computing services are considered **resources**
- All communications must be secured **regardless of network location**
- Access to resources is granted **in sessions only**
- Access is determined by **dynamic policy**, influenced by user characteristics and behavior
- Every owned or associated asset is **continuously monitored**, no inherent trust

## Architecture

**Control Plane:**

- **PDP (Policy Decision Point):** centralized authorization engine that evaluates access requests against defined policies and makes allow/deny decisions
- **Policy Engine + Administrator** define the policies

**Data Plane:**

- **PEP (Policy Enforcement Point):** intercepts access requests and enforces the PDP decisions (allow/block)

```
Subject -> [Untrusted] -> PEP -> [Trusted] -> Enterprise Resource
                          ^
                         PDP (Control Plane)
```

## Challenges of ZTA Migration

- High complexity and operational costs
- Incompatibility with legacy systems
- User authentication fatigue and workflow disruption
- Expensive and disruptive: continuous process; every department must change workflows, tools, and approaches

## Related Concepts

- [[Secure by Design]]: ZTA is a complementary design principle
- [[Defense in Depth]]: ZTA complements layered defense
- [[Threat Modelling]]: ZTA arises from the assumption that the system is already under attack
