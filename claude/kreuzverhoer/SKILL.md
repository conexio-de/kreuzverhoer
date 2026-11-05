---
name: kreuzverhoer
description: "Nimmt eine Entscheidung mit echtem Zielkonflikt ins Kreuzverhör: fünf Berater, anonyme Gegenprüfung, Faktencheck, klares Urteil. Trigger: Kreuzverhör, /kreuzverhör, auf den Prüfstand, durch die Mangel drehen."
---

# Kreuzverhör

Dieser Skill prüft eine Entscheidung, bevor sie fällt. Statt einer einzelnen Einschätzung entstehen fünf unabhängige Antworten aus fest verteilten Blickwinkeln. Sie werden anonym gegeneinander bewertet, ihre tragenden Behauptungen werden gegen Quellen geprüft, und ein Vorsitz fasst alles zu einem Urteil zusammen, das seine Annahmen offenlegt.

Entstanden ist der Skill bei der Prüfung eines Businessplans für eine Gründung. Eine erste KI-Einschätzung klang überzeugend und lag an zwei entscheidenden Stellen falsch, weil mehrere Modelle dieselbe unbelegte Annahme wiederholt hatten. Deshalb zählen in diesem Skill Belege mehr als Einigkeit.

Methodische Grundlage ist Andrej Karpathys LLM Council: mehrere Modelle beantworten dieselbe Frage, bewerten die anonymisierten Antworten gegenseitig in einer Rangliste, und ein Vorsitz führt sie zusammen. Diese Fassung arbeitet in Claude mit Sub-Agenten auf verschiedenen Claude-Modellen und ergänzt Rückfragen, Belegpflicht, Faktencheck und eine Sternwertung für die Belastbarkeit.

Alle Ausgaben an den Nutzer sind auf Deutsch.

---

## Einsatzbereich

Ein Kreuzverhör braucht mehrere Minuten und viele Modellaufrufe. Es lohnt sich, wenn eine falsche Entscheidung teuer wäre und mehr als eine Antwort vertretbar ist.

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

## Modellwahl

Sub-Agenten auf demselben Modell teilen dieselben Denkmuster und damit dieselben Fehler. Karpathy umgeht das mit Modellen verschiedener Anbieter. Innerhalb von Claude kommt man dem am nächsten, wenn die Rollen auf unterschiedliche Modelle verteilt werden, über den `model`-Parameter des Agent-Tools:

| Rolle | Modell | Begründung |
|---|---|---|
| Advocatus Diaboli | `opus` | Gründliches Nachrechnen und Gegenlesen |
| Grundsatzdenker | `opus` | Hinterfragt die Fragestellung selbst |
| Chancensucher | `sonnet` | Ideenbreite, anderes Modell als die Analytiker |
| Außenstehender | `haiku` | Weniger Fachwissen passt zur Rolle des Laien |
| Macher | `sonnet` | Pragmatisch und schnell |
| Gegenprüfer (5×) | `sonnet` | Vergleichen und bewerten, parallel, kostengünstig |
| Faktenchecker | `opus` | Sorgfältige Recherche und Quellenbewertung |
| Vorsitz | `opus`, bei hohem Einsatz `fable` | Stärkstes Urteilsvermögen am Ende |

`fable` nur für den Vorsitz und nur bei Entscheidungen mit hohem Einsatz (Gründung, große Investition, Vertrag), weil es deutlich teurer ist. Ist ein Modell nicht verfügbar, den Agenten ohne `model`-Parameter starten (er nutzt dann das Hauptmodell) und das im Protokoll vermerken.

Auch gemischte Claude-Modelle bleiben eine Modellfamilie. Die Gegenprüfung ersetzt deshalb nicht den Faktencheck in Schritt 4.

---

## Die fünf Berater

Jede Rolle ist eine Arbeitsweise, keine Figur. Zusammen decken sie eine Vorlage von mehreren Seiten ab.

### 1. Der Advocatus Diaboli

Liest die Vorlage wie ein Prüfer, der einen Grund zur Ablehnung sucht. Er rechnet nach, stellt Aussagen nebeneinander und benennt Widersprüche, Lücken und Risiken. Findet er nichts Gravierendes, prüft er die Annahmen, die als selbstverständlich gelten. Sein Ziel ist eine Entscheidung, die einer harten Prüfung standhält.

### 2. Der Grundsatzdenker

