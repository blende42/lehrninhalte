# Lösungen – Fachlogik in Services bündeln

Diese Musterlösung zeigt eine einfache Standardlösung. Ziel ist nicht eine grosse Architektur, sondern eine klare Trennung:

```text
Main steuert den Ablauf.
LagerService bündelt Fachlogik.
ProduktSpeicher beschreibt den Speichervertrag.
CsvProduktSpeicher speichert und lädt CSV-Daten.
Produkt hält Daten.
```

Bewusst nicht verwendet werden Frameworks, Datenbanken, automatische Objekterzeugung oder komplexe Architekturmodelle.

---

## Basis

### Aufgaben 1 und 2 – Verantwortlichkeiten erkennen

| Handlung | Passende Verantwortung |
|---|---|
| Produktliste laden | Persistenz |
| Verkauf prüfen | Fachlogik |
| Bestand reduzieren | Fachlogik |
| Produkte speichern | Persistenz |
| Erfolgsmeldung ausgeben | Ablauf / Ausgabe |
| Warnung bei tiefem Bestand prüfen | Fachlogik |

`Main` soll den Ablauf sichtbar machen. Verkaufsregeln und Bestandsänderungen gehören in den `LagerService`. Speichern und Laden bleiben bei `ProduktSpeicher` und `CsvProduktSpeicher`.

---

## `Produkt`

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

`Produkt` hält Daten. Es steuert keinen Verkauf und speichert keine Datei.

---

## `LagerService`

```java
package ch.allianz.youngoitv.lager;

import ch.allianz.youngoitv.lager.model.Produkt;

public class LagerService {
    public boolean bestandPruefen(Produkt produkt, int menge) {
        return menge > 0 && produkt.getBestand() >= menge;
    }

    public boolean verkaufen(Produkt produkt, int menge) {
        if (!bestandPruefen(produkt, menge)) {
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
}
```

Der Service enthält fachliche Regeln. Er liest keine CSV-Datei, schreibt keine CSV-Datei und zeigt kein Menü an.

---

## `ProduktSpeicher`

```java
package ch.allianz.youngoitv.lager;

import ch.allianz.youngoitv.lager.model.Produkt;
import java.util.ArrayList;

public interface ProduktSpeicher {
    void speichern(ArrayList<Produkt> produkte, String dateipfad);
}
```

`ProduktSpeicher` beschreibt den Vertrag für Persistenz. Die Fachlogik bleibt im `LagerService`.

---

## `CsvProduktSpeicher`

```java
package ch.allianz.youngoitv.lager;

import ch.allianz.youngoitv.lager.model.Produkt;
import java.util.ArrayList;

public class CsvProduktSpeicher implements ProduktSpeicher {
    @Override
    public void speichern(ArrayList<Produkt> produkte, String dateipfad) {
        for (Produkt produkt : produkte) {
            String zeile = produkt.getName() + ";" + produkt.getPreis() + ";" + produkt.getBestand();
            System.out.println(zeile);
        }
    }
}
```

In einer vollständigen Lösung würde diese Klasse die CSV-Datei schreiben oder lesen. Sie entscheidet aber nicht, ob ein Verkauf erlaubt ist.

---

## `Main`

```java
package ch.allianz.youngoitv.lager;

import ch.allianz.youngoitv.lager.model.Produkt;
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        Produkt produkt = new Produkt("Maus", 24.90, 10);
        LagerService lagerService = new LagerService();

        boolean verkauft = lagerService.verkaufen(produkt, 3);

        if (verkauft) {
            System.out.println("Verkauf erfolgreich");
        } else {
            System.out.println("Zu wenig Bestand");
        }

        if (lagerService.warnungPruefen(produkt, 5)) {
            System.out.println("Warnung: tiefer Bestand");
        }

        ArrayList<Produkt> produkte = new ArrayList<>();
        produkte.add(produkt);

        ProduktSpeicher speicher = new CsvProduktSpeicher();
        speicher.speichern(produkte, "target/produkte.csv");
    }
}
```

`Main` zeigt den Ablauf. Die fachliche Entscheidung liegt im Service.

---

## Vertiefung

### Service und Persistenz vergleichen

| Aufgabe | Passende Stelle | Begründung |
|---|---|---|
| Verkauf prüfen | `LagerService` | fachliche Regel |
| CSV-Zeile schreiben | `CsvProduktSpeicher` | Persistenz |
| Bestand erhöhen | `LagerService` | fachliche Änderung |
| Datei speichern | `CsvProduktSpeicher` | Persistenz |
| Warnung prüfen | `LagerService` | fachliche Regel |
| Speichervertrag beschreiben | `ProduktSpeicher` | gemeinsamer Vertrag |

### Beispieltests

```java
package ch.allianz.youngoitv.lager;

import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.junit.jupiter.api.Assertions.assertFalse;
import static org.junit.jupiter.api.Assertions.assertTrue;

import ch.allianz.youngoitv.lager.model.Produkt;
import org.junit.jupiter.api.Test;

class LagerServiceTest {
    @Test
    void verkaufenReduziertBestand() {
        Produkt produkt = new Produkt("Maus", 24.90, 10);
        LagerService service = new LagerService();

        boolean verkauft = service.verkaufen(produkt, 3);

        assertTrue(verkauft);
        assertEquals(7, produkt.getBestand());
    }

    @Test
    void verkaufenMitZuHoherMengeBleibtUnveraendert() {
        Produkt produkt = new Produkt("Maus", 24.90, 10);
        LagerService service = new LagerService();

        boolean verkauft = service.verkaufen(produkt, 11);

        assertFalse(verkauft);
        assertEquals(10, produkt.getBestand());
    }
}
```

---

## Transfer

Ein weiterer Service ist nur sinnvoll, wenn er eine klare fachliche Aufgabe bündelt. Ein `BestellService` könnte später passen, wenn Bestellungen eigene Regeln haben. Ein `CsvService` wäre hier eher problematisch, weil CSV bereits Aufgabe von `CsvProduktSpeicher` ist.

Zu viele Services werden problematisch, wenn Lernende für eine einfache Regel viele kleine Dateien öffnen müssen. Eine Methode im bestehenden `LagerService` ist dann oft verständlicher.

---

## Typische Fehlerhinweise

| Fehler | Hinweis |
|---|---|
| Verkaufsregel bleibt in `Main` | Fachlogik gehört in den `LagerService` |
| `CsvProduktSpeicher` verkauft Produkte | Persistenz und Fachlogik werden vermischt |
| Service gibt direkt viele Texte aus | Service soll möglichst fachliche Werte zurückgeben |
| `Produkt` steuert die ganze Lagerverwaltung | Datenklasse wird überladen |
| nach dem Umbau keine Prüfung ausführen | Refactoring kann Verhalten unbemerkt verändern |

---

## Verifikation

Die Java-Beispiele wurden als temporäres Maven-Projekt unter `/tmp/fachlogik-services-validierung` geprüft.

Ausgeführt:

```bash
mvn test
```

Ergebnis:

```text
Tests run: 4, Failures: 0, Errors: 0, Skipped: 0
BUILD SUCCESS
```

Zusätzlich wurde `Main` mit `java -cp target/classes ch.allianz.youngoitv.lager.Main` ausgeführt. Erwartete Ausgabe:

```text
Verkauf erfolgreich
Maus;24.9;7
```
