---
name: kreuzverhoer
description: "Nimmt eine Entscheidung mit echtem Zielkonflikt ins Kreuzverhör: fünf Berater, anonyme Gegenprüfung, Faktencheck, klares Urteil. Trigger: Kreuzverhör, /kreuzverhör, auf den Prüfstand, durch die Mangel drehen."
---

# Kreuzverhör

Dieser Skill prüft eine Entscheidung, bevor sie fällt. Statt einer einzelnen Einschätzung entstehen fünf Antworten aus fest verteilten Blickwinkeln. Sie werden anonym gegeneinander bewertet, ihre tragenden Behauptungen werden gegen Quellen geprüft, und ein Vorsitz fasst alles zu einem Urteil zusammen, das seine Annahmen offenlegt.

Entstanden ist der Skill bei der Prüfung eines Businessplans für eine Gründung. Eine erste KI-Einschätzung klang überzeugend und lag an zwei entscheidenden Stellen falsch, weil dieselbe unbelegte Annahme mehrfach wiederholt worden war. Deshalb zählen hier Belege mehr als Einigkeit.

Methodische Grundlage ist Andrej Karpathys LLM Council: mehrere Modelle beantworten dieselbe Frage, bewerten die anonymisierten Antworten gegenseitig in einer Rangliste, und ein Vorsitz führt sie zusammen.

Alle Ausgaben an den Nutzer sind auf Deutsch.

**Zu dieser Fassung:** Sie ist für Umgebungen ohne Sub-Agenten gedacht, etwa ChatGPT. Ein Modell übernimmt alle Rollen nacheinander. Die Berater sind dadurch weniger unabhängig als bei getrennten Agenten. Die Arbeitsregeln (Belegpflicht, Anonymisierung, Faktencheck) gleichen das so weit wie möglich aus. Wenn verfügbar, ein Thinking- oder Reasoning-Modell und die Websuche nutzen.

---

## Einsatzbereich

Ein Kreuzverhör ist aufwendig. Es lohnt sich, wenn eine falsche Entscheidung teuer wäre und mehr als eine Antwort vertretbar ist.

Passende Anlässe:

- „Trägt mein Businessplan, und wo würde ein Prüfer ansetzen?“
- „Soll ich meine Leistung als Monatspauschale oder als Projektpreis anbieten?“
- „Den Shop jetzt auf ein neues System umziehen oder erst nach dem Weihnachtsgeschäft?“
- „Welche von zwei Positionierungen für die Startseite trägt weiter?“
- „Lohnt sich ein eigener Messestand, oder reicht der Besuch?“

Nicht passend, direkt beantworten oder erledigen:

- Fragen mit einer feststellbaren richtigen Antwort („Welcher Umsatzsteuersatz gilt für Beratungsleistungen?“)
- Aufträge zum Erstellen von Inhalten („Formuliere eine Absage an den Bewerber“)
- reine Verarbeitung („Übersetze dieses Dokument ins Englische“)

Das Verhör ist darauf ausgelegt, Schwachstellen zu finden. Ein ausgewogenes Urteil entsteht trotzdem, weil der Chancensucher und der Vorsitz Gegengewicht geben. Wer erkennbar Zustimmung erwartet, bekommt dennoch eine ehrliche Bewertung.

---

## Die fünf Berater

Jede Rolle ist eine Arbeitsweise, keine Figur.

### 1. Der Advocatus Diaboli

Liest die Vorlage wie ein Prüfer, der einen Grund zur Ablehnung sucht. Er rechnet nach, stellt Aussagen nebeneinander und benennt Widersprüche, Lücken und Risiken. Findet er nichts Gravierendes, prüft er die Annahmen, die als selbstverständlich gelten.

### 2. Der Grundsatzdenker

Prüft zuerst die Frage selbst. Was soll am Ende erreicht werden, und führt die gestellte Frage dorthin? Er trennt Ziel und Mittel, legt unausgesprochene Voraussetzungen offen und schlägt eine andere Fragestellung vor, wenn die ursprüngliche zu eng gefasst ist.

### 3. Der Chancensucher

Fragt, was im Vorhaben steckt, wenn es gut läuft: ungenutzte Hebel, angrenzende Märkte, Spielraum bei Preis und Paketen, Wege, aus einer Einzelleistung etwas Wiederholbares zu machen. Risiken überlässt er den anderen.

### 4. Der Außenstehende

Kennt weder die Branche noch die Vorgeschichte und verwendet bewusst kein Fachwissen. Er markiert Fachbegriffe ohne Erklärung, Zahlen ohne Einordnung und Schritte, die nur für Eingeweihte logisch sind.

### 5. Der Macher

Denkt in Arbeitsschritten: Was ist zuerst zu tun, wer macht es, bis wann und mit welchen Mitteln? Pläne ohne erkennbaren Anfang oder mit unrealistischen Fristen benennt er klar.

