---
title: CMOS
aliases:
  - CMOS-Technologie
  - Complementary MOS
  - NMOS
  - PMOS
  - Transmission Gate
  - Pseudo-NMOS
  - Tristate
tags:
  - digitaltechnik
  - logic
description: "CMOS gate construction — NMOS/PMOS as switches, complementary pull-up/pull-down networks, complex gates (AOI/OAI), Transmission Gate, Pseudo-NMOS, and Tristate buffers."
---

**CMOS** (Complementary Metal-Oxide-Semiconductor) is the dominant technology for implementing digital logic gates. Every CMOS gate consists of complementary **PMOS** (pull-up) and **NMOS** (pull-down) networks.

## Transistoren als Schalter

| Transistor | Leitet wenn | Sperrt wenn | Netzwerk |
|---|---|---|---|
| **NMOS** | Gate = 1 | Gate = 0 | Pull-down (Verbindung zu GND) |
| **PMOS** | Gate = 0 | Gate = 1 | Pull-up (Verbindung zu $V_{DD}$) |

NMOS leitet **starke Nullen**, PMOS leitet **starke Einsen**.

## Komplementäre CMOS-Logik

Grundprinzip: Für jede Schaltfunktion gibt es ein **Pull-up-Netzwerk** (PMOS) und ein **Pull-down-Netzwerk** (NMOS), die **komplementär** zueinander geschaltet sind:

- Pull-down: **Serielle** Transistoren = AND; **Parallele** Transistoren = OR
- Pull-up: **Serielle** Transistoren = OR (der negierten Eingänge); **Parallele** Transistoren = AND (der negierten Eingänge)

$$\text{Pull-up ist das Komplement des Pull-down}$$

### Entwurfsregeln

1. Bestimme die **Pull-down-Funktion** (wann soll der Ausgang 0 sein?)
2. Baue das Pull-down-Netzwerk aus NMOS-Transistoren (Seriell = AND, Parallel = OR)
3. Baue das Pull-up-Netzwerk als **duales** Netz: Seriell ↔ Parallel tauschen, NMOS ↔ PMOS tauschen
4. Ausgang ist immer **invertiert** (CMOS-Gatter implementieren nativ NAND, NOR, NOT)

## Grundgatter

| Gatter | NMOS Pull-down | PMOS Pull-up | Transistoren |
|---|---|---|---|
| **NOT** (Inverter) | 1 NMOS (seriell) | 1 PMOS (seriell) | 2 |
| **NAND** ($n$ Eingänge) | $n$ NMOS in Serie | $n$ PMOS parallel | $2n$ |
| **NOR** ($n$ Eingänge) | $n$ NMOS parallel | $n$ PMOS in Serie | $2n$ |
| **AND** | NAND + Inverter | | $2n + 2$ |
| **OR** | NOR + Inverter | | $2n + 2$ |

> [!NOTE]
> NAND und NOR sind die **nativen** CMOS-Gatter. AND und OR benötigen einen zusätzlichen Inverter am Ausgang.

## Komplexe Gatter (AOI / OAI)

Beliebige Funktionen lassen sich direkt als CMOS-Gatter realisieren, ohne zweistufige NAND/NOR-Logik:

### AND-OR-Invert (AOI)

$$Y = \overline{A \cdot B + C \cdot D}$$

Pull-down: $(A$ seriell $B)$ parallel $(C$ seriell $D)$ — alles NMOS.
Pull-up: $(A$ parallel $B)$ seriell $(C$ parallel $D)$ — alles PMOS (dual).

### OR-AND-Invert (OAI)

$$Y = \overline{(A + B) \cdot (C + D)}$$

Pull-down: $(A$ parallel $B)$ seriell $(C$ parallel $D)$ — NMOS.
Pull-up: $(A$ seriell $B)$ parallel $(C$ seriell $D)$ — PMOS.

## Transmission Gate (TG)

Ein **Transmission Gate** besteht aus einem NMOS und einem PMOS **parallel** geschaltet, mit komplementären Gate-Signalen ($EN$ und $\overline{EN}$):

| $EN$ | Verhalten |
|---|---|
| 1 | **Durchlässig**: Eingang wird zum Ausgang durchgeschaltet |
| 0 | **Hochohmig** ($Z$): Ausgang getrennt |

- Leitet sowohl starke Nullen (NMOS) als auch starke Einsen (PMOS) gut
- Wird für **Multiplexer**, **XOR-Gatter** und **Latches** verwendet

## Pseudo-NMOS

Ersetzt das PMOS-Pull-up-Netzwerk durch einen **einzelnen, immer eingeschalteten PMOS-Transistor** (Gate fest an GND):

- **Vorteil**: weniger Transistoren ($n + 1$ statt $2n$), schnellerer Ausgang
- **Nachteil**: statischer Stromverbrauch wenn Pull-down aktiv (Kurzschluss $V_{DD}$ → GND); schwächere Logik-0 (Spannungsteiler)

> [!WARNING]
> Pseudo-NMOS verbraucht statische Leistung und wird nur in speziellen Anwendungen eingesetzt (z. B. Speicherzellen, NOR-Flash).

## Tristate-Ausgang

Ein Tristate-Buffer hat drei Ausgangszustände: **0**, **1** und **hochohmig** ($Z$):

| $EN$ | $A$ | $Y$ |
|---|---|---|
| 0 | $\times$ | $Z$ (hochohmig) |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

Implementierung: Inverter mit zusätzlichen NMOS/PMOS-Transistoren, die durch $EN$ gesteuert den Pfad zu $V_{DD}$ bzw. GND unterbrechen.

**Anwendung**: Busse, bei denen mehrere Quellen denselben Draht treiben (aber immer nur eine zur gleichen Zeit aktiv).

## Related Concepts

- [[Logikgatter]]: Gattertypen und Bubble Pushing auf Logikebene
- [[Kombinatorische Logik]]: Schaltnetze aus CMOS-Gattern
- [[Halbleiterspeicher]]: Speicherzellen nutzen CMOS-Transistoren (6T-SRAM, 1T1C-DRAM)
- [[Programmierbare Logik]]: FPGA-Logikzellen basieren auf CMOS-LUTs und programmierbaren Schaltern
