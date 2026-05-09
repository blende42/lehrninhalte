# Arbeitsblatt – Java-Packages

## Lernziele

- erklären, wozu Packages in Java verwendet werden
- Package-Namen nach der Konvention mit umgekehrter Domain aufbauen
- `package`-Deklarationen passend zur Ordnerstruktur verwenden
- eigene Klassen aus anderen Packages mit `import` einbinden
- ein kleines Java-Projekt ohne Maven kompilieren, ohne `.class`-Dateien in `src` zu erzeugen

---

## Warum Packages?

Mit mehreren Klassen wird ein Projekt schnell unübersichtlich.

Bisher konnten kleine Beispiele oft in einer Datei stehen. Bei einer Produktverwaltung entstehen aber mehrere Aufgaben:

- `Produkt` beschreibt ein einzelnes Produkt.
- `ProduktVerwaltung` enthält die Logik für mehrere Produkte.
- `Main` startet das Programm.

Packages helfen, solche Klassen fachlich zu ordnen.

---

## Package-Namen als Konvention

In Java verwendet man für eigene Packages meistens die umgekehrte Domain.

Für diese Unterlagen verwenden wir:

```text
ch.allianz.youngoitv
```

Daraus entstehen zum Beispiel:

```text
ch.allianz.youngoitv.produktverwaltung
ch.allianz.youngoitv.produktverwaltung.model
ch.allianz.youngoitv.produktverwaltung.service
```

Warum umgekehrte Domain?

- Eine Domain ist weltweit eindeutig.
- Umgekehrt gelesen beginnt der Package-Name mit dem Land oder der Organisation.
- Danach folgen Projektname und fachliche Bereiche.
- So entstehen weniger Namenskonflikte mit Klassen aus anderen Projekten.

Konventionen:

- Package-Namen werden klein geschrieben.
- Keine Umlaute, Leerzeichen oder Bindestriche verwenden.
- Der Package-Name muss zur Ordnerstruktur passen.

---

## Projektstruktur

Eine einfache Produktverwaltung kann so aufgebaut sein:

```text
produktverwaltung-packages/
  src/
    ch/
      allianz/
        youngoitv/
          produktverwaltung/
            Main.java
            model/
              Produkt.java
            service/
              ProduktVerwaltung.java
  out/
```

`src` enthält nur Quellcode mit `.java`-Dateien.

`out` enthält später die kompilierten `.class`-Dateien. Dieser Ordner wird von `javac` erzeugt oder vorbereitet.

---

## Package-Deklaration

Die Package-Deklaration steht ganz oben in der Java-Datei, direkt nach möglichen Kommentaren.

Datei:

```text
src/ch/allianz/youngoitv/produktverwaltung/model/Produkt.java
```

Code:

```java
package ch.allianz.youngoitv.produktverwaltung.model;

public class Produkt {
    private String name;
    private double preis;
}
```

Wichtig: Ordnerstruktur und Package-Deklaration beschreiben denselben Pfad.

---

## Eigene Klassen importieren

Wenn eine Klasse eine andere Klasse aus einem anderen Package verwendet, braucht es einen Import.

`ProduktVerwaltung` liegt im Package `service`, verwendet aber `Produkt` aus `model`.

```java
package ch.allianz.youngoitv.produktverwaltung.service;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;
import java.util.ArrayList;

public class ProduktVerwaltung {
    private ArrayList<Produkt> produkte = new ArrayList<>();
}
```

Unterschied:

- `java.util.ArrayList` kommt aus der Java-Standardbibliothek.
- `ch.allianz.youngoitv.produktverwaltung.model.Produkt` kommt aus dem eigenen Projekt.

---

## Beispiel: Main

```java
package ch.allianz.youngoitv.produktverwaltung;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;
import ch.allianz.youngoitv.produktverwaltung.service.ProduktVerwaltung;

public class Main {
    public static void main(String[] args) {
        ProduktVerwaltung verwaltung = new ProduktVerwaltung();
        verwaltung.hinzufuegen(new Produkt("Tastatur", 49.90));
        verwaltung.hinzufuegen(new Produkt("Monitor", 179.00));
        verwaltung.hinzufuegen(new Produkt("Maus", 24.50));

        verwaltung.gibAlleAus();
        System.out.println("Gesamtwert: " + verwaltung.berechneGesamtwert());
    }
}
```

`Main` kennt die beiden anderen Klassen nur über ihre Imports.

---

## Kompilieren ohne Maven

Für diesen Einstieg wird bewusst ohne Maven gearbeitet. So bleibt sichtbar, was `javac` und `java` mit Packages machen.

Aus dem Projektordner:

```bash
mkdir -p out
javac -d out $(find src -name "*.java")
```

`-d out` bedeutet: Die kompilierten `.class`-Dateien werden in den Ordner `out` geschrieben.

Danach enthält `out` automatisch wieder die Package-Ordnerstruktur:

```text
out/
  ch/
    allianz/
      youngoitv/
        produktverwaltung/
          Main.class
          model/
            Produkt.class
          service/
            ProduktVerwaltung.class
```

`src` bleibt sauber und enthält nur `.java`-Dateien.

---

## Programm starten

Gestartet wird nicht mit einem Dateipfad, sondern mit dem vollständigen Klassennamen.

