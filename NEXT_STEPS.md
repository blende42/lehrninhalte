# Übergabe – aktueller Stand und nächste Schritte

Diese Datei dient als kurzer Einstiegspunkt für eine neue Session.

## Aktueller Stand

Die Unterrichtssequenz ist in [CONTENT.md](./CONTENT.md) als empfohlene Reihenfolge dokumentiert.

Aktuell vorbereitet sind:

1. Primitive Datentypen, Wrapper und Parsing
2. String-Grundlagen
3. String-Vertiefung und einfache Textverarbeitung
4. Mini-Projekt Parser
5. StringBuilder
6. Arrays
7. Arrays vertiefen
8. 2D-Arrays
9. Methoden
10. Methoden festigen und Refactoring
11. Klassen und Objekte
12. Kapselung, Getter und Setter
13. Objektarrays und Verwaltungslogik
14. ArrayList
15. Java-Packages
16. Algorithmen und Datenstrukturen

Die zuletzt erstellte Einheit ist **Algorithmen und Datenstrukturen**. In derselben Session wurde ausserdem der Block **Java-Packages** erstellt und danach mit einer Vertiefung zu Algorithmen in Packages ergänzt.

Neue Package-Dateien:

- [Arbeitsblatt_Packages.md](./Arbeitsblaetter/Arbeitsblatt_Packages.md)
- [Uebungen_Packages.md](./Uebungen/Uebungen_Packages.md)
- [Loesungen_Packages.md](./Musterloesungen/Loesungen_Packages.md)

Neue Algorithmen-Dateien:

- [Arbeitsblatt_Algorithmen_Datenstrukturen.md](./Arbeitsblaetter/Arbeitsblatt_Algorithmen_Datenstrukturen.md)
- [Arbeitsblatt_Sortieralgorithmen.md](./Arbeitsblaetter/Arbeitsblatt_Sortieralgorithmen.md)
- [Uebungen_Algorithmen_Datenstrukturen.md](./Uebungen/Uebungen_Algorithmen_Datenstrukturen.md)
- [Loesungen_Algorithmen_Datenstrukturen.md](./Musterloesungen/Loesungen_Algorithmen_Datenstrukturen.md)

Wichtige Inhalte aus der letzten Session:

- Package-Domain: `ch.allianz.youngoitv`
- Packages mit umgekehrter Domain, Ordnerstruktur, Imports und Kompilieren ohne Maven nach `out`
- Package-Block enthält einen kompakten Sichtbarkeitsabschnitt zu `public`, `private`, package-private und `protected` als Ausblick
- Vertiefungsübung: `ArrayAlgorithmen`, `SortierAlgorithmen` und `Main` in Packages aufteilen
- Vertiefungsübung Aufgabe 12: Pensionskassen-Simulation in `Main`, `simulation/PensionskassenSimulation` und `service/Beitragssaetze` aufteilen
- Algorithmen-Einstieg mit linearer Suche, Minimum, Maximum und Zählen
- Sortieralgorithmen mit `int[]`: Bubble Sort und Selection Sort
- Transfer: Preise mit `double[]` und optional Produkte nach Preis sortieren
- Zusatzübung Zinseszins: normale Zinsformel in einer Schleife, keine Potenzformel
- Zusatzübung Pensionskasse: Kapitalentwicklung von Alter 20 bis 65 mit Mini, Standard und Maxi
- Pensionskassenübung nutzt Sparbeiträge aus Anhang A-3 des lokalen Dokuments `/home/pm/Dokumente/Bvg/PK_AS_ID_2022_def.pdf`
- Vereinfachung Pensionskasse: zuerst vorhandenes Kapital verzinsen, danach Arbeitnehmer- und Arbeitgeber-Sparbeiträge gutschreiben
- CSV-Ausgabe mit Semikolon und stdout-Weiterleitung, danach Import in Excel und Liniendiagramm

## Nächster geplanter Block

Als nächstes kann das Thema **mehrdateilige Java-Projekte vertiefen oder Einstieg in Maven** vorbereitet werden.

