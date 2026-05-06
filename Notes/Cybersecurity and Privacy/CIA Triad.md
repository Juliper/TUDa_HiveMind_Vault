---
title:
aliases:
tags:
description: "The five security goals: Confidentiality, Integrity, Authenticity, Availability, Non-Repudiation."
---

> [!NOTE] Definition
> The CIA triad is a set of security goals that inform **the development of modern systems**.

## The Five Goals

| Goal | Definition | Attack Scenario |
|---|---|---|
| **Confidentiality** | Only authorized personnel can access the contents of data | Eavesdropping, sniffing |
| **Integrity** | Data is not corrupted, tampered with, or altered by unauthorized parties | Man-in-the-middle, tampering |
| **Authenticity** | The source identity is genuine | Spoofing (sending messages pretending to be Alice) |
| **Availability** | Reliable and timely access to data and services for authorized parties | DoS/DDoS - overwhelming or crashing services |
| **Non-Repudiation** | No entity can falsely deny performing an action | Internal threat (Alice herself misbehaves) |

> [!NOTE]
> Non-Repudiation does not target an external attacker. It protects against misbehavior by authorized users themselves.

## Trade-Offs

Ideally: complementary design goals.
In reality: they exist in a state of perpetual tension.

| Industry/Data Type | Priority Pillar | Rationale | Secondary Pillars |
|---|---|---|---|
| Banks/Fintech | Integrity | Inaccurate transactions lead to systemic failure and loss of trust | Confidentiality, Availability |
| Military/Intelligence | Confidentiality | Disclosure of state secrets costs lives | Integrity, Availability |
| Healthcare | Availability | Access to patient records is a matter of life or death | Integrity, Confidentiality |
| E-commerce/Media | Availability | Downtime during a sales event means revenue loss | Integrity, Confidentiality |

## Related Concepts

- [[What is Cybersecurity?]]: core vocabulary and definitions
- [[Threat Modelling]]: structured process to identify CIA violations
- [[Secure by Design]]: principles to protect the CIA goals
