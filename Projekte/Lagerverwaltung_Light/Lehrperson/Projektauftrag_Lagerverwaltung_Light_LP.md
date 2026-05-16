# Projektauftrag Lagerverwaltung Light LP

[Zur Projektübersicht](../README.md) | [Lernenden-Version](../Lernende/Projektauftrag_Lagerverwaltung_Light.md)

## Didaktischer Zweck

Dieses Mini-Projekt bündelt die bisherige Java-Sequenz in einem offenen, aber fachlich klar begrenzten Auftrag.

Die Lernenden sollen bekannte Konzepte selbständig kombinieren:

- Klassen und Objekte
- Kapselung
- `ArrayList`
- Methoden
- Maven
- Packages
- CSV-Persistenz
- Tests mit JUnit
- Verantwortlichkeiten
- Interfaces
- Polymorphie
- Wiederverwendung

Der Auftrag soll sichtbar machen, ob Lernende Strukturentscheidungen treffen, Fachlogik von Infrastruktur trennen und ihr Vorgehen begründen können. Es ist keine Schritt-für-Schritt-Übung und keine Vorlage für eine einzige Zielarchitektur.

## Beobachtungspunkte

Während der Bearbeitung sind besonders diese Punkte diagnostisch interessant:

- Bleibt zu viel Code in `main`?
- Werden Klassen nach fachlichen Verantwortlichkeiten geschnitten?
- Wird das Produktmodell gekapselt oder werden Attribute direkt öffentlich gemacht?
- Wird die `ArrayList` sicher und nachvollziehbar verwendet?
- Werden Verkauf und Bestand fachlich korrekt behandelt?
- Werden ungültige Werte aktiv abgefangen?
- Ist CSV-Laden und CSV-Speichern nachvollziehbar getrennt von der Fachlogik?
- Werden Tests für Fachlogik geschrieben oder nur triviale Methoden geprüft?
- Wird ein Interface sinnvoll eingesetzt oder nur formal ergänzt?
- Können Lernende erklären, warum ihre Struktur so gewählt wurde?
- Gibt es unnötige Code-Duplikate beim Formatieren, Suchen oder Speichern?

## Typische Schwierigkeiten

- Lernende starten direkt mit Datei-I/O und verlieren die Fachlogik aus dem Blick.
- `main` wird zur Sammelstelle für Laden, Verkaufen, Speichern und Anzeigen.
- Verkauf wird nur als Ausgabe simuliert, ohne den Bestand im Objekt zu verändern.
- Ungültige Werte werden ignoriert oder erst sehr spät behandelt.
- CSV-Parsing wird zu kompliziert oder zu fragil.
- Tests hängen unnötig stark von echten Dateien ab.
- Interface und konkrete Implementierung werden verwechselt.
- Eine zweite Speicherart wird zu früh umgesetzt, bevor der Pflichtteil stabil ist.
- Es werden zu viele Architektur-Abstraktionen gebaut, bevor die Fachlogik funktioniert.
- Wiederverwendung wird mit unnötiger Vererbung verwechselt.

## Mögliche Hilfestellungen

Hilfestellungen sollten Orientierung geben, ohne die Lösung vorzugeben.

Geeignete Impulse:

- „Welche Klasse kennt die Liste der Produkte?“
- „Welche Methode verändert den Bestand wirklich?“
- „Kannst du den Verkauf testen, ohne zuerst eine CSV-Datei zu lesen?“
- „Welche Verantwortung hat diese Klasse genau?“
- „Wo würdest du später eine zweite Speicherart anschliessen?“
- „Welche drei Randfälle beweisen, dass dein Verkauf robust ist?“
- „Welche Codezeilen sind fast gleich und könnten wiederverwendet werden?“

Bei Bedarf kann eine kleine Skizze mit möglichen Verantwortlichkeiten helfen. Diese sollte als Beispiel und nicht als vorgeschriebene Architektur gezeigt werden.

## Bewertungsideen

Eine Bewertung kann mit einem einfachen Raster erfolgen. Gewichtung je nach Unterrichtsziel:

- Fachfunktion: Pflichtanforderungen, Verkauf, Bestandsänderung, Hinzufügen und Anzeigen funktionieren.
- Persistenz und Fehlerfälle: CSV-Laden, CSV-Speichern, ungültige Werte und doppelte Namen werden nachvollziehbar behandelt.
- Struktur: Klassen, Packages, Verantwortlichkeiten, Interface, Polymorphie und Wiederverwendung sind sinnvoll eingesetzt.
- Tests: mindestens 4 fachliche JUnit-Tests prüfen zentrale Logik und Randfälle.
- Reflexion: Entscheidungen, Schwierigkeiten und Verbesserungsmöglichkeiten werden konkret begründet.

Bewertungsideen sollten nicht dazu führen, dass alle Lösungen gleich aussehen müssen. Verschiedene einfache Strukturen können fachlich richtig sein.

## Mögliche Lösungsrichtungen

Keine vollständige Musterlösung ist zwingend nötig. Mögliche Lösungsrichtungen reichen aus, solange die Auswertung über Pflichtanforderungen, Tests, Demo und Reflexion erfolgen kann.

Mögliche Bausteine:

- eine Produktklasse mit Name, Preis und Bestand
- eine Verwaltungsklasse, die Produkte sucht, ergänzt und Verkäufe ausführt
- eine Speicher-Schnittstelle für Laden und Speichern
- eine CSV-Implementierung dieser Speicher-Schnittstelle
- ein Einstiegspunkt, der Laden, einfache Bedienung oder Demo und Speichern koordiniert
- JUnit-Tests für Verkauf, ungültige Werte und Ergänzen von Produkten

Diese Bausteine sind keine Zielarchitektur. Lernende dürfen anders strukturieren, wenn Verantwortlichkeiten, Testbarkeit und Verständlichkeit stimmen.

## Hinweise zu Architekturentscheidungen

Achte weniger auf perfekte Architekturbegriffe und stärker auf nachvollziehbare Entscheidungen:

- Ist klar, welche Klasse Fachlogik enthält?
- Ist klar, welche Klasse oder Methode CSV-Daten liest und schreibt?
- Sind Modell, Fachlogik und Programmstart nicht unnötig vermischt?
- Unterstützen Packages die Orientierung?
- Wird das Interface dort eingesetzt, wo Austauschbarkeit sinnvoll erklärbar ist?
- Bleibt die Lösung einfacher als das Problem?
- Können Lernende ihre Struktur mit eigenen Worten begründen?

Nicht verlangen:

- Spring
- Dependency Injection Frameworks
- Datenbank
- REST-API
- GUI
- komplexe abstrakte Basisklassen
- vollständiges Repository-Pattern

## Bezug zur Lernenden-Version

Die [Lernenden-Version](../Lernende/Projektauftrag_Lagerverwaltung_Light.md) enthält den offenen Projektauftrag mit Anforderungen, technischem Rahmen, Testanforderungen, Abgabe und Reflexionsfragen.

Diese Lehrpersonen-Version ergänzt:

- didaktischen Zweck
- diagnostische Beobachtungspunkte
- typische Schwierigkeiten
- mögliche Hilfestellungen
- Bewertungsideen
- mögliche Lösungsrichtungen ohne vollständige Musterlösung
- Hinweise zu Architekturentscheidungen
