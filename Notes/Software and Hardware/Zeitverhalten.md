---
title: Zeitverhalten
aliases:
  - Propagation Delay
  - Contamination Delay
  - Timing
  - tpd
  - tcd
  - Glitch
  - Hazard
  - Critical Path
  - Kritischer Pfad
tags:
  - digitaltechnik
  - logic
description: "Timing behavior of combinational circuits: propagation delay tpd, contamination delay tcd, glitches from unequal path delays, and the critical path."
---

Real gates are not instantaneous. **Zeitverhalten** (timing behavior) describes how signal changes propagate through a circuit with finite gate delays.

## Verzögerungszeiten (Delay Definitions)

### Propagation Delay $t_{pd}$

The **propagation delay** $t_{pd}$ is the **maximum** time from when any input changes to when all outputs have settled to their final values.

$$t_{pd} = \max(\text{all paths from input to output})$$

- Measured to the **last** output to finish changing
- Guarantees that after $t_{pd}$, all outputs are valid
- Determines the **minimum clock period** in synchronous designs: $T_{clk} \geq t_{pd}$

### Contamination Delay $t_{cd}$

The **contamination delay** $t_{cd}$ is the **minimum** time from when any input changes to when any output **begins** to change (first output starts moving away from its old value).

$$t_{cd} = \min(\text{all paths from input to output})$$

- Measured to the **first** output to start changing
- Models the earliest moment at which an output can no longer be relied upon

> [!NOTE]
> The window between $t_{cd}$ and $t_{pd}$ is when outputs are in a transient, unreliable state. Downstream circuits must not sample during this window.

## Kritischer Pfad (Critical Path)

The **critical path** is the longest combinational path through the circuit — it determines $t_{pd}$.

$$t_{pd}^{\text{circuit}} = \sum_{\text{gates on critical path}} t_{pd}^{\text{gate}}$$

To improve circuit speed (reduce clock period), the critical path must be shortened — either by restructuring logic or by inserting pipeline registers.

## Glitches und Hazards

A **Glitch** (also called a hazard) is a momentary, incorrect output value caused by signals arriving at a gate via paths of **different lengths**.

### Cause

When an input change propagates through two paths of unequal delay, the gate combining them sees an intermediate state where both old and new values are simultaneously present — producing a brief erroneous output pulse.

### Example

Function $F = \overline{A}\,C + A\,B$: changing $A$ from 1→0 while $B=C=1$:
- Fast path (through $A\,B$): sees $A=0$ quickly → this term goes to 0
- Slow path (through $\overline{A}\,C$): $\overline{A}$ delayed → this term not yet 1

Brief moment where both terms are 0 → $F$ glitches to 0 before stabilizing at 1.

### Hazard Types

| Type | Glitch on | Cause |
|---|---|---|
| **Static-1 hazard** | Output should stay 1, briefly goes 0 | Incompletely covered adjacent minterms in DNF |
| **Static-0 hazard** | Output should stay 0, briefly goes 1 | Incompletely covered adjacent maxterms in KNF |
| **Dynamic hazard** | Output changes, but oscillates multiple times | Multiple feedback-free paths of 3+ different delays |

### Hazard-Free Design

Static hazards can be eliminated by adding **consensus terms** — redundant product terms that bridge the gap between adjacent minterms on the KV map. Every pair of overlapping groups in the KV map should share a third group covering the boundary.

> [!IMPORTANT]
> In synchronous (clocked) designs, glitches are generally harmless as long as outputs settle before the next clock edge samples them. Hazard elimination is critical in asynchronous circuits where glitches can trigger unintended state transitions.

## Timing-Analyse (Zusammenfassung)

| Parameter | Definition | Measured as |
|---|---|---|
| $t_{pd}$ | Propagation delay | Max path delay — when all outputs are valid |
| $t_{cd}$ | Contamination delay | Min path delay — when first output starts changing |
| Critical path | Longest path | Determines $t_{pd}$ and maximum clock frequency |

For a chain of $k$ gates in series:

$$t_{pd}^{\text{total}} = \sum_{i=1}^{k} t_{pd,i} \qquad t_{cd}^{\text{total}} = \sum_{i=1}^{k} t_{cd,i}$$

For gates in parallel (multiple independent paths converging):

$$t_{pd}^{\text{total}} = \max_i(t_{pd,i}) \qquad t_{cd}^{\text{total}} = \min_i(t_{cd,i})$$

## Related Concepts

- [[Kombinatorische Logik]]: timing applies to all combinational (Schaltnetz) circuits
- [[Logikgatter]]: each gate type has its own $t_{pd}$ and $t_{cd}$ specifications
- [[Karnaugh-Veitch-Diagramme]]: grouping rules for hazard-free minimization
