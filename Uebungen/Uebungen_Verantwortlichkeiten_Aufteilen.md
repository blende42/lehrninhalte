# Übungen – Code strukturieren und Verantwortlichkeiten aufteilen

## Vorwissen

Du brauchst:

- Klassen und Objekte
- Getter und Setter
- `ArrayList`
- Methoden mit Rückgabewerten
- CSV-Laden und CSV-Speichern
- Maven-Projektstruktur
- einfache Tests mit `mvn test`
- Grundlagen aus Refactoring mit Tests

Nicht verwendet werden:

- Datenbanken
- ORM
- Spring
- Clean Architecture
- formales Repository-Pattern
- REST-APIs
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
      model/Produkt.java
      service/ProduktVerwaltung.java
  src/test/java/
    ch/allianz/youngoitv/produktverwaltung/service/
      ProduktVerwaltungTest.java
```

Beispieldatei:

```text
name;preis
Tastatur;79.90
Monitor;249.00
Maus;39.50
```

Prüfe nach Refactoring-Schritten:

```bash
mvn test
```

Wenn du noch keine Tests hast, nutze kleine manuelle Prüfungen in `Main` und ergänze danach einfache Tests für `ProduktVerwaltung`.

---

## Basis

### Aufgabe 1 – Verantwortlichkeiten zuordnen

Ordne jede Aufgabe einer Klasse zu.

| Aufgabe | Klasse |
|---|---|
| Produktname und Preis speichern | |
| Produkt nach Name suchen | |
| Gesamtwert berechnen | |
| CSV-Datei lesen | |
| CSV-Datei schreiben | |
| Programm starten | |
| Ablauf laden, bearbeiten, speichern auslösen | |

Verwende diese Klassen:

- `Produkt`
- `ProduktVerwaltung`
- `CsvProduktLeser`
- `CsvProduktSpeicher`
- `Main`

---

### Aufgabe 2 – Code in Main markieren

Nimm deine aktuelle `Main.java`.

Auftrag:

1. Markiere Zeilen, die Fachlogik enthalten.
2. Markiere Zeilen, die Dateilogik enthalten.
3. Markiere Zeilen, die nur Ablaufsteuerung sind.
4. Schreibe drei kurze Beispiele auf.

Beispiel:

```text
Fachlogik: Produkt suchen und Preis ändern
Dateilogik: Files.readAllLines(...)
Ablauf: zuerst laden, danach speichern
```

---

### Aufgabe 3 – Methoden aus Main verschieben

Suche in `Main` Code, der Produkte fachlich verarbeitet.

Beispiel für Code, der nicht in `Main` bleiben soll:

```java
for (Produkt produkt : produkte) {
    if (produkt.getName().equals("Maus")) {
        produkt.setPreis(34.90);
    }
}
```

Auftrag:

1. Verschiebe Produktsuche in `ProduktVerwaltung`.
2. Verschiebe Preisänderung in `ProduktVerwaltung`.
3. Verschiebe Gesamtwertberechnung in `ProduktVerwaltung`.
4. Lasse `Main` nur die Methoden aufrufen.

Erwartete Methoden:

```java
public Produkt findeProdukt(String name)
public boolean aenderePreis(String name, double neuerPreis)
public double berechneGesamtwert()
```

---

### Aufgabe 4 – CSV-Laden aus Main entfernen

Wenn `Main` CSV-Zeilen selbst liest oder zerlegt, verschiebe diese Logik.

Auftrag:

1. Erstelle oder verwende `CsvProduktLeser`.
2. Die Methode lädt Produkte aus einem Dateipfad.
3. `Main` ruft nur noch diese Methode auf.
4. `Main` enthält kein `Files.readAllLines(...)` und kein `split(";")` mehr.

Erwartung:

```java
CsvProduktLeser leser = new CsvProduktLeser();
ArrayList<Produkt> produkte = leser.ladeProdukte("data/produkte.csv");
```

---

### Aufgabe 5 – CSV-Speichern aus Main entfernen

Wenn `Main` CSV-Zeilen selbst erzeugt oder mit `Files.write(...)` schreibt, verschiebe diese Logik.

Auftrag:

1. Erstelle oder verwende `CsvProduktSpeicher`.
2. Die Methode speichert eine `ArrayList<Produkt>`.
3. `Main` ruft nur noch diese Methode auf.
4. `Main` enthält kein direktes Erzeugen von CSV-Zeilen und kein `Files.write(...)` mehr.

Erwartung:

```java
CsvProduktSpeicher speicher = new CsvProduktSpeicher();
speicher.speichereProdukte(verwaltung.getProdukte(), "data/produkte.csv");
```

---

### Aufgabe 6 – Main kurz lesen können

Formuliere deine `Main` so, dass der Ablauf schnell erkennbar ist.

Check:

```text
1. Produkte laden
2. ProduktVerwaltung erstellen
3. Produkte bearbeiten
4. Produkte speichern
5. Ergebnis ausgeben oder prüfen
```

In `Main` sollen keine Schleifen über CSV-Zeilen mehr stehen.

---

## Vertiefung

### Aufgabe 7 – Überladene Main schrittweise refaktorieren

Refaktoriere nicht alles auf einmal.

Auftrag:

1. Starte mit funktionierendem Code.
2. Verschiebe zuerst nur die Produktsuche.
3. Führe `mvn test` aus.
4. Verschiebe danach die Preisänderung.
5. Führe wieder `mvn test` aus.
6. Verschiebe danach CSV-Laden und anschliessend CSV-Speichern in kleinen Schritten.
7. Prüfe erneut.

Notiere nach jedem Schritt:

```text
Was wurde verschoben?
In welche Klasse?
Welche Prüfung wurde ausgeführt?
```

---

### Aufgabe 8 – Doppelte Logik entfernen

Suche nach doppelter Logik.

Beispiele:

- Produkt wird an mehreren Stellen mit derselben Schleife gesucht
- CSV-Zeile wird an mehreren Stellen gleich aufgebaut
- Gesamtwert wird an mehreren Stellen berechnet

Auftrag:

1. Markiere eine doppelte Stelle.
2. Entscheide, welche Klasse dafür zuständig ist.
3. Ersetze die doppelte Logik durch einen Methodenaufruf.

---

### Aufgabe 9 – Sprechende Methodennamen wählen

Prüfe deine Methodennamen.

Schlechte Namen:

```text
mach()
daten()
produkt()
start()
```

Bessere Namen:

```text
ladeProdukte(...)
speichereProdukte(...)
findeProdukt(...)
aenderePreis(...)
berechneGesamtwert()
```

Auftrag:

1. Suche zwei unklare Methodennamen.
2. Benenne sie verständlicher.
3. Führe danach `mvn test` aus.

---

### Aufgabe 10 – Tests nach dem Refactoring

Prüfe mindestens die Fachlogik.

Beispieltests:

```text
aenderePreis gibt true zurück, wenn Produkt existiert
aenderePreis gibt false zurück, wenn Produkt fehlt
berechneGesamtwert liefert die Summe aller Preise
findeProdukt gibt null zurück, wenn nichts gefunden wurde
```

Auftrag:

1. Schreibe oder ergänze einfache Tests für `ProduktVerwaltung`.
2. Verwende keine echte CSV-Datei für diese Tests.
3. Führe `mvn test` aus.

---

### Aufgabe 11 – Verantwortlichkeiten dokumentieren

Fülle diese Tabelle für deinen aktuellen Code aus.

| Klasse | Verantwortung | Darf nicht machen |
|---|---|---|
| `Produkt` | | |
| `ProduktVerwaltung` | | |
| `CsvProduktLeser` | | |
| `CsvProduktSpeicher` | | |
| `Main` | | |

Beispiel:

```text
ProduktVerwaltung
Verantwortung: Produkte suchen, ändern, berechnen
Darf nicht machen: CSV-Dateien lesen oder schreiben
```

---

## Transfer

Diese Aufgaben sind anspruchsvoller. Bearbeite sie erst, wenn Basis und Vertiefung stabil funktionieren.

### Transfer 1 – Einfachen Statistik-Service entwerfen

Überlege, ob eine neue Klasse sinnvoll ist.

Gewünschte Statistik:

- Anzahl Produkte
- Gesamtwert
- Durchschnittspreis
- teuerstes Produkt

Auftrag:

1. Entscheide, ob das in `ProduktVerwaltung` bleiben soll oder eine neue Klasse verdient.
2. Begründe deine Entscheidung in drei Sätzen.
3. Skizziere mögliche Methodennamen.

Mögliche Klasse:

```text
ProduktStatistik
```

Wichtig: Erstelle die Klasse nur, wenn die Verantwortung klar ist.

---

### Transfer 2 – Export-Service als Idee skizzieren

Ein Export soll später vielleicht anders funktionieren als normales Speichern.

Auftrag:

1. Skizziere eine mögliche Klasse `ProduktExport`.
2. Notiere, welche Aufgabe diese Klasse hätte.
3. Notiere, was weiterhin bei `CsvProduktSpeicher` bleiben würde.

Beispiel:

```text
ProduktExport: entscheidet, welche Produkte exportiert werden
CsvProduktSpeicher: schreibt die CSV-Datei
```

---

### Transfer 3 – Backup-Funktion zuordnen

Beim Speichern kann vor dem Überschreiben eine Backup-Datei erzeugt werden.

Auftrag:

1. Entscheide, ob die Backup-Funktion in `Main`, `CsvProduktSpeicher` oder eine neue Klasse gehört.
2. Begründe deine Entscheidung.
3. Prüfe, ob die Klasse dadurch zu viele Aufgaben bekommt.

---

### Transfer 4 – Neue Klasse oder Methode?

Bewerte diese Erweiterungen.

| Erweiterung | Neue Klasse? | Begründung |
|---|---|---|
| Preis eines Produkts ändern | | |
| Produkte als CSV speichern | | |
| teuerstes Produkt berechnen | | |
| Backup-Datei erzeugen | | |
| Programm starten | | |

Nutze als Regel:

```text
Eine neue Klasse lohnt sich, wenn eine klare eigene Verantwortung entsteht.
```

---

## Typische Fehler prüfen

Prüfe deinen Code bewusst:

- Bleibt alles in `Main`?
- Werden Datei- und Fachlogik vermischt?
- Wurden Klassen nur umbenannt, aber nicht entlastet?
- Sind Methodennamen verständlich?
- Wurde nach jedem Refactoring `mvn test` ausgeführt?
- Haben neue Klassen eine klare Verantwortung?
- Gibt es zu viele kleine Klassen ohne Nutzen?
- Kann `ProduktVerwaltung` ohne CSV-Datei getestet werden?

---

## Reflexion

Beantworte kurz:

1. Woran erkennst du, dass eine Klasse zu viel macht?
2. Warum ist `Main` als Orchestrator sinnvoll?
3. Warum wird Code durch getrennte Verantwortlichkeiten besser testbar?
4. Welche Struktur hilft später bei REST oder Spring?
