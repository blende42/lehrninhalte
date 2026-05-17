# Lösungen – Gemeinsamen Code mit Vererbung wiederverwenden

Diese Musterlösung zeigt eine einfache Standardlösung. Ziel ist nicht eine grosse Vererbungshierarchie, sondern ein kleiner Refactoring-Schritt: gemeinsamer Hilfscode wird in eine kleine Basisklasse verschoben.

Nicht verwendet werden:

- abstrakte Klassen als Vertiefung
- tiefe Vererbungshierarchien
- komplexes `super(...)`
- `instanceof`
- Downcasting
- Template Method
- Dependency Injection
- Spring

---

## Basis

### Aufgaben 1 und 2 – Gemeinsamen Code erkennen

| Beobachtung | Einordnung | Begründung |
|---|---|---|
| Produktname lesen | gemeinsam | beide Speicherklassen brauchen `produkt.getName()` |
| Produktpreis lesen | gemeinsam | beide Speicherklassen brauchen `produkt.getPreis()` |
| CSV-Zeile mit `;` erzeugen | konkret | gehört zum CSV-Format |
| Konsolenzeile mit `:` erzeugen | konkret | gehört zur Konsolenausgabe |
| Datei schreiben | konkret | nur `CsvProduktSpeicher` schreibt eine Datei |
| Konsole ausgeben | konkret | nur `KonsolenProduktSpeicher` gibt direkt aus |

Eine gemeinsame Hilfsmethode ist hier sinnvoll, weil beide Klassen Name und Preis zusammensetzen. Das Trennzeichen bleibt aber variabel, damit CSV und Konsole unterschiedlich bleiben können.

---

## Gemeinsames Interface `ProduktSpeicher`

```java
package ch.allianz.youngoitv.produktverwaltung;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;
import java.util.ArrayList;

public interface ProduktSpeicher {
    void speichern(ArrayList<Produkt> produkte, String dateipfad);
}
```

`ProduktSpeicher` beschreibt den Vertrag. Jede Implementierung muss `speichern(...)` anbieten.

---

## Kleine Basisklasse `ProduktSpeicherBasis`

```java
package ch.allianz.youngoitv.produktverwaltung;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;

public class ProduktSpeicherBasis {
    protected String produktZeile(Produkt produkt, String trennzeichen) {
        return produkt.getName() + trennzeichen + produkt.getPreis();
    }
}
```

Die Basisklasse bleibt bewusst klein. Sie enthält nur gemeinsame Hilfslogik und keine Speicherentscheidung.

`protected` passt hier, weil die Methode für Unterklassen gedacht ist. Sie gehört nicht zum öffentlichen Vertrag des Interfaces.

Die Klasse wird hier bewusst nicht als `abstract` eingeführt, weil abstrakte Klassen in dieser Einheit nicht vertieft werden.

---

## `CsvProduktSpeicher`

```java
package ch.allianz.youngoitv.produktverwaltung;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.ArrayList;

public class CsvProduktSpeicher extends ProduktSpeicherBasis implements ProduktSpeicher {
    @Override
    public void speichern(ArrayList<Produkt> produkte, String dateipfad) {
        ArrayList<String> zeilen = new ArrayList<>();

        for (Produkt produkt : produkte) {
            zeilen.add(produktZeile(produkt, ";"));
        }

        try {
            Files.write(Path.of(dateipfad), zeilen);
        } catch (IOException e) {
            System.out.println("Datei konnte nicht gespeichert werden: " + dateipfad);
        }
    }
}
```

`CsvProduktSpeicher` erbt die Hilfsmethode, bleibt aber für CSV zuständig. Das Schreiben der Datei bleibt in der konkreten Klasse.

---

## `KonsolenProduktSpeicher`

```java
package ch.allianz.youngoitv.produktverwaltung;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;
import java.util.ArrayList;

public class KonsolenProduktSpeicher extends ProduktSpeicherBasis implements ProduktSpeicher {
    @Override
    public void speichern(ArrayList<Produkt> produkte, String dateipfad) {
        for (Produkt produkt : produkte) {
            System.out.println(produktZeile(produkt, ": "));
        }
    }
}
```

Hinweis: `dateipfad` wird hier nicht verwendet. Der Parameter bleibt trotzdem vorhanden, weil die Signatur zum Interface passt.

