# Lösungen – Interfaces für austauschbare Services

Diese Musterlösung zeigt eine kleine Standardlösung. Es wird bewusst nur ein Interface eingeführt.

Nicht verwendet werden:

- Spring
- Dependency Injection
- abstrakte Klassen
- komplexe Polymorphie
- mehrere Interfaces
- Datenbanken
- formales Repository-Pattern

---

## Aufgabe 1 – Bestehende Speichermethode finden

Eine passende Speichermethode ist:

```text
Methode: speichern
Parameter: ArrayList<Produkt> produkte, String dateipfad
Rückgabetyp: void
```

Wenn die bestehende Klasse bereits `speichereProdukte(...)` verwendet, kann dieser Name beibehalten werden. Entscheidend ist, dass Interface und Implementierung exakt zusammenpassen.

Die Umsetzung bleibt in `CsvProduktSpeicher`:

```text
CSV-Zeilen erzeugen
Kopfzeile ergänzen
Produktdaten als Text schreiben
Datei speichern
```

---

## Aufgabe 2 – Interface ProduktSpeicher

```java
package ch.allianz.youngoitv.produktverwaltung;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;
import java.util.ArrayList;

public interface ProduktSpeicher {
    void speichern(ArrayList<Produkt> produkte, String dateipfad);
}
```

`ProduktSpeicher` ist der Vertrag. Das Interface sagt nur, welche Methode vorhanden sein muss.

---

## Aufgabe 3 – CsvProduktSpeicher anpassen

