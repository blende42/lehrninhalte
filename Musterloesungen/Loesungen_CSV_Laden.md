# Lösungen – Produktdaten aus CSV-Dateien laden

## Aufgabe 1 – CSV-Zeile verstehen

Gegeben:

```text
Tastatur;79.90
```

Antworten:

1. Produktname: `Tastatur`
2. Preis: `79.90`
3. Trennzeichen: `;`
4. Die Zeile ist Text. Ein `Produkt`-Objekt entsteht erst durch Zerlegen, Parsen und `new Produkt(...)`.

---

## Aufgabe 2 und 3 – Zeile splitten und Preis parsen

```java
String zeile = "Tastatur;79.90";
String[] teile = zeile.split(";");

String name = teile[0];
String preisText = teile[1];
double preis = Double.parseDouble(preisText);

System.out.println(name);
System.out.println(preisText);
System.out.println(preis);
```

Erwartete Ausgabe:

```text
Tastatur
79.90
79.9
```

---

## Aufgabe 4 – Produkt erzeugen

```java
Produkt produkt = new Produkt(name, preis);

System.out.println(produkt.getName());
System.out.println(produkt.getPreis());
```

---

## Standardlösung mit getrennten Klassen

Die Grundlösung enthält auch zwei kleine Transfer-Erweiterungen:

- Kommentarzeilen mit `#` ignorieren
- übersprungene Zeilen zählen

Diese beiden Teile können weggelassen werden, wenn nur der Pflichtteil gelöst werden soll.

### `Produkt.java`

```java
package ch.allianz.youngoitv.produktverwaltung.model;

public class Produkt {
    private String name;
    private double preis;

    public Produkt(String name, double preis) {
        this.name = name;
        setPreis(preis);
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

### `ProduktVerwaltung.java`

```java
package ch.allianz.youngoitv.produktverwaltung.service;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;
import java.util.ArrayList;

public class ProduktVerwaltung {
    public int zaehleProdukte(ArrayList<Produkt> produkte) {
        return produkte.size();
    }

    public double berechneGesamtwert(ArrayList<Produkt> produkte) {
        double summe = 0.0;

        for (int i = 0; i < produkte.size(); i++) {
            summe = summe + produkte.get(i).getPreis();
        }

        return summe;
    }
}
```

### `CsvProduktLeser.java`

```java
package ch.allianz.youngoitv.produktverwaltung;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.ArrayList;

public class CsvProduktLeser {
    private int uebersprungeneZeilen;

    public Produkt parseProdukt(String zeile) {
        String bereinigteZeile = zeile.trim();

        if (bereinigteZeile.isEmpty()) {
            uebersprungeneZeilen++;
            return null;
        }

        if (bereinigteZeile.startsWith("#")) {
            uebersprungeneZeilen++;
            return null;
        }

        String[] teile = bereinigteZeile.split(";");

        if (teile.length != 2) {
            System.out.println("Fehlerhafte Zeile übersprungen: " + zeile);
            uebersprungeneZeilen++;
            return null;
        }

        String name = teile[0].trim();
        String preisText = teile[1].trim();

        try {
            double preis = Double.parseDouble(preisText);
            return new Produkt(name, preis);
        } catch (NumberFormatException e) {
            System.out.println("Ungültiger Preis in Zeile: " + zeile);
            uebersprungeneZeilen++;
            return null;
        }
    }

    public ArrayList<Produkt> ladeProdukte(String dateipfad) {
        ArrayList<Produkt> produkte = new ArrayList<>();
        uebersprungeneZeilen = 0;

        try {
            ArrayList<String> zeilen = new ArrayList<>(Files.readAllLines(Path.of(dateipfad)));

            for (int i = 0; i < zeilen.size(); i++) {
                Produkt produkt = parseProdukt(zeilen.get(i));

                if (produkt != null) {
                    produkte.add(produkt);
                }
            }
        } catch (IOException e) {
            System.out.println("Datei nicht gefunden: " + dateipfad);
        }

        return produkte;
    }