Prüft zuerst die Frage selbst. Was soll am Ende erreicht werden, und führt die gestellte Frage dorthin? Er trennt Ziel und Mittel, legt unausgesprochene Voraussetzungen offen und schlägt eine andere Fragestellung vor, wenn die ursprüngliche zu eng gefasst ist.

### 3. Der Chancensucher

Fragt, was im Vorhaben steckt, wenn es gut läuft. Er sucht ungenutzte Hebel, angrenzende Märkte, Spielraum bei Preis und Paketen und Wege, aus einer Einzelleistung etwas Wiederholbares zu machen. Risiken überlässt er bewusst den anderen.

### 4. Der Außenstehende

Kennt weder die Branche noch die Vorgeschichte und liest nur, was vorliegt. Er markiert Fachbegriffe ohne Erklärung, Zahlen ohne Einordnung und Schritte, die nur für Eingeweihte logisch sind. So zeigt er, wie die Vorlage auf Kunden, Prüfer oder Geldgeber wirkt.

### 5. Der Macher

Denkt in Arbeitsschritten: Was ist zuerst zu tun, wer macht es, bis wann und mit welchen Mitteln? Pläne ohne erkennbaren Anfang oder mit unrealistischen Fristen benennt er klar.

**Warum diese Besetzung:** Advocatus Diaboli und Chancensucher bewerten dieselbe Vorlage aus entgegengesetzten Richtungen, Risiko und Potenzial. Grundsatzdenker und Macher setzen an den beiden Enden an, bei der Frage und bei der Umsetzung. Der Außenstehende prüft, ob das Ganze ohne Insiderwissen verständlich ist.

---

## Ablauf

### Schritt 1: Kontext, Rückfragen, Fragestellung

**A. Kontext lesen.** Was der Nutzer schreibt, reicht selten für ein belastbares Urteil. Deshalb kurz zusammentragen und lesen:

- gespeicherte Informationen zum Nutzer, soweit sie für die Frage eine Rolle spielen (Geschäftsmodell, Rolle, Rahmenbedingungen)
- Projektdateien, `CLAUDE.md` oder einen `memory/`-Ordner, falls vorhanden
- angehängte oder genannte Dateien, vollständig
- frühere Kreuzverhör-Protokolle zum selben Thema
- weitere Unterlagen, die zur Frage passen (bei Preisfragen etwa Umsätze oder frühere Angebote)

**B. Kippende Fakten erfragen.** Hängt das Urteil an einem Fakt, den nur der Nutzer kennt (Vertragslage, Zusagen von Kunden, Absprachen mit Behörden, wie ein Arbeitsverhältnis endet), diese Fragen vor dem Verhör stellen: höchstens drei, gebündelt in einer Nachricht, wo verfügbar mit AskUserQuestion. Nicht den ungünstigsten Fall unterstellen und das Verhör darauf aufbauen. Ist der Nutzer nicht erreichbar, die Lücke in der Fragestellung als „unbekannt“ führen.

Ist der Gegenstand insgesamt unklar („Kreuzverhör: mein Business“), eine einzige Rückfrage dazu stellen.

**C. Fragestellung schreiben.** Eine Fassung für alle fünf Berater, bestehend aus:

1. der zu treffenden Entscheidung
2. den Fakten aus Unterlagen und Antworten des Nutzers, jeweils mit Herkunft („laut Plan S. 12“, „laut Nutzer“)
3. den ausdrücklich markierten Unbekannten
4. dem, was auf dem Spiel steht

Die Fragestellung enthält keine eigene Analyse. Sätze wie „hier fehlt X“ lenken alle fünf Berater auf denselben Punkt. Selbstaussagen des Nutzers über Markt oder Preise („liegt unter Marktniveau“) als Selbstaussage kennzeichnen.

Die Fragestellung in eine Datei schreiben, damit alle Agenten dieselbe Fassung lesen und sie im Protokoll erhalten bleibt. Längere Unterlagen per Pfad übergeben.

### Schritt 2: Das Verhör (5 Sub-Agenten parallel)

Alle fünf Berater in einer Nachricht starten, jeweils mit dem Modell aus der Tabelle. Jede Antwort umfasst 150 bis 300 Wörter.

**Vorlage für den Berater-Prompt:**

