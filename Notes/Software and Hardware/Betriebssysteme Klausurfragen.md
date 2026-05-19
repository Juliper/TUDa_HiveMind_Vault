---
title: Betriebssysteme Klausurfragen
aliases:
  - BS Klausurfragen
tags:
  - betriebssysteme
  - klausurvorbereitung
description: "Sammlung typischer Klausurfragen und Musterantworten für das Modul Betriebssysteme."
draft: false
---

## Welche Aufgaben hat ein OS?

- Isolation und Hardwarezugriffskontrolle für Anwendungen
- Kontrolliert und optimiert Programmausführung und Ressourcenmanagement
- Bietet Abstraktion (erleichtert Entwicklung, da Hardware-Details verborgen werden)

## Motivation für ein OS

- Mehrere Programme für die gleiche Hardware
- Gleiche Programme auf unterschiedlicher Hardware
- Immer schneller werdende Entwicklung der Hardware
- Immer größer werdende Komplexität der Programme/Systeme

## Was sollte ein OS optimieren?

### Prozessorauslastung

Anteil der Zeit, in der die CPU mit der Ausführung von Anweisungen beschäftigt ist. Sollte maximiert werden, um die Hardware optimal zu nutzen.

$$\text{Auslastung} = 1 - p^n$$

wobei $p$ die Wahrscheinlichkeit ist, dass ein Prozess auf I/O wartet und $n$ die Anzahl der Prozesse.

### Durchsatz

Anzahl der pro Zeiteinheit abgeschlossenen Prozesse. Sollte maximiert werden.

### Bearbeitungszeit (Turnaround Time)

Zeit von der Übermittlung eines Prozesses an das OS bis zu seiner Fertigstellung. Summe aus Wartezeit und Laufzeit. Sollte minimiert werden.

### Reaktionszeit (Response Time)

Zeit von der Übermittlung bis zur ersten Ausgabe des Prozesses. Sollte insbesondere in interaktiven Systemen minimiert werden.

## Welche Kernelarten gibt es?

- **Monolithisch**: Führt alle OS-Dienste im Kernel aus. Bessere Leistung, aber geringere Flexibilität und Zuverlässigkeit.
- **Microkernel**: Lagert viele Dienste in den Benutzermodus aus. Bessere Modularität und Sicherheit, aber mehr Overhead durch IPC.

## Was sind x86-Architektur Schutzringe?

Vier Privilegierungsebenen (Ring 0–3):
- **Ring 0** (Kernel Mode): Voller Hardwarezugriff
- **Ring 1–2**: Selten genutzt (z.B. Gerätetreiber)
- **Ring 3** (User Mode): Eingeschränkter Zugriff, muss System Calls nutzen

## Welche Arten von Prozessen gibt es?

- **Zombie-Prozess**: Ist beendet, aber noch nicht aus der Prozesstabelle entfernt (belegt Speicher)
- **Orphan-Prozess**: Parent-Prozess wurde bereits terminiert

Privilegierungsmodi:
- **User Mode**: Kann keine privilegierten Operationen ausführen → muss System Calls nutzen
- **Kernel Mode**: Kann privilegierte Operationen ausführen

## Was sind Threads und Prozesse?

Ein **Programm** ist passiver Code auf der Festplatte. Ein **Prozess** ist die aktive Ausführung dieses Codes — die Einheit, die vom OS zur Ausführung auf der CPU geschedult wird.

Innerhalb eines Prozesskontexts können mehrere **Threads** existieren. Threads teilen sich den Adressraum eines Prozesses.

## Linux vs. Windows Prozessmodell

Während Windows explizit zwischen Threads und Prozessen unterscheidet (mit 1:1 User-to-Kernel-Thread-Mapping), existieren in Linux nur Tasks. Je nachdem wie Tasks via `clone()` erstellt werden, teilen sie sich Ressourcen oder nicht. Linux implementiert kein klassisches Thread-Modell direkt, abstrahiert es aber über `clone()`. Beide nutzen One-to-One Mapping.

## Welche Zustände kann ein Prozess haben?

`new` → `ready` → `running`/`blocked` → `terminated`

Aus `running` kann ein Prozess auch nach `blocked` wechseln (z.B. bei I/O-Warten) und von dort zurück nach `ready`.

## Was sind System Calls?

Schnittstelle zwischen Prozess und OS-Kernel, damit Programme Kernel-Services nutzen können.

**Ablauf am Beispiel `read()`:**

1. User-Level-Prozess ruft Syscall-Wrapper auf
2. Wrapper legt Syscall-Nummer in Register `RAX` und Parameter in vorgesehene Register
3. Wrapper löst Software-Interrupt (Trap) aus
4. Prozessor wechselt in Kernel Mode und ruft Syscall-Dispatcher auf
5. Dispatcher sucht den Handler anhand der Syscall-Nummer in der Syscall-Tabelle
6. Handler verarbeitet den Syscall
7. Kontrolle wird an den Wrapper zurückgegeben, Prozessor kehrt in User Mode zurück

## Was ist Multiprogramming?

Mehrere Prozesse laufen **pseudoparallel** im System. Die CPU wechselt in schneller Abfolge zwischen Prozessen (Context Switching). Konzeptionell hat jeder Prozess seine eigene „virtuelle CPU". Dadurch wird bessere CPU-Auslastung erzielt.

## POSIX-Prozessverwaltung unter UNIX

