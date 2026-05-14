# Lerninhalte

Diese Übersicht listet die vorhandenen Lerninhalte des Repositories nach Materialtyp und Thema. Sie dient als Orientierung für Unterrichtsplanung, Wiederholung und Weiterentwicklung der Unterlagen.

## Begleitende Prozess- und Begriffsbibliothek

Diese Dateien unterstützen die KI-gestützte Erstellung und Prüfung von Lehrmitteln. Die verbindlichen Regeln bleiben in [AGENTS.md](./AGENTS.md).

### Begriffe

- [Orchestrierung](./docs/begriffe/orchestrierung.md)
  - kurze Erklärung für koordinierte Build- und Werkzeugabläufe
- [Convention over Configuration](./docs/begriffe/convention_over_configuration.md)
  - Maven-Konventionen wie `src/main/java` verständlich erklärt
- [Build-Artefakt](./docs/begriffe/build_artifact.md)
  - erzeugte Dateien wie `.class`-Dateien und Build-Ordner
- [Classpath](./docs/begriffe/classpath.md)
  - Suchort für kompilierte Klassen beim Starten mit `java`
- [Package vs. Verzeichnis](./docs/begriffe/package_vs_directory.md)
  - Zusammenhang zwischen Java-Package und Ordnerstruktur

### Prozesse

- [Arbeitsblatt erstellen](./docs/prozesse/arbeitsblatt_erstellen.md)
  - Checkliste für lernzielorientierte Arbeitsblätter
- [Übungen erstellen](./docs/prozesse/uebungen_erstellen.md)
  - Checkliste für klare, gestaffelte Übungsaufträge
- [Repetition und Vertiefung erstellen](./docs/prozesse/repetition_und_vertiefung_erstellen.md)
  - Checkliste für diagnostisch nutzbare Repetitions- und Vertiefungsübungen
- [Musterlösungen erstellen](./docs/prozesse/musterloesungen_erstellen.md)
  - Checkliste für kompakte Referenzlösungen
- [Review Didaktik](./docs/prozesse/review_didaktik.md)
  - Prüfpunkte für EFZ-Niveau, Lernprogression und Verständlichkeit
- [Review Java und Maven](./docs/prozesse/review_java_maven.md)
  - Prüfpunkte für Java-, Package-, Classpath- und Maven-Korrektheit

### Repo-Skills

- [arbeitsblatt-erstellen](./.agents/skills/arbeitsblatt-erstellen/SKILL.md)
  - unterstützt das Erstellen oder gezielte Überarbeiten von Arbeitsblättern
- [uebungen-erstellen](./.agents/skills/uebungen-erstellen/SKILL.md)
  - unterstützt klare, gestaffelte und prüfbare Übungsaufträge
- [repetition-vertiefung-erstellen](./.agents/skills/repetition-vertiefung-erstellen/SKILL.md)
  - unterstützt kurze, diagnostische Repetitions- und Vertiefungsübungen
- [musterloesungen-erstellen](./.agents/skills/musterloesungen-erstellen/SKILL.md)
  - unterstützt kompakte, fachlich korrekte Musterlösungen
- [svg-pruefen](./.agents/skills/svg-pruefen/SKILL.md)
  - unterstützt die Prüfung von SVG-Grafiken auf XML, Lesbarkeit und Einbindung
- [java-maven-validieren](./.agents/skills/java-maven-validieren/SKILL.md)
  - unterstützt die technische Prüfung von Java-, Package-, Classpath- und Maven-Beispielen
- [git-repo-updaten](./.agents/skills/git-repo-updaten/SKILL.md)
  - kontrollierter Git-Abschluss nur bei ausdrücklichem Benutzerauftrag

Hinweis: `.codex/skills` ist eine veraltete Skill-Ablage. Die aktuellen Repo-Skills liegen unter `.agents/skills`.

## Empfohlene Unterrichtsreihenfolge

Diese Reihenfolge erfasst die bisher aufgebauten Konzepte und Übungen. Die Einträge bilden die bisher vorbereitete Unterrichtssequenz.

### 1. Primitive Datentypen, Wrapper und Parsing

Ziel: Unterschied zwischen primitiven Werten und Wrapper-Objekten verstehen, typische Fehler mit `null`, Vergleich und Parsing erkennen.

Material:

- [Tag 1 – Primitive Datentypen & Wrapper](./Arbeitsblaetter/arbeitsblatt_java_wrapper.md)
- [Tag 1 – Primitive Datentypen & Wrapper, String und Visualisierungen](./Arbeitsblaetter/arbeitsblatt_theorie_kombiniert.md)
- [Primitive Werte vs. Wrapper-Objekte](./graphics/java_wert_vs_objekt_wrapper.svg)
- [Theorie – Wrapper-Klassen](./Uebungen/theorie_wrapper.md)
- [Übungen – Primitive Datentypen & Wrapper](./Uebungen/uebungen_java_wrapper.md)

### 2. String-Grundlagen

Ziel: `String` als Objekt nutzen, Vergleiche korrekt durchführen, wichtige Methoden anwenden und Immutability verstehen.

Material:

- [Tag 2 – String-Klasse](./Arbeitsblaetter/string_arbeitsblatt.md)
- [Theorie – String](./Uebungen/theorie_string.md)
- [Übungen – String-Klasse](./Uebungen/string_uebungen.md)
- [String-Immutability](./Arbeitsblaetter/arbeitsblatt_grafiken/tag5_konzept_immutability_string.svg)

### 3. String-Vertiefung und einfache Textverarbeitung

Ziel: String-Methoden kombinieren, Teilstrings extrahieren, Inhalte prüfen, ersetzen und einfache Eingaben validieren.

Material:

- [Tag 3 – String-Klasse, Vertiefung](./Arbeitsblaetter/string_arbeitsblatt_v2.md)
- [Übungen – String-Klasse, Vertiefung](./Uebungen/string_uebungen_v2.md)

### 4. Mini-Projekt Parser

Ziel: String-Verarbeitung in einem kleinen zusammenhängenden Auftrag anwenden und erste Parser-Ideen üben.

Material:

- [Parser-Grafik](./graphics/parser_grafik.svg)
- [Tag 4 – String-Klasse, Mini-Projekt Parser](./Uebungen/string_mini_projekt_v3.md)
- [Tag 4 – String-Klasse, Mini-Projekt Parser erweitert](./Uebungen/string_mini_projekt_v3_updated.md)
- [Musterlösungen – Mini-Projekt String Parser](./Musterloesungen/string_parser_loesungen.md)

### 5. StringBuilder

Ziel: Unterschied zwischen unveränderbarem `String` und veränderbarem `StringBuilder` verstehen und typische Operationen anwenden.

Material:

- [Arbeitsblatt – Strings & StringBuilder](./Arbeitsblaetter/arbeitsblatt_stringbuilder.md)
- [Tag 5 – StringBuilder](./Arbeitsblaetter/tag5_stringbuilder_arbeitsblatt.md)
- [Tag 5 – StringBuilder mit eingebetteten Grafiken](./Arbeitsblaetter/arbeitsblatt_grafiken/tag5_stringbuilder_arbeitsblatt.md)
- [String-Verkettung mit Plus](./Arbeitsblaetter/arbeitsblatt_grafiken/tag5_prozess_string_verketten_plus.svg)
- [String vs. StringBuilder](./Arbeitsblaetter/arbeitsblatt_grafiken/tag5_vergleich_string_vs_stringbuilder.svg)
- [Übungen – StringBuilder & Parser](./Uebungen/uebungen_stringbuilder.md)
- [Musterlösungen – StringBuilder & Parser](./Musterloesungen/musterloesungen_stringbuilder.md)

### 6. Arrays

Ziel: Arrays anlegen, Werte über Indizes lesen und typische Schleifenmuster wie Summe, Maximum, Zählen und Suche anwenden.