    public int getUebersprungeneZeilen() {
        return uebersprungeneZeilen;
    }
}
```

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

        for (int i = 0; i < produkte.size(); i++) {
            Produkt produkt = produkte.get(i);
            System.out.println(produkt.getName() + ": " + produkt.getPreis());
        }

        ProduktVerwaltung verwaltung = new ProduktVerwaltung();
        System.out.println("Anzahl Produkte: " + verwaltung.zaehleProdukte(produkte));
        System.out.println("Gesamtwert: " + verwaltung.berechneGesamtwert(produkte));
        System.out.println("Übersprungene Zeilen: " + leser.getUebersprungeneZeilen());
    }
}
```

---

## Beispielhafte CSV-Datei

`data/produkte.csv`:

```text
Tastatur;79.90
Monitor;249.00
Maus;39.50
```

Erwartete Ausgabe:

```text
Tastatur: 79.9
Monitor: 249.0
Maus: 39.5
Anzahl Produkte: 3
Gesamtwert: 368.4
Übersprungene Zeilen: 0
```

---

## Fehlerfälle

Beispiel mit Fehlern:

```text
Tastatur;79.90

Monitor;abc
Maus
Kabel;9.90;Aktion
# Kommentar
```

Erwartung:

- `Tastatur` wird geladen.
- Die leere Zeile wird übersprungen.
- `Monitor;abc` wird wegen ungültigem Preis übersprungen.
- `Maus` wird wegen fehlender Spalte übersprungen.
- `Kabel;9.90;Aktion` wird wegen zusätzlicher Spalte übersprungen.
- Kommentarzeilen mit `#` werden optional übersprungen.

---

## Aufgabe 13 – Verantwortung prüfen

1. `CsvProduktLeser` liest die Datei und wandelt CSV-Zeilen in Produkte um.
2. `ProduktVerwaltung` berechnet Anzahl und Gesamtwert.
3. `Main` startet den Ablauf und gibt Resultate aus.
4. In `main` soll keine Parsing- oder Berechnungslogik stehen.

---

## Transfer optional

### Leerzeichen bereinigen

Die Standardlösung nutzt:

```java
String bereinigteZeile = zeile.trim();
String name = teile[0].trim();
String preisText = teile[1].trim();
```

Damit funktioniert auch:

```text
 Tastatur ; 79.90
```

### Kommentare ignorieren

Die Standardlösung überspringt Kommentarzeilen:

```java
if (bereinigteZeile.startsWith("#")) {
    uebersprungeneZeilen++;
    return null;
}
```

### Fehlerhafte Zeilen zählen

Die Variable `uebersprungeneZeilen` wird bei ignorierten oder fehlerhaften Zeilen erhöht.

### Zusätzliches Attribut

Eine mögliche Erweiterung wäre:

```text
Tastatur;79.90;12
```

Dann müsste `Produkt` ein zusätzliches Attribut erhalten, zum Beispiel `bestand`. Für die Grundlösung bleibt es bei `name` und `preis`.

---

## Typische Fehlerhinweise

- Bei `split(",")` wird die Beispielzeile nicht korrekt in zwei Teile zerlegt.
- Ohne `Double.parseDouble(...)` bleibt der Preis ein `String`.
- Ohne `new ArrayList<>()` können keine Produkte hinzugefügt werden.
- Ohne `trim()` führen Leerzeichen schnell zu schwer sichtbaren Fehlern.
- Wenn alles in `main` steht, ist die Dateilogik schlecht von der Fachlogik getrennt.

---

## Verifikation

Die Java-Beispiele wurden als kleines Maven-Projekt unter `/tmp/csv-laden-validierung` geprüft.

Ausgeführter Befehl:

```bash
mvn test
```

Ergebnis:

```text
Tests run: 3, Failures: 0, Errors: 0, Skipped: 0
BUILD SUCCESS
```

Zusätzlich wurde die kompilierte `Main`-Klasse ausgeführt:

```bash
java -cp target/classes ch.allianz.youngoitv.produktverwaltung.Main
```

Die Ausgabe entsprach dem erwarteten Beispiel mit drei geladenen Produkten.
