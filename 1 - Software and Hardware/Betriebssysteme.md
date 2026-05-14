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
description: ""
draft: false
---
# Klausurfragen

## Welche Aufgaben hat ein OS?

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/882cb2c0-6c41-4d17-8968-9fb6e0764966/Untitled.png)

## Motivation für OS

- mehrere Programme für die gleiche Hardware
- gleiche Programme auf unterschiedlicher Hardware
- immer schneller werdende Entwicklung der Hardware
- immer größer werdenen Komplexität der Programme/Systeme

## OS

- Isolation und Hardwarezugriffkontrolle für Anwendungen
- Kontrolliert und optimiert Programmausführung und Resourcen Management
- Bietet Abstraktion (leichter für Entwicklung weil HW unwichtig)

## System Design

- Abstraction (Prozesse, Threads, …)
- Mechanisms (open, fork, create, …)
- Policies (Prozessausführung, Speichermanagment)

## Was sollte ein OS optimieren?

### Prozessorauslastung

Dies ist der Anteil der Zeit, in der die CPU mit der Ausführung von Anweisungen beschäftigt ist (1 P.). Um die Systemhardware optimal nutzen zu können, sollte dieses Kriterium maximiert werden (1 P.).

Auslastung = (1 - p ^ n)

### Durchsatz

Die Anzahl der pro Zeiteinheit abgeschlossenen Prozesse (1 P.). Dies sollte maximal sein (1 P.), sodass möglichst viele Prozesse bedient werden können.

### Bearbeitungszeit

Die Zeit, die ein Prozess benötigt von der Übermittlung eines Prozesses an das Betriebssystem bis zu seiner Fertigstellung (1 P.). Dies ist die Summe der Zeit, die ein Prozess im Status “Bereit” oder “Warten” verbringt plus der Zeit, die im laufenden Zustand verbracht wird. Dieses Kriterium sollte minimiert werden (1 P.).

### Reaktionszeit

Die Zeit, die ein Prozess benötigt, um seine erste Ausgabe zu erzeugen. Das Zeitintervall von der Übermittlung des Prozesses an das Betriebssystem bis zum Moment indem es beginnt zu reagieren (1 P.). Dieses Kriterium sollte insbesondere in interaktiven Systemen minimiert werden (1 P.).

## Welche Kernelarten gibt es?

- monolithischen := führt alle Betriebssystemdienste im Kernel aus
    - - bessere Leistung
    - - geringere Flexibilität und Zuverlässigkeit
- microkrenel := lagert viele dienste in benutzermodus aus
    - - bessere Modularität und Sicherheit

## Was sind x86-Architektur Schutzringe?

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/ce8ba2df-691b-4663-ac92-d1bb0c5f9e8c/Untitled.png)

---

## Welche Arten Prozess gibt es?

- zombie prozess := ist fertig aber noch nicht terminiert (nimmt speicher weg)
- orphan prozess := parent schon terminiert

Werden duch privilege bits angegeben:

- Usermode := Kann keine privileged operationen ausführen (→ Systemcalls)
- Kernelmode := Kann privileged operations ausführen

## Was sind Threads und Prozesse?

Programm ist passiver Code auf der Festplatte und ein Prozess ist die aktive Ausführung des Codes

Ein Prozess ist die Abstraktion eines ausgeführten Programms (1 P.). / Einheit die vom Betriebssystem zur Ausführung auf dem CPU geschedult wird (1 P). Innerhalb eines Prozesskontexts können mehrere Threads existieren (1P.). Threads teilen die Adress Space eines Prozesses.(1 P.)

## Linux vs. Windows

Während Windows zwischen Threads und Prozessen unterscheidet existieren in Linux nur Prozesse. Windows nutzt user-threads und kernel-threads mit einer eins zu eins Abbildung. In Linux werden Prozesse Tasks genannt. Je nach dem, wie die Tasks via clone() implementiert worden sind, benutzen diese gegebenfalls geteilte Ressourcen oder laufen in verschiedenen privilige rings. Informell kann man sagen, dass Linux nicht direkt das klassische Thread Modell implementiert, jedoch kann man mit clone() das ganze abstrahieren. Linux benutzt außerdem one-to-one mapping.

