---
title: EiKI
aliases:
  - Einführung in KI
tags:
  - fb20
  - bachelor
  - semester-5
  - 5CP
description: ""
draft: false
---

- Planning (VL 13) nicht so relevant und auch Anwendungsaufgabe wie in Übung 11 werden nicht drankommen
- Taschenrechner zugelassen
- Cutsets
- Collapsing nodes
- Beweise anschauen
- Erklären, Rechnen und Ankreuzen Aufgaben
- Übungen sind gut
- A* beweis heraussuchen
- skolemesierung resolution

# Hilfsblatt

## KI Grundlagen

- KI sind Intelligente Maschinen, die Aufgaben erledigen können für die man menschenähnliche Intelligenz braucht
    
- General/strong AI (kann Alles) vs. Narrow/weak AI (Inselbegabung)
    
- Eigenschaften von KI
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/7878845f-76a0-45d4-a4aa-9859dd62c74e/Untitled.png)
    
    - Adaptability: Durch Erfahrung besser werden
    - Autonmous: Selbständiges arbeiten ohne Hilfestellungen
    - Law of Thoughts: Verstehen was richtig ist
    - Rational Behavior: Mach ich das richtige? (Maximierung von X)

## Intelligenz Grundlagen

Intelligenz ist die Fähigkeit, zu denken, zu lernen und entsprechend einer Situation und der Umgebung zu handeln. Sie ist ein Prozess der Anwendung von Wissen. Sie kann auch als die Fähigkeit definiert werden, sich an die Veränderungen in der Umwelt anzupassen.

### Turing Test

Wenn ein System von einem anderen intelligenten System nicht aufgrund seines Verhaltens erkannt werden kann.

1. Mensch verhört zwei Systeme (einer ist ein Computer)
2. Wenn er den Computer nicht erkennt, hat der Computer den Test bestanden

### Chinese Room Argument

Ist intelligentes Verhalten auch Intelligenz? Ist die Person hier intelligent?

1. Eine Person ist in einem Raum mit detaillierten Anleitungen wie man Mandarin übersetzen kann ohne dass man die Sprache verstehen kann.
2. Eine andere Person ist außerhalb und kann chinesische Notizen in den Raum schieben und bekommt sie übersetzt

## KI Systeme definieren

An AI system can be defined as the study of rational agents and their environments.

### Enviroment

Ist die Umgebung eines Agenten (z.B. bei Schach sind es das Brett du die Spielsteine). Ein Enviroment kann folgende Eigenschaften haben:

- Discrete (klar definierte, endlichviele Zustände) vs. Continuous
    - klar definierte, endlichviele Zustände (Schach) oder unendliche viele Zustände (Fußball)
- Observable vs. Partially Observable or Unobservable
    - Man kann den kompletten Zustand zu jedem zeitpunkt ermitteln oder nur teilweise
- Static vs. Dynamic
- Single Agent vs. Multiple Agents
- Accessible vs. Inaccessible
    - Wenn Agent komplettes Enviroment durch Aktionen erfassen kann
- Deterministic vs. Non-deterministic/Stochastic
    - Wenn der nächste Zustand nur vom aktuellen Zustand und den Handlungen des Agenten abhängt
- Episodic vs. Non-episodic/Sequential
    - In an episodic environment, each episode consists of the agent perceiving and then acting. The quality of its action depends just on the episode itself. In sequential environments the agent requires memory of past actions.

### Agent

Ein Agent nimmt die Umgebung wahr (Sense), trifft eigenständig Entscheidungen (Think) und handelt (Act).

**Reflex agent**

- Trifft Entscheidung nur anhand der aktuellen Wahrnehmung und nicht vergangenen
- Sehr beschränkt in seinen Entscheidungen
- Trifft Entscheidung nur anhand Dingen die er aktuell aktiv wahrnemen kann
- Schwer zu updaten und speichern in komplexen Enviroments

**Model-based**

- Merkt sich vergangene Zustände und trifft mit aktuellem Entscheidungen

**Goal-based**

