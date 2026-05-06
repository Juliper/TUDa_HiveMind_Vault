---
title: Sequenzenkalkül
aliases:
  - Sequent Calculus
  - Sequenz
  - Gentzen-Kalkül
tags:
  - automaten
  - logik
description: "Sequenzenkalkül (Gentzen-Kalkül) — Beweissystem mit Sequenzen, strukturellen und logischen Regeln für Aussagen- und Prädikatenlogik."
draft: false
---

Der **Sequenzenkalkül** (auch Gentzen-Kalkül) ist ein formales Beweissystem, das — im Gegensatz zum [[Resolutionskalkül]] — **direkt** Allgemeingültigkeit nachweist, ohne den Umweg über Widerlegung.

## Sequenzen

Eine **Sequenz** hat die Form:

$$\Gamma \vdash \Delta$$

| Komponente | Bedeutung |
|---|---|
| $\Gamma$ (Antezedent) | Endliche Menge von Formeln (Annahmen) |
| $\Delta$ (Sukzedent) | Endliche Menge von Formeln (Behauptungen) |

**Semantik**: $\Gamma \vdash \Delta$ ist gültig gdw. $\bigwedge \Gamma \to \bigvee \Delta$ allgemeingültig ist. D. h.: Jede Belegung, die alle Formeln in $\Gamma$ wahr macht, macht mindestens eine Formel in $\Delta$ wahr.

## Axiom

$$\frac{}{\Gamma, \varphi \vdash \Delta, \varphi} \quad \text{(Ax)}$$

Eine Sequenz ist ein **Axiom**, wenn eine Formel auf **beiden Seiten** vorkommt.

## Strukturelle Regeln

| Regel | Schema |
|---|---|
| **Weakening links** | $\dfrac{\Gamma \vdash \Delta}{\Gamma, \varphi \vdash \Delta}$ |
| **Weakening rechts** | $\dfrac{\Gamma \vdash \Delta}{\Gamma \vdash \Delta, \varphi}$ |
| **Contraction** | Mehrfaches Vorkommen einer Formel auf einer Seite wird zu einem |

## Logische Regeln (Aussagenlogik)

### Negation

$$\frac{\Gamma \vdash \Delta, \varphi}{\Gamma, \neg\varphi \vdash \Delta} \; (\neg L) \qquad \frac{\Gamma, \varphi \vdash \Delta}{\Gamma \vdash \Delta, \neg\varphi} \; (\neg R)$$

### Konjunktion

$$\frac{\Gamma, \varphi, \psi \vdash \Delta}{\Gamma, \varphi \wedge \psi \vdash \Delta} \; (\wedge L) \qquad \frac{\Gamma \vdash \Delta, \varphi \quad \Gamma \vdash \Delta, \psi}{\Gamma \vdash \Delta, \varphi \wedge \psi} \; (\wedge R)$$

### Disjunktion

$$\frac{\Gamma, \varphi \vdash \Delta \quad \Gamma, \psi \vdash \Delta}{\Gamma, \varphi \vee \psi \vdash \Delta} \; (\vee L) \qquad \frac{\Gamma \vdash \Delta, \varphi, \psi}{\Gamma \vdash \Delta, \varphi \vee \psi} \; (\vee R)$$

### Implikation

$$\frac{\Gamma \vdash \Delta, \varphi \quad \Gamma, \psi \vdash \Delta}{\Gamma, \varphi \to \psi \vdash \Delta} \; (\to L) \qquad \frac{\Gamma, \varphi \vdash \Delta, \psi}{\Gamma \vdash \Delta, \varphi \to \psi} \; (\to R)$$

## Quantorenregeln (Prädikatenlogik)

$$\frac{\Gamma, \varphi[t/x] \vdash \Delta}{\Gamma, \forall x\, \varphi \vdash \Delta} \; (\forall L) \qquad \frac{\Gamma \vdash \Delta, \varphi[y/x]}{\Gamma \vdash \Delta, \forall x\, \varphi} \; (\forall R)^*$$

$$\frac{\Gamma, \varphi[y/x] \vdash \Delta}{\Gamma, \exists x\, \varphi \vdash \Delta} \; (\exists L)^* \qquad \frac{\Gamma \vdash \Delta, \varphi[t/x]}{\Gamma \vdash \Delta, \exists x\, \varphi} \; (\exists R)$$

> [!WARNING]
> Bei $(\forall R)$ und $(\exists L)$ muss $y$ eine **frische Variable** sein (Eigenvariablenbedingung), die weder in $\Gamma$, $\Delta$ noch in $\varphi$ frei vorkommt (außer an der Stelle von $x$).

## Beweisführung

Ein **Beweis** ist ein Baum, der von unten nach oben gelesen wird:
1. Wurzel = zu beweisende Sequenz (Ziel)
2. Regeln anwenden, bis alle Blätter **Axiome** sind
3. Wenn alle Blätter Axiome → Beweis erfolgreich

> [!NOTE]
> Die Regelanwendung erfolgt **rückwärts** (von der Konklusion zu den Prämissen). Man "zerlegt" die Zielsequenz systematisch.

## Korrektheit und Vollständigkeit

| Eigenschaft | Aussage |
|---|---|
| **Korrekt** | Jede beweisbare Sequenz ist gültig |
| **Vollständig** | Jede gültige Sequenz ist beweisbar |

Gilt sowohl für die aussagenlogische als auch die prädikatenlogische Variante.

## Related Concepts

- [[Aussagenlogik]]: Sequenzenkalkül für AL-Beweise
- [[Prädikatenlogik]]: Erweiterung mit Quantorenregeln
- [[Resolutionskalkül]]: Alternatives Beweisverfahren (Widerlegung)
