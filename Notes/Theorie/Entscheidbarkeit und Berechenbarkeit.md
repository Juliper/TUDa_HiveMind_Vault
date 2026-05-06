---
title: Entscheidbarkeit und Berechenbarkeit
aliases:
  - Decidability
  - Entscheidbarkeit
  - Berechenbarkeit
  - Halteproblem
  - Halting Problem
  - Reduktion
tags:
  - automaten
  - logik
description: "Entscheidbarkeit und Berechenbarkeit — entscheidbare vs. erkennbare Sprachen, Halteproblem, Reduktionen und Grenzen der Berechnung."
draft: false
---

**Entscheidbarkeit** beschäftigt sich mit der fundamentalen Frage: Welche Probleme können von [[Turingmaschinen]] algorithmisch gelöst werden — und welche nicht?

## Grundbegriffe

| Begriff | Definition |
|---|---|
| **Entscheidbar** (rekursiv) | Eine Sprache $L$, für die eine TM existiert, die auf **jeder** Eingabe hält und korrekt akzeptiert/verwirft |
| **Erkennbar** (r.e.) | Eine Sprache $L$, für die eine TM existiert, die $w \in L$ akzeptiert (bei $w \notin L$ evtl. nicht hält) |
| **Ko-erkennbar** | $\overline{L}$ ist erkennbar |
| **Unentscheidbar** | Keine TM entscheidet $L$ |

> [!IMPORTANT]
> $L$ ist entscheidbar $\Longleftrightarrow$ $L$ ist erkennbar **und** ko-erkennbar.

## Entscheidbare Probleme

| Problem | Sprache | Status |
|---|---|---|
| Wortproblem für DFA | $\{\langle A, w \rangle \mid w \in L(A)\}$ | Entscheidbar |
| Leerheitsproblem für DFA | $\{\langle A \rangle \mid L(A) = \emptyset\}$ | Entscheidbar |
| Äquivalenzproblem für DFA | $\{\langle A, B \rangle \mid L(A) = L(B)\}$ | Entscheidbar |
| Wortproblem für CFG | $\{\langle G, w \rangle \mid w \in L(G)\}$ | Entscheidbar (CYK) |
| Leerheitsproblem für CFG | $\{\langle G \rangle \mid L(G) = \emptyset\}$ | Entscheidbar |

## Das Halteproblem

> Gibt es eine TM, die bei Eingabe $\langle M, w \rangle$ entscheidet, ob $M$ auf $w$ hält?

$$H = \{\langle M, w \rangle \mid M \text{ hält auf Eingabe } w\}$$

**Satz (Turing, 1936)**: Das Halteproblem ist **unentscheidbar**.

### Beweis (Diagonalisierung)

Angenommen, $H$ sei entscheidbar durch eine TM $D$. Konstruiere eine TM $\hat{D}$:
- Bei Eingabe $\langle M \rangle$: Simuliere $D(\langle M, \langle M \rangle \rangle)$
- Falls $D$ akzeptiert (M hält auf $\langle M \rangle$): **loop** (halte nicht)
- Falls $D$ verwirft: **akzeptiere**

Was passiert bei $\hat{D}(\langle \hat{D} \rangle)$?
- Falls $\hat{D}$ hält auf $\langle \hat{D} \rangle$: $D$ akzeptiert → $\hat{D}$ loopt → Widerspruch
- Falls $\hat{D}$ nicht hält: $D$ verwirft → $\hat{D}$ akzeptiert → Widerspruch

> [!NOTE]
> $H$ ist zwar unentscheidbar, aber **erkennbar**: Eine TM kann $M$ auf $w$ simulieren und akzeptieren, falls $M$ hält. Das Komplement $\overline{H}$ ist dagegen **nicht erkennbar**.

## Reduktionen

Eine **Reduktion** von Problem $A$ auf Problem $B$ ($A \leq_m B$) ist eine berechenbare Funktion $f$, sodass:

$$w \in A \Longleftrightarrow f(w) \in B$$

### Anwendung

- Wenn $A \leq_m B$ und $B$ entscheidbar → $A$ entscheidbar
- Wenn $A \leq_m B$ und $A$ unentscheidbar → $B$ **unentscheidbar**

Die zweite Richtung wird genutzt, um Unentscheidbarkeit zu beweisen: Man reduziert ein bekannt unentscheidbares Problem (z. B. $H$) auf das neue Problem.

## Weitere unentscheidbare Probleme

| Problem | Beschreibung |
|---|---|
| Halteproblem auf leerem Band | Hält $M$ auf $\varepsilon$? |
| Totalitätsproblem | Hält $M$ auf **jeder** Eingabe? |
| Äquivalenzproblem für TMs | $L(M_1) = L(M_2)$? |
| Satz von Rice | **Jede** nichttriviale semantische Eigenschaft von TMs ist unentscheidbar |
| Post'sches Korrespondenzproblem | Gibt es eine Folge von Indizes, die oben und unten gleich ergibt? |

## Satz von Rice

> Sei $\mathcal{S}$ eine nichttriviale Eigenschaft erkennbarer Sprachen (d. h. manche TMs haben sie, manche nicht). Dann ist die Sprache $\{\langle M \rangle \mid L(M) \in \mathcal{S}\}$ **unentscheidbar**.

> [!WARNING]
> Der Satz von Rice gilt nur für **semantische** Eigenschaften (Eigenschaften der erkannten Sprache), nicht für syntaktische Eigenschaften der TM-Beschreibung (z. B. "hat $M$ genau 5 Zustände?" ist entscheidbar).

## Related Concepts

- [[Turingmaschinen]]: Grundlegendes Berechnungsmodell
- [[Formale Sprachen]]: Einordnung in die Chomsky-Hierarchie
- [[Prädikatenlogik]]: Unentscheidbarkeit der prädikatenlogischen Allgemeingültigkeit