- Wie Model-based, weiß aber auch welche Zustände gut sind
- Agent “denkt” also: “Was passiert wenn ich X mache”
- Wir kompliziert wenn nur viele Aktionen zu gewollten Zustand führen

**Utility-based**

- Wie Goal-based aber verwenden utility function

**Learning**

- Lernt von der Vergangenheit und wird besser
- Ist robuster gegen unbekannte Enviroments
- Vier konzeptionelle Elemente
    - **Learning Element:** Sorgt für Verbesserung durch lernen aus dem Enviroment
    - **Critic:** Gibt Feedback anhand einer bestimmten Metrik
    - **Performance Element:** Wählt richtige Aktionen aus
    - **Problem Generator:** Schlägt Aktionen vor die zu neuen Situationen führen

## Probleme definieren

### Begriffe:

- State Space: Alle möglichen Zuständen bzw. Situationen im Enviroment
- Path: Eine Sequenz von Zustände verbunden mit einer Aktionen Sequenz
- Transition: Stellt eine Aktion da
- Costs: Transitions können verschiedene Wertungen haben
- Solution: Path der zur Lösung führt
- Optimal Solution: Solution mit min Aktionen
- Planning Problem: Ein Probelm mit einem initalien Zustand den wir in einen Zielzustand verwandeln können
- Optimierungs Probleme: Ein Problem mit mehreren Lösungszuständen, aber das Ziel ist einen optimalen Zusatnd zu finden, anhand einer bestimmten funktion.

### Wie formuliert man ein Problem?

1. State Space and Initial State: Definiere den Anfangszustand und alle möglichen Zustände
2. Descriptions of Actions: Beschreibe alle möglichen Aktionen in einem Zustand
3. Goal Test: Teste ob der aktuelle Zustand dem Zielzustand entspricht
4. Costs: Definiere Kosten für Aktionen

### Wie kann man so ein Problem darstellen?

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/09fb394a-a810-499b-a04e-0db5e4d3e419/Untitled.png)

- Wie Zustandsautomat
- Jeder Knoten stellt Zustand da und Pfeile die Aktionen

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/081e188b-042c-44a0-b0e5-7bf0824d6a8e/Untitled.png)

- Baumdiagramm
- Jeder Knoten des Baums stellt einen gesamten Path im State Space Graph da

### Unterschied zwischen State und Node

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/fe7d1f44-27cc-4ba5-b608-289bf69503a5/Untitled.png)

## Uninformierte Suche

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/6ad5c04b-c1e4-4563-8a08-9d00b2edfbec/Untitled.png)

