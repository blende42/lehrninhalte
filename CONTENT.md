# Lerninhalte

Diese Übersicht listet die vorhandenen Lerninhalte des Repositories nach Materialtyp und Thema. Sie dient als Orientierung für Unterrichtsplanung, Wiederholung, Projektarbeit und Weiterentwicklung der Unterlagen.

## Begleitende Didaktik-, Prozess- und Begriffsbibliothek

Diese Dateien unterstützen die KI-gestützte Erstellung und Prüfung von Lehrmitteln. Die verbindlichen Regeln bleiben in [AGENTS.md](./AGENTS.md).

### Didaktik

- [Didaktische Entwicklungslogik](./docs/didaktik/entwicklungslogik.md)
  - begründet die Entwicklung von Java-Grundlagen über Datenstrukturen, OOP, Maven, Tests, CSV-Persistenz, Verantwortlichkeiten, Interfaces und Services bis zu Projektarbeit, Projekt-Review, Architektur-Festigung, JDBC/H2, Mapping, mehreren Tabellen, Repository als einfachem strukturiertem Datenzugriff, technischem Logging als Beobachtbarkeit, technischer Konfiguration und einfacher Mehrsprachigkeit mit `Locale` und `ResourceBundle`

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
- [Projekt erstellen](./docs/prozesse/projekt_erstellen.md)
  - Checkliste für grössere Mini-Projekte mit Lernenden- und Lehrpersonen-Version
- [Projekt-Review](./docs/prozesse/projekt_review.md)
  - Checkliste für individuelle Reviews von Mini-Projekten mit Architekturgespräch, Reflexion und nächsten Lernschritten
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
- [projekt-erstellen](./.agents/skills/projekt-erstellen/SKILL.md)
  - unterstützt strukturierte Mini-Projekte mit Lernenden- und Lehrpersonen-Version
- [projekt-review](./.agents/skills/projekt-review/SKILL.md)
  - unterstützt strukturierte Projekt-Reviews mit Architekturgespräch, Reflexionsfragen, Testreview und Refactoring-Ideen
- [musterloesungen-erstellen](./.agents/skills/musterloesungen-erstellen/SKILL.md)
  - unterstützt kompakte, fachlich korrekte Musterlösungen
- [svg-pruefen](./.agents/skills/svg-pruefen/SKILL.md)
  - unterstützt die Prüfung von SVG-Grafiken auf XML, Lesbarkeit und Einbindung
- [java-maven-validieren](./.agents/skills/java-maven-validieren/SKILL.md)
  - unterstützt die technische Prüfung von Java-, Package-, Classpath- und Maven-Beispielen
- [git-repo-updaten](./.agents/skills/git-repo-updaten/SKILL.md)
  - kontrollierter Git-Abschluss nur bei ausdrücklichem Benutzerauftrag

Hinweis: `.codex/skills` ist eine veraltete Skill-Ablage. Die aktuellen Repo-Skills liegen unter `.agents/skills`.

### Vorlagen

- [Projekt-Review Vorlage](./templates/projekt_review_template.md)
  - wiederverwendbare Markdown-Vorlage für individuelle Projekt-Reviews mit Reflexion, Beobachtungspunkten und nächsten Lernschritten

## Empfohlene Unterrichtsreihenfolge

Diese Reihenfolge erfasst die bisher aufgebauten Konzepte und Übungen. Die Einträge bilden die bisher vorbereitete Unterrichtssequenz.

### Didaktische Entwicklungslinie

Die Reihenfolge ist bewusst als roter Faden aufgebaut: Grundlagen, Datenstrukturen, OOP, Maven, Tests, Refactoring, CSV-Persistenz, Verantwortlichkeiten, Interfaces, Polymorphie, Wiederverwendung, Vererbung und Services führen schrittweise zu Projektarbeit, Projekt-Review, Architektur-Festigung, JDBC/H2, Mapping, mehreren Tabellen, Repository als einfachem strukturiertem Datenzugriff, technischem Logging als Beobachtbarkeit, technischer Konfiguration und einfacher Mehrsprachigkeit.

Architektur wird dabei nicht abstrakt vorangestellt. Sie entsteht aus konkreten Problemen im Code: zu viel Logik in `Main`, vermischte Datei- und Fachlogik, doppelte Codeabschnitte, schwer testbare Methoden oder unklare Verantwortlichkeiten. Nach den Services folgt deshalb bewusst eine Festigungsphase, in der Lernende diese Strukturentscheidungen an bekannten Beispielen sichern.

Die ausführliche Begründung steht in [Didaktische Entwicklungslogik](./docs/didaktik/entwicklungslogik.md).

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

Hinweis: Dieses Mini-Projekt ist Altbestand unter `Uebungen`. Neue Mini-Projekte werden unter `Projekte` abgelegt.

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

### 27. Code strukturieren und Verantwortlichkeiten aufteilen

Ziel: Verantwortlichkeiten in der bekannten Produktverwaltung erkennen, `Main` entlasten, Fachlogik, Dateilogik und Ablaufsteuerung trennen sowie Code einfacher testbar und wartbar machen, ohne formale Enterprise-Architektur einzuführen.

Material:

- [Arbeitsblatt – Code strukturieren und Verantwortlichkeiten aufteilen](./Arbeitsblaetter/Arbeitsblatt_Verantwortlichkeiten_Aufteilen.md)
- [Code strukturieren: Verantwortlichkeiten aufteilen](./graphics/verantwortlichkeiten_aufteilen.svg)
- [Übungen – Code strukturieren und Verantwortlichkeiten aufteilen](./Uebungen/Uebungen_Verantwortlichkeiten_Aufteilen.md)
- [Lösungen – Code strukturieren und Verantwortlichkeiten aufteilen](./Musterloesungen/Loesungen_Verantwortlichkeiten_Aufteilen.md)

### 28. Interfaces für austauschbare Services

Ziel: Ein erstes Interface als Vertrag verstehen, `CsvProduktSpeicher` als konkrete Implementierung einordnen und `Main` so anpassen, dass es mit dem Typ `ProduktSpeicher` arbeitet, ohne Spring, Dependency Injection oder komplexe Architektur einzuführen.

Material:

- [Arbeitsblatt – Interfaces für austauschbare Services](./Arbeitsblaetter/Arbeitsblatt_Interfaces_Austauschbare_Services.md)
- [Interface als Vertrag: ProduktSpeicher](./graphics/interface_produkt_speicher.svg)
- [Übungen – Interfaces für austauschbare Services](./Uebungen/Uebungen_Interfaces_Austauschbare_Services.md)
- [Lösungen – Interfaces für austauschbare Services](./Musterloesungen/Loesungen_Interfaces_Austauschbare_Services.md)

### 29. Mehrere Klassen mit demselben Interface

Ziel: Eine zweite konkrete Implementierung `KonsolenProduktSpeicher` einführen, mehrere Klassen mit demselben Interface-Vertrag vergleichen und sichtbar machen, dass `Main` weiterhin mit `ProduktSpeicher` arbeitet, während nur die konkrete Umsetzung ausgetauscht wird.

Material:

- [Arbeitsblatt – Mehrere Klassen mit demselben Interface](./Arbeitsblaetter/Arbeitsblatt_Mehrere_Implementierungen_Interface.md)
- [Mehrere Implementierungen eines Interface](./graphics/mehrere_implementierungen_interface.svg)
- [Übungen – Mehrere Klassen mit demselben Interface](./Uebungen/Uebungen_Mehrere_Implementierungen_Interface.md)
- [Lösungen – Mehrere Klassen mit demselben Interface](./Musterloesungen/Loesungen_Mehrere_Implementierungen_Interface.md)

### 30. Unterschiedliche Objekte über dasselbe Interface verwenden

Ziel: Praktisch beobachten, dass eine Variable vom Interface-Typ `ProduktSpeicher` nacheinander unterschiedliche konkrete Objekte enthalten kann, während der Methodenaufruf gleich bleibt und die konkrete Klasse das Verhalten bestimmt.

Material:

- [Arbeitsblatt – Unterschiedliche Objekte über dasselbe Interface verwenden](./Arbeitsblaetter/Arbeitsblatt_Polymorphie_Interface.md)
- [Polymorphie mit Interface-Typ](./graphics/polymorphie_interface.svg)
- [Übungen – Unterschiedliche Objekte über dasselbe Interface verwenden](./Uebungen/Uebungen_Polymorphie_Interface.md)
- [Lösungen – Unterschiedliche Objekte über dasselbe Interface verwenden](./Musterloesungen/Loesungen_Polymorphie_Interface.md)

### 31. Code-Duplikate vermeiden und gemeinsamen Code wiederverwenden

Ziel: Mehrfach kopierten oder sehr ähnlichen Code in `CsvProduktSpeicher` und `KonsolenProduktSpeicher` erkennen, kleine Hilfsmethoden zur Wiederverwendung einsetzen und damit die Motivation für spätere Vererbung vorbereiten, ohne tiefe OOP-Theorie einzuführen.

Material:

- [Arbeitsblatt – Code-Duplikate vermeiden und gemeinsamen Code wiederverwenden](./Arbeitsblaetter/Arbeitsblatt_Code_Wiederverwenden.md)
- [Code-Duplikate vermeiden und gemeinsamen Code wiederverwenden](./graphics/code_wiederverwenden.svg)
- [Übungen – Code-Duplikate vermeiden und gemeinsamen Code wiederverwenden](./Uebungen/Uebungen_Code_Wiederverwenden.md)
- [Lösungen – Code-Duplikate vermeiden und gemeinsamen Code wiederverwenden](./Musterloesungen/Loesungen_Code_Wiederverwenden.md)

