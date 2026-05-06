---
title: Threat Modelling
aliases:
tags:
description: Structured process to identify, quantify, and address security risks.
---

**Threat Modelling** is a structured process to identify, quantify, and address security risks in a system. It can be applied to software, architectures, processes, and data.

## The Four Driving Questions

1. **What are we working on?** -> identify the asset to defend
2. **What can go wrong?** -> define risks and threats
3. **What are we going to do about it?** -> threat mitigation or elimination; balance security and functionality
4. **Did we do a good job?** -> validate and test

## STRIDE

**STRIDE** is a framework developed by Microsoft for identifying and categorizing computer security threats. It helps developers think like attackers during system design.

| Letter | Threat Type | Description |
|---|---|---|
| **S** | Spoofing | Pretending to be someone or something else |
| **T** | Tampering | Modifying data or code without authorization |
| **R** | Repudiation | Denying that an action took place |
| **I** | Information Disclosure | Leaking sensitive data to unauthorized parties |
| **D** | Denial of Service | Making services or data unavailable to clients |
| **E** | Elevation of Privilege | Gaining unpermitted access to data, hosts, or networks |

> STRIDE maps directly to the [[CIA Triad]]: S->Authenticity, T->Integrity, R->Non-Repudiation, I->Confidentiality, D->Availability, E->Integrity/Availability.

## PASTA

**PASTA** (Process for Attack Simulation and Threat Analysis) is a risk-centric threat model focused on the most relevant risks to a protected asset.

1. Define Objectives
	- Identify business and process objectives
	- Identify critical services
	- Define regulatory and compliance objectives
2. Define Technical Scope
	- Define the attack surface
	- Define the system architecture
	- Identify all infrastructure components (codebase, databases, external APIs, PKI, OS)
3. Application Decomposition & Analysis
	- Define system components and trust boundaries
	- Define use-cases, user roles, and permissions
	- Define data-flow boundaries
4. Threat Analysis
	*  Like 3.
5. Weakness & Vulnerability Analysis
	- Define attack scenarios
	- Identify vulnerability sources
	- Run code reviews and vulnerability scans
6. Attacks Modeling & Simulation
	- Identify attack vectors and simulate attacks
7. Risk Analysis & Management
	- Calculate the risk
	- Identify mitigations based on the risk assessment

## Related Concepts

- [[CIA Triad]]: STRIDE maps to CIA goals
- [[What is Cybersecurity?]]: core vocabulary
- [[Indicator of Compromise]]: what to observe after a successful compromise
- [[MITRE ATT&CK]]: database of real-world tactics and techniques used in threat modelling
