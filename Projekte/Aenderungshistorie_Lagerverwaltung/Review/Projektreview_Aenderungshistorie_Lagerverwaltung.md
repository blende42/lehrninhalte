# Projektreview Änderungshistorie für Lagerverwaltung

[Zur Projektübersicht](../README.md) | [Projektauftrag](../Lernende/Projektauftrag_Aenderungshistorie_Lagerverwaltung.md) | [Hinweise für Lehrperson](../Lehrperson/Projektauftrag_Aenderungshistorie_Lagerverwaltung_LP.md)

Diese Review-Session ist ein Einzelgespräch im Coaching- und Mentoring-Stil. Es geht nicht um Noten oder eine perfekte Zielarchitektur, sondern um Verstehen, Begründen und gezielte Verbesserung.

## 1. Ziel des Reviews

Der Review unterstützt die Nachbesprechung des Mini-Projekts `Änderungshistorie für Lagerverwaltung`.

Im Fokus stehen:

- Architektur und Verantwortlichkeiten
- Fachlogik und Nachvollziehbarkeit
- Testbarkeit und sinnvolle Randfälle
- Reflexion über Strukturentscheidungen
- kleine, konkrete Verbesserungen

Nicht im Fokus stehen:

- Syntaxdetails ohne Bezug zur Lösung
- eine vollständige Musterlösung
- eine fixe Zielarchitektur
- Prüfungsrhetorik oder Bewertungsnoten

Leitidee:

```text
Die Lösung soll nicht nur funktionieren.
Sie soll erklärbar, testbar und gezielt verbesserbar sein.
```

## 2. Projektpräsentation

Der Lernende zeigt kurz die Anwendung und erklärt den groben Ablauf. Eine kleine Demo mit Beispieldaten reicht.

Die Fragen sind eine Auswahl für das Gespräch. Die Lehrperson wählt wenige passende Fragen aus und vertieft dort, wo Architektur, Verantwortlichkeiten oder Tests noch unklar sind.

Mögliche Fragen:

- Welche Funktion deiner Lagerverwaltung zeigst du zuerst?
- Wie löst du eine Bestandsänderung aus?
- Wie löst du eine Preisänderung aus?
- Wo wird der alte Wert gelesen?
- Wo wird der neue Wert gesetzt?
- Wie entsteht ein Historieneintrag?
- Wie zeigst du die Änderungshistorie an?
- Wie speicherst du die Historie als CSV?
- Wie lädst du die Historie wieder aus CSV?
- Welche Tests möchtest du zeigen?

Beobachtung:

- Ist der Ablauf nachvollziehbar?
- Sind die wichtigsten Klassen benennbar?
- Wird klar, wo Fachlogik, Historie und Persistenz liegen?

## 3. Architekturgespräch

In diesem Teil geht es um Entscheidungen und Begründungen. Fachbegriffe sind hilfreich, aber weniger wichtig als klare Erklärungen.

Fragen zur Struktur:

- Warum hast du diese Struktur gewählt?
- Welche Packages verwendest du, und warum?
- Welche Klassen sind zentral?
- Welche Klasse startet nur den Ablauf?
- Welche Klasse enthält Fachlogik?
- Welche Klasse kennt das Änderungsjournal?
- Welche Klasse kennt das CSV-Format der Historie?
- Welche Klasse wird am schnellsten zu gross?

Fragen zu Verantwortlichkeiten:

- Warum gibt es eigene Klassen für Änderungen oder warum nicht?
- Gibt es einen `JournalService`? Wenn ja, welche Verantwortung hat er?
- Falls es keinen `JournalService` gibt: Wo liegt die Verantwortung für die Historie?
- Was macht `LagerService`?
- Enthält `LagerService` nur Lagerlogik oder auch Journal- und CSV-Logik?
- Bleibt `Produkt` ein Datenobjekt?
- Gibt es doppelte Logik beim Erstellen von Historieneinträgen?

Mögliche Verantwortlichkeitstabelle für das Gespräch:

| Klasse oder Bereich | Mögliche Verantwortung | Gesprächspunkt |
| --- | --- | --- |
| `Main` | Ablauf starten und steuern | Bleibt `Main` klein? |
| `LagerService` | Fachlogik für Lageränderungen | Enthält er passende Regeln? |
| `JournalService` oder `AenderungsJournal` | Historie und Nachvollziehbarkeit | Ist die Journal-Verantwortung klar? |
| `ProduktSpeicher` | Persistenz von Produkten und Historie | Ist CSV von Fachlogik getrennt? |
| `Produkt` | Produktdaten | Bleibt das Objekt einfach? |
| `AenderungsEintrag` | Zeitpunkt, alter Wert, neuer Wert, Grund | Sind die Daten vollständig? |

