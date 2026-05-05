---
title: Endliche Zustandsautomaten
aliases:
  - FSM
  - Finite State Machine
  - Zustandsautomat
  - Moore-Automat
  - Mealy-Automat
  - State Machine
tags:
  - digitaltechnik
  - logic
description: "Finite State Machines (FSM) — Moore and Mealy types, state diagrams, state encoding, design flow from specification to gate-level circuit, and FSM decomposition."
---

An **Endlicher Zustandsautomat** (Finite State Machine, FSM) is a synchronous sequential circuit with:

- $n$ input bits: $a_0, \ldots, a_{n-1}$
- $k$ output bits: $y_0, \ldots, y_{k-1}$
- A finite set of **internal states** (encoded in $m \geq 1$ bits)
- **CLK** and **Reset**

At each rising clock edge:
- If **Reset** is active → go to the **start state**
- Otherwise → compute **next state** and **outputs** from the current state and inputs

## Zustandsdiagramm (State Diagram)

FSMs are represented as **directed graphs**:

| Element | Darstellung |
|---|---|
| **Zustände** (states) | Nodes with symbolic names ($S_0, S_1, \ldots$) |
| **Übergänge** (transitions) | Directed edges labeled with Boolean input conditions |
| **Reset** | Unconditional edge without source, pointing to start state |
| **Ausgaben** (outputs) | In states (Moore) or on edges (Mealy) |

**Conventions**:
- No two outgoing edges from one state may be satisfiable simultaneously
- If no edge condition is met, the state remains unchanged (implicit self-loop)
- Outputs can be given as full minterms or — more commonly — only the asserted signals are listed

## Moore vs. Mealy

| | Moore | Mealy |
|---|---|---|
| **Ausgaben hängen ab von** | Nur dem aktuellen Zustand | Zustand **und** Eingaben |
| **Ausgaben notiert** | In den Zustandsknoten | An den Kanten |
| **Reaktionsgeschwindigkeit** | Ausgang ändert sich erst im **nächsten** Takt | Ausgang ändert sich **im selben** Takt |
| **Zustände** | Oft **mehr** nötig (Ausgabe muss im Zustand kodiert sein) | Oft **weniger** (Ausgabe auf Kante flexibler) |
| **Glitch-Gefahr** | Gering (Ausgang ist registriert) | Höher (Ausgang ist kombinatorisch) |

### Faustregeln

- **Moore** besser, wenn Ausgaben **statisch** sind (z. B. Ampelphasen)
- **Mealy** besser, wenn Ausgaben **kurzfristige Aktionen** auslösen (z. B. Schloss öffnen, Fehlermeldung)
- Mealy erkennt Muster **einen Takt früher** als ein äquivalenter Moore-Automat

## Zustandstabellen

### Zustandsübergangstabelle (Next-State Table)

| $S$ (aktuell) | Eingaben | $S'$ (nächster Zustand) |
|---|---|---|
| $S_0$ | Bedingung | $S_1$ |
| ... | ... | ... |

### Ausgabetabelle (Output Table)

- **Moore**: $S \rightarrow Y$ (Ausgabe nur von Zustand abhängig)
- **Mealy**: $(S, \text{Eingaben}) \rightarrow Y$

> [!NOTE]
> Implizite Bedingungen beachten: Selbstschleifen im Diagramm müssen als explizite Zeilen in der Tabelle erscheinen.

## Zustandskodierung

Die symbolischen Zustände müssen in $m$-Bit-Binärwerte übersetzt werden:

| Kodierung | Bits $m$ | Eigenschaft |
|---|---|---|
| **Binär** (Durchnummerieren) | $\lceil \log_2 |S| \rceil$ | Minimale Bitbreite; komplexere Logik |
| **One-Hot** | $|S|$ | Ein Bit pro Zustand; einfachere Next-State-Logik, mehr Flip-Flops |
| **Ausgabekodierung** | variabel | Zustandsbits = Ausgabebits (wenn Ausgaben eindeutig pro Zustand) |

