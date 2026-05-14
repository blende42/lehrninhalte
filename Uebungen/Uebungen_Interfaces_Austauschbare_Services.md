# Übungen – Interfaces für austauschbare Services

## Vorwissen

Du brauchst:

- Klassen und Objekte
- `ArrayList`
- Methoden mit Parametern
- CSV-Speichern
- Verantwortlichkeiten in der Produktverwaltung
- `Main` als Orchestrator
- Maven-Projektstruktur

Nicht verwendet werden:

- Spring
- Dependency Injection
- abstrakte Klassen
- komplexe Polymorphie
- Datenbanken
- ORM
- formales Repository-Pattern
- generische CSV-Frameworks

---

## Vorbereitung

Arbeite mit der bekannten Produktverwaltung.

Beispielstruktur:

```text
produktverwaltung-maven/
  pom.xml
  data/
    produkte.csv
  src/main/java/
    ch/allianz/youngoitv/produktverwaltung/
      Main.java
      CsvProduktLeser.java
      CsvProduktSpeicher.java
      ProduktSpeicher.java
      model/Produkt.java
      service/ProduktVerwaltung.java
```

Die bestehende Speicherklasse soll weiterhin CSV-Dateien schreiben.

Ziel dieser Übung:

```text
Main verwendet ProduktSpeicher als Typ.
CsvProduktSpeicher bleibt die konkrete Umsetzung.
```

Prüfe nach der Umstellung:

```bash
mvn test
```

Wenn keine Tests vorhanden sind, verwende mindestens:

```bash
mvn package
```

---

## Basis

### Aufgabe 1 – Bestehende Speichermethode finden

Öffne `CsvProduktSpeicher`.

Auftrag:

1. Finde die Methode, die Produkte speichert.
2. Notiere Methodennamen, Parameter und Rückgabetyp.
3. Entscheide, welche Teile zur Umsetzung gehören.

Beispiel:

```text
Methode: speichern
Parameter: ArrayList<Produkt>, String dateipfad
Rückgabetyp: void
Umsetzung: CSV-Zeilen erzeugen und Datei schreiben
```

Falls deine bestehende Methode `speichereProdukte(...)` heisst, darfst du diesen Namen beibehalten. Wichtig ist, dass Interface und Klasse denselben Namen, dieselben Parameter und denselben Rückgabetyp verwenden.

---

### Aufgabe 2 – Interface ProduktSpeicher erstellen

Erstelle ein Interface `ProduktSpeicher`.

Auftrag:

1. Lege `ProduktSpeicher.java` im gleichen Package wie `CsvProduktSpeicher` an.
2. Definiere genau eine Methode.
3. Verwende dieselbe Methodensignatur wie im Speicher.

Beispiel:

```java
public interface ProduktSpeicher {
    void speichern(ArrayList<Produkt> produkte, String dateipfad);
}
```

Ergänze im vollständigen Code die nötigen Imports für `ArrayList` und `Produkt`.

Wichtig: Das Interface enthält keine Schleife, kein `Files.write(...)` und keine CSV-Details.

---

### Aufgabe 3 – CsvProduktSpeicher anpassen

Passe `CsvProduktSpeicher` an.

Auftrag:

1. Ergänze `implements ProduktSpeicher`.
2. Stelle sicher, dass die Methode exakt zum Interface passt.
3. Lasse die bestehende CSV-Logik in `CsvProduktSpeicher`.

Beispiel:

```java
public class CsvProduktSpeicher implements ProduktSpeicher {
    public void speichern(ArrayList<Produkt> produkte, String dateipfad) {
        // bestehende CSV-Logik bleibt hier
    }
}
```

---

### Aufgabe 4 – Main gegen das Interface schreiben

Passe `Main` an.

Vorher:

```java
CsvProduktSpeicher speicher = new CsvProduktSpeicher();
speicher.speichern(produkte, "data/produkte.csv");
```

Nachher:

```java
ProduktSpeicher speicher = new CsvProduktSpeicher();
speicher.speichern(produkte, "data/produkte.csv");
```

Auftrag:

1. Ändere den Variablentyp auf `ProduktSpeicher`.
2. Erzeuge weiterhin `new CsvProduktSpeicher()`.
3. Speichere wie vorher.

---

### Aufgabe 5 – Verhalten prüfen

Prüfe, ob sich das Verhalten nicht verändert hat.

Auftrag:

1. Starte das Programm oder führe `mvn test` aus.
2. Prüfe, ob die CSV-Datei weiterhin geschrieben wird.
3. Notiere, was sich geändert hat.
4. Notiere, was gleich geblieben ist.

Erwartung:

```text
Geändert: Main verwendet ProduktSpeicher als Typ.
Gleich: Produkte werden weiterhin als CSV gespeichert.
```

---

## Vertiefung

### Aufgabe 6 – Vertrag und Umsetzung unterscheiden

Ordne die Aussagen zu.