||Completeness|Time Complexity|Space Complexity|Optimality|
|---|---|---|---|---|
|Breadth first search|Ja falls alle Kosten positiv ansonsten endless loops|O(b^d)||JA weil nach Kosten expandiert wird|
|Uniform cost search|Ja falls alle Kosten positiv ansonsten endless loops|$O(b^{1+floor(OptCost/eps)})$||JA weil nach Kosten expandiert wird|
|Depth first search|Nop, kann bei unendlicher Tiefe und loops nix|Erkundet Branch bis zur maximalen Tiefe, schlecht wen tiefe des Ziels höher|Nur aktuellen branch und unexpandierten geschwiter werden gespeichert, daher linear O (b * m)|Nop|
|Depth limited search|Nop|O(b^l)|O(b * l|nop|
|Iterative deeping depth first search|Jep|Ersten Level werden d mal erkundet|O(b * d)|Jep|
|Bidirectional Search|||||

### Uniform cost search (Dijkstra bei graph search)

- Jeder Knoten hat Kosten zugeordnet
- Kosten werden über Pfad hinweg addiert
- Stoppt nicht direkt wenn Goal erreicht sondern erforscht aktuelles Level zuende

### Breadth first search

- Wie uniform cost aber alle Kosten sind gleich
- Erkundet Level für Level von Links nach Rechts
- Stoppt wenn Goal erreicht

### Depth first search

- Erforscht erst alle linken Pfade
- Geht Schrittweise zurück und erforscht Alternativen von Links nach Rechts
- Stoppt wenn Goal erreicht

### Depth limited search

- limitiert Suchtiefe zu l

### Iterative deeping depth first search

- Tiefe wird Schrittweise erhöht

### Bidirectional Search

- Zwei Suchen gleichzeitig

## Heuristiken

- Jede Consitent Heuristic ist admissible
- Wenn h(n) consitent dann sinkt der Wert von f(n) auf einem Pfad nicht

### Admissible

- h(n) ≤ h*(n) (wahre kosten von n bis zum Ziel)
- z.B. Luftlinie

### Consistent

- h(n) ≤ c(n,a,n’) (Kosten durch Aktion a)+ h(n’)

### Dominance

- Wenn h1 und h2 admissable und h2(n) ≥ h1(n) dann ist h2 dominant
- Dominante heuristiken = weniger expandieren

### Combinations

- Wenn h1 und h2 admissible dann h(n) = max{h1(n), h2(n), … hm(n)} auch und dominiert h1 und h2

## Informierte Suche

||Completeness|Time Complexity|Space Complexity|Optimality|
|---|---|---|---|---|
|Greedy Best-first Search|Nop, weil endlos Schleifen|O(b^m)|O(b^m)|Nop|
|A* Search|Jep, außer es gibt unendlich viele Knoten mit f(n) ≤ f(G)|||Wenn h(n) admissible|

### Greedy Best-first Search

- f(n) = h(n)
- Benutzt heuristik Funktion die die Kosten von einem Knoten zum Ziel abschätzt. Daran wird dan entschieden welcher Knoten expandiert wird

### A* Search

- Berücksichtigt berreits entstandene Kosten
- f(n) = g(n) “Kosten bis jetzt um n zu erreichen” + h(n) “Schätzung der Kosten um von n zum Ziel zu gelangen”
- Benutz f(n) um zu bestimmen welcher Knoten expandiert werden soll

## Lokale Suche

Gut für große Suchräume, da nur ein Zustand betrachtet wird und daher nicht mehrer Pfade gespeichert werden müssen. Stellt aber keine Completeness oder Optimality sicher.

### Ridge Problem

Wenn diskrete states versuchen continuierliche bereiche abzutasten

### Multi-Dimensional problem

Globales Optimum schwerer zu finden wenn viele features

### Algorithmen

### Hill Climbing / Greed Local Search

Findet nur lokale Maxima

1. Alle Nachbarzustände angucken
2. Und den wählen mit dem max Wert
3. oder beenden falls es überall nur weniger ist

### Randomized Restart Hill Climbing

Wie normales aber mehrmals an verschiedenen Startpositionen

### Stochastic Hill-Climbing

Die nächsten Zustände werden zufällig gewählt, wobei gute Zustände eine höhere wahrscheinlichkeit haben

### Gradient Descent

Mittels Gradienten hill finden. Benutzt Lerning Rate für Schrittweite

### Beam Search

Wie hill climbing aber, man merkt sich nicht nur einen Zustand sondern k und nimmt immer die k besten Nachfolger

### Simulated Annealing

Ab und zu Schritt in falsche Reichtung.

As time passes, the probability that a down-hill step is taken is gradually reduced and the size of any down-hill step taken is decreased.

Temperatur ist parameter, der bestimmt wie oft schlechte moves gemacht wird

### Adversial Search

||Completeness|Time Complexity|Space Complexity|Optimality|
|---|---|---|---|---|
|Minimax|Jep, wenn Baum endlich|O(b^m)|O(b*m)|Jep, wenn Gegner optimal|
|Alpha Beta Pruning|Jep, außer es gibt unendlich viele Knoten mit f(n) ≤ f(G)|||Wenn h(n) admissible|

### MINIMAX

Auf jeder Stufe des Baums ist MIN oder MAX am Zug

1. Von unten nach oben auswerten, welchen Weg min bzw. max wählen würden

### Alpha Beta Pruning

Es wird immer gepruned, wenn alpha ≥ beta

1. Root wird mit geg. Schranken initialisiert
2. Baum wird depth first durchgangen
3. Wenn an leafs angekommen wird wenn MAX am Zug ist alpha geupdated und beta wenn MIN am zug ist
4. Wir gehen den Baum wieder nach oben und alpha beta wird geupdated

## Constraint Satisfaction Problems

Besteht aus:

- Einem Zustand, der durch Variablen mit Werten aus bestimmten Domänen beschrieben wird
- Ein Goal Test bestehend aus Constraints

### General-purpose heuristics

- Mininum Remaining Values Heuristic: Wähle die Variable mit den wenigsten consitenten werten
- Degree Heuristic: Wähle die Variable mit den meisten constraints
- Least Constraining Value Heuristic: Wähle den Wert der für die anderen Variablen die wenigsten Werte ausschließt

### Cryptarithmetic-Problem

1. Domänen von Variablen definieren (z.B. domain(A) = {1, …, 9})
2. Constraints definieren

### Backtracking-Search

1. Der Reihenfolge nach Variablen auswählen und den ersten Wert der Domäne zuweisen
2. Checken on Varibale konsistent mit constraints ist
3. Nächste Variable wählen
4. Falls nicht konsistent anderen Wert in Domäne wählen
5. Falls Domäne komplett durchlaufen, den Wert der vorherigen Variable ändern

Verbesserungen:

### Forward-Checking

Wie Backtracking-Search, aber wenn ein Wert zugewiesen wird, wird überprüft ob Werte für andere Variablen ausgeschlossen werden (Domände wird aktualisiert)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/d956cb76-7c83-45c4-8627-a951fa31e9c1/Untitled.png)