```
Rolle: [Name des Beraters]
Arbeitsweise: [Beschreibung der Rolle von oben]

Fragestellung: [Pfad]
Unterlagen: [Pfad(e)]

Beurteile die Fragestellung ausschließlich aus deiner Rolle. Die übrigen Blickwinkel übernehmen andere Berater, du musst also nicht abwägen. Sag klar, was du für richtig, falsch oder lohnend hältst, und begründe es mit Bezug auf die Unterlagen.

Kennzeichne jede Zahl, Marktangabe und Rechtsbehauptung:
[U] steht so in den Unterlagen oder der Fragestellung
[R] von dir nachgerechnet
[Q] mit Quelle belegt (Quelle nennen)
[A] deine Annahme oder Einschätzung
Rechtsfolgen nur als sicher darstellen, wenn du sie belegen kannst, sonst als [A] mit Hinweis, was zu prüfen wäre. Was als unbekannt markiert ist, gilt als unbekannt, nicht als Fehler.

Umfang: 150 bis 300 Wörter, Deutsch, ohne Einleitung.
```

### Schritt 3: Die Gegenprüfung (5 Sub-Agenten parallel)

Vor der Bewertung werden die Antworten von den Rollennamen getrennt. Sonst bewerten Prüfer die Rolle statt des Inhalts. Die fünf Antworten per Skript zufällig den Buchstaben A bis E zuordnen und in eine Datei schreiben. Die Zuordnung festhalten, sie wird für die Wertung und für Schritt 5 gebraucht.

Dann fünf Prüfer starten, jeder mit allen fünf Antworten.

**Vorlage für den Prüfer-Prompt:**

```
Aufgabe: Bewerte fünf anonymisierte Antworten auf dieselbe Fragestellung.

Fragestellung: [Pfad]
Antworten A bis E: [Pfad]
Unterlagen zum Abgleich: [Pfad(e)]

Beantworte vier Fragen und nenne dabei die Buchstaben:
1. Welche Antwort trägt am meisten zur Entscheidung bei, und warum?
2. Welcher Antwort fehlt am meisten, und was genau?
3. Welche Aussagen sind falsch oder unbelegt? Achte besonders auf [A]-Angaben und auf Widersprüche zu den Unterlagen. Sieh in den Unterlagen nach, bevor du behauptest, dort fehle etwas.
4. Gibt es einen Punkt, den keine Antwort behandelt? Nur nennen, wenn er das Ergebnis ändern kann, und als „wesentlich“ oder „Randrisiko“ einordnen, mit Begründung für diesen Fall. „Nichts Wesentliches“ ist eine gültige Antwort.

Bewerte danach alle fünf Antworten:
- Rangliste von Platz 1 (trägt am meisten) bis Platz 5. Jeder Platz genau einmal.
- Sterne für die Belastbarkeit, mehrfach vergebbar:
  5 = schlüssig und belegt
  4 = überwiegend belegt, kleine Lücken
  3 = plausibel, aber mit wichtigen unbelegten Annahmen
  2 = deutliche Lücken oder Fehler
  1 = nicht tragfähig

Schließe mit diesem Block ab (Beispielwerte ersetzen):
RANGLISTE: C, A, E, B, D
STERNE: A=4, B=3, C=5, D=2, E=3

Umfang: höchstens 250 Wörter ohne Abschlussblock, Deutsch.
```

**Gleichklang prüfen:** Nennen alle Prüfer denselben blinden Fleck, ist das zunächst ein Hinweis auf eine gemeinsame Modellneigung, kein starker Befund. Solche Punkte gehen immer in den Faktencheck.

**Wertung berechnen:** Buchstaben wieder den Beratern zuordnen und je Berater zwei Werte bilden:

- **Ø Rang:** Durchschnitt der fünf Platzierungen (1 = trägt am meisten), eine Nachkommastelle
- **Ø Sterne:** Durchschnitt der fünf Sternwertungen, eine Nachkommastelle

Die Werte per Skript berechnen. Darstellung: Sterne auf halbe Sterne runden und mit ★ (voll), ⯪ (halb) und ☆ (leer) auf fünf Stellen auffüllen, dahinter der genaue Wert. Beispiele: 4,4 → ★★★★⯪ 4,4; 3,6 → ★★★⯪☆ 3,6; 2,8 → ★★★☆☆ 2,8. Sortierung nach Ø Rang, bei Gleichstand nach Sternen.

