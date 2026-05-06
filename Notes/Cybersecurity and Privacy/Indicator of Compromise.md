---
title: Indicator of Compromise
aliases:
tags:
description: Digital forensic artifacts that indicate a system or network has been compromised.
---
An **Indicator of Compromise (IoC)** is a digital forensic artifact that indicates a system or network has been compromised.

## Types of IoCs

| Type | Examples |
|---|---|
| **Network-based** | IPs, domains, URLs, network patterns, port usage |
| **File-based** | Malicious or unfamiliar files, file hashes, malware binaries |
| **Host-based** | Suspicious processes, suspicious registry-key changes, unauthorized user accounts, log anomalies |
| **Behavioral-based** | Suspicious user behavior, irregular login patterns, irregular data transfer (exfiltration), lateral movement |

## Pyramid of Pain

The **Pyramid of Pain** illustrates the inverse relationship between the types of IoCs used by adversaries and the amount of "pain" or difficulty inflicted on them when defenders deny those indicators.

```
         TTPs              <- Tough! 
        Tools              <- Challenging
   Network/Host Artifacts  <- Annoying
      Domain Names         <- Simple
      IP Addresses         <- Easy
      Hash Values          <- Trivial
```

**Implication:** Blocking hash values is trivially circumvented (the attacker changes one byte). Blocking **TTPs** (Tactics, Techniques, Procedures) forces attackers to change their entire approach, which is significantly more expensive.

-> Effective defense targets the upper layers of the pyramid.

## Related Concepts

- [[Cyber Threat Intelligence]]: IoCs are the raw material for CTI
- [[MITRE ATT&CK]]: structures TTPs from real-world attacks
- [[Threat Modelling]]: IoCs feed into threat analysis
