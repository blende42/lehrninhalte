# Lösungen – Produktdaten als CSV-Dateien speichern

## Aufgabe 1 – Produkt als CSV-Zeile darstellen

```java
Produkt produkt = new Produkt("Tastatur", 79.90);
String zeile = produkt.getName() + ";" + produkt.getPreis();

System.out.println(zeile);
```

Erwartete Ausgabe:

```text
Tastatur;79.9
```

---

## Aufgabe 2 und 3 – Methode und mehrere Produkte

```java
public String produktAlsCsvZeile(Produkt produkt) {
    return produkt.getName() + ";" + produkt.getPreis();
}
```

Mehrere Produkte:

```java
ArrayList<String> zeilen = new ArrayList<>();

for (int i = 0; i < produkte.size(); i++) {
    Produkt produkt = produkte.get(i);
    zeilen.add(produktAlsCsvZeile(produkt));
}
```

---

## Standardlösung mit getrennten Klassen

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

Diese Klasse wird hier gebraucht, um gespeicherte Dateien erneut zu laden.

```java
package ch.allianz.youngoitv.produktverwaltung;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.ArrayList;

public class CsvProduktLeser {
    public Produkt parseProdukt(String zeile) {
        String bereinigteZeile = zeile.trim();

        if (bereinigteZeile.isEmpty()) {
            return null;
        }

        String[] teile = bereinigteZeile.split(";");

        if (teile.length != 2) {
            System.out.println("Fehlerhafte Zeile übersprungen: " + zeile);
            return null;
        }

        String name = teile[0].trim();
        String preisText = teile[1].trim();

        try {
            double preis = Double.parseDouble(preisText);
            return new Produkt(name, preis);
        } catch (NumberFormatException e) {
            System.out.println("Ungültiger Preis in Zeile: " + zeile);
            return null;
        }
    }

    public ArrayList<Produkt> ladeProdukte(String dateipfad) {
        ArrayList<Produkt> produkte = new ArrayList<>();

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
}
```

### `CsvProduktSpeicher.java`

```java
package ch.allianz.youngoitv.produktverwaltung;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.ArrayList;

public class CsvProduktSpeicher {
    public String produktAlsCsvZeile(Produkt produkt) {
        return produkt.getName().trim() + ";" + produkt.getPreis();
    }

    public void speichereProdukte(ArrayList<Produkt> produkte, String dateipfad) {
        ArrayList<String> zeilen = new ArrayList<>();

        for (int i = 0; i < produkte.size(); i++) {
            Produkt produkt = produkte.get(i);

            if (istGueltig(produkt)) {
                zeilen.add(produktAlsCsvZeile(produkt));
            }
        }

        try {
            Files.write(Path.of(dateipfad), zeilen);
        } catch (IOException e) {
            System.out.println("Datei konnte nicht gespeichert werden: " + dateipfad);
        }
    }

    private boolean istGueltig(Produkt produkt) {
        if (produkt == null) {
            System.out.println("Produkt wird nicht gespeichert: null");
            return false;
        }

        if (produkt.getName() == null || produkt.getName().trim().isEmpty()) {
            System.out.println("Produkt wird nicht gespeichert: leerer Name");
            return false;
        }

        if (produkt.getPreis() < 0) {
            System.out.println("Produkt wird nicht gespeichert: negativer Preis");
            return false;
        }

        return true;
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
        ArrayList<Produkt> produkte = new ArrayList<>();
        produkte.add(new Produkt("Tastatur", 79.90));
        produkte.add(new Produkt("Monitor", 249.00));
        produkte.add(new Produkt("Maus", 39.50));

        CsvProduktSpeicher speicher = new CsvProduktSpeicher();
        speicher.speichereProdukte(produkte, "data/produkte.csv");

        CsvProduktLeser leser = new CsvProduktLeser();
        ArrayList<Produkt> geladeneProdukte = leser.ladeProdukte("data/produkte.csv");

        ProduktVerwaltung verwaltung = new ProduktVerwaltung();
        System.out.println("Anzahl Produkte: " + verwaltung.zaehleProdukte(geladeneProdukte));
        System.out.println("Gesamtwert: " + verwaltung.berechneGesamtwert(geladeneProdukte));
    }
}
```

Erwartete Ausgabe:

```text
Anzahl Produkte: 3
Gesamtwert: 368.4
```

Erwarteter Dateiinhalt in `data/produkte.csv`:

