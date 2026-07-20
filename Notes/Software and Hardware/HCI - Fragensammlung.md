---
title:
aliases:
tags:
  - fb20
description:
draft: false
---
## Unsichere Fragen:

* Was sind die 4 Bestandteile von User Centered Design? Nenne das Ziel von jedem. Nenne eine praktische Methode zu jedem Bestandteil und erkläre diese.
* Unterschied zwischen Visibility und Feedback
* External cognition / Distributed Cognition / Extended Mind Theory erklären und 3 Arte nennen, jeweils ein Beispiel geben

## A - Cognition

> [!question]- 1.1 Wie viele Chunks passen ins Arbeitsgedächtnis? Wie kann man das auf Interaktionsdesign anwenden?
>
> **7 ± 2 Chunks**. Anwendung: Menüs, Auswahllisten, Navigationspunkte oder gleichzeitig sichtbare Optionen auf ~7 Elemente begrenzen; Information in sinnvolle Chunks gruppieren (z.B. Telefonnummern in Blöcke), damit sie ins Arbeitsgedächtnis passt.

> [!question]- 1.2 Was sagt die Distributed Cognition / Extended Mind Theory aus? Nenne die zwei Arten und jeweils ein Beispiel.
>
> Technologie (z.B. das Smartphone) übernimmt und **ersetzt Teile des eigenen Verstandes/Gedächtnisses**. Statt Nummern und Wege zu erinnern, nutzen wir Funktionen des Geräts - das Denken erstreckt sich also über die Grenzen des Gehirns hinaus in die Umwelt. Das erhöht die Bedeutung guter Interfaces.
> 
> **Extended/External Memory** - navigating with a map or writing down notes
> **Extended/External Process** - speed display in your car or calculator

> [!question]- 1.3 Was ist das **Model Human Processor** und welche Aspekte beinhaltet es nicht?
>
>Modelliert den Menschen mit drei Blöcken
> - a sensory input subsystem
> - a central information processing subsystem
> - a motor output subsystem
>
> Das Modell klammert **Körper**, **Emotionen** und **Kontext**  aus - es behandelt den Menschen wie einen reinen Informationsverarbeiter.

> [!question]- 1.5 Erkläre die 2 Richtungen der Wahrnehmung anhand eines Beispiels.
>
> - **Bottom-Up (data-driven)**: Wahrnehmung wird direkt aus dem Sinnesreiz aufgebaut - von einfachen Merkmalen (Kanten, Farben, Kontraste) hin zu komplexen Strukturen, ohne Vorwissen.
> - **Top-Down (knowledge-driven)**: Vorwissen, Erwartung und Kontext prägen die Interpretation; mehrdeutige/unvollständige Reize werden mit Erfahrung ergänzt.
> - **Beispiel "13"**: Bei Bottom-Up nur zwei senkrechte und drei horizontale Striche. Bei Top-Down sind wird es als 13 oder B wahrgenommen.

> [!question]- 1.6 Was sagt Helmholtz's theory of unconscious inference aus? Zeichne ein Beispiel.
>
> Wahrnehmung ist das Ergebnis **unbewusster, automatischer Schlüsse**, die das Gehirn aus mehrdeutigen Sinnesdaten auf Basis von Erfahrung zieht - es landet bei der wahrscheinlichsten Interpretation der Welt. (Beispiel Zugschienen mit zwei horizontalen)

> [!question]- 1.7 Was sind die Gestalt Laws.
>
>  Gestalt Principles are principles/laws of human perception that describe how humans group similar elements, recognize patterns and simplify complex images when we perceive objects.
>  
> - **Closure**: The principle of closure states that when we look at a complex arrangement of visual elements, we tend to look for a single, recognizable pattern.
> - **figure-ground**: The figure-ground principle states that people instinctively perceive objects as either being in the foreground or the background. As a human, you can focus on either the foreground or the background
> - **Common Fate**: The law of common fate suggests that when multiple visual elements move in the same direction or at the same speed, we tend to perceive them as a cohesive unit or a single entity rather than individual components.
> - **proximity**: The principle of proximity states that things that are close together appear to be more related than things that are spaced farther apart.
> - **similarity**: The principle of similarity states that when things appear to be similar to each other, we group them together and we also tend to think they have the same function.
> - **common-region**: The principle of the common region is highly related to proximity. It states that when objects are located within the same closed region, we perceive them as being grouped together
> - **continuity**: The principle of continuity states that elements that are arranged on a line or curve are perceived to be more related than elements not on the line or curve.

