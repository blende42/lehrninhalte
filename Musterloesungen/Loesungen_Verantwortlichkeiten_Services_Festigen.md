# Lösungen – Verantwortlichkeiten und Services festigen

Diese Musterlösung zeigt eine einfache Standardlösung. Ziel ist nicht eine neue Architektur, sondern eine klare Begründung der bekannten Struktur:

```text
Main steuert den Ablauf.
LagerService enthält Fachlogik.
ProduktSpeicher beschreibt den Persistenzvertrag.
CsvProduktSpeicher lädt und speichert CSV-Daten.
Produkt hält Daten.
```

---

## Basis

### Aufgabe 1 – Verantwortlichkeiten zuordnen

| Methode oder Handlung | Passende Klasse | Begründung |
|---|---|---|
| Produktname speichern | `Produkt` | gehört zu den Produktdaten |
| Produktpreis speichern | `Produkt` | gehört zu den Produktdaten |
| Bestand nach Verkauf reduzieren | `LagerService` | fachliche Regel |
| prüfen, ob eine Verkaufsmenge gültig ist | `LagerService` | fachliche Prüfung |
| Laden und Speichern als Vertrag beschreiben | `ProduktSpeicher` | gemeinsamer Persistenzvertrag |
| Produkte aus CSV-Datei konkret laden | `CsvProduktSpeicher` | konkrete CSV-Umsetzung |
| Produkte in CSV-Datei konkret speichern | `CsvProduktSpeicher` | konkrete CSV-Umsetzung |
| Programmablauf starten | `Main` | Startpunkt des Programms |
| `LagerService` und `ProduktSpeicher` verwenden | `Main` | Ablauf zusammensetzen |
| CSV-Zeile mit `split(";")` zerlegen | `CsvProduktSpeicher` | CSV-Format verarbeiten |
| Warnung bei tiefem Bestand prüfen | `LagerService` | fachliche Regel |

Kurzbegründung:

```text
Main soll lesbar zeigen, was passiert.
Der Service entscheidet fachlich.
Die Speicherklasse kennt das CSV-Format.
```

---

### Aufgaben 2 und 3 – Logik in Main erkennen

Mögliche Markierung:

| Codeausschnitt | Kategorie | Soll bleiben? | Falls nein: Wohin? |
|---|---|---|---|
| `new CsvProduktSpeicher()` | Ablaufsteuerung | ja | bleibt in `Main` |
| `speicher.ladeProdukte(...)` | Persistenzaufruf | ja | Aufruf bleibt, Details liegen in `CsvProduktSpeicher` |
| `Produkt produkt = produkte.get(0)` | Ablaufsteuerung | ja | bleibt als Beispielablauf |
| `menge > 0` | Fachlogik | nein | `LagerService` |
| `produkt.getBestand() >= menge` | Fachlogik | nein | `LagerService` |
| `produkt.setBestand(...)` | Fachlogik | nein | `LagerService` |
| `speicher.speichereProdukte(...)` | Persistenzaufruf | ja | Aufruf bleibt, Details liegen in `CsvProduktSpeicher` |

Die direkte Verkaufsprüfung und Bestandsänderung sind in `Main` problematisch, weil sie schwerer testbar sind und den Ablauf mit fachlichen Details vermischen.

---

## Kompakte Standardlösung

### `Produkt.java`

```java
package ch.allianz.youngoitv.lager.model;

public class Produkt {
    private String name;
    private double preis;
    private int bestand;

    public Produkt(String name, double preis, int bestand) {
        this.name = name;
        this.preis = preis;
        this.bestand = bestand;
    }

    public String getName() {
        return name;
    }

    public double getPreis() {
        return preis;
    }

    public int getBestand() {
        return bestand;
    }

    public void setBestand(int bestand) {
        this.bestand = bestand;
    }
}
```

`Produkt` speichert Daten. Es entscheidet nicht, ob ein Verkauf erlaubt ist, und kennt keine CSV-Datei.

### `LagerService.java`

```java
package ch.allianz.youngoitv.lager;

import ch.allianz.youngoitv.lager.model.Produkt;
import java.util.ArrayList;

public class LagerService {
    public boolean bestandReicht(Produkt produkt, int menge) {
        return menge > 0 && produkt.getBestand() >= menge;
    }

    public boolean verkaufen(Produkt produkt, int menge) {
        if (!bestandReicht(produkt, menge)) {
            return false;
        }

        produkt.setBestand(produkt.getBestand() - menge);
        return true;
    }

    public void bestandErhoehen(Produkt produkt, int menge) {
        if (menge <= 0) {
            return;
        }

        produkt.setBestand(produkt.getBestand() + menge);
    }

    public boolean warnungPruefen(Produkt produkt, int grenze) {
        return produkt.getBestand() < grenze;
    }

    public double berechneLagerwert(ArrayList<Produkt> produkte) {
        double summe = 0.0;

        for (Produkt produkt : produkte) {
            summe = summe + produkt.getPreis() * produkt.getBestand();
        }

        return summe;
    }
}
```