## Welche Zustände kann ein Prozess haben?

- new, ready, blocked, running, terminated

## Was sind System Calls?

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/0f9f667c-30d9-4a61-9db9-6af879d100d4/Untitled.png)

- Damit Programme services vom OS Kernel benutzen können
- Schnittstelle zwischen Prozess und OS
- hardwarebezogene Dienste (Speicherzugriff), prozesse (erstellen, ausführen)

Für read():

1. User-level prozess benutz syscall wrapper
2. The wrapper function places the system call number 0 in the accumulator register RAX and parameters in designated registers
3. The wrapper function calls a trap function to generate a software interrupt (exception)
4. Processor switches to kernel mode and invokes the syscall dispatcher
5. The syscall dispatcher looks up the syscall handler corresponding to the syscall number from the syscall table
6. The corresponding syscall handler processes the syscall
7. Control is returned to the calling wrapper function, processor retuns to user mode

## User vs. Kernel Level Threads

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/b778446a-7d52-48ba-aa97-c7355e6ed634/Untitled.png)

Threadtable := enthält program counter, stack pointer, registers, state, etc. für alle threads

### User level

- Komplett in User Space (OS unabhängig)
- Threadtable für jeden Prozess
- Effizient (threadswitching sehr fast weil ohne kernel)

### Kernel level

- nur ein Thread table von kernel gemanaged (aufwändiger)
- Can manage blocking system calls gracefully

## Was ist Multiprogramming?

### Pseudoparallelität

- mehrere Prozesse laufen scheinbar parallel
- Konzeptionell betrachtet hat jeder Prozess seine eigene „virtuelle CPU“
- CPU wechselt schnell zwischen Prozessen (Context Switching)

Mehrere Prozesse laufen parallel im System (1 P.) Wird dadurch erreicht, dass Prozesse in rapider abfolge abgewechselt werden (1 P.). Dadurch kann bessere Effizienz erzielt werden (1 P.)

## Was ist POSIX unter UNIX?

Portable Operating System Interface (POSIX)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/cd32478a-94e3-4df1-bccf-5c3dc817d9a9/Untitled.png)

### Unter UNIX

- fork := kopiert parent (gibt 0 zurück wenn child und child prozess id an parent), wenn failed dann negativ
- exec := läd programm in child und führt es aus
- wait := parent wartet bis child fertig
- kill := parent terminiert child

Ein elternprozess ruft den syscall fork auf (1 P.) und kreiert dadurch eine kopie von sich selbst (1 P.). Mithilfe des syscalls exec (1 P.) lädt das Kindprozess einen neuen Programmcode in den Prozess und startet es (1 P.).

## Wie funktioniert IPC?

### Message Passing-based IPC

- send und receive
- OS regelt alles → mehr overhead (syscalls)

### Shared Memory-based IPC

- Prozesse teilen sich bestimmten virtuellen speicher
- OS unabhängig → schneller
- Prozesse regeln Kommunikation

## Was sind I/O oder CPU bound Prozesse?

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/3d6695fb-9e41-4b34-9e57-a1fd3809c7a4/Untitled.png)

## Wie sieht Prozess Speicher und Stackframe aus?

### Speicheraufbau

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/4a172eb2-13a7-4de8-a745-e8f7f13c7eba/Untitled.png)

- Stack := temporäre Daten wie zum Beispiel Return-adressen, lokale Variablen und Funktionsparameter, LIFO, besteht aus frames für je einen Funktionsaufruf, wächst nach unten
- heap := Dynamisch verwalteter Speicherbereich, der wachsen und schrumpfen kann (nachoben), wenn der Prozess läuft
- Data := globale variablen und für alle prozesse zugänglich
- Text := programmcode

### Stackframe bei Funktionsaufruf

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/18c6f94e-deaf-470e-8bdb-3ac3dec5ea2d/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/6a72b073-7064-422a-a61a-f6cee3ec94fa/Untitled.png)

