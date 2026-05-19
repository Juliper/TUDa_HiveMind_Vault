---
title: Device Drivers
aliases:
  - Gerätetreiber
tags:
  - operating-systems
  - io
description: "Device-specific kernel code that translates abstract OS operations into hardware-specific commands"
draft: false
---

> [!NOTE] Definition
> A device driver is device-specific code in the OS kernel that controls a hardware device by reading and writing its controller registers.

## Properties

- Each device controller exposes device registers
- The driver translates abstract operations (read/write) into concrete register manipulations
- Typically part of the OS kernel, written by the hardware manufacturer
- Must be **reentrant** - must function correctly despite interruptions

## Responsibilities

- Input parameter validation
- Translate abstract operations into concrete hardware addresses
- Queue requests if the device is busy
- Initialize device status
- Write to control registers and read status registers
- Block if the I/O operation requires waiting
- Error handling and possible transfer abort
- Forward device output to the calling software

## I/O Buffers

| Buffering Strategy | Description |
|-------------------|-------------|
| **Unbuffered** | Direct transfer - leads to many interrupts |
| **User-space buffer** | Reduces interrupts but can cause issues |
| **Kernel buffer** | Intermediate buffer; data copied to user buffer |
| **Double buffering** | Two kernel buffers - one being filled while the other is read |

## Spooling

A dedicated daemon process with exclusive device access (e.g., printer). Regular processes place files in a spooling directory; the daemon forwards them to the device, enabling shared access to exclusive devices.

## Related Concepts

- [[Interrupt-Verarbeitung]]: drivers are invoked as part of interrupt handling
- [[Programmed IO vs Interrupt-driven IO]]: the I/O modes drivers implement
