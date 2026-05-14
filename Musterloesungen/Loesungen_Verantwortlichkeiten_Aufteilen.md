# Lösungen – Code strukturieren und Verantwortlichkeiten aufteilen

Diese Musterlösung zeigt eine einfache Standardlösung. Sie bleibt bei der bekannten Produktverwaltung und trennt nur die wichtigsten Verantwortlichkeiten.

Nicht verwendet werden:

- Clean Architecture
- Spring
- formales Repository-Pattern
- Datenbanken
- unnötige Zusatzklassen

---

## Aufgabe 1 – Verantwortlichkeiten zuordnen

| Aufgabe | Klasse |
|---|---|
| Produktname und Preis speichern | `Produkt` |
| Produkt nach Name suchen | `ProduktVerwaltung` |
| Gesamtwert berechnen | `ProduktVerwaltung` |
| CSV-Datei lesen | `CsvProduktLeser` |
| CSV-Datei schreiben | `CsvProduktSpeicher` |
| Programm starten | `Main` |
| Ablauf laden, bearbeiten, speichern auslösen | `Main` |

Merksatz:

```text
Main kennt den Ablauf.
ProduktVerwaltung kennt die Fachlogik.
CSV-Klassen kennen Dateien.
Produkt hält Daten.
```

---

## Aufgaben 2 bis 6 – Main entlasten

### Vorher: Main macht zu viel

Typische problematische Stellen in `Main`:

```text
CSV-Zeilen lesen
CSV-Zeilen mit split(";") zerlegen
Produkte in einer Schleife suchen
Preise direkt ändern
Gesamtwert direkt berechnen
CSV-Zeilen direkt schreiben
```

Diese Logik wird aufgeteilt.

---

## Zielstruktur

```text
src/main/java/
  ch/allianz/youngoitv/produktverwaltung/
    Main.java
    CsvProduktLeser.java
    CsvProduktSpeicher.java
    model/
      Produkt.java
    service/
      ProduktVerwaltung.java
```

---

## Kompakte Standardlösung

### `Produkt.java`

```java
package ch.allianz.youngoitv.produktverwaltung.model;

public class Produkt {
    private String name;
    private double preis;

    public Produkt(String name, double preis) {
        this.name = name;
        this.preis = preis;
    }

    public String getName() {
        return name;
    }

    public double getPreis() {
        return preis;
    }

    public void setPreis(double preis) {
        if (preis >= 0) {
            this.preis = preis;
        }
    }
}
```

Verantwortung: `Produkt` hält Daten. Es liest keine Dateien und berechnet keine Auswertungen über mehrere Produkte.

### `ProduktVerwaltung.java`

```java
package ch.allianz.youngoitv.produktverwaltung.service;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;
import java.util.ArrayList;

public class ProduktVerwaltung {
    private ArrayList<Produkt> produkte;

    public ProduktVerwaltung(ArrayList<Produkt> produkte) {
        this.produkte = produkte;
    }

    public ArrayList<Produkt> getProdukte() {
        return produkte;
    }

    public Produkt findeProdukt(String name) {
        for (Produkt produkt : produkte) {
            if (produkt.getName().equals(name)) {
                return produkt;
            }
        }

        return null;
    }

    public boolean aenderePreis(String name, double neuerPreis) {
        if (neuerPreis < 0) {
            return false;
        }

        Produkt produkt = findeProdukt(name);

        if (produkt == null) {
            return false;
        }

        produkt.setPreis(neuerPreis);
        return true;
    }

    public double berechneGesamtwert() {
        double summe = 0.0;

        for (Produkt produkt : produkte) {
            summe = summe + produkt.getPreis();
        }

        return summe;
    }

    public int zaehleProdukte() {
        return produkte.size();
    }
}
```

Verantwortung: `ProduktVerwaltung` enthält Fachlogik. Sie kennt keine Datei-Befehle.

### `CsvProduktLeser.java`

```java
package ch.allianz.youngoitv.produktverwaltung;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.ArrayList;

public class CsvProduktLeser {
    public ArrayList<Produkt> ladeProdukte(String dateipfad) {
        ArrayList<Produkt> produkte = new ArrayList<>();

        try {
            ArrayList<String> zeilen = new ArrayList<>(Files.readAllLines(Path.of(dateipfad)));

            for (String zeile : zeilen) {
                if (zeile.equalsIgnoreCase("name;preis")) {
                    continue;
                }

                String[] teile = zeile.split(";");

                if (teile.length == 2) {
                    String name = teile[0].trim();

                    try {
                        double preis = Double.parseDouble(teile[1].trim());
                        produkte.add(new Produkt(name, preis));
                    } catch (NumberFormatException e) {
                        System.out.println("Ungültiger Preis in Zeile: " + zeile);
                    }
                }
            }
        } catch (IOException e) {
            System.out.println("Datei konnte nicht gelesen werden: " + dateipfad);
        }

        return produkte;
    }
}
```