Material:

- [Arbeitsblatt – Arrays](./Arbeitsblaetter/Arbeitsblatt_Arrays.md)
- [Arrays – Konzept](./graphics/grafik_arrays_konzept.svg)
- [Arrays – Konzept mit Beispiel](./graphics/grafik_arrays_konzept_beispiel.svg)
- [Übungen – Arrays](./Uebungen/Uebungen_Arrays.md)
- [Lösungen – Arrays](./Musterloesungen/Loesungen_Arrays.md)
- [Lösungen – Arrays im Stil](./Musterloesungen/Loesungen_Arrays_im_Stil.md)

### 7. Arrays vertiefen

Ziel: bekannte Array-Muster variieren, kombinieren und Edge Cases bewusst behandeln.

Material:

- [Arbeitsblatt – Arrays, Vertiefung](./Arbeitsblaetter/Arbeitsblatt_Arrays_Vertiefung.md)
- [Übungen – Arrays, Vertiefung](./Uebungen/Uebungen_Arrays_Vertiefung.md)

### 8. 2D-Arrays

Ziel: 2D-Arrays als Tabellen verstehen, Zeilen auswerten und unterschiedliche Zeilenlängen sowie leere Zeilen berücksichtigen.

Material:

- [Arbeitsblatt – Arrays 2D, Vertiefung](./Arbeitsblaetter/Arbeitsblatt_2D_Arrays_Vertiefung.md)
- [Übungen – 2D Arrays, Vertiefung](./Uebungen/Uebungen_2D_Arrays.md)
- [Lösungen – 2D Arrays](./Musterloesungen/Loesungen_2D_Arrays.md)

### 9. Methoden

Ziel: Methoden mit Parametern, Rückgabewerten und `void` schreiben und bekannte Array-Auswertungen in Methoden auslagern.

Material:

- [Arbeitsblatt – Methoden in Java](./Arbeitsblaetter/Arbeitsblatt_Methoden.md)
- [Übungen – Methoden in Java](./Uebungen/Uebungen_Methoden.md)
- [Lösungen – Methoden in Java](./Musterloesungen/Loesungen_Methoden.md)

### 10. Methoden festigen und Refactoring

Ziel: bestehenden Code gezielt umbauen, Methodennamen bewusst wählen, einfache Testausgaben formulieren und `main` übersichtlich halten.

Material:

- [Arbeitsblatt – Methoden festigen und Refactoring](./Arbeitsblaetter/Arbeitsblatt_Methoden_Festigung.md)
- [Übungen – Methoden festigen und Refactoring](./Uebungen/Uebungen_Methoden_Festigung.md)
- [Lösungen – Methoden festigen und Refactoring](./Musterloesungen/Loesungen_Methoden_Festigung.md)

### 11. Klassen und Objekte

Ziel: Klasse und Objekt unterscheiden, Attribute, Methoden und Konstruktoren verwenden und einfache Objektarrays auswerten.

Material:

- [Arbeitsblatt – Klassen und Objekte](./Arbeitsblaetter/Arbeitsblatt_Klassen_und_Objekte.md)
- [Java: Klasse und Objekt](./graphics/java_klasse_objekt_konzept.svg)
- [Java: Variable und Objekt-Referenz](./graphics/java_objekt_referenz.svg)
- [Übungen – Klassen und Objekte](./Uebungen/Uebungen_Klassen_und_Objekte.md)
- [Lösungen – Klassen und Objekte](./Musterloesungen/Loesungen_Klassen_und_Objekte.md)

### 12. Kapselung, Getter und Setter

Ziel: Attribute schützen, kontrollierten Zugriff über Getter und Setter verwenden und einfache Validierung einbauen.

Material:

- [Arbeitsblatt – Kapselung, Getter und Setter](./Arbeitsblaetter/Arbeitsblatt_Kapselung_Getter_Setter.md)
- [Java: Kapselung mit private](./graphics/java_kapselung_private.svg)
- [Java: Getter, Setter und Validierung](./graphics/java_getter_setter_validierung.svg)
- [Übungen – Kapselung, Getter und Setter](./Uebungen/Uebungen_Kapselung_Getter_Setter.md)
- [Lösungen – Kapselung, Getter und Setter](./Musterloesungen/Loesungen_Kapselung_Getter_Setter.md)

### 13. Objektarrays und Verwaltungslogik

Ziel: Mehrere gekapselte Objekte in Arrays verwalten, suchen, zählen, auswerten und kontrolliert verändern.

Material:

- [Arbeitsblatt – Objektarrays und Verwaltungslogik](./Arbeitsblaetter/Arbeitsblatt_Objektarrays_Verwaltungslogik.md)
- [Übungen – Objektarrays und Verwaltungslogik](./Uebungen/Uebungen_Objektarrays_Verwaltungslogik.md)
- [Lösungen – Objektarrays und Verwaltungslogik](./Musterloesungen/Loesungen_Objektarrays_Verwaltungslogik.md)

### 14. ArrayList

Ziel: Eine dynamische Sammlung verwenden und bekannte Verwaltungslogik von Arrays auf `ArrayList` übertragen.

Material:

- [Arbeitsblatt – ArrayList in Java](./Arbeitsblaetter/Arbeitsblatt_ArrayList.md)
- [Übungen – ArrayList](./Uebungen/Uebungen_ArrayList.md)
- [Lösungen – ArrayList](./Musterloesungen/Loesungen_ArrayList.md)

### 15. Repetition Java Intro

Ziel: Klassen und Objekte, Kapselung, `ArrayList` und Methoden in vielen kleinen Aufgaben kombinieren und diagnostisch sichtbar machen, ob die Grundlagen verinnerlicht wurden.

Material:

- [Repetition Java Intro – Lernenden-Version](./Repetitionen/Repetition_Java_Intro/Lernende/Repetition_Java_Intro.md)
- [Repetition Java Intro – Lehrpersonen-Version](./Repetitionen/Repetition_Java_Intro/Lehrperson/Repetition_Java_Intro_LP.md)

### 16. Java-Packages

Ziel: Mehrere Java-Klassen mit Packages strukturieren, Package-Namen nach umgekehrter Domain-Konvention verwenden und ohne Maven sauber nach `out` kompilieren.

Material:

- [Arbeitsblatt – Java-Packages](./Arbeitsblaetter/Arbeitsblatt_Packages.md)
- [Übungen – Java-Packages](./Uebungen/Uebungen_Packages.md)
- [Lösungen – Java-Packages](./Musterloesungen/Loesungen_Packages.md)

### 17. Algorithmen und Datenstrukturen

Ziel: Einfache Algorithmen auf Arrays verstehen, lineare Suche, Minimum, Maximum und Zählen anwenden, Bubble Sort und Selection Sort mit `int[]` nachvollziehen sowie einfache Simulationen mit Schleifen umsetzen.

Material:

- [Arbeitsblatt – Algorithmen und Datenstrukturen](./Arbeitsblaetter/Arbeitsblatt_Algorithmen_Datenstrukturen.md)
- [Arbeitsblatt – Sortieralgorithmen](./Arbeitsblaetter/Arbeitsblatt_Sortieralgorithmen.md)
- [Übungen – Algorithmen und Datenstrukturen](./Uebungen/Uebungen_Algorithmen_Datenstrukturen.md)
- [Lösungen – Algorithmen und Datenstrukturen](./Musterloesungen/Loesungen_Algorithmen_Datenstrukturen.md)

### 18. Maven Einstieg

Ziel: Maven als orchestrierendes Build-Tool verstehen, den bekannten manuellen Build-Prozess mit `javac -d out` und `java -cp out` mit `mvn compile`, `mvn clean`, `src/main/java` und `target` vergleichen sowie `Convention over Configuration` praktisch anwenden.

Material:

- [Arbeitsblatt – Maven Einstieg](./Arbeitsblaetter/Arbeitsblatt_Maven_Einstieg.md)
- [Maven orchestriert den Java-Build](./graphics/maven_orchestriert_build.svg)
- [Übungen – Maven Einstieg](./Uebungen/Uebungen_Maven_Einstieg.md)
- [Lösungen – Maven Einstieg](./Musterloesungen/Loesungen_Maven_Einstieg.md)

### 19. Maven-Projekte ausführen und paketieren

Ziel: `compile`, Programmstart und `package` unterscheiden, `target/classes` und einfache JAR-Dateien als Build-Ergebnisse einordnen, Java-`package` von Maven `package` trennen sowie reproduzierbare Builds als Grundlage für Build-Server und CI/CD vorbereiten.

Material:

- [Arbeitsblatt – Maven-Projekte ausführen und paketieren](./Arbeitsblaetter/Arbeitsblatt_Maven_Ausfuehren_und_Paketieren.md)
- [Maven compile, run und package](./graphics/maven_compile_run_package.svg)
- [Übungen – Maven-Projekte ausführen und paketieren](./Uebungen/Uebungen_Maven_Ausfuehren_und_Paketieren.md)
- [Lösungen – Maven-Projekte ausführen und paketieren](./Musterloesungen/Loesungen_Maven_Ausfuehren_und_Paketieren.md)

### 20. Maven-Projekte mit einfachen Tests vorbereiten

Ziel: Fachlogik von `main` trennen, kleine prüfbare Methoden mit klaren Rückgabewerten schreiben, erwartete und tatsächliche Resultate systematisch vergleichen und Edge Cases bewusst prüfen, ohne bereits JUnit, externe Dependencies oder Maven Central einzuführen.

Material:

- [Arbeitsblatt – Maven-Projekte mit einfachen Tests vorbereiten](./Arbeitsblaetter/Arbeitsblatt_Maven_Einfache_Tests_Vorbereiten.md)
- [Übungen – Maven-Projekte mit einfachen Tests vorbereiten](./Uebungen/Uebungen_Maven_Einfache_Tests_Vorbereiten.md)
- [Lösungen – Maven-Projekte mit einfachen Tests vorbereiten](./Musterloesungen/Loesungen_Maven_Einfache_Tests_Vorbereiten.md)

### 21. Von manuellen Tests zu automatisierten Tests mit JUnit

Ziel: Die bekannte Testidee aus erwarteten und tatsächlichen Resultaten mit JUnit Jupiter automatisieren, Testcode unter `src/test/java` vom Produktivcode trennen, die erste externe Maven-Dependency kontrolliert einführen und `mvn test` als standardisierten Testlauf nutzen.

Material:

- [Arbeitsblatt – Von manuellen Tests zu automatisierten Tests mit JUnit](./Arbeitsblaetter/Arbeitsblatt_JUnit_Einstieg.md)
- [JUnit: manuell zu automatisiert](./graphics/junit_manuell_zu_automatisiert.svg)
- [Übungen – Von manuellen Tests zu automatisierten Tests mit JUnit](./Uebungen/Uebungen_JUnit_Einstieg.md)
- [Lösungen – Von manuellen Tests zu automatisierten Tests mit JUnit](./Musterloesungen/Loesungen_JUnit_Einstieg.md)

### 22. Wenn automatisierte Tests fehlschlagen

Ziel: Fehlgeschlagene JUnit-Tests ruhig analysieren, `expected` und `actual` unterscheiden, Stacktraces grob einordnen, Fehler mit `mvn test` reproduzierbar prüfen, Edge Cases ergänzen und Regressionstests als Sicherheitsnetz verstehen.

Material:

- [Arbeitsblatt – Wenn automatisierte Tests fehlschlagen](./Arbeitsblaetter/Arbeitsblatt_JUnit_Fehleranalyse.md)
- [JUnit: Workflow bei fehlgeschlagenen Tests](./graphics/junit_test_fehlschlag_workflow.svg)
- [Übungen – Wenn automatisierte Tests fehlschlagen](./Uebungen/Uebungen_JUnit_Fehleranalyse.md)
- [Lösungen – Wenn automatisierte Tests fehlschlagen](./Musterloesungen/Loesungen_JUnit_Fehleranalyse.md)

### 23. Refactoring mit Tests absichern

Ziel: Bestehenden Code in kleinen Schritten verbessern, ohne das gewünschte Verhalten absichtlich zu ändern, und mit `mvn test` vor und nach jedem Refactoring prüfen, ob die bekannten Erwartungen weiterhin erfüllt sind.

Material:

- [Arbeitsblatt – Refactoring mit Tests absichern](./Arbeitsblaetter/Arbeitsblatt_Refactoring_mit_Tests.md)
- [Refactoring mit Tests absichern](./graphics/refactoring_mit_tests_workflow.svg)
- [Übungen – Refactoring mit Tests absichern](./Uebungen/Uebungen_Refactoring_mit_Tests.md)
- [Lösungen – Refactoring mit Tests absichern](./Musterloesungen/Loesungen_Refactoring_mit_Tests.md)

### 24. Produktdaten aus CSV-Dateien laden

Ziel: Einfache Persistenz mit CSV-Dateien verstehen, Produktdaten zeilenweise lesen, mit `split(";")` parsen, in `Produkt`-Objekte umwandeln und in einer `ArrayList` für die bekannte Produktverwaltung bereitstellen.

Material:

- [Arbeitsblatt – Produktdaten aus CSV-Dateien laden](./Arbeitsblaetter/Arbeitsblatt_CSV_Laden.md)
- [CSV-Daten in Java-Objekte umwandeln](./graphics/csv_laden_produktverwaltung.svg)
- [Übungen – Produktdaten aus CSV-Dateien laden](./Uebungen/Uebungen_CSV_Laden.md)
- [Lösungen – Produktdaten aus CSV-Dateien laden](./Musterloesungen/Loesungen_CSV_Laden.md)

### 25. Produktdaten als CSV-Dateien speichern

Ziel: Persistenz vervollständigen, `Produkt`-Objekte in CSV-Zeilen umwandeln, mehrere Produkte aus einer `ArrayList` in eine Datei schreiben und das Speicherformat durch erneutes Laden prüfen.

Material:

- [Arbeitsblatt – Produktdaten als CSV-Dateien speichern](./Arbeitsblaetter/Arbeitsblatt_CSV_Speichern.md)
- [Java-Objekte als CSV-Datei speichern](./graphics/csv_speichern_produktverwaltung.svg)
- [Übungen – Produktdaten als CSV-Dateien speichern](./Uebungen/Uebungen_CSV_Speichern.md)
- [Lösungen – Produktdaten als CSV-Dateien speichern](./Musterloesungen/Loesungen_CSV_Speichern.md)

### 26. Persistenzablauf vertiefen

Ziel: Laden, Bearbeiten, Speichern und erneutes Laden als vollständigen Persistenzablauf verstehen, Arbeitsspeicher und Datei unterscheiden, Änderungen bewusst speichern, Speicher- und Ladeformat prüfen sowie einfache Praxisfälle wie Backup, Export, Kopfzeile und Änderungsstatistik einordnen.

Material:

- [Arbeitsblatt – Persistenzablauf vertiefen](./Arbeitsblaetter/Arbeitsblatt_Persistenzablauf_Vertiefen.md)
- [Persistenzablauf: Laden, Bearbeiten, Speichern](./graphics/persistenzablauf_laden_bearbeiten_speichern.svg)
- [Übungen – Persistenzablauf vertiefen](./Uebungen/Uebungen_Persistenzablauf_Vertiefen.md)
- [Lösungen – Persistenzablauf vertiefen](./Musterloesungen/Loesungen_Persistenzablauf_Vertiefen.md)

### Nächster sinnvoller Block

