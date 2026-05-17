# Didaktische Entwicklungslogik

Diese Datei beschreibt den roten Faden der Unterrichtsreihe. Sie erklärt, warum die Themen nicht isoliert stehen, sondern schrittweise aufeinander aufbauen.

## Roter Faden

Die Reihe entwickelt sich von kleinen Java-Grundlagen zu strukturierter Softwareentwicklung:

```text
Grundlagen
-> Datenstrukturen
-> OOP
-> Maven
-> Tests
-> Refactoring
-> Persistenz
-> Verantwortlichkeiten
-> Interfaces
-> Polymorphie
-> Wiederverwendung
-> Vererbung
-> Services
-> Projekte
-> Projekt-Review
-> Architektur-Festigung
```

## Grundlagen und Datenstrukturen

Am Anfang stehen primitive Datentypen, Wrapper, `String`, `StringBuilder`, Arrays, 2D-Arrays und Methoden. Diese Themen schaffen Sprachsicherheit: Lernende sollen Werte, Objekte, Schleifen, Bedingungen, Rückgabewerte und einfache Auswertungen sicher lesen und schreiben können.

Datenstrukturen kommen früh, weil spätere Programme fast immer mehrere Werte oder mehrere Objekte verwalten. Such-, Zähl-, Maximum- und Sortieraufgaben zeigen, wie wiederkehrende Muster entstehen. Diese Muster werden später in Methoden, Klassen und Services wiederverwendet.

## OOP, Maven, Tests und Refactoring

OOP folgt, sobald einfache Abläufe und Datenstrukturen verstanden sind. Klassen, Objekte, Kapselung, Getter, Setter, Objektarrays und `ArrayList` machen sichtbar, dass Programme nicht nur aus einzelnen Anweisungen bestehen, sondern aus zusammenarbeitenden Objekten.

Maven wird eingeführt, wenn mehrere Dateien, Packages und Build-Schritte nicht mehr sinnvoll von Hand verwaltet werden sollen. Maven ersetzt Java nicht, sondern macht Kompilieren, Testen und Paketieren reproduzierbar.

Tests kommen danach, weil Fachlogik nun in Methoden und Klassen liegt. Erst dadurch können erwartete und tatsächliche Resultate sinnvoll automatisiert geprüft werden. Refactoring baut darauf auf: Struktur darf verbessert werden, solange die Tests zeigen, dass das Verhalten gleich bleibt.

## Persistenz vor grösserer Architektur

Persistenz wird bewusst vor grösseren Architekturthemen eingeführt. CSV-Dateien sind konkret, sichtbar und für Lernende nachvollziehbar. Sie zeigen, dass Daten im Arbeitsspeicher temporär sind und erst durch Speichern dauerhaft werden.

Dadurch entsteht ein echtes Strukturproblem: Laden, Speichern, Fachlogik und Ablaufsteuerung sollen nicht alle in `Main` landen. Persistenz macht Verantwortlichkeiten praktisch notwendig, ohne bereits Datenbanken, Frameworks oder komplexe Architekturmodelle einzuführen.

## Verantwortlichkeiten bis Services

Nach der Persistenz wird die Struktur schrittweise präziser:

- Verantwortlichkeiten trennen `Main`, Datenobjekte, Fachlogik und Dateilogik.
- Interfaces führen einen Vertrag ein, ohne sofort viele Abstraktionen zu verlangen.
- Polymorphie zeigt praktisch, dass derselbe Interface-Typ unterschiedliche konkrete Objekte verwenden kann.
- Wiederverwendung macht doppelte oder sehr ähnliche Logik sichtbar.
- Vererbung wird vorsichtig aus einem echten Wiederverwendungsproblem heraus eingeführt.
- Services bündeln Fachlogik, damit `Main` klein bleibt und Persistenz getrennt bleibt.

Diese Reihenfolge vermeidet zu frühe Architekturbegriffe. Lernende sehen zuerst konkrete Probleme im Code und erst danach eine passende Strukturidee.

## Projektarbeit und Projekt-Review

Projektarbeit wird erst nach diesen Grundlagen sinnvoll, weil ein Projekt mehrere Konzepte gleichzeitig verlangt: Daten modellieren, Sammlungen verwalten, Methoden schreiben, testen, speichern, Verantwortlichkeiten trennen und Code schrittweise verbessern.

Das Projekt-Review folgt darauf, weil die Qualität nicht nur am Ergebnis sichtbar wird. Im Review können Lernende erklären, warum Klassen existieren, wo Fachlogik liegt, wie Tests eingesetzt wurden und welche Strukturentscheidungen noch verbessert werden könnten.

## Warum jetzt eine Festigungsphase folgt

Nach den Services sind viele wichtige Strukturideen eingeführt. Genau deshalb ist eine Festigungsphase sinnvoll. Die Lernenden kennen nun viele Begriffe, müssen sie aber in konkretem Code sicher unterscheiden:

- Was gehört in `Main`?
- Was gehört in ein Datenobjekt?
- Was ist Fachlogik?
- Was ist Persistenz?
- Was ist ein Interface-Vertrag?
- Was ist eine konkrete Implementierung?
- Wann hilft ein Service?
- Wann wird eine Struktur zu kompliziert?

Die Architektur-Festigung soll keine neue grosse Theorie einführen. Sie soll sichtbar machen, ob Verantwortlichkeiten, Persistenz, Interfaces und Services in einer bekannten Lagerverwaltung wirklich verstanden wurden.

## Bewusste Nicht-Ziele

Für den aktuellen Stand werden bewusst nicht eingeführt:

- keine Datenbank
- kein Spring
- keine Dependency Injection
- kein formales Repository Pattern
- keine Clean Architecture
- keine komplexen Frameworks
- keine zu frühe REST-API

Der Fokus bleibt auf EFZ-Niveau: kleine Java-Programme, klare Verantwortlichkeiten, einfache Tests und nachvollziehbare Strukturentscheidungen.
