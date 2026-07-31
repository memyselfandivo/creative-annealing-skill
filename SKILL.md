---
name: creative-annealing
description: Generiert kreative Ideen zu einem Thema/Problem über einen strukturierten "Simulated Annealing"-Prozess — breite, unbewertete Exploration zuerst, dann mehrere Eliminationsrunden bis auf genau 3 finale Ideen, mit nachvollziehbarer Begründung in jeder Runde. Nutze diesen Skill IMMER, wenn der User "creative-annealing" erwähnt oder explizit sagt — egal ob mit oder ohne weitere Details (Thema, Startanzahl). Auch bei nur teilweisen Angaben (nur Thema, nur Anzahl, oder gar nichts außer dem Trigger-Wort) triggert dieser Skill — er übernimmt die fehlenden Angaben selbst über gezielte Rückfragen. Nicht triggern bei allgemeinen Kreativitäts- oder Brainstorming-Anfragen ohne den expliziten Trigger-Begriff.
---

# Creative Annealing

Ein mehrstufiger Ideenfindungsprozess nach dem Vorbild von Simulated Annealing: viele unkonventionelle Ideen generieren (hohe "Temperatur"), dann schrittweise selektieren und verfeinern (Abkühlung), bis am Ende genau 3 belastbare Ideen übrig bleiben. Der Wert liegt nicht nur im Ergebnis, sondern in der Nachvollziehbarkeit — der User soll im Nachhinein sehen können, welcher Ansatz aus der Exploration wo rausgeflogen ist und warum, um ggf. Ansätze händisch zu kombinieren.

Die zentrale Charakteristik des Originalverfahrens ist dabei nicht "viele kreative Ideen", sondern dass die Exploration bewusst auch **gegen die Intuition** und **quer zum Ziel** sucht, nicht nur variantenreich in Richtung Ziel. Erst durch diesen bewussten Umweg entstehen in den Folgerunden Ideen, die auf einem unerwarteten Pfad zum Ziel führen. Schritt 2 bildet das über vier Suchrichtungen ab, nicht nur eine.

## Trigger-Erkennung

Sobald der Trigger "creative-annealing" im Prompt vorkommt, unterscheide zwei Varianten:

**Variante A — vollständige Angabe.** Der Prompt enthält zusätzlich zum Trigger sowohl (1) eine Beschreibung der Idee/des Themas als auch (2) eine Startanzahl an Ideen für die Explorationsrunde.
→ Intake-Fragen überspringen, direkt weiter mit Schritt 1 (Klärung).

**Variante B — nackter Trigger.** Der Prompt enthält nur den Trigger, ohne Beschreibung und/oder ohne Startanzahl.
→ Fehlende Angaben einzeln nacheinander erfragen (nicht beide Fragen in einer Nachricht bündeln):
1. "Um welche Idee/welches Problem geht es?"
2. "Mit wie vielen Ideen soll die Explorationsrunde starten?"

Bei der zweiten Frage, falls der User unsicher ist oder nach einer Empfehlung fragt: empfiehl **7** als sinnvolles Minimum (Begründung siehe unten). Danach weiter mit Schritt 1.

Ist nur eine der beiden Angaben vorhanden (z. B. Thema ja, Anzahl nein), nur die fehlende einzeln nachfragen.

## Warum 7 das empfohlene Minimum ist

Reduktionsregel (siehe Schritt 3): mindestens 2 Ideen weniger pro Runde. Bei einer Startanzahl von 5 oder 6 springt die erste Reduktionsrunde bereits direkt auf 3 — es gibt keine echte Zwischenrunde, nur Exploration + Finalrunde. Das funktioniert technisch, unterläuft aber den Sinn des mehrstufigen Abkühlens. Ab 7 Start-Ideen ist mindestens eine echte Zwischenrunde garantiert. Größere Startanzahlen (10, 15, 20...) erzeugen entsprechend mehr Zwischenrunden und mehr Explorationsbreite — sinnvoll bei komplexeren oder unklareren Problemen.

## Schritt 1: Klärung

Bevor die Explorationsrunde beginnt, kurz klären, was für die Ideenfindung relevant ist — aber nur was wirklich unklar ist, nicht pauschal alles abfragen:
- Um welches Problem/Thema geht es konkret?
- Gibt es Rahmenbedingungen, Zielgruppe, Constraints, einen Einsatzkontext?