Nach `Persistenzablauf vertiefen` bietet sich als nächstes Thema eine kompakte **Persistenz-Repetition oder einfache Architekturvorbereitung** an:

- vollständigen Lade-Bearbeiten-Speichern-Zyklus festigen
- Verantwortlichkeiten in `Main`, Fachlogik und Dateilogik wiederholen
- spätere Schichten-Ideen vorbereiten, ohne bereits formale Patterns einzuführen

## Geplante spätere Themenblöcke

Nach der aktuellen Testing-, Refactoring- und Persistenz-Sequenz sind folgende grössere Themenbereiche geplant.

### 1. Dateien und Persistenz

- CSV
- Laden und Speichern
- einfache Persistenz
- praxisnahe Datenhaltung ohne Datenbank

### 2. Vererbung und Interfaces

- Vererbung
- Polymorphie
- Interfaces
- gemeinsame Typen und austauschbare Implementierungen

### 3. Architektur und Schichten

- Trennung von Verantwortlichkeiten
- Service-Schicht
- Repository-Idee
- Testbarkeit durch bessere Struktur

### 4. REST und Client/Server

- HTTP-Grundlagen
- JSON
- REST-APIs
- Client/Server-Modell

Didaktische Begründung:

- zuerst greifbare Datenhaltung
- danach objektorientierte Erweiterung
- danach strukturelle Architektur
- danach REST/API als Anwendung der vorherigen Konzepte

## Arbeitsblätter

Arbeitsblätter führen neue Konzepte ein, enthalten kurze Theorie, Beispiele, typische Stolpersteine und Reflexionsfragen.

### Primitive Datentypen, Wrapper und Parsing

- [Tag 1 – Primitive Datentypen & Wrapper](./Arbeitsblaetter/arbeitsblatt_java_wrapper.md)
  - Primitive Datentypen vs. Wrapper-Klassen
  - Autoboxing und Autounboxing
  - `null` bei Wrapper-Objekten
  - `String` zu Zahl mit Parsing
  - Vergleich mit `==` und `equals()`
  - Sichere Eingabe und Fehlerbehandlung
- [Tag 1 – Primitive Datentypen & Wrapper, String und Visualisierungen](./Arbeitsblaetter/arbeitsblatt_theorie_kombiniert.md)
  - Kombinierte Theorie zu Wrapper-Klassen und `String`
  - Autoboxing, Autounboxing und Parsing
  - String-Grundlagen, Immutability, Methoden und Vergleich
  - Einbindung von Konzeptgrafiken

### Strings

- [Tag 2 – String-Klasse](./Arbeitsblaetter/string_arbeitsblatt.md)
  - String-Grundlagen
  - String-Vergleich
  - Immutability
  - Wichtige Methoden
- [Tag 3 – String-Klasse, Vertiefung](./Arbeitsblaetter/string_arbeitsblatt_v2.md)
  - Kombination von String-Methoden
  - Teilstrings, Prüfung und Ersetzung
  - Vergleich als Wiederholung

### Strings und StringBuilder

- [Arbeitsblatt – Strings & StringBuilder](./Arbeitsblaetter/arbeitsblatt_stringbuilder.md)
  - Problem häufiger String-Verkettung
  - `StringBuilder` als veränderbare Alternative
  - Methoden wie `append()`, `insert()`, `delete()`, `replace()` und `reverse()`
- [Tag 5 – StringBuilder](./Arbeitsblaetter/tag5_stringbuilder_arbeitsblatt.md)
  - Konzeptgrafiken zu String-Verkettung und Immutability
  - Vergleich `String` und `StringBuilder`
  - Kurze Theorie und Übung
- [Tag 5 – StringBuilder mit eingebetteten Grafiken](./Arbeitsblaetter/arbeitsblatt_grafiken/tag5_stringbuilder_arbeitsblatt.md)
  - Variante im Grafik-Unterverzeichnis mit denselben Tag-5-Inhalten

### Arrays

- [Arbeitsblatt – Arrays](./Arbeitsblaetter/Arbeitsblatt_Arrays.md)
  - Zweck von Arrays
  - Index und Zugriff auf Elemente
  - Arrays mit Schleifen
  - Typische Fehler
- [Arbeitsblatt – Arrays, Vertiefung](./Arbeitsblaetter/Arbeitsblatt_Arrays_Vertiefung.md)
  - Muster beim Durchlaufen von Arrays
  - Maximum, Suche, Zählen und Kombinationen
  - Transferaufgaben und Reflexion
- [Arbeitsblatt – Arrays 2D, Vertiefung](./Arbeitsblaetter/Arbeitsblatt_2D_Arrays_Vertiefung.md)
  - 2D-Arrays als Tabelle
  - Zeilenweise Auswertung
  - Summe, Durchschnitt und Maximum
  - Edge Cases wie unterschiedliche Zeilenlängen und leere Zeilen

### Methoden

- [Arbeitsblatt – Methoden in Java](./Arbeitsblaetter/Arbeitsblatt_Methoden.md)
  - Methoden mit Parametern und Rückgabewerten
  - `void`, `return` und Methodenaufrufe
  - Array-Auswertungen in Methoden auslagern
  - typische Fehler und Edge Cases
- [Arbeitsblatt – Methoden festigen und Refactoring](./Arbeitsblaetter/Arbeitsblatt_Methoden_Festigung.md)
  - bestehenden Code in Methoden zerlegen
  - Methodennamen, Parameter und Rückgabewerte bewusst wählen
  - einfache Testausgaben mit erwarteten Resultaten
  - Refactoring von Array- und String-Auswertungen

### Klassen und Objekte

- [Arbeitsblatt – Klassen und Objekte](./Arbeitsblaetter/Arbeitsblatt_Klassen_und_Objekte.md)
  - Klasse und Objekt unterscheiden
  - Attribute, Methoden und Konstruktoren
  - `this` im Konstruktor
  - einfache Objekte erstellen und verwenden
- [Arbeitsblatt – Kapselung, Getter und Setter](./Arbeitsblaetter/Arbeitsblatt_Kapselung_Getter_Setter.md)
  - private Attribute
  - Getter und Setter
  - Validierung im Setter
  - bewusster Verzicht auf unnötige Setter
- [Arbeitsblatt – Objektarrays und Verwaltungslogik](./Arbeitsblaetter/Arbeitsblatt_Objektarrays_Verwaltungslogik.md)
  - Objektarrays erstellen und durchlaufen
  - Getter bei gekapselten Objekten verwenden
  - Such-, Zähl- und Maximum-Muster mit Objekten
  - einfache Verwaltungslogik ohne `ArrayList`
- [Arbeitsblatt – ArrayList in Java](./Arbeitsblaetter/Arbeitsblatt_ArrayList.md)
  - Unterschied zwischen Array und `ArrayList`
  - `add`, `get`, `set`, `remove` und `size`
  - Schleifen über `ArrayList`
  - Verwaltungslogik mit dynamischer Sammlung
- [Arbeitsblatt – Java-Packages](./Arbeitsblaetter/Arbeitsblatt_Packages.md)
  - Package-Konvention mit umgekehrter Domain
  - `package`-Deklaration und passende Ordnerstruktur
  - Imports für eigene Klassen und Standardbibliothek
  - Sichtbarkeit mit `public`, `private`, package-private und `protected` als Ausblick
  - Algorithmen in Hilfsklassen und Packages aufteilen
  - Pensionskassen-Simulation in `Main`, `simulation` und `service` strukturieren
  - Kompilieren nach `out` ohne Maven
- [Arbeitsblatt – Algorithmen und Datenstrukturen](./Arbeitsblaetter/Arbeitsblatt_Algorithmen_Datenstrukturen.md)
  - Algorithmus und Datenstruktur unterscheiden
  - lineare Suche, Minimum, Maximum und Zählen
  - wiederholte Berechnung wie Zinseszins
  - einfacher Aufwand, Simulationen und Randfälle
