---
title: Halbleiterspeicher
aliases:
  - Speicherfeld
  - Memory Array
  - SRAM
  - DRAM
  - ROM
  - Flash
  - RAM
  - Bitzelle
  - Wordline
  - Bitline
tags:
  - digitaltechnik
  - logic
description: "Memory arrays in digital systems — bit cells, wordlines, bitlines, SRAM, DRAM, ROM/Flash types, and memory organization with decoders and sense amplifiers."
---

Ein **Halbleiterspeicher** (Memory Array) ist ein zweidimensionales Feld von **Bitzellen**, das binäre Daten adressierbar speichert. Speicher bilden zusammen mit Logik die Grundbausteine digitaler Systeme.

## Speicherfeld-Organisation

Ein Speicherfeld hat $N$ Adressbits und $M$ Datenbits:

| Parameter | Definition |
|---|---|
| **Tiefe** (Depth) | $2^N$ — Anzahl der Wörter (Zeilen) |
| **Breite** (Width) | $M$ — Anzahl der Bits pro Wort (Spalten) |
| **Größe** (Size) | $\text{Tiefe} \times \text{Breite} = 2^N \times M$ Bits |

Beispiel: 1024-word $\times$ 32-bit Array = $2^{10} \times 32 = 32\,768$ Bits = 4 KiB.

### Aufbau

```
                 ┌──────────┐
Address ──N──→  │  Decoder  │──→ Wordlines (2^N)
                 └──────────┘
                      │
                 ┌──────────┐
                 │  Bit Cell │──→ Bitlines (M)
                 │  Array    │
                 └──────────┘
                      │
                    Data (M Bits)
```

### Wordline und Bitline

- **Wordline**: Ausgang des Adressdecoders; wählt **eine Zeile** aus (One-Hot). Maximal eine Wordline darf gleichzeitig HIGH sein.
- **Bitline**: Verbindet alle Bitzellen einer Spalte; überträgt Daten beim Lesen und Schreiben.

### Bitzelle (Bit Cell)

Jede Bitzelle speichert ein Bit und wird über Wordline und Bitline angesprochen:

- **Schreiben** (Store): Wordline = 1, gewünschter Wert auf Bitline treiben → Bitzelle übernimmt den Wert
- **Lesen** (Load): Wordline = 1, Bitline hochohmig (Z) → Bitzelle treibt ihren gespeicherten Wert auf die Bitline

## Speichertypen

### RAM (Random Access Memory) — flüchtig

| Typ | Zelle | Transistoren | Eigenschaft |
|---|---|---|---|
| **SRAM** (Static) | 6 Transistoren (6T) — zwei kreuzgekoppelte Inverter + 2 Zugriffstransistoren | 6T | Schnell; kein Refresh; teurer pro Bit |
| **DRAM** (Dynamic) | 1 Transistor + 1 Kondensator (1T1C) | 1T1C | Kompakt; benötigt periodischen **Refresh** (Kondensator verliert Ladung); langsamer als SRAM |

> [!NOTE]
> SRAM wird für **Caches** und **Register Files** verwendet (schnell, wenig Kapazität). DRAM wird für **Hauptspeicher** verwendet (hohe Kapazität, günstiger pro Bit).

### ROM (Read-Only Memory) — nicht-flüchtig

| Typ | Programmierung | Löschbar? |
|---|---|---|
| **ROM** | Bei Herstellung (Masken-ROM) | Nein |
| **PROM** | Einmalig programmierbar (Fuse/Antifuse) | Nein |
| **EPROM** | Elektrisch programmierbar | UV-Licht (komplett) |
| **EEPROM** | Elektrisch programmierbar | Elektrisch (byteweise) |
| **Flash** | Elektrisch programmierbar | Elektrisch (blockweise) |

Flash-Speicher ist die Grundlage von SSDs, USB-Sticks und Smartphone-Speicher.

## Logik via Speicher

Ein Speicherfeld kann **beliebige kombinatorische Logikfunktionen** realisieren, indem die Wahrheitstabelle direkt gespeichert wird:

- **Adresse** = Eingangskombination
- **Datenwort** = Ausgangswerte für diese Kombination

### Lookup Table (LUT)

Eine LUT ist ein kleines Speicherfeld (typisch $2^k \times 1$ Bit), das eine $k$-stellige Boolesche Funktion realisiert:

1. Adresse = $k$ Eingangsbits → Decoder wählt Zeile
2. Gespeichertes Bit = Funktionswert für diese Eingangskombination

LUTs sind die Grundbausteine von [[Programmierbare Logik|FPGAs]] (typisch 4–6 Eingänge).

## SystemVerilog-Modellierung

### RAM

```systemverilog
module ram #(parameter N=6, M=32)
    (input  logic        clk, we,
     input  logic [N-1:0] adr,
     input  logic [M-1:0] din,
     output logic [M-1:0] dout);

    logic [M-1:0] mem [2**N-1:0];

    always_ff @(posedge clk)
        if (we) mem[adr] <= din;    // synchrones Schreiben

    assign dout = mem[adr];          // asynchrones Lesen
endmodule
```

### ROM

```systemverilog
module rom(input  logic [1:0] adr,
           output logic [2:0] dout);
    always_comb
        case(adr)
            2'b11: dout = 3'b010;
            2'b10: dout = 3'b100;
            2'b01: dout = 3'b110;
            2'b00: dout = 3'b011;
        endcase
endmodule
```

## Mehrport-Speicher und Register Files

Ein **Register File** hat typisch 2 Lese-Ports und 1 Schreib-Port, um gleichzeitig zwei Operanden zu lesen und ein Ergebnis zu schreiben (z. B. in Prozessoren).

## Schieberegister mit parallelem Laden

Ein Schieberegister mit **Load**-Signal kann als:
- **Normales $N$-Bit-Register** fungieren ($Load = 1$: paralleles Laden von $D_0, \ldots, D_{N-1}$)
- **Schieberegister** fungieren ($Load = 0$: serielles Schieben von $S_{in}$)

Dadurch realisierbar als:
- **Seriell-Parallel-Wandler**: $S_{in} \to Q_{0:N-1}$ (mit $Load = 0$)
- **Parallel-Seriell-Wandler**: $D_{0:N-1} \to S_{out}$ (mit $Load = 1$)

## Related Concepts

- [[Speicherelemente]]: Flip-Flops und Register als Einzelspeicher
- [[CMOS]]: Transistor-Level-Implementierung von Speicherzellen (6T-SRAM, 1T1C-DRAM)
- [[Programmierbare Logik]]: FPGAs nutzen LUTs (kleine Speicher) als Logikbausteine
- [[Kombinatorische Logik]]: Decoder als Adressierungslogik im Speicherfeld
- [[Verilog]]: SystemVerilog-Modellierung von RAM und ROM
