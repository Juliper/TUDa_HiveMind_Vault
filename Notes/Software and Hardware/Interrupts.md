---
title: Interrupts
aliases:
  - Hardware Interrupts
tags:
  - operating-systems
  - hardware
description: "Signals from hardware or software that notify the OS of events requiring attention"
draft: false
---

> [!NOTE] Definition
> An interrupt is a signal to the OS that an important event needs immediate attention. The CPU pauses the current process and handles the interrupt.

## Types of Interrupts

| Type | Trigger |
|------|---------|
| **Input Ready** | Device has data ready to be read |
| **Output Complete** | Device finished writing data |
| **Error Condition** | Hardware error (e.g., division by zero) |
| **Clock Interrupt** | Timer tick for [[Preemptive vs Non-preemptive Scheduling|preemptive scheduling]] |

## Interrupt Handling Steps

1. CPU checks the interrupt request line after each instruction
2. If an interrupt is pending, the current process state is saved (see [[Process Control Block]])
3. The interrupt is dispatched (interrupt dispatcher) and the appropriate handler is executed (interrupt handler)
4. If not a fatal error, the process state is restored and execution continues

## Interrupt Controller

- Devices send interrupt signals
- The interrupt controller prioritizes and forwards them to the CPU
- Each device is numbered; the number indexes the **interrupt vector table** containing handler information

## Related Concepts

- [[Precise vs Imprecise Interrupts]]: how cleanly the CPU state is preserved
- [[Context Switch]]: interrupts often trigger context switches
- [[Programmed IO vs Interrupt-driven IO]]: interrupts enable efficient I/O