## Was ist ein Process Control Block?

- Program Counter := Adresse der nächsten Anweisung
- Register Content := Werte der CPU-Register
- Stack Pointer := aktuellen Zustand des Stacks (Funktionsaufrufe, lokale Variablen) des Prozesse
- Memory Allocations := Basisadresse und Größe des Speichers
- Open files := Eine Liste der Dateien, auf die der Prozess zugreift, und deren Zustand (geöffnet, geschlossen
- Accounting information := Informationen zur Ressourcennutzung und Laufzeit
- Planungsinformationen := Priorität des Prozesses in Warteschlange

## Welche Schritte bei Prozessstart?

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/ae80f0b1-4c6a-4dac-b58f-d072dda74c48/Untitled.png)

---

## Welche Arten von Memory Management gibt es?

## Keine Abstraktion

- Prozesse benutzten einfach physischen Speicher
- Nur ein Prozess gleichzeitig im Speicher
- Mit Swapping Parallelität möglich
- Problem: Absolute Adressen schlecht wenn Speicher sich ändert
    - → Static Relocation: Adressen vor Ausführung wird umgeschrieben

## Partitionierung

### Fixed

- Basisadressen der einzelnen Partitionen muss bekannt sein
- Physische Adresse = base adresse + logische adresse
- Einfach, fast context switch, aber interne fragmentierung

### Variable

- Basisadresse und Limit
- Physische adresse = Base + logische adresse (muss kleiner als limit + base sein)
- Problem externe fragmentierung

## Segmentierung

- Speicher wird in viele kleine Teile aufgeteilt und Prozessen zugeteilt
- Wieder base und limit
- Segment table base register (STBR) points to segment table’s location in memory and segment table length register (STLR) specifies the number of segments in a program
- keine interne Fragmentierung
- Jedes Segment muss aneinanderhängend im Speicher liegen aber nicht kompletter Adressraum
- Externe Fragmentierung möglich

## Was ist interne und externe Fragmentierung?

### interne Fragmentierung

Mit interner Fragmentierung bezeichnet man die Situation, in der eine Partition des Hauptspeichers einem Prozess zugeordnet ist, diese den Speicher aber nicht wirklich benutzt (1 P). Dabei ist dieser Speicher nicht für andere Prozesse verfügbar (1 P.). Dieses Problem kann bei einer statischen Parititionierung des Hauptspeichers (Fixed Partitions) auftreten (1 P.), in der alle Prozesse gleich große Partitionen des Hauptspeichers zugeordnet werden. Auch andere richtige beispiele können genannt werden.

### externe Fragmentierung

Externe Fragmentierung bezeichnet ein Problem, bei dem nach dem wiederholten Laden und Freigeben von Prozessen in den Hauptspeicher im Speicher verstreute unbenutzte ’Löcher’ entstehen (1 P.), die andere Prozesse nicht nutzen können (1 P.) Dieses Problem kann auftreten, wenn Prozesse Partitionen des Hauptspeichers variabler Größe zugeordnet werden (variable partitions) (1 P.) Auch andere richtige beispiele können genannt werden.

## Was sind allocation Strategien?

- First fit := erstes das passt
- next fit := wie first fist aber suche startet bei letzem endpunkt
- Best fit := wählt kleinstes Element dass groß genug
- Worst fit := nimmt größtes Segment
- Quick fit := erstellt liste um löcher zu organisieren nach größe

## Logische Adresse in physische Umwandeln

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/c415ea1c-5465-4cb8-8e89-c76b784b93b6/Untitled.png)

- Offset darf nicht größer als Limit sein
- Erster Hexwert von logischer Adresse entspricht Segmentnummer
- Physische Adresse := Basis + Offset

## Was ist ein TLB?

MMU stores a cache of recently used mappings from the operating system’s page table

## Was ist Swapping und Paging?

