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

Die zuletzt erstellte Einheit ist **ArrayList**:

- [Arbeitsblatt_ArrayList.md](./Arbeitsblaetter/Arbeitsblatt_ArrayList.md)
- [Uebungen_ArrayList.md](./Uebungen/Uebungen_ArrayList.md)
- [Loesungen_ArrayList.md](./Musterloesungen/Loesungen_ArrayList.md)

## Nächster geplanter Block

Als nächstes soll das Konzept der **Java-Packages** erläutert werden.

Sinnvolle Inhalte:

- Warum Pakete verwendet werden
- `package`-Deklaration am Anfang einer Java-Datei
- Ordnerstruktur passend zum Package-Namen
- `import` für Klassen aus anderen Paketen
- Unterschied zwischen Standardbibliothek-Import und eigenen Klassen
- einfache Projektstruktur mit mehreren Klassen
- typische Fehler:
  - Package-Deklaration passt nicht zur Ordnerstruktur
  - Import fehlt
  - falscher Klassenname oder falscher Pfad
  - Startklasse liegt im falschen Package

## Passender Anschluss

Der Block sollte an die Produktverwaltung mit `ArrayList` anschliessen.

Mögliche einfache Struktur:

```text
src/
  ch/beispiel/verwaltung/
    Main.java
  ch/beispiel/model/
    Produkt.java
  ch/beispiel/service/
    ProduktVerwaltung.java
```

Didaktisch sinnvoll ist zuerst eine kleine Struktur mit maximal drei Packages:

- `model` für Datenklassen wie `Produkt`
- `service` oder `verwaltung` für Logik
- ein Hauptpackage mit `Main`

## Verifikation der zuletzt erstellten Einheiten

Für die letzten Java-Einheiten wurden temporäre Testklassen unter `/tmp` erstellt und geprüft:

- Methoden
- Methoden-Festigung
- Klassen und Objekte
- Kapselung, Getter und Setter
- Objektarrays und Verwaltungslogik
- ArrayList

Die Java-Beispiele wurden mit `javac` kompiliert und mit `java` ausgeführt. SVG-Grafiken zu Klassen/Kapselung wurden mit `xmllint` geprüft und mit `rsvg-convert` gerendert.

## Wichtige Repo-Regeln

- Deutsch mit Locale `de_CH`.
- Schweizer Hochdeutsch mit `ss` statt Eszett.
- Dateinamen nur mit ASCII-Zeichen.
- Bei neuen oder geänderten Inhalten `README.md` und `CONTENT.md` mitführen.
- Java-Beispiele klein und auf EFZ-Niveau halten.
- Keine Git-Schreibaktionen ausführen, ausser sie werden ausdrücklich verlangt.