### Constraint Graph

Jeder Variable ist ein Knoten und jede Kante stellt Cosntraint da

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/cf0f9e61-fd5e-4b14-8cba-72d9d8bd9752/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/305cafeb-1974-49c6-b6ea-d9f2731b223d/Untitled.png)

Die am wenigsten andere beeinflusst

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/1eb8a2b8-b254-4232-83ff-168668e01711/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/0e8336d7-b0b1-4115-8a50-0ab46a4caa8b/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/94176994-dba2-49a3-98b4-9bb1e3a953c5/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/2c11d73a-2318-4cf1-9712-b9789434fd29/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/3f9c7ea4-0b88-44bc-94d7-eb17e7c44123/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/d515459d-df94-4e22-905e-58f7bed565bb/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/1f0bc96d-a4f6-4855-8c92-810d658c1be6/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/0785573d-d10c-4689-be3a-52b6cf8e8ca6/Untitled.png)

## Aussagenlogik

### Resolution

Geg.: Knowledgebase (Menge von Formeln in KNF) und neues Wissen (neue Formeln)

1. Negation der neuen Formel zu Knowledgebase hinzufügen
2. Dann alle Literale nebeneinander aufschreiben und geschickt kombinieren
3. Es gilt: (A OR B) AND NOT B == A

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/e49e2b63-378f-4064-af37-05dcb80a314b/Untitled.png)

### Intelligent Agents

- Nimmt enviroment wahr mit Sensoren
- Wahrnehmung und knowledge base für aktionen verwenden

### Knowledge-based Agents

- Represent states, actions, etc…
- Incorporate new percepts
- Update internal representations of the world
- Deduce hidden properties of the world
- Deduce appropriate actions

## Prädikatenlogik

Skolemisierung

Resolution

## Unsicherheiten

Formeln:

- $P(A \lor B) = P(A) + P(B) - P(A \land B)$
- $P(A|B) = \frac{P(A\land B)}{P(B)}$ bzw. $P(A\land B) = P(A|B) \cdot P(B)$ (Produktregel)
- $P(Y) = \sum^n_{i=1} P(x_i,Y)$

Rationalität: $0 \leq P(A \land B) \leq min(P(A), P(B))$

### Variablen-Eliminationsalgorithmus

