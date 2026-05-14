# Lösungen – Mehrere Klassen mit demselben Interface

Diese Musterlösung zeigt eine kompakte Standardlösung. Es wird genau eine zweite Implementierung ergänzt: `KonsolenProduktSpeicher`.

Nicht verwendet werden:

- Spring
- Dependency Injection
- Factory
- abstrakte Klassen
- komplexe Polymorphie
- Datenbanken
- formales Repository-Pattern

---

## Aufgabe 1 – Interface erneut lesen

Eine passende Signatur ist:

```text
Methode: speichern
Parameter: ArrayList<Produkt> produkte, String dateipfad
Rückgabetyp: void
```

Der Vertrag verlangt:

```text
Jede Implementierung von ProduktSpeicher muss Produkte mit speichern(...) entgegennehmen können.
```

Das Interface legt nur den Methodenvertrag fest. Es entscheidet nicht, ob in eine Datei geschrieben oder auf der Konsole ausgegeben wird.

---

## Aufgaben 2 und 3 – KonsolenProduktSpeicher erstellen

```java
package ch.allianz.youngoitv.produktverwaltung;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;
import java.util.ArrayList;

public class KonsolenProduktSpeicher implements ProduktSpeicher {
    @Override
    public void speichern(ArrayList<Produkt> produkte, String dateipfad) {
        for (Produkt produkt : produkte) {
            System.out.println(produkt.getName() + ": " + produkt.getPreis());
        }
    }
}
```

Hinweis: `dateipfad` wird hier nicht verwendet. Der Parameter bleibt trotzdem vorhanden, weil die Signatur zum Interface passen muss.

---

## Gemeinsames Interface ProduktSpeicher

```java
package ch.allianz.youngoitv.produktverwaltung;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;
import java.util.ArrayList;

public interface ProduktSpeicher {
    void speichern(ArrayList<Produkt> produkte, String dateipfad);
}
```

`ProduktSpeicher` ist der gemeinsame Vertrag für beide konkreten Klassen.

---

## CsvProduktSpeicher als erste Umsetzung