### 32. Gemeinsamen Code mit Vererbung wiederverwenden

Ziel: `extends` vorsichtig aus einem echten Wiederverwendungsproblem heraus einführen, eine kleine Basisklasse `ProduktSpeicherBasis` für gemeinsame Hilfsmethoden nutzen und Interface als Vertrag von Vererbung als gemeinsamer Implementierung unterscheiden.

Material:

- [Arbeitsblatt – Gemeinsamen Code mit Vererbung wiederverwenden](./Arbeitsblaetter/Arbeitsblatt_Vererbung_Code_Wiederverwenden.md)
- [Gemeinsamen Code mit Vererbung wiederverwenden](./graphics/vererbung_code_wiederverwenden.svg)
- [Übungen – Gemeinsamen Code mit Vererbung wiederverwenden](./Uebungen/Uebungen_Vererbung_Code_Wiederverwenden.md)
- [Lösungen – Gemeinsamen Code mit Vererbung wiederverwenden](./Musterloesungen/Loesungen_Vererbung_Code_Wiederverwenden.md)

### 33. Fachlogik in Services bündeln

Ziel: Eine einfache Service-Klasse `LagerService` einführen, fachliche Regeln aus `Main` herauslösen, Persistenz von Fachlogik trennen und kleine Schichten als verständliche Ordnung vorbereiten.

Material:

- [Arbeitsblatt – Fachlogik in Services bündeln](./Arbeitsblaetter/Arbeitsblatt_Fachlogik_Services.md)
- [Fachlogik in Services bündeln](./graphics/fachlogik_services.svg)
- [Übungen – Fachlogik in Services bündeln](./Uebungen/Uebungen_Fachlogik_Services.md)
- [Lösungen – Fachlogik in Services bündeln](./Musterloesungen/Loesungen_Fachlogik_Services.md)

### 34. Verantwortlichkeiten und Services festigen

Ziel: Die bekannten Strukturideen der Lagerverwaltung diagnostisch festigen, Verantwortlichkeiten von `Main`, `Produkt`, `LagerService`, `ProduktSpeicher` und `CsvProduktSpeicher` begründen, Fachlogik und Persistenz bewusst trennen, kleine Refactorings durchführen und Service-Methoden mit Tests absichern, ohne eine neue grosse Technologie einzuführen.

Material:

- [Arbeitsblatt – Verantwortlichkeiten und Services festigen](./Arbeitsblaetter/Arbeitsblatt_Verantwortlichkeiten_Services_Festigen.md)
- [Verantwortlichkeiten und Services festigen](./graphics/verantwortlichkeiten_services_festigen.svg)
- [Übungen – Verantwortlichkeiten und Services festigen](./Uebungen/Uebungen_Verantwortlichkeiten_Services_Festigen.md)
- [Lösungen – Verantwortlichkeiten und Services festigen](./Musterloesungen/Loesungen_Verantwortlichkeiten_Services_Festigen.md)

### 35. JDBC mit eingebetteter H2-Datenbank

Ziel: Datenbanken als alternative Persistenz verstehen, mit JDBC eine Verbindung zu H2 herstellen, einfache SQL-Befehle ausführen, `Connection`, `PreparedStatement` und `ResultSet` verwenden und die bekannte Idee von `ProduktSpeicher` als austauschbare Persistenz weiterführen, ohne ORM-Frameworks einzuführen.

Material:

- [Arbeitsblatt – JDBC mit eingebetteter H2-Datenbank](./Arbeitsblaetter/Arbeitsblatt_JDBC_H2_Grundlagen.md)
- [Übungen – JDBC mit eingebetteter H2-Datenbank](./Uebungen/Uebungen_JDBC_H2_Grundlagen.md)
- [Lösungen – JDBC mit eingebetteter H2-Datenbank](./Musterloesungen/Loesungen_JDBC_H2_Grundlagen.md)

### 36. DbProduktSpeicher mit JDBC und H2

Ziel: Die bekannte Lagerverwaltung um `DbProduktSpeicher` als echte alternative Implementierung von `ProduktSpeicher` erweitern, CSV- und Datenbank-Persistenz vergleichen, CRUD mit JDBC in der Persistenzklasse strukturieren und zeigen, dass `LagerService` und Fachlogik beim Wechsel der Persistenz unverändert bleiben.

Material:

- [Arbeitsblatt – DbProduktSpeicher mit JDBC und H2](./Arbeitsblaetter/Arbeitsblatt_DbProduktSpeicher_JDBC_H2.md)
- [Übungen – DbProduktSpeicher mit JDBC und H2](./Uebungen/Uebungen_DbProduktSpeicher_JDBC_H2.md)
- [Lösungen – DbProduktSpeicher mit JDBC und H2](./Musterloesungen/Loesungen_DbProduktSpeicher_JDBC_H2.md)

### 37. Bestehende Persistenz auf Datenbank erweitern

Ziel: Die bestehende Lagerverwaltung evolutionär um weitere H2-Persistenzbereiche erweitern, `DbAenderungsSpeicher` und eine Tabelle `AENDERUNG` einführen, JDBC-Muster aus `DbProduktSpeicher` wiederverwenden und beobachten, dass Services und Fachlogik trotz wachsender Persistenz möglichst stabil bleiben.

Material:

- [Arbeitsblatt – Bestehende Persistenz auf Datenbank erweitern](./Arbeitsblaetter/Arbeitsblatt_Persistenz_Datenbank_Erweitern.md)
- [Evolutionäre Persistenz-Erweiterung](./graphics/evolutionaere_persistenz_erweiterung.svg)
- [Übungen – Bestehende Persistenz auf Datenbank erweitern](./Uebungen/Uebungen_Persistenz_Datenbank_Erweitern.md)
- [Lösungen – Bestehende Persistenz auf Datenbank erweitern](./Musterloesungen/Loesungen_Persistenz_Datenbank_Erweitern.md)

### 38. Mapping zwischen Objekten und Datenbank

Ziel: Bewusst verstehen, dass Java-Objekte nicht direkt in der Datenbank existieren, sondern zwischen `Produkt`-Objekten und Zeilen der Tabelle `PRODUKT` übersetzt werden müssen; `ResultSet` zu Objekt, Objekt zu `PreparedStatement` und Mapping als Verantwortung von `DbProduktSpeicher` einordnen.

Material:

- [Arbeitsblatt – Mapping zwischen Objekten und Datenbank](./Arbeitsblaetter/Arbeitsblatt_Objekt_Datenbank_Mapping.md)
- [Mapping zwischen Objekten und Datenbank](./graphics/objekt_datenbank_mapping.svg)
- [Übungen – Mapping zwischen Objekten und Datenbank](./Uebungen/Uebungen_Objekt_Datenbank_Mapping.md)
- [Lösungen – Mapping zwischen Objekten und Datenbank](./Musterloesungen/Loesungen_Objekt_Datenbank_Mapping.md)

### 39. Mehrere Tabellen, Beziehungen und Repository

Ziel: Fachlich zusammengehörige Daten über mehrere Tabellen abbilden, `Produkt`, `PreisAenderung` und `BestandsAenderung` über `PRODUKT_ID` verbinden, Mapping über mehrere `ResultSet`-Abfragen strukturieren und `ProduktRepository` sowie `AenderungsRepository` als einfache Bündelung von JDBC- und Mapping-Code einführen, während `LagerService` fachlich bleibt.

Material:

- [Arbeitsblatt – Mehrere Tabellen, Beziehungen und Repository](./Arbeitsblaetter/Arbeitsblatt_Tabellen_Beziehungen_Repository.md)
- [Repository als Evolutionsschritt](./graphics/repository_evolutionsschritt.svg)
- [Repository und Tabellenbeziehungen](./graphics/repository_und_tabellenbeziehungen.svg)
- [Übungen – Mehrere Tabellen, Beziehungen und Repository](./Uebungen/Uebungen_Tabellen_Beziehungen_Repository.md)
- [Lösungen – Mehrere Tabellen, Beziehungen und Repository](./Musterloesungen/Loesungen_Tabellen_Beziehungen_Repository.md)

### 40. Technisches Logging in Java einführen

Ziel: Technische Abläufe in der gewachsenen Lagerverwaltung mit SLF4J und Logback gezielt sichtbar machen, `System.out.println` von dauerhaftem Logging unterscheiden, Log-Level sinnvoll verwenden und Repository-Klassen bei JDBC-Zugriffen sowie Fehlerfällen sparsam und nachvollziehbar loggen, ohne Logging mit Fachlogik oder Tests zu verwechseln.

Material:

- [Arbeitsblatt – Technisches Logging in Java einführen](./Arbeitsblaetter/Arbeitsblatt_Technisches_Logging.md)
- [Technisches Logging in Java](./graphics/technisches_logging_java.svg)
- [Übungen – Technisches Logging in Java einführen](./Uebungen/Uebungen_Technisches_Logging.md)
- [Lösungen – Technisches Logging in Java einführen](./Musterloesungen/Loesungen_Technisches_Logging.md)

### 41. Technische Konfiguration in Java

Ziel: Technische Einstellungen der gewachsenen Lagerverwaltung aus dem Java-Code herauslösen, `.properties`-Dateien mit `java.util.Properties` laden, DB-URL, Dateipfade, vorbereitete Logging-Werte und H2-Modus zentral konfigurieren und Fachlogik klar von technischer Konfiguration trennen, ohne Spring, YAML oder Konfigurationsframeworks einzuführen.

Material:

- [Arbeitsblatt – Technische Konfiguration in Java](./Arbeitsblaetter/Arbeitsblatt_Technische_Konfiguration.md)
- [Technische Konfiguration in Java](./graphics/technische_konfiguration_java.svg)
- [Übungen – Technische Konfiguration in Java](./Uebungen/Uebungen_Technische_Konfiguration.md)
- [Lösungen – Technische Konfiguration in Java](./Musterloesungen/Loesungen_Technische_Konfiguration.md)

### 42. Mehrsprachigkeit mit Locale und ResourceBundle

Ziel: Sichtbare Texte der bekannten Lagerverwaltung aus dem Java-Code herauslösen, `Locale` als Sprache und Region einordnen, `ResourceBundle` mit `messages_de.properties`, `messages_fr.properties` und `messages_it.properties` verwenden und technische Konfiguration klar von I18N trennen, ohne Frameworks oder Web-I18N einzuführen.

Material:

- [Arbeitsblatt – Mehrsprachigkeit mit Locale und ResourceBundle](./Arbeitsblaetter/Arbeitsblatt_I18N_ResourceBundle.md)
- [Mehrsprachigkeit mit Locale und ResourceBundle](./graphics/i18n_resourcebundle_locale.svg)
- [Übungen – Mehrsprachigkeit mit Locale und ResourceBundle](./Uebungen/Uebungen_I18N_ResourceBundle.md)
- [Lösungen – Mehrsprachigkeit mit Locale und ResourceBundle](./Musterloesungen/Loesungen_I18N_ResourceBundle.md)

### 43. REST-Schnittstellen mit Spring Boot einführen

Ziel: Die bekannte Lagerverwaltung über eine neue HTTP-/REST-Zugriffsschicht erreichbar machen, ohne `LagerService`, Repositorys und JDBC/H2 fachlich umzubauen. Die Lernenden verstehen Client/Server, HTTP Request/Response, URL, Endpoint, JSON, `@RestController`, `@GetMapping`, `@PostMapping`, automatische JSON-Ausgabe und `curl` anhand kleiner Endpoints auf `localhost:8080`.

Material:

- [Arbeitsblatt – REST-Schnittstellen mit Spring Boot einführen](./Arbeitsblaetter/Arbeitsblatt_REST_SpringBoot_Einstieg.md)
- [REST-Schnittstellen mit Spring Boot](./graphics/rest_springboot_einstieg.svg)
- [Übungen – REST-Schnittstellen mit Spring Boot einführen](./Uebungen/Uebungen_REST_SpringBoot_Einstieg.md)
- [Lösungen – REST-Schnittstellen mit Spring Boot einführen](./Musterloesungen/Loesungen_REST_SpringBoot_Einstieg.md)

### Nächster sinnvoller Block

Nach `REST-Schnittstellen mit Spring Boot einführen` bietet sich als nächstes Thema eine Festigung von REST Controller und HTTP-Grundlagen an:

- REST Controller als Zugriffsschicht wiederholen
- `GET` und `POST` an bekannten Lager-Endpunkten festigen
- HTTP Request, Response, Header und Body genauer unterscheiden
- JSON-Antworten und JSON-Request-Bodies analysieren
- `curl -i`, `Content-Type` und typische Fehler gezielt einsetzen
- Controller, Service und Repository weiterhin klar trennen
- noch keine Security, keine DTOs, keine Validation, keine Swagger/OpenAPI-Dokumentation und keine komplexe Fehlerbehandlung einführen

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
- [Arbeitsblatt – Code strukturieren und Verantwortlichkeiten aufteilen](./Arbeitsblaetter/Arbeitsblatt_Verantwortlichkeiten_Aufteilen.md)
  - Verantwortung als Hauptaufgabe einer Klasse erklären
  - `Main` als Startpunkt und Orchestrator einordnen
  - Fachlogik, Dateilogik und Ablaufsteuerung unterscheiden
  - bekannte Rollen `Produkt`, `ProduktVerwaltung`, `CsvProduktLeser`, `CsvProduktSpeicher` und `Main` zuordnen
  - Architekturgrafik zur Trennung von Rollen und Verantwortlichkeiten
  - typische Fehlerbilder bei überladener `Main` und künstlichen Klassen sichtbar machen
  - Ausblick auf spätere Schichten, Services und REST geben
- [Arbeitsblatt – Interfaces für austauschbare Services](./Arbeitsblaetter/Arbeitsblatt_Interfaces_Austauschbare_Services.md)
  - Interface als Vertrag erklären
  - `ProduktSpeicher` als erstes einzelnes Interface einführen
  - `CsvProduktSpeicher implements ProduktSpeicher` als konkrete Umsetzung zeigen
  - `Main` mit Variable vom Interface-Typ arbeiten lassen
  - Konzeptgrafik zum Vertrag zwischen `Main`, `ProduktSpeicher`, `CsvProduktSpeicher` und CSV-Datei
  - Austauschbarkeit als kleine, nachvollziehbare Idee vorbereiten
  - Fehlerbilder wie Implementierungsdetails im Interface und zu viele Interfaces sichtbar machen
  - Ausblick auf spätere Services, Schichten und weitere Implementierungen geben
- [Arbeitsblatt – Mehrere Klassen mit demselben Interface](./Arbeitsblaetter/Arbeitsblatt_Mehrere_Implementierungen_Interface.md)
  - zweite Implementierung `KonsolenProduktSpeicher` einführen
  - `ProduktSpeicher` als gemeinsamen Vertrag beibehalten
  - gleiche Methodensignatur mit unterschiedlichem Verhalten vergleichen
  - Konzeptgrafik zu gemeinsamem Vertrag und austauschbaren Implementierungen einbinden
  - `Main` weiterhin mit dem Interface-Typ arbeiten lassen
  - konkrete Implementierung zwischen `CsvProduktSpeicher` und `KonsolenProduktSpeicher` austauschen
  - Vertrag und Umsetzung klar trennen
  - typische Fehlerbilder beim Verändern des Interfaces, falschen Signaturen und zu vielen Implementierungen sichtbar machen
- [Arbeitsblatt – Unterschiedliche Objekte über dasselbe Interface verwenden](./Arbeitsblaetter/Arbeitsblatt_Polymorphie_Interface.md)
  - `ProduktSpeicher` als Variable vom Interface-Typ bewusst verwenden
  - nacheinander `CsvProduktSpeicher` und `KonsolenProduktSpeicher` zuweisen
  - gleichen Methodenaufruf mit unterschiedlichem Verhalten beobachten
  - Interface-Typ, konkretes Objekt und ausgeführten Code unterscheiden
  - Polymorphie praktisch und ohne abstrakte OOP-Theorie vorbereiten
  - typische Fehler wie direkte Interface-Instanziierung, Downcasting und unnötige Fallunterscheidungen sichtbar machen
- [Arbeitsblatt – Code-Duplikate vermeiden und gemeinsamen Code wiederverwenden](./Arbeitsblaetter/Arbeitsblatt_Code_Wiederverwenden.md)
  - ähnliche Codeabschnitte in `CsvProduktSpeicher` und `KonsolenProduktSpeicher` sichtbar machen
  - Problem mehrfach kopierter Logik vor der Lösung erklären
  - Produktformatierung mit kleinen Hilfsmethoden auslagern
  - Wiederverwendung als Wartbarkeitsvorteil einordnen
  - Unterschiede zwischen CSV-Datei und Konsolenausgabe bewusst getrennt lassen
  - Vererbung mit `extends` nur als vorsichtigen Ausblick vorbereiten
- [Arbeitsblatt – Gemeinsamen Code mit Vererbung wiederverwenden](./Arbeitsblaetter/Arbeitsblatt_Vererbung_Code_Wiederverwenden.md)
  - `extends` aus einem konkreten Wiederverwendungsproblem heraus einführen
  - `ProduktSpeicherBasis` als kleine Basisklasse für gemeinsame Hilfsmethoden nutzen
  - `CsvProduktSpeicher` und `KonsolenProduktSpeicher` mit `extends` und `implements` zeigen
  - Interface als Vertrag und Vererbung als gemeinsame Implementierung unterscheiden
  - Konzeptgrafik zu Interface, Basisklasse, konkreten Klassen und unterschiedlichem Verhalten einbinden
  - Grenzen von Vererbung, typische Fehler und Alternative mit Hilfsklasse sichtbar machen
- [Arbeitsblatt – Fachlogik in Services bündeln](./Arbeitsblaetter/Arbeitsblatt_Fachlogik_Services.md)
  - einfache Service-Idee mit `LagerService` einführen
  - Fachlogik aus `Main` herauslösen
  - `Produkt`, `LagerService`, `ProduktSpeicher`, `CsvProduktSpeicher` und `Main` nach Verantwortung unterscheiden
  - Persistenz und Fachlogik klar trennen
  - kleine Schichten als Ordnung für verständlicheren und besser testbaren Code vorbereiten
  - typische Fehler und Reflexionsfragen zu zu viel Logik in falschen Klassen sichtbar machen
- [Arbeitsblatt – Verantwortlichkeiten und Services festigen](./Arbeitsblaetter/Arbeitsblatt_Verantwortlichkeiten_Services_Festigen.md)
  - Verantwortlichkeiten von `Main`, `Produkt`, `LagerService`, `ProduktSpeicher` und `CsvProduktSpeicher` diagnostisch festigen
  - Fachlogik, Persistenzlogik und Ablaufsteuerung in vorhandenem Code unterscheiden
  - Vergleichsgrafik zu Fehlstruktur «alles in `Main`» und getrennter Struktur einbinden
  - typische Fehlstrukturen wie alles in `Main`, Persistenz im Service und Fachregeln in Speicherklassen analysieren
  - kleine Refactoring-Schritte mit erneuter Verhaltensprüfung vorbereiten
  - Service-Methoden als gut testbare fachliche Regeln einordnen
  - Reflexionsfragen zu Grenzen kleiner Strukturen und zu vielen Services stellen