> [!question]- 1.9 Was sind Affordances? Nenne die Typen.
>
> Affordances sind Eigenschaften eines Artefakts, die einen bestimmten Gebrauch **nahelegen** ("ist für"), oft in Physiologie/Körper verankert. Sind sie gut, braucht es keine Labels.
> 
> - **Perceptible**: Perceptible eigenschaften deuten auf nutzung hin (tür mit griff -> ziehen)
> - **Hidden**: keine obvious affordance und nutzer muss auf erfahrung und trial and error setzen (hover/click in dropdown menus)
> - **False**: objekt deutet auf nutzung hin, die es nicht gibt (unterstrichener text aber kein hyperlink, tür mit griff aber muss aufgedrückt werden)

> [!question]- 1.11 Was sind Constraints? Wie hängen sie mit Affordances zusammen?
>
> Constraints **schränken die möglichen Handlungen ein** - das "Inverse" von Affordances (und ergänzen sie oft). Ziele: Bedienfehler vermeiden, zu merkende Information minimieren. Arten:
> - **Physical** - Stecker passt nur in einer Ausrichtung.
> - **Logical** - logische Schlüsse schließen Lösungen aus (z.B. nur gültige Kalendertage wählbar).
> - **Semantic** - Weltwissen
> - **Cultural**: Konventionen wie rot = Stopp
> - **Zusammenhang**: Affordances zeigen, was *getan werden kann*, Constraints beschränken, was *nicht getan werden kann* - zusammen engen sie den Möglichkeitsraum auf die intendierten Aktionen ein.

> [!question]- 1.12 Nenne die Dark Patterns.
>
> - **Nagging** - redirection of expected functionality that persists across interactions (e.g. repeated pop-ups asking to enable notifications after being dismissed)
> - **Obstruction** - making a process more difficult than necessary to dissuade an action (e.g. burying "cancel subscription" behind multiple confirmation screens)
> - **Sneaking** - Attempting to hide, disguise, or delay the divulging of information that is relevant to the user (hide ads in reviews)
> - **Interface Interference** - Manipulation of the user interface that privileges certain actions over others (highlight buttons etc)
> - **Forced Action** - Wenn user gewzungen sind eine AKtion auszuführen

> [!question]- Was für Mappings gibt es?
>
> Connect functionality to (UI) elements/to the real world.
> 
> - **Spatial Analogy** - arrange controls the same way as their real-world counterparts (room lamps, driving wheel, car stereo audio fader)
> - **Physical Analogy** - mapping follows physical real-world behavior (e.g. rising level = more, falling level = less); natural for additive dimensions like amount, heat, volume, thickness, brightness, weight
> - **Cultural Analogy** - mapping follows cultural conventions (e.g. Western left-to-right writing conveys linear ordering)
> - **Perceptual Analogy** - the input/output device looks like the actual thing it controls or monitors (e.g. Mercedes car seat controls)

> [!question]- Was ist ein Conceptual Model?
>
> Eine **High-Level-Beschreibung eines Produkts** - ein mentales Modell, das erlaubt, Effekte eigener Handlungen vorherzusagen und mit Problemen umzugehen; geformt durch Erfahrung, Übung, Instruktion. Gutes Conceptual Model: Operationen/Ergebnisse werden konsistent präsentiert, der Nutzer erhält ein kohärentes Bild des Systems.

> [!question]- Unterschied zwischen Visibility und Feedback.
>
> - **Visibility**: die relevanten Funktionen/Möglichkeiten und der aktuelle Zustand sind **sichtbar**, sodass der Nutzer sieht, was er tun kann (verringert den Gulf of Execution).
> - **Feedback**: das System gibt **Rückmeldung über das Ergebnis** einer Handlung, sodass der Nutzer erkennt, was passiert ist (verringert den Gulf of Evaluation). Visibility betrifft *vor* der Aktion, Feedback *nach* der Aktion.

