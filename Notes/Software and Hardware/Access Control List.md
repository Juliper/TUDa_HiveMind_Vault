---
title: Access Control List
aliases:
  - ACL
tags:
  - operating-systems
  - security
description: "A list of permissions attached to a resource specifying which subjects can access it and how"
draft: false
---

> [!NOTE] Definition
> An Access Control List (ACL) is attached to each resource (file, device, etc.) and specifies which users or processes have which permissions (read, write, execute).

## Structure

Each entry in an ACL contains:
- **Subject** (user or group)
- **Permissions** (read, write, execute, etc.)

Example: `file.txt: [alice: rw, bob: r, group-dev: rwx]`

## ACL vs Capabilities

| Approach | Perspective | Description |
|----------|-------------|-------------|
| **ACL** | Per resource | Lists who can access this resource |
| **Capability list** | Per subject | Lists what resources this user can access |

## Related Concepts

- [[Bell-LaPadula Modell]]: formal model for confidentiality-based access control
- [[Biba Modell]]: formal model for integrity-based access control
- [[CIA Triad]]: ACLs primarily enforce confidentiality and integrity
