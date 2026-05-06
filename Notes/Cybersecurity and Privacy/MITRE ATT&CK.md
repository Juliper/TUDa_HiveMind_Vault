---
title: MITRE ATT&CK
aliases:
  - ATT&CK
  - TTP
  - Tactics Techniques Procedures
tags:
  - cybersecurity
  - threat-intelligence
description: "Globally accessible database of real-world adversary tactics and techniques; structures CTI and threat models."
---

**MITRE ATT&CK** is a globally accessible, free database of adversary tactics and techniques based on real-world observations of cyberattacker behavior. It helps defenders structure [[Cyber Threat Intelligence]] and design better threat models.

MITRE data is based on real-world cyberattacks.

## TTPs

| Level              | Definition                                                  | Example                   |
| ------------------ | ----------------------------------------------------------- | ------------------------- |
| **T - Tactics**    | High-level goals of the attacker when compromising a system | *Initial Access*          |
| **T - Techniques** | Specific method to achieve the tactic's goal                | *Supply Chain Compromise* |
| **P - Procedures** | Concrete implementation used during an attack               | *Infostealer malware*     |

## ATT&CK Matrix

The ATT&CK matrix lists tactics as columns with techniques below them.

## Use Cases

- Structuring [[Cyber Threat Intelligence]]
- Mapping known attacks onto TTPs (e.g. [[Advanced Persistent Threat]])
- Building better [[Threat Modelling|threat models]]
- Identifying defensive gaps

## Related Concepts

- [[Cyber Threat Intelligence]]: MITRE structures CTI analysis
- [[Indicator of Compromise]]: IoCs are tied to techniques and procedures
- [[Threat Modelling]]: MITRE ATT&CK enriches threat analysis
- [[Advanced Persistent Threat]]: APT groups are tracked in ATT&CK
