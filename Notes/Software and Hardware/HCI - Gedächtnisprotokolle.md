---
title: HCI - Gedächtnisprotokolle
aliases:
  - TK2 - Gedächtnisprotokolle
tags:
  - fb20
description: "Von Studierenden gesammelte Klausurfragen der HCI/TK2-Klausuren, gruppiert nach Semester, mit ausgearbeiteten Lösungen."
draft: false
---
## A - Cognition

> [!question]- 1.1 Wie viele Chunks passen ins Arbeitsgedächtnis? Wie kann man das auf Interaktionsdesign anwenden?
>
> **7 ± 2 Chunks** (Miller). Anwendung: Menüs, Auswahllisten, Navigationspunkte oder gleichzeitig sichtbare Optionen auf ~7 Elemente begrenzen; Information in sinnvolle Chunks gruppieren (z.B. Telefonnummern in Blöcke), damit sie ins Arbeitsgedächtnis passt.

> [!question]- 1.2 Was sagt die Extended Mind Theory aus? Nenne ein Beispiel.
>
> Technologie (z.B. das Smartphone) übernimmt und **ersetzt Teile des eigenen Verstandes/Gedächtnisses**. Statt Nummern und Wege zu erinnern, nutzen wir Funktionen des Geräts - das Denken erstreckt sich also über die Grenzen des Gehirns hinaus in die Umwelt. Das erhöht die Bedeutung guter Interfaces. Beispiel: Navigation per Karten-App statt sich Routen zu merken.

> [!question]- 1.3 Was beinhaltet Human Information Processing *nicht*? Nenne zwei Aspekte.
>
> Das Modell klammert **soziale**, **emotionale** und **motivationale** Faktoren des Nutzers aus - es behandelt den Menschen wie einen reinen Informationsverarbeiter (Eingabe → Verarbeitung → Ausgabe) ohne Gefühle, Motivation oder sozialen Kontext.

> [!question]- 1.4 Kritik an Human Centered Design (Norman). Nenne je ein Beispiel für gute und weniger gute Eignung.
>
> Norman selbst ("Human-Centered Design Considered Harmful"): die starke Fokussierung auf **einzelne Nutzer und deren geäußerte Bedürfnisse** kann zu überladenen, inkohärenten Designs führen und den Blick auf die eigentliche **Aktivität** verstellen; Activity-Centered Design ist oft robuster.
> - **Gut geeignet**: gut verstandene Alltagsprodukte mit klaren, bekannten Nutzerbedürfnissen (z.B. Türklinke, Thermostat).
> - **Weniger geeignet**: komplexe Expert:innen-Werkzeuge oder echte Innovationen, bei denen Nutzer ihre Bedürfnisse (noch) nicht benennen können.

> [!question]- 1.5 Erkläre die 2 Richtungen der Wahrnehmung (Bottom-Up und Top-Down) ausführlich am Beispiel des Bilds (die "13").
>
> - **Bottom-Up (data-driven)**: Wahrnehmung wird direkt aus dem Sinnesreiz aufgebaut - von einfachen Merkmalen (Kanten, Farben, Kontraste) hin zu komplexen Strukturen, ohne Vorwissen.
> - **Top-Down (knowledge-driven)**: Vorwissen, Erwartung und Kontext prägen die Interpretation; mehrdeutige/unvollständige Reize werden mit Erfahrung ergänzt.
> - **Beispiel "13"**: dasselbe mehrdeutige Zeichen wird als **B** oder als **13** gelesen, je nachdem ob es in der Reihe A-B-C (Buchstaben-Kontext) oder 12-13-14 (Zahlen-Kontext) steht - der Top-Down-Kontext entscheidet über die Deutung derselben Bottom-Up-Sinnesdaten.