Zusätzlich für Schritt 2 selbst festlegen (in der Regel keine Rückfrage an den User nötig, nur bei echter Unklarheit):
- **Zielrichtung**: was ist die naheliegende, "übliche" Richtung, in die eine Lösung zielt?
- **Gegenrichtung**: was wäre das plausible Gegenteil dieser Zielrichtung?

Nicht jedes Ziel hat eine sauber definierbare Gegenrichtung — bei abstrakteren Zielen wirkt sie zwangsläufig etwas konstruiert. Das ist eine bewusst in Kauf genommene Eigenschaft dieses Verfahrens, kein Fehler, der behoben werden muss. Im Zweifel eine plausible, nachvollziehbare Gegenrichtung wählen und weitermachen, statt lange danach zu suchen.

Wenn die ursprüngliche Beschreibung das schon abdeckt, diesen Schritt kurz halten oder überspringen.

## Schritt 2: Explorationsrunde (hohe Temperatur)

Generiere genau N Ideen (N = Startanzahl). Keine Bewertung, keine Vorauswahl, keine Selbstzensur — auch schwache, extreme oder auf den ersten Blick unpraktische Ideen gehören rein.

Verteile die N Ideen bewusst auf **drei Suchrichtungen** relativ zur Zielrichtung, statt sie alle nur variantenreich Richtung Ziel zu denken:

- **Gegenrichtung (~25%)**: Ideen, die explizit GEGEN das Ziel arbeiten oder dessen Gegenteil verfolgen (siehe Zielrichtung/Gegenrichtung aus Schritt 1). Beispiel Ziel "mehr junge Kunden gewinnen": Ideen, die explizit ältere Zielgruppen bedienen oder aktiv keine neuen Kunden anziehen.
- **Kreativ-quer (~50%)**: breit gestreute, sehr kreative Ideen abseits des direkten Zielpfads — weder klar Richtung Ziel noch klar dagegen. Intern selbst auf Streuung achten: ein Teil davon darf im selben Themenfeld wie das Ziel extrem/radikal sein, ein anderer Teil ruhig aus einem komplett anderen Themenfeld kommen. Diese Streuung muss nicht als eigene Unterkategorie ausgewiesen werden, nur die Ideen selbst sollen sich spürbar unterscheiden.
- **Zielrichtung (~25%)**: übliche kreative Ideen, die erkennbar auf das Ziel hinarbeiten. Das ist die einzige Richtung, die ein klassisches Brainstorming ohnehin abdecken würde.

Prozentsätze sind Richtwerte, müssen bei N nicht exakt aufgehen. Diese Verteilung ist der eigentliche Zweck der Explorationsrunde. Eine Runde, in der praktisch alle Ideen aus der Zielrichtung stammen (nur zunehmend kreativer variiert), hat die Kernidee des Verfahrens verfehlt — genau das ist der Fehler, der vermieden werden soll.

Für JEDE Idee dieser Runde angeben:
- **Idee**: kurz und prägnant
- **Richtung**: eine der drei Suchrichtungen (Gegenrichtung / Kreativ-quer / Zielrichtung)
- **Ansatz**: 1 Satz zur grundsätzlichen Denkrichtung/Strategie dahinter (z. B. "Umkehrung der Nutzererwartung", "Kombination zweier fremder Branchen", "radikale Vereinfachung", "Analogie aus der Natur"). Das ist der Anker, an dem der User später einen verworfenen Ansatz wiedererkennen kann.

## Schritt 3: Rundenplan berechnen

Berechne den kompletten Rundenplan EINMAL nach der Explorationsrunde und zeige ihn dem User kurz und transparent (z. B. als eine Zeile: "Rundenplan: 12 → 8 → 5 → 3"), bevor die erste Zwischenrunde beginnt.

Formel:
```
R (Reduktion pro Runde) = clamp( round(0.30 × N), 2, floor(0.50 × N) )
```
- N = Startanzahl (aus Schritt 2, bleibt für die ganze Formel fix)
- Untergrenze: mindestens 2 Ideen weniger pro Runde
- Obergrenze: nie mehr als 50% der Start-Ideen (bezogen auf N, nicht auf die aktuell verbleibende Anzahl)
- Optimalwert: 30% von N, gerundet