Wenn sich zu viele Prozesse im Hauptspeicher befinden, sodass nicht genügend Speicher für alle verfügbar ist, kann der Speicherinhalt eines Prozesses der gerade nicht läuft (1 P.) auf die Festplatte kopiert werden (1 P.) Dadurch steht mehr Hauptspeicher für andere Prozesse zur Verfügung (1 P.).

Bei Swapping wird der Speicher eines gesamten Prozesses aus dem Hauptspeicher verbannt (1 P.). Bei Paging betrifft dies lediglich eine Memory page eines Prozesses (1 P.)

## Wie merken wo freier Speicher?

- Bitmaps := Speicher wird in allocation units eingeteilt die mit 0 (frei) und 1 (belegt) getagt werden
- linked list := Speicher segment zeigen aufeinander und merken sich start position und länge

## Memory Management Requirements

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/9662e6d0-58b3-4085-8720-b29fa4eeacbf/Untitled.png)

---

## Welche Scheduling Arten gibt es?

### Metriken

- turnaround time := Endzeit - Startzeit (beinhaltet auch wartezeit)
- reaction time := Startzeit - Start Ausführung
- wait time := alle Wartezeiten addieren

### Batch

- non-preemptive scheduling or preemptive with very long time slices
- wenig context switching → mehr leistung
- soviele jobs wie möglich ausführen
- turnaround time (Zeit von job submit bis complete) minimieren
- hohe CPU Auslastung
- First Come First Served, Shortest Job First, Shortest Remaining Time Next

### Interactive

- Für Systeme mit Usern die auf antwort warten
- Geringe respone time
- kleine jobs sollen schnell sein und bei großen okay wenn länger dauert
- Round Robin := Prozesse stellen sich in Warteschlange an und erhalten ein Quantum Zeit für Berechnungen, dann stellen sie sichw wieder hinten an
- Priority := Zuerst Prozesse mit hoher Priorität ausführen
- Multiple Queues := Priority aber Prozesse werden demoted wenn einmal ausgeführt
- Shortest Process := Process with estimated shortest running time scheduled next
- Guaranteed := Each user out of 𝒏 users is guaranteed to receive 𝟏/𝒏 of CPU time
- Lottery := wie lotto lol
- Fair-Share:= Each user gets a specified fraction of CPU time, regardless of the number of processes it has

### Realtime

- Systeme mit strikten Zeitanforderungen (Multimedia)
- Muss vorhersehbar sein

## Page Replacements Algorithmen

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/11954bcd-3367-4262-87b3-b9f0d320458d/Untitled.png)

### Page Table Entries (PTE)

- Present bit: is page in physical memory or not
- Protection bits: access privileges to page (read/write/execute)
- Modified bit (also called dirty bit): 1 = modified ; 0 = not
- Referenced bit: tells whether page has been referenced for reading or writing
- Caching disabled bit: indicates that page shall not be cached

### Optimal

- evict the page that is least likely to be referenced in the near future

### Not Recently Used

- R=0, M=0 > R=0, M=1 > R=1, M=0 > R=1, M=1

### First-In, First-Out

- When page fault occurs, the page that has been longest in memory is evicted

### Second-Chance

- Wie FIFO aber wenn R = 1:
- Then R bit is set to zero and oldest page is moved to the end of the linked list, as if it were a new page

### Clock

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/f5d1ebfa-368b-4524-af2d-e39e01d9e3c1/Untitled.png)

### Least Recently Used

- When page fault occurs, evict page frame that has been unused for the longest amount of time

### Not Frequently Used

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/5ac106f4-a92e-44bb-ae8b-82142b9379a0/Untitled.png)

### Ageing

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/883d616a-a8ad-4317-84b9-3747bd62bfd1/Untitled.png)

### Working Set

### WSClock

### Thrashing

## Was ist ein Context Switch?

### Schritte

1. PCB wird gespeichert
2. Anderes PCB wird geladen

### Vor und Nachteile

- Bei vielen Context Switches Performance einbuße
- Ermöglicht Multiprogramming (Pseudoparallelität)

