---
title: Speicherelemente
aliases:
  - Storage Elements
  - Latch
  - Flip-Flop
  - DFF
  - D-Latch
  - SR-Latch
  - Register
  - Synchrone Schaltungen
  - Metastabilität
  - Setup Time
  - Hold Time
tags:
  - digitaltechnik
  - logic
description: "Latches, flip-flops, and registers — the memory elements of sequential circuits — plus synchronous design discipline, timing constraints, metastability, and clock skew."
---

**Speicherelemente** store binary state and are the fundamental building blocks of sequential circuits ([[Kombinatorische Logik|Schaltwerke]]). Combined with combinational logic and a clock, they enable synchronous digital systems.

## SR-Latch (Set-Reset)

The simplest memory element, built from two cross-coupled NOR (or NAND) gates:

| $S$ | $R$ | $Q$ | $\overline{Q}$ | Verhalten |
|---|---|---|---|---|
| 0 | 0 | $Q_{prev}$ | $\overline{Q}_{prev}$ | **Hold** — state unchanged |
| 1 | 0 | 1 | 0 | **Set** |
| 0 | 1 | 0 | 1 | **Reset** |
| 1 | 1 | — | — | **Verboten** — undefined state |

The $S=R=1$ case is **forbidden** because both outputs would attempt to be 0, and the final state upon release is unpredictable.

## D-Latch

Adds a **data input** $D$ and a **clock/enable** $CLK$:

| $CLK$ | Verhalten |
|---|---|
| 1 | **Transparent**: $Q = D$ (output follows input) |
| 0 | **Latched**: $Q$ holds its last value |

The D-Latch eliminates the forbidden state of the SR-Latch but is **level-sensitive** — output can change as long as $CLK = 1$.

## D-Flip-Flop (DFF)

An **edge-triggered** storage element (built from two D-Latches in master-slave configuration):

- Captures input $D$ at the **rising clock edge** only
- Output $Q$ changes only after the clock edge, then remains stable until the next edge
- Provides a clean sampling point — avoids the transparency problem of latches

$$Q^+ = D \quad \text{(sampled at rising edge of CLK)}$$

## Register

A **Register** is a group of $n$ parallel D-Flip-Flops sharing the same $CLK$ and $Reset$ signals. Stores an $n$-bit word.

Optional **Enable** ($EN$): when $EN=0$, the register holds its value (feedback MUX on each DFF input).

## Synchrone Entwurfsdisziplin

In **synchronous design**, feedback loops are broken by registers:

1. Every circuit element is either a **register** or a **combinational block**
2. At least one element must be a register
3. All registers are driven by the **same clock** signal
4. Every cyclic path contains **at least one register**

This ensures the circuit state changes only at clock edges, making behavior predictable and analyzable.

## Zeitverhalten von Flip-Flops

### Eingangs-Timing (Setup & Hold)

The data input $D$ must be **stable** within a window around the clock edge to avoid **metastability**:

| Parameter | Definition |
|---|---|
| $t_{setup}$ | Time $D$ must be stable **before** the clock edge |
| $t_{hold}$ | Time $D$ must be stable **after** the clock edge |
| $t_a = t_{setup} + t_{hold}$ | **Aperture time** — total forbidden-change window |

Typical order of magnitude: ~10 ps in modern CMOS.

### Ausgangs-Timing (Clock-to-Q)

| Parameter | Definition |
|---|---|
| $t_{ccq}$ | **Contamination delay** clock-to-Q: shortest time until $Q$ starts changing |
| $t_{pcq}$ | **Propagation delay** clock-to-Q: longest time until $Q$ has settled |

## Dynamische Entwurfsdisziplin

For combinational logic between two registers (Register 1 → combinational block → Register 2):

### Setup-Bedingung (max. Taktfrequenz)

$$t_{pcq,1} + t_{pd} + t_{setup,2} \leq T_{CLK}$$

$$\Rightarrow f_{CLK} \leq \frac{1}{t_{pcq} + t_{pd} + t_{setup}}$$

The **critical path** (longest combinational path) determines the maximum clock frequency.

### Hold-Bedingung (Datenstabilität)

$$t_{ccq,1} + t_{cd} \geq t_{hold,2}$$

If violated: insert **buffer gates** on the shortest path to increase $t_{cd}$.

> [!IMPORTANT]
> The setup constraint limits **clock speed**; the hold constraint ensures **data integrity**. Hold violations cannot be fixed by slowing the clock — they require structural changes (adding delay on fast paths).

### Berechnungsbeispiel

Given: $t_{ccq} = 30\,\text{ps}$, $t_{pcq} = 50\,\text{ps}$, $t_{setup} = 60\,\text{ps}$, $t_{hold} = 70\,\text{ps}$, three gates with $t_{cd} = 25\,\text{ps}$, $t_{pd} = 35\,\text{ps}$ each:

- $t_{pd} = 3 \times 35 = 105\,\text{ps}$ → $f_{CLK} \leq \frac{1}{215\,\text{ps}} = 4{,}65\,\text{GHz}$ ✓
- $t_{ccq} + t_{cd} = 30 + 25 = 55\,\text{ps} < 70\,\text{ps} = t_{hold}$ ✗ → Hold-Verletzung!
- Fix: add buffer → $t_{cd} = 50\,\text{ps}$ → $30 + 50 = 80\,\text{ps} > 70\,\text{ps}$ ✓

## Taktverschiebung (Clock Skew)

The clock does not arrive at all registers simultaneously due to different wire lengths (**clock tree**) or logic in the clock path (**gated clock**).

$$t_{skew} = \text{max. difference in clock arrival time between two registers}$$

Modified timing constraints:
- **Setup**: $t_{pcq,1} + t_{pd} + t_{setup,2} + t_{skew} \leq T_{CLK}$
- **Hold**: $t_{ccq,1} + t_{cd} \geq t_{hold,2} + t_{skew}$

Clock skew generally **tightens** both constraints.

## Metastabilität

When $D$ changes during the aperture window ($t_a$), the flip-flop may enter a **metastable state** — an unstable equilibrium between 0 and 1 that resolves to either value after a random delay.

In the voltage transfer curve: a metastable point $V_C$ lies at the unstable intersection where $V_{out} = V_{in}$; a small perturbation drives it toward one of the two stable states ($V_A = 0$ or $V_B = V_{DD}$).

### Asynchrone Eingänge & Synchronizer

External signals (user buttons, communication interfaces) cannot guarantee timing relative to the internal clock → **metastability risk**.

Solution: **Two-stage synchronizer** (Schieberegister):
1. First flip-flop samples the asynchronous input — may go metastable
2. Metastable state resolves (with high probability) before the **next** clock edge
3. Second flip-flop samples a now-stable value

The probability of remaining metastable decreases **exponentially** with available resolution time.

## Related Concepts

- [[Kombinatorische Logik]]: Schaltwerk (sequential) vs. Schaltnetz (combinational)
- [[Zeitverhalten]]: combinational propagation and contamination delays feed into timing analysis
- [[Pipelining]]: registers split combinational paths into pipeline stages
- [[Endliche Zustandsautomaten]]: FSMs use registers to store state
