# Lösungen – Persistenzablauf vertiefen

Diese Musterlösung zeigt eine kompakte Standardlösung. Sie bleibt bewusst bei einfachen Klassen, `ArrayList`, Schleifen und klaren Rückgabewerten.

Nicht verwendet werden:

- Datenbanken
- JSON
- Streams API
- generische CSV-Frameworks
- komplexe Exception-Hierarchien
- formales Repository-Pattern

---

## Aufgaben 1 bis 8 – Grundablauf

Der vollständige Ablauf ist:

```text
CSV-Datei laden
-> Produkte in ArrayList verwalten
-> Produkt hinzufügen
-> Preis ändern
-> Produkte speichern
-> Datei erneut laden
-> Änderungen prüfen
```

Vor dem Laden liegen die Daten in `data/produkte.csv`. Nach dem Laden liegen sie zusätzlich als `ArrayList<Produkt>` im Arbeitsspeicher. Dauerhaft wird eine Änderung erst nach dem Speichern.

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
    private ArrayList<Produkt> produkte;

    public ProduktVerwaltung(ArrayList<Produkt> produkte) {
        this.produkte = produkte;
    }

    public ArrayList<Produkt> getProdukte() {
        return produkte;
    }

    public void fuegeProduktHinzu(Produkt produkt) {
        produkte.add(produkt);
    }

    public boolean aenderePreis(String name, double neuerPreis) {
        if (neuerPreis < 0) {
            return false;
        }

        for (int i = 0; i < produkte.size(); i++) {
            Produkt produkt = produkte.get(i);

            if (produkt.getName().equals(name)) {
                produkt.setPreis(neuerPreis);
                return true;
            }
        }

        return false;
    }

    public Produkt findeProdukt(String name) {
        for (int i = 0; i < produkte.size(); i++) {
            Produkt produkt = produkte.get(i);

            if (produkt.getName().equals(name)) {
                return produkt;
            }
        }

        return null;
    }

    public double berechneGesamtwert() {
        double summe = 0.0;

        for (int i = 0; i < produkte.size(); i++) {
            summe = summe + produkte.get(i).getPreis();
        }

        return summe;
    }

    public int zaehleProdukte() {
        return produkte.size();
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
    private int fehlerhafteZeilen;

    public int getFehlerhafteZeilen() {
        return fehlerhafteZeilen;
    }

    public ArrayList<Produkt> ladeProdukte(String dateipfad) {
        ArrayList<Produkt> produkte = new ArrayList<>();
        fehlerhafteZeilen = 0;

        try {
            ArrayList<String> zeilen = new ArrayList<>(Files.readAllLines(Path.of(dateipfad)));

            for (int i = 0; i < zeilen.size(); i++) {
                String zeile = zeilen.get(i).trim();

                if (zeile.isEmpty()) {
                    continue;
                }

                if (istKopfzeile(zeile)) {
                    continue;
                }

                Produkt produkt = parseProdukt(zeile);

                if (produkt != null) {
                    produkte.add(produkt);
                }
            }
        } catch (IOException e) {
            System.out.println("Datei konnte nicht gelesen werden: " + dateipfad);
        }

        return produkte;
    }

    private boolean istKopfzeile(String zeile) {
        return zeile.equalsIgnoreCase("name;preis");
    }

    private Produkt parseProdukt(String zeile) {
        String[] teile = zeile.split(";");

        if (teile.length != 2) {
            fehlerhafteZeilen++;
            return null;
        }

        String name = teile[0].trim();
        String preisText = teile[1].trim();

        if (name.isEmpty()) {
            fehlerhafteZeilen++;
            return null;
        }

        try {
            double preis = Double.parseDouble(preisText);
            return new Produkt(name, preis);
        } catch (NumberFormatException e) {
            fehlerhafteZeilen++;
            return null;
        }
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
import java.nio.file.StandardCopyOption;
import java.util.ArrayList;

public class CsvProduktSpeicher {
    public void speichereProdukte(ArrayList<Produkt> produkte, String dateipfad, boolean mitKopfzeile) {
        ArrayList<String> zeilen = new ArrayList<>();

        if (mitKopfzeile) {
            zeilen.add("name;preis");
        }

        for (int i = 0; i < produkte.size(); i++) {
            Produkt produkt = produkte.get(i);
            zeilen.add(produktAlsCsvZeile(produkt));
        }

        try {
            Files.write(Path.of(dateipfad), zeilen);
        } catch (IOException e) {
            System.out.println("Datei konnte nicht gespeichert werden: " + dateipfad);
        }
    }

    public void speichereMitBackup(ArrayList<Produkt> produkte, String dateipfad, String backupPfad) {
        try {
            if (Files.exists(Path.of(dateipfad))) {
                Files.copy(Path.of(dateipfad), Path.of(backupPfad), StandardCopyOption.REPLACE_EXISTING);
            }
        } catch (IOException e) {
            System.out.println("Backup konnte nicht erstellt werden: " + backupPfad);
        }

        speichereProdukte(produkte, dateipfad, true);
    }

    public void exportiereProdukte(ArrayList<Produkt> produkte, String exportPfad) {
        speichereProdukte(produkte, exportPfad, true);
    }

    private String produktAlsCsvZeile(Produkt produkt) {
        return produkt.getName() + ";" + produkt.getPreis();
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
        ArrayList<Produkt> geladeneProdukte = leser.ladeProdukte("data/produkte.csv");

        ProduktVerwaltung verwaltung = new ProduktVerwaltung(geladeneProdukte);

        int anzahlGeladen = verwaltung.zaehleProdukte();
        int fehlerhafteZeilen = leser.getFehlerhafteZeilen();
        double gesamtwertVorher = verwaltung.berechneGesamtwert();

        verwaltung.fuegeProduktHinzu(new Produkt("Webcam", 89.90));

        int geaenderteProdukte = 0;
        if (verwaltung.aenderePreis("Maus", 34.90)) {
            geaenderteProdukte++;
        }

        if (!verwaltung.aenderePreis("Drucker", 199.00)) {
            System.out.println("Produkt nicht gefunden: Drucker");
        }

        CsvProduktSpeicher speicher = new CsvProduktSpeicher();
        speicher.speichereMitBackup(
                verwaltung.getProdukte(),
                "data/produkte.csv",
                "data/produkte-backup.csv"
        );
        speicher.exportiereProdukte(verwaltung.getProdukte(), "data/produkte-export.csv");

        ArrayList<Produkt> erneutGeladen = leser.ladeProdukte("data/produkte.csv");
        ProduktVerwaltung pruefung = new ProduktVerwaltung(erneutGeladen);

        Produkt webcam = pruefung.findeProdukt("Webcam");
        Produkt maus = pruefung.findeProdukt("Maus");

        double gesamtwertNachher = pruefung.berechneGesamtwert();

        System.out.println("Geladene Produkte vor Änderung: " + anzahlGeladen);
        System.out.println("Erneut geladene Produkte: " + pruefung.zaehleProdukte());
        System.out.println("Webcam vorhanden: " + (webcam != null));
        System.out.println("Neuer Mauspreis: " + maus.getPreis());
        System.out.println("Gesamtwert vorher: " + runde(gesamtwertVorher));
        System.out.println("Gesamtwert nachher: " + runde(gesamtwertNachher));
        System.out.println("Veränderung: " + runde(gesamtwertNachher - gesamtwertVorher));
        System.out.println("Geladene Produkte: " + anzahlGeladen);
        System.out.println("Geänderte Produkte: " + geaenderteProdukte);
        System.out.println("Gespeicherte Produkte: " + pruefung.zaehleProdukte());
        System.out.println("Fehlerhafte CSV-Zeilen: " + fehlerhafteZeilen);
    }

    private static double runde(double wert) {
        return Math.round(wert * 10.0) / 10.0;
    }
}
```

---

## Aufgabe 9 – Gesamtwert vergleichen

Mit dieser Startdatei:

```text
name;preis
Tastatur;79.90
Monitor;249.00
Maus;39.50
```

ist der Gesamtwert vorher:

```text
79.90 + 249.00 + 39.50 = 368.4
```

Nach `Webcam;89.90` und `Maus;34.90`:

```text
79.90 + 249.00 + 34.90 + 89.90 = 453.7
```

Die Veränderung ist:

```text
453.7 - 368.4 = 85.3
```

---

## Aufgabe 10 – Ungültige CSV-Zeilen zählen

Beispieldatei:

```text
name;preis
Tastatur;79.90
Kabel
Monitor;abc
Maus;39.50
```

`Kabel` hat zu wenige Spalten. `Monitor;abc` hat keinen gültigen Preis.

Erwartung:

```text
Fehlerhafte CSV-Zeilen: 2
```

Die gültigen Produkte werden trotzdem geladen.

---

## Aufgabe 11 – Leere Produktliste behandeln

```java
ArrayList<Produkt> leereListe = new ArrayList<>();

CsvProduktSpeicher speicher = new CsvProduktSpeicher();
speicher.speichereProdukte(leereListe, "data/leere-produkte.csv", true);

CsvProduktLeser leser = new CsvProduktLeser();
ArrayList<Produkt> erneutGeladen = leser.ladeProdukte("data/leere-produkte.csv");

System.out.println("Leere Produktliste geladen: " + erneutGeladen.size() + " Produkte");
```

Erwartung:

```text
Leere Produktliste geladen: 0 Produkte
```

Eine leere Liste ist kein Fehler. Mit Kopfzeile enthält die Datei nur:

```text
name;preis
```

---

## Aufgabe 12 – Nicht vorhandenes Produkt

```java
if (!verwaltung.aenderePreis("Drucker", 199.00)) {
    System.out.println("Produkt nicht gefunden: Drucker");
}
```

Erwartung:

```text
Produkt nicht gefunden: Drucker
```

Die Methode verändert in diesem Fall kein Produkt.

---

## Aufgabe 13 – Speicher- und Ladeformat

Der Speicher schreibt:

```text
name;preis
Tastatur;79.9
```

Der Leser erwartet:

- optional die Kopfzeile `name;preis`
- danach genau zwei Spalten
- Trennzeichen `;`
- Preis als Text, der mit `Double.parseDouble(...)` lesbar ist

Damit passen Lade- und Speicherformat zusammen.

---

## Aufgabe 14 – Verantwortung prüfen

| Klasse | Verantwortung |
|---|---|
| `CsvProduktLeser` | CSV-Datei lesen, Kopfzeile überspringen, fehlerhafte Zeilen zählen |
| `CsvProduktSpeicher` | Produkte als CSV speichern, Backup und Export schreiben |
| `ProduktVerwaltung` | Produkte verwalten, Preis ändern, suchen, Gesamtwert berechnen |
| `Main` | Ablauf starten und Resultate ausgeben |

`Main` darf den Ablauf zeigen. Die Schleifen für Lesen, Speichern, Suchen und Berechnen sollen aber in den passenden Klassen liegen.

---

## Transfer – Backup, Export und Statistik

### Backup

```java
speicher.speichereMitBackup(
        verwaltung.getProdukte(),
        "data/produkte.csv",
        "data/produkte-backup.csv"
);
```

Die Backup-Datei enthält den alten Zustand. Danach wird `data/produkte.csv` mit dem neuen Zustand überschrieben.

### Export

```java
speicher.exportiereProdukte(verwaltung.getProdukte(), "data/produkte-export.csv");
```

Die Exportdatei ist eine zusätzliche Datei. Sie muss die Hauptdatei nicht ersetzen.

### Änderungsstatistik

```java
System.out.println("Geladene Produkte: " + anzahlGeladen);
System.out.println("Geänderte Produkte: " + geaenderteProdukte);
System.out.println("Gespeicherte Produkte: " + pruefung.zaehleProdukte());
System.out.println("Fehlerhafte CSV-Zeilen: " + fehlerhafteZeilen);
```

Beispiel:

```text
Geladene Produkte: 3
Geänderte Produkte: 1
Gespeicherte Produkte: 4
Fehlerhafte CSV-Zeilen: 2
```

---

## Reflexion – mögliche Antworten

1. Laden alleine reicht nicht, weil Änderungen danach nur im Arbeitsspeicher passieren.
2. Änderungen müssen bewusst gespeichert werden, damit sie nach Programmende noch vorhanden sind.
3. Ein Backup ist sinnvoll, weil `Files.write(...)` die bestehende Datei überschreibt.
4. Datei- und Fachlogik sollten getrennt bleiben, damit Lesen, Speichern und Berechnen nicht vermischt werden.
5. Zustand bedeutet: die aktuellen Daten der Anwendung, zum Beispiel Produkte, Preise und Änderungen.

---

## Typische Fehlerhinweise

- Wenn nach dem Bearbeiten nicht gespeichert wird, bleibt die Datei unverändert.
- Wenn nach dem Speichern nicht erneut geladen wird, wird das Dateiformat nicht wirklich geprüft.
- Wenn die Kopfzeile nicht übersprungen wird, entsteht ein falsches Produkt `name`.
- Wenn der Preis als `String` bleibt, kann kein Gesamtwert berechnet werden.
- Wenn die falsche Liste gespeichert wird, fehlen Änderungen in der Datei.
- Wenn fehlerhafte Zeilen nicht gezählt werden, bleibt die Datenqualität unsichtbar.
- Wenn `data` fehlt, kann die Datei nicht geschrieben werden.

---

## Verifikation

Die Java-Beispiele wurden als kleines Maven-Projekt unter `/tmp/persistenzablauf-validierung` geprüft.

Ausgeführter Befehl:

```bash
mvn package
```

Ergebnis:

```text
BUILD SUCCESS
```

Zusätzlich wurde die kompilierte `Main`-Klasse ausgeführt:

```bash
java -cp target/classes ch.allianz.youngoitv.produktverwaltung.Main
```

Die Ausgabe zeigte:

- drei gültig geladene Produkte aus der Startdatei
- zwei fehlerhafte CSV-Zeilen
- ein neu hinzugefügtes Produkt `Webcam`
- den geänderten Preis von `Maus`
- vier erneut geladene Produkte
- eine erzeugte Backup-Datei
- eine erzeugte Exportdatei