`KonsolenProduktSpeicher` erbt dieselbe Hilfsmethode, gibt aber weiterhin auf der Konsole aus.

---

## Beispiel-`Main` zur Prüfung

```java
package ch.allianz.youngoitv.produktverwaltung;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        ArrayList<Produkt> produkte = new ArrayList<>();
        produkte.add(new Produkt("Maus", 34.9));
        produkte.add(new Produkt("Tastatur", 79.9));

        ProduktSpeicher csvSpeicher = new CsvProduktSpeicher();
        csvSpeicher.speichern(produkte, "target/produkte.csv");

        ProduktSpeicher konsolenSpeicher = new KonsolenProduktSpeicher();
        konsolenSpeicher.speichern(produkte, "target/produkte.csv");
    }
}
```

Erwartete Konsolenausgabe:

```text
Maus: 34.9
Tastatur: 79.9
```

Erwarteter Dateiinhalt in `target/produkte.csv`:

```text
Maus;34.9
Tastatur;79.9
```

Das Verhalten bleibt fachlich gleich: CSV wird als CSV geschrieben, Konsole bleibt Konsole.

---

## Vertiefung

### Aufgabe 7 – Was gehört wohin?

| Methode oder Logik | Interface | Basisklasse | konkrete Klasse |
|---|---|---|---|
| `speichern(...)` | ja, als Vertrag | nein | ja, als Umsetzung |
| `produktZeile(...)` | nein | ja | wird von Unterklassen genutzt |
| Datei mit `Files.write(...)` schreiben | nein | nein | `CsvProduktSpeicher` |
| `System.out.println(...)` verwenden | nein | nein | `KonsolenProduktSpeicher` |
| `istProduktListeLeer(...)` | nein | eventuell | nur wenn beide Klassen es gleich brauchen |
| CSV-Trennzeichen festlegen | nein | nein | `CsvProduktSpeicher` |

`speichern(...)` gehört nicht in die Basisklasse, weil CSV-Datei und Konsole unterschiedliche Speicherlogik haben.

### Aufgabe 8 – Interface und Basisklasse vergleichen

| Element | Aufgabe | Beispiel im Projekt |
|---|---|---|
| Interface | Vertrag beschreiben | `ProduktSpeicher` mit `speichern(...)` |
| Basisklasse | gemeinsame Implementierung bereitstellen | `ProduktSpeicherBasis` mit `produktZeile(...)` |
| konkrete Klasse | spezifisches Verhalten umsetzen | CSV schreiben oder Konsole ausgeben |

Kurzform:

```text
Interface = Was muss angeboten werden?
Vererbung = Welcher gemeinsame Code wird wiederverwendet?
Konkrete Klasse = Was passiert wirklich?
```

### Aufgabe 9 – Prüfung nach dem Refactoring

Mögliche Notiz:

```text
mvn package erfolgreich.
Main ausgeführt.
CsvProduktSpeicher schreibt target/produkte.csv.
KonsolenProduktSpeicher gibt Produkte auf der Konsole aus.
Das Verhalten bleibt gleich.
```

### Aufgabe 10 – Lesbarkeit und Wartbarkeit

Mögliche Antwort:

```text
Die Basisklasse hilft hier, weil die gemeinsame Formatierung an einer Stelle steht.
Sie ist noch klein genug, weil sie keine Datei- oder Konsolenlogik enthält.
Eine Änderung an der gemeinsamen Grundformatierung wäre nun einfacher.
CSV-spezifische Änderungen bleiben weiterhin im CsvProduktSpeicher.
Konsolenspezifische Änderungen bleiben weiterhin im KonsolenProduktSpeicher.
```

---

## Transfer

### Aufgabe 11 – Weitere Hilfsmethoden prüfen

`istLeer(...)` kann sinnvoll sein, wenn beide Klassen leere Produktlisten gleich behandeln:

```java
protected boolean istLeer(ArrayList<Produkt> produkte) {
    return produkte.isEmpty();
}
```

`anzahlMeldung(...)` gehört nur dann in die Basisklasse, wenn beide Klassen dieselbe Meldung verwenden. Wenn nur die Konsole eine Meldung ausgibt, bleibt die Methode besser im `KonsolenProduktSpeicher`.

### Aufgabe 12 – Ungeeignete Auslagerung

Diese Methode gehört nicht in die Basisklasse:

```java
public void speichern(ArrayList<Produkt> produkte, String ziel) {
    // schreibt manchmal in eine Datei und manchmal auf die Konsole
}
```

Problem:

- Die Methode müsste CSV und Konsole gleichzeitig kennen.
- Die Basisklasse würde zu viel Verantwortung übernehmen.
- Die konkreten Klassen würden unklar.
- Es entstehen schnell Fallunterscheidungen statt klare Klassen.

### Aufgabe 13 – Wann ist Vererbung nicht sinnvoll?

| Vererbung ist sinnvoll, wenn ... | Vererbung ist nicht sinnvoll, wenn ... |
|---|---|
| wirklich gemeinsamer Code vorhanden ist | Code nur zufällig ähnlich aussieht |
| die Basisklasse klein bleibt | die Basisklasse viele Spezialfälle kennen muss |
| das Verhalten nach dem Umbau gleich bleibt | konkrete Klassen ihre klare Verantwortung verlieren |

### Aufgabe 14 – Alternative mit Hilfsklasse

Eine mögliche Alternative:

```java
public class ProduktFormatierer {
    public String produktZeile(Produkt produkt, String trennzeichen) {
        return produkt.getName() + trennzeichen + produkt.getPreis();
    }
}
```

Vorteil:

```text
CsvProduktSpeicher und KonsolenProduktSpeicher müssen nicht von einer gemeinsamen Basisklasse erben.
```

Nachteil:

```text
Beide Klassen brauchen ein zusätzliches Hilfsobjekt oder erstellen den Formatierer selbst.
```

Für diese Einheit ist die Basisklasse passend, weil genau Vererbung als Wiederverwendungsidee geübt wird. In grösseren Projekten muss man beide Varianten bewusst abwägen.

---

## Typische Fehlerhinweise

| Fehler | Korrektur |
|---|---|
| `implements ProduktSpeicher` wird entfernt | `extends` und `implements` lösen unterschiedliche Probleme und können zusammen vorkommen |
| `ProduktSpeicherBasis` implementiert unnötig das Interface | die Basisklasse enthält nur Hilfsmethoden, sie speichert nicht selbst |
| `speichern(...)` wird in die Basisklasse verschoben | konkrete Speicherlogik bleibt in den konkreten Klassen |
| CSV- und Konsolenlogik werden vermischt | Unterschiede bewusst erhalten |
| Basisklasse heisst nur `Basis` | Name soll die Verantwortung zeigen, zum Beispiel `ProduktSpeicherBasis` |
| Nach dem Refactoring wird nicht geprüft | mindestens `mvn package`, besser vorhandene Tests mit `mvn test` |
| `instanceof` wird eingebaut | Klassen sollen nicht über Typabfragen gesteuert werden |

---

## Kurze Reflexion

Der wirklich gemeinsame Code ist hier die einfache Produktformatierung aus Name, Trennzeichen und Preis. Datei schreiben und Konsole ausgeben bleiben bewusst in den konkreten Klassen.

Ein Interface beschreibt den Vertrag. Vererbung teilt gemeinsame Implementierung. Beides kann zusammen verwendet werden, löst aber unterschiedliche Probleme.

Vererbung ist nicht immer die richtige Lösung. Sie ist sinnvoll, wenn die Basisklasse klein bleibt und wirklich gemeinsamer Code wiederverwendet wird. Sie ist problematisch, wenn Unterschiede versteckt werden oder die Basisklasse zu viele Spezialfälle kennen muss.

Tests oder mindestens ein Maven-Build helfen, weil Refactoring die Struktur ändern soll, nicht das gewünschte Verhalten.

---

## Verifikation

Die Java-Beispiele wurden mit einem temporären Maven-Projekt geprüft:

```bash
mvn package
```

Ergebnis:

```text
BUILD SUCCESS
```

Zusätzlich wurde `Main` ausgeführt:

```bash
java -cp target/classes ch.allianz.youngoitv.produktverwaltung.Main
```

Ergebnis:

```text
Maus: 34.9
Tastatur: 79.9
```

Die Datei `target/produkte.csv` enthielt:

```text
Maus;34.9
Tastatur;79.9
```

Es waren keine JUnit-Tests im temporären Projekt hinterlegt. Darum wurde mit `mvn package` und einer manuellen Ausführung von `Main` geprüft.