```text
Tastatur;79.9
Monitor;249.0
Maus;39.5
```

---

## Aufgabe 8 – Leere Produktliste speichern

```java
ArrayList<Produkt> leereListe = new ArrayList<>();

CsvProduktSpeicher speicher = new CsvProduktSpeicher();
speicher.speichereProdukte(leereListe, "data/produkte.csv");
```

Erwartung:

- Die Datei wird geschrieben.
- Die Datei enthält keine Produktzeilen.
- Beim erneuten Laden entstehen null Produkte.

---

## Aufgabe 9 – Überschreiben prüfen

```java
ArrayList<Produkt> einProdukt = new ArrayList<>();
einProdukt.add(new Produkt("Maus", 39.50));

CsvProduktSpeicher speicher = new CsvProduktSpeicher();
speicher.speichereProdukte(einProdukt, "data/produkte.csv");
```

Erwarteter Dateiinhalt:

```text
Maus;39.5
```

Hinweis: `Files.write(...)` ersetzt den bisherigen Dateiinhalt. Es wird nicht angehängt.

---

## Aufgabe 10 – Ungültige Produkte

Die Standardlösung prüft vor dem Speichern:

- Produkt ist nicht `null`
- Name ist nicht leer
- Preis ist nicht negativ

Wenn `Produkt` bereits im Konstruktor oder in Settern prüft, kann diese Prüfung dort liegen. In dieser Lösung prüft `CsvProduktSpeicher` nochmals ruhig vor dem Schreiben und überspringt ungültige Produkte.

Beispiel:

```java
produkte.add(new Produkt("", 10.00));
produkte.add(new Produkt("Kabel", -5.00));
```

Erwartung:

```text
Produkt wird nicht gespeichert: leerer Name
Produkt wird nicht gespeichert: negativer Preis
```

Die übrigen gültigen Produkte werden trotzdem gespeichert.

---

## Kurze manuelle Prüfungen

- Drei Produkte speichern und erneut laden: Anzahl `3`
- Gesamtwert nach erneutem Laden: `368.4`
- Leere Liste speichern und erneut laden: Anzahl `0`
- Zuerst drei Produkte, danach ein Produkt speichern: Die Datei enthält nur die zuletzt gespeicherte Liste.

---

## Optional – Einfacher StringBuilder

Für zwei Felder reicht String-Verkettung. Wenn später mehr Felder dazukommen, kann ein einfacher `StringBuilder` verwendet werden:

```java
public String produktAlsCsvZeileMitStringBuilder(Produkt produkt) {
    StringBuilder builder = new StringBuilder();
    builder.append(produkt.getName().trim());
    builder.append(";");
    builder.append(produkt.getPreis());
    return builder.toString();
}
```

Für die Grundlösung ist diese Variante nicht nötig.

---

## Verantwortung prüfen

1. `CsvProduktSpeicher` wandelt Produkte in CSV-Zeilen um und schreibt die Datei.
2. `CsvProduktLeser` liest die Datei und erzeugt wieder Produkte.
3. `ProduktVerwaltung` berechnet Anzahl und Gesamtwert.
4. `Main` startet nur den Ablauf und enthält keine Datei- oder Fachlogik.

---

## Typische Fehlerhinweise

- Wenn `;` fehlt, kann der Leser die Zeile später nicht korrekt mit `split(";")` zerlegen.
- Wenn die Datei angehängt statt überschrieben wird, entstehen doppelte Produkte.
- Wenn die Speicherlogik in `main` bleibt, ist die Trennung der Verantwortlichkeiten schlecht.
- Wenn eine leere Liste als Fehler behandelt wird, wird ein gültiger Fall unnötig kompliziert.
- Wenn Preistexte mit Komma gespeichert werden, kann `Double.parseDouble(...)` sie später nicht lesen.

---

## Verifikation

Die Java-Beispiele wurden als kleines Maven-Projekt unter `/tmp/csv-speichern-loesung-validierung` geprüft.

Ausgeführter Befehl:

```bash
mvn test
```

Ergebnis:

```text
BUILD SUCCESS
```

Zusätzlich wurde die kompilierte `Main`-Klasse ausgeführt:

```bash
java -cp target/classes ch.allianz.youngoitv.produktverwaltung.Main
```

Die Ausgabe zeigte drei erneut geladene Produkte und den Gesamtwert `368.4`. Die erzeugte Datei `data/produkte.csv` enthielt die erwarteten CSV-Zeilen.