Ablauf:
```
remaining = N
solange remaining > 3:
    next = remaining - R
    wenn next <= 3: next = 3   // Finalrunde erzwingt IMMER genau 3,
                                 // unabhängig davon, was R ergäbe
    remaining = next
```

Die Finalrunde ist also ein Sonderfall: sie landet immer exakt bei 3, auch wenn die reguläre Reduktion R eigentlich weniger oder mehr Abzug bedeuten würde.

Beispiele zur Orientierung:
- N=7: R=2 → 7 → 5 → 3 (1 Zwischenrunde + Finalrunde)
- N=10: R=3 → 10 → 7 → 4 → 3 (2 Zwischenrunden + Finalrunde)
- N=20: R=6 → 20 → 14 → 8 → 3 (2 Zwischenrunden + Finalrunde, letzter Sprung größer als R, das ist gewollt)

## Schritt 4: Zwischenrunden (Abkühlung)

Diese Runden sind KEINE reinen Filterrunden — das gilt besonders für Ideen aus Gegenrichtung und Kreativ-quer. Statt sie einfach zu verwerfen, sollen sie aktiv weiterentwickelt/gedreht werden, sodass sie sich schrittweise dem Ziel annähern. Der eigentliche kreative Ertrag entsteht genau hier: eine Idee, die in der Exploration bewusst gegen das Ziel lief, wird über 1-2 Zwischenrunden so transformiert, dass sie am Ende auf einem unerwarteten Weg zum Ziel beiträgt — nicht trotz, sondern wegen ihres ungewöhnlichen Ausgangspunkts.

Beispiel: eine Gegenrichtungs-Idee ("Laden bewusst für ältere, traditionelle Buchleser gestalten") kann in der nächsten Runde zu einer zieldienlichen Idee gedreht werden ("aus verstaubt-traditionell wird eine quirky, cozy Countryside-Ästhetik, die gerade bei jungen Leuten als kultig gilt") — statt einfach gestrichen zu werden, weil sie auf den ersten Blick nicht zum Ziel passt.

Aus den Ideen der Vorrunde die gemäß Rundenplan verbleibende Anzahl auswählen. Ideen dürfen dabei weiterentwickelt, gedreht oder zu einer neuen Idee verschmolzen werden.

Für JEDE überlebende Idee angeben:
- **Idee**: aktueller Stand (kann gegenüber der Vorrunde verfeinert, gedreht oder verändert sein)
- **Richtung**: ursprüngliche Richtung aus Schritt 2 beibehalten, auch wenn die Idee inzwischen näher am Ziel liegt — so bleibt sichtbar, aus welcher Ecke der Exploration eine Idee stammt
- **Begründung**: warum sie diese Runde überlebt hat, im Vergleich zu den in dieser Runde ausgeschiedenen Ideen — bei einer Drehung/Transformation kurz erklären, wie sie sich dem Ziel angenähert hat

Nicht explizit auflisten, welche Ideen ausgeschieden sind — die stehen bereits in der Vorrunde und bleiben dort nachlesbar. Der User kann jederzeit auf eine frühere Runde zurückgreifen und fragen "was ist mit Ansatz X passiert" oder "kombiniere X mit Y".

## Schritt 5: Finalrunde

Exakt 3 Ideen, im gleichen Format wie die Zwischenrunden (Idee + Begründung), aber deutlich als Abschluss gekennzeichnet — hier idealerweise etwas ausführlicher begründet, da dies die Endauswahl ist.

## Output-Format

Gliedere die Antwort klar nach Runden, damit der User jederzeit auf eine bestimmte Runde/Idee zurückverweisen kann:

```
## Rundenplan: N → ... → 3

## Runde 1: Exploration (N Ideen)
1. **[Idee]** — Richtung: [Gegenrichtung/Kreativ-quer/Zielrichtung] — Ansatz: [...]
2. ...

## Runde 2: Zwischenrunde ([Anzahl] Ideen)
1. **[Idee]** — Richtung: [ursprüngliche Richtung] — Begründung: [...]
2. ...

[weitere Zwischenrunden falls vorhanden]

## Finalrunde (3 Ideen)
1. **[Idee]** — Richtung: [ursprüngliche Richtung] — Begründung: [...]
2. ...
3. ...
```

Nach der Finalrunde kurz anbieten, dass der User einzelne Ideen aus früheren Runden nachträglich kombinieren oder wiederbeleben kann.
