# Lösungen – Unterschiedliche Objekte über dasselbe Interface verwenden

Diese Musterlösung zeigt die praktische Polymorphie mit der bekannten Produktverwaltung. Der Fokus liegt auf beobachtbarem Verhalten:

```text
gleicher Interface-Typ
gleicher Methodenaufruf
anderes konkretes Objekt
anderes Verhalten
```

Nicht verwendet werden:

- abstrakte Klassen
- `instanceof`
- Downcasting
- Dependency Injection
- Spring
- Factory
- Datenbank
- komplexe Vererbung

---

## Aufgabe 1 – Interface-Typ als Variable verwenden

Passende Lösung:

```java
ProduktSpeicher speicher;
```

Antworten:

| Frage | Antwort |
|---|---|
| Typ der Variable | `ProduktSpeicher` |
| Warum nicht `CsvProduktSpeicher`? | Dann könnte dieselbe Variable keinen `KonsolenProduktSpeicher` aufnehmen. |
| Welche Methode ist bekannt? | `speichern(...)` |

Kurzer Merksatz:

```text
Main kennt den Vertrag ProduktSpeicher, nicht die Details jeder konkreten Klasse.
```

---

## Gemeinsamer Vertrag ProduktSpeicher

```java
package ch.allianz.youngoitv.produktverwaltung;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;
import java.util.ArrayList;

public interface ProduktSpeicher {
    void speichern(ArrayList<Produkt> produkte, String dateipfad);
}
```

Das Interface legt nur fest, welche Methode vorhanden sein muss.

---

## CsvProduktSpeicher

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

        for (Produkt produkt : produkte) {
            zeilen.add(produkt.getName() + ";" + produkt.getPreis());
        }

        try {
            Path pfad = Path.of(dateipfad);
            Path ordner = pfad.getParent();

            if (ordner != null) {
                Files.createDirectories(ordner);
            }

            Files.write(pfad, zeilen);
        } catch (IOException e) {
            System.out.println("Datei konnte nicht gespeichert werden: " + dateipfad);
        }
    }
}
```

Verhalten: Produkte werden als CSV-Datei gespeichert.

---

## KonsolenProduktSpeicher

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

Verhalten: Produkte werden auf der Konsole ausgegeben.

Hinweis: `dateipfad` wird hier nicht benötigt. Der Parameter bleibt trotzdem erhalten, weil die Signatur zum Interface passen muss.

---

## Aufgaben 2 und 3 – Zwei konkrete Objekte verwenden

```java
ProduktSpeicher speicher;

speicher = new CsvProduktSpeicher();
speicher.speichern(produkte, "data/produkte.csv");

speicher = new KonsolenProduktSpeicher();
speicher.speichern(produkte, "data/produkte.csv");
```

Wichtig:

- `speicher` bleibt vom Typ `ProduktSpeicher`.
- `speicher.speichern(...)` bleibt gleich.
- Das konkrete Objekt wird gewechselt.
- Das Verhalten ändert sich.

---

## Aufgaben 4 und 5 – Verhalten vergleichen

| Schritt | Inhalt der Variable `speicher` | Methodenaufruf | Beobachtung |
|---|---|---|---|
| 1 | `new CsvProduktSpeicher()` | `speicher.speichern(...)` | CSV-Datei wird geschrieben |
| 2 | `new KonsolenProduktSpeicher()` | `speicher.speichern(...)` | Produkte werden auf der Konsole ausgegeben |

Gleich bleibt:

- Variablentyp `ProduktSpeicher`
- Methodenaufruf `speicher.speichern(...)`
- Produktliste
- restlicher Ablauf in `Main`

Geändert wird:

- das konkrete Objekt hinter der Variable
- der tatsächlich ausgeführte Code
- die sichtbare Wirkung

---

## Kompakte Main-Lösung

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

        speicher = new KonsolenProduktSpeicher();
        speicher.speichern(produkte, "data/produkte.csv");
    }
}
```

`Main` bleibt weitgehend gleich, weil `Main` nur den gemeinsamen Vertrag nutzt.

---

## Aufgabe 6 – Beide Implementierungen nacheinander

Mögliche Beobachtung:

```text
Beim ersten Aufruf wird data/produkte.csv geschrieben.
Beim zweiten Aufruf erscheinen dieselben Produkte auf der Konsole.
Der Methodenaufruf ist in beiden Fällen gleich.
Die konkrete Klasse in der Variable entscheidet das Verhalten.
```

---

## Aufgabe 7 – Ablauf dokumentieren

| Zeitpunkt | Variable `speicher` enthält | Java ruft Code aus dieser Klasse auf |
|---|---|---|
| erster Aufruf | `CsvProduktSpeicher` | `CsvProduktSpeicher` |
| zweiter Aufruf | `KonsolenProduktSpeicher` | `KonsolenProduktSpeicher` |

Kurze Erklärung:

```text
Die Variable hat den Interface-Typ ProduktSpeicher.
Zur Laufzeit steckt aber ein konkretes Objekt in dieser Variable.
Java führt die Methode der konkreten Klasse aus.
```

---

## Aufgabe 8 – Verantwortlichkeitstabelle

