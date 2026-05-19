---
title: Hypervisor Types
aliases:
  - Hypervisor Typen
  - Virtualisierung
tags:
  - operating-systems
  - virtualization
description: "The two types of hypervisors for running multiple OS instances on a single machine"
draft: false
---

> [!NOTE] Definition
> A hypervisor (Virtual Machine Monitor) enables multiple operating systems to run simultaneously on the same physical hardware.

## Types

### Type 1 - Bare Metal
- Runs directly on hardware, no host OS
- Guest OSes run on top of the hypervisor
- Better performance and security
- Examples: VMware ESXi, Xen, Microsoft Hyper-V

### Type 2 - Hosted
- Runs as an application on top of a host OS
- Easier to set up, but additional overhead from the host OS layer
- Examples: VirtualBox, VMware Workstation

```mermaid
graph TD
    subgraph "Type 1"
        HW1[Hardware] --> HV1[Hypervisor]
        HV1 --> G1[Guest OS 1]
        HV1 --> G2[Guest OS 2]
    end
    subgraph "Type 2"
        HW2[Hardware] --> HOS[Host OS]
        HOS --> HV2[Hypervisor]
        HV2 --> G3[Guest OS 1]
        HV2 --> G4[Guest OS 2]
    end
```

## Use Cases

- Server consolidation
- Isolation between workloads
- Testing and development environments
- Cloud computing infrastructure

## Related Concepts

- [[User Mode und Kernel Mode]]: virtualization adds another privilege layer
- [[x86 Schutzringe]]: modern CPUs have hardware virtualization extensions