- `fork()`: Kopiert den Parent-Prozess. Gibt 0 im Child zurück, die Child-PID im Parent. Bei Fehler negativ.
- `exec()`: Lädt ein neues Programm in den Prozess und führt es aus.
- `wait()`: Parent wartet, bis Child beendet ist.
- `kill()`: Sendet Signal an einen Prozess (kann zur Terminierung führen).

## Wie funktioniert IPC?

### Message Passing

- Kommunikation über `send()` und `receive()`
- OS regelt alles → mehr Overhead durch Syscalls

### Shared Memory

- Prozesse teilen sich einen virtuellen Speicherbereich
- OS-unabhängig nach Einrichtung → schneller
- Prozesse müssen Synchronisation selbst regeln

## Was ist interne und externe Fragmentierung?

### Interne Fragmentierung

Eine Partition ist einem Prozess zugeordnet, aber der Prozess nutzt nicht den gesamten zugewiesenen Speicher. Der ungenutzte Bereich ist für andere Prozesse nicht verfügbar. Tritt bei **Fixed Partitions** auf.

### Externe Fragmentierung

Nach wiederholtem Laden und Freigeben von Prozessen entstehen verstreute freie Speicherbereiche, die einzeln zu klein für neue Prozesse sind. Tritt bei **Variable Partitions** und Segmentierung auf.

## Was sind Allocation-Strategien?

- **First Fit**: Erstes Loch, das groß genug ist
- **Next Fit**: Wie First Fit, aber Suche startet beim letzten Endpunkt
- **Best Fit**: Kleinstes Loch, das noch groß genug ist
- **Worst Fit**: Größtes verfügbares Loch
- **Quick Fit**: Organisiert freie Löcher nach Größe in separaten Listen

## Was ist ein TLB?

Translation Lookaside Buffer — ein Cache in der MMU, der kürzlich verwendete Zuordnungen aus der Page Table speichert, um die Adressübersetzung zu beschleunigen.

## Was ist Swapping und Paging?

Wenn zu viele Prozesse im Hauptspeicher sind, kann der Speicherinhalt eines inaktiven Prozesses auf die Festplatte ausgelagert werden.

- **Swapping**: Der gesamte Speicher eines Prozesses wird ausgelagert
- **Paging**: Nur einzelne Pages eines Prozesses werden ausgelagert

## Was sind Critical Regions?

Ein kritischer Abschnitt ist ein Codesegment, das auf geteilte Ressourcen (Variablen, Speicher, Dateien) zugreift. Es muss sichergestellt werden, dass zu jedem Zeitpunkt nur ein Prozess den kritischen Abschnitt ausführt (Mutual Exclusion).

## Was sind Race Conditions?

Eine Wettlaufsituation entsteht, wenn zwei oder mehr Prozesse geteilte Daten gleichzeitig modifizieren oder auslesen und das Endergebnis von der zeitlichen Abfolge der einzelnen Operationen abhängt.

## Was sind Deadlocks und Livelocks?

**Deadlock**: Mehrere Prozesse blockieren sich gegenseitig, weil jeder auf eine Ressource wartet, die ein anderer hält.

**Livelock**: Prozesse ändern ständig ihren Zustand als Reaktion aufeinander, kommen aber trotzdem nicht voran.

## Was ist ein Context Switch?

1. PCB (Process Control Block) des aktuellen Prozesses wird gespeichert
2. PCB des nächsten Prozesses wird geladen

**Vorteile**: Ermöglicht Multiprogramming (Pseudoparallelität)
**Nachteile**: Bei zu vielen Context Switches Performance-Einbuße

## Welche I/O-Mechanismen gibt es?

### Programmed I/O

CPU kontrolliert den Datentransfer direkt. CPU fragt in einem Busy-Wait-Loop ständig das Statusregister des Geräts ab. **Nachteil**: Verschwendet viel CPU-Zeit.

### Interrupt-driven I/O

Der I/O-Prozess wird blockiert, bis die Daten bereitstehen. Das Gerät erzeugt einen Interrupt, wenn es fertig ist. **Vorteil**: CPU kann während des Wartens andere Prozesse ausführen.

## Demand Paging vs. Pre-Paging

- **Demand Paging**: Pages werden erst geladen, wenn der Prozess darauf zugreift (Page Fault löst Laden aus)
- **Pre-Paging**: Das System versucht vorherzusagen, welche Pages benötigt werden, und lädt sie vorab

## Was ist ein Process Control Block (PCB)?

Enthält alle Informationen, die das OS über einen Prozess speichert:

- **Program Counter**: Adresse der nächsten Anweisung
- **Registerinhalte**: Werte der CPU-Register
- **Stack Pointer**: Zustand des Stacks
- **Speicherzuweisungen**: Basisadresse und Größe
- **Offene Dateien**: Liste der Dateien und deren Zustand
- **Accounting-Informationen**: Ressourcennutzung und Laufzeit
- **Scheduling-Informationen**: Priorität in der Warteschlange

## Logische Adresse in physische umwandeln (Segmentierung)

1. Erster Teil der logischen Adresse = Segmentnummer
2. Restlicher Teil = Offset
3. Offset darf nicht größer als das Limit des Segments sein
4. **Physische Adresse** = Basisadresse des Segments + Offset

## Resource Deadlock Conditions

Alle vier Bedingungen müssen gleichzeitig gelten:

1. **Mutual Exclusion**: Jede Ressource ist genau einem Prozess zugewiesen oder frei
2. **Hold and Wait**: Prozesse halten Ressourcen und fordern zusätzliche an
3. **No Pre-emption**: Zugewiesene Ressourcen können nicht entzogen werden
4. **Circular Wait**: Es existiert eine zirkuläre Kette wartender Prozesse