- [Arbeitsblatt – JDBC mit eingebetteter H2-Datenbank](./Arbeitsblaetter/Arbeitsblatt_JDBC_H2_Grundlagen.md)
  - Datenbanken als alternative Persistenz zu CSV einführen
  - Vergleichsgrafik zu H2 Embedded, H2 Server-Modus, JDBC und austauschbarer Persistenz einbinden
  - JDBC, H2 Embedded, `Connection`, `PreparedStatement`, `ResultSet` und einfache SQL-Befehle erklären
  - `ProduktSpeicher`, `CsvProduktSpeicher` und `DbProduktSpeicher` als austauschbare Persistenzidee einordnen
  - Embedded- und Server-Modus von H2 auf Grundniveau vergleichen
  - typische Fehlerbilder wie offene Connections, falsches `ResultSet`-Lesen und vermischte SQL-/Fachlogik sichtbar machen
- [Arbeitsblatt – DbProduktSpeicher mit JDBC und H2](./Arbeitsblaetter/Arbeitsblatt_DbProduktSpeicher_JDBC_H2.md)
  - `DbProduktSpeicher` als konkrete neue Implementierung von `ProduktSpeicher` einführen
  - CSV- und Datenbank-Persistenz in der bekannten Lagerverwaltung vergleichen
  - Konzeptgrafik zu `LagerService`, `ProduktSpeicher`, `CsvProduktSpeicher`, `DbProduktSpeicher`, CSV-Datei und H2-Datenbank einbinden
  - `Connection`, `PreparedStatement`, `ResultSet` und CRUD im Kontext einer Speicherklasse strukturieren
  - zeigen, dass `Main` nur die Implementierung wechselt und `LagerService` unverändert bleibt
  - typische Fehlerbilder zu JDBC in `Main`, vermischter Fachlogik, fehlendem `ResultSet.next()` und ignorierten Exceptions sichtbar machen
  - Reflexion zur Verantwortung von `DbProduktSpeicher` und zur Rolle des Interfaces anleiten
- [Arbeitsblatt – Bestehende Persistenz auf Datenbank erweitern](./Arbeitsblaetter/Arbeitsblatt_Persistenz_Datenbank_Erweitern.md)
  - evolutionäre Weiterentwicklung der bekannten Lagerverwaltung erklären
  - `AenderungsEintrag`, `AenderungsSpeicher`, `CsvAenderungsSpeicher` und `DbAenderungsSpeicher` einordnen
  - zusätzliche Tabelle `AENDERUNG` für Preis- und Bestandsänderungen einführen
  - Architekturgrafik zur schrittweisen Erweiterung von Produkt- und Änderungs-Persistenz einbinden
  - JDBC-Muster aus `DbProduktSpeicher` wiederverwenden, ohne neue Framework-Architektur einzuführen
  - Mapping von `ResultSet` zu Objekt mit kleiner Hilfsmethode zeigen
  - stabile Fachlogik trotz wachsender Persistenz reflektieren
- [Arbeitsblatt – Mapping zwischen Objekten und Datenbank](./Arbeitsblaetter/Arbeitsblatt_Objekt_Datenbank_Mapping.md)
  - bewusst zwischen Java-Objekt und Datenbankzeile unterscheiden
  - `Produkt`-Attribute den Spalten `ID`, `NAME`, `PREIS` und `BESTAND` zuordnen
  - Konzeptgrafik zu `Produkt`, `DbProduktSpeicher`, `PreparedStatement`, `ResultSet` und Tabelle `PRODUKT` einbinden
  - `ResultSet` zu `Produkt` und `Produkt` zu `PreparedStatement` als zwei Mapping-Richtungen zeigen
  - Mapping als Verantwortung von `DbProduktSpeicher` einordnen
  - Java-Typen, SQL-Typen und passende JDBC-Methoden vergleichen
  - typische Fehler wie fehlendes `ResultSet.next()`, falsche Spaltennamen und falsche Platzhalter-Reihenfolge sichtbar machen
  - erklären, warum spätere Frameworks existieren, ohne ORM einzuführen
- [Arbeitsblatt – Mehrere Tabellen, Beziehungen und Repository](./Arbeitsblaetter/Arbeitsblatt_Tabellen_Beziehungen_Repository.md)
  - fachlich zusammengehörige Daten über `PRODUKT`, `PREISAENDERUNG` und `BESTANDSAENDERUNG` darstellen
  - `PRODUKT_ID` als einfachen Fremdschlüssel zu `PRODUKT.ID` erklären
  - Mapping von mehreren Tabellen zu `Produkt`, `PreisAenderung` und `BestandsAenderung` zeigen
  - Repository als Evolutionsschritt von einer überschaubaren Persistenzklasse zu fachlich getrennten Repositorys visualisieren
  - sortierte Änderungshistorien mit `ORDER BY ZEITPUNKT` und ISO-Zeitpunkten einordnen
  - Grafik zu `LagerService`, Repositorys, JDBC, H2 und Tabellenbeziehungen einbinden
  - `ProduktRepository` und `AenderungsRepository` als normale Klassen für strukturierten Datenzugriff einführen
  - JDBC- und Mapping-Code bündeln, ohne ORM, JPA, Hibernate, Spring Data oder generische Repositorys einzuführen
  - Fachlogik im `LagerService` von Datenzugriff und Mapping trennen
  - typische Fehler wie JDBC in `Main`, Mapping im Service, falsches `ResultSet`-Lesen und falsch modellierte Beziehungen sichtbar machen
- [Arbeitsblatt – Technisches Logging in Java einführen](./Arbeitsblaetter/Arbeitsblatt_Technisches_Logging.md)
  - Logging als technische Beobachtbarkeit nach wachsender Persistenzkomplexität einführen
  - Grafik zu `LagerService`, Repositorys, JDBC, Loggern, Log-Ausgabe und Abgrenzung zu Tests einbinden
  - `System.out.println` von dauerhaftem technischem Logging unterscheiden
  - SLF4J als Schnittstelle und Logback als konkrete Umsetzung einordnen
  - Logger pro Klasse, Log-Level und Repository-Logging praktisch zeigen
  - Exception-Logging mit Kontext statt verschluckter Fehler erklären
  - typische Fehler wie zu viele `INFO`-Logs, sensible Daten und Logging als Fachlogik sichtbar machen
- [Arbeitsblatt – Technische Konfiguration in Java](./Arbeitsblaetter/Arbeitsblatt_Technische_Konfiguration.md)
  - technische Konfiguration als nächsten Infrastrukturschritt nach JDBC/H2, Repository und Logging einführen
  - Grafik zu `app.properties`, Konfigurationsklasse, `ProduktRepository` und H2-Datenbank einbinden
  - Fachlogik von technischer Konfiguration trennen
  - `.properties`-Dateien und `java.util.Properties` anhand kleiner Beispiele erklären
  - DB-URL, Dateipfade, vorbereiteten Logging-Level und H2-Modus als technische Einstellungen einordnen
  - zentrale Konfigurationsklasse `AppConfig` ohne Frameworks vorbereiten
  - H2 Embedded und Server über Konfigurationswerte vergleichen
  - typische Fehler wie Hardcoding, mehrfaches Laden, fehlende Pflichtwerte und I18N-Verwechslung sichtbar machen
- [Arbeitsblatt – Mehrsprachigkeit mit Locale und ResourceBundle](./Arbeitsblaetter/Arbeitsblatt_I18N_ResourceBundle.md)
  - I18N als einfache Mehrsprachigkeit nach technischer Konfiguration einführen
  - Grafik zu `Locale`, `ResourceBundle`, Sprachdateien und sprachabhängiger Ausgabe einbinden
  - `Locale` als Sprache und optional Region erklären
  - `ResourceBundle` als Java-Mechanismus für sprachabhängige Texte zeigen
  - `messages_de.properties`, `messages_fr.properties` und `messages_it.properties` aufbauen
  - sichtbare Texte aus `Main` auslagern
  - technische Konfiguration und I18N trotz gleichem Dateiformat `.properties` trennen
  - typische Fehler wie falsche Dateinamen, fehlende Schlüssel und vermischte Verantwortlichkeiten sichtbar machen
- [Arbeitsblatt – REST-Schnittstellen mit Spring Boot einführen](./Arbeitsblaetter/Arbeitsblatt_REST_SpringBoot_Einstieg.md)
  - REST als neue Zugriffsschicht vor dem bestehenden `LagerService` einführen
  - Client/Server, HTTP Request/Response, URL, Endpoint und JSON anhand von `localhost:8080` erklären
  - `@RestController`, `@GetMapping`, `@PostMapping`, `@RequestBody` und automatische JSON-Ausgabe auf EFZ-Niveau zeigen
  - `curl` als technisches Werkzeug für `GET` und `POST` verwenden
  - typische Fehler wie Fachlogik im Controller, direkter Repository-Zugriff, falsche URL, fehlender `Content-Type` und ungültiges JSON sichtbar machen
  - Security, JPA, Spring Data, DTOs, Validation, Swagger/OpenAPI, Lombok und komplexe Fehlerbehandlung bewusst ausschliessen

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
- [Code strukturieren: Verantwortlichkeiten aufteilen](./graphics/verantwortlichkeiten_aufteilen.svg)
  - `Main`, `Produkt`, `ProduktVerwaltung`, `CsvProduktLeser` und `CsvProduktSpeicher` als getrennte Rollen zeigen
  - `Main` als Orchestrator statt Sammelort für alle Logik einordnen
  - Fachlogik und Dateilogik klar trennen
  - Testbarkeit und spätere Erweiterungen als Nutzen der Struktur sichtbar machen
