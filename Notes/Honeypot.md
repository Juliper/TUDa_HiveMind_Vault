---
title: Honeypot
aliases:
  - Honeypots
tags:
  - cybersecurity
  - network-security
  - threat-intelligence
description: "Decoy system designed to lure adversaries into exposing themselves by attacking it."
---

A **Honeypot** is a decoy system whose purpose is to lure adversaries to expose themselves by attacking it.

## Properties

- Not a real production service or VM
- Not made to be immediately visible (too obvious would be a red flag)
- Emulates deliberately vulnerable services
- Part of the [[Intrusion Detection System|IDS]] ecosystem

## Purpose

1. **IDS Component:** expose attackers that bypass traditional IDS/IPS systems
2. **Research:** deployed as canaries for researchers to learn new adversary TTPs (see [[MITRE ATT&CK]])

## Types

| Type | Description | Risk | Use Case |
|---|---|---|---|
| **High-Interaction** | Complete, realistic OS | High; complex to maintain | Research; captures complex adversary behavior |
| **Low-Interaction** | Only basic services and OS layers | Low; easy to deploy | Production; easily fingerprinted by sophisticated attackers |

## Advantages

- **High Fidelity Alerts:** honeypots receive no legitimate traffic, so any connection is almost always hostile
- **Efficiency:** no need to process large amounts of traffic
- **Intelligence Gathering:** potential source of novel adversary TTPs

## Disadvantages

- **Narrow field of view:** only sees attackers that reach it
- **Takeover risk:** if an attacker breaks out of containment, the honeypot becomes an attack vector into the production network
- **Fingerprinting:** simple honeypots can be identified as fake environments

## AI-Powered Honeypots

A major issue for traditional honeypots is lack of realism. Tools like Cowrie cannot properly emulate complex commands (e.g. `wget`).

GenAI/LLMs enable honeypots with maximally realistic behavior at relatively low cost:

- LLMs are great at pattern matching and reusing context: adversary sends a command, the LLM generates the appropriate response
- Example research: shelLM (Sladic et al., 2024) uses LLMs as shell-based honeypots

## Related Concepts

- [[Intrusion Detection System]]: honeypots complement IDS/IPS
- [[Cyber Threat Intelligence]]: honeypot data feeds CTI
- [[MITRE ATT&CK]]: novel TTPs from honeypots feed back into the database