Fragen zu Erweiterbarkeit:

- Wo wäre eine neue Änderungsart schwierig einzubauen?
- Wo könnten Duplikate entstehen?
- Welche Methode würdest du zuerst ändern, wenn eine neue Anforderung kommt?
- Welche Klasse würdest du nicht weiter vergrössern?

## 4. Testreview

Der Testreview fragt nicht nur, ob Tests vorhanden sind. Wichtig ist, welche Fachlogik sie absichern.

Fragen zu fachlichen Tests:

- Welche Tests geben dir am meisten Sicherheit?
- Gibt es einen Test für Bestandsänderungen?
- Gibt es einen Test für Preisänderungen?
- Wird geprüft, dass alter und neuer Wert korrekt gespeichert werden?
- Wird geprüft, dass Zeitpunkt, Änderungsart und Grund vorhanden sind?
- Wird eine ungültige Änderung geprüft?
- Was passiert bei negativem Preis?
- Was passiert bei negativem Bestand?

Fragen zur Historie:

- Prüft ein Test, dass ein Historieneintrag entsteht?
- Prüft ein Test mehrere Historieneinträge?
- Wird die Reihenfolge der Historie geprüft?
- Wird die gespeicherte Historie wieder geladen?
- Ist das Laden der Historie automatisiert getestet oder manuell nachgewiesen?

Fragen zur Testqualität:

- Prüfen die Tests Fachlogik oder nur Getter und Setter?
- Hängen die Tests unnötig stark von echten Dateien ab?
- Welche Tests prüfen Fachlogik ohne Datei?
- Welche Tests prüfen bewusst CSV-Speichern und CSV-Laden?
- Welche Fachlogik könntest du ohne Datei testen?
- Welcher Test fehlt noch als nächster sinnvoller Schritt?

## 5. Refactoring-Ideen

Der Refactoring-Teil bleibt klein. Es geht um konkrete nächste Schritte, nicht um eine komplette Neuschreibung.

Mögliche Diskussionspunkte:

- Journal-Logik aus `Main` oder `LagerService` trennen
- Verantwortlichkeiten zwischen Lagerlogik, Journal und Persistenz schärfen
- Methoden vereinfachen oder aufteilen
- Benennungen verbessern
- Tests für fehlende Randfälle ergänzen
- doppelte Logik beim Erstellen von Historieneinträgen reduzieren
- CSV-Laden und CSV-Speichern in eine klar zuständige Klasse verschieben
- Zeitstempel-Erzeugung an eine nachvollziehbare Stelle legen

Leitfragen für jede Refactoring-Idee:

- Was wird dadurch verständlicher?
- Was wird leichter testbar?
- Welche spätere Änderung wird einfacher?
- Ist der Schritt klein genug, um ihn sicher umzusetzen?

## 6. Reflexion

Die Reflexion soll zeigen, wie der Lernende über die eigene Lösung denkt.

Mögliche Fragen:

- Was war an der Änderungshistorie schwieriger als erwartet?
- Welche Struktur hat dir geholfen?
- Welche Verantwortung war unklar?
- Welche Klasse ist am besten gelungen?
- Welche Klasse wurde zu gross?
- Was würdest du heute anders lösen?
- Welche Entscheidung hättest du früher treffen sollen?
- Welche Fachregel war schwer zu testen?
- Welche Erweiterung wäre fachlich sinnvoll, aber strukturell schwierig?
- Wo ist deine Lösung bewusst einfach geblieben?

## 7. Nächste Lernschritte

Am Ende werden wenige konkrete nächste Schritte festgehalten.

Mögliche nächste Schritte:

- einen zusätzlichen fachlichen Test ergänzen
- CSV-Laden oder CSV-Speichern besser von Fachlogik trennen
- eine überladene Methode aufteilen
- Methodennamen präzisieren
- Verantwortlichkeiten in einer kurzen Tabelle dokumentieren
- Historie für weitere Änderungstypen vorbereiten
- bestehende Struktur anhand einer kleinen Erweiterung erneut prüfen

Kurzer Ausblick:

- Weitere fachliche Erweiterungen sollen zuerst über Verantwortlichkeiten geplant werden.
- Die Struktur darf wachsen, aber nur mit begründeten Klassen.
- `Main` bleibt Ablaufsteuerung.
- Fachlogik und Persistenz bleiben getrennt.
- Tests sollen sichtbar machen, welche Regeln stabil sind.