**Warum diese Besetzung:** Advocatus Diaboli und Chancensucher bewerten aus entgegengesetzten Richtungen, Risiko und Potenzial. Grundsatzdenker und Macher setzen an den beiden Enden an, bei der Frage und bei der Umsetzung. Der Außenstehende prüft die Verständlichkeit ohne Insiderwissen.

---

## Ablauf

### Schritt 1: Kontext, Rückfragen, Fragestellung

**A. Kontext lesen.** Angehängte oder genannte Dateien vollständig lesen. Gespeicherte Informationen zum Nutzer nur einbeziehen, wenn sie für die Frage eine Rolle spielen.

**B. Kippende Fakten erfragen.** Hängt das Urteil an einem Fakt, den nur der Nutzer kennt (Vertragslage, Zusagen von Kunden, Absprachen mit Behörden), höchstens drei Fragen gebündelt stellen und auf die Antwort warten. Nicht den ungünstigsten Fall unterstellen.

Ist der Gegenstand insgesamt unklar, eine einzige Rückfrage dazu stellen.

**C. Fragestellung schreiben.** Eine Fassung, auf die sich alle Berater beziehen:

1. die zu treffende Entscheidung
2. die Fakten aus Unterlagen und Antworten des Nutzers, jeweils mit Herkunft („laut Plan S. 12“, „laut Nutzer“)
3. ausdrücklich markierte Unbekannte
4. was auf dem Spiel steht

Keine eigene Analyse in die Fragestellung. Selbstaussagen des Nutzers über Markt oder Preise als Selbstaussage kennzeichnen. Die Fragestellung dem Nutzer kurz zeigen (drei bis acht Zeilen) und dann weitermachen.

### Schritt 2: Das Verhör (fünf Berater nacheinander)

Jeden Berater in einem eigenen, klar abgegrenzten Abschnitt schreiben. Für die Unabhängigkeit:

- Jeder Berater stützt sich nur auf Fragestellung und Unterlagen. Er nimmt nie Bezug auf einen anderen Berater, weder zustimmend noch widersprechend.
- Vor jedem Berater die Rolle neu ansetzen, als wären die vorigen Abschnitte nicht geschrieben.
- Ganz in der Rolle bleiben, nicht abwägen.
- 150 bis 300 Wörter je Berater.

**Belegpflicht:** Jede Zahl, Marktangabe und Rechtsbehauptung kennzeichnen:
- [U] steht so in den Unterlagen oder der Fragestellung
- [R] nachgerechnet
- [Q] mit Quelle belegt (Quelle nennen)
- [A] Annahme oder Einschätzung

Rechtsfolgen nur als sicher darstellen, wenn sie belegt sind. Was als unbekannt markiert ist, gilt als unbekannt, nicht als Fehler.

Die Berater-Antworten dem Nutzer nur auf Wunsch vollständig zeigen.

### Schritt 3: Die Gegenprüfung (anonym)

Die fünf Antworten in zufälliger Reihenfolge den Buchstaben A bis E zuordnen, nicht in der Reihenfolge, in der sie entstanden sind. Dann als unbeteiligter Prüfer, der die Rollen nicht kennt, vier Fragen beantworten:

1. Welche Antwort trägt am meisten zur Entscheidung bei, und warum?
2. Welcher Antwort fehlt am meisten, und was genau?
3. Welche Aussagen sind falsch oder unbelegt? Besonders [A]-Angaben und Widersprüche zu den Unterlagen prüfen, und erst in den Unterlagen nachsehen, bevor dort etwas als fehlend gilt.
4. Gibt es einen Punkt, den keine Antwort behandelt? Nur nennen, wenn er das Ergebnis ändern kann, eingeordnet als „wesentlich“ oder „Randrisiko“. „Nichts Wesentliches“ ist eine gültige Antwort.

Danach bewerten:

5. **Rangliste** aller fünf Antworten von Platz 1 (trägt am meisten) bis Platz 5, jeder Platz genau einmal.
6. **Sterne für die Belastbarkeit** je Antwort: 5 = schlüssig und belegt, 4 = überwiegend belegt, 3 = plausibel mit wichtigen unbelegten Annahmen, 2 = deutliche Lücken oder Fehler, 1 = nicht tragfähig.

Weil hier ein einziges Modell prüft, die Bewertung aus drei unterschiedlich strengen Prüfersichten wiederholen: streng, neutral, wohlwollend. So entstehen je Antwort drei Platzierungen und drei Sternwertungen.

Höchstens 250 Wörter für die Fragen 1 bis 4. Gleichlautende Behauptungen mehrerer Berater sind kein Beleg, sondern ein Prüfauftrag.

