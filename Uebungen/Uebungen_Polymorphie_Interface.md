# Übungen – Unterschiedliche Objekte über dasselbe Interface verwenden

## Vorwissen

Du brauchst:

- Klassen und Objekte
- `ArrayList`
- Methoden mit Parametern
- Maven-Projektstruktur
- `ProduktSpeicher` als Interface
- `CsvProduktSpeicher implements ProduktSpeicher`
- `KonsolenProduktSpeicher implements ProduktSpeicher`
- `Main` arbeitet mit dem Interface-Typ

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

Ziel dieser Übung:

```text
Eine Variable vom Interface-Typ enthält nacheinander unterschiedliche konkrete Objekte.
Der Methodenaufruf bleibt gleich.
Das beobachtete Verhalten ist unterschiedlich.
```

Prüfe nach praktischen Änderungen:

```bash
mvn test
```

Wenn keine Tests vorhanden sind:

```bash
mvn package
```

---

## Basis

### Aufgabe 1 – Interface-Typ als Variable verwenden

Öffne `Main`.

Lege eine Variable vom Interface-Typ an:

```java
ProduktSpeicher speicher;
```

Auftrag:

1. Notiere den Typ der Variable.
2. Notiere, warum der Typ nicht `CsvProduktSpeicher` sein soll.
3. Notiere, welche Methode über diese Variable aufgerufen werden darf.

Hilfssatz:

```text
Die Variable hat den Typ ProduktSpeicher, weil Main nur den gemeinsamen Vertrag kennen soll.
```

---

### Aufgabe 2 – Zuerst CsvProduktSpeicher verwenden

Weise der Variable zuerst ein CSV-Objekt zu:

```java
speicher = new CsvProduktSpeicher();
```

Rufe danach die Methode auf:

```java
speicher.speichern(produkte, "data/produkte.csv");
```

Auftrag:

1. Führe das Programm aus oder starte die vorhandenen Prüfungen.
2. Beobachte, ob eine CSV-Datei geschrieben wird.
3. Notiere den Methodenaufruf.
4. Notiere das sichtbare Verhalten.

---

### Aufgabe 3 – Danach KonsolenProduktSpeicher verwenden

Weise derselben Variable ein anderes passendes Objekt zu:

```java
speicher = new KonsolenProduktSpeicher();
```

Rufe wieder dieselbe Methode auf:

```java
speicher.speichern(produkte, "data/produkte.csv");
```

Auftrag:

1. Ändere nicht den Variablentyp.
2. Ändere nicht den Methodennamen.
3. Beobachte die Konsolenausgabe.
4. Notiere, was anders ist als beim CSV-Speicher.

Hinweis: `dateipfad` wird im `KonsolenProduktSpeicher` bewusst nicht genutzt. Der Parameter bleibt vorhanden, weil die Methode zum Interface passen muss.

---

### Aufgabe 4 – Verhalten vergleichen

Fülle die Tabelle aus:

| Schritt | Inhalt der Variable `speicher` | Methodenaufruf | Beobachtung |
|---|---|---|---|
| 1 | `new CsvProduktSpeicher()` | `speicher.speichern(...)` | |
| 2 | `new KonsolenProduktSpeicher()` | `speicher.speichern(...)` | |

Beantworte danach:

1. Welche Codezeile ist gleich geblieben?
2. Welche Codezeile hat die konkrete Klasse gewechselt?
3. Welche Klasse entscheidet über das Verhalten?

---

### Aufgabe 5 – Main fast unverändert lassen

Prüfe deine `Main`-Klasse.

Auftrag:

1. Lasse die Produktliste gleich.
2. Lasse den Aufruf `speicher.speichern(...)` gleich.
3. Wechsle nur das konkrete Objekt hinter `new`.
4. Erkläre in zwei Sätzen, warum `Main` nicht stark angepasst werden muss.

---

## Vertiefung

### Aufgabe 6 – Beide Implementierungen nacheinander verwenden

Ergänze in `Main` bewusst beide Aufrufe nacheinander:

```java
ProduktSpeicher speicher = new CsvProduktSpeicher();
speicher.speichern(produkte, "data/produkte.csv");

speicher = new KonsolenProduktSpeicher();
speicher.speichern(produkte, "data/produkte.csv");
```

Auftrag:

1. Führe das Programm aus.
2. Prüfe die CSV-Datei.
3. Prüfe die Konsolenausgabe.
4. Markiere beide gleichen Methodenaufrufe.
5. Schreibe auf, warum trotzdem unterschiedliche Dinge passieren.