> [!question]- 1.6 Was sagt Helmholtz's theory of unconscious inference aus? Zeichne ein Beispiel.
>
> Wahrnehmung ist das Ergebnis **unbewusster, automatischer Schlüsse**, die das Gehirn aus mehrdeutigen Sinnesdaten auf Basis von Erfahrung zieht - es landet bei der wahrscheinlichsten Interpretation der Welt. (Zugschienen mit zwei horizontalen)

> [!question]- 1.7 Was sind die Gestalt Laws.
>
>  Gestalt Principles are principles/laws of human perception that describe how humans group similar elements, recognize patterns and simplify complex images when we perceive objects.
> - Closure: The principle of closure states that when we look at a complex arrangement of visual elements, we tend to look for a single, recognizable pattern.
> - figure-ground: The figure-ground principle states that people instinctively perceive objects as either being in the foreground or the background. As a human, you can focus on either the foreground or the background
> - Common Fate: The law of common fate suggests that when multiple visual elements move in the same direction or at the same speed, we tend to perceive them as a cohesive unit or a single entity rather than individual components.
> - proximity: The principle of proximity states that things that are close together appear to be more related than things that are spaced farther apart.
> - similarity: The principle of similarity states that when things appear to be similar to each other, we group them together and we also tend to think they have the same function.
> - common-region: The principle of the common region is highly related to proximity. It states that when objects are located within the same closed region, we perceive them as being grouped together
> - continuity: The principle of continuity states that elements that are arranged on a line or curve are perceived to be more related than elements not on the line or curve.

> [!question]- 1.9 Was sind Affordances? Nenne zwei und erkläre sie (Bild: 2 Tassen + Teekanne).
>
> Affordances sind Eigenschaften eines Artefakts, die einen bestimmten Gebrauch **nahelegen** ("ist für"), oft in Physiologie/Körper verankert. Sind sie gut, braucht es keine Labels.
> 
> - Perceptible: Perceptible eigenschaften deuten auf nutzung hin (tür)
> - Hidden: keine obvious affordance und nutzer muss auf erfahrung und trial and error setzen (hover/click in dropdown menus)
> - False: objekt deutet auf nutzung hin, die es nicht gibt (unterstrichener text aber kein hyperlink)

> [!question]- 1.10 Gib ein Beispiel für eine False Affordance.
>
> Eine False Affordance legt eine Handlung nahe, die es nicht gibt oder die nicht funktioniert - z.B. eine **Türklinke, die zum Ziehen einlädt, obwohl gedrückt werden muss** ("Norman Door"), oder unterstrichener, farbiger Text, der wie ein Link aussieht, aber keiner ist.

> [!question]- 1.11 Was sind Constraints? Wie hängen sie mit Affordances zusammen?
>
> Constraints **schränken die möglichen Handlungen ein** - das "Inverse" von Affordances (und ergänzen sie oft). Ziele: Bedienfehler vermeiden, zu merkende Information minimieren. Arten:
> - **Physical** - Stecker passt nur in einer Ausrichtung.
> - **Logical** - logische Schlüsse schließen Lösungen aus (z.B. nur gültige Kalendertage wählbar).
> - (weitere: **Semantic** - Weltwissen; **Cultural** - Konventionen wie rot = Stopp.)
> - **Zusammenhang**: Affordances zeigen, was *getan werden kann*, Constraints beschränken, was *nicht getan werden kann* - zusammen engen sie den Möglichkeitsraum auf die intendierten Aktionen ein.

> [!question]- 1.12 Nenne die Dark Patterns.
>
> Nagging · Obstruction · Sneaking · Interface Interference · Forced Action
> - **Nagging** - redirection of expected functionality that persists across interactions (e.g. repeated pop-ups asking to enable notifications after being dismissed)
> - **Obstruction** - making a process more difficult than necessary to dissuade an action (e.g. burying "cancel subscription" behind multiple confirmation screens)
> - Sneaking - Attempting to hide, disguise, or delay the divulging of information that is relevant to the user (hide ads in reviews)
> - Interface Interference - Manipulation of the user interface that privileges certain actions over others (highlight buttons etc)
> - Forced Action - ?