- [Arbeitsblatt – Sortieralgorithmen](./Arbeitsblaetter/Arbeitsblatt_Sortieralgorithmen.md)
  - Bubble Sort mit `int[]`
  - Selection Sort mit `int[]`
  - Vergleichen, Tauschen und Schleifengrenzen
- [Arbeitsblatt – Maven Einstieg](./Arbeitsblaetter/Arbeitsblatt_Maven_Einstieg.md)
  - Maven als orchestrierendes Build-Tool
  - Dirigent-/Orchester-Analogie für den Begriff orchestrieren
  - Prozessgrafik zu Quellcode, Maven, `javac`, `.class`-Dateien und `target/classes`
  - `Convention over Configuration` mit `src/main/java` und `target`
  - Vergleich von `src`, `out`, `javac -d out`, `java -cp out` mit `mvn compile` und `mvn clean`
  - typische Fehler bei Maven-Struktur, Arbeitsverzeichnis und `pom.xml`
- [Arbeitsblatt – Maven-Projekte ausführen und paketieren](./Arbeitsblaetter/Arbeitsblatt_Maven_Ausfuehren_und_Paketieren.md)
  - Unterschied zwischen `compile`, Programmstart und `package`
  - `target/classes` als Ort erzeugter `.class`-Dateien
  - einfache JAR-Datei als Build-Artefakt
  - Unterschied zwischen Java-`package` und Maven `package`
  - reproduzierbare und standardisierte Builds
  - kurzer Ausblick auf Build-Server, Jenkins und CI/CD ohne technische Tiefe
- [Arbeitsblatt – Maven-Projekte mit einfachen Tests vorbereiten](./Arbeitsblaetter/Arbeitsblatt_Maven_Einfache_Tests_Vorbereiten.md)
  - Unterschied zwischen manuellen Testausgaben und systematischer Prüfung
  - erwartetes Resultat und tatsächliches Resultat vergleichen
  - Fachlogik von `main` trennen
  - kleine prüfbare Methoden für Rabatt, Suche und Gesamtwert
  - Edge Cases bewusst prüfen
  - Prozessgrafik zur Trennung von `main`, Fachlogik und manueller Prüfung
  - Abgrenzung zu JUnit, Dependencies und Maven Central
- [Arbeitsblatt – Von manuellen Tests zu automatisierten Tests mit JUnit](./Arbeitsblaetter/Arbeitsblatt_JUnit_Einstieg.md)
  - JUnit Jupiter als Automatisierung bekannter manueller Prüfungen
  - `src/main/java` und `src/test/java` trennen
  - `@Test` und `assertEquals` einführen
  - erste externe Dependency mit `scope test` in `pom.xml`
  - `.m2`-Repository und Maven Central kurz einordnen
  - `mvn test` und `target/surefire-reports` als standardisierten Testlauf sichtbar machen
  - Regressionstest einfach erklären
  - Vergleichsgrafik von manueller Prüfung zu JUnit und `mvn test`
  - erster Download nach Maven Central und lokales `.m2` nur kurz erwähnen
- [Arbeitsblatt – Wenn automatisierte Tests fehlschlagen](./Arbeitsblaetter/Arbeitsblatt_JUnit_Fehleranalyse.md)
  - fehlgeschlagene Tests als hilfreiche Rückmeldung verstehen
  - `expected` und `actual` in `assertEquals`-Fehlermeldungen lesen
  - Stacktrace grob einordnen
  - `mvn test` bei fehlerhaften Tests und gestoppte Builds erklären
  - `target/surefire-reports` kurz sichtbar machen
  - Edge Cases und Regressionstests als Sicherheitsnetz nutzen
  - Abgrenzung zu TDD, Mocking, Coverage, Integrationstests und technischer CI/CD-Umsetzung
- [Arbeitsblatt – Refactoring mit Tests absichern](./Arbeitsblaetter/Arbeitsblatt_Refactoring_mit_Tests.md)
  - Refactoring als Strukturverbesserung bei gleichem Verhalten erklären
  - Tests vor und nach kleinen Änderungen mit `mvn test` ausführen
  - `main` von Fachlogik entlasten
  - lange Methoden aufteilen, Methodennamen verbessern und Duplikate reduzieren
  - Tests als Sicherheitsnetz gegen Regressionen nutzen
  - kurzer Ausblick auf spätere Service- und Repository-Ideen
- [Arbeitsblatt – Produktdaten aus CSV-Dateien laden](./Arbeitsblaetter/Arbeitsblatt_CSV_Laden.md)
  - Persistenz als dauerhafte Speicherung ausserhalb des Programms
  - CSV als einfache strukturierte Textdatei
  - Produktdaten mit `split(";")` und Parsing in Objekte umwandeln
  - Dateilogik und Fachlogik trennen
  - Prozessgrafik zur Umwandlung von CSV-Zeilen in `ArrayList<Produkt>`
- [Arbeitsblatt – Produktdaten als CSV-Dateien speichern](./Arbeitsblaetter/Arbeitsblatt_CSV_Speichern.md)
  - Persistenz um das Speichern ergänzen
  - Produktobjekte in CSV-Zeilen umwandeln
  - mehrere Produkte aus einer `ArrayList` in eine Datei schreiben
  - Überschreiben, leere Listen und einfache Fehlerfälle behandeln
  - Speicher- und Ladeformat durch erneutes Laden prüfen
  - Prozessgrafik zum Speichern von `ArrayList<Produkt>` als CSV-Datei
- [Arbeitsblatt – Persistenzablauf vertiefen](./Arbeitsblaetter/Arbeitsblatt_Persistenzablauf_Vertiefen.md)
  - Persistenz als Ablauf aus Laden, Bearbeiten, Speichern und erneutem Laden
  - Arbeitsspeicher und Datei als unterschiedliche Orte für Zustand
  - bewusste Speicherung von Änderungen
  - Speicher- und Ladeformat mit Kopfzeile `name;preis` vergleichen
  - Prozessgrafik zum vollständigen Ablauf mit Datei, Arbeitsspeicher, Fachlogik und Prüfung
  - Fehlerfälle, Backup, Export und Ausblick auf spätere Schichten-Themen

## Konzeptgrafiken

Konzeptgrafiken visualisieren Beziehungen, Abläufe und typische Denkmodelle. Sie ergänzen Arbeitsblätter und Theorieblätter.

### Allgemeine Unterrichtsgrafiken

- [Arrays – Konzept](./graphics/grafik_arrays_konzept.svg)
  - Array als zusammengehörige Reihe von Werten
  - Indexbasierter Zugriff
- [Arrays – Konzept mit Beispiel](./graphics/grafik_arrays_konzept_beispiel.svg)
  - Konkretes Beispiel für Werte, Indizes und Zugriff
- [Primitive Werte vs. Wrapper-Objekte](./graphics/java_wert_vs_objekt_wrapper.svg)
  - Unterschied zwischen Wert und Objekt
  - Grundlage für Wrapper-Klassen und `null`
- [Parser-Grafik](./graphics/parser_grafik.svg)
  - Verarbeitung eines Textes in einzelne Bestandteile
  - Bezug zu String- und Parser-Aufgaben
- [Java: Klasse und Objekt](./graphics/java_klasse_objekt_konzept.svg)
  - Klasse als Bauplan und Objekte als konkrete Exemplare
  - Attribute, Methoden, Konstruktor und `this`
- [Java: Variable und Objekt-Referenz](./graphics/java_objekt_referenz.svg)
  - Unterschied zwischen primitiver Variable und Objektvariable
  - Referenz auf Objekt und Objektzustand
- [Java: Kapselung mit private](./graphics/java_kapselung_private.svg)
  - private Attribute schützen den Objektzustand
  - Zugriff erfolgt kontrolliert über Methoden