## B - Metaphor

> [!question]- Die Arten von Metaphern mit Vor- und Nachteile nennen.
>
> - **Verb-based**: Bekannte Aktivität auf neue übertragen (cut & paste, drag & drop)
> - **Noun-based**: Eigenschaften eines neuen Objekts per Analogie erschließen (Ordner haben Erstelldatum & Besitzer)
> - **Noun+verb-based**: Aktivitäten und Objekt gemeinsam übertragen (Papierkorb: löschen + wiederherstellen)
>   
>   **Vorteile:**
>   - Vermitteln das konzeptuelle Modell → schnelleres Lernen
> 
> **Nachteile:**
> - Nutzer denken nur in der Metapher; Mehrdeutigkeit; falsche Erwartungen (Funktionen, die es nicht gibt); kulturell geprägt; Ease-of-learning vs. ease-of-use; Metaphors can hamper development of expertise
> - Designer übernehmen schlechte Altdesigns; eingeengter Problemraum; blockiert neue Paradigmen
> - Brüche: Papierkorb auf_dem Desktop; gleiche Geste, andere Bedeutung (Ordner = löschen, Laufwerk = auswerfen)

## C - Design Process

> [!question]- 1.4 Was ist Human Centered Design?
> Hier einfach Folien angucken, das ist soviel Kram
>make systems usable and useful by focusing on the users, their needs and requirements, and by applying human factors/ergonomics, and usability knowledge and techniques
>
>Bestandteile:
> - Iterative process with the human in the centre
> - Focus on empathy and understanding the user within the context
> - Human involvement in every step of the process (only conducting a user study is not HCD)
> - Highly interdisciplinary teams (computer science, psychology, social science, design …)

> [!question]- 1.4 Was sind die einzelnen Schritte im Human Centered Design?
> **Specify context of use:** User, Nutzung und Kontext verstehen mittels Observations/ Ethnography, Interviews (structured, semi-structured, unstructured), Focus groups
> **Specify user requirements** findings aus step 1 formalisieren mittels Requirements specification, Persona, Scenario
> **Design solutions** Create and iterate multiple prototypes mit hogh oder low fidelity prototypes
> **Evaluate against requirements** Collect data on how a real user is interacting with the system mit quantitativen (lab, fiel study oder umfrage) oder qualitative (grounded theory / thematic analysis)

> [!question]- 1.4 Kritik an Human Centered Design (Norman). Nenne je ein Beispiel für gute und weniger gute Eignung.
>
> Norman selbst ("Human-Centered Design Considered Harmful"): die starke Fokussierung auf **einzelne Nutzer und deren geäußerte Bedürfnisse** kann zu überladenen, inkohärenten Designs führen und den Blick auf die eigentliche **Aktivität** verstellen; Activity-Centered Design ist oft robuster.
> - **Gut geeignet**: gut verstandene Alltagsprodukte mit klaren, bekannten Nutzerbedürfnissen (z.B. Türklinke, Thermostat).
> - **Weniger geeignet**: komplexe Expert:innen-Werkzeuge oder echte Innovationen, bei denen Nutzer ihre Bedürfnisse (noch) nicht benennen können.

> [!question]- 2.1 Welche 2 Arten von Fehlern gibt es und was unterscheidet sie?
>
> - **Slips (Ausführungsfehler)**: die Absicht ist richtig, aber die Ausführung geht daneben (z.B. richtige Absicht, falscher Knopf) - meist bei Routine/automatisierten Handlungen.
> - **Mistakes (Planungsfehler)**: bereits die Absicht/das Ziel ist falsch (falsches mentales Modell), die Handlung wird dann "korrekt" zum falschen Ziel ausgeführt.

> [!question]- 2.2 Was ist Transparenz?
>
> Interne Änderungen der Implementierung versuchen das interface beizubehalten um den User nicht zu verwirren (schlechtes Beispiel FTP (eigneer CLient sieht anders aus), gutes Beispiel NFS (sieht im explorer einfach wie ein ordner aus))