> [!question]- Erkläre Affordance, markiere zwei Dinge im Bild. Wie stehen Constraints und Affordances zueinander? Reale vs. perceived Affordances?
>
> Affordance = nahegelegte Handlung. Im Bild z.B. **Knöpfe (drücken)** und **Dreh-Regler (drehen)** markieren.
> - **Real affordance**: physisch offensichtliche Handlung (Griff → greifen).
> - **Perceived affordance**: wahrgenommene/gelernte Möglichkeit (Screen-Button sieht drückbar aus).
> - **Beziehung**: Constraints sind das Inverse von Affordances - zusammen engen sie den Handlungsraum auf das Intendierte ein.

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

> [!question]- Nenne das im Bild (Fernbedienung) angewandte Gestalt Law + zwei weitere erklären.
>
> Im Fernbedienungs-Beispiel meist **Proximity** (räumlich nahe Tasten werden als Gruppe wahrgenommen). Zwei weitere:
> - **Similarity**: gleich aussehende Tasten (Form/Farbe) werden gruppiert.
> - **Common Region**: Tasten in einem gemeinsamen umrandeten Bereich gehören zusammen.

> [!question]- Zwei Gulfs nennen und kurz erklären.
>
> - **Gulf of Execution**: Lücke zwischen den Absichten des Nutzers und den vom System angebotenen Aktionen - kann ich meine Absicht direkt umsetzen?
> - **Gulf of Evaluation**: Lücke zwischen dem Systemzustand/Feedback und dessen Interpretation - erkenne ich, ob mein Ziel erreicht wurde?

> [!question]- Unterschied zwischen Visibility und Feedback.
>
> - **Visibility**: die relevanten Funktionen/Möglichkeiten und der aktuelle Zustand sind **sichtbar**, sodass der Nutzer sieht, was er tun kann (verringert den Gulf of Execution).
> - **Feedback**: das System gibt **Rückmeldung über das Ergebnis** einer Handlung, sodass der Nutzer erkennt, was passiert ist (verringert den Gulf of Evaluation). Visibility betrifft *vor* der Aktion, Feedback *nach* der Aktion.

> [!question]- External Cognition erklären und 3 Arten nennen, je ein Beispiel.
>
> **External Cognition** = kognitive Last in die Umwelt auslagern.
> - **Externalizing to reduce memory load**: Wissen nach außen verlagern (Geburtstage → Kalender, To-Dos → Post-its).
> - **Computational offloading**: externe Repräsentation reduziert Aufwand (Stift & Papier statt Kopfrechnen; arabische vs. römische Zahlen).
> - **Annotating & cognitive tracing**: Markieren/Abhaken (erledigte To-Do-Einträge abstreichen).

> [!question]- What is distributed Cognition? Name examples.
> Forms of reducing internal memory/computation load by using the external world:
> - **External memory** - navigating with a map or writing down notes.
> - **External Process** -  speed display in your car or calculator
## B - Metaphor

> [!question]- Drei Arten von Metaphern nennen und eine mit Beispiel erklären.
>
> **Verb-based**, **Noun-based**, **Noun+verb-based**.
> - **Verb-based**: bekannte/neue Aktivitäten teilen konzeptuelle Ähnlichkeit - z.B. *cut and paste*, *drag and drop*.
> - (Noun-based: Ordner mit Erstelldatum/Besitzer; Noun+verb-based: Papierkorb, in den man löscht und aus dem man wiederherstellt.)
## C - Design Process

> [!question]- 2.1 Welche 2 Arten von Fehlern gibt es und was unterscheidet sie?
>
> - **Slips (Ausführungsfehler)**: die Absicht ist richtig, aber die Ausführung geht daneben (z.B. richtige Absicht, falscher Knopf) - meist bei Routine/automatisierten Handlungen.
> - **Mistakes (Planungsfehler)**: bereits die Absicht/das Ziel ist falsch (falsches mentales Modell), die Handlung wird dann "korrekt" zum falschen Ziel ausgeführt.

