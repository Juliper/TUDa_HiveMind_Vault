---
title: Kontextfreie Grammatiken
aliases:
  - CFG
  - Context-Free Grammar
  - Kontextfreie Sprache
  - CFL
  - Chomsky-Normalform
  - CNF
  - CYK-Algorithmus
  - CYK
tags:
  - automaten
  - logik
description: "Kontextfreie Grammatiken (CFG) — Ableitungen, Ableitungsbäume, Mehrdeutigkeit, Chomsky-Normalform und CYK-Algorithmus für das Wortproblem."
draft: false
---

Eine **kontextfreie Grammatik** (CFG) erzeugt [[Formale Sprachen|kontextfreie Sprachen]] (Typ 2 der Chomsky-Hierarchie). Sie ist mächtiger als [[Reguläre Ausdrücke]] und wird u. a. zur Beschreibung von Programmiersprachen-Syntax verwendet.

## Formale Definition

Eine CFG ist ein 4-Tupel $G = (V, \Sigma, P, S)$:

| Komponente | Bedeutung |
|---|---|
| $V$ | Endliche Menge von **Variablen** (Nichtterminale) |
| $\Sigma$ | Endliches **Terminalalphabet** ($V \cap \Sigma = \emptyset$) |
| $P \subseteq V \times (V \cup \Sigma)^*$ | Endliche Menge von **Produktionsregeln** $A \to \alpha$ |
| $S \in V$ | **Startsymbol** |

Eine Regel $A \to \alpha$ bedeutet: Die Variable $A$ kann durch die Zeichenkette $\alpha$ ersetzt werden — **unabhängig vom Kontext** (daher "kontextfrei").

## Ableitung

Eine **Ableitung** ist eine Folge von Regelanwendungen:

$$S \Rightarrow \alpha_1 \Rightarrow \alpha_2 \Rightarrow \ldots \Rightarrow w \in \Sigma^*$$

| Ableitungstyp | Beschreibung |
|---|---|
| **Linksableitung** | Immer die **linkeste** Variable wird ersetzt |
| **Rechtsableitung** | Immer die **rechteste** Variable wird ersetzt |

Die erzeugte Sprache: $L(G) = \{w \in \Sigma^* \mid S \Rightarrow^* w\}$

## Ableitungsbaum (Parse Tree)

Ein Ableitungsbaum visualisiert die Struktur einer Ableitung:
- Wurzel = Startsymbol $S$
- Innere Knoten = Variablen
- Blätter (von links nach rechts gelesen) = abgeleitetes Wort
- Kinder eines Knotens $A$ = rechte Seite einer Regel $A \to \alpha$

## Mehrdeutigkeit (Ambiguity)

Eine CFG $G$ heißt **mehrdeutig**, wenn es ein Wort $w \in L(G)$ gibt, das **zwei verschiedene Ableitungsbäume** hat.

> [!WARNING]
> Mehrdeutigkeit ist eine Eigenschaft der **Grammatik**, nicht der Sprache. Manche Sprachen sind **inhärent mehrdeutig**: Keine CFG für sie ist eindeutig.

## Chomsky-Normalform (CNF)

Jede CFG kann in eine äquivalente Grammatik in **Chomsky-Normalform** transformiert werden, in der alle Regeln die Form haben:

$$A \to BC \quad \text{oder} \quad A \to a \quad \text{(und optional } S \to \varepsilon\text{)}$$

wobei $A, B, C \in V$, $a \in \Sigma$, und $B, C \neq S$.

### Umwandlung in CNF

1. **$\varepsilon$-Regeln eliminieren**: $A \to \varepsilon$ entfernen (außer $S \to \varepsilon$)
2. **Kettenregeln eliminieren**: $A \to B$ durch direkte Regeln ersetzen
3. **Terminale isolieren**: $a$ in Regeln der Länge $\geq 2$ durch neue Variable $T_a \to a$ ersetzen
4. **Lange Regeln aufbrechen**: $A \to B_1 B_2 \ldots B_k$ in Kette von Zweier-Regeln umwandeln

## CYK-Algorithmus

Der **Cocke-Younger-Kasami** (CYK) Algorithmus löst das **Wortproblem** für CFGs in CNF: Gegeben $G$ und $w$, gilt $w \in L(G)$?

**Prinzip**: Dynamische Programmierung (Bottom-Up)

Für $w = a_1 a_2 \ldots a_n$ berechne die Tabelle $T[i,j]$ = Menge der Variablen, die $a_i \ldots a_j$ ableiten können:

1. **Basis**: $T[i,i] = \{A \mid A \to a_i \in P\}$
2. **Schritt**: $T[i,j] = \{A \mid \exists k: A \to BC \in P,\; B \in T[i,k],\; C \in T[k+1,j]\}$
3. **Ergebnis**: $w \in L(G) \Leftrightarrow S \in T[1,n]$

**Komplexität**: $\mathcal{O}(n^3 \cdot |G|)$

## Abschlusseigenschaften kontextfreier Sprachen

| Operation | Abgeschlossen? |
|---|---|
| Vereinigung $L_1 \cup L_2$ | Ja |
| Konkatenation $L_1 \cdot L_2$ | Ja |
| Kleene-Stern $L^*$ | Ja |
| Schnitt $L_1 \cap L_2$ | **Nein** |
| Komplement $\overline{L}$ | **Nein** |
| Schnitt mit regulärer Sprache $L_1 \cap R$ | Ja |

## Related Concepts

- [[Kellerautomaten]]: Äquivalentes Berechnungsmodell (PDA ↔ CFG)
- [[Formale Sprachen]]: CFGs erzeugen Typ-2-Sprachen
- [[Pumping-Lemma]]: CFL-Pumping-Lemma zum Nachweis der Nicht-Kontextfreiheit
- [[Reguläre Ausdrücke]]: Jede reguläre Sprache ist kontextfrei (echte Teilmenge)
