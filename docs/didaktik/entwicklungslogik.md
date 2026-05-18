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
-> CSV-Persistenz
-> Verantwortlichkeiten
-> Interfaces
-> Polymorphie
-> Wiederverwendung
-> Vererbung
-> Services
-> Projekte
-> Projekt-Review
-> Architektur-Festigung
-> relationale Datenbank mit JDBC/H2
-> austauschbare Persistenz
-> Mapping zwischen Objekten und Datenbank
-> mehrere Tabellen und Beziehungen
-> Repository als strukturierter Datenzugriff
-> technisches Logging als Beobachtbarkeit
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

Die Persistenz bleibt danach nicht stehen. Sie wächst schrittweise: zuerst CSV-Laden und CSV-Speichern, danach alternative Speicherklassen, später JDBC mit H2 und schliesslich mehrere Tabellen mit eigenem Mapping. So entsteht Architektur aus konkretem Wachstum statt aus abstrakter Theorie.

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

## Anschluss: erste relationale Datenbank

Nach CSV-Persistenz, Verantwortlichkeiten, Interfaces und Services kann eine erste Datenbank sinnvoll eingeführt werden. Die Datenbank erscheint nicht als komplett neue Architektur, sondern als weitere Persistenzform.

Die bekannte Idee bleibt erhalten:

```text
ProduktSpeicher
├── CsvProduktSpeicher
└── DbProduktSpeicher
```

So wird sichtbar, dass Persistenz austauschbar ist. JDBC und H2 führen eine neue Technik ein, aber die Fachlogik bleibt weiterhin im Service und die Ablaufsteuerung bleibt in `Main`.

`DbProduktSpeicher` wird deshalb nicht als Bruch verstanden, sondern als alternative Implementierung zu `CsvProduktSpeicher`. H2 und JDBC erweitern die bestehende Persistenzidee: dieselbe Lagerverwaltung kann Daten nun in einer Datenbank statt in einer Datei speichern. Fachlogik, Services und die grobe Ablaufsteuerung sollen dabei möglichst stabil bleiben.

Die Anwendung wächst evolutionär. Zuerst gibt es eine Tabelle `PRODUKT`, dann zusätzliche Änderungsdaten, danach Mapping zwischen Fachobjekten und Tabellen und schliesslich mehrere zusammenhängende Tabellen. Jede Erweiterung macht eine neue Strukturfrage sichtbar, bevor ein neuer Begriff eingeführt wird.

Der Einstieg bleibt bewusst klein:

- H2 als eingebettete Datenbank
- JDBC mit `Connection`, `PreparedStatement` und `ResultSet`
- einfache SQL-Befehle wie `CREATE TABLE`, `INSERT`, `SELECT`, `UPDATE` und `DELETE`
- kurzer Vergleich zwischen Embedded- und Server-Modus

## Persistenzarchitektur und evolutionäre Erweiterung

Nach CSV wird Persistenz schrittweise komplexer. Eine einzelne Datei oder eine einzelne Speicherklasse reicht für einfache Produktdaten aus. Sobald aber weitere fachliche Daten dazukommen, zum Beispiel Preisänderungen oder Bestandsänderungen, wächst auch der Code für Laden, Speichern und Mapping.

Alternative Persistenzimplementierungen helfen, weil die Fachlogik nicht wissen muss, ob Daten aus CSV oder aus H2 kommen. Ein gemeinsamer Vertrag wie `ProduktSpeicher` macht sichtbar: Die Anwendung kann dieselbe fachliche Arbeit erledigen, obwohl die technische Speicherung unterschiedlich ist.

Mit einer Datenbank entsteht zusätzlich Mapping. Java-Objekte liegen nicht direkt in Tabellen. Werte aus einem `ResultSet` müssen zu Fachobjekten werden, und Objektwerte müssen in ein `PreparedStatement` eingesetzt werden. Dieses Mapping ist keine Fachregel, sondern eine eigene Persistenzverantwortung.

Mehrere Tabellen erzeugen neue Strukturfragen. Ein Produkt, Preisänderungen und Bestandsänderungen gehören fachlich zusammen, liegen aber in verschiedenen Tabellen. Beziehungen wie `PRODUKT_ID` müssen im Code nachvollziehbar geladen, gespeichert und gemappt werden.

Repositorys werden deshalb als einfache Persistenzklassen eingeführt. In dieser Reihe bedeutet Repository nicht Enterprise-Pattern, sondern: ein strukturierter Ort für Datenzugriff und Mapping in einem fachlichen Bereich. Ein `ProduktRepository` kennt Produktdaten, ein `AenderungsRepository` kennt Änderungsdaten. Die Fachlogik bleibt im Service.

## Technische Beobachtbarkeit durch Logging

Nach JDBC/H2, Mapping, mehreren Tabellen und Repositorys passiert in der bekannten Lagerverwaltung genug technische Arbeit im Hintergrund, dass einfache Konsolenausgaben nicht mehr ausreichen. Technisches Logging wird deshalb erst jetzt eingeführt: Die Lernenden haben konkrete Abläufe, die sie beobachten müssen.

Logging macht sichtbar, welche Repository-Methode arbeitet, welche JDBC-Aktion vorbereitet wird und welcher Fehler technisch aufgetreten ist. Es bleibt aber Beobachtbarkeit. Fachregeln bleiben im Service und Tests bleiben die Prüfung des erwarteten Verhaltens.

Der Einstieg bleibt bewusst klein:

- SLF4J als Logging-Schnittstelle
- Logback als konkrete Ausgabe-Umsetzung
- Logger pro Klasse
- Log-Level `DEBUG`, `INFO`, `WARN` und `ERROR`
- Logging in Repository-Klassen bei Datenzugriff und Fehlerfällen

## Architekturbegriffe aus echten Problemen

Neue Architekturbegriffe werden nicht abstrakt vorangestellt. Zuerst entsteht ein konkretes Problem im Code, danach erhält die passende Struktur einen Namen. So bleibt der Begriff an Erfahrung gebunden.

Beispiele:

- Ein Interface wird sinnvoll, wenn mehrere austauschbare Persistenzimplementierungen entstehen.
- Ein Service wird sinnvoll, wenn Fachlogik sonst in `Main` oder in Speicherklassen verteilt wird.
- Vererbung wird sinnvoll diskutiert, wenn doppelter oder sehr ähnlicher Code sichtbar wird.
- Ein Repository wird sinnvoll, wenn JDBC- und Mapping-Code durch mehrere Tabellen wächst.

Damit lernen die Lernenden Architektur nicht als Sammlung grosser Begriffe, sondern als Werkzeug zur Lösung konkreter Strukturprobleme.

## Bewusste Nicht-Ziele

Für den Datenbank- und Repository-Einstieg werden bewusst nicht eingeführt:

- kein Spring
- keine Dependency Injection
- kein ORM
- kein Hibernate
- kein JPA
- kein Spring Data Repository
- kein generisches Repository
- keine automatische Query-Generierung
- kein formales Repository Pattern
- keine komplexe Clean Architecture
- keine komplexen Frameworks
- keine zu frühe REST-API

Repository wird nur einfach als strukturierter Datenzugriff eingeführt: JDBC-Code, SQL-Anweisungen und Mapping werden an einem nachvollziehbaren Ort gebündelt. Es geht nicht um Framework-Magie, automatische Persistenz oder Enterprise-Architektur.

Der Fokus bleibt auf EFZ-Niveau: kleine Java-Programme, klare Verantwortlichkeiten, einfache Tests und nachvollziehbare Strukturentscheidungen.
