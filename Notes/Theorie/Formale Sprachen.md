---
title: Formale Sprachen
aliases:
  - Formal Languages
  - Alphabet
  - Wort
  - Sprache
  - Kleene-Stern
tags:
  - automaten
  - logik
description: "Grundbegriffe formaler Sprachen — Alphabet, Wort, Sprache, Sprachoperationen (Vereinigung, Konkatenation, Kleene-Stern) als Fundament der Automatentheorie."
draft: false
---

**Formale Sprachen** bilden das mathematische Fundament der Automatentheorie und beschreiben die Mengen von Zeichenketten, die von Automaten erkannt oder von Grammatiken erzeugt werden.

## Grundbegriffe

| Begriff | Definition |
|---|---|
| **Alphabet** $\Sigma$ | Endliche, nichtleere Menge von Symbolen (Zeichen) |
| **Wort** $w$ | Endliche Folge von Symbolen aus $\Sigma$, z. B. $w = a_1 a_2 \ldots a_n$ |
| **Leeres Wort** $\varepsilon$ | Wort der Länge 0 (enthält kein Symbol) |
| **Wortlänge** $|w|$ | Anzahl der Symbole in $w$; $|\varepsilon| = 0$ |
| **$\Sigma^*$** (Kleene-Stern) | Menge aller Wörter über $\Sigma$ (einschließlich $\varepsilon$) |
| **$\Sigma^+$** | $\Sigma^* \setminus \{\varepsilon\}$ — alle nichtleeren Wörter |
| **Sprache** $L$ | Beliebige Teilmenge $L \subseteq \Sigma^*$ |

> [!NOTE]
> $\Sigma^*$ ist immer **abzählbar unendlich**, selbst für ein einelementiges Alphabet. Die Menge aller Sprachen über $\Sigma$ ist dagegen **überabzählbar** (Potenzmenge von $\Sigma^*$).

## Wortoperationen

| Operation | Notation | Definition |
|---|---|---|
| **Konkatenation** | $u \cdot v$ oder $uv$ | Hintereinanderhängen: $u = a_1\ldots a_m$, $v = b_1\ldots b_n$ $\Rightarrow$ $uv = a_1\ldots a_m b_1\ldots b_n$ |
| **Potenz** | $w^k$ | $k$-fache Konkatenation; $w^0 = \varepsilon$ |
| **Reversal** | $w^R$ | Umkehrung: $(a_1 a_2 \ldots a_n)^R = a_n \ldots a_2 a_1$ |

Die Konkatenation ist **assoziativ** mit **neutralem Element** $\varepsilon$, d. h. $(\Sigma^*, \cdot, \varepsilon)$ ist ein Monoid.

## Sprachoperationen

Seien $L_1, L_2 \subseteq \Sigma^*$ Sprachen:

| Operation | Notation | Definition |
|---|---|---|
| **Vereinigung** | $L_1 \cup L_2$ | $\{w \mid w \in L_1 \text{ oder } w \in L_2\}$ |
| **Schnitt** | $L_1 \cap L_2$ | $\{w \mid w \in L_1 \text{ und } w \in L_2\}$ |
| **Komplement** | $\overline{L}$ | $\Sigma^* \setminus L$ |
| **Konkatenation** | $L_1 \cdot L_2$ | $\{uv \mid u \in L_1, v \in L_2\}$ |
| **Kleene-Stern** | $L^*$ | $\bigcup_{k=0}^{\infty} L^k = \{\varepsilon\} \cup L \cup LL \cup LLL \cup \ldots$ |
| **Kleene-Plus** | $L^+$ | $\bigcup_{k=1}^{\infty} L^k = L \cdot L^*$ |

> [!IMPORTANT]
> Der Kleene-Stern enthält **immer** $\varepsilon$ (da $L^0 = \{\varepsilon\}$), unabhängig davon, ob $\varepsilon \in L$.

## Die Chomsky-Hierarchie

Formale Sprachen werden nach der Ausdrucksstärke der erzeugenden Grammatiken klassifiziert:

| Typ | Sprachklasse | Erkenner | Abgeschlossen unter |
|---|---|---|---|
| **Typ 3** | Reguläre Sprachen | [[Deterministische Endliche Automaten\|DFA]] / [[Nichtdeterministische Endliche Automaten\|NFA]] | $\cup, \cap, \overline{\phantom{L}}, \cdot, *$ |
| **Typ 2** | Kontextfreie Sprachen | [[Kellerautomaten\|PDA]] | $\cup, \cdot, *$ (nicht $\cap, \overline{\phantom{L}}$) |
| **Typ 1** | Kontextsensitive Sprachen | Linear beschränkte Automaten | $\cup, \cap, \cdot, *$ |
| **Typ 0** | Rekursiv aufzählbare Sprachen | [[Turingmaschinen\|TM]] | $\cup, \cdot, *$ |

Jede Klasse ist echte Teilmenge der nächsten: Typ 3 $\subsetneq$ Typ 2 $\subsetneq$ Typ 1 $\subsetneq$ Typ 0 $\subsetneq \mathcal{P}(\Sigma^*)$.

## Related Concepts

- [[Deterministische Endliche Automaten]]: Erkenner für reguläre Sprachen (Typ 3)
- [[Reguläre Ausdrücke]]: Kompakte Notation für reguläre Sprachen
- [[Kontextfreie Grammatiken]]: Erzeuger für kontextfreie Sprachen (Typ 2)
- [[Turingmaschinen]]: Erkenner für Typ-0-Sprachen