> [!question]- 2.3 Was sind die 7 Stages of Action? Was sind die beiden Gulfs? Setze sie in Beziehung zu den 7 Stages.
>  **7 Stages**: Goal → Intention → Action Sequence → Execution → (Welt) → Perception → Interpretation → Comparison/Evaluation.
>  
>  - **Gulf of Execution**: bietet das System Aktionen passend zu den Absichten des Nutzers? Deckt die "absteigende" Hälfte ab (Goal → Intention → Action Sequence → Execution).
> - **Gulf of Evaluation**: bietet das System sichtbares, im Sinne der Absicht interpretierbares Feedback? Deckt die "aufsteigende" Hälfte ab (Perception → Interpretation → Comparison).
>  
> - **Goal**: The customer wants fresh pastries for breakfast the next morning. Error: They do not realize that all food must be collected on the same day.
> - **Intention**: The customer plans to order from the nearest bakery. Error: They assume the first bakery shown is the closest one.
> - **Action Sequence**: The customer wants to filter bakeries by distance. Error: They use the price filter instead because the icons are unclear.
> - **Execution**: The customer selects a pickup time. Error: They accidentally choose 17:00 instead of 19:00.
> - **Perception**: The customer looks for an order confirmation. Error: They miss it because it appears only briefly as a popup.
> - **Interpretation**: The customer reads “Reserved until 18:30.”Error: They mistake this for the pickup time instead of the collection deadline.
> - **Comparison**: The customer checks whether the goal was achieved. Error: They believe the platform failed because the surprise bag did not contain the exact pastries they expected, even though the order was fulfilled correctly.
>   
> **The Gulf of Execution** occurs when customers know what they want to do but struggle to figure out how to do it, for example because the pickup options are hard to find.
> **The Gulf of Evaluation** occurs when the system does not clearly communicate the order status and details, making it hard for customers to judge whether their goal was achieved.

> [!question]- 2.4 Was sind die 4 Bestandteile von User Centered Design? Nenne Ziel + je eine Methode und erkläre sie.
>
> Die 4 Aktivitäten des Interaction Design:
> 1. **Analyze I (Needs/Requirements)** - Ziel: Nutzer und Anforderungen verstehen. Methode: **Interviews/Ethnografie**.
> 2. **Design** - Ziel: Alternativen entwickeln. Methode: **Storyboards/Sketching**.
> 3. **Implement (Prototyping)** - Ziel: interaktive Versionen bauen. Methode: **Low-/High-Fidelity-Prototyp** (z.B. Paper Prototype).
> 4. **Analyze II (Evaluation)** - Ziel: Designs bewerten. Methode: **Usability Testing / heuristische Evaluation**.

> [!question]- 2.5 Was sind Horizontal und Vertical Prototypes?
>
> - **Horizontal Prototype**: bildet **viele Funktionen breit, aber flach** ab (Oberfläche/Navigation über den ganzen Funktionsumfang, ohne Tiefe) - gut, um Gesamtstruktur und Umfang zu prüfen.
> - **Vertical Prototype**: bildet **wenige Funktionen in voller Tiefe** ab (eine Funktion end-to-end lauffähig) - gut, um einen kritischen Ablauf realistisch zu testen.

> [!question]- 2.6 Unterschied "Getting the design right" vs. "Getting the right design"?
>
> - **Getting the right design**: das *richtige Konzept* finden - breit Alternativen erkunden und die passende Design-Idee auswählen (formativ, früh im Prozess).
> - **Getting the design right**: das *gewählte Design* korrekt ausarbeiten und verfeinern/polieren (summativ, später im Prozess).