1. Schrittweise Variablen auswählen
2. Alle P (Wahrscheinlichkeiten) in denen die Variable auftritt zusuammenfassen zu $f_x(y,z)$ y,z sind dabei alle andere variablen die in P vorkamen
3. Speziellfall: Wenn x variable und nur P(x|a) ausgewählt wird und daher $f_x(a) = \sum_x P(x|a) = 1$

### Probabilities

Fassen folgende Effekte zusammen:

- Laziness: Man will nicht alles aufzählen was falsch laufen kann
- Theoretical Ignorance: Man kann manche Sachen garnicht wissen
- Practical Ignorance: Über manche Sachen weiß man einfach nicht bescheid (Stau)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/cd0994b1-d2a0-487b-bf72-d7a829f34043/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/96d1b4ec-49c0-4fbe-9224-9ae545262c7d/Untitled.png)

### Arten von Wahrscheinlichkeiten

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/5e6dbd96-09fc-4c34-bf4f-d2e1fd959215/Untitled.png)

- Joint Distribution/Verbundswahrscheinlichkeit: $P(x,y) = P(nok, nos) = 0.768$
- Marginalisierung: $P(nok) = \sum^n_{i=1}P(s_i, nok) = 0.768 + 0.132 + 0.035$
- $P(a,b|c) = \frac{P(a \land b \land c)}{P(c)}$
- $P(A \land B) = P(A) \cdot P(B|A)$ bzw. $P(A_n \land ...\land A_1) = P(A_n | A_{n-1} \land ... \land A_1) \cdot P(A_{n-1}\land ... \land A_1)$(Kettenregel)
- $P(x|y) = \frac{P(y|x)P(x)}{P(y)}$ (Bayes)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/27c44476-3abd-40db-a01e-490ceafc74f1/Untitled.png)

### Bayesian Networks

Verwendung von unabhängigkeiten um Repräsentation zu komprimieren führt zu nur linearem Wachstum nach n

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/5edf90ef-e83f-43ed-ac20-bf1c85747865/Untitled.png)

### Samling Techniques

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/c7ad0bfd-88cf-4697-90f5-49b7a07b9bbc/Untitled.png)

- Forward: Einfach für jeden Zustand zufällig einen Wert wählen (True, False) und an der erhaltenen Statistik Wahrscheinlichkeiten berechnen
- Gibbs Sampling: Wenn man irgendwo im Graphen etwas true haben will zum testen dann beginnt man mit passendender Evidenz und zieht nur andere Variablen neu (dank markov blanket)
- Markov Blanket: Jeder Knoten ist unabhängig von anderen Knoten außer Eltern, Kinder und Kinder-eltern

## Machine Learning

Ist nicht Input + Program = Output sondern Input + Output = Program

### Arten von Learning

- Memorization (Declarative Knowledge)
    - Anhäufung von Fakten
    - Wir limitiert von Zeit und Speicher
- Generalization (Imperative Knowledge)
    - Aus bereits vorhandenen Wissen neues ableiten
    - limitiert durch genauigkeit der ableitung
- Supervised Learning
    - Lernen mit gelabelte Datensätze
- Unsupervised Learning
    - Lernt auf Datensatz ohne label und soll einfach Unterschiede bzw. Ähnlichkeiten erkennen
- Reinforcement Learning
    - Lernt durch positiven und negativen reward nach Aktionen

## Supervised Learning

### Task types

- Classification: Will einen neuen Wert einem Label zuordnen (sucht Funktionen die Datenpunkte nach Klasse gut trennt)
- Regression: Will neuen Wert vorhersagen (Funktion die gut auf allen Punkten liegt)

### Feature Engineering

- Feature als vektoren
- welche Feature sind wichtig
- Garbage in Garbage out: schlechte Daten verursachen bias

### Evaluation