**Wertung berechnen:** Buchstaben wieder den Beratern zuordnen. Je Berater Ø Rang (1 = trägt am meisten) und Ø Sterne bilden, jeweils eine Nachkommastelle, mit einem Code-Werkzeug, wenn verfügbar. Sterne auf halbe Sterne runden und mit ★ (voll), ⯪ (halb) und ☆ (leer) auf fünf Stellen auffüllen, dahinter der genaue Wert, zum Beispiel ★★★⯪☆ 3,6. Sortierung nach Ø Rang, bei Gleichstand nach Sternen.

Rang und Sterne getrennt lesen: Der Rang zeigt, welche Sicht vorn liegt, die Sterne zeigen, ob sie trägt.

### Schritt 4: Der Faktencheck

Die drei bis sechs Behauptungen auswählen, auf denen das Urteil ruhen würde: Marktzahlen, Rechtsfolgen, Rechenergebnisse und alles, was mehrere Berater gleich behaupten. Mit Websuche prüfen, falls verfügbar, und Zahlen nachrechnen.

Je Behauptung festhalten:
- Ergebnis: bestätigt / teilweise richtig / falsch / nicht prüfbar
- Begründung in ein bis zwei Sätzen
- Quelle mit Link und Datum, oder Rechenweg
- Bedeutung für diesen Fall: hoch / gering

Ohne Websuche Angaben zu aktuellen Marktdaten oder zur Rechtslage als „nicht geprüft“ markieren. Rechtliche und steuerliche Punkte sind allgemeine Information, im Urteil kurz auf Fachberatung verweisen.

### Schritt 5: Das Urteil

In der Rolle des Vorsitzes alles zusammenführen:

- Vom Faktencheck widerlegte Aussagen sind keine Argumente mehr, höchstens korrigierte Annahmen.
- Belege wiegen schwerer als Häufigkeit.
- Randrisiken als Randrisiken kennzeichnen.
- Der besser belegten Position folgen, auch gegen die Mehrheit.
- Die Wertung ist ein Hinweis. Widerlegt der Faktencheck eine hoch bewertete Antwort, gilt der Faktencheck.
- Bewusst getroffene und begründete Entscheidungen des Nutzers respektieren, Abweichungen als Option kennzeichnen.
- Festlegen: Eine Empfehlung mit Bedingungen ist zulässig, eine ohne Richtung nicht.

### Schritt 6: Ausgabe im Chat

```
## Urteil im Kreuzverhör: {Thema in wenigen Worten}

### Wertung der Gegenprüfung

| Platz | Berater | Ø Rang | Belastbarkeit |
|:---:|---|:---:|---|
| 1 | {Berater} | {x,x} | {★★★★⯪ x,x} |
| … | … | … | … |

*Ø Rang: 1 = trägt am meisten. Belastbarkeit: 5 Sterne = schlüssig und belegt, 1 Stern = nicht tragfähig.*

{ein bis zwei Sätze Einordnung}

### Wo Einigkeit herrscht
{Punkte, zu denen mehrere Berater gelangt sind und die belegt oder plausibel sind}

### Wo gestritten wird
{echte Meinungsverschiedenheiten mit beiden Positionen und dem Grund}

### Blinde Flecken, die das Verhör aufgedeckt hat
{nur wesentliche Punkte aus Gegenprüfung und Faktencheck}

### Tragende Annahmen
{zwei bis vier Annahmen mit Status belegt / Aussage des Nutzers / ungeprüft, und was sich ändert, wenn eine nicht zutrifft}

### Die Empfehlung
{klar und begründet}

### Der erste Schritt
{genau ein konkreter Schritt}
```

Aufzählungen nutzen, Absätze kurz halten. Sterne immer mit Zahl dahinter zeigen. Quellen aus dem Faktencheck am Ende als verlinkte Liste.

**Korrigiert der Nutzer danach einen Punkt**, das Urteil nicht verteidigen. Sagen, welche Teile entfallen oder sich ändern, und neu einordnen.

---

## Arbeitsregeln

- **Fakten erfragen statt unterstellen.**
- **Fragestellung ohne Wertung.**
- **Berater strikt getrennt halten.** Kein Berater bezieht sich auf einen anderen.
- **Für die Gegenprüfung anonymisieren und mischen.**
- **Rang und Sterne getrennt lesen.**
- **Gleichklang prüfen.** Was mehrere Berater gleich behaupten, kommt in den Faktencheck.
- **Belege vor Mehrheit.**
- **Einfache Fragen direkt beantworten.**
- **Das Urteil muss allein stehen** und seine Annahmen offen zeigen.
- **Ehrlich bleiben,** auch wenn erkennbar Zustimmung erwartet wird.

---

Methode nach Andrej Karpathys LLM Council. Die Grundidee fester Denkrollen geht auf den LLM-Council-Skill von Ole Lehmann zurück. Texte, Ablauf und Erweiterungen dieser Fassung sind eigenständig formuliert. Bereitgestellt von conexio.de unter MIT-Lizenz.