Rang und Sterne getrennt lesen: Der Rang zeigt, welche Sicht vorn liegt, die Sterne zeigen, ob sie trägt. Platz 1 mit drei Sternen bedeutet: die beste Antwort in einem schwachen Feld.

### Schritt 4: Der Faktencheck (1 Sub-Agent)

Aus Beratern und Gegenprüfung die drei bis sechs Behauptungen auswählen, auf denen das Urteil ruhen würde: Marktzahlen, Rechtsfolgen, Rechenergebnisse und alles, was mehrere Agenten gleich behaupten. Einen Faktenchecker (`opus`) mit Websuche starten.

**Vorlage für den Faktencheck-Prompt:**

```
Aufgabe: Prüfe die folgenden Behauptungen aus einem Kreuzverhör. Nutze Websuche für aktuelle Marktzahlen und Rechtslage und rechne Zahlen nach. Unterlagen: [Pfad(e)].

Behauptungen:
1. [Behauptung] (von: Berater oder Prüfer)
2. ...

Je Behauptung:
- Ergebnis: bestätigt / teilweise richtig / falsch / nicht prüfbar
- Begründung in ein bis zwei Sätzen
- Quelle mit Link und Datum, oder Rechenweg
- Bedeutung für diesen Fall: hoch / gering (gering etwa bei einem Randfall, dessen Voraussetzungen hier nicht vorliegen)

Deutsch, ohne Einleitung.
```

Rechtliche und steuerliche Punkte gibt der Faktenchecker als allgemeine Information aus. Das Urteil verweist dann kurz auf eine Fachberatung (Anwalt, Steuerberater).

### Schritt 5: Das Urteil (1 Sub-Agent)

Den Vorsitz als eigenen Sub-Agenten starten (`opus`, bei hohem Einsatz `fable`). Er erhält Fragestellung, Berater-Antworten mit Rollennamen, Gegenprüfungen, Wertung und Faktencheck.

**Vorlage für den Vorsitz-Prompt:**

```
Rolle: Vorsitz eines Kreuzverhörs.
Aufgabe: Aus fünf Berater-Antworten, ihren Gegenprüfungen, der Wertung und dem Faktencheck ein Urteil bilden.

Fragestellung: [Pfad]
Berater-Antworten mit Rollennamen: [Pfad]
Gegenprüfungen: [Pfad]
Wertung (Ø Rang, Ø Sterne je Berater): [Pfad oder Tabelle]
Faktencheck: [Pfad]

Regeln:
- Vom Faktencheck widerlegte Aussagen sind keine Argumente mehr. Höchstens als korrigierte Annahme erwähnen.
- Belege wiegen schwerer als Häufigkeit. Eine belegte Aussage schlägt fünf gleichlautende unbelegte.
- Randrisiken als Randrisiken kennzeichnen.
- Folge der besser belegten Position, auch gegen die Mehrheit, und sag, warum.
- Die Wertung ist ein Hinweis. Widerlegt der Faktencheck eine hoch bewertete Antwort, gilt der Faktencheck.
- Entscheidungen, die der Nutzer erkennbar bewusst und begründet getroffen hat, als solche respektieren. Abweichende Vorschläge als Option kennzeichnen, nicht als Fehler.
- Leg dich fest. Eine Empfehlung mit Bedingungen ist zulässig, eine ohne Richtung nicht.

Gliederung, Deutsch:

## Wertung der Gegenprüfung
[Tabelle mit Platz, Berater, Ø Rang und Belastbarkeit unverändert übernehmen. Darunter ein bis zwei Sätze: wer vorn liegt und warum, und ob Rang und Sterne auseinanderfallen.]

## Wo Einigkeit herrscht
[Punkte, zu denen mehrere Berater unabhängig gelangt sind und die belegt oder plausibel sind.]

## Wo gestritten wird
[Echte Meinungsverschiedenheiten mit beiden Positionen und dem Grund, warum sie auseinandergehen.]

## Blinde Flecken, die das Verhör aufgedeckt hat
[Nur wesentliche Punkte aus Gegenprüfung oder Faktencheck.]

## Tragende Annahmen
[Zwei bis vier Annahmen mit Status belegt / Aussage des Nutzers / ungeprüft, und was sich ändert, wenn eine nicht zutrifft.]

## Die Empfehlung
[Klare Empfehlung mit Begründung.]

## Der erste Schritt
[Genau ein konkreter Schritt.]
```