```java
package ch.allianz.youngoitv.produktverwaltung;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.ArrayList;

public class CsvProduktSpeicher implements ProduktSpeicher {
    public void speichern(ArrayList<Produkt> produkte, String dateipfad) {
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

`CsvProduktSpeicher` ist die konkrete Umsetzung. Die CSV-Logik bleibt dort.

---

## Aufgabe 4 – Main gegen das Interface schreiben

```java
package ch.allianz.youngoitv.produktverwaltung;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        ArrayList<Produkt> produkte = new ArrayList<>();
        produkte.add(new Produkt("Maus", 34.90));
        produkte.add(new Produkt("Tastatur", 79.90));

        ProduktSpeicher speicher = new CsvProduktSpeicher();
        speicher.speichern(produkte, "data/produkte.csv");

        System.out.println("Produkte gespeichert: " + produkte.size());
    }
}
```

Links steht der Vertrag:

```text
ProduktSpeicher speicher
```

Rechts steht die konkrete Klasse:

```text
new CsvProduktSpeicher()
```

---

## Aufgabe 5 – Verhalten prüfen

Erwartete Beobachtung:

```text
Geändert: Main verwendet ProduktSpeicher als Typ.
Gleich: Produkte werden weiterhin als CSV-Datei gespeichert.
```

Das Refactoring soll zuerst das Verhalten behalten. Die Struktur wird verbessert, nicht die Fachfunktion verändert.

---

## Aufgabe 6 – Vertrag und Umsetzung unterscheiden

| Aussage | Vertrag oder Umsetzung? |
|---|---|
| Methode `speichern(...)` muss vorhanden sein | Vertrag |
| CSV-Zeile mit Semikolon erzeugen | Umsetzung |
| Datei mit `Files.write(...)` schreiben | Umsetzung |
| Rückgabetyp ist `void` | Vertrag |
| Preis aus `Produkt` lesen | Umsetzung |

---

## Aufgabe 7 – Codeabschnitte zuordnen

| Codeabschnitt | Einordnung |
|---|---|
| `public interface ProduktSpeicher` | Interface |
| `void speichern(ArrayList<Produkt> produkte, String dateipfad);` | Vertrag |
| `public class CsvProduktSpeicher implements ProduktSpeicher` | Verbindung von Umsetzung und Vertrag |
| `zeilen.add(produkt.getName() + ";" + produkt.getPreis());` | konkrete CSV-Umsetzung |
| `Files.write(Path.of(dateipfad), zeilen);` | konkrete Datei-Umsetzung |

Begründung: Das Interface kennt keine CSV-Zeilen und keine Dateioperationen. Diese Details gehören in `CsvProduktSpeicher`.

---

## Aufgabe 8 – Methodennamen und Parameter prüfen

Interface und Implementierung müssen zusammenpassen:

```text
gleicher Methodenname
gleiche Parameter
gleiche Reihenfolge
gleicher Rückgabetyp
```

Typischer Fehler:

```java
public void speichere(ArrayList<Produkt> produkte, String dateipfad) {
    // ...
}
```

Diese Methode heisst anders als `speichern(...)`. Dann erfüllt `CsvProduktSpeicher` den Vertrag nicht korrekt.

---

## Aufgabe 9 – Main bewusst lesen

Mögliche Erklärung:

```text
Main verwendet links den Typ ProduktSpeicher, weil es nur den Vertrag kennen muss.
Rechts wird CsvProduktSpeicher erzeugt, weil aktuell weiterhin als CSV-Datei gespeichert wird.
```

`Main` soll keine CSV-Zeilen erzeugen und keine Datei direkt mit `Files.write(...)` schreiben.

---

## Transfer 1 – Zweite Implementierung überlegen

Mögliche Idee:

```text
KonsolenProduktSpeicher
```

Diese Klasse könnte Produkte auf der Konsole ausgeben. Sie könnte denselben Vertrag `ProduktSpeicher` erfüllen, weil sie ebenfalls eine Methode `speichern(...)` anbietet. Sie wäre aber keine dauerhafte Speicherung.

---

## Transfer 2 – KonsolenProduktSpeicher als Idee

`speichern(...)` würde über die Produkte laufen und Name sowie Preis ausgeben.

Vorteil:

```text
einfach zum Demonstrieren oder manuellen Prüfen
```

Nachteil:

```text
Die Daten werden nicht dauerhaft gespeichert.
```

Die Klasse muss in dieser Einheit nicht ausprogrammiert werden.

---

## Transfer 3 – BackupProduktSpeicher als Idee

Ein `BackupProduktSpeicher` könnte vor dem Überschreiben eine Kopie der alten Datei erstellen.

Diese Klasse hätte Datei-Logik, weil Backup direkt mit Dateien zusammenhängt. Sie ist anspruchsvoller als `CsvProduktSpeicher`, weil sie zwei Dinge koordinieren muss:

```text
Backup erzeugen
neue Datei speichern
```

Darum reicht es hier, die Idee zu beschreiben.

---

## Transfer 4 – Nutzen für spätere Themen

Interfaces helfen später, weil Code gegen einen Vertrag arbeiten kann.

Beispiele:

- Tests können später mit einer einfachen Ersatzimplementierung arbeiten.
- Services können über klare Methodenverträge genutzt werden.
- Bei REST kann eine Schicht später anders angebunden werden.
- Eine Implementierung kann ausgetauscht werden, ohne überall den Ablauf umzubauen.

Noch wird keine REST-Anwendung gebaut.

---

## Typische Fehlerhinweise

| Fehler | Korrektur |
|---|---|
| Interface enthält `Files.write(...)` | Datei-Code zurück in `CsvProduktSpeicher` |
| Methode heisst im Interface anders als in der Klasse | Signatur angleichen |
| `implements ProduktSpeicher` fehlt | in `CsvProduktSpeicher` ergänzen |
| `Main` nutzt weiterhin überall `CsvProduktSpeicher` als Typ | Variable auf `ProduktSpeicher` ändern |
| zweite Implementierung wird zu früh gebaut | zuerst das eine Interface verstehen |
| Verhalten ändert sich beim Refactoring | speichern erneut ausführen und Datei prüfen |

---

## Reflexion – mögliche Antworten

1. Ein Interface ist ein Vertrag, weil es festlegt, welche Methode eine Klasse anbieten muss.
2. Austauschbar bedeutet hier: Eine andere Klasse könnte später denselben Vertrag erfüllen.
3. `Main` wird weniger stark an eine konkrete Speicherklasse gebunden.
4. Wir führen nur ein Interface ein, damit das neue Konzept überschaubar bleibt.
5. Später könnten auch Leser, Exporte, Backups oder externe Services austauschbar werden.

---

## Verifikation

Die Java-Beispiele wurden als temporäres Maven-Projekt unter `/tmp/interfaces-services-validierung` geprüft.

Ausgeführter Befehl:

```bash
mvn package
```

Ergebnis:

```text
BUILD SUCCESS
```

Hinweis: Im temporären Projekt wurden die Produktionsklassen kompiliert. Es waren keine Testklassen hinterlegt, deshalb wurden dort keine Tests ausgeführt.

Zusätzlich wurde die kompilierte `Main`-Klasse ausgeführt:

```bash
java -cp target/classes ch.allianz.youngoitv.produktverwaltung.Main
```

Die Ausgabe zeigte:

```text
Produkte gespeichert: 2
```

Die erzeugte CSV-Datei enthielt:

```text
name;preis
Maus;34.9
Tastatur;79.9
```