> [!question]- 2.2 Was ist Transparenz?
>
> Interne Änderungen der Implementierung versuchen das interface beizubehalten um den User nicht zu verwirren (schlechtes Beispiel FTP (eigneer CLient sieht anders aus), gutes Beispiel NFS (sieht im explorer einfach wie ein ordner aus))

> [!question]- 2.3 Was sind die 7 Stages of Action? Zeichne den Graph. Was sind die beiden Gulfs? Setze sie in Beziehung zu den 7 Stages.
>
> **7 Stages**: Goal → Intention → Action Sequence → Execution → (Welt) → Perception → Interpretation → Comparison/Evaluation.
> - **Gulf of Execution**: bietet das System Aktionen passend zu den Absichten des Nutzers? Deckt die "absteigende" Hälfte ab (Goal → Intention → Action Sequence → Execution).
> - **Gulf of Evaluation**: bietet das System sichtbares, im Sinne der Absicht interpretierbares Feedback? Deckt die "aufsteigende" Hälfte ab (Perception → Interpretation → Comparison).
> Beide Gulfs sind die Lücken, die überbrückt werden müssen, damit Absicht und Systemreaktion zusammenpassen.

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
> - **Low Fidelity**: unähnliches Medium (Papier, Karton); schnell, billig, leicht änderbar, maximiert Iterationen vor dem Coden. Beispiel: Paper Prototype, Wizard of Oz. **+** billig/schnell, leicht änderbar, ermutigt Kritik (sieht unfertig aus).
> - **High Fidelity**: nah am finalen System, detailliert, interaktiv. Beispiel: klickbares Mock-up. **+** realistisches Erleben, ohne Designer testbar, deckt Detail-/Interaktionsprobleme auf. **−** wirkt "fertig" (Nutzer kritisieren weniger, Management hält es für fertig), Fokus auf Details statt großer Probleme.

> [!question]- Storyboard zu einem Getränkeautomaten (7 P).
>
> Ein **Storyboard** ist eine Sequenz von Skizzen, die einen Nutzungsablauf im Kontext zeigt (Nutzer, Aktion, Systemreaktion). Für den Automaten z.B.: (1) Nutzer tritt heran, (2) wählt Getränk, (3) wirft Geld ein / bezahlt, (4) Automat gibt Getränk + Wechselgeld aus, (5) Nutzer entnimmt. Bewertet wird das **Verständnis der Funktionsweise**, nicht die Zeichenkunst.

> [!question]- Why is user involvement important?
>
> - **Functionality**: Entwickler verstehen die Ziele besser → passenderes, nutzbareres Produkt.
> - **Expectation Management**: realistische Nutzererwartungen, weniger Enttäuschung.
> - **Ownership**: beteiligte Nutzer akzeptieren/verzeihen Probleme eher.

## D - Evaluation

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

> [!question]- 4.1 Wie sollte ein häufig geklicktes UI-Element nach Fitts's Law platziert werden? Begründe.
>
> An den **Bildschirmrändern oder in den Ecken**. Nach $T = a + b\cdot\log_2(2D/W)$ sinkt die Zeit mit größerer effektiver Zielbreite $W$: am Rand "stoppt" der Cursor an der Bildschirmkante, die Zielgröße wird also **effektiv unendlich** (man kann nicht drüber hinaus). Ecken sind am besten (in zwei Richtungen begrenzt). Alternativ nah an der aktuellen Cursorposition (kleines $D$).