- [Interface als Vertrag: ProduktSpeicher](./graphics/interface_produkt_speicher.svg)
  - `Main` arbeitet gegen das Interface `ProduktSpeicher`
  - `CsvProduktSpeicher` setzt den Vertrag um und enthält die Dateilogik
  - CSV-Datei bleibt das konkrete Speicherziel
  - Verhalten bleibt gleich, Struktur wird flexibler
- [Mehrere Implementierungen eines Interface](./graphics/mehrere_implementierungen_interface.svg)
  - `ProduktSpeicher` als gemeinsamer Vertrag
  - `CsvProduktSpeicher` und `KonsolenProduktSpeicher` erfüllen denselben Vertrag
  - konkrete Umsetzung ist austauschbar
  - `Main` arbeitet weiterhin mit `ProduktSpeicher`
  - Verhalten kann unterschiedlich sein
- [Polymorphie mit Interface-Typ](./graphics/polymorphie_interface.svg)
  - `ProduktSpeicher speicher` als Variable vom Interface-Typ
  - `CsvProduktSpeicher` und `KonsolenProduktSpeicher` als austauschbare konkrete Objekte
  - gleicher Aufruf `speicher.speichern(...)`
  - unterschiedliche Wirkung mit CSV-Datei oder Konsolenausgabe
  - konkrete Klasse entscheidet das Verhalten
- [Code-Duplikate vermeiden und gemeinsamen Code wiederverwenden](./graphics/code_wiederverwenden.svg)
  - ähnliche Logik in `CsvProduktSpeicher` und `KonsolenProduktSpeicher` sichtbar machen
  - gemeinsames Auslagern in Hilfsmethoden zeigen
  - weniger Duplikate, Änderungen an einer Stelle und bessere Wartbarkeit hervorheben
  - Vererbung nur als vorsichtigen Ausblick einordnen
- [Gemeinsamen Code mit Vererbung wiederverwenden](./graphics/vererbung_code_wiederverwenden.svg)
  - `ProduktSpeicher` als Interface und Vertrag zeigen
  - `ProduktSpeicherBasis` als kleine Basisklasse mit gemeinsamen Hilfsmethoden zeigen
  - `CsvProduktSpeicher` und `KonsolenProduktSpeicher` mit `extends` und `implements` einordnen
  - konkrete Klassen behalten CSV- beziehungsweise Konsolenverhalten
  - Interface als gleicher Vertrag und Vererbung als gemeinsame Implementierung unterscheiden
- [Fachlogik in Services bündeln](./graphics/fachlogik_services.svg)
  - `Main` als Ablaufsteuerung zeigen
  - `LagerService` als Ort für Fachlogik zeigen
  - `ProduktSpeicher` als Persistenzvertrag und `CsvProduktSpeicher` als CSV-Umsetzung einordnen
  - `Produkt` als Datenklasse darstellen
  - getrennte Verantwortlichkeiten und kleine Schichten-Idee sichtbar machen
- [Verantwortlichkeiten und Services festigen](./graphics/verantwortlichkeiten_services_festigen.svg)
  - Fehlstruktur «alles in `Main`» mit getrennter Struktur vergleichen
  - `Main`, `LagerService`, `ProduktSpeicher`, `CsvProduktSpeicher` und `Produkt` nach Verantwortung darstellen
  - zeigen, dass `Main` klein bleibt, Fachlogik im Service liegt und Persistenz separat bleibt
- [JDBC und H2: Embedded oder Server](./graphics/jdbc_h2_embedded_vs_server.svg)
  - H2 Embedded und H2 Server-Modus vergleichen
  - JDBC als Verbindungsschicht zwischen Java-Anwendung und Datenbank zeigen
  - `ProduktSpeicher`, `CsvProduktSpeicher` und `DbProduktSpeicher` als austauschbare Persistenz einordnen
- [CSV und Datenbank als austauschbare Persistenz](./graphics/csv_vs_db_produkt_speicher.svg)
  - `LagerService` als unveränderte Fachlogik zeigen
  - `ProduktSpeicher` als gemeinsamer Interface-Vertrag einordnen
  - `CsvProduktSpeicher` mit CSV-Datei und `DbProduktSpeicher` mit H2-Datenbank vergleichen
  - JDBC als Verbindung zwischen Java und Datenbank sichtbar machen
- [Evolutionäre Persistenz-Erweiterung](./graphics/evolutionaere_persistenz_erweiterung.svg)
  - `LagerService` als stabile Fachlogik zeigen
  - `ProduktSpeicher` und `AenderungsSpeicher` als nützliche Interfaces einordnen
  - CSV- und DB-Implementierungen für Produkte und Änderungen vergleichen
  - `DbProduktSpeicher` und `DbAenderungsSpeicher` über JDBC den Tabellen `PRODUKT` und `AENDERUNG` zuordnen
- [Mapping zwischen Objekten und Datenbank](./graphics/objekt_datenbank_mapping.svg)
  - `Produkt`-Objekt, `DbProduktSpeicher`, `PreparedStatement`, Tabelle `PRODUKT` und `ResultSet` in Beziehung setzen
  - Schreibweg `Objekt -> SQL-Werte` und Leseweg `ResultSet -> Objekt` sichtbar machen
  - zeigen, dass JDBC rohe Daten liefert und Fachlogik getrennt bleibt
- [Repository als Evolutionsschritt](./graphics/repository_evolutionsschritt.svg)
  - von `DbProduktSpeicher` zu `ProduktRepository` und `AenderungsRepository` überleiten
  - zeigen, dass Repositorys durch wachsenden Persistenz- und Mapping-Code sinnvoll werden
  - Fachlogik im `LagerService` von Datenzugriff und Mapping abgrenzen
- [Repository und Tabellenbeziehungen](./graphics/repository_und_tabellenbeziehungen.svg)
  - `LagerService`, `ProduktRepository`, `AenderungsRepository`, JDBC und H2-Datenbank einordnen
  - Tabellen `PRODUKT`, `PREISAENDERUNG` und `BESTANDSAENDERUNG` mit `ID` und `PRODUKT_ID` verbinden
  - Mapping als Übersetzung und Repository als Bündelung von Datenzugriff sichtbar machen
  - zeigen, dass Fachlogik getrennt bleibt
- [Technisches Logging in Java](./graphics/technisches_logging_java.svg)
  - zeigt `LagerService` als Fachlogik und Repositorys als technische Datenzugriffsorte
  - macht Logger mit `DEBUG`, `INFO`, `WARN` und `ERROR` sichtbar
  - grenzt Logging von `System.out.println`, Tests und Fachlogik ab
- [Technische Konfiguration in Java](./graphics/technische_konfiguration_java.svg)
  - zeigt `app.properties` mit `db.url`, `csv.path` und `log.level`
  - führt über Konfigurationsklasse zu `ProduktRepository` und H2-Datenbank
  - macht unterschiedliche Konfigurationen für dieselbe Anwendung sichtbar
  - grenzt technische Konfiguration von Fachlogik ab
- [Mehrsprachigkeit mit Locale und ResourceBundle](./graphics/i18n_resourcebundle_locale.svg)
  - zeigt `Locale`, `ResourceBundle`, `messages_de.properties`, `messages_fr.properties` und `messages_it.properties`
  - führt zu sprachabhängiger Ausgabe mit gleichem Java-Code
  - macht sichtbar, dass Texte nicht hartcodiert werden
  - grenzt technische Konfiguration von I18N ab
- [REST-Schnittstellen mit Spring Boot](./graphics/rest_springboot_einstieg.svg)
  - zeigt `curl` als Client, HTTP/JSON als Austausch und den REST Controller als neue Zugriffsschicht
  - führt weiter zum bestehenden `LagerService`, Repository und H2
  - macht sichtbar, dass REST die Fachlogik nicht ersetzt
  - grenzt Controller-Verantwortung von Service- und Repository-Verantwortung ab
- [Projektreview Änderungshistorie Architektur](./graphics/projektreview_aenderungshistorie_architektur.svg)
  - `Main`, `LagerService`, `JournalService`, `ProduktSpeicher`, `Produkt` und `AenderungsEintrag` nach Verantwortung darstellen
  - zeigen, dass Historie neue Verantwortlichkeiten erzeugt und Services wachsen können
  - Fehlstruktur, getrennte Struktur und Tests als Hilfe beim Refactoring sichtbar machen

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
- [Übungen – Code strukturieren und Verantwortlichkeiten aufteilen](./Uebungen/Uebungen_Verantwortlichkeiten_Aufteilen.md)
  - Verantwortlichkeiten bestehenden Codeabschnitten zuordnen
  - Fachlogik aus `Main` in `ProduktVerwaltung` verschieben
  - CSV-Laden und CSV-Speichern aus `Main` in passende Klassen verschieben
  - überladene `Main` schrittweise refaktorieren und Tests ausführen
  - Transfer mit Statistik-Service, Export-Service-Idee, Backup-Zuordnung und Entscheidung neue Klasse oder Methode
- [Übungen – Interfaces für austauschbare Services](./Uebungen/Uebungen_Interfaces_Austauschbare_Services.md)
  - `ProduktSpeicher` als Interface erstellen
  - `CsvProduktSpeicher` mit `implements ProduktSpeicher` anpassen
  - `Main` auf den Interface-Typ umstellen
  - unverändertes Speicherverhalten mit `mvn test` oder `mvn package` prüfen
  - Vertrag und Umsetzung in Codeabschnitten unterscheiden
  - Transfer mit Ideen für `KonsolenProduktSpeicher` und `BackupProduktSpeicher`
