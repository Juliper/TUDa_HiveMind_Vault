---
title: Bell-LaPadula Model
aliases:
  - Bell-LaPadula Modell
tags:
  - operating-systems
  - security
description: "Security model that enforces confidentiality through no-read-up and no-write-down rules"
draft: false
---

> [!NOTE] Definition
> The Bell-LaPadula model is a formal security model focused on **confidentiality**. It prevents information from flowing from higher security levels to lower ones.

## Rules

| Rule | Description |
|------|-------------|
| **No Read Up** (Simple Security) | A subject cannot read data at a higher security level |
| **No Write Down** (Star Property) | A subject cannot write data to a lower security level |

This ensures that classified information cannot leak to unclassified levels.

## Related Concepts

- [[Biba Modell]]: the dual model focused on integrity instead of confidentiality
- [[Access Control List]]: another access control mechanism
- [[CIA Triad]]: confidentiality is one of the three security goals