`LagerService` enthält fachliche Regeln. Er liest und schreibt keine Dateien.

### `ProduktSpeicher.java`

```java
package ch.allianz.youngoitv.lager;

import ch.allianz.youngoitv.lager.model.Produkt;
import java.util.ArrayList;

public interface ProduktSpeicher {
    ArrayList<Produkt> ladeProdukte(String dateipfad);

    void speichereProdukte(ArrayList<Produkt> produkte, String dateipfad);
}
```

`ProduktSpeicher` beschreibt, was ein Speicher können muss. Das Interface enthält keine Verkaufsregel.

### `CsvProduktSpeicher.java`

```java
package ch.allianz.youngoitv.lager;

import ch.allianz.youngoitv.lager.model.Produkt;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.ArrayList;

public class CsvProduktSpeicher implements ProduktSpeicher {
    @Override
    public ArrayList<Produkt> ladeProdukte(String dateipfad) {
        ArrayList<Produkt> produkte = new ArrayList<>();

        try {
            for (String zeile : Files.readAllLines(Path.of(dateipfad))) {
                if (zeile.equalsIgnoreCase("name;preis;bestand")) {
                    continue;
                }

                String[] teile = zeile.split(";");

                if (teile.length == 3) {
                    String name = teile[0].trim();
                    double preis = Double.parseDouble(teile[1].trim());
                    int bestand = Integer.parseInt(teile[2].trim());
                    produkte.add(new Produkt(name, preis, bestand));
                }
            }
        } catch (IOException | NumberFormatException e) {
            System.out.println("Produkte konnten nicht geladen werden: " + dateipfad);
        }

        return produkte;
    }

    @Override
    public void speichereProdukte(ArrayList<Produkt> produkte, String dateipfad) {
        ArrayList<String> zeilen = new ArrayList<>();
        zeilen.add("name;preis;bestand");

        for (Produkt produkt : produkte) {
            zeilen.add(produkt.getName() + ";" + produkt.getPreis() + ";" + produkt.getBestand());
        }

        try {
            Files.write(Path.of(dateipfad), zeilen);
        } catch (IOException e) {
            System.out.println("Produkte konnten nicht gespeichert werden: " + dateipfad);
        }
    }
}
```

`CsvProduktSpeicher` kennt CSV-Details. Er entscheidet nicht, ob ein Verkauf gültig ist.

### `Main.java`

```java
package ch.allianz.youngoitv.lager;

import ch.allianz.youngoitv.lager.model.Produkt;
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        ProduktSpeicher speicher = new CsvProduktSpeicher();
        ArrayList<Produkt> produkte = speicher.ladeProdukte("data/produkte.csv");

        LagerService lagerService = new LagerService();

        if (produkte.isEmpty()) {
            System.out.println("Keine Produkte vorhanden");
            return;
        }

        Produkt produkt = produkte.get(0);

        boolean verkauft = lagerService.verkaufen(produkt, 3);

        if (verkauft) {
            System.out.println("Verkauf erfolgreich");
        } else {
            System.out.println("Verkauf nicht möglich");
        }

        if (lagerService.warnungPruefen(produkt, 5)) {
            System.out.println("Warnung: tiefer Bestand");
        }

        speicher.speichereProdukte(produkte, "target/produkte.csv");
    }
}
```

`Main` zeigt den Ablauf. Verkaufsdetails und CSV-Details sind ausgelagert.

---

## Vertiefung

### Aufgabe 7 – Schlechte Struktur analysieren

Problematische Methode:

```java
public boolean verkaufenUndSpeichern(Produkt produkt, int menge, String pfad)
```

Markierung:

| Codeanteil | Kategorie |
|---|---|
| `menge <= 0` prüfen | Fachlogik |
| Bestand prüfen | Fachlogik |
| Bestand reduzieren | Fachlogik |
| Produkte als CSV speichern | Persistenz |

Problem:

```text
Eine Speicherklasse entscheidet über Verkaufsregeln.
```

Bessere Aufteilung:

- `LagerService.verkaufen(produkt, menge)` entscheidet und ändert den Bestand.
- `CsvProduktSpeicher.speichereProdukte(produkte, pfad)` speichert den aktuellen Zustand.
- `Main` ruft beide Schritte in der passenden Reihenfolge auf.

---

### Aufgabe 8 – Doppelte Logik zusammenführen

Doppelte Prüfungen wie diese sollten nicht mehrfach verteilt bleiben:

```java
menge > 0
produkt.getBestand() >= menge
```

Passende Zusammenführung:

```java
public boolean bestandReicht(Produkt produkt, int menge) {
    return menge > 0 && produkt.getBestand() >= menge;
}
```

Danach verwenden andere Methoden dieselbe Prüfung:

```java
public boolean verkaufen(Produkt produkt, int menge) {
    if (!bestandReicht(produkt, menge)) {
        return false;
    }

    produkt.setBestand(produkt.getBestand() - menge);
    return true;
}
```

Vorteil: Wenn sich die Regel ändert, muss sie nur an einer Stelle angepasst werden.

---

### Aufgabe 9 – Geeignete Service-Methoden

| Methode | Geeignet für `LagerService`? | Begründung |
|---|---|---|
| `verkaufen(Produkt produkt, int menge)` | ja | fachliche Handlung |
| `bestandErhoehen(Produkt produkt, int menge)` | ja | fachliche Bestandsänderung |
| `warnungPruefen(Produkt produkt, int grenze)` | ja | fachliche Prüfung |
| `speichereCsvDatei(ArrayList<Produkt> produkte)` | nein | Persistenz |
| `zeigeMenue()` | nein | Ausgabe und Bedienung |
| `berechneLagerwert(ArrayList<Produkt> produkte)` | ja | fachliche Auswertung |
| `parseCsvZeile(String zeile)` | nein | CSV-Verarbeitung |

---

### Aufgaben 10 und 11 – Namen verbessern und CSV entfernen

Mögliche Umbenennungen:

| Ungünstig | Besser |
|---|---|
| `mache(...)` | `verkaufen(...)` |
| `check(...)` | `bestandReicht(...)` |
| `update(...)` | `bestandErhoehen(...)` |
| `save(...)` | `speichereProdukte(...)` |
| `run()` | `starteAblauf()` oder direkt `main(...)` |

CSV-Schreiben gehört nicht in `LagerService` oder `Produkt`.

Falsch platziert:

```java
public class LagerService {
    public void speichereNachVerkauf(Produkt produkt, String dateipfad) {
        // CSV schreiben
    }
}
```

Besser:

```java
lagerService.verkaufen(produkt, 3);
speicher.speichereProdukte(produkte, "target/produkte.csv");
```

---

## Testaufgaben

### `LagerServiceTest.java`

```java
package ch.allianz.youngoitv.lager;

import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.junit.jupiter.api.Assertions.assertFalse;
import static org.junit.jupiter.api.Assertions.assertTrue;

import ch.allianz.youngoitv.lager.model.Produkt;
import org.junit.jupiter.api.Test;

class LagerServiceTest {
    @Test
    void verkaufen_mitGenugBestand_reduziertBestand() {
        Produkt produkt = new Produkt("Maus", 24.90, 10);
        LagerService service = new LagerService();

        boolean verkauft = service.verkaufen(produkt, 3);

        assertTrue(verkauft);
        assertEquals(7, produkt.getBestand());
    }

    @Test
    void verkaufen_mitZuHoherMenge_veraendertBestandNicht() {
        Produkt produkt = new Produkt("Maus", 24.90, 10);
        LagerService service = new LagerService();

        boolean verkauft = service.verkaufen(produkt, 11);

        assertFalse(verkauft);
        assertEquals(10, produkt.getBestand());
    }

    @Test
    void verkaufen_mitNull_veraendertBestandNicht() {
        Produkt produkt = new Produkt("Maus", 24.90, 10);
        LagerService service = new LagerService();

        boolean verkauft = service.verkaufen(produkt, 0);

        assertFalse(verkauft);
        assertEquals(10, produkt.getBestand());
    }

    @Test
    void verkaufen_mitNegativerMenge_veraendertBestandNicht() {
        Produkt produkt = new Produkt("Maus", 24.90, 10);
        LagerService service = new LagerService();

        boolean verkauft = service.verkaufen(produkt, -2);

        assertFalse(verkauft);
        assertEquals(10, produkt.getBestand());
    }

    @Test
    void bestandErhoehen_mitGueltigerMenge_erhoehtBestand() {
        Produkt produkt = new Produkt("Maus", 24.90, 10);
        LagerService service = new LagerService();

        service.bestandErhoehen(produkt, 5);

        assertEquals(15, produkt.getBestand());
    }

    @Test
    void bestandErhoehen_mitUngueltigerMenge_veraendertBestandNicht() {
        Produkt produkt = new Produkt("Maus", 24.90, 10);
        LagerService service = new LagerService();

        service.bestandErhoehen(produkt, -5);

        assertEquals(10, produkt.getBestand());
    }

    @Test
    void warnungPruefen_unterGrenze_liefertTrue() {
        Produkt produkt = new Produkt("Maus", 24.90, 4);
        LagerService service = new LagerService();

        assertTrue(service.warnungPruefen(produkt, 5));
    }

    @Test
    void warnungPruefen_genauBeiGrenze_liefertFalse() {
        Produkt produkt = new Produkt("Maus", 24.90, 5);
        LagerService service = new LagerService();

        assertFalse(service.warnungPruefen(produkt, 5));
    }
}
```

