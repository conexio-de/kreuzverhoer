# Kreuzverhör

**Ein deutscher Entscheidungs-Skill für Claude und ChatGPT.** Fünf KI-Berater prüfen eine Entscheidung aus fest verteilten Blickwinkeln. Ihre Antworten werden anonym gegeneinander bewertet, ein Faktencheck prüft die tragenden Behauptungen, und ein Vorsitz bildet ein Urteil, das seine Annahmen offenlegt.

Bereitgestellt von [conexio.de – SEO- und GEO-Beratung](https://conexio.de).

---

## Warum es diesen Skill gibt

Ich wollte meinen Businessplan für eine Gründung kritisch prüfen lassen. Eine einzelne KI-Antwort war mir dafür zu wenig, weil man ihr nicht ansieht, ob sie stimmt.

Der erste Versuch mit mehreren KI-Beratern hat das bestätigt: Das Ergebnis klang überzeugend und lag an zwei Stellen falsch. Mehrere Berater hatten eine unbelegte Selbstaussage aus dem Plan übernommen, und alle Prüfer hielten einen Randfall für das größte Risiko. Daraus sind die Regeln entstanden, die den Skill heute ausmachen: Rückfragen statt Annahmen, Belegpflicht, ein eigener Faktencheck und eine Wertung, die zwischen „überzeugend“ und „belegt“ unterscheidet.

## Wofür er gedacht ist

**Passend:** Businesspläne, Preismodelle, Positionierung, Migrationen, Strategiewechsel. Alles, wo ein Fehler teuer wäre und mehr als eine Antwort vertretbar ist.

**Nicht passend:** Fragen mit einer feststellbaren richtigen Antwort, Schreibaufträge, Übersetzungen. Solche Anfragen beantwortet der Skill direkt.

## Die fünf Berater

| Berater | Arbeitsweise |
|---|---|
| **Advocatus Diaboli** | Liest wie ein Prüfer, der einen Ablehnungsgrund sucht, und rechnet nach |
| **Grundsatzdenker** | Prüft zuerst die Frage selbst und trennt Ziel und Mittel |
| **Chancensucher** | Sucht ungenutzte Hebel und Spielraum bei Preis und Paketen |
| **Außenstehender** | Liest ohne Branchenwissen und markiert, was nur Eingeweihte verstehen |
| **Macher** | Denkt in Arbeitsschritten: was zuerst, wer, bis wann |

## Ablauf

1. **Rückfragen:** Hängt das Urteil an einem Fakt, den nur du kennst, fragt der Skill zuerst nach.
2. **Verhör:** Fünf Berater antworten unabhängig. Jede Zahl wird markiert als Unterlage, nachgerechnet, belegt oder Annahme.
3. **Gegenprüfung:** Anonymisierte Bewertung mit Rangliste und Sternen für die Belastbarkeit.
4. **Faktencheck:** Die tragenden Behauptungen werden per Websuche und Rechnung geprüft.
5. **Urteil:** Wertung, Einigkeit, Streitpunkte, blinde Flecken, tragende Annahmen, Empfehlung und genau ein erster Schritt.

## Beispiel: Businessplan für eine Gründung

Gekürzt aus dem Fall, an dem der Skill entwickelt wurde.

> ### Wertung der Gegenprüfung
>
> | Platz | Berater | Ø Rang | Belastbarkeit |
> |:---:|---|:---:|---|
> | 1 | Advocatus Diaboli | 1,4 | ★★★★⯪ 4,4 |
> | 2 | Macher | 2,2 | ★★★★☆ 4,0 |
> | 3 | Grundsatzdenker | 2,8 | ★★★⯪☆ 3,6 |
> | 4 | Außenstehender | 3,8 | ★★★☆☆ 3,2 |
> | 5 | Chancensucher | 4,8 | ★★⯪☆☆ 2,4 |
>
> *Ø Rang: 1 = trägt am meisten. Belastbarkeit: 5 Sterne = schlüssig und belegt, 1 Stern = nicht tragfähig.*
>
> Der Advocatus Diaboli liegt vorn, weil seine Liquiditätsrechnung nachgerechnet ist. Der Chancensucher bringt eine brauchbare Idee, stützt sie aber fast nur auf Annahmen.
>
> ### Tragende Annahmen
> Zwei Mandate starten in den ersten drei Monaten (Aussage des Gründers). Startet das erste einen Monat später, wird der Saldo auch mit Zuschuss negativ.
>
> ### Der erste Schritt
> Die fachkundige Stelle noch diese Woche festlegen.

## Installation

### Claude

**Variante A:** Diesen Satz in einen neuen Chat kopieren:

> Bitte installiere diesen Skill für mich: https://github.com/conexio-de/kreuzverhoer – die Datei liegt unter `claude/kreuzverhoer/SKILL.md`.

**Variante B:** [`downloads/kreuzverhoer-claude.zip`](downloads/kreuzverhoer-claude.zip) herunterladen und in Claude als eigenen Skill hinzufügen. Anleitung von Anthropic: [Use skills in Claude](https://support.claude.com/en/articles/12512180-use-skills-in-claude).

Die Claude-Fassung startet die Berater als getrennte Sub-Agenten auf verschiedenen Claude-Modellen (Opus, Sonnet, Haiku), damit sie möglichst unabhängig urteilen.

### ChatGPT

[`downloads/kreuzverhoer-chatgpt.zip`](downloads/kreuzverhoer-chatgpt.zip) herunterladen. Darin:

- **`kreuzverhoer/SKILL.md`** für ChatGPT-Arbeitsbereiche mit freigeschalteten Skills ([Infos von OpenAI](https://academy.openai.com/public/resources/skills))
- **`custom-gpt-anweisungen.txt`** zum Einfügen in ein eigenes GPT oder Projekt. Funktioniert überall, Websuche aktivieren.

In ChatGPT spielt ein Modell alle Rollen nacheinander. Die Berater sind dadurch weniger unabhängig als in der Claude-Fassung.

## Aufruf

- „Kreuzverhör: Trägt mein Businessplan?“
- „/kreuzverhör Monatspauschale oder Projektpreis?“
- „Nimm das auf den Prüfstand.“
- „Dreh das durch die Mangel.“

## Inhalt des Repositorys

```
claude/kreuzverhoer/SKILL.md        Skill für Claude
chatgpt/kreuzverhoer/SKILL.md       Skill für ChatGPT
chatgpt/custom-gpt-anweisungen.txt  Kurzfassung für eigene GPTs und Projekte
downloads/                          fertige ZIP-Pakete
```

## Hinweis

Rechtliche und steuerliche Einschätzungen im Urteil sind allgemeine Informationen und ersetzen keine Fachberatung.

## Herkunft und Lizenz

Die Methode geht auf Andrej Karpathys [LLM Council](https://github.com/karpathy/llm-council) zurück: mehrere Modelle, anonyme Rangliste, Vorsitz. Die Grundidee fester Denkrollen stammt aus dem LLM-Council-Skill von Ole Lehmann. Texte, Ablauf und Erweiterungen dieser Fassung sind eigenständig formuliert.

Lizenz: [MIT](LICENSE). Du darfst den Skill frei nutzen, verändern und weitergeben, auch kommerziell.

---

**conexio.de** · SEO- und GEO-Beratung aus Oranienburg · [conexio.de](https://conexio.de)