- [Übungen – Mehrere Klassen mit demselben Interface](./Uebungen/Uebungen_Mehrere_Implementierungen_Interface.md)
  - `KonsolenProduktSpeicher` als zweite Implementierung erstellen
  - `ProduktSpeicher` erneut implementieren und Methodensignatur prüfen
  - `Main` zwischen `CsvProduktSpeicher` und `KonsolenProduktSpeicher` umstellen
  - unterschiedliches Verhalten beobachten und vergleichen
  - Vertrag, Umsetzung und Nutzung des Vertrags unterscheiden
  - Transferideen zu `BackupProduktSpeicher`, `StatistikProduktSpeicher` und `JsonProduktSpeicher` diskutieren
- [Übungen – Unterschiedliche Objekte über dasselbe Interface verwenden](./Uebungen/Uebungen_Polymorphie_Interface.md)
  - `ProduktSpeicher`-Variable anlegen und nacheinander zwei konkrete Objekte verwenden
  - `speicher.speichern(...)` mehrfach gleich aufrufen
  - CSV-Datei und Konsolenausgabe als unterschiedliche Wirkung vergleichen
  - Ablauf und Verantwortlichkeiten dokumentieren
  - Transferideen zu doppeltem Speichern, `LoggingProduktSpeicher` und `BackupProduktSpeicher` skizzieren
- [Übungen – Code-Duplikate vermeiden und gemeinsamen Code wiederverwenden](./Uebungen/Uebungen_Code_Wiederverwenden.md)
  - doppelte und ähnliche Codeabschnitte markieren
  - Gemeinsamkeiten und Unterschiede zwischen Speicherklassen beschreiben
  - Produktformatierung in Hilfsmethoden auslagern
  - bestehendes Verhalten mit Maven erneut prüfen
  - Wartbarkeit nach kleinen Refactorings reflektieren
  - Transfer zu Logging-Ausgabe, Statistik-Hilfsmethode und gemeinsamer Basisklasse als Idee
- [Übungen – Gemeinsamen Code mit Vererbung wiederverwenden](./Uebungen/Uebungen_Vererbung_Code_Wiederverwenden.md)
  - doppelte Hilfsmethoden in `CsvProduktSpeicher` und `KonsolenProduktSpeicher` markieren
  - gemeinsame Produktformatierung erkennen und in `ProduktSpeicherBasis` verschieben
  - konkrete Speicherklassen mit `extends ProduktSpeicherBasis` und `implements ProduktSpeicher` anpassen
  - Verhalten nach dem Refactoring mit Maven und manueller Prüfung kontrollieren
  - entscheiden, welche Methoden in Basisklasse, Interface oder konkrete Klasse gehören
  - Transfer zu Grenzen von Vererbung und Alternative mit Hilfsklasse diskutieren
- [Übungen – Fachlogik in Services bündeln](./Uebungen/Uebungen_Fachlogik_Services.md)
  - fachliche Regeln in bestehendem Code markieren
  - `LagerService` erstellen und Verkaufslogik aus `Main` verschieben
  - `bestandPruefen(...)`, `verkaufen(...)`, `bestandErhoehen(...)` und `warnungPruefen(...)` umsetzen
  - `Main` vereinfachen und Persistenz beim `ProduktSpeicher` belassen
  - kleine Tests oder Prüfungen für Service-Methoden ergänzen
  - Transfer zu weiteren Services, ungeeigneten Verantwortlichkeiten und Grenzen zu vieler Services diskutieren
- [Übungen – Verantwortlichkeiten und Services festigen](./Uebungen/Uebungen_Verantwortlichkeiten_Services_Festigen.md)
  - vorhandene Methoden und Codeabschnitte nach Verantwortung zuordnen
  - problematische Logik in `Main`, Fachlogik und Persistenzlogik markieren
  - Logik aus `Main` in `LagerService` verschieben und `Main` vereinfachen
  - bewusst schlechte Strukturen analysieren und doppelte Prüfungen zusammenführen
  - geeignete und ungeeignete Service-Methoden unterscheiden
  - Tests für Service-Methoden, Fehlerfälle und angepasste Struktur ergänzen
  - Transfer zu weiteren Services, Grenzen kleiner Strukturen und zukünftigen Erweiterungen diskutieren
- [Übungen – JDBC mit eingebetteter H2-Datenbank](./Uebungen/Uebungen_JDBC_H2_Grundlagen.md)
  - H2-Dependency ergänzen, Embedded-Verbindung herstellen und Tabelle `PRODUKT` erstellen
  - Produkte mit `INSERT`, `SELECT`, `UPDATE` und `DELETE` bearbeiten
  - `PreparedStatement` mit Parametern und `ResultSet` korrekt verwenden
  - mehrere Produkte speichern, Produkte nach ID suchen und ungültige Werte behandeln
  - Ressourcen korrekt schliessen und CSV mit Datenbank-Persistenz vergleichen
  - H2 Server-Modus kurz starten, JDBC-URL anpassen und `DbProduktSpeicher` als Idee diskutieren
- [Übungen – DbProduktSpeicher mit JDBC und H2](./Uebungen/Uebungen_DbProduktSpeicher_JDBC_H2.md)
  - `DbProduktSpeicher` erstellen und `ProduktSpeicher` korrekt implementieren
  - H2-Verbindung, Tabelle `PRODUKT`, Speichern, Laden, Aktualisieren und Löschen praktisch umsetzen
  - `Main` auf `DbProduktSpeicher` umstellen und bestehende Fachlogik weiterverwenden
- [Übungen – Bestehende Persistenz auf Datenbank erweitern](./Uebungen/Uebungen_Persistenz_Datenbank_Erweitern.md)
  - `AenderungsEintrag`, `AenderungsSpeicher` und `DbAenderungsSpeicher` ergänzen
  - Tabelle `AENDERUNG` erstellen und Änderungen speichern, lesen und nach Produkt filtern
  - bestehende Services und `Main`-Struktur weiterverwenden
  - Preis- und Bestandsänderungen, mehrere Tabellen, Fehlerfälle und Mapping vertiefen
  - Transfer zu stabilen Services, mehreren Tabellen und sinnvollem Refactoring
  - mehrere Produkte speichern, nach ID suchen, Datenbank leeren, Fehlerfälle behandeln und Ressourcen prüfen
  - CSV- und DB-Implementierung vergleichen sowie Embedded- und Server-Modus einordnen
  - Transferfragen zu weiteren Persistenzarten, unveränderter Fachlogik und hilfreichen Interfaces bearbeiten
- [Übungen – Mapping zwischen Objekten und Datenbank](./Uebungen/Uebungen_Objekt_Datenbank_Mapping.md)
  - Mapping-Tabelle zwischen `Produkt` und `PRODUKT` erstellen
  - aus `ResultSet` ein `Produkt` erzeugen und mehrere Zeilen korrekt mit `next()` lesen
  - `PreparedStatement` mit Produktwerten befüllen
  - INSERT-, UPDATE- und SELECT-Mapping in `DbProduktSpeicher` strukturieren
  - fehlerhafte Datensätze, `null`-Werte, Datentypen und doppelte Mapping-Logik analysieren
  - Mapping auf `AenderungsEintrag` übertragen
  - Transfer zu CSV-Mapping, ORM-Motivation, `Main`-Verantwortung und weiteren Persistenzarten bearbeiten
- [Übungen – Mehrere Tabellen, Beziehungen und Repository](./Uebungen/Uebungen_Tabellen_Beziehungen_Repository.md)
  - Tabellen `PREISAENDERUNG` und `BESTANDSAENDERUNG` mit `PRODUKT_ID` erstellen
  - `PreisAenderung` und `BestandsAenderung` als Modellklassen einordnen
  - `ProduktRepository` und `AenderungsRepository` erstellen und Verantwortlichkeiten prüfen
  - Preis- und Bestandsänderungen mit `PreparedStatement` speichern
  - Änderungen zu einem Produkt mit `ResultSet` laden und sortieren
  - Mapping-Methoden auslagern, doppelte JDBC-Logik bewusst reduzieren und Fehlerfälle behandeln
  - Transfer zu Repository-Nutzen, repetitivem Mapping, stabiler Fachlogik und späteren Persistenzframeworks bearbeiten
- [Übungen – Technisches Logging in Java einführen](./Uebungen/Uebungen_Technisches_Logging.md)
  - Maven-Dependencies für `slf4j-api` und `logback-classic` ergänzen
  - Logger in `ProduktRepository` und `AenderungsRepository` anlegen
  - technische `System.out.println`-Ausgaben durch Logger-Aufrufe ersetzen
  - `DEBUG`, `INFO`, `WARN` und `ERROR` an Repository- und JDBC-Beispielen einsetzen
  - bewusst zu viele Logs erkennen und reduzieren
  - Transfer zu Tests, Fachlogik, sensiblen Daten und Server-Anwendungen bearbeiten
- [Übungen – Technische Konfiguration in Java](./Uebungen/Uebungen_Technische_Konfiguration.md)
  - `app.properties` erstellen und mit `java.util.Properties` laden
  - DB-URL, Dateipfad, H2-Modus und vorbereiteten Logging-Level ausgeben
  - bestehende H2-Konfiguration aus dem Code auslagern
  - `Main` vereinfachen und Konfiguration zentral bündeln
  - fehlende Properties, Standardwerte und ungültige Werte prüfen
  - Embedded- und Server-H2 über Konfigurationsdateien vergleichen
  - Transfer zu Hardcoding, Fachlogik-Abgrenzung und grösseren Anwendungen bearbeiten
