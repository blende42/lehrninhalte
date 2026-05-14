# Übungen – Mehrere Klassen mit demselben Interface

## Vorwissen

Du brauchst:

- Klassen und Objekte
- `ArrayList`
- Methoden mit Parametern
- CSV-Speichern
- Verantwortlichkeiten in der Produktverwaltung
- `ProduktSpeicher` als Interface
- `CsvProduktSpeicher implements ProduktSpeicher`
- `Main` als Orchestrator
- Maven-Projektstruktur

Nicht verwendet werden:

- Spring
- Dependency Injection
- Factory
- abstrakte Klassen
- Datenbanken
- Repository-Pattern
- komplexe Polymorphie

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
      KonsolenProduktSpeicher.java
      ProduktSpeicher.java
      model/Produkt.java
      service/ProduktVerwaltung.java
```

`KonsolenProduktSpeicher.java` ist die neue Datei, die du in dieser Übung ergänzt.

Ziel dieser Übung:

```text
Eine zweite Klasse implementiert ProduktSpeicher.
Main arbeitet weiterhin mit ProduktSpeicher.
Nur die konkrete Klasse wird gewechselt.
```

Prüfe nach praktischen Änderungen:

```bash
mvn test
```

Wenn keine Tests vorhanden sind, verwende mindestens:

```bash
mvn package
```

---

## Basis

### Aufgabe 1 – Interface erneut lesen

Öffne `ProduktSpeicher`.

Auftrag:

1. Notiere den Methodennamen.
2. Notiere die Parameter in der richtigen Reihenfolge.
3. Notiere den Rückgabetyp.
4. Schreibe in einem Satz, was der Vertrag verlangt.

Beispiel:

```text
Der Vertrag verlangt eine Methode speichern(...), die eine Produktliste entgegennimmt.
```

---

### Aufgabe 2 – KonsolenProduktSpeicher erstellen

Erstelle die Klasse `KonsolenProduktSpeicher` im gleichen Package wie `CsvProduktSpeicher`.

Auftrag:

1. Lege `KonsolenProduktSpeicher.java` an.
2. Ergänze `implements ProduktSpeicher`.
3. Implementiere dieselbe Methode wie im Interface.
4. Verwende keine Datei-Logik in dieser Klasse.

Grundstruktur:

```java
public class KonsolenProduktSpeicher implements ProduktSpeicher {
    @Override
    public void speichern(ArrayList<Produkt> produkte, String dateipfad) {
        // Produkte auf der Konsole ausgeben
    }
}
```

Ergänze im vollständigen Code die passenden Imports für `ArrayList` und `Produkt`.

---

### Aufgabe 3 – speichern(...) für die Konsole umsetzen

Setze die Methode so um, dass alle Produkte ausgegeben werden.

Beispielausgabe:

```text
Tastatur: 49.9
Maus: 19.9
Monitor: 179.0
```

Mögliche Umsetzung:

```java
for (Produkt produkt : produkte) {
    System.out.println(produkt.getName() + ": " + produkt.getPreis());
}
```

Wichtig:

- Die Methode heisst gleich wie im Interface.
- Die Parameter bleiben gleich.
- Der Rückgabetyp bleibt gleich.
- Der Unterschied liegt nur im Verhalten.

---

### Aufgabe 4 – Main auf KonsolenProduktSpeicher umstellen

Suche in `Main` die Stelle, an der der Speicher erzeugt wird.

Vorher:

```java
ProduktSpeicher speicher = new CsvProduktSpeicher();
```

Nachher:

```java
ProduktSpeicher speicher = new KonsolenProduktSpeicher();
```

Auftrag:

1. Ändere nur die konkrete Klasse rechts von `new`.
2. Lasse den Variablentyp `ProduktSpeicher`.
3. Lasse den Aufruf `speicher.speichern(...)` gleich.
4. Baue oder teste das Projekt.

---

### Aufgabe 5 – Verhalten beobachten

Führe das Programm aus oder verwende die vorhandenen Prüfungen.

Auftrag:

1. Notiere, was bei `CsvProduktSpeicher` passiert.
2. Notiere, was bei `KonsolenProduktSpeicher` passiert.
3. Markiere, welche Zeile in `Main` geändert wurde.
4. Notiere, welche Zeilen in `Main` gleich geblieben sind.

Erwartung:

| Speicher | Beobachtung |
|---|---|
| `CsvProduktSpeicher` | Produkte werden in eine CSV-Datei geschrieben |
| `KonsolenProduktSpeicher` | Produkte werden auf der Konsole ausgegeben |

---

### Aufgabe 6 – Wieder zurück wechseln

Stelle `Main` wieder auf die CSV-Implementierung zurück.

```java
ProduktSpeicher speicher = new CsvProduktSpeicher();
```

Auftrag:

1. Prüfe, ob das Projekt wieder baut.
2. Prüfe, ob die CSV-Datei wieder geschrieben wird.
3. Erkläre, warum `Main` nicht komplett umgebaut werden musste.

---

## Vertiefung

### Aufgabe 7 – Gemeinsame Elemente finden

Vergleiche `CsvProduktSpeicher` und `KonsolenProduktSpeicher`.

Fülle die Tabelle aus:

| Frage | Antwort |
|---|---|
| Welches Interface implementieren beide Klassen? | |
| Welche Methode haben beide Klassen? | |
| Welche Parameter hat diese Methode? | |
| Was ist bei beiden gleich? | |
| Was ist unterschiedlich? | |

---

### Aufgabe 8 – Vertrag und Umsetzung unterscheiden

Ordne die Aussagen zu.

| Aussage | Vertrag oder Umsetzung? |
|---|---|
| `void speichern(ArrayList<Produkt> produkte, String dateipfad)` | |
| Produkte mit Semikolon zu CSV-Zeilen zusammensetzen | |
| Produkte mit `System.out.println(...)` ausgeben | |
| `implements ProduktSpeicher` verwenden | |
| Datei mit `Files.write(...)` schreiben | |
| `Main` verwendet den Typ `ProduktSpeicher` | |

Verwende:

- Vertrag
- Umsetzung
- Nutzung des Vertrags

---

### Aufgabe 9 – Warum kann Main gleich bleiben?

Beantworte schriftlich in drei bis fünf Sätzen:

1. Warum kann `Main` weiterhin `ProduktSpeicher` als Typ verwenden?
2. Warum bleibt der Aufruf `speicher.speichern(...)` gleich?
3. Was entscheidet, ob eine CSV-Datei geschrieben oder auf die Konsole ausgegeben wird?

Hilfssatz:

```text
Main kennt den Vertrag. Die konkrete Klasse bestimmt das Verhalten.
```

---

### Aufgabe 10 – Signatur bewusst prüfen

Erzeuge kurz einen kleinen Fehler und korrigiere ihn danach wieder.

Mögliche Fehler:

- Methode in `KonsolenProduktSpeicher` in `ausgeben(...)` umbenennen
- Parameter `String dateipfad` entfernen
- Rückgabetyp von `void` auf `String` ändern

Auftrag:

1. Führe `mvn test` oder `mvn package` aus.
2. Lies die Fehlermeldung.
3. Notiere, was nicht mehr zum Interface passt.
4. Korrigiere den Fehler.
5. Führe die Prüfung erneut aus.

---

### Aufgabe 11 – Einfache Prüfung wiederholen

Führe nach dem Zurückwechseln auf `CsvProduktSpeicher` nochmals eine Prüfung aus.

Auftrag:

1. Starte `mvn test` oder `mvn package`.
2. Starte falls nötig das Programm.
3. Prüfe die Ausgabe oder die CSV-Datei.
4. Notiere das Resultat.

Beispielnotiz:

```text
mvn package erfolgreich. Main verwendet ProduktSpeicher. CsvProduktSpeicher schreibt weiterhin die CSV-Datei.
```

---

## Transfer

### Aufgabe 12 – BackupProduktSpeicher als Idee

Beschreibe eine mögliche Klasse `BackupProduktSpeicher`.

Beantworte:

1. Welches Interface müsste die Klasse implementieren?
2. Welche Methode müsste sie besitzen?
3. Was wäre ihr anderes Verhalten?
4. Warum wäre das später nützlich?

Du musst diese Klasse nicht programmieren.

---

### Aufgabe 13 – StatistikProduktSpeicher überlegen

Stell dir eine Klasse `StatistikProduktSpeicher` vor.

Mögliche Idee:

```text
Beim Speichern wird nur ausgegeben, wie viele Produkte vorhanden sind und wie hoch der Gesamtwert ist.
```

Beantworte:

1. Passt diese Idee noch zum Namen `ProduktSpeicher`?
2. Wäre das wirklich Speichern oder eher Auswerten?
3. Welche Verantwortung hätte diese Klasse?
4. Warum muss man bei neuen Implementierungen auf klare Rollen achten?

---

### Aufgabe 14 – JsonProduktSpeicher nur als Konzept

Diskutiere die Idee `JsonProduktSpeicher` nur als Konzept.

Beantworte:

1. Welche Methode müsste diese Klasse haben?
2. Was wäre anders als bei CSV?
3. Warum wird JSON in dieser Einheit noch nicht umgesetzt?
4. Warum reicht `KonsolenProduktSpeicher` für das aktuelle Lernziel?

Wichtig: Kein JSON-Code schreiben.

---

### Aufgabe 15 – Warum ist Austauschbarkeit später hilfreich?

Beantworte in eigenen Worten:

1. Warum kann es nützlich sein, wenn mehrere Klassen denselben Vertrag erfüllen?
2. Warum ist das für Tests hilfreich?
3. Warum ist das für spätere Services hilfreich?
4. Welche Gefahr entsteht, wenn zu viele Implementierungen zu früh eingeführt werden?

---

## Reflexion

Beantworte kurz:

1. Was bleibt gleich, wenn die Implementierung gewechselt wird?
2. Warum hilft das Interface dabei?
3. Was ist der Unterschied zwischen Vertrag und Umsetzung?
4. Warum ist `KonsolenProduktSpeicher` didaktisch einfacher als eine Datenbank?
5. Welche weiteren Implementierungen wären später denkbar?