> [!question]- 4.2 Ändert sich das bei Touch- statt Mausinput? Begründe.
>
> **Ja.** Beim Touch gibt es den "unendlichen Rand"-Vorteil nicht - der Finger wird nicht von der Bildschirmkante gestoppt, Ränder/Ecken sind sogar schlechter erreichbar (Rahmen, Griff). Zudem verdeckt der Finger das Ziel ("fat finger"), sodass eine **ausreichend große Zielfläche $W$** wichtiger wird als eine randnahe Platzierung.

> [!question]- Fitts's Law (Rechnung, Vor-/Nachteile, wann verwendet).
>
> $T = a + b\cdot\log_2(2D/W)$ - sagt die Zeigezeit aus **Distanz $D$** und **Zielbreite $W$** voraus. Verwendet zur **modellbasierten Vorhersage** von Zeigeaufgaben (Buttons, Menüs). **+** schnell, ohne Nutzer, gut für Vergleiche. **−** nur für einfache Zeigebewegungen, ignoriert Fehler/Kognition.

> [!question]- Fitts's Law: runder Button r = 1 cm, Distanz 16 cm. Berechne ID. Allgemein erklären. Welche Desktop-Orte sind leicht erreichbar und warum?
>
> $ID = \log_2(2D/W)$ mit $D = 16$ cm und $W = 2r = 2$ cm → $ID = \log_2(2\cdot16/2) = \log_2(16) = \mathbf{4\ bit}$.
> Fitts's Law: Zeigezeit wächst mit Distanz und sinkt mit Zielgröße. **Ränder und Ecken** sind sehr leicht erreichbar, weil der Cursor dort stoppt → effektiv **unendliche Zielbreite $W$** → kleiner Term $\log_2(2D/W)$.

## F - GOMS

> [!question]- Wo kann GOMS eingesetzt werden? (1 P)
>
> Zur **modellbasierten Evaluation eines Interfaces ohne Nutzer** - sogar bevor das System gebaut ist. Für **Expertennutzer bei Routineaufgaben** mit vorhersehbarem Ablauf (nicht für kreative Aufgaben/Problemlösung).

> [!question]- 2 Vorteile und 2 Nachteile von GOMS. (4 P)
>
> **Vorteile**: günstig und schnell durchführbar; liefert Ergebnisse schon vor Systemfertigstellung; erleichtert vergleichende Evaluationen.
> **Nachteile**: nur bei vorhersehbaren Aufgaben sinnvoll (nicht für neue UI-Techniken); setzt fehlerfreies Expertenverhalten voraus (nicht für Gelegenheitsnutzer); Operatorzeiten nicht eindeutig definiert.

> [!question]- Methode + Operatoren gegeben: Reihenfolge, Beschreibung und Gesamtzeit angeben. (5 P)
>
> **Keystroke Level Model**: die Operatoren der Methode in Ausführungsreihenfolge auflisten, jedem seine gegebene Dauer zuordnen (z.B. K = Tastendruck, P = Pointing/Fitts, M = mentale Vorbereitung, H = Homing), kurz beschreiben und die Zeiten **aufsummieren** = vorhergesagte Ausführungszeit eines Experten. (Konkrete Zahl je nach gegebenen Werten.)

## G - Interfaces

> [!question]- Was sind Tangible User Interfaces? Nenne Vor- und Nachteil. (3 P)
>
> **TUIs** verknüpfen digitale Information mit **physischen, greifbaren Objekten**, die man direkt manipuliert.
> - **Vorteil**: intuitive, direkte Manipulation; nutzt Körper/Motorik und reale Affordances.
> - **Nachteil**: eingeschränkte Flexibilität/Skalierbarkeit; physische Objekte sind teuer, statisch und schlecht rekonfigurierbar.

> [!question]- Was ist eine Multimodale UI? Nenne ein Beispiel. (2 P)
>
> Eine UI, die **mehrere Ein-/Ausgabemodalitäten** kombiniert (Sprache, Gestik, Touch, Blick, Haptik). Beispiel: Sprachassistent mit gleichzeitiger Touch-/Displaybedienung, oder AR-Brille mit Sprach- + Gesteneingabe.