> [!question]- High- und Low-Fidelity-Prototypen erklären, Beispiel, Vor-/Nachteile.
>
> - **Low Fidelity**: unähnliches Medium (Papier, Karton); schnell, billig, leicht änderbar, maximiert Iterationen vor dem Coden. Beispiel: Paper Prototype, Wizard of Oz. 
> - **+** billig/schnell, leicht änderbar, ermutigt Kritik (sieht unfertig aus).
> - **High Fidelity**: nah am finalen System, detailliert, interaktiv. Beispiel: klickbares Mock-up.
> - **+** realistisches Erleben, ohne Designer testbar, deckt Detail-/Interaktionsprobleme auf.
> - **−** wirkt "fertig" (Nutzer kritisieren weniger, Management hält es für fertig), Fokus auf Details statt großer Probleme.

> [!question]- Was ist ein Storyboard
>
> Ein **Storyboard** ist eine Sequenz von Skizzen, die einen Nutzungsablauf im Kontext zeigt (Nutzer, Aktion, Systemreaktion). Für den Automaten z.B.: (1) Nutzer tritt heran, (2) wählt Getränk, (3) wirft Geld ein / bezahlt, (4) Automat gibt Getränk + Wechselgeld aus, (5) Nutzer entnimmt.

> [!question]- Why is user involvement important?
>
> - **Functionality**: Entwickler verstehen die Ziele besser → passenderes, nutzbareres Produkt.
> - **Expectation Management**: realistische Nutzererwartungen, weniger Enttäuschung.
> - **Ownership**: beteiligte Nutzer akzeptieren/verzeihen Probleme eher.

## D - Evaluation  (muss noch machen)

> [!question]- 3.1 Ein nicht nennenswerter Einfluss der IV auf Fingerbeschwerden - kann daraus auf das Gegenteil geschlossen werden?
>
> **Nein.** Ein nicht signifikantes Ergebnis heißt nur, dass **kein Effekt nachgewiesen** wurde - "absence of evidence is not evidence of absence". Es könnte trotzdem ein Effekt existieren, der z.B. wegen zu kleiner Stichprobe, zu großer Streuung oder zu geringer Teststärke nicht entdeckt wurde. Die Nullhypothese wird nicht *bewiesen*, sondern nur *nicht verworfen*.

> [!question]- 3.2 Erkläre Within-Subject- und Between-Subject-Design. Nenne je einen Nachteil.
>
> - **Within-Subject**: jede:r Teilnehmer:in durchläuft **alle** Bedingungen. Nachteil: **Reihenfolge-/Lern-/Ermüdungseffekte** (carry-over), die per Counterbalancing ausgeglichen werden müssen.
> - **Between-Subject**: jede:r durchläuft **nur eine** Bedingung. Nachteil: **individuelle Unterschiede** zwischen den Gruppen, daher mehr Teilnehmer für gleiche Aussagekraft nötig.

> [!question]- 3.3 Unterschied zwischen Labor- und Feldstudie.
>
> - **Laborstudie**: kontrollierte Umgebung, hohe **interne Validität/Reliabilität**, Störvariablen minimiert - aber geringe **ökologische Validität** (unrealistisch).
> - **Feldstudie**: reale Umgebung, hohe ökologische Validität - aber wenig Kontrolle über Störvariablen, schlechter replizierbar.

> [!question]- 3.4 Sind mit einer Likert-Skala ermittelte Daten quantitativ oder qualitativ? Begründe.
>
> Likert-Daten sind **ordinal**: die Stufen sind geordnet (z.B. "stimme gar nicht zu" … "stimme voll zu"), aber die Abstände sind **nicht garantiert gleich**. Streng genommen also **qualitativ (kategorial-geordnet)**, auch wenn sie mit Zahlen kodiert und in der Praxis oft quantitativ ausgewertet werden.