```java
package ch.allianz.youngoitv.produktverwaltung;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.ArrayList;

public class CsvProduktSpeicher implements ProduktSpeicher {
    @Override
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

`CsvProduktSpeicher` erfüllt denselben Vertrag, schreibt aber eine CSV-Datei.

---

## Aufgabe 4 – Main auf KonsolenProduktSpeicher umstellen

```java
package ch.allianz.youngoitv.produktverwaltung;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        ArrayList<Produkt> produkte = new ArrayList<>();
        produkte.add(new Produkt("Maus", 34.90));
        produkte.add(new Produkt("Tastatur", 79.90));

        ProduktSpeicher speicher = new KonsolenProduktSpeicher();
        speicher.speichern(produkte, "data/produkte.csv");
    }
}
```

Links steht weiterhin der Interface-Typ:

```text
ProduktSpeicher speicher
```

Rechts steht die konkrete Implementierung:

```text
new KonsolenProduktSpeicher()
```

---

## Aufgabe 5 – Verhalten beobachten

| Speicher | Beobachtung |
|---|---|
| `CsvProduktSpeicher` | Produkte werden in eine CSV-Datei geschrieben |
| `KonsolenProduktSpeicher` | Produkte werden auf der Konsole ausgegeben |

Gleich bleibt:

- `ProduktSpeicher` als Variablentyp
- `speicher.speichern(...)` als Methodenaufruf
- Methodensignatur im Interface
- Produktliste

Unterschiedlich ist die konkrete Umsetzung hinter `new`.

---

## Aufgabe 6 – Wieder zurück wechseln

Zurück zur CSV-Umsetzung:

```java
ProduktSpeicher speicher = new CsvProduktSpeicher();
```

Der restliche Aufruf bleibt gleich:

```java
speicher.speichern(produkte, "data/produkte.csv");
```

`Main` muss nicht komplett umgebaut werden, weil beide Klassen denselben Vertrag erfüllen.

---

## Aufgabe 7 – Gemeinsame Elemente finden

| Frage | Antwort |
|---|---|
| Welches Interface implementieren beide Klassen? | `ProduktSpeicher` |
| Welche Methode haben beide Klassen? | `speichern(...)` |
| Welche Parameter hat diese Methode? | `ArrayList<Produkt> produkte, String dateipfad` |
| Was ist bei beiden gleich? | Interface, Methodensignatur, Rückgabetyp |
| Was ist unterschiedlich? | CSV-Datei schreiben oder Konsole ausgeben |

---

## Aufgabe 8 – Vertrag und Umsetzung unterscheiden

| Aussage | Einordnung |
|---|---|
| `void speichern(ArrayList<Produkt> produkte, String dateipfad)` | Vertrag |
| Produkte mit Semikolon zu CSV-Zeilen zusammensetzen | Umsetzung |
| Produkte mit `System.out.println(...)` ausgeben | Umsetzung |
| `implements ProduktSpeicher` verwenden | Verbindung zur Vertragserfüllung |
| Datei mit `Files.write(...)` schreiben | Umsetzung |
| `Main` verwendet den Typ `ProduktSpeicher` | Nutzung des Vertrags |

---

## Aufgabe 9 – Warum kann Main gleich bleiben?

Mögliche Antwort:

```text
Main verwendet den Typ ProduktSpeicher und kennt deshalb nur den Vertrag.
Der Aufruf speicher.speichern(...) bleibt gleich, weil beide Klassen dieselbe Methode anbieten.
Welche Aktion ausgeführt wird, entscheidet die konkrete Klasse rechts von new.
Bei CsvProduktSpeicher wird eine Datei geschrieben.
Bei KonsolenProduktSpeicher werden die Produkte auf der Konsole ausgegeben.
```

---

## Aufgabe 10 – Signatur bewusst prüfen

Typischer Fehler:

```java
public void ausgeben(ArrayList<Produkt> produkte, String dateipfad) {
    // ...
}
```

Diese Methode erfüllt den Vertrag nicht, weil das Interface `speichern(...)` verlangt.

Weitere typische Signaturfehler:

- anderer Methodenname
- fehlender Parameter
- andere Reihenfolge der Parameter
- anderer Rückgabetyp

Korrektur: Die Signatur in jeder Implementierung muss exakt zum Interface passen.

---

## Aufgabe 11 – Einfache Prüfung wiederholen

Mögliche Notiz nach der Prüfung:

```text
mvn package erfolgreich.
Main verwendet ProduktSpeicher als Typ.
CsvProduktSpeicher und KonsolenProduktSpeicher erfüllen beide den Vertrag.
```

Wenn Tests vorhanden sind, ist `mvn test` vorzuziehen. Wenn keine Tests vorhanden sind, reicht für diese technische Prüfung `mvn package`.

---

## Transfer – BackupProduktSpeicher

Mögliche Antwort:

```text
BackupProduktSpeicher müsste ProduktSpeicher implementieren.
Die Klasse müsste ebenfalls speichern(ArrayList<Produkt> produkte, String dateipfad) anbieten.
Sie könnte vor dem Überschreiben zuerst eine Kopie der alten Datei erstellen.
Das wäre später nützlich, wenn Daten nicht versehentlich verloren gehen sollen.
```

Die Klasse wird hier nicht programmiert, weil sie zusätzliche Dateischritte braucht.

---

## Transfer – StatistikProduktSpeicher

Mögliche Antwort:

```text
StatistikProduktSpeicher ist als Idee kritisch.
Wenn nur Anzahl und Gesamtwert ausgegeben werden, wird eigentlich nicht gespeichert.
Die Klasse wäre eher ein Statistik-Service als ein ProduktSpeicher.
```

Wichtiger Punkt: Nicht jede mögliche Klasse passt sinnvoll zu einem bestehenden Interface. Der Vertrag muss zur Verantwortung passen.

---

## Transfer – JsonProduktSpeicher

Mögliche Antwort:

```text
JsonProduktSpeicher müsste dieselbe Methode speichern(...) besitzen.
Intern würde er Produkte anders formatieren als CsvProduktSpeicher.
JSON wird hier nicht umgesetzt, weil sonst ein neues Dateiformat vom eigentlichen Lernziel ablenkt.
KonsolenProduktSpeicher reicht, um gleiche Methode und anderes Verhalten sichtbar zu machen.
```

---

## Transfer – Nutzen austauschbarer Implementierungen

Mehrere Implementierungen sind später nützlich, weil Code gegen einen Vertrag arbeiten kann.

Beispiele:

- Eine einfache Konsolenimplementierung kann beim manuellen Prüfen helfen.
- Eine CSV-Implementierung kann echte Dateien schreiben.
- Später könnten Tests mit einer einfachen Ersatzimplementierung arbeiten.
- Services können klarer getrennt werden.

Gefahr: Zu viele Implementierungen zu früh machen das Programm schwerer verständlich.

---

## Typische Fehlerhinweise

| Fehler | Korrektur |
|---|---|
| Interface wird verändert statt eine zweite Klasse zu erstellen | `ProduktSpeicher` unverändert lassen |
| `implements ProduktSpeicher` fehlt | in beiden Speicherklassen ergänzen |
| Methodensignatur stimmt nicht überein | Namen, Parameter und Rückgabetyp angleichen |
| `Main` verwendet wieder konkrete Klassen als Typ | links `ProduktSpeicher` verwenden |
| beide Klassen machen dasselbe | Verhalten klar unterscheiden |
| `KonsolenProduktSpeicher` schreibt plötzlich Dateien | Konsolenklasse auf Konsolenausgabe beschränken |
| zu viele neue Implementierungen | nur eine zweite Implementierung praktisch bauen |

---

## Reflexion – mögliche Antworten

1. Gleich bleiben Interface, Methodensignatur, Variablentyp und Methodenaufruf in `Main`.
2. Das Interface hilft, weil beide Klassen denselben Vertrag erfüllen.
3. Der Vertrag legt fest, welche Methode vorhanden sein muss. Die Umsetzung entscheidet, was intern passiert.
4. `KonsolenProduktSpeicher` ist einfacher als eine Datenbank, weil keine neue Technik nötig ist.
5. Später wären zum Beispiel `BackupProduktSpeicher` oder ein anderer Datei-Export denkbar.

---

## Verifikation

Die Java-Beispiele wurden als temporäres Maven-Projekt unter `/tmp/mehrere-implementierungen-loesung-validierung` geprüft.

Ausgeführter Befehl:

```bash
mvn package
```

Ergebnis:

```text
BUILD SUCCESS
```

Hinweis: Im temporären Projekt wurden die Produktionsklassen kompiliert. Es waren keine Testklassen hinterlegt, deshalb wurden dort keine Tests ausgeführt.

Zusätzlich wurde die kompilierte `Main`-Klasse mit `KonsolenProduktSpeicher` ausgeführt:

```bash
java -cp target/classes ch.allianz.youngoitv.produktverwaltung.Main
```

Die Ausgabe zeigte:

```text
Maus: 34.9
Tastatur: 79.9
```
