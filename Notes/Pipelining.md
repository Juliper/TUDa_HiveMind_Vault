---
title: Pipelining
aliases:
  - Pipeline
  - Parallelität
  - Parallelism
  - Latenz
  - Durchsatz
  - Throughput
  - Latency
tags:
  - digitaltechnik
  - logic
description: "Spatial and temporal parallelism in digital circuits — pipelining registers increase throughput at the cost of latency."
---

**Parallelität** allows digital systems to process more data per unit of time. Two fundamental types exist; they can be combined for maximum throughput.

## Arten der Parallelität

| Type | Principle | Example |
|---|---|---|
| **Räumliche Parallelität** (spatial) | Duplicate hardware to process multiple data sets **simultaneously** | Two ovens baking in parallel |
| **Zeitliche Parallelität** (temporal / pipelining) | Split one task into stages; overlap **different stages** of successive data sets | Assembly line: next item starts stage 1 while the previous is in stage 2 |

## Grundbegriffe

| Term | Definition |
|---|---|
| **Datensatz** | One input vector that produces one output vector |
| **Latenz** (Latency) | Time from when a data set enters to when its result exits |
| **Durchsatz** (Throughput) | Number of data sets processed per unit of time |

$$\text{Parallelism increases throughput}$$

## Pipelining in Schaltungen

Insert **pipeline registers** ([[Speicherelemente|DFF registers]]) into a combinational path to split it into stages:

### Ohne Pipeline (1 Stage)

$$f_{CLK} \leq \frac{1}{t_{pcq} + t_{pd,\text{total}} + t_{setup}}$$

$$\text{Latenz} = 1 \cdot T_{CLK}$$

### Mit $k$ Pipeline-Stufen

Each stage contains a portion of the original combinational logic, separated by registers:

$$f_{CLK} \leq \frac{1}{t_{pcq} + t_{pd,\text{longest stage}} + t_{setup}}$$

$$\text{Latenz} = k \cdot T_{CLK}$$

### Beispiel

Circuit with four gate blocks: $t_{pd} = 2, 3, 2, 4\,\text{ns}$; $t_{pcq} = 0{,}3\,\text{ns}$; $t_{setup} = 0{,}2\,\text{ns}$:

| Configuration | $T_{CLK,\min}$ | $f_{CLK}$ | Latenz |
|---|---|---|---|
| No pipeline | $0{,}3 + 9{,}0 + 0{,}2 = 9{,}5\,\text{ns}$ | 105 MHz | 9,5 ns (1 cycle) |
| 2 stages | $0{,}3 + 5{,}0 + 0{,}2 = 5{,}5\,\text{ns}$ | 182 MHz | 11 ns (2 cycles) |
| 3 stages | $0{,}3 + 4{,}0 + 0{,}2 = 4{,}5\,\text{ns}$ | 222 MHz | 13,5 ns (3 cycles) |

> [!NOTE]
> More stages → higher throughput (faster clock) but also **higher latency** (more cycles) and **more hardware** (pipeline registers add area and power). Pipeline registers also add their own $t_{pcq}$ and $t_{setup}$ overhead to each stage.

## Bewertung

### Vorteile
- **Higher throughput**: more results per second (higher $f_{CLK}$)
- Clock frequency limited only by the **longest stage**, not the total path

### Nachteile
- **Higher latency**: each data set takes more clock cycles
- **Register overhead**: $t_{pcq} + t_{setup}$ added to each stage
- **Data dependencies**: if stage $k+1$ needs the result of stage $k$ from the same data set, stalls or forwarding logic are required

### Ausbalancierung

Pipeline stages should be **balanced** (equal propagation delay). The longest stage determines $T_{CLK}$ — an unbalanced pipeline wastes the clock budget on short stages.

$$\text{Ideal: } t_{pd,\text{stage } i} \approx \frac{t_{pd,\text{total}}}{k} \quad \forall i$$

### When Pipelining Helps

Pipelining improves throughput only when **many data sets** must be processed in sequence. For a single data set, pipelining increases latency without benefit.

## Related Concepts

- [[Speicherelemente]]: pipeline registers are DFF banks splitting the combinational path
- [[Zeitverhalten]]: $t_{pd}$ of the critical stage determines the pipeline clock rate
- [[Arithmetische Schaltungen]]: pipelined adders and multipliers for high-throughput datapaths
- [[Kombinatorische Logik]]: the combinational logic between pipeline stages