Verantwortung: `CsvProduktLeser` liest Dateien und wandelt CSV-Zeilen in Produkte um. Er berechnet keinen Gesamtwert.

### `CsvProduktSpeicher.java`

```java
package ch.allianz.youngoitv.produktverwaltung;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.ArrayList;

public class CsvProduktSpeicher {
    public void speichereProdukte(ArrayList<Produkt> produkte, String dateipfad) {
        ArrayList<String> zeilen = new ArrayList<>();
        zeilen.add("name;preis");

        for (Produkt produkt : produkte) {
            zeilen.add(produkt.getName() + ";" + produkt.getPreis());
        }

        try {
            Files.write(Path.of(dateipfad), zeilen);
        } catch (IOException e) {
            System.out.println("Datei konnte nicht gespeichert werden: " + dateipfad);
        }
    }
}
```

Verantwortung: `CsvProduktSpeicher` schreibt Produkte als CSV-Datei. Er sucht keine Produkte und ändert keine Preise.

### `Main.java`

```java
package ch.allianz.youngoitv.produktverwaltung;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;
import ch.allianz.youngoitv.produktverwaltung.service.ProduktVerwaltung;
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        CsvProduktLeser leser = new CsvProduktLeser();
        ArrayList<Produkt> produkte = leser.ladeProdukte("data/produkte.csv");

        ProduktVerwaltung verwaltung = new ProduktVerwaltung(produkte);

        boolean geaendert = verwaltung.aenderePreis("Maus", 34.90);
        double gesamtwert = verwaltung.berechneGesamtwert();

        CsvProduktSpeicher speicher = new CsvProduktSpeicher();
        speicher.speichereProdukte(verwaltung.getProdukte(), "data/produkte.csv");

        System.out.println("Preis geändert: " + geaendert);
        System.out.println("Anzahl Produkte: " + verwaltung.zaehleProdukte());
        System.out.println("Gesamtwert: " + Math.round(gesamtwert * 10.0) / 10.0);
    }
}
```

Verantwortung: `Main` startet den Ablauf. Die Details liegen in anderen Klassen.

---

## Aufgabe 7 – Schrittweise refaktorieren

Eine sinnvolle Reihenfolge:

```text
1. Ausgangszustand mit mvn test prüfen
2. Produktsuche nach ProduktVerwaltung verschieben
3. mvn test ausführen
4. Preisänderung nach ProduktVerwaltung verschieben
5. mvn test ausführen
6. CSV-Laden nach CsvProduktLeser verschieben
7. mvn test ausführen
8. CSV-Speichern nach CsvProduktSpeicher verschieben
9. mvn test ausführen
```

Wichtig: Nach jedem kleinen Schritt prüfen. So findet man Fehler schneller.

---

## Aufgabe 8 – Doppelte Logik entfernen

Beispiel:

Vorher wird an mehreren Stellen mit einer Schleife nach einem Produkt gesucht.

Besser:

```java
Produkt produkt = verwaltung.findeProdukt("Maus");
```

Die Suchlogik steht nur noch einmal in `ProduktVerwaltung`.

---

## Aufgabe 9 – Sprechende Methodennamen

Gute Methodennamen:

| Aufgabe | Methodenname |
|---|---|
| Produkte laden | `ladeProdukte(...)` |
| Produkte speichern | `speichereProdukte(...)` |
| Produkt suchen | `findeProdukt(...)` |
| Preis ändern | `aenderePreis(...)` |
| Gesamtwert berechnen | `berechneGesamtwert()` |
| Produkte zählen | `zaehleProdukte()` |

Methodennamen sollen sagen, was passiert. Sie sollen nicht nur `mach`, `start` oder `daten` heissen.

---

## Aufgabe 10 – Tests nach dem Refactoring

Die Fachlogik kann ohne CSV-Datei getestet werden.

Beispiel für einfache JUnit-Tests:

```java
package ch.allianz.youngoitv.produktverwaltung.service;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;
import org.junit.jupiter.api.Test;
import java.util.ArrayList;
import static org.junit.jupiter.api.Assertions.*;

class ProduktVerwaltungTest {
    @Test
    void aenderePreisFindetProdukt() {
        ArrayList<Produkt> produkte = new ArrayList<>();
        produkte.add(new Produkt("Maus", 39.50));

        ProduktVerwaltung verwaltung = new ProduktVerwaltung(produkte);

        assertTrue(verwaltung.aenderePreis("Maus", 34.90));
        assertEquals(34.90, produkte.get(0).getPreis(), 0.001);
    }

    @Test
    void aenderePreisGibtFalseWennProduktFehlt() {
        ArrayList<Produkt> produkte = new ArrayList<>();
        ProduktVerwaltung verwaltung = new ProduktVerwaltung(produkte);

        assertFalse(verwaltung.aenderePreis("Drucker", 199.00));
    }

    @Test
    void berechneGesamtwertSummiertPreise() {
        ArrayList<Produkt> produkte = new ArrayList<>();
        produkte.add(new Produkt("Maus", 34.90));
        produkte.add(new Produkt("Tastatur", 79.90));

        ProduktVerwaltung verwaltung = new ProduktVerwaltung(produkte);

        assertEquals(114.80, verwaltung.berechneGesamtwert(), 0.001);
    }
}
```

