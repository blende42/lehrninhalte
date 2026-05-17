# Projektauftrag Änderungshistorie für Lagerverwaltung LP

[Zur Projektübersicht](../README.md) | [Lernenden-Version](../Lernende/Projektauftrag_Aenderungshistorie_Lagerverwaltung.md)

## Didaktischer Zweck

Dieses Mini-Projekt schliesst an die gefestigten Strukturkonzepte der Lagerverwaltung an. Die Lernenden führen keine grosse neue Technologie ein, sondern erweitern eine bekannte Anwendung um eine fachliche Anforderung.

Im Zentrum steht die Frage, ob Lernende Verantwortlichkeiten auf eine neue Situation übertragen können:

- aktuelle Produktdaten verwalten
- fachliche Änderungen durchführen
- Änderungen protokollieren
- Historie anzeigen
- Historie als CSV speichern
- Historie aus CSV laden
- Fachlogik testen

Der Auftrag soll sichtbar machen, ob Lernende die bekannten Rollen von `Main`, Services, Produktmodell und Persistenz bewusst anwenden und begründen können.

Es soll keine vollständige Musterlösung entstehen. Verschiedene einfache Strukturen sind fachlich vertretbar, wenn Verantwortlichkeiten, Testbarkeit und Lesbarkeit stimmen.

## Diagnostische Beobachtungspunkte

Während der Bearbeitung sind besonders diese Punkte interessant:

- Bleibt `Main` Ablaufsteuerung oder sammelt es wieder Fachlogik?
- Wird die Historie als fachliches Objekt verstanden oder nur als Konsolentext?
- Werden Bestandsänderung und Preisänderung fachlich sauber erfasst?
- Sind alter Wert, neuer Wert, Zeitpunkt und Grund zuverlässig vorhanden?
- Wird CSV-Schreiben in fachlichen Klassen vermischt?
- Wird die bestehende Lagerverwaltung verständlich erweitert?
- Werden Tests für Fachlogik geschrieben oder nur Getter und Setter geprüft?
- Können Lernende erklären, warum eine Klasse für eine Verantwortung zuständig ist?
- Wird ein möglicher `JournalService` sinnvoll begründet oder nur formal ergänzt?
- Bleibt die Lösung einfacher als das Problem?

## Typische Schwierigkeiten

- Die Änderung wird zwar ausgeführt, aber nicht protokolliert.
- Es wird nur Text auf der Konsole ausgegeben, aber kein Historieneintrag gespeichert.
- Alte Werte werden nach der Änderung gelesen und sind dadurch verloren.
- Zeitpunkt, Grund oder Änderungsart fehlen.
- Ungültige Änderungen wie negative Preise oder negative Bestände werden trotzdem protokolliert.
- Preisänderungen und Bestandsänderungen werden unnötig kompliziert modelliert.
- CSV-Details landen im `LagerService`.
- `Main` erstellt Einträge, verändert Produkte, speichert Dateien und gibt alles aus.
- Tests hängen stark von echten Dateien ab, obwohl die Fachlogik separat testbar wäre.
- Lernende bauen zu früh optionale Filter oder Statistiken, bevor der Pflichtteil stabil ist.
- Es wird eine starre Zielarchitektur erwartet, statt eigene Entscheidungen zu begründen.

## Mögliche Hilfestellungen

Hilfestellungen sollten Fragen stellen und keine vollständige Struktur vorgeben.

Geeignete Impulse:

- „Wann musst du den alten Wert lesen: vor oder nach der Änderung?“
- „Welche Klasse weiss, dass eine Preisänderung protokolliert werden muss?“
- „Kannst du einen Historieneintrag testen, ohne eine CSV-Datei zu schreiben?“
- „Welche Klasse kennt das CSV-Format der Historie?“
- „Kannst du gespeicherte Historieneinträge wieder laden und anzeigen?“
- „Was ist der Unterschied zwischen Produktdaten und Historie?“
- „Welche Verantwortung hat dein Journal?“
- „Welche Logik darf in `Main` bleiben?“
- „Welche drei Fälle beweisen, dass deine Historie fachlich funktioniert?“

Bei Bedarf kann eine kleine Verantwortungsskizze helfen. Sie sollte als mögliche Richtung und nicht als Zielarchitektur gezeigt werden.

## Bewertungsideen

Eine Bewertung kann mit einem einfachen Raster erfolgen. Gewichtung je nach Unterrichtsziel:

- Fachfunktion: Bestands- und Preisänderungen werden korrekt protokolliert.
- Historieneintrag: Zeitpunkt, Produkt, Änderungsart, Grund, alter Wert und neuer Wert sind vorhanden.
- Anzeige und Persistenz: Historie ist sichtbar, als CSV speicherbar und wieder ladbar.
- Struktur: Fachlogik, Persistenz und Ablaufsteuerung sind erkennbar getrennt.
- Tests: mindestens 3 fachliche JUnit-Tests prüfen zentrale Logik.
- Lesbarkeit: Klassen, Methoden und Packages sind verständlich benannt.
- Reflexion: Verantwortlichkeiten und Entscheidungen werden konkret begründet.

Bewertungsideen sollen nicht dazu führen, dass alle Lösungen gleich aussehen. Der Projektcharakter bleibt wichtig.

## Mindeststandard für erfüllt

Der Pflichtteil ist grundsätzlich erfüllt, wenn diese Punkte nachvollziehbar vorhanden sind:

- Bestandsänderungen und Preisänderungen werden protokolliert.
- Jeder Historieneintrag enthält Zeitpunkt, Produkt, Änderungsart, Grund, alten Wert und neuen Wert.
- Negative Preise und negative Bestände werden nicht als gültige Änderung protokolliert.
- Die Historie kann angezeigt, als CSV gespeichert und wieder aus CSV geladen werden.
- Die Fachlogik der Historie ist nicht vollständig in `Main`.
- Mindestens 3 fachliche JUnit-Tests prüfen Bestandsänderung, Preisänderung und Pflichtdaten oder ungültige Änderungen.
- Die Lernenden können kurz begründen, welche Klasse welche Verantwortung hat.

Optionale Filter, Statistiken oder zusätzliche Exportdateien sollten erst bewertet werden, wenn dieser Mindeststandard stabil ist.

## Mögliche Lösungsrichtungen

Keine vollständige Musterlösung bereitstellen.

Mögliche Bausteine:

- ein Eintrag für Änderungen, zum Beispiel `AenderungsEintrag`
- getrennte Einträge für Preis- und Bestandsänderungen, wenn gut begründet
- ein Journal, das mehrere Einträge sammelt
- ein Service, der fachliche Protokollierung bündelt
- eine CSV-Klasse, die Historieneinträge speichert und lädt
- Erweiterungen im bestehenden `LagerService`, wenn die Klasse dadurch nicht überladen wird
- JUnit-Tests für Preisänderung, Bestandsänderung und ungültige Änderung

Diese Bausteine sind keine Zielarchitektur. Sie dienen als Gesprächsgrundlage.

## Hinweise auf Architekturentscheidungen

Wichtige Architekturfragen für die Nachbesprechung:

- Ist die Historie Teil der Fachlogik oder der Persistenz?
- Wo entsteht der Historieneintrag?
- Wer kennt das CSV-Format der Historie und kann es wieder einlesen?
- Bleibt `Produkt` ein Datenobjekt oder bekommt es zu viele Aufgaben?
- Wird `LagerService` erweitert oder entsteht ein eigener `JournalService`?
- Ist ein eigener Service hilfreich oder wird die Struktur dadurch unnötig kompliziert?
- Sind Interfaces sinnvoll eingesetzt oder nur aus Gewohnheit ergänzt?
- Kann die zentrale Fachlogik ohne echte Datei getestet werden?

Nicht verlangen:

- Datenbank
- Spring
- REST-API
- GUI
- externe Libraries ausser JUnit
- vollständiges Repository-Pattern
- starre Zielarchitektur

## Bezug zur Lernenden-Version

Die [Lernenden-Version](../Lernende/Projektauftrag_Aenderungshistorie_Lagerverwaltung.md) enthält den offenen Projektauftrag mit Ausgangslage, Ziel, technischem Rahmen, Pflichtanforderungen, optionalen Erweiterungen, Qualitätsanforderungen, Testanforderungen, Abgabe und Reflexionsfragen.

Diese Lehrpersonen-Version ergänzt:

- didaktischen Zweck
- diagnostische Beobachtungspunkte
- typische Schwierigkeiten
- mögliche Hilfestellungen
- Bewertungsideen
- Mindeststandard für erfüllt
- mögliche Lösungsrichtungen ohne vollständige Musterlösung
- Hinweise auf Architekturentscheidungen