Sinnvolle Inhalte:

- bestehende Produktverwaltung mit Packages nochmals praktisch festigen
- Unterschied zwischen manuellem Kompilieren und Build-Tool sichtbar machen
- Nutzen von Maven für Standardstruktur, Abhängigkeiten und wiederholbare Builds erklären
- `src/main/java` als Maven-Konvention vorbereiten
- bekannte Befehle mit `javac -d out` und `java -cp out` mit Maven-Zielen vergleichen
- typische Fehler:
  - manuelle `out`-Struktur mit Maven-`target` verwechseln
  - aus dem falschen Arbeitsverzeichnis starten
  - Package-Struktur in `src/main/java` falsch abbilden
  - Maven zu früh als Magie verwenden, ohne Classpath verstanden zu haben

## Passender Anschluss

Der nächste Block sollte an die Produktverwaltung mit `ArrayList`, Packages und den Algorithmen-Übungen anschliessen.

Aktuelle einfache Struktur im Package-Block:

```text
src/
  ch/allianz/youngoitv/produktverwaltung/
    Main.java
    model/
      Produkt.java
    service/
      ProduktVerwaltung.java
out/
```

Didaktisch sinnvoll ist als nächstes ein Vergleich:

- ohne Maven: `src`, `out`, `javac -d out`, `java -cp out`
- mit Maven: `src/main/java`, `target`, `mvn compile`, `mvn exec:java` oder später ein JAR

Die Package-Wiederholungsübung mit der Pensionskassen-Simulation wurde bereits als Aufgabe 12 im bestehenden Package-Übungsblatt ergänzt. Der nächste fachlich sinnvolle Schritt ist deshalb der Maven-Einstieg.

Empfohlener Startprompt für die nächste Session:

```text
Bitte lies AGENTS.md und NEXT_STEPS.md. Danach briefe mich kurz zum geplanten Block "Maven Einstieg", bevor du Dateien änderst. Der Block soll an Java-Packages, die Produktverwaltung und die Algorithmen-/Pensionskassenübungen anschliessen.
```

Mögliche neue Dateien für den Maven-Einstieg:

- `Arbeitsblaetter/Arbeitsblatt_Maven_Einstieg.md`
- `Uebungen/Uebungen_Maven_Einstieg.md`
- `Musterloesungen/Loesungen_Maven_Einstieg.md`

Beim Erstellen des Maven-Blocks `README.md`, `CONTENT.md` und `NEXT_STEPS.md` wieder mitführen.

## Verifikation der zuletzt erstellten Einheiten

Für die letzten Java-Einheiten wurden temporäre Testklassen unter `/tmp` erstellt und geprüft:

- Methoden
- Methoden-Festigung
- Klassen und Objekte
- Kapselung, Getter und Setter
- Objektarrays und Verwaltungslogik
- ArrayList
- Java-Packages
- Algorithmen und Datenstrukturen

Die Java-Beispiele wurden mit `javac` kompiliert und mit `java` ausgeführt. Der Package-Block wurde ohne Maven mit Ausgabe nach `out` geprüft, inklusive Vertiefung mit `ArrayAlgorithmen`, `SortierAlgorithmen` und aufgeteilter Pensionskassen-Simulation. Der Algorithmen-Block wurde mit temporären Testklassen kompiliert und ausgeführt, inklusive Zinseszins, Sortierung und Pensionskassen-Simulation mit CSV-Ausgabe. SVG-Grafiken zu Klassen/Kapselung wurden mit `xmllint` geprüft und mit `rsvg-convert` gerendert.

## Wichtige Repo-Regeln

- Deutsch mit Locale `de_CH`.
- Schweizer Hochdeutsch mit `ss` statt Eszett.
- Dateinamen nur mit ASCII-Zeichen.
- Bei neuen oder geänderten Inhalten `README.md` und `CONTENT.md` mitführen.
- Java-Beispiele klein und auf EFZ-Niveau halten.
- Keine Git-Schreibaktionen ausführen, ausser sie werden ausdrücklich verlangt.