Hinweis: Diese Tests prüfen `ProduktVerwaltung` direkt. Sie brauchen keine Datei.

---

## Aufgabe 11 – Verantwortlichkeitstabelle

| Klasse | Verantwortung | Darf nicht machen |
|---|---|---|
| `Produkt` | Name und Preis halten | Dateien lesen, Gesamtwert berechnen |
| `ProduktVerwaltung` | Produkte suchen, ändern, zählen und berechnen | CSV-Dateien lesen oder schreiben |
| `CsvProduktLeser` | CSV-Dateien lesen und Produkte erzeugen | Preise ändern, Gesamtwert berechnen |
| `CsvProduktSpeicher` | Produkte als CSV-Datei speichern | Produkte suchen oder Fachregeln prüfen |
| `Main` | Ablauf starten und Methoden aufrufen | Fachlogik und Dateidetails selbst erledigen |

---

## Transfer 1 – Statistik-Service

Eine neue Klasse `ProduktStatistik` ist nur sinnvoll, wenn Statistik deutlich mehr wird als eine einzelne Methode.

Mögliche Methoden:

```text
berechneDurchschnittspreis(...)
findeTeuerstesProdukt(...)
zaehleProdukte(...)
```

Für wenige einfache Methoden darf es in `ProduktVerwaltung` bleiben. Wenn viele Auswertungen dazukommen, kann eine eigene Statistik-Klasse klarer sein.

---

## Transfer 2 – Export-Service

Mögliche Aufteilung:

```text
ProduktExport: entscheidet, welche Produkte exportiert werden
CsvProduktSpeicher: schreibt die CSV-Datei
```

Beispiel: `ProduktExport` könnte später nur Produkte über einem bestimmten Preis auswählen. Das Schreiben der Datei bleibt trotzdem im `CsvProduktSpeicher`.

---

## Transfer 3 – Backup-Funktion

Eine einfache Backup-Funktion kann zuerst in `CsvProduktSpeicher` liegen, weil sie direkt mit Dateioperationen vor dem Speichern zusammenhängt.

Wenn Backup später komplexer wird, zum Beispiel mit Zeitstempel, mehreren Versionen oder Zielordnern, kann eine eigene Klasse sinnvoll werden.

Nicht gut: Backup direkt in `Main`, wenn dort dadurch wieder viele Datei-Details stehen.

---

## Transfer 4 – Neue Klasse oder Methode?

| Erweiterung | Neue Klasse? | Begründung |
|---|---|---|
| Preis eines Produkts ändern | Nein | passt zur Fachlogik in `ProduktVerwaltung` |
| Produkte als CSV speichern | Ja | eigene Dateiverantwortung in `CsvProduktSpeicher` |
| teuerstes Produkt berechnen | Eher nein | kann zuerst in `ProduktVerwaltung` bleiben |
| Backup-Datei erzeugen | Eher nein | kann einfach im `CsvProduktSpeicher` starten |
| Programm starten | Nein | bleibt Aufgabe von `Main` |

Eine neue Klasse lohnt sich, wenn sie eine klare eigene Verantwortung hat und den Code wirklich einfacher macht.

---

## Reflexion – mögliche Antworten

1. Eine Klasse macht zu viel, wenn sie Dateien liest, Fachregeln berechnet, Ausgaben macht und den Ablauf steuert.
2. `Main` als Orchestrator ist sinnvoll, weil der Programmablauf sichtbar bleibt, ohne Detailarbeit zu mischen.
3. Getrennte Verantwortlichkeiten verbessern Tests, weil Fachlogik ohne echte Datei geprüft werden kann.
4. Eine klare Trennung von `Main`, Fachlogik und Dateilogik bereitet spätere Services, Schichten, REST oder Spring vor.

---

## Verifikation

Die Java-Beispiele wurden als temporäres Maven-Projekt unter `/tmp/verantwortlichkeiten-loesung-validierung` geprüft.

Ausgeführter Befehl:

```bash
mvn package
```

Ergebnis:

```text
BUILD SUCCESS
```

Hinweis: In diesem temporären Projekt wurden die Produktionsklassen kompiliert. Die JUnit-Beispiele im Lösungstext zeigen passende Tests, waren dort aber nicht als Testdateien hinterlegt.

Zusätzlich wurde die kompilierte `Main`-Klasse ausgeführt:

```bash
java -cp target/classes ch.allianz.youngoitv.produktverwaltung.Main
```

Die Ausgabe zeigte:

- Produkte wurden aus `data/produkte.csv` geladen
- der Preis von `Maus` wurde geändert
- Produkte wurden wieder gespeichert
- Anzahl und Gesamtwert wurden ausgegeben
