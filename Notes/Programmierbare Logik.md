---
title: Programmierbare Logik
aliases:
  - PLA
  - PAL
  - FPGA
  - Field Programmable Gate Array
  - Programmable Logic Array
  - Programmable Array Logic
  - Logic Cell
  - LUT
tags:
  - digitaltechnik
  - logic
description: "Programmable logic devices — PLA, PAL, and FPGA architecture with logic cells, LUTs, IOBs, switch matrices, and function blocks."
---

**Programmierbare Logik** ermöglicht die Realisierung digitaler Schaltungen auf rekonfigurierbarer Hardware, ohne anwendungsspezifische Chips (ASICs) fertigen zu müssen.

## Performanz vs. Flexibilität

| Implementierung | Eigenschaft |
|---|---|
| **ASIC** | Maximale Performanz; optimierte Datenpfade; nicht änderbar nach Fertigung |
| **Software-Prozessor** | Maximale Flexibilität; generische Architektur; sequentielle Ausführung |
| **FPGA** | Kompromiss: Flexibilität eines Prozessors mit Performanz nahe ASIC; im Feld programmierbar |

## PLA (Programmable Logic Array)

Ein PLA realisiert kombinatorische Logik in **Sum-of-Products** (DNF) Form:

- **Eingabefeld** (AND-Plane): Programmierbare AND-Verknüpfungen erzeugen Produktterme (Implikanten)
- **Ausgabefeld** (OR-Plane): Programmierbare OR-Verknüpfungen kombinieren Produktterme zu Ausgängen

$$Y_i = \sum \text{(ausgewählte Produktterme)}$$

Beide Ebenen sind programmierbar → maximale Flexibilität bei zweistufiger Logik.

## PAL (Programmable Array Logic)

- **AND-Plane**: Programmierbar (wie PLA)
- **OR-Plane**: **Fest** verdrahtet (jeder Ausgang hat feste Anzahl Eingänge)

Günstiger als PLA, da nur eine Ebene programmiert werden muss; ausreichend für viele Anwendungen.

### Vergleich

| Baustein | AND-Ebene | OR-Ebene |
|---|---|---|
| **ROM** | Fest (Decoder = alle Minterme) | Programmierbar |
| **PLA** | Programmierbar | Programmierbar |
| **PAL** | Programmierbar | Fest |

## FPGA (Field Programmable Gate Array)

Ein FPGA ist ein Feld aus programmierbaren **Logikzellen**, verbunden durch ein programmierbares **Routing-Netzwerk**:

### Architektur-Übersicht

| Komponente | Abkürzung | Funktion |
|---|---|---|
| **Logic Cell** | LC | Kombinatorische Logik (LUT) + Speicher (FF) + Carry-Kette |
| **I/O Block** | IOB | Schnittstelle zu physikalischen Pins (Ein-/Ausgabe, Tristate) |
| **Switch Matrix** | SM | Programmierbare Leitungskreuzungen für Routing |
| **Function Block** | FB | Spezialisierte Ressourcen (BRAM, DSP, PLL, Kommunikation) |

### Programmierbare Schalter

Jeder programmierbareSchalter wird durch ein Konfigurationsbit ($C$) gesteuert:

| $C$ | Verhalten |
|---|---|
| 0 | Hochohmig ($Z$) — Verbindung getrennt |
| 1 | Durchgeschaltet — Signal wird weitergeleitet |

Implementiert als CMOS-Buffer mit Gate-Signal aus dem Konfigurationsspeicher.

### Konfigurationsspeicher

| Technologie | Eigenschaft |
|---|---|
| **SRAM-basiert** | Schnell beschreibbar; **flüchtig** (verliert Konfiguration bei Stromausfall); statische Leistungsaufnahme |
| **Flash-basiert** | Nicht-flüchtig (Konfiguration bleibt erhalten); aufwendiger zu beschreiben |

### Logic Cell (LC)

Eine Logic Cell enthält:

1. **LUT** (Lookup Table): Realisiert beliebige kombinatorische Funktion mit 2–6 Eingängen ([[Halbleiterspeicher|LUT als kleines Speicherfeld]])
2. **Flip-Flop**: Optionaler Ausgangsregister für sequentielle Logik
3. **Carry-In** ($C_{in}$): Spezielle Carry-Kette für schnelle [[Arithmetische Schaltungen|Arithmetik]]
4. **Konfigurations-MUX**: Wählt zwischen kombinatorischem ($Y$) und registriertem ($X$) Ausgang

### I/O Block (IOB)

- Verbindet interne Logik mit physikalischen **Pins** ($P$)
- **Output Driver** ($OD$) kann permanent oder per $OEN$-Signal deaktiviert werden (Tristate)
- Konfigurierbar: Spannungs-Level, maximale Stromstärke
- Eingang ($ID$) liest den Pin-Zustand

### Switch Matrix (SM)

Programmierbare Leitungskreuzungen, die durch ein Gitter von Schaltern realisiert werden. Jede Kreuzung kann individuell verbunden oder getrennt werden → flexibles Routing zwischen LCs und IOBs.

### Function Blocks (FB)

Häufig benötigte Spezialbausteine als dedizierte Ressourcen auf dem FPGA:

- **Block RAM (BRAM)**: Kleine SRAM-Speicher (wenige Kilobit)
- **DSP-Blöcke**: Multiplizierer und MAC-Einheiten für Signalverarbeitung
- **PLL** (Phase-Locked Loop): Taktmodifikation (Frequenzvervielfachung/-teilung)
- **Kommunikations-Treiber**: USART, USB, Ethernet
- **Kleine Prozessoren**: Embedded Soft-/Hard-Cores

### FPGA-Hersteller

| Hersteller | Produktfamilien |
|---|---|
| **Xilinx** (AMD) | Zynq, Virtex, Kintex, 7-series, UltraScale+ |
| **Intel** (ex Altera) | Cyclone, Aria, Stratix |
| **Microsemi** | IGLOO, SmartFusion, PolarFire, ProAsic |
| **Lattice** | iCE, Mach |

## Related Concepts

- [[Halbleiterspeicher]]: LUTs sind kleine Speicher; FPGA-Konfiguration nutzt SRAM/Flash
- [[CMOS]]: Programmierbare Schalter und LUTs basieren auf CMOS-Transistoren
- [[Kombinatorische Logik]]: LUTs realisieren beliebige Boolesche Funktionen
- [[Normalformen]]: PLA implementiert DNF direkt in Hardware
- [[Verilog]]: SystemVerilog wird in FPGA-Konfigurationen synthetisiert