- [Java: Getter, Setter und Validierung](./graphics/java_getter_setter_validierung.svg)
  - Getter lesen Attributwerte
  - Setter prüfen und ändern Attributwerte kontrolliert
- [Maven orchestriert den Java-Build](./graphics/maven_orchestriert_build.svg)
  - Quellcode unter `src/main/java`
  - Maven als Koordinator des Build-Ablaufs
  - `javac` als weiterhin verwendetes Werkzeug
  - erzeugte `.class`-Dateien unter `target/classes`
- [Maven compile, run und package](./graphics/maven_compile_run_package.svg)
  - `compile`, Programmstart und `package` als getrennte Schritte
  - `target/classes` als erzeugtes Build-Ergebnis
  - einfache JAR-Datei als Build-Artefakt
  - Unterschied zwischen Java-`package` und Maven `package`
- [Maven-Projekte mit einfachen Tests vorbereiten](./graphics/maven_tests_vorbereiten.svg)
  - Trennung von `main` und Fachlogik
  - Fachlogik mit klaren Eingaben und Rückgabewerten
  - manuelle Prüfung mit erwartetem und tatsächlichem Resultat
- [JUnit: manuell zu automatisiert](./graphics/junit_manuell_zu_automatisiert.svg)
  - JUnit automatisiert bekannte manuelle Prüfungen
  - Vergleich von Ausgabe plus menschlichem Vergleich mit `assertEquals`
  - `src/main/java`, `src/test/java` und `mvn test` als Testlauf
  - Fachlogik liegt nicht in `main`
- [JUnit: Workflow bei fehlgeschlagenen Tests](./graphics/junit_test_fehlschlag_workflow.svg)
  - roter Testlauf, Analyse und Korrektur als ruhiger Ablauf
  - `expected` und `actual` als zentrale Hinweise
  - erneuter grüner Testlauf nach der Korrektur
  - Tests als Sicherheitsnetz gegen Regressionen
- [Refactoring mit Tests absichern](./graphics/refactoring_mit_tests_workflow.svg)
  - `mvn test` vor und nach kleinen Refactoring-Schritten
  - Verhalten bleibt gleich, Struktur wird besser
  - Tests als Sicherheitsnetz gegen Regressionen
  - grüner Pfad zum nächsten kleinen Schritt, roter Pfad zur Korrektur
- [CSV-Daten in Java-Objekte umwandeln](./graphics/csv_laden_produktverwaltung.svg)
  - CSV-Datei, Zeile lesen, `split(";")`, Produkt erzeugen und `ArrayList<Produkt>`
  - Parsing als Verbindung zwischen Strings und Objekten
  - Trennung von Dateilogik und Fachlogik
  - einfache Fehlerfälle beim Laden
- [Java-Objekte als CSV-Datei speichern](./graphics/csv_speichern_produktverwaltung.svg)
  - `ArrayList<Produkt>`, Produktobjekte durchlaufen, CSV-Zeile erzeugen, Datei schreiben und CSV-Datei
  - String-Verarbeitung als Verbindung zwischen Objekten und Textdateien
  - Speicher- und Ladeformat müssen zusammenpassen
  - Trennung von Datei- und Fachlogik
- [Persistenzablauf: Laden, Bearbeiten, Speichern](./graphics/persistenzablauf_laden_bearbeiten_speichern.svg)
  - vollständiger Ablauf von CSV-Datei über Laden, `ArrayList<Produkt>`, Bearbeiten, Speichern und erneutes Laden
  - Arbeitsspeicher als temporär und Datei als dauerhaft sichtbar machen
  - Speicher- und Ladeformat, Datei- und Fachlogik sowie Prüfung durch erneutes Laden einordnen
  - Backup und Export als einfache Erweiterung markieren

### Arbeitsblattgrafiken zu StringBuilder

- [String-Immutability](./Arbeitsblaetter/arbeitsblatt_grafiken/tag5_konzept_immutability_string.svg)
  - `String` als unveränderbarer Wert
  - Neue Objekte bei Veränderung
- [String-Verkettung mit Plus](./Arbeitsblaetter/arbeitsblatt_grafiken/tag5_prozess_string_verketten_plus.svg)
  - Ablauf und Kosten wiederholter Verkettung
- [String vs. StringBuilder](./Arbeitsblaetter/arbeitsblatt_grafiken/tag5_vergleich_string_vs_stringbuilder.svg)
  - Vergleich von unveränderbaren Strings und veränderbarem Builder

## Übungen

Übungen dienen der Anwendung und Vertiefung. Sie sind teilweise nach Basis, Aufbau, Vertiefung und Transfer gestaffelt.

### Primitive Datentypen, Wrapper und Parsing

- [Übungen – Primitive Datentypen & Wrapper](./Uebungen/uebungen_java_wrapper.md)
  - Fehler durch `null`
  - Primitive vs. Wrapper
  - `String` zu Zahl
  - `==` oder `equals()`
  - Sichere Eingabe und Schleifen
- [Theorie – Wrapper-Klassen](./Uebungen/theorie_wrapper.md)
  - Grundidee von Wrapper-Klassen
  - Autoboxing und Unboxing
  - Methoden erkunden
  - Merksätze und Arbeitsauftrag

### Strings

- [Theorie – String](./Uebungen/theorie_string.md)
  - Grundidee von `String`
  - Immutability
  - Methoden, Vergleich und Eingabe
- [Übungen – String-Klasse](./Uebungen/string_uebungen.md)
  - Vergleich und `equals()`
  - Gross- und Kleinschreibung
  - Immutability
  - Umlaute und Eingaben
- [Übungen – String-Klasse, Vertiefung](./Uebungen/string_uebungen_v2.md)
  - Methoden kombinieren
  - Teilstrings
  - Text prüfen und ersetzen
  - Eingabe validieren
  - Mini-Projekt
- [Tag 4 – String-Klasse, Mini-Projekt Parser](./Uebungen/string_mini_projekt_v3.md)
  - Einfacher Wort-Parser
  - Wortgrenzen und Delimiter
  - Bereinigte Ausgabe
  - Wortklassifikation und Statistik
- [Tag 4 – String-Klasse, Mini-Projekt Parser erweitert](./Uebungen/string_mini_projekt_v3_updated.md)
  - Erweiterte Parser-Anforderungen
  - Delimiter definieren
  - Verarbeitung, Klassifikation und Statistik

### StringBuilder und Parser

- [Übungen – StringBuilder & Parser](./Uebungen/uebungen_stringbuilder.md)
  - `append()`, `insert()`, `delete()`, `replace()` und `reverse()`
  - Kombination mehrerer Operationen
  - Vereinfachte Parser-Hauptaufgabe

### Arrays

- [Übungen – Arrays](./Uebungen/Uebungen_Arrays.md)
  - Basis: Arrays anlegen und ausgeben
  - Aufbau: Summe, Maximum und Zählen
  - Vertiefung: Suche und Index
  - Transfer: Temperaturen und Noten
- [Übungen – Arrays, Vertiefung](./Uebungen/Uebungen_Arrays_Vertiefung.md)
  - Muster erkennen
  - Variation von Such- und Auswertungsaufgaben
  - Kombination mit Messwerten
  - Edge Cases und Reflexion
- [Übungen – 2D Arrays, Vertiefung](./Uebungen/Uebungen_2D_Arrays.md)
  - Ausgabe von 2D-Arrays
  - Summe und Durchschnitt pro Zeile
  - Gesamtmaximum und Gesamtdurchschnitt
  - Beste Messreihe
  - Edge Cases mit unterschiedlichen Längen und leeren Zeilen

### Methoden

- [Übungen – Methoden in Java](./Uebungen/Uebungen_Methoden.md)
  - Methoden aufrufen und Rückgabewerte verwenden
  - einfache Methoden mit `int`, `boolean` und `void`
  - Array-Auswertungen als Methoden
  - 2D-Array-Auswertungen mit Hilfsmethoden
  - Edge Cases bei leeren Arrays
