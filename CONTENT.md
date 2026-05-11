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

### 15. Java-Packages

Ziel: Mehrere Java-Klassen mit Packages strukturieren, Package-Namen nach umgekehrter Domain-Konvention verwenden und ohne Maven sauber nach `out` kompilieren.

Material:

- [Arbeitsblatt – Java-Packages](./Arbeitsblaetter/Arbeitsblatt_Packages.md)
- [Übungen – Java-Packages](./Uebungen/Uebungen_Packages.md)
- [Lösungen – Java-Packages](./Musterloesungen/Loesungen_Packages.md)

### 16. Algorithmen und Datenstrukturen

Ziel: Einfache Algorithmen auf Arrays verstehen, lineare Suche, Minimum, Maximum und Zählen anwenden, Bubble Sort und Selection Sort mit `int[]` nachvollziehen sowie einfache Simulationen mit Schleifen umsetzen.

Material:

- [Arbeitsblatt – Algorithmen und Datenstrukturen](./Arbeitsblaetter/Arbeitsblatt_Algorithmen_Datenstrukturen.md)
- [Arbeitsblatt – Sortieralgorithmen](./Arbeitsblaetter/Arbeitsblatt_Sortieralgorithmen.md)
- [Übungen – Algorithmen und Datenstrukturen](./Uebungen/Uebungen_Algorithmen_Datenstrukturen.md)
- [Lösungen – Algorithmen und Datenstrukturen](./Musterloesungen/Loesungen_Algorithmen_Datenstrukturen.md)

### 17. Maven Einstieg

Ziel: Maven als orchestrierendes Build-Tool verstehen, den bekannten manuellen Build-Prozess mit `javac -d out` und `java -cp out` mit `mvn compile`, `mvn clean`, `src/main/java` und `target` vergleichen sowie `Convention over Configuration` praktisch anwenden.

Material:

- [Arbeitsblatt – Maven Einstieg](./Arbeitsblaetter/Arbeitsblatt_Maven_Einstieg.md)
- [Maven orchestriert den Java-Build](./graphics/maven_orchestriert_build.svg)
- [Übungen – Maven Einstieg](./Uebungen/Uebungen_Maven_Einstieg.md)
- [Lösungen – Maven Einstieg](./Musterloesungen/Loesungen_Maven_Einstieg.md)

### 18. Maven-Projekte ausführen und paketieren

Ziel: `compile`, Programmstart und `package` unterscheiden, `target/classes` und einfache JAR-Dateien als Build-Ergebnisse einordnen, Java-`package` von Maven `package` trennen sowie reproduzierbare Builds als Grundlage für Build-Server und CI/CD vorbereiten.

Material:

- [Arbeitsblatt – Maven-Projekte ausführen und paketieren](./Arbeitsblaetter/Arbeitsblatt_Maven_Ausfuehren_und_Paketieren.md)
- [Maven compile, run und package](./graphics/maven_compile_run_package.svg)
- [Übungen – Maven-Projekte ausführen und paketieren](./Uebungen/Uebungen_Maven_Ausfuehren_und_Paketieren.md)
- [Lösungen – Maven-Projekte ausführen und paketieren](./Musterloesungen/Loesungen_Maven_Ausfuehren_und_Paketieren.md)

### Nächster sinnvoller Block

Nach `Maven-Projekte ausführen und paketieren` bietet sich als nächstes Thema **Maven-Projekte mit einfachen Tests vorbereiten** an:

- Unterschied zwischen manuellen Testausgaben und automatisierten Tests vorbereiten
- Projektstruktur für Tests grob einführen
- JUnit erst dann gezielt und langsam einführen
- externe Dependencies und Maven Central weiterhin bewusst begrenzen

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