| Aussage | Vertrag oder Umsetzung? |
|---|---|
| Methode `speichern(...)` muss vorhanden sein | |
| CSV-Zeile mit Semikolon erzeugen | |
| Datei mit `Files.write(...)` schreiben | |
| Rückgabetyp ist `void` | |
| Preis aus `Produkt` lesen | |

Verwende:

- Vertrag
- Umsetzung

---

### Aufgabe 7 – Codeabschnitte zuordnen

Ordne diese Codezeilen ein.

```java
public interface ProduktSpeicher
```

```java
void speichern(ArrayList<Produkt> produkte, String dateipfad);
```

```java
public class CsvProduktSpeicher implements ProduktSpeicher
```

```java
zeilen.add(produkt.getName() + ";" + produkt.getPreis());
```

```java
Files.write(Path.of(dateipfad), zeilen);
```

Auftrag:

1. Markiere, was zum Interface gehört.
2. Markiere, was zur konkreten CSV-Umsetzung gehört.
3. Begründe zwei Zuordnungen kurz.

---

### Aufgabe 8 – Methodennamen und Parameter prüfen

Prüfe, ob Interface und Implementierung zusammenpassen.

Checkliste:

- gleicher Methodenname
- gleiche Parameter
- gleiche Reihenfolge der Parameter
- gleicher Rückgabetyp
- `implements ProduktSpeicher` vorhanden

Auftrag:

1. Erzeuge absichtlich einen kleinen Signaturfehler, zum Beispiel nur kurz einen anderen Methodennamen.
2. Führe `mvn test` oder `mvn package` aus.
3. Lies die Fehlermeldung.
4. Korrigiere den Fehler vor der Abgabe wieder.

---

### Aufgabe 9 – Main bewusst lesen

Lies deine `Main`.

Auftrag:

1. Suche die Stelle mit `ProduktSpeicher speicher`.
2. Erkläre in zwei Sätzen, warum dort links Interface und rechts konkrete Klasse stehen.
3. Prüfe, ob `Main` weiterhin keine CSV-Details enthält.

Hilfssatz:

```text
Main kennt den Vertrag. CsvProduktSpeicher erledigt die konkrete Arbeit.
```

---

## Transfer

Diese Aufgaben sind anspruchsvoller. Bearbeite sie erst, wenn Basis und Vertiefung stabil funktionieren.

### Transfer 1 – Zweite Implementierung überlegen

Überlege eine zweite mögliche Implementierung.

Beispiele:

- `KonsolenProduktSpeicher`
- `BackupProduktSpeicher`

Auftrag:

1. Wähle eine mögliche Klasse.
2. Beschreibe ihre Aufgabe in drei Sätzen.
3. Entscheide, ob sie denselben Vertrag `ProduktSpeicher` erfüllen könnte.

Du musst die Klasse noch nicht implementieren.

---

### Transfer 2 – KonsolenProduktSpeicher als Idee

Ein `KonsolenProduktSpeicher` könnte Produkte nur ausgeben.

Auftrag:

1. Skizziere, was `speichern(...)` in dieser Klasse tun würde.
2. Erkläre, warum trotzdem derselbe Methodenvertrag sinnvoll sein kann.
3. Nenne einen Nachteil dieser Implementierung.

Beispiel:

```text
KonsolenProduktSpeicher speichert nicht dauerhaft.
Er eignet sich eher zum Testen oder Demonstrieren.
```

---

### Transfer 3 – BackupProduktSpeicher als Idee

Ein `BackupProduktSpeicher` könnte vor dem Speichern eine Kopie der alten Datei erzeugen.

Auftrag:

1. Beschreibe die Zusatzaufgabe.
2. Entscheide, ob diese Klasse direkt Datei-Logik enthalten darf.
3. Begründe, warum diese Idee anspruchsvoller ist als `CsvProduktSpeicher`.

---

### Transfer 4 – Nutzen für spätere Themen

Erkläre kurz, warum Interfaces später hilfreich sein können.

Nutze diese Begriffe:

- Tests
- Services
- REST
- austauschbare Implementierung

Wichtig: Beschreibe nur die Idee. Baue noch keine REST-Anwendung und kein Framework ein.

---

## Typische Fehler prüfen

Prüfe deinen Code bewusst:

- Enthält das Interface Implementierungsdetails?
- Passt die Methodensignatur exakt?
- Implementiert `CsvProduktSpeicher` das Interface wirklich?
- Verwendet `Main` den Typ `ProduktSpeicher`?
- Hat sich das Verhalten beim Speichern versehentlich geändert?
- Wurden `mvn test` oder `mvn package` ausgeführt?
- Wurde nur ein Interface eingeführt?
- Sind Namen wie `ProduktSpeicher` und `CsvProduktSpeicher` klar unterscheidbar?

---

## Reflexion

Beantworte kurz:

1. Warum ist ein Interface ein Vertrag?
2. Was bedeutet austauschbar?
3. Was gewinnt man, wenn `Main` gegen ein Interface arbeitet?
4. Warum führen wir zunächst nur ein Interface ein?
5. Welche weiteren Services könnten später austauschbar werden?
