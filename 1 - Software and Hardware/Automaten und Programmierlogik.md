---
title: AuPL
aliases:
  - Automaten und Programmierlogik
  - Automaten und formale Sprachen
tags:
  - 5CP
  - fb20
  - bachelor
  - pflichtmodul
  - semester-3
description: "Automatentheorie und formale Logik — formale Sprachen, endliche Automaten, Kellerautomaten, Turingmaschinen, Aussagenlogik, Prädikatenlogik, Beweiskalküle."
draft: false
---

# Syllabus

| Moodle       | —                                 |
| ------------ | --------------------------------- |
| Dozent       | Prof. Dr. U. Kohlenbach           |
| Vorlesung    | —                                 |
| Übung        | —                                 |
| Prüfungsform | Klausur                           |

# Teil I — Automatentheorie und formale Sprachen

## Kapitel 1 — Grundlagen formaler Sprachen

- [[Formale Sprachen]]: Alphabet $\Sigma$, Wörter $w \in \Sigma^*$, Sprachen $L \subseteq \Sigma^*$; Wort- und Sprachoperationen (Konkatenation, Kleene-Stern); Chomsky-Hierarchie (Typ 0–3)

## Kapitel 2 — Endliche Automaten

- [[Deterministische Endliche Automaten]]: DFA als 5-Tupel $(Q, \Sigma, \delta, q_0, F)$; erweiterte Übergangsfunktion $\hat{\delta}$; akzeptierte Sprache $L(A)$; Produktkonstruktion (Schnitt, Vereinigung); Komplementautomat; Minimalautomat
- [[Nichtdeterministische Endliche Automaten]]: NFA, $\varepsilon$-NFA; Nichtdeterminismus; Potenzmengenkonstruktion (Subset Construction); Äquivalenz DFA $\equiv$ NFA $\equiv$ $\varepsilon$-NFA

## Kapitel 3 — Reguläre Ausdrücke

- [[Reguläre Ausdrücke]]: Syntax und Semantik regulärer Ausdrücke; Satz von Kleene (RE $\equiv$ DFA $\equiv$ NFA); Thompson's Construction (RE → NFA); Zustandselimination (DFA → RE); algebraische Gesetze

## Kapitel 4 — Grenzen regulärer Sprachen

- [[Pumping-Lemma]]: Pumping-Lemma für reguläre Sprachen; Beweisschema für Nicht-Regularität; Abschlusseigenschaften regulärer Sprachen ($\cup, \cap, \overline{\phantom{L}}, \cdot, *$)

## Kapitel 5 — Kontextfreie Sprachen

- [[Kontextfreie Grammatiken]]: CFG als 4-Tupel $(V, \Sigma, P, S)$; Ableitungen und Ableitungsbäume; Mehrdeutigkeit; Chomsky-Normalform (CNF); CYK-Algorithmus (Wortproblem in $\mathcal{O}(n^3)$); Abschlusseigenschaften kontextfreier Sprachen
- [[Kellerautomaten]]: PDA als 7-Tupel; Akzeptanz durch Endzustand vs. leeren Keller; Äquivalenz CFG $\equiv$ PDA; deterministischer PDA (DPDA) als echte Teilklasse
- [[Pumping-Lemma]]: Pumping-Lemma für kontextfreie Sprachen; 5-Teile-Zerlegung $w = uvxyz$

## Kapitel 6 — Berechenbarkeit

- [[Turingmaschinen]]: TM als 7-Tupel; Berechnung und Akzeptanz (hält/hält nicht); Varianten (Mehrband, NTM); universelle TM; Church-Turing-These
- [[Entscheidbarkeit und Berechenbarkeit]]: Entscheidbar vs. erkennbar vs. ko-erkennbar; Halteproblem (Diagonalisierungsbeweis); Reduktionen ($A \leq_m B$); Satz von Rice; weitere unentscheidbare Probleme

# Teil II — Formale Logik

## Kapitel 7 — Aussagenlogik

- [[Aussagenlogik]]: Syntax (Formeln, Junktoren $\neg, \wedge, \vee, \to, \leftrightarrow$); Semantik (Belegungen, Wahrheitstafeln); Erfüllbarkeit, Allgemeingültigkeit, Folgerung; KNF und DNF; wichtige Äquivalenzen (De Morgan, Kontraposition); Kompaktheitssatz

## Kapitel 8 — Beweiskalküle (Aussagenlogik)

- [[Resolutionskalkül]]: Klauselform; Resolutionsregel; Widerlegungsvollständigkeit; Korrektheit und Vollständigkeit
- [[Sequenzenkalkül]]: Sequenzen $\Gamma \vdash \Delta$; Axiome; strukturelle Regeln; logische Regeln ($\neg, \wedge, \vee, \to$); Rückwärtsbeweisführung

## Kapitel 9 — Prädikatenlogik

- [[Prädikatenlogik]]: Signaturen; Syntax (Terme, Formeln, Quantoren $\forall, \exists$); freie und gebundene Variablen; Semantik (Strukturen, Interpretationen, Variablenbelegungen, Erfüllungsrelation $\models$); Modellbegriff; Kompaktheitssatz; Unentscheidbarkeit der PL1

## Kapitel 10 — Normalformen und Resolution (Prädikatenlogik)

- [[Normalformen der Prädikatenlogik]]: Pränexe Normalform; Skolemisierung (Eliminierung von $\exists$-Quantoren durch Skolem-Funktionen); Herbrand-Universum und Herbrand-Strukturen; Satz von Herbrand (Reduktion auf aussagenlogische Unerfüllbarkeit)
- [[Resolutionskalkül]]: Prädikatenlogische Resolution mit Unifikation; allgemeinster Unifikator (mgu); Occurs-Check; Korrektheit und Vollständigkeit (Satz von Robinson)
- [[Sequenzenkalkül]]: Quantorenregeln ($\forall L, \forall R, \exists L, \exists R$); Eigenvariablenbedingung