- [Übungen – Methoden festigen und Refactoring](./Uebungen/Uebungen_Methoden_Festigung.md)
  - bestehende Schleifen in Methoden auslagern
  - einfache Testausgaben formulieren
  - Grenzen als Parameter verwenden
  - String- und 2D-Array-Auswertungen refaktorieren
  - kleine Auswertung mit mehreren Methoden strukturieren

### Klassen und Objekte

- [Übungen – Klassen und Objekte](./Uebungen/Uebungen_Klassen_und_Objekte.md)
  - Klassen lesen und Objekte erstellen
  - Methoden und Konstruktoren ergänzen
  - Produktklasse mit Rückgabewert und Validierung
  - Array von Objekten auswerten
- [Übungen – Kapselung, Getter und Setter](./Uebungen/Uebungen_Kapselung_Getter_Setter.md)
  - private Attribute einführen
  - Getter und Setter schreiben
  - Setter mit Validierung ergänzen
  - Bankkonto mit kontrollierten Methoden
  - Objektarray ohne direkten Attributzugriff auswerten
- [Übungen – Objektarrays und Verwaltungslogik](./Uebungen/Uebungen_Objektarrays_Verwaltungslogik.md)
  - Produktarray erstellen und ausgeben
  - Gesamtwert und Durchschnitt berechnen
  - Produkte suchen und zählen
  - teuerstes Produkt finden
  - Preise kontrolliert verändern
- [Übungen – ArrayList](./Uebungen/Uebungen_ArrayList.md)
  - `ArrayList<Produkt>` erstellen und füllen
  - Produkte ausgeben, suchen, zählen und entfernen
  - teuerstes Produkt finden
  - Preise kontrolliert verändern
  - Verwaltung ohne Berechnungsschleifen in `main`
- [Übungen – Java-Packages](./Uebungen/Uebungen_Packages.md)
  - Package-Deklarationen und Ordner zuordnen
  - Produktverwaltung in `model`, `service` und `Main` aufteilen
  - Imports für eigene Klassen ergänzen
  - Sichtbarkeit von Klassen und Methoden begründen
  - Algorithmen in `ArrayAlgorithmen` und `SortierAlgorithmen` strukturieren
  - Pensionskassen-Simulation in Packages aufteilen und als CSV ausgeben
  - ohne Maven nach `out` kompilieren und mit Classpath starten
- [Übungen – Algorithmen und Datenstrukturen](./Uebungen/Uebungen_Algorithmen_Datenstrukturen.md)
  - lineare Suche, Minimum, Maximum und Zählen
  - Bubble Sort und Selection Sort ergänzen
  - absteigend sortieren und Sortierung prüfen
  - Preise und optional Produktobjekte sortieren
  - Zinseszins mit Schleife berechnen
  - Pensionskassenkapital simulieren und als CSV für Excel ausgeben
- [Übungen – Maven Einstieg](./Uebungen/Uebungen_Maven_Einstieg.md)
  - Begriffe rund um Maven, `javac`, `java`, `pom.xml`, `src/main/java` und `target` zuordnen
  - Produktverwaltung von manueller Struktur nach Maven-Struktur migrieren
  - `mvn clean` und `mvn compile` ausführen und einordnen
  - Fehlerdiagnose zu falscher Projektstruktur und falschem Arbeitsverzeichnis
  - Reflexion zu `Convention over Configuration`
  - Transfer zur Pensionskassen-Simulation und optionaler Ausblick auf weitere Tools mit Konventionen
- [Übungen – Maven-Projekte ausführen und paketieren](./Uebungen/Uebungen_Maven_Ausfuehren_und_Paketieren.md)
  - `compile`, Programmstart und `package` zuordnen
  - `mvn compile` ausführen und `target/classes` untersuchen
  - Produktverwaltung mit `java -cp target/classes` starten
  - `mvn package` ausführen und JAR-Datei unter `target` einordnen
  - Fehlerdiagnose zu Java-`package`, Maven `package`, `target`, Arbeitsverzeichnis und Maven-Magie
  - reproduzierbare Builds und Build-Server-Ausblick reflektieren
- [Übungen – Maven-Projekte mit einfachen Tests vorbereiten](./Uebungen/Uebungen_Maven_Einfache_Tests_Vorbereiten.md)
  - Methode mit erwartetem Resultat manuell prüfen
  - mehrere Testfälle mit `if`/`else` ausgeben
  - Suche und Gesamtwert der Produktverwaltung prüfen
  - Fachlogik aus `main` herauslösen
  - Edge Cases bewusst ergänzen
  - reflektieren, warum diese Struktur später für JUnit hilfreich ist
- [Übungen – Von manuellen Tests zu automatisierten Tests mit JUnit](./Uebungen/Uebungen_JUnit_Einstieg.md)
  - manuelle Prüfung in JUnit-Test umwandeln
  - mehrere einfache Testmethoden mit `@Test` und `assertEquals` schreiben
  - Edge Cases für Rabatt, Suche und Gesamtwert testen
  - Fachlogik aus `main` herauslösen und prüfbar machen
  - Produktverwaltung mit mehreren JUnit-Tests prüfen
  - reflektieren, warum `mvn test` für Teamarbeit, Build-Server und CI/CD wichtig ist
- [Übungen – Wenn automatisierte Tests fehlschlagen](./Uebungen/Uebungen_JUnit_Fehleranalyse.md)
  - fehlgeschlagene `assertEquals`-Meldungen lesen
  - absichtlich fehlerhafte Rabattberechnung korrigieren
  - falsche Erwartung im Test erkennen
  - Stacktrace grob einordnen
  - mehrere Testfehler unterscheiden
  - Edge Cases und Regressionen bewusst erzeugen und korrigieren
  - Produktsuche und Gesamtwertberechnung mit Tests absichern
- [Übungen – Refactoring mit Tests absichern](./Uebungen/Uebungen_Refactoring_mit_Tests.md)
  - grünen Ausgangszustand mit `mvn test` herstellen
  - Logik aus `main` verschieben
  - lange Methoden schrittweise aufteilen
  - doppelte Rabattberechnung zentralisieren
  - sprechende Methodennamen wählen
  - Regression bewusst erzeugen, erkennen und korrigieren
  - Produktverwaltung schrittweise refaktorieren
- [Übungen – Produktdaten aus CSV-Dateien laden](./Uebungen/Uebungen_CSV_Laden.md)
  - CSV-Zeilen in Produkte umwandeln
  - mehrere Produkte aus Datei laden
  - `ArrayList<Produkt>` füllen und auswerten
  - leere, unvollständige und ungültige Zeilen behandeln
- [Übungen – Produktdaten als CSV-Dateien speichern](./Uebungen/Uebungen_CSV_Speichern.md)
  - Produkte in CSV-Zeilen umwandeln
  - mehrere Produkte in eine Datei speichern
  - gespeicherte Produkte erneut laden und prüfen
  - leere Listen, Überschreiben und einfache Fehlerfälle behandeln
- [Übungen – Persistenzablauf vertiefen](./Uebungen/Uebungen_Persistenzablauf_Vertiefen.md)
  - Produkte aus CSV laden, ausgeben, bearbeiten, speichern und erneut laden
  - neues Produkt hinzufügen und Preis eines bestehenden Produkts ändern
  - Gesamtwert vor und nach der Änderung vergleichen
  - ungültige CSV-Zeilen zählen und leere Produktlisten behandeln
  - Transfer mit Backup-Datei, Exportdatei, Kopfzeile und Änderungsstatistik

## Repetitionen

Repetitionen kombinieren mehrere bekannte Lerneinheiten und dienen der Diagnose, ob zentrale Konzepte verinnerlicht wurden. Sie liegen getrennt von normalen Übungen unter `Repetitionen/<Name>/` und bestehen standardmässig aus einer Lernenden-Version und einer Lehrpersonen-Version mit gegenseitigen Links.