```bash
java -cp out ch.allianz.youngoitv.produktverwaltung.Main
```

`-cp out` bedeutet: Java sucht die kompilierten Klassen im Ordner `out`.

---

## Vertiefung: Algorithmen aufteilen

Packages sind nicht nur für Produktverwaltungen nützlich. Auch bekannte Algorithmen können fachlich getrennt werden.

Beispielstruktur:

```text
src/
  ch/
    allianz/
      youngoitv/
        algorithmen/
          Main.java
          algorithms/
            ArrayAlgorithmen.java
            SortierAlgorithmen.java
          simulation/
            PensionskassenSimulation.java
out/
```

Mögliche Aufteilung:

- `ArrayAlgorithmen` enthält Suche, Minimum, Maximum und Zählen.
- `SortierAlgorithmen` enthält Bubble Sort und Selection Sort.
- `PensionskassenSimulation` enthält die längere Simulation.
- `Main` startet nur Beispiele und bleibt kurz.

Wenn `Main` Methoden aus `algorithms` verwendet, braucht es Imports.

```java
import ch.allianz.youngoitv.algorithmen.algorithms.ArrayAlgorithmen;
import ch.allianz.youngoitv.algorithmen.algorithms.SortierAlgorithmen;
```

Die Methoden in diesen Hilfsklassen sind `public static`, damit sie von `Main` direkt aufgerufen werden können.

```java
int minimum = ArrayAlgorithmen.findeMinimum(zahlen);
SortierAlgorithmen.bubbleSort(zahlen);
```

---

## Vertiefung: Simulation aufteilen

Bei einer längeren Simulation hilft eine fachliche Aufteilung besonders.

Beispiel Pensionskassen-Simulation:

```text
src/
  ch/
    allianz/
      youngoitv/
        pensionskasse/
          Main.java
          simulation/
            PensionskassenSimulation.java
          service/
            Beitragssaetze.java
out/
```

Mögliche Verantwortung:

- `Main` startet das Programm.
- `PensionskassenSimulation` enthält die Jahresschleife, die Kapitalberechnung und die CSV-Ausgabe.
- `Beitragssaetze` kennt die Beitragssätze und liefert passende Prozentsätze zurück.

So bleibt sichtbar, welche Klasse welche Aufgabe hat. Die Simulation kann weiterhin ohne Maven kompiliert werden.

```bash
mkdir -p out
javac -d out $(find src -name "*.java")
java -cp out ch.allianz.youngoitv.pensionskasse.Main > pensionskasse.csv
```

---

## Sichtbarkeit und Packages

Mit mehreren Packages wird auch Sichtbarkeit wichtiger.

| Modifier | Bedeutung | Typische Verwendung |
| --- | --- | --- |
| `public` | von überall erreichbar | Klassen und Methoden, die aus anderen Packages verwendet werden |
| `private` | nur in derselben Klasse erreichbar | Attribute und interne Hilfsmethoden |
| kein Modifier | nur im selben Package erreichbar | package-private Hilfsklassen oder Hilfsmethoden |
| `protected` | im selben Package und in Unterklassen erreichbar | später wichtig bei Vererbung |

Beispiel:

```java
public class Beitragssaetze {
    public static double ermittleArbeitgeberSatz(int alter) {
        return ermittleSatzFuerAlter(alter);
    }

    private static double ermittleSatzFuerAlter(int alter) {
        if (alter >= 20 && alter <= 24) {
            return 6.00;
        }

        return 0.0;
    }

    static boolean istAktivesAlter(int alter) {
        return alter >= 20 && alter <= 65;
    }
}
```

Einordnung:

- `Beitragssaetze` ist `public`, weil die Klasse aus einem anderen Package importiert wird.
- `ermittleArbeitgeberSatz` ist `public`, weil die Simulation diese Methode aufruft.
- `ermittleSatzFuerAlter` ist `private`, weil sie nur ein internes Detail ist.
- `istAktivesAlter` hat keinen Modifier und ist deshalb nur im selben Package sichtbar.
- `protected` wird hier nicht benötigt. Es wird später bei Vererbung wichtiger.

---

## Typische Stolpersteine

- Package-Deklaration und Ordnerstruktur passen nicht zusammen.
- Package-Namen enthalten Grossbuchstaben, Umlaute oder Bindestriche.
- `import` für eine eigene Klasse fehlt.
- Klassen oder Methoden sind nicht `public`, obwohl sie aus einem anderen Package verwendet werden.
- Interne Hilfsmethoden sind unnötig `public`.
- `java.util.ArrayList` und eigene Projektklassen werden beim Import verwechselt.
- `.class`-Dateien werden versehentlich in `src` erzeugt.
- Beim Starten wird `java Main` statt des vollständigen Klassennamens verwendet.
- Das Programm wird aus einem falschen Arbeitsverzeichnis kompiliert oder gestartet.

---

## Reflexion

- Warum ist eine umgekehrte Domain als Package-Anfang sinnvoll?
- Welche Klassen gehören in `model`, welche eher in `service`?
- Warum sollen `.class`-Dateien nicht in `src` liegen?
- Was ist beim Starten einer Klasse mit Package anders als bei einer Klasse ohne Package?