Die Kodierung der Ein-/Ausgänge ist meist durch die Anwendung vorgegeben.

## FSM als Schaltung

Eine FSM wird als synchrone Schaltung realisiert:

```
             ┌──────────────┐     ┌──────────┐
Eingaben ──→ │  Next-State   │──→ │ Zustands- │──→ aktueller Zustand
             │    Logic      │    │ register  │         │
             └──────────────┘     └──────────┘         │
                    ↑                  ↑  CLK, Reset    │
                    └──────────────────┘                │
                                                        ↓
                                              ┌──────────────┐
                                              │   Output      │──→ Ausgaben
                                              │    Logic      │
                                              └──────────────┘
```

- **Moore**: Output Logic hat nur den Zustand als Eingang
- **Mealy**: Output Logic hat Zustand **und** Eingaben

## Entwurfsverfahren (Design Flow)

1. **Definiere** Ein- und Ausgänge
2. **Wähle** Moore oder Mealy
3. **Zeichne** das Zustandsdiagramm
4. **Kodiere** die Zustände (und ggf. Ein-/Ausgänge)
5. **Stelle** Zustandsübergangs- und Ausgabetabelle auf
6. **Leite** boolesche Gleichungen ab (mit [[Karnaugh-Veitch-Diagramme|KV-Minimierung]] unter Ausnutzung von Don't Cares)
7. **Entwirf** den Schaltplan: Gatter + Register

### Beispiel: Ampelsteuerung

4 Zustände (Moore): $A$ (grün/rot), $AB$ (gelb/rot), $B$ (rot/grün), $BA$ (rot/gelb). Binäre Kodierung mit 2 Zustandsbits ($s_1, s_0$), 2 Eingänge ($a_A, a_B$), 4 Ausgänge ($y_3, y_2, y_1, y_0$). Die 6 Booleschen Funktionen ($s_1', s_0', y_3, y_2, y_1, y_0$) werden aus den kodierten Tabellen per KV-Diagramm minimiert.

### Beispiel: Mustererkennung „1101"

**Moore** (5 Zustände, $S_0$–$S_4$): Ausgang $y=1$ im Zustand $S_4$. Übergänge berücksichtigen **Überlappung** (ähnlich KMP-Algorithmus): z.B. von $S_4$ mit Eingang $1$ → $S_2$ (nicht $S_0$, da „…1" Beginn eines neuen Musters sein könnte).

**Mealy** (4 Zustände, $S_0$–$S_3$): Ausgang $y=1$ auf der Kante von $S_2$ nach $S_1$ bei Eingang $a=1$ (Abschluss von „1101"). Erkennt das Muster **einen Takt früher** als der Moore-Automat.

## Zerlegen von Zustandsautomaten (FSM Decomposition)

Komplexe FSMs werden in **einfachere, kommunizierende FSMs** zerlegt:

- Reduziert die Zustandsanzahl pro Teilautomat
- Verbessert Übersichtlichkeit und Wartbarkeit
- Teilautomaten kommunizieren über **interne Signale**

**Beispiel**: Ampelsteuerung mit Festumzugsmodus → zerlegt in:
1. **Modus-FSM** (2 Zustände: Normal / Festumzug)
2. **Ampel-FSM** (4 Zustände wie bisher, aber mit Modus-Signal $M$ als zusätzlichem Eingang)

Statt einer einzelnen FSM mit $4 \times 2 = 8$ Zuständen: zwei FSMs mit 2 + 4 = 6 Zuständen und einfacherer Logik.

## Related Concepts

- [[Speicherelemente]]: Zustandsregister speichern den aktuellen FSM-Zustand
- [[Kombinatorische Logik]]: Next-State und Output Logic sind Schaltnetze
- [[Karnaugh-Veitch-Diagramme]]: Minimierung der Zustandsübergangs- und Ausgangslogik
- [[Normalformen]]: Wahrheitstabellen als Zwischenschritt im Entwurf
- [[Boolesche Algebra]]: algebraische Vereinfachung der Logikgleichungen
