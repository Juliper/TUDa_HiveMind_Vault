---
title: Advanced Persistent Threat
aliases:
  - APT
  - APT Group
tags:
  - cybersecurity
  - threat-intelligence
description: "Well-resourced, often state-sponsored adversaries that compromise high-value targets over multi-year campaigns."
---

**Advanced Persistent Threats (APTs)** are well-resourced and trained adversaries that conduct multi-year intrusion campaigns targeting highly sensitive economic, proprietary, or national security information.

**APT Groups** are threat actors capable of launching APT-like sophisticated attacks. They are often directly operated by nation-states or are state-sponsored groups. Rarely, APTs act as ordinary cybercriminals.

## APT Attack Phases

1. **Incursion**: enter the network via social engineering or malware on vulnerable systems
2. **Discovery**: move "low and slow"; map the internal network, analyze defenses, build parallel kill chains
3. **Capture**: access unprotected systems; collect data over an extended period; install malware for persistent access
4. **Exfiltration**: send collected information back to the attacker base for further analysis and exploitation

## Case Study: APT29 vs. SolarWinds (2020)

**APT29** (also known as Cozy Bear) is a Russian APT group.

The 2020 SolarWinds attack was an exceptional supply-chain attack:

1. SolarWinds Orion software update compromised with a malicious binary (SUNBURST). Over 18,000 organizations install the trojanized update
2. SUNBURST activates 12 to 14 days after installation, after validating the environment
3. DNS lookups establish a custom HTTPS C2 tunnel
4. Full Cobalt Strike C2 tunnel installed; hands-on-keyboard reconnaissance
5. Domain admin credentials obtained via AD tools
6. SAML signing certificate stolen; SAML tokens forged; Azure AD accessed with admin permissions
7. Federation trust modified for long-term access
8. O365 tools used for data exfiltration (March to December 2020)

## Related Concepts

- [[MITRE ATT&CK]]: APT groups and their TTPs are tracked in ATT&CK
- [[Cyber Threat Intelligence]]: APT activity is a primary CTI source
- [[Indicator of Compromise]]: APT activity leaves characteristic IoCs
- [[Secure by Design]]: principles that make APT attacks harder (compartmentalization, least privilege)