## Was sind Write-hit Policies

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/3917a6b1-f7c2-46e3-84c9-e709a299ff1a/Untitled.png)

## Was sind Write-miss Policies

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/4098816e-063b-49b1-8c91-6fff5384c974/Untitled.png)

## Welche Cache Eigenschaften gibt es?

- Split := Getrennter Cache für Instruction und Data
- Unified := Nur ein Cache für beides
- Inclusive := Daten werden im Core Cache und geteilten Cache gespeichert
- Exclusive := Daten nur im Core Cache oder geteiltem Cache
- Non-exclusive := Daten können in beiden Caches sein

## Demanding vs. Pre Paging

Wenn Demand-Paging genutzt wird, werden Pages erst dann in den physischen Speicher geladen (oder angelegt), wenn der Prozess versucht auf sie zuzugreifen. Bei Pre-Paging versucht das System, vorauszuberechnen welche Pages benötigt werden und lädt diese in den Speicher bevor der Prozess tatsächlich versucht auf sie zuzugreifen.

---

## Was sind critical Regions?

Ein kritischer Abschnitt ist ein Codesegment (1 P.), der eine geteilte Variable, Speicher oder Datei bearbeitet oder ausliest (1 P.). Es muss sichergestellt werden, dass immer nur ein Prozess(1 P.) sich im kritischen Abschnitt befindet bzw. diesen ausführt (1 P.)

## Was sind Deadlocks und Livelocks?

- Resource deadlocks: concurrent processes blocking each other while waiting for resources to become available

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/9e87704e-201b-4a82-bdc2-d1157fed055f/Untitled.png)

## Was sind Semaphores?

## Was ist Biba Model?

## Was ist ein Bell-LaPadula Seurity Modell?

## Was sind Race Conditions?

Eine Wettlaufsituation entsteht, wenn zwei Prozesse geteilte Daten modifizieren oder auslesen (z.B. geteilte Variablen). (1 P.) Die Wettlaufsituation ist vorhanden, wenn die zeitliche Abfolge wann einzelne Schritte der Prozesse durchgeführt werden, einen Einfluss auf das Endgültige Resultat haben. (1 P.)

## Was ist ACL (Access control list)?

## Nutzerauthentifizierung?

## Welche I/O Mechanismen gibt es?

### Programmed I/O

Programmed I/O: I/O Datentransfer zu Gerät wird direkt vom CPU kontrolliert / durchgeführt (1 P.) CPU ist in einem busy wait loop und fragt ständig den Statusregister des devices ab (1 P.) Nachteil: CPU muss im Busy-wait warten, bis Daten vom Gerät bereit sind / Verbraucht sehr viel CPU-Zeit (1 P.).

### Interrupt-driven I/O

Interrupt-driven I/O: Der I/O ausführende Prozess wird geblockt, bis die Daten vom Gerät bereitstehen. (1 P.) Wenn die Daten bereitstehen, generiert das Gerät einen Interrupt, der den CPU benachrichtigt / durch den der wartende Prozess wieder aktiviert wird (1 P.) Vorteil: Während des I/O vorganges kann der Scheduler andere Prozesse weiterlaufen lassen (1 P.).

# Zusammenfassung

## Binärzahlen

- Einerkomplement := negative zahlen normal darstellen und dann bitflip
- Zweikomplement := negative zaheln normal, bitflip und +1

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/93a78d07-0205-4fd3-808c-51549a20d7be/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/30928420-3185-40ea-92d1-41a1b20c1670/Untitled.png)

# Scheduling and Threads

### Interrupts

- Signal für OS dass ein wichtiges Event needs care

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/b125e562-4dbd-4e4e-9a2c-8655827452a4/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/6ece17ba-e4f2-40a6-861d-867445607c0d/Untitled.png)

## Clock interrupts

- Non-preemptive := Jeder Prozess läuft bis er blockiert oder freiwillig CPU freigibt
- Preemptive := Prozesse bekommen Zeit zugeteilt

## Context switch

1. PCB speichern
2. Anderes PCB laden