> [!question]- 3.5 Keyboard-Layout-Studie: Ein Layout mit den häufigsten Tasten nebeneinander soll schnelleres Tippen und geringere Ermüdung ermöglichen. Überprüfe das.
>
> - **Unabhängige Variable**: Tastatur-Layout, z.B. Werte {QWERTZ, neues Layout, Dvorak}.
> - **Abhängige Variablen messen**: Tippgeschwindigkeit (Wörter/Anschläge pro Minute, Zeit), Fehlerrate; Fingerermüdung über subjektiven Fragebogen (z.B. Likert) oder physiologisch.
> - **Aufgabe**: einen vorgegebenen Standardtext abtippen (gleich für alle).
> - **Hypothesen**: (H1) Das neue Layout erhöht die Tippgeschwindigkeit ggü. QWERTZ. (H2) Das neue Layout reduziert die berichtete Fingerermüdung.
> - **Variablen**: Kontrollvariable = gleicher Text/gleiche Hardware; Zufallsvariable = Zuweisung der Teilnehmer zu Gruppen; Störvariable = Vorerfahrung/Tippkönnen der Teilnehmer.
> - **Design**: **Between-Subject**, um starke **Lerneffekte** zu vermeiden (wer QWERTZ kennt, ist beim ersten Layout im Vorteil); alternativ within mit Counterbalancing, aber Transfereffekte drohen.

> [!question]- Studie: abhängige/unabhängige/Störvariablen, Lerneffekt, konkretes Experiment, 200 Personen within/between?
>
> - **Unabhängige Variable**: vom Versuchsleiter variiert (z.B. Menüanzahl). **Abhängige Variable**: gemessen (Zeit, Fehler, Präferenz). **Störvariable**: unkontrollierter Einflussfaktor (Motivation).
> - **Lerneffekt**: Teilnehmer werden über die Bedingungen hinweg besser; Gegenmaßnahme: **Counterbalancing** (Reihenfolge ausbalancieren) oder Between-Subject-Design.
> - **200 Personen**: genug für **Between-Subject** (individuelle Unterschiede mitteln sich heraus, kein Lern-/Transfereffekt).

> [!question]- Klappspaten vs. Standardmodell (Hubkraft + Ergonomie per 9-Punkte-Skala): IVs (mit Werten), DVs (begründen). Bei 20 Teilnehmern within oder between?
>
> - **Unabhängige Variable**: Spatenmodell, Werte {Klappspaten, Standardmodell}.
> - **Abhängige Variablen**: **Hubkraft** (objektiv gemessen, quantitativ) und **Ergonomie** (subjektiv per 9-Punkte-Skala, ordinal) - beide messen die postulierte Überlegenheit.
> - **20 Teilnehmer** → **Within-Subject** (jede:r testet beide Spaten), weil die kleine Stichprobe sonst zu große individuelle Unterschiede zwischen zwei Gruppen hätte; Reihenfolge counterbalancen.

> [!question]- Was ist der Hawthorne-Effekt?
>
> Teilnehmer ändern ihr Verhalten allein deshalb, weil sie **wissen, dass sie beobachtet werden** - nicht wegen der eigentlichen Manipulation. Bedroht die Validität von Studien.

## E - Fittss Law

▪ ID = log2(1+D/W) = log2(1+8cm/6cm) = log2(2.34) = 1.22
▪ MT = a + b * ID = 0.5s + 0.5(s/bits) * 1.22bits = 1.11s

> [!question]- 4.1 Wie sollte ein häufig geklicktes UI-Element nach Fitts's Law platziert werden? Begründe.
>
> An den **Bildschirmrändern oder in den Ecken**. Nach $T = a + b\cdot\log_2(1 + (D/W))$ sinkt die Zeit mit größerer effektiver Zielbreite $W$: am Rand "stoppt" der Cursor an der Bildschirmkante, die Zielgröße wird also **effektiv unendlich** (man kann nicht drüber hinaus). Ecken sind am besten (in zwei Richtungen begrenzt). Alternativ nah an der aktuellen Cursorposition (kleines $D$).

> [!question]- 4.2 Ändert sich das bei Touch- statt Mausinput? Begründe.
>
> **Ja.** Beim Touch gibt es den "unendlichen Rand"-Vorteil nicht - der Finger wird nicht von der Bildschirmkante gestoppt, Ränder/Ecken sind sogar schlechter erreichbar (Rahmen, Griff). Zudem verdeckt der Finger das Ziel ("fat finger"), sodass eine **ausreichend große Zielfläche $W$** wichtiger wird als eine randnahe Platzierung.