- $MeanSquareError = \frac{1}{n}\sum^n_{i = 1} (y_i - y'_i)^2$

### Overfitting

Sehr komplexe Lösung die gut für unsere Trainingsdaten ist, aber schlecht bei anderen Daten

Verhindern (Regularisierungsmethoden) durch:

- Split Data: Bestimmte Daten “geheim” halten und Modell darauf testen um overfitting zu erkennen
- Early Stopping: Learning wird gestoppt, wenn Fehler auf Test set wieder steigt
- Dropout: Macht Netz robuster, da während Training Neuronen oder Verbindungen ausgestellt werden

## Deep Learning

Skipt das manuelle Feature Extraction sondern verwendet neuronale Netze dafür

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/292e0941-dfd3-4afd-8754-5e73cb792076/Untitled.png)

### Aktivierungs Funktion

- Fügt neuronalen Netzten nicht-linearität zu wodurch auch nicht lineare Probleme gelößt werden können
- Ermöglichen backpropagation

### Forward Propagation

Für einen Knoten einfach alle input * weight und ann aufsummieren und in aktivierungsfunktion packen

### Backpropagation (nochmal angucken)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/637b00ce-0cb7-4947-8884-ced7a46a3c29/Untitled.png)

Gradient decent

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/b41bdcaf-cac9-4a4b-8806-ada2290510d2/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/2859b0b4-fe8b-478e-9b83-ea81ffc8ecba/Untitled.png)

## Reinforcement Learning

Agent erhält feedback in Form von Belohnugen und Agent will diese Belohnungen maximieren

Sucht nach Policys (welche Aktion in welchem State) um summe aller rewards zu maximieren (unendliche Summen schwer zu maximieren)

Ist meistens als Markov Decision Process (MDP) dargestellt wobei reinforcement learning eigentlich ohne mdp modell ist

Ist NICHT supervised learning, weil kein korrektes input/output paar gegeben wird

### Markov Decision Process (MDP)

- Besteht aus Zuständen, Aktionen, Transitionen (In welchen Zustand s’ kommt man, wenn man in Zustand s Aktion a ausführt P(s’|s, a)) und eine Reward Function
- Nächstes Zustand ist unabhängig von vergangenen Zuständen und Prozessen

### Credit Assignment Problem

- Wenn man für eine Sequenz von Aktionen eine Belohnung erhält, kann man nicht wissen welche Aktion den Reward verursacht hat

### Für Summierung von Rewards mit discount Faktoren

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/9c7f8ba6-f625-425c-aff3-fb7e88f5b710/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/280ec5ad-befe-42c7-8732-a3f646d4f3bb/Untitled.png)

### Value Iteration

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/270e1d0f-0648-4f44-ac1d-d0c9e38b0d01/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/c08ca092-c6ed-4545-8ec4-6078f43ff9ce/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/4dd7b363-a653-439e-8505-31d42e5be80c/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/a648e821-f0e6-4003-8486-5b98e7dad433/Untitled.png)

### Sample-based policy evaluation

- Take samples of outcomes s’ (by doing the action!) and average

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/ceababa1-30fc-4d7d-b2e2-fc8dce725427/Untitled.png)

### Temporal-Difference Learning

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/f334cae5-df95-41dc-be7f-1bc683d3f3ea/Untitled.png)

### Exploration Dilemma

Um etwas optimal zu machen muss man ertsmal fehler machen

### Q-Learning

### AlphaGO etc.

- GO hat riesigen Suchbaum bzw. Spielbaum
- mittels Modell dahger kein klassisches reinforcement learning
- Evaluierung der Spielzustände wird durch neuronales Netzt gemacht
- Das Auswählen der Pfade die man expandierung will werden durch eine Gewichtung von Exploration und Exploitation gemacht

## Planning

Explizitere und genauere Beschreibung des Enviroments (logische Darstellung von States und Actions)

Wir wollen eine Sequenz an Actionen um unsere Subgoals zu erfüllen

Frame Problem: Man spezifiziert nur was sich ändert und nicht was gleich bleibt

Qualification Problem: Schwierig zu definieren was alles erfüllt sein muss damit eine Aktion ausführbar ist

Ramification Problem: Schwierig alle Effekte einer Aktion zu definieren

### STRIPS

- Zustände werden durch alles was wahr ist beschrieben, der Rest ist falsch
- Aktionen haben Vorbedinung und ändern Sachen zu wahr oder falsch