Service-Tests verwenden keine echte CSV-Datei. Dadurch bleibt klar: Sie prüfen Fachlogik, nicht Persistenz.

---

## Transfer

### Weitere mögliche Services

Ein weiterer Service ist sinnvoll, wenn eine neue Gruppe fachlicher Regeln entsteht.

| Idee | Einschätzung |
|---|---|
| `BestellService` | sinnvoll, wenn Bestellungen eigene Regeln haben |
| `InventurService` | sinnvoll, wenn Inventur mehr als eine einfache Liste ist |
| `PreisService` | sinnvoll, wenn Rabatte und Preisregeln zunehmen |
| `WarnService` | eher unnötig, solange nur eine einfache Warnregel besteht |

Für die aktuelle kleine Lagerverwaltung reicht meistens ein `LagerService`.

### Grenzen kleiner Strukturen

Ein `LagerService` hilft, wenn mehrere fachliche Regeln zusammengehören. Er wird zu gross, wenn er plötzlich CSV-Dateien schreibt, Menüs anzeigt, Bestellungen verarbeitet, Preise berechnet und Inventurberichte erstellt.

Mehrere Services sind erst sinnvoll, wenn die fachlichen Aufgaben klar getrennt sind. Zu viele Services sind problematisch, wenn eine einfache Änderung über viele kleine Klassen verteilt wird.

### Erweiterungen einordnen

| Erweiterung | Betroffene Klasse | Nicht betroffen | Sinnvolle Tests |
|---|---|---|---|
| Mindestbestand pro Produkt | `Produkt`, `LagerService` | `CsvProduktSpeicher`, ausser das CSV-Format wird erweitert | Warnung unter, genau bei und über Grenze |
| Rabatte bei grosser Verkaufsmenge | `LagerService` | `CsvProduktSpeicher` | Preis- oder Rabattregel mit Grenzfällen |
| Export als andere Datei | `CsvProduktSpeicher` oder neue Speicherklasse | `LagerService` | Datei wird mit erwarteten Zeilen geschrieben |
| zweite Speicherart | neue Klasse mit `ProduktSpeicher` | `LagerService` | gleiche Produkte werden anders gespeichert |

---

## Typische Fehlerhinweise

| Fehler | Hinweis |
|---|---|
| alles bleibt in `Main` | `Main` wird schwer lesbar und schlecht testbar |
| `LagerService` schreibt CSV-Dateien | Fachlogik und Persistenz werden vermischt |
| `Produkt` verkauft sich selbst | Datenklasse übernimmt zu viel |
| gleiche Prüfung steht mehrfach im Code | Regeln können auseinanderlaufen |
| Vererbung wird ohne Wiederverwendungsproblem eingesetzt | Struktur wird unnötig schwer |
| `LagerService` enthält Menüs, CSV und Fachregeln | Service wird zu gross |
| `CsvProduktSpeicher` prüft Verkaufsregeln | Speicherklasse enthält Fachlogik |

---

## Kurze Strukturbegründung

Diese Aufteilung ist sinnvoll, weil jede Klasse eine klare Aufgabe hat:

- `Main` bleibt kurz und zeigt den Ablauf.
- `LagerService` ist gut testbar, weil er keine Datei braucht.
- `ProduktSpeicher` macht sichtbar, dass Persistenz eine eigene Verantwortung ist.
- `CsvProduktSpeicher` kapselt CSV-Details.
- `Produkt` bleibt einfach und verständlich.

Die Struktur ist bewusst klein. Sie soll Lernenden helfen, Verantwortlichkeiten zu erklären, nicht möglichst viele Klassen erzeugen.

---

## Verifikation

Die Java-Beispiele wurden als temporäres Maven-Projekt unter `/tmp/verantwortlichkeiten-services-festigen-validierung` geprüft.

Ausgeführt:

```bash
mvn test
```

Ergebnis:

```text
Tests run: 8, Failures: 0, Errors: 0, Skipped: 0
BUILD SUCCESS
```

Zusätzlich wurde `Main` mit folgendem Befehl ausgeführt:

```bash
java -cp target/classes ch.allianz.youngoitv.lager.Main
```

Erwartete Ausgabe:

```text
Verkauf erfolgreich
```

Die erzeugte Datei `target/produkte.csv` enthält danach den reduzierten Bestand.
