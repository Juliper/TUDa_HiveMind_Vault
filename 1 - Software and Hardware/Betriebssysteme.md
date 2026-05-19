---
title: BS
aliases:
  - Betriebssysteme
tags:
  - fb20
  - bachelor
  - pflichtmodul
  - semester-5
  - 5CP
description: "Grundlagen der Betriebssysteme: Prozesse, Speicherverwaltung, Scheduling, I/O, Sicherheit und Virtualisierung."
draft: false
---

# Syllabus

| Moodle       | Link        |
| ------------ | ----------- |
| Dozent       | -           |
| Prüfungsform | Klausur     |

## Lecture 1 - Einführung & Kernelarchitektur

### Grundlagen
- [[Aufgaben eines Betriebssystems]]
- [[System Design Prinzipien]]
- [[x86 Schutzringe]]

### Kernelarchitektur
- [[Monolithischer Kernel]]
- [[Microkernel]]

## Lecture 2 - Prozesse und Threads

### Prozesse
- [[Prozess vs Programm]]
- [[Prozesszustände]]
- [[Process Control Block]]
- [[Prozessspeicher und Stackframe]]
- [[Zombie und Orphan Prozesse]]
- [[User Mode und Kernel Mode]]

### System Calls
- [[System Calls]]
- [[POSIX Prozessverwaltung]]

### Threads
- [[User-Level vs Kernel-Level Threads]]
- [[Multithreading-Modelle]]
- [[Linux vs Windows Prozessmodell]]

## Lecture 3 - Scheduling

### Scheduling-Grundlagen
- [[Scheduling-Metriken]]
- [[Preemptive vs Non-preemptive Scheduling]]
- [[Context Switch]]

### Scheduling-Algorithmen
- [[Batch Scheduling]]
- [[Interactive Scheduling]]
- [[Realtime Scheduling]]

### Interrupts
- [[Interrupts]]
- [[Precise vs Imprecise Interrupts]]

## Lecture 4 - Memory Management

### Speicherabstraktion
- [[Speicherverwaltung ohne Abstraktion]]
- [[Fixed Partitions]]
- [[Variable Partitions]]
- [[Segmentierung]]

### Fragmentierung
- [[Interne und Externe Fragmentierung]]
- [[Allocation-Strategien]]
- [[Freispeicherverwaltung]]

### Paging
- [[Paging und Swapping]]
- [[Demand Paging vs Pre-Paging]]
- [[Translation Lookaside Buffer]]
- [[Multilevel Page Tables]]
- [[Page Table Entries]]

### Page Replacement
- [[Page Replacement Algorithmen]]
- [[Thrashing]]

## Lecture 5 - Caches

- [[Cache-Eigenschaften]]
- [[Write-hit und Write-miss Policies]]

## Lecture 6 - Interprocess Communication

### IPC-Mechanismen
- [[Message Passing IPC]]
- [[Shared Memory IPC]]
- [[Remote Procedure Call]]

## Lecture 7 - Synchronisation

### Probleme
- [[Race Conditions]]
- [[Critical Regions]]

### Lösungsansätze
- [[Lock-Variablen und Prozess-Alternation]]
- [[Petersons Solution]]
- [[Atomare Instruktionen]]
- [[Semaphore und Mutexes]]

## Lecture 8 - Deadlocks

- [[Resource Deadlock Conditions]]
- [[Deadlock-Strategien]]
- [[Bankers Algorithmus]]

## Lecture 9 - Device I/O

- [[Programmed IO vs Interrupt-driven IO]]
- [[Interrupt-Verarbeitung]]
- [[Device Drivers]]

## Lecture 10 - Security

### Schutzziele
- [[CIA Triad]]

### Sicherheitsmodelle
- [[Bell-LaPadula Modell]]
- [[Biba Modell]]
- [[Access Control List]]

### Angriffe
- [[Runtime-Angriffe]]
- [[Buffer Overflow]]

## Lecture 11 - File Systems

- [[Dateitypen und Dateistruktur]]
- [[Disk Partitions]]
- [[File Allocation-Typen]]

## Lecture 12 - Virtualisierung

- [[Hypervisor Typen]]

# Klausurvorbereitung
## Klausurfragen

Siehe [[Betriebssysteme Klausurfragen]] für eine Sammlung typischer Klausurfragen mit Musterantworten.

## Übungsaufgaben
<!-- Links zu Altklausuren, Übungsblättern o.ä. -->
