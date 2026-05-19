---
title: Biba Model
aliases:
  - Biba Modell
tags:
  - operating-systems
  - security
description: "Security model that enforces data integrity through no-read-down and no-write-up rules"
draft: false
---

> [!NOTE] Definition
> The Biba model is a formal security model focused on **integrity**. It prevents untrusted data from contaminating trusted data.

## Rules

| Rule | Description |
|------|-------------|
| **No Read Down** | A subject cannot read data at a lower integrity level |
| **No Write Up** | A subject cannot write data to a higher integrity level |

This ensures that low-integrity (potentially corrupted) data cannot influence high-integrity data.

## Related Concepts

- [[Bell-LaPadula Modell]]: the dual model focused on confidentiality
- [[CIA Triad]]: integrity is one of the three security goals
