# Übungen – Java-Packages

## Basis

### Aufgabe 1 – Package und Ordner zuordnen

Ordne die Package-Deklaration dem passenden Ordner zu.

Package:

```java
package ch.allianz.youngoitv.produktverwaltung.model;
```

Welcher Ordner ist korrekt?

```text
src/ch/allianz/youngoitv/produktverwaltung/model/
src/ch/allianz/youngoitv/model/produktverwaltung/
src/produktverwaltung/ch/allianz/youngoitv/model/
```

---

### Aufgabe 2 – Package-Deklarationen ergänzen

Ergänze für jede Datei die passende `package`-Zeile.

```text
src/ch/allianz/youngoitv/produktverwaltung/Main.java
src/ch/allianz/youngoitv/produktverwaltung/model/Produkt.java
src/ch/allianz/youngoitv/produktverwaltung/service/ProduktVerwaltung.java
```

---

### Aufgabe 3 – Konvention prüfen

Welche Package-Namen passen zur Java-Konvention?

```text
ch.allianz.youngoitv.produktverwaltung
ch.Allianz.YoungOITV.Produktverwaltung
ch.allianz.youngoitv.produkt-verwaltung
ch.allianz.youngoitv.produktverwaltung.service
```

Begründe kurz.

---

## Aufbau

### Aufgabe 4 – Produktklasse in ein Package legen

Erstelle die Datei:

```text
src/ch/allianz/youngoitv/produktverwaltung/model/Produkt.java
```

Vorgaben:

- Package: `ch.allianz.youngoitv.produktverwaltung.model`
- Attribute: `name`, `preis`
- Konstruktor mit Name und Preis
- Getter für beide Attribute
- Setter für `preis` mit Prüfung auf `>= 0`
- Methode `ausgeben`

---

### Aufgabe 5 – ProduktVerwaltung in ein Package legen

Erstelle die Datei:

```text
src/ch/allianz/youngoitv/produktverwaltung/service/ProduktVerwaltung.java
```

Vorgaben:

- Package: `ch.allianz.youngoitv.produktverwaltung.service`
- Verwende intern eine `ArrayList<Produkt>`.
- Importiere `Produkt`.
- Importiere `ArrayList`.
- Schreibe die Methoden:
  - `hinzufuegen(Produkt produkt)`
  - `gibAlleAus()`
  - `berechneGesamtwert()`
  - `findeProdukt(String name)`

---

### Aufgabe 6 – Main mit Imports schreiben

Erstelle die Datei:

```text
src/ch/allianz/youngoitv/produktverwaltung/Main.java
```

Vorgaben:

- Package: `ch.allianz.youngoitv.produktverwaltung`
- Importiere `Produkt`.
- Importiere `ProduktVerwaltung`.
- Erstelle eine Verwaltung.
- Füge drei Produkte hinzu.
- Gib alle Produkte und den Gesamtwert aus.
- Suche nach `"Maus"` und prüfe das Resultat auf `null`.

---

## Vertiefung

### Aufgabe 7 – Fehler finden

Die Datei liegt hier:

```text
src/ch/allianz/youngoitv/produktverwaltung/model/Produkt.java
```

Der Code beginnt so:

```java
package ch.allianz.youngoitv.produktverwaltung.service;
```

Was ist falsch? Korrigiere die Package-Deklaration.

---

### Aufgabe 8 – Ohne Maven kompilieren

Kompiliere das Projekt ohne Maven.

Vorgaben:

- `.class`-Dateien dürfen nicht in `src` entstehen.
- Verwende den Ausgabeordner `out`.
- Starte danach die Klasse `Main`.

Notiere die zwei Befehle zum Kompilieren und Starten.

---

### Aufgabe 9 – Classpath erklären

Erkläre in eigenen Worten:

```bash
java -cp out ch.allianz.youngoitv.produktverwaltung.Main
```

Gehe auf diese Punkte ein:

- Wofür steht `-cp out`?
- Warum steht am Schluss kein Dateipfad?
- Warum reicht `java Main` nicht?

---

## Transfer

### Aufgabe 10 – Kundenverwaltung strukturieren

Erstelle eine zweite kleine Struktur nach demselben Muster.

```text
src/ch/allianz/youngoitv/kundenverwaltung/
  Main.java
  model/Kunde.java
  service/KundenVerwaltung.java
```

Vorgaben:

- `Kunde` hat `name` und `kundennummer`.
- `KundenVerwaltung` speichert Kunden in einer `ArrayList`.
- `Main` erstellt mindestens zwei Kunden und gibt sie aus.
- Kompiliere nach `out`.
- Starte mit dem vollständigen Klassennamen.

