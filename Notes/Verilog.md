---
title: Verilog
aliases:
  - SystemVerilog
  - HDL
  - Hardware Description Language
  - Hardwarebeschreibungssprache
tags:
  - digitaltechnik
  - logic
description: "SystemVerilog as a hardware description language — module syntax, combinational and sequential logic, parameterized modules, generate statements, and testbenches."
---

**SystemVerilog** ist eine Hardwarebeschreibungssprache (HDL), die digitale Schaltungen auf verschiedenen Abstraktionsebenen beschreibt: **behavioral** (Verhalten), **RTL** (Register-Transfer-Ebene) und **structural** (Gatternetz). SystemVerilog ist eine Obermenge von Verilog und der aktuelle IEEE-Standard (IEEE 1800).

## Grundlegende Syntax

- **Case-sensitive**: `reset` $\neq$ `Reset`
- Bezeichner dürfen **nicht mit Ziffern** beginnen
- Whitespace (Leerzeichen, Tabulatoren, Leerzeilen) ist irrelevant
- Kommentare: `//` (Zeilenende) oder `/* ... */` (Block)

### Numerische Literale

Syntax: `<N>'<B><Wert>` wobei `<N>` = Bitbreite, `<B>` = Basis (`b`, `d`, `o`, `h`):

| Literal | Bitbreite | Basis | Dezimal |
|---|---|---|---|
| `3'b101` | 3 | binär | 5 |
| `8'hAB` | 8 | hex | 171 |
| `3'd6` | 3 | dezimal | 6 |
| `42` | 32 (default) | dezimal | 42 |

Unterstriche als optische Trenner möglich: `8'b1010_1011`.

## Modulstruktur

Ein **Modul** ist die grundlegende Entwurfseinheit:

```systemverilog
module modulname(input  logic a, b,
                 output logic y);
    // Beschreibung
endmodule
```

## Kombinatorische Logik

### Nebenläufige Zuweisung (`assign`)

```systemverilog
assign y = ~b & ~c | a & ~b;  // Boolesche Gleichung
```

### Bitweise Operatoren

| Operator | Funktion |
|---|---|
| `&` | AND |
| `\|` | OR |
| `^` | XOR |
| `~` | NOT |
| `~&`, `~\|`, `~^` | NAND, NOR, XNOR |

### Reduktionsoperatoren (unär)

Reduzieren einen Vektor auf ein einzelnes Bit:

```systemverilog
assign y = &a;   // AND-Reduktion: a[7] & a[6] & ... & a[0]
assign p = ^a;   // XOR-Reduktion (Parität)
```

### Bedingte Zuweisung (ternär)

```systemverilog
assign y = s ? d1 : d0;  // MUX: wenn s=1 dann d1, sonst d0
```

### Konkatenation und Replikation

```systemverilog
assign y = {a[2:1], {3{b[0]}}, a[0], 6'b100010};  // Zusammensetzen
```

### Operatorpräzedenz (absteigend)

`[]` > `~, !, &, |, ^` (unär) > `*, /, %` > `+, -` > `<<, >>, <<<, >>>` > `<, <=, >, >=` > `==, !=` > `&, ~&` > `^, ~^` > `|, ~|` > `&&` > `||` > `?:` > `{}`

### Interne Verbindungsknoten

```systemverilog
module fulladder(input  logic a, b, cin,
                 output logic s, cout);
    logic p, g;                    // interne Signale
    assign p = a ^ b;
    assign g = a & b;
    assign s = p ^ cin;
    assign cout = g | (p & cin);
endmodule
```

## Strukturelle Beschreibung

Module können andere Module **instanziieren**:

```systemverilog
module nand3(input logic d, e, f, output logic w);
    logic s;
    and3 andgate(d, e, f, s);     // Portzuweisung nach Position
    inv  inverter(s, w);
endmodule
```

**Portzuweisung nach Namen** (empfohlen ab ~10 Ports):

```systemverilog
and3 andgate(.a(d), .b(e), .c(f), .y(s));
```

## Sequentielle Logik (`always`-Blöcke)

### Ereignissteuerung

| Syntax | Auslöser |
|---|---|
| `@(posedge clk)` | Steigende Taktflanke |
| `@(negedge clk)` | Fallende Taktflanke |
| `@(a, b)` oder `@(a or b)` | Änderung von `a` oder `b` |
| `@*` | Änderung **aller** gelesenen Signale (kombinatorisch) |

### Blocking vs. Non-Blocking

| Art | Syntax | Verhalten | Verwenden für |
|---|---|---|---|
| **Blocking** | `=` | Sequentiell: nächste Zeile wartet | `always_comb` (kombinatorisch) |
| **Non-Blocking** | `<=` | Parallel: alle gleichzeitig vorgemerkt | `always_ff` (sequentiell) |

> [!IMPORTANT]
> **Niemals** Blocking und Non-Blocking in demselben `always`-Block mischen. Ein Signal darf nur von **einem** Prozess (`assign` oder `always`) getrieben werden.

### Spezialisierte `always`-Blöcke