> [!question]- Unterschied zwischen VR und AR. (1 P)
>
> **VR** ersetzt die reale Umgebung vollständig durch eine virtuelle. **AR** **ergänzt** die reale Umgebung um virtuelle Elemente (nach Azuma: kombiniert real + virtuell, interaktiv in Echtzeit, 3D-registriert).

> [!question]- 3 Aspekte von AR nach Azuma.
>
> AR (1) **kombiniert real und virtuell**, (2) ist **interaktiv in Echtzeit**, (3) ist **3D-registriert** (virtuelle Objekte räumlich korrekt in der Realwelt verankert).

> [!question]- Wofür steht REPL?
>
> **Read-Eval-Print Loop.**

## H - Datenvisualisierung

> [!question]- 4 Gemüse mit Werten zu 3 Zeitpunkten - welcher Datentyp? (1 P)
>
> **Quantitativ** (Mengen/Werte) über der Zeit, mit einer **kategorialen/nominalen** Dimension (die 4 Gemüsesorten) und einer geordneten Zeitachse - also quantitative Daten je Kategorie über einen (diskreten) Zeitverlauf.

> [!question]- Daten visualisieren, Diagrammtyp benennen und begründen. (4 P)
>
> **Grouped/Multiple Bar Chart** oder - wenn der zeitliche Trend betont werden soll - **Line Chart** (eine Linie je Gemüsesorte). Begründung: Balken eignen sich zum **Vergleich diskreter Werte** über Kategorien/Zeitpunkte; Linien zeigen **Trends** über die Zeit. Kein Pie Chart (die Werte summieren sich nicht sinnvoll zu 100 %). Weitere Diagrammtypen zur Einordnung: **Scatter Plot** für Zusammenhänge zweier quantitativer Variablen, **Pie Chart** nur für Anteile, die zu 100 % summieren.

## I - Usability & Design-Prinzipien

> [!question]- Unterschied zwischen Usability und User Experience.
>
> - **Usability**: Ausmaß, in dem ein Produkt von bestimmten Nutzern genutzt werden kann, um bestimmte Ziele mit **Effectiveness, Efficiency und Satisfaction** in einem bestimmten Kontext zu erreichen.
> - **User Experience**: das gesamte **Erleben** der Interaktion - wie sich das Produkt anfühlt und wie es genutzt wird (befriedigend, ästhetisch, angenehm). UX umfasst *alle* Aspekte; Usability ist nur ein Teil davon. Man designt *für* eine Experience, nicht die UX selbst.

> [!question]- 4 von 6 Usability Goals nennen und kurz erklären.
>
> - **Effectiveness** - akkurate, vollständige Aufgabenerfüllung möglich?
> - **Efficiency** - hohe Produktivität nach dem Erlernen haltbar?
> - **Safety** - Fehlerspektrum begrenzt, Erholung leicht?
> - **Learnability** - lässt sich die Bedienung durch Ausprobieren erschließen?
> - (weitere: **Utility** - passende Funktionen vorhanden? **Memorability** - erinnert man sich an die Bedienung?)

> [!question]- 2 von 10 Golden Rules nennen und erklären - in welcher Design-Phase, Bezug zu gutem UI?
>
> Beispiele (Shneiderman): **"Strive for consistency"** (einheitliche Aktionen/Begriffe/Layouts - z.B. "Speichern" immer gleich platziert), **"Offer informative feedback"** (auf jede Aktion sichtbare Rückmeldung) und **"Prevent errors"** (Bedienung so gestalten, dass Fehler kaum möglich sind - z.B. ungültige Optionen ausgrauen). Einsatz v.a. in der **Design- und Evaluationsphase** (auch heuristische Evaluation). Bezug: Sie geben Orientierung und stellen sicher, dass die gravierendsten Usability-Probleme vermieden werden - notwendige, aber nicht hinreichende Bedingung für exzellentes UI.