> [!question]- Was ist Fitts's Law und Vor-/Nachteile
> The time required to rapidly move to a target area
> 
> ID (Index of Difficulty) = log2(1+(D/W))
> MT (Movement Time) = a + b * ID
> D = Distanz, W = Width of Target
> 
>**+** schnell, ohne Nutzer, gut für Vergleiche. 
>**−** nur für einfache Zeigebewegungen, ignoriert Fehler/Kognition.

## F - GOMS

> [!question]- Was ist GOMS und wo kann es eingesetzt werden? Nenne Vor- und Nachteile.
> (Goals (user goal), Operators (possible user actions), Methods (learned procedures to achiev a goal) und Selction Rules (decides which methods to use))
>
> Zur **modellbasierten Evaluation eines Interfaces ohne Nutzer** - sogar bevor das System gebaut ist. Für **Expertennutzer bei Routineaufgaben** mit vorhersehbarem Ablauf (nicht für kreative Aufgaben/Problemlösung). Muss das Userwissen modellieren.
> 
> **Vorteile**: günstig und schnell durchführbar; liefert Ergebnisse schon vor Systemfertigstellung; erleichtert vergleichende Evaluationen.
> **Nachteile**: nur bei vorhersehbaren Aufgaben sinnvoll (nicht für neue UI-Techniken); setzt fehlerfreies Expertenverhalten voraus (nicht für Gelegenheitsnutzer); Operatorzeiten nicht eindeutig definiert.

> [!question]- Methode + Operatoren gegeben: Reihenfolge, Beschreibung und Gesamtzeit angeben. (5 P)
>
> **Keystroke Level Model**: die Operatoren der Methode in Ausführungsreihenfolge auflisten, jedem seine gegebene Dauer zuordnen (z.B. K = Tastendruck, P = Pointing/Fitts, M = mentale Vorbereitung, H = Homing), kurz beschreiben und die Zeiten **aufsummieren** = vorhergesagte Ausführungszeit eines Experten. (Konkrete Zahl je nach gegebenen Werten.)

## G - Usability & Design-Prinzipien

> [!question]- Unterschied zwischen Usability und User Experience.
>
> - **Usability**: Ausmaß, in dem ein Produkt von bestimmten Nutzern genutzt werden kann, um bestimmte Ziele mit **Effectiveness, Efficiency und Satisfaction** in einem bestimmten Kontext zu erreichen.
> - **User Experience**: das gesamte **Erleben** der Interaktion - wie sich das Produkt anfühlt und wie es genutzt wird (befriedigend, ästhetisch, angenehm). UX umfasst *alle* Aspekte; Usability ist nur ein Teil davon. Man designt *für* eine Experience, nicht die UX selbst.

> [!question]- Usability Goals nennen und kurz erklären.
▪ Effectiveness
“Is the product capable of allowing users to perform tasks accurately and completely?”(doing “right” things, good quality results)
▪ Efficiency
“Once users have learned how to use a product to carry out their tasks, can they sustain a high level of productivity?” (doing things in the most economical way)
▪ Safety
“What is the range of errors that are possible using the product and what measures are there to permit users to recover easily?
▪ Utility
“Does the product provide an appropriate set of functions that will enable users to carry out all their tasks in the way they want to do them?”
▪ Learnability
“Is it possible for the user to work out how to use the product by exploring the interface and trying out certain actions?”
▪ Memorability
“What kinds of interface support have been provided to help users remember how to carry out tasks?”

> [!question]- 2 von 10 Golden Rules nennen und erklären - in welcher Design-Phase, Bezug zu gutem UI?
>
> Beispiele (Shneiderman): **"Strive for consistency"** (einheitliche Aktionen/Begriffe/Layouts - z.B. "Speichern" immer gleich platziert), **"Offer informative feedback"** (auf jede Aktion sichtbare Rückmeldung) und **"Prevent errors"** (Bedienung so gestalten, dass Fehler kaum möglich sind - z.B. ungültige Optionen ausgrauen). Einsatz v.a. in der **Design- und Evaluationsphase** (auch heuristische Evaluation). Bezug: Sie geben Orientierung und stellen sicher, dass die gravierendsten Usability-Probleme vermieden werden - notwendige, aber nicht hinreichende Bedingung für exzellentes UI.