| Block | Verwendung | Vorteil gegenüber `always` |
|---|---|---|
| `always_comb` | Kombinatorische Logik | Einmalige Auswertung bei Simulationsstart; Fehlermeldung bei mehrfachen Treibern |
| `always_ff` | Flip-Flop-Logik | Synthese-Tools erkennen Absicht und warnen bei Fehlern |
| `always_latch` | Latch-Logik | Warnung, falls Latch unbeabsichtigt |

### Modellierung von Speicherelementen

**D-Latch**:
```systemverilog
always_latch if (CLK) Q <= D;
```

**D-Flip-Flop**:
```systemverilog
always_ff @(posedge CLK) Q <= D;
```

**Asynchron rücksetzbares DFF**:
```systemverilog
always_ff @(posedge CLK, posedge RST)
    if (RST) Q <= 0;
    else     Q <= D;
```

**Synchron rücksetzbares DFF**:
```systemverilog
always_ff @(posedge CLK)
    if (RST) Q <= 0;
    else     Q <= D;
```

**DFF mit Enable**:
```systemverilog
always_ff @(posedge CLK)
    if      (RST) Q <= 0;
    else if (EN)  Q <= D;
```

### Allgemeine Zuweisungsregeln

- Interne Zustände: in `always_ff @(posedge CLK)` mit `<=`
- Einfache kombinatorische Logik: `assign`
- Komplexe kombinatorische Logik: `always_comb` mit `=`
- Ein Signal darf **nicht** von mehreren nebenläufigen Prozessen beschrieben werden

## Parametrisierte Module

```systemverilog
module mux2xW
    #(parameter WIDTH=8)
    (input  logic [WIDTH-1:0] A, B,
     input  logic S,
     output logic [WIDTH-1:0] Y);
    assign Y = S ? A : B;
endmodule
```

Instanziierung mit anderem Parameter:
```systemverilog
localparam W = 4;
mux2xW #(W) mux_inst(a, b, s, y);
```

## `generate`-Anweisung

Für iterative oder bedingte Instanziierung:

```systemverilog
module shift_reg #(parameter WIDTH=8, parameter DEPTH=3)
    (input  logic CLK, RST,
     input  logic [WIDTH-1:0] D,
     output logic [WIDTH-1:0] Q);

    logic [WIDTH-1:0] c [0:DEPTH];
    assign c[0] = D;
    assign Q    = c[DEPTH];

    genvar i;
    generate
        for (i=0; i<DEPTH; i=i+1) begin
            register #(WIDTH) r (.CLK(CLK), .RST(RST), .D(c[i]), .Q(c[i+1]));
        end
    endgenerate
endmodule
```

## Testumgebungen (Testbenches)

Eine **Testbench** ist ein HDL-Modul **ohne Ports**, das ein DUT (Device Under Test) instanziiert und stimuliert:

```systemverilog
module simple_tb;
    logic a, b, c, y;
    simple uut(a, b, c, y);          // Unit Under Test

    initial begin
        $dumpfile("simple_tb.vcd");   // Waveform-Datei
        $dumpvars;
        a = 0; b = 0; c = 0; #10;    // Stimuli mit Zeitverzögerung
               b = 1; c = 0; #10;
        $display("FINISHED");         // Textausgabe
        $finish;                      // Simulation beenden
    end
endmodule
```

### Selbstprüfender Testrahmen

```systemverilog
a=0; b=0; c=0; #10; assert(y===1) else $error("000 failed.");
```

### Ausgabe und Zeitfunktionen

| Funktion | Beschreibung |
|---|---|
| `$display(format, ...)` | Textausgabe (wie `printf` in C) |
| `$time` | Aktuelle Simulationszeit (integer) |
| `$realtime` | Aktuelle Simulationszeit (real) |
| `$finish` | Simulation beenden |
| `$dumpfile` / `$dumpvars` | VCD-Waveform-Datei erzeugen |

Platzhalter: `%d` (dezimal), `%b` (binär), `%h` (hex), `%m` (Modulname), `%t` (Zeit).

### Takterzeugung

```systemverilog
logic clk = 0, reset = 1;
always #(0.5/10) clk <= ~clk;        // Takt erzeugen
initial @(posedge clk) reset <= 0;    // Reset nach erstem Takt
```

> [!NOTE]
> Testbenches werden **nicht synthetisiert** — sie dienen nur der Simulation. Konstrukte wie `initial`, `#delay` und `$display` haben keine Hardware-Entsprechung.

## Tristate und hochohmiger Ausgang

```systemverilog
assign y = en ? a : 4'bz;   // Tristate: wenn en=0 → hochohmig
```

## Verzögerungen (nur Simulation)

```systemverilog
`timescale 1ns / 10ps
assign #1 {ab, bb, cb} = ~{a, b, c};  // 1 Zeiteinheit Verzögerung
assign #2 n1 = ab & bb & cb;          // 2 Zeiteinheiten
```

## Related Concepts

- [[Kombinatorische Logik]]: `assign` und `always_comb` beschreiben Schaltnetze
- [[Speicherelemente]]: `always_ff` modelliert Flip-Flops und Register
- [[Endliche Zustandsautomaten]]: FSMs werden als Two-Process-Modell in SystemVerilog kodiert
- [[CMOS]]: SystemVerilog-Beschreibungen werden in CMOS-Gatter synthetisiert
- [[Programmierbare Logik]]: FPGA-Synthese übersetzt SystemVerilog in LUT-Konfigurationen