---

### Aufgabe 11 – Algorithmen in Packages aufteilen

Teile bekannte Algorithmen aus dem Algorithmen-Block in mehrere Klassen auf.

Erstelle diese Struktur:

```text
src/ch/allianz/youngoitv/algorithmen/
  Main.java
  algorithms/ArrayAlgorithmen.java
  algorithms/SortierAlgorithmen.java
```

Vorgaben für `ArrayAlgorithmen`:

- Package: `ch.allianz.youngoitv.algorithmen.algorithms`
- Methoden:
  - `enthaelt(int[] zahlen, int gesucht)`
  - `findeMinimum(int[] zahlen)`
  - `findeMaximum(int[] zahlen)`
  - `zaehleMindestens(int[] zahlen, int grenze)`

Vorgaben für `SortierAlgorithmen`:

- Package: `ch.allianz.youngoitv.algorithmen.algorithms`
- Methoden:
  - `bubbleSort(int[] zahlen)`
  - `selectionSort(int[] zahlen)`

Vorgaben für `Main`:

- Package: `ch.allianz.youngoitv.algorithmen`
- Importiere `ArrayAlgorithmen`.
- Importiere `SortierAlgorithmen`.
- Erstelle ein `int[]`.
- Gib Minimum, Maximum und Suchresultat aus.
- Sortiere ein Array mit Bubble Sort und gib es aus.

Kompiliere ohne Maven:

```bash
mkdir -p out
javac -d out $(find src -name "*.java")
```

Starte:

```bash
java -cp out ch.allianz.youngoitv.algorithmen.Main
```

Kontrolliere danach, dass in `src` keine `.class`-Dateien entstanden sind.

---

### Aufgabe 12 – Pensionskassen-Simulation in Packages aufteilen

Teile die Pensionskassen-Simulation aus dem Algorithmen-Block in mehrere Klassen auf.

Erstelle diese Struktur:

```text
src/ch/allianz/youngoitv/pensionskasse/
  Main.java
  simulation/PensionskassenSimulation.java
  service/Beitragssaetze.java
```

Vorgaben für `Beitragssaetze`:

- Package: `ch.allianz.youngoitv.pensionskasse.service`
- Methoden:
  - `ermittleArbeitnehmerSatz(int alter, String variante)`
  - `ermittleArbeitgeberSatz(int alter)`
- Die Methode für Arbeitnehmer kennt die Varianten `Mini`, `Standard` und `Maxi`.

Vorgaben für `PensionskassenSimulation`:

- Package: `ch.allianz.youngoitv.pensionskasse.simulation`
- Importiere `Beitragssaetze`.
- Simuliere Alter `20` bis `65`.
- Verwende variable Jahreslöhne und Zinssätze.
- Verzinsung erfolgt am Anfang jedes Jahres.
- Danach werden Arbeitnehmer- und Arbeitgeber-Sparbeiträge gutgeschrieben.
- Gib CSV-Zeilen mit Semikolon aus.

Vorgaben für `Main`:

- Package: `ch.allianz.youngoitv.pensionskasse`
- Importiere `PensionskassenSimulation`.
- Starte die Simulation.

Kompiliere ohne Maven:

```bash
mkdir -p out
javac -d out $(find src -name "*.java")
```

Starte mit stdout-Weiterleitung:

```bash
java -cp out ch.allianz.youngoitv.pensionskasse.Main > pensionskasse.csv
```

Öffne `pensionskasse.csv` in Excel und erstelle ein Liniendiagramm mit den Varianten `Mini`, `Standard` und `Maxi`.

Kontrolliere danach:

- `src` enthält nur `.java`-Dateien.
- `out` enthält die `.class`-Dateien.
- `pensionskasse.csv` enthält eine Kopfzeile und die Jahre von Alter `20` bis `65`.

Sichtbarkeitsfrage:

- Welche Klassen und Methoden müssen `public` sein, weil sie aus einem anderen Package verwendet werden?
- Welche Hilfsmethoden könnten `private` bleiben?
- Wo wäre kein Modifier möglich, wenn eine Methode nur im selben Package verwendet wird?

---

## Reflexion

- Welche Vorteile bringen Packages bei mehreren Klassen?
- Warum beginnt das Package mit `ch.allianz.youngoitv`?
- Welche Dateien brauchen Imports für eigene Klassen?
- Wie stellst du sicher, dass `src` keine `.class`-Dateien enthält?
- Welche Algorithmen gehören sinnvoll in dieselbe Klasse?
- Welche Klasse sollte bei der Pensionskassen-Simulation die Beitragssätze kennen?
- Warum sollte nicht jede Methode automatisch `public` sein?