- [Repetition Java Intro – Lernenden-Version](./Repetitionen/Repetition_Java_Intro/Lernende/Repetition_Java_Intro.md)
  - direkt abgabefähige Repetitionsserie
  - Pflichtteil, Vertiefung und optionale Transferaufgaben
  - Produktverwaltung mit Klassen, Kapselung, `ArrayList` und Methoden
- [Repetition Java Intro – Lehrpersonen-Version](./Repetitionen/Repetition_Java_Intro/Lehrperson/Repetition_Java_Intro_LP.md)
  - gleicher Aufgabenkern mit didaktischen Hinweisen
  - Diagnosehinweise, Beobachtungspunkte, Hilfestellungen und Zeitangaben

## Musterlösungen

Musterlösungen halten kompakte Referenzlösungen und Bewertungshilfen bereit.

- [Lösungen – Arrays](./Musterloesungen/Loesungen_Arrays.md)
  - Einstiegslösung zu Arrays
- [Lösungen – Arrays im Stil](./Musterloesungen/Loesungen_Arrays_im_Stil.md)
  - Summe, Maximum, Zählen, Suche, Index, Temperaturen und Noten
- [Lösungen – 2D Arrays](./Musterloesungen/Loesungen_2D_Arrays.md)
  - Ausgabe, Zeilensummen, Durchschnitt, Maximum und Edge Cases
- [Lösungen – Methoden in Java](./Musterloesungen/Loesungen_Methoden.md)
  - Methodenaufrufe, Rückgabewerte und Array-Hilfsmethoden
- [Lösungen – Methoden festigen und Refactoring](./Musterloesungen/Loesungen_Methoden_Festigung.md)
  - Refactoring-Lösungen zu Array-, String- und 2D-Array-Aufgaben
- [Lösungen – Klassen und Objekte](./Musterloesungen/Loesungen_Klassen_und_Objekte.md)
  - Personen- und Produktklasse mit Konstruktoren, Methoden und Objektarray-Auswertung
- [Lösungen – Kapselung, Getter und Setter](./Musterloesungen/Loesungen_Kapselung_Getter_Setter.md)
  - gekapselte Produktklasse, Bankkonto und Objektarray-Auswertung über Getter
- [Lösungen – Objektarrays und Verwaltungslogik](./Musterloesungen/Loesungen_Objektarrays_Verwaltungslogik.md)
  - Produktverwaltung mit Objektarray, Suche, Zählen, Maximum und Preisänderung
- [Lösungen – ArrayList](./Musterloesungen/Loesungen_ArrayList.md)
  - Produktverwaltung mit `ArrayList`, Suche, Entfernen, Maximum und Preisänderung
- [Lösungen – Java-Packages](./Musterloesungen/Loesungen_Packages.md)
  - Produktverwaltung, Algorithmen und Pensionskassen-Simulation mit Package-Struktur, Imports, `javac -d out` und `java -cp out`
- [Lösungen – Algorithmen und Datenstrukturen](./Musterloesungen/Loesungen_Algorithmen_Datenstrukturen.md)
  - Such-, Zähl-, Minimum- und Maximum-Methoden, Bubble Sort, Selection Sort, Zinseszins und Pensionskassen-Simulation
- [Lösungen – Maven Einstieg](./Musterloesungen/Loesungen_Maven_Einstieg.md)
  - kompakte Lösungen zur Maven-Begriffsklärung, Projektstruktur, `pom.xml`, Fehlerdiagnose und Reflexion
- [Lösungen – Maven-Projekte ausführen und paketieren](./Musterloesungen/Loesungen_Maven_Ausfuehren_und_Paketieren.md)
  - kompakte Lösungen zu `compile`, Programmstart, `package`, `target/classes`, JAR-Artefakt, Fehlerdiagnose und CI/CD-Ausblick
- [Lösungen – Maven-Projekte mit einfachen Tests vorbereiten](./Musterloesungen/Loesungen_Maven_Einfache_Tests_Vorbereiten.md)
  - kompakte Lösungen zu erwarteten und tatsächlichen Resultaten, einfachen Prüfhilfen, Trennung von `main` und Fachlogik, Produktverwaltung, Edge Cases und Reflexion
- [Lösungen – Von manuellen Tests zu automatisierten Tests mit JUnit](./Musterloesungen/Loesungen_JUnit_Einstieg.md)
  - kompakte Lösung mit `pom.xml`, `src/main/java`, `src/test/java`, einfacher Testklasse, `@Test`, `assertEquals`, sparsam `assertTrue`, Edge Cases, Fehlerdiagnose und `mvn test`-Verifikation
- [Lösungen – Wenn automatisierte Tests fehlschlagen](./Musterloesungen/Loesungen_JUnit_Fehleranalyse.md)
  - kompakte Lösungen zu `expected` und `actual`, Fehlerursachen, korrigierter Fachlogik, Edge Cases, Regressionen, `mvn test`, einfachen Surefire-Hinweisen und Reflexion
- [Lösungen – Refactoring mit Tests absichern](./Musterloesungen/Loesungen_Refactoring_mit_Tests.md)
  - kompakte Lösungen zu grünem Ausgangszustand, kleinen Refactoring-Schritten, entlasteter `main`, zentralisierter Fachlogik, Regressionen und `mvn test`-Verifikation
- [Lösungen – Produktdaten aus CSV-Dateien laden](./Musterloesungen/Loesungen_CSV_Laden.md)
  - kompakte Standardlösung mit `CsvProduktLeser`, `Produkt`, `ProduktVerwaltung`, `ArrayList`, `split(";")`, `Double.parseDouble(...)` und einfachen Fehlerfällen
- [Lösungen – Produktdaten als CSV-Dateien speichern](./Musterloesungen/Loesungen_CSV_Speichern.md)
  - kompakte Standardlösung mit `CsvProduktSpeicher`, `CsvProduktLeser`, `Produkt`, `ProduktVerwaltung`, `ArrayList`, `Files.write(...)`, erneutem Laden, leeren Listen und einfachen Fehlerfällen
- [Lösungen – Persistenzablauf vertiefen](./Musterloesungen/Loesungen_Persistenzablauf_Vertiefen.md)
  - kompakte Standardlösung mit `Produkt`, `ProduktVerwaltung`, `CsvProduktLeser`, `CsvProduktSpeicher` und `Main`
  - vollständiger Ablauf aus Laden, Bearbeiten, Speichern, erneutem Laden und Prüfen
  - Gesamtwertvergleich, fehlerhafte CSV-Zeilen, leere Listen, Backup, Export, Kopfzeile und Änderungsstatistik
  - dokumentierte Validierung mit temporärem Maven-Projekt
- [Musterlösungen – StringBuilder & Parser](./Musterloesungen/musterloesungen_stringbuilder.md)
  - StringBuilder-Methoden und vereinfachter Parser
- [Musterlösungen – Mini-Projekt String Parser](./Musterloesungen/string_parser_loesungen.md)
  - Naive, strukturierte und erweiterte Lösung
  - Bewertungsskala und Lehrerhinweise

## Ergänzende Vorlagen und Workflows

Diese Dateien sind keine direkten Lerninhalte für Java, unterstützen aber die Erstellung konsistenter Unterrichtsgrafiken.

- [SVG-Workflow-Sheet](./templates/svg_workflow_sheet.md)
- [SVG-Workflow-Sheet für Lernende](./templates/lernende/svg_workflow_sheet_lernende.md)
- [Arbeitsblatt SVG-Grafiken](./templates/lernende/arbeitsblatt_svg_grafiken.md)
- [SVG-Templates](./templates/)
- [Prompts für Grafiktypen](./templates/prompts/)