## Wann Schedule

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/681554e8-e93f-4b61-bb6d-591f0ac826de/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/3b5d1c9c-8c13-4bab-bb81-aea4f095ebfa/Untitled.png)

## Multithreading modelle

- many-to-one: Viele User Threads werden durch einen Kernel Thread organisiert
- one-to-one: Jeder User Thread wird durch einen Kernel Thread organisiert
- many-to-many: Viele User Threads werden durch eine Menge Kernel Threads organisiert

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/de4d63b1-552d-40e3-9f4c-5209024316c3/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/014f7016-23fa-430b-b780-e79045d0e4a7/Untitled.png)

# File Systems (fehlt)

abstractions of data blocks on disk

- Anzahl Prozesse = (2 ^ BaseLimitRegister - OS) / 2 ^ logische Adress Bits
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/bb121e5a-0033-40cf-8c5b-9e7d5e6f3944/Untitled.png)
    
- Letzte Segment Adresse = Base - Length - 1
    

## File Types

- Regular files, Directories, Character special files (I/o devices), Block special files (disks)

## File Naming

- UNIX Case sensitive / MS-DOS nicht
- Dateiendungen bei UNIX unwichtig / MS wichtig

## File Structure

- Byte oriented, record, tree structure

Zugriffsarten und alle operationen fehlen

## Disk Partitions

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/6111139b-3e75-46ef-85ed-d590d388f252/Untitled.png)

## Allocation Types

- Contiguous := Datei ebsteht aus zusammenhängenden Blocks auf disk
    - external fragmentation
    - max size muss vorher bekannt sein
- Linked-list := Zeigen immer auf nächsten Block
    - keine externe fragmentierung
    - nur erste block adresse muss bekannt sein
    - random access sehr slow

## Multilevel Pagetables

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/e31c2a01-6906-4d2f-9557-2ea8a921e8db/Untitled.png)

- PTE Größe = PFN + Verwaltungsbits
- PDE Größe = PFN + Verwaltungsbits
- PFN = Phys. Bits - 16 (Page Offset)

# Interprocess Communication (IPC)

## Remote Procedure Call (RPC)

- proxy (stub) bei client und server
- failen oft (Duplikate müssen vermieden werden)
- Server muss sich informationen merken um Duplikate zu löschen
- ACK nötig
- Client muss unacknowledged RPC neu senden

## Race Condition

- zwei oder mehr prozesse bearbeiten geteilten speicher
- ergebnis hängt von schnelligkeit ab

## Critical Regioan

- Wo prozesse geteilten speicher bearbeiten
- Gegen Race conditions
    - No two processes may be simultaneously inside their critical regions
    - No assumptions may be made about speeds or the number of CPUs
    - No process running outside its critical region may block other processes
    - No process should have to wait forever to enter its critical region.
    - Interrupts disablen innerhalb dieser

## Lock variablen

- variable die angibt ob ein prozess in critical region

## Prozess alternation

- turn variable zeigt an welcher prozess dran ist

## Peterson Solution

- turn variable und interested array(prozess gibt an ob er will)
- Only if turn == i and the other process’ flag is not set, may process i proceed to the critical region

## Atomic instructions

- CPU Instructions für mutual exclusion

## Sleep and wakeup

- Wenn prozess auf critical region warten werden sie geblockt und dann wieder geweckt

## Semaphore/Mutexes/cond variables/monitor

idkkkk

# Deadlocks

## Resources Typen

- Preemptable := Resourcen die ohne nachteile prozessen einfach genommen werden können
- Non-preemptable := Resourcen die man nicht einfach nehmen kann

## Resource Deadlock Conditions

1. Mutual exclusion := Jeder Resource ist genau einem Prozess zugewiesen oder free
2. Hold and wait := Processes currently holding resources granted earlier can request additional resources
3. No pre-emption := Resources previously granted cannot be forcibly taken away from a process
4. Circular wait condition := There must exist a circular list of processes each of which is waiting for a resource held by the next member of the chain

## Deadlock vermeiden