- [Übungen – Mehrsprachigkeit mit Locale und ResourceBundle](./Uebungen/Uebungen_I18N_ResourceBundle.md)
  - Sprachdateien `messages_de.properties`, `messages_fr.properties` und `messages_it.properties` erstellen
  - Begrüssungstext und einfache Meldungen über `ResourceBundle` laden
  - `Locale` zwischen Deutsch, Französisch und Italienisch wechseln
  - hartcodierte Texte aus `Main` entfernen
  - einfache Fehlermeldungen übersetzen
  - fehlende Übersetzungen, Standard-Locale und zusätzliche Sprache untersuchen
  - Transfer zu Schweizer Mehrsprachigkeit, Konfigurationsabgrenzung und grösseren Anwendungen bearbeiten
- [Übungen – REST-Schnittstellen mit Spring Boot einführen](./Uebungen/Uebungen_REST_SpringBoot_Einstieg.md)
  - Spring-Boot-Anwendung starten und Port `8080` beobachten
  - ersten `ProduktController` mit `@RestController` und bestehendem `LagerService` erstellen
  - `GET /produkte` und `POST /produkte` mit JSON umsetzen
  - `curl` für `GET`, `POST`, Header, Body und Statuscode-Beobachtung einsetzen
  - mehrere Produkte senden, JSON-Struktur analysieren und Logging bei REST-Aufrufen beobachten
  - Transfer zu unveränderter Fachlogik, REST als Zugriffsschicht, Konsole vs. HTTP, JSON und `curl` bearbeiten

## Repetitionen

Repetitionen kombinieren mehrere bekannte Lerneinheiten und dienen der Diagnose, ob zentrale Konzepte verinnerlicht wurden. Sie liegen getrennt von normalen Übungen unter `Repetitionen/<Name>/` und bestehen standardmässig aus einer Lernenden-Version und einer Lehrpersonen-Version mit gegenseitigen Links.

- [Repetition Java Intro – Lernenden-Version](./Repetitionen/Repetition_Java_Intro/Lernende/Repetition_Java_Intro.md)
  - direkt abgabefähige Repetitionsserie
  - Pflichtteil, Vertiefung und optionale Transferaufgaben
  - Produktverwaltung mit Klassen, Kapselung, `ArrayList` und Methoden
- [Repetition Java Intro – Lehrpersonen-Version](./Repetitionen/Repetition_Java_Intro/Lehrperson/Repetition_Java_Intro_LP.md)
  - gleicher Aufgabenkern mit didaktischen Hinweisen
  - Diagnosehinweise, Beobachtungspunkte, Hilfestellungen und Zeitangaben

## Projekte

Projekte sind grössere, zusammenhängende Mini-Projekte. Sie kombinieren mehrere bisherige Konzepte, verlangen mehr Eigenständigkeit als normale Übungen und werden getrennt nach Lernenden- und Lehrpersonen-Version geführt.

- [Projekte](./Projekte/README.md)
  - Überblick über Zweck, Abgrenzung und Standardstruktur für Mini-Projekte
- [Prozess – Projekt erstellen](./docs/prozesse/projekt_erstellen.md)
  - wiederverwendbare Checkliste für Planung, Struktur, Anforderungen, Reflexion und Bewertungsideen
- [Prozess – Projekt-Review](./docs/prozesse/projekt_review.md)
  - wiederverwendbare Checkliste für Präsentation, Architekturgespräch, Testreview, Refactoring-Ideen und individuelle Lernschritte
- [Skill – projekt-erstellen](./.agents/skills/projekt-erstellen/SKILL.md)
  - Repo-Skill für strukturierte Mini-Projekte mit getrennten Versionen
- [Skill – projekt-review](./.agents/skills/projekt-review/SKILL.md)
  - Repo-Skill für individuelle Projekt-Reviews mit Coaching-Fokus
- [Lagerverwaltung Light](./Projekte/Lagerverwaltung_Light/README.md)
  - ausgearbeitetes Mini-Projekt im fachlichen Kontext einer einfachen Lagerverwaltung
- [Projektauftrag Lagerverwaltung Light – Lernenden-Version](./Projekte/Lagerverwaltung_Light/Lernende/Projektauftrag_Lagerverwaltung_Light.md)
  - offener Projektauftrag mit Ausgangslage, realen Lagerfällen, technischem Rahmen, Pflichtanforderungen, optionalen Erweiterungen, Tests, Abgabe und Reflexion
- [Projektauftrag Lagerverwaltung Light – Lehrpersonen-Version](./Projekte/Lagerverwaltung_Light/Lehrperson/Projektauftrag_Lagerverwaltung_Light_LP.md)
  - ergänzende Hinweise zu didaktischem Zweck, Beobachtungspunkten, Schwierigkeiten, Hilfestellungen, Bewertungsideen und möglichen Lösungsrichtungen
- [Änderungshistorie für Lagerverwaltung](./Projekte/Aenderungshistorie_Lagerverwaltung/README.md)
  - Mini-Projekt zur fachlichen Erweiterung der bekannten Lagerverwaltung um protokollierte Preis- und Bestandsänderungen mit Zeitpunkt, altem Wert, neuem Wert, Änderungsart und Grund
- [Projektauftrag Änderungshistorie für Lagerverwaltung – Lernenden-Version](./Projekte/Aenderungshistorie_Lagerverwaltung/Lernende/Projektauftrag_Aenderungshistorie_Lagerverwaltung.md)
  - offener Projektauftrag mit Ausgangslage, technischem Rahmen, prüfbaren Pflichtanforderungen, speicher- und ladbarer CSV-Historie, optionalen Erweiterungen, Tests, Abgabe, Verantwortlichkeitsbegründung und Reflexion
- [Projektauftrag Änderungshistorie für Lagerverwaltung – Lehrpersonen-Version](./Projekte/Aenderungshistorie_Lagerverwaltung/Lehrperson/Projektauftrag_Aenderungshistorie_Lagerverwaltung_LP.md)
  - ergänzende Hinweise zu didaktischem Zweck, diagnostischen Beobachtungspunkten, Schwierigkeiten, Hilfestellungen, Bewertungsideen, Mindeststandard, Architekturentscheidungen und möglichen Lösungsrichtungen ohne vollständige Musterlösung
- [Projektreview Änderungshistorie für Lagerverwaltung](./Projekte/Aenderungshistorie_Lagerverwaltung/Review/Projektreview_Aenderungshistorie_Lagerverwaltung.md)
  - Coaching-Leitfaden für Einzelreview mit Projektpräsentation, Architekturgespräch, Testreview, Refactoring-Ideen, Reflexion und nächsten Lernschritten
- [Reflexion Änderungshistorie für Lagerverwaltung](./Projekte/Aenderungshistorie_Lagerverwaltung/Review/Reflexion_Aenderungshistorie_Lagerverwaltung.md)
  - kurze Reflexionsvorlage für Lernende zu Projektstruktur, Fachlogik, Tests, Architektur, Refactoring und persönlicher Einschätzung
- [Projektreview Änderungshistorie Architektur](./graphics/projektreview_aenderungshistorie_architektur.svg)
  - begleitende Review-Grafik zu Verantwortlichkeiten, wachsender Fachlogik, Historie, Persistenz und Tests

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
- [Lösungen – Code strukturieren und Verantwortlichkeiten aufteilen](./Musterloesungen/Loesungen_Verantwortlichkeiten_Aufteilen.md)
  - kompakte Standardlösung zur Zuordnung von Verantwortlichkeiten
  - `Main` als Orchestrator, `ProduktVerwaltung` für Fachlogik und CSV-Klassen für Dateilogik
  - sprechende Methodennamen, schrittweises Refactoring und einfache Verantwortlichkeitstabelle
  - Transferhinweise zu Statistik-Service, Export-Idee, Backup-Zuordnung und neuer Klasse oder Methode
  - dokumentierte Validierung mit temporärem Maven-Projekt
- [Lösungen – Interfaces für austauschbare Services](./Musterloesungen/Loesungen_Interfaces_Austauschbare_Services.md)
  - kompakte Standardlösung mit `ProduktSpeicher`, `CsvProduktSpeicher implements ProduktSpeicher` und `Main` mit Interface-Typ
  - Vertrag und Umsetzung unterscheiden
  - Verhalten bleibt gleich, Speicherlogik bleibt in `CsvProduktSpeicher`
  - typische Fehlerhinweise und kurze Transferantworten
  - dokumentierte Validierung mit temporärem Maven-Projekt
- [Lösungen – Mehrere Klassen mit demselben Interface](./Musterloesungen/Loesungen_Mehrere_Implementierungen_Interface.md)
  - kompakte Standardlösung mit `ProduktSpeicher`, `CsvProduktSpeicher implements ProduktSpeicher` und `KonsolenProduktSpeicher implements ProduktSpeicher`
  - `Main` verwendet weiterhin `ProduktSpeicher` als Typ
  - konkrete Implementierung wird zwischen CSV-Datei und Konsolenausgabe ausgetauscht
  - Vertrag, Umsetzung und Nutzung des Vertrags werden kurz unterschieden
  - typische Signatur- und Rollenfehler werden benannt
  - dokumentierte Validierung mit temporärem Maven-Projekt
- [Lösungen – Unterschiedliche Objekte über dasselbe Interface verwenden](./Musterloesungen/Loesungen_Polymorphie_Interface.md)
  - kompakte Standardlösung mit `ProduktSpeicher` als Interface-Typ
  - `CsvProduktSpeicher` und `KonsolenProduktSpeicher` werden nacheinander derselben Variable zugewiesen
  - gleicher Aufruf `speicher.speichern(...)` mit unterschiedlichem beobachtbarem Verhalten
  - praktische Polymorphie kurz erklärt, ohne abstrakte Klassen, `instanceof` oder Downcasting
  - typische Fehlerhinweise und dokumentierte Maven-Verifikation