---

### Aufgabe 7 – Ablauf dokumentieren

Dokumentiere den Ablauf in eigenen Worten:

| Zeitpunkt | Variable `speicher` enthält | Java ruft Code aus dieser Klasse auf |
|---|---|---|
| erster Aufruf | | |
| zweiter Aufruf | | |

Verwende die Begriffe:

- Interface-Typ
- konkretes Objekt
- gleicher Methodenaufruf
- unterschiedliches Verhalten

---

### Aufgabe 8 – Verantwortlichkeitstabelle ergänzen

Fülle die Tabelle aus:

| Teil | Verantwortung |
|---|---|
| `ProduktSpeicher` | |
| `CsvProduktSpeicher` | |
| `KonsolenProduktSpeicher` | |
| `Main` | |

Zusatzfrage:

```text
Warum wäre es ungünstig, wenn Main selbst CSV-Dateien schreiben und Konsolenausgaben formatieren würde?
```

---

### Aufgabe 9 – Gleiches Interface, unterschiedliche Wirkung erklären

Erkläre in drei bis fünf Sätzen:

1. Warum darf die Variable `speicher` beide konkreten Objekte aufnehmen?
2. Warum bleibt `speicher.speichern(...)` gleich?
3. Warum ist das Ergebnis trotzdem unterschiedlich?

Verwende diesen Satzanfang:

```text
Die Variable hat den Interface-Typ ProduktSpeicher. Deshalb ...
```

---

## Transfer

### Aufgabe 10 – Doppeltes Speichern als Idee

Stelle dir vor, Produkte sollen gleichzeitig gespeichert und auf der Konsole ausgegeben werden.

Beschreibe eine einfache Idee:

1. Zuerst `CsvProduktSpeicher` verwenden.
2. Danach `KonsolenProduktSpeicher` verwenden.
3. Beide Male denselben Methodenaufruf nutzen.

Notiere:

```text
Welche Zeilen in Main wären nötig?
Welche Zeilen bleiben gleich?
```

Wichtig: Erstelle dafür noch keine neue komplexe Architektur.

---

### Aufgabe 11 – LoggingProduktSpeicher skizzieren

Skizziere nur als Idee eine weitere Implementierung:

```text
LoggingProduktSpeicher
```

Auftrag:

1. Welche Methode müsste diese Klasse haben?
2. Was könnte diese Klasse ausgeben?
3. Warum müsste sie `ProduktSpeicher` implementieren?
4. Warum soll diese Klasse noch nicht zusätzlich umgesetzt werden?

---

### Aufgabe 12 – BackupProduktSpeicher skizzieren

Skizziere nur als Idee:

```text
BackupProduktSpeicher
```

Auftrag:

1. Welchen Vertrag müsste die Klasse erfüllen?
2. Was wäre ihr besonderes Verhalten?
3. Warum könnte `Main` weiterhin mit `ProduktSpeicher` arbeiten?

---

### Aufgabe 13 – Warum erleichtert Polymorphie spätere Erweiterungen?

Beantworte schriftlich:

1. Was müsste gleich bleiben, damit eine neue Speicherklasse austauschbar ist?
2. Was dürfte sich in der neuen Klasse unterscheiden?
3. Warum ist das für spätere Erweiterungen hilfreich?

---

## Typische Fehler prüfen

Prüfe deinen Code bewusst auf diese Fehler:

| Prüfung | Erfüllt? |
|---|---|
| `ProduktSpeicher` wird nicht mit `new ProduktSpeicher()` erzeugt | |
| Die Variable in `Main` hat den Typ `ProduktSpeicher` | |
| `CsvProduktSpeicher` und `KonsolenProduktSpeicher` implementieren das Interface | |
| Der Methodenaufruf `speicher.speichern(...)` bleibt gleich | |
| Es wird kein `instanceof` verwendet | |
| Es wird kein Downcasting verwendet | |
| `Main` enthält keine unnötige Fallunterscheidung für Speicherarten | |

---

## Reflexion

Beantworte zum Schluss:

1. Was bleibt gleich, wenn die konkrete Klasse gewechselt wird?
2. Was verändert sich?
3. Warum hilft ein Interface bei austauschbaren Implementierungen?
4. Warum sprechen wir hier von unterschiedlichem Verhalten?
5. Welche weiteren Implementierungen wären später denkbar?