- Ignorieren, falls nicht wahrscheinlich oder wirtschaftlich
- Detection mittels Resource allocation graph (Zyklen) Algo fehlt
- Avoidance := System gibt resourcen nur frei wenn sicher
    - State ist sicher wenn es eine Fahrplan gibt ohne deadlocks
    - Bankers Algorithmus gibt nur resource wenn sicher

## Deadlock Recovery

- Pre-emption := Resourcen wegnehmen
- Killing process := Prozesse beenden um resourcen freigeben
- Rollback := Prozess speichern Checkpoint und bei deadlock können sie dahin zurückgesetzt werden

# Caches & Memory Allocation

## Cachearten

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/07c50bc9-a904-48c4-981c-01a46bc8fad4/Untitled.png)

# Run-time attacks

Programm wird während bösartig Laufzeit (Binaries die auf disk liegen werden nicht angepasst)

## Attackarten

- Denial Of Service
- Remote code execution
- Privilege escalation
- Buffer-Overflow Vulnerability

# Device I/O

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/c602c013-86f6-40cf-bdab-2ace865eb7b7/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/f5ed50d2-6498-4be0-ba5e-6c770a8d0635/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/9d4d6183-5efa-49dd-8f7a-9c52b3d54723/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/812f8031-3973-4a65-8bba-dd82c8ef73ef/Untitled.png)

1. Device Interrupt
2. Interrupt Controller bestimmt welcher device interrupt als erstes behandelt wird und leitet an CPU weiter
3. CPU behandelt interrupt (Speichert aktuellen Prozess und behandelt dann Interrupt)

## Interrupttypen

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/2a8cb17d-bb8d-4cfc-8772-76cf51d2dad6/Untitled.png)

- Precise := Program Counter saved, alle Instructions vor PC ausgeführt, alle nach PC nicht ausgeführt, Ausführungsstand der PC Instruction ist bekannt
- Imprecise := Gegenteil :D (braucht viel mehr Informationen um aktuellen Zustand abzubilden)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/7fb1a055-c95d-4c9f-af64-83a61e3ede5c/Untitled.png)

## Device Drivers

- device controller exposes device registers
- device-specific code required to use these registers for controlling the device is called the device driver
- part of the operating system kernel
- Device driver must handle gracefully the termination of current transfer and cancellation of possible pending requests to that device

## Programmed I/O

- CPU macht Datentransfer
- CPU überprift in einem busy wait loop ständig Register ab bis Daten bereit
- Verbraucht viel CPU Zeit weil sie einfach nur wartet

## Interrupt-driven I/O

- I/O Prozess geblockt bis device bereit
- Device schickt interrupt wenn rdy
- Waitng Prozess geht weiter
- CPU kann während wait anders benutzt werde

# Security

## Security Goals

- Confidentially := Daten vor Unbefugten schützen
- Integrity := Daten vo unbefugter Änderung schützen
- Availability := DoS und so

## Zugriffsverwaltungen

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/9b0aabfc-95a5-4000-8bc0-b5f348d9e017/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/092fa87d-be16-42aa-8e8a-7b920b09fb67/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/457eede4-d8a3-4efe-a634-0ec0350e8f7f/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/a09ea4ff-9466-4238-98d3-7b090529bef0/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/a8f10869-43c9-47bd-a02c-bc65106576bf/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/9955e2de-8817-477c-840e-4d8182ad0db6/Untitled.png)

# Virtualisation

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/4eb9f56d-c4af-4e6b-873d-a4cf51a99679/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/8236894d-0977-4f80-9141-989c9f6017b4/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/fd5e30be-baf2-4075-befe-6da5544607ab/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/c518e2dc-a8f2-435f-8e00-bb3f2140e673/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/bac079f3-e2af-4717-bf10-ba43d61b65d2/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/9223737b-a400-4d68-8c5f-998dd365ea22/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/258b0893-e3dc-41e3-856a-671925eb7753/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/5c72d3cf-e8bd-48b7-952e-f64af72b86a6/Untitled.png)