- [Lösungen – Code-Duplikate vermeiden und gemeinsamen Code wiederverwenden](./Musterloesungen/Loesungen_Code_Wiederverwenden.md)
  - kompakte Standardlösung zum Erkennen ähnlicher Codeblöcke in `CsvProduktSpeicher` und `KonsolenProduktSpeicher`
  - kleine Hilfsmethoden für CSV- und Konsolenformatierung
  - Verhalten nach dem Refactoring prüfen
  - vorsichtiger Ausblick auf gemeinsame Basisklassen, ohne Vererbung zu vertiefen
  - typische Fehlerhinweise und dokumentierte Maven-Verifikation
- [Lösungen – Gemeinsamen Code mit Vererbung wiederverwenden](./Musterloesungen/Loesungen_Vererbung_Code_Wiederverwenden.md)
  - kompakte Standardlösung mit `ProduktSpeicher`, `ProduktSpeicherBasis`, `CsvProduktSpeicher` und `KonsolenProduktSpeicher`
  - gemeinsame Hilfsmethode `produktZeile(...)` in einer kleinen Basisklasse
  - konkrete Speicherlogik bleibt in den konkreten Klassen
  - Interface als Vertrag und Vererbung als gemeinsame Implementierung kurz unterscheiden
  - typische Fehlerhinweise und dokumentierte Maven-Verifikation mit manueller `Main`-Ausführung
- [Lösungen – Fachlogik in Services bündeln](./Musterloesungen/Loesungen_Fachlogik_Services.md)
  - kompakte Standardlösung mit `Produkt`, `LagerService`, `ProduktSpeicher`, `CsvProduktSpeicher` und `Main`
  - Fachlogik im `LagerService`, Persistenz in `CsvProduktSpeicher` und Ablauf in `Main`
  - Beispieltests für Service-Methoden
  - typische Fehlerhinweise und dokumentierte Maven-Verifikation
- [Lösungen – Verantwortlichkeiten und Services festigen](./Musterloesungen/Loesungen_Verantwortlichkeiten_Services_Festigen.md)
  - kompakte Standardlösung zur Verantwortlichkeitszuordnung von `Main`, `Produkt`, `LagerService`, `ProduktSpeicher` und `CsvProduktSpeicher`
  - Diagnose problematischer Strukturen wie Verkaufslogik in `Main` oder Fachregeln in Speicherklassen
  - kleine Refactoring-Beispiele für Verkaufslogik, doppelte Prüfungen, Methodennamen und CSV-Trennung
  - einfache JUnit-Tests für `LagerService` und eine kleine Leerlisten-Prüfung in `Main`
  - typische Fehlerhinweise, kurze Strukturbegründungen und dokumentierte Maven-Verifikation
- [Lösungen – JDBC mit eingebetteter H2-Datenbank](./Musterloesungen/Loesungen_JDBC_H2_Grundlagen.md)
  - kompakte Standardlösung mit H2-Dependency, Embedded-JDBC-URL und vollständiger `DbDemo`
  - `CREATE TABLE`, `INSERT`, `SELECT`, `UPDATE`, `DELETE`, `PreparedStatement` und `ResultSet` nachvollziehbar zeigen
  - Embedded- und Server-Modus kurz vergleichen
  - typische Fehlerhinweise zu Connections, SQL-Strings, `ResultSet.next()` und vermischter Fach-/Persistenzlogik
  - dokumentierte Maven-Verifikation mit temporärem H2-Projekt
- [Lösungen – DbProduktSpeicher mit JDBC und H2](./Musterloesungen/Loesungen_DbProduktSpeicher_JDBC_H2.md)
  - kompakte Standardlösung mit `Produkt`, `ProduktSpeicher`, unverändertem `LagerService`, `DbProduktSpeicher` und `Main`
  - `DbProduktSpeicher implements ProduktSpeicher` mit H2 Embedded, `CREATE TABLE`, `INSERT`, `SELECT`, `UPDATE`, `DELETE`, `PreparedStatement` und `ResultSet`
  - zeigt, dass `Main` nur die konkrete Persistenz austauscht und `LagerService` frei von SQL bleibt
  - Vergleich von CSV- und Datenbank-Persistenz sowie typische Fehlerhinweise
  - dokumentierte Maven-Verifikation mit `mvn test` und ausgeführter `Main`
- [Lösungen – Bestehende Persistenz auf Datenbank erweitern](./Musterloesungen/Loesungen_Persistenz_Datenbank_Erweitern.md)
  - kompakte Standardlösung mit `AenderungsEintrag`, `AenderungsSpeicher`, `DbAenderungsSpeicher` und kleiner `Main`
  - zusätzliche Tabelle `AENDERUNG`, CRUD für Änderungsdaten, `PreparedStatement`, `ResultSet` und Mapping-Hilfsmethode
  - zeigt evolutionäre Architektur: `LagerService` bleibt frei von SQL, `Main` bleibt Ablaufsteuerung
  - Vergleich CSV und Datenbank, typische Fehlerhinweise und Ausblick auf späteres Refactoring
  - dokumentierte Maven-Verifikation mit `mvn package` und ausgeführter `Main`
- [Lösungen – Mapping zwischen Objekten und Datenbank](./Musterloesungen/Loesungen_Objekt_Datenbank_Mapping.md)
  - kompakte Standardlösung für manuelles Mapping im `DbProduktSpeicher`
  - zeigt `ResultSet` zu `Produkt` und `Produkt` zu `PreparedStatement`
  - enthält INSERT-, UPDATE- und SELECT-Mapping mit privaten Hilfsmethoden
  - vergleicht CSV-Mapping und DB-Mapping, nennt typische Fehler und erklärt kurz die spätere Motivation für ORM-Frameworks
  - dokumentierte Maven-Verifikation mit H2 Embedded und ausgeführter `Main`
- [Lösungen – Mehrere Tabellen, Beziehungen und Repository](./Musterloesungen/Loesungen_Tabellen_Beziehungen_Repository.md)
  - kompakte Standardlösung mit `PRODUKT`, `PREISAENDERUNG` und `BESTANDSAENDERUNG`
  - nutzt `PRODUKT_ID` als einfache Beziehung zu `PRODUKT.ID`
  - zeigt `ProduktRepository` und `AenderungsRepository` als strukturierte Persistenzklassen
  - enthält Mapping von `ResultSet` zu `Produkt`, `PreisAenderung` und `BestandsAenderung`
  - enthält Objekt-zu-`PreparedStatement`-Mapping für Produkte, Preisänderungen und Bestandsänderungen
  - zeigt, dass `LagerService` fachlich bleibt und `Main` nur Ablaufsteuerung enthält
  - typische Fehlerhinweise und dokumentierte Maven-Verifikation mit temporärem Prüfprojekt
- [Lösungen – Technisches Logging in Java einführen](./Musterloesungen/Loesungen_Technisches_Logging.md)
  - kompakte Standardlösung mit Maven-Dependencies für SLF4J und Logback
  - zeigt Logger-Deklaration und `logger.info`, `logger.debug`, `logger.warn`, `logger.error`
  - enthält Logging-Beispiele für `ProduktRepository` und `AenderungsRepository`
  - grenzt Logging von `System.out.println`, Fachlogik und Tests ab
  - typische Fehlerhinweise, kurze Reflexionsantworten und dokumentierte Maven-Verifikation
- [Lösungen – Technische Konfiguration in Java](./Musterloesungen/Loesungen_Technische_Konfiguration.md)
  - kompakte Standardlösung mit `config/app.properties`, `KonfigurationLaden`, `AppConfig`, konfigurierter `ProduktRepository`-Erstellung und kleiner `Main`
  - zeigt `java.util.Properties`, Pflichtwerte, Standardwerte und einfache Validierung
  - vergleicht H2 Embedded und Server über unterschiedliche `.properties`-Dateien
  - grenzt technische Konfiguration von Fachlogik, Logging und I18N ab
  - typische Fehlerhinweise, kurze Reflexionsantworten und dokumentierte Maven-Verifikation mit temporärem Prüfprojekt
- [Lösungen – Mehrsprachigkeit mit Locale und ResourceBundle](./Musterloesungen/Loesungen_I18N_ResourceBundle.md)
  - kompakte Standardlösung mit `messages_de.properties`, `messages_fr.properties`, `messages_it.properties`, `Locale`, `ResourceBundle` und kleiner `Main`
  - zeigt sprachabhängige Konsolenausgabe und Entfernen hartcodierter sichtbarer Texte
  - grenzt I18N von technischer Konfiguration ab
  - typische Fehlerhinweise, kurze Reflexionsantworten und dokumentierte Maven-Verifikation mit temporärem Prüfprojekt
- [Lösungen – REST-Schnittstellen mit Spring Boot einführen](./Musterloesungen/Loesungen_REST_SpringBoot_Einstieg.md)
  - kompakte Standardlösung mit Spring-Boot-Startklasse, Web-Starter und `ProduktController`
  - zeigt `GET /produkte`, `GET /produkte/{id}`, `POST /produkte`, `@RequestBody`, `@PathVariable` und automatische JSON-Ausgabe
  - verwendet den bestehenden `LagerService` statt Repositorys direkt aus dem Controller aufzurufen
  - enthält `curl`-Beispiele, Statuscode-Beobachtung, JSON-Einordnung, typische Fehlerhinweise und kurze Reflexionsantworten
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