| Teil | Verantwortung |
|---|---|
| `ProduktSpeicher` | legt den gemeinsamen Vertrag fest |
| `CsvProduktSpeicher` | speichert Produkte als CSV-Datei |
| `KonsolenProduktSpeicher` | gibt Produkte auf der Konsole aus |
| `Main` | erstellt Produkte, wählt ein Speicherobjekt und ruft `speichern(...)` auf |

Zusatzfrage:

```text
Wenn Main selbst CSV-Dateien schreibt und Konsolenausgaben formatiert,
wird Main wieder zu gross. Die Verantwortlichkeiten wären vermischt.
```

---

## Aufgabe 9 – Gleiche Methode, unterschiedliche Wirkung

Mögliche Antwort:

```text
Die Variable hat den Interface-Typ ProduktSpeicher.
Deshalb darf sie jedes Objekt aufnehmen, das ProduktSpeicher implementiert.
CsvProduktSpeicher und KonsolenProduktSpeicher bieten beide speichern(...) an.
Der Aufruf bleibt gleich, aber Java verwendet den Code der konkreten Klasse.
Darum wird einmal eine CSV-Datei geschrieben und einmal auf die Konsole ausgegeben.
```

Das ist praktische Polymorphie:

```text
gleicher Typ, gleicher Aufruf, unterschiedliches konkretes Verhalten
```

Wichtig: Zuerst wird das Verhalten beobachtet. Der Fachbegriff Polymorphie fasst diese Beobachtung nur zusammen.

---

## Transfer – Doppeltes Speichern

Eine einfache Idee ohne neue Architektur:

```java
ProduktSpeicher speicher = new CsvProduktSpeicher();
speicher.speichern(produkte, "data/produkte.csv");

speicher = new KonsolenProduktSpeicher();
speicher.speichern(produkte, "data/produkte.csv");
```

Beide Aufrufe nutzen denselben Vertrag. Es wird keine Factory und keine Dependency Injection benötigt.

---

## Transfer – LoggingProduktSpeicher

Mögliche Skizze:

```text
LoggingProduktSpeicher implements ProduktSpeicher
Methode: speichern(ArrayList<Produkt> produkte, String dateipfad)
Verhalten: gibt aus, wie viele Produkte gespeichert werden sollen
```

Beispielausgabe:

```text
Speichern gestartet: 2 Produkte
```

Diese Klasse wird hier nicht umgesetzt, weil sonst zu viele Implementierungen gleichzeitig entstehen.

---

## Transfer – BackupProduktSpeicher

Mögliche Skizze:

```text
BackupProduktSpeicher implements ProduktSpeicher
Methode: speichern(ArrayList<Produkt> produkte, String dateipfad)
Verhalten: könnte zuerst eine Sicherungskopie erstellen
```

`Main` könnte weiterhin mit `ProduktSpeicher` arbeiten, wenn die Klasse denselben Vertrag erfüllt.

---

## Transfer – Warum erleichtert Polymorphie Erweiterungen?

Mögliche Antwort:

```text
Gleich bleiben müssen Interface und Methodensignatur.
Unterschiedlich sein darf die konkrete Umsetzung.
Dadurch kann später eine neue Speicherklasse ergänzt werden,
ohne den restlichen Ablauf in Main stark umzubauen.
```

---

## Typische Fehlerhinweise

| Fehler | Korrektur |
|---|---|
| `new ProduktSpeicher()` verwenden | eine konkrete Klasse erzeugen, z. B. `new CsvProduktSpeicher()` |
| Variable als `CsvProduktSpeicher` deklarieren | links den Interface-Typ `ProduktSpeicher` verwenden |
| `speichern(...)` unterschiedlich benennen | Signatur aus dem Interface exakt einhalten |
| `instanceof` verwenden | für diese Einheit unnötig; das konkrete Objekt entscheidet selbst |
| Downcasting verwenden | vermeiden; über den Interface-Typ arbeiten |
| `Main` mit vielen Speicherfällen füllen | `Main` soll nur das passende Objekt verwenden und `speichern(...)` aufrufen |

---

## Reflexion – mögliche Antworten

| Frage | Mögliche Antwort |
|---|---|
| Was bleibt gleich? | Interface-Typ, Methodenname, Parameter und Aufruf |
| Was verändert sich? | konkrete Klasse und sichtbares Verhalten |
| Warum hilft das Interface? | beide Klassen erfüllen denselben Vertrag |
| Warum unterschiedliches Verhalten? | jede konkrete Klasse hat ihre eigene Umsetzung |
| Weitere Implementierungen? | z. B. `BackupProduktSpeicher` oder `LoggingProduktSpeicher` als spätere Idee |

---

## Verifikation

Die Java-Beispiele wurden als temporäres Maven-Projekt geprüft.

Ausgeführt:

```bash
mvn package
```

Ergebnis:

```text
BUILD SUCCESS
```

Zusätzlich wurde `Main` ausgeführt. Beobachtung:

```text
Maus: 34.9
Tastatur: 79.9
```

Die CSV-Datei enthielt:

```text
Maus;34.9
Tastatur;79.9
```

Es waren keine Testklassen hinterlegt; deshalb wurde `mvn package` statt `mvn test` als technische Prüfung dokumentiert.