Vor der Ausgabe gleicht das Hauptmodell das Urteil mit Faktencheck und Unterlagen ab und korrigiert, was widerlegt ist oder den Unterlagen widerspricht.

### Schritt 6: Ausgabe im Chat

Das Urteil als Markdown direkt im Chat ausgeben, ohne zusätzliche Dateien:

```
## Urteil im Kreuzverhör: {Thema in wenigen Worten}

### Wertung der Gegenprüfung

| Platz | Berater | Ø Rang | Belastbarkeit |
|:---:|---|:---:|---|
| 1 | {Berater} | {x,x} | {★★★★⯪ x,x} |
| … | … | … | … |

*Ø Rang: Durchschnitt der Platzierungen durch die Prüfer, 1 = trägt am meisten. Belastbarkeit: 5 Sterne = schlüssig und belegt, 1 Stern = nicht tragfähig.*

{ein bis zwei Sätze Einordnung}

### Wo Einigkeit herrscht
{Inhalt}

### Wo gestritten wird
{Inhalt}

### Blinde Flecken, die das Verhör aufgedeckt hat
{Inhalt}

### Tragende Annahmen
{Inhalt}

### Die Empfehlung
{Inhalt}

### Der erste Schritt
{Inhalt}
```

Aufzählungen nutzen, Absätze kurz halten. Sterne immer mit Zahl dahinter zeigen, damit die Wertung auch dort lesbar bleibt, wo der halbe Stern nicht dargestellt wird. Quellen aus dem Faktencheck am Ende als verlinkte Liste. Die einzelnen Berater-Antworten nur auf Wunsch vollständig zeigen.

**Korrigiert der Nutzer danach einen Punkt**, das Urteil nicht verteidigen. Sagen, welche Teile damit entfallen oder sich ändern, und den Rest neu einordnen.

### Schritt 7: Protokoll (optional)

Ein Protokoll nur anlegen, wenn der Nutzer es wünscht oder die Entscheidung später nachvollziehbar sein muss. Dateiname `kreuzverhoer-protokoll-[Zeitstempel].md`, Inhalt: Fragestellung, eingesetzte Modelle, Berater-Antworten, Gegenprüfungen, Wertung mit Einzelplatzierungen und Sternen je Prüfer, Faktencheck und Urteil.

---

## Beispiel: Businessplan für eine Gründung

Das Beispiel geht auf den Fall zurück, an dem der Skill entwickelt wurde. Zahlen und Antworten sind gekürzt.

**Nutzer:** „Kreuzverhör: Anbei mein Businessplan für den Gründungszuschuss. Ich mache mich als SEO-Berater selbstständig. Trägt der Plan, und kommt er bei der fachkundigen Stelle durch?“

**Rückfrage (Schritt 1):** „Der Plan sagt nicht, wie das bisherige Arbeitsverhältnis endet. Davon hängt der Anspruch auf den Zuschuss ab. Wie ist das geregelt?“
**Nutzer:** „Es endet vor der Gründung, der Antrag ist mit der Agentur für Arbeit abgestimmt.“

**Der Advocatus Diaboli:** „Engpass ist die Liquidität, nicht der Gewinn. Im dritten Monat bleiben wenige hundert Euro [U], ohne Zuschuss wäre der Saldo negativ [R]. Kommt der erste Zahlungseingang einen Monat später, reicht auch der Zuschuss nicht [R] …“

**Der Grundsatzdenker:** „Ob der Antrag durchkommt, ist die kleinere Frage. Entscheidend ist, ob das Modell nach Ende der Förderung trägt. Der Überschuss im ersten Jahr ist knapp [U] …“

**Der Chancensucher:** „Interim-Mandate stehen im ersten Jahr mit null im Plan [U]. Unternehmen, deren SEO-Leitung ausfällt, buchen solche Einsätze oft über mehrere Monate [A] …“

**Der Außenstehende:** „Was bedeutet ein Sichtbarkeitsindex von 0,47 [U]? Als Sachbearbeiter bräuchte ich Umsatzzahlen statt Fachkennzahlen …“

**Der Macher:** „Die fachkundige Stelle ist im Plan noch offen [U]. Ohne ihre Stellungnahme gibt es keinen Antrag. Das gehört in diese Woche …“

**Faktencheck (Auszug):**
- „Der Tagessatz liegt unter Marktniveau“ (Selbstaussage im Plan, von vier Beratern übernommen): falsch. Der Median selbstständiger SEO-Berater mit über sechs Jahren Erfahrung liegt bei rund 720 € pro Tag (freelancermap, September 2026), der Satz im Plan darüber. Bedeutung: hoch.
- „Rentenversicherungspflicht nach § 2 Nr. 9 SGB VI“ (von allen Prüfern als blinder Fleck genannt): teilweise richtig. Greift nur bei im Wesentlichen einem Auftraggeber, geplant sind mehrere Mandate. Bedeutung: gering.

**Urteil (Auszug):**

*Wertung der Gegenprüfung:*

| Platz | Berater | Ø Rang | Belastbarkeit |
|:---:|---|:---:|---|
| 1 | Der Advocatus Diaboli | 1,4 | ★★★★⯪ 4,4 |
| 2 | Der Macher | 2,2 | ★★★★☆ 4,0 |
| 3 | Der Grundsatzdenker | 2,8 | ★★★⯪☆ 3,6 |
| 4 | Der Außenstehende | 3,8 | ★★★☆☆ 3,2 |
| 5 | Der Chancensucher | 4,8 | ★★⯪☆☆ 2,4 |

Der Advocatus Diaboli liegt vorn, weil seine Liquiditätsrechnung nachgerechnet ist. Der Chancensucher bringt eine brauchbare Idee, stützt sie aber fast nur auf Annahmen.

*Wo Einigkeit herrscht:* Das Vorhaben ist tragfähig, die ersten drei Monate sind bei der Liquidität knapp.

*Wo gestritten wird:* Der Preis. Mehrere Berater wollen ihn anheben, der Faktencheck zeigt aber, dass er schon über dem Freelancer-Median liegt. Eine Anhebung ist damit eine Option, kein Befund.

*Blinde Flecken:* Die Liquiditätsplanung enthält keine Sondervorauszahlung zur Umsatzsteuer für den Fall einer Dauerfristverlängerung.

*Tragende Annahmen:* Zwei Mandate starten in den ersten drei Monaten (Aussage des Nutzers). Der Zuschuss wird bewilligt (ungeprüft, Ermessensleistung). Startet das erste Mandat einen Monat später, wird der Saldo auch mit Zuschuss negativ.

*Empfehlung:* Gründen und einreichen, nach drei Korrekturen: Formulierungen ersetzen, die gegen den Bedarf am Zuschuss sprechen, Widersprüche im Plan auflösen und einen Puffer für das erste Quartal ausweisen. Steuerliche Details mit dem Steuerberater klären.

*Erster Schritt:* Die fachkundige Stelle noch diese Woche festlegen.

---

## Arbeitsregeln

- **Fakten erfragen statt unterstellen.** Hängt das Urteil an einem Fakt, den nur der Nutzer kennt, vor dem Verhör nachfragen.
- **Fragestellung ohne Wertung.** Eigene Analyse in der Fragestellung lenkt alle Berater in dieselbe Richtung.
- **Berater gleichzeitig starten.** Nacheinander gestartete Agenten kosten Zeit, und spätere Antworten können frühere aufgreifen.
- **Modelle mischen.** Gleiche Modelle teilen gleiche blinde Flecken.
- **Anonym bewerten.** Sichtbare Rollennamen beeinflussen das Urteil der Prüfer.
- **Rang und Sterne getrennt lesen.** Der Rang zeigt, welche Sicht vorn liegt, die Sterne, ob sie trägt.
- **Gleichklang prüfen.** Was mehrere Modelle gleich behaupten, kommt in den Faktencheck.
- **Belege vor Mehrheit.** Der Vorsitz folgt der besser belegten Position.
- **Einfache Fragen direkt beantworten.** Nicht jede Frage braucht ein Kreuzverhör.
- **Das Urteil muss allein stehen.** Die meisten Nutzer lesen nur das Urteil. Es muss ohne die Einzelantworten verständlich sein und seine Annahmen offen zeigen.
- **Ehrlich bleiben,** auch wenn erkennbar Zustimmung erwartet wird.

---

Methode nach Andrej Karpathys LLM Council. Die Grundidee fester Denkrollen geht auf den LLM-Council-Skill von Ole Lehmann zurück. Texte, Ablauf und Erweiterungen dieser Fassung sind eigenständig formuliert. Bereitgestellt von conexio.de unter MIT-Lizenz.
