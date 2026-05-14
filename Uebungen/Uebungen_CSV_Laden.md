# Übungen – Produktdaten aus CSV-Dateien laden

## Vorwissen

Du brauchst:

- Klassen und Objekte
- Getter und Setter
- `ArrayList`
- Methoden mit Rückgabewerten
- einfache String-Verarbeitung
- `split(";")`
- `Double.parseDouble(...)`
- Maven-Projektstruktur
- einfache JUnit-Tests oder manuelle Prüfungen

Nicht verwendet werden:

- Datenbanken
- JSON
- Streams API
- generische Parser
- ORM
- Multi-Threading
- komplexe Exception-Strukturen

---

## Vorbereitung

Nutze die bekannte Produktverwaltung.

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
      model/Produkt.java
      service/ProduktVerwaltung.java
```

Lege die Datei `data/produkte.csv` an:

```text
Tastatur;79.90
Monitor;249.00
Maus;39.50
```

Prüfe regelmässig:

```bash
mvn test
```

Wenn noch keine passenden Tests vorhanden sind, prüfe mit kleinen Ausgaben in `main`.

---

## Basis

### Aufgabe 1 – CSV-Zeile verstehen

Gegeben ist:

```text
Tastatur;79.90
```

Beantworte schriftlich:

1. Welcher Teil ist der Produktname?
2. Welcher Teil ist der Preis?
3. Welches Zeichen trennt die beiden Werte?
4. Warum ist diese Zeile noch kein `Produkt`-Objekt?

---

### Aufgabe 2 – Eine Zeile splitten

Schreibe in `Main` einen kleinen Test mit dieser Zeile:

```java
String zeile = "Tastatur;79.90";
```

Auftrag:

1. Zerlege die Zeile mit `split(";")`.
2. Gib den Namen aus.
3. Gib den Preistext aus.
4. Prüfe, ob beide Werte korrekt angezeigt werden.

Erwartete Ausgabe:

```text
Tastatur
79.90
```

---

### Aufgabe 3 – Preis parsen

Erweitere Aufgabe 2.

Auftrag:

1. Wandle den Preistext mit `Double.parseDouble(...)` in einen `double` um.
2. Speichere das Resultat in einer Variable `preis`.
3. Gib `preis` aus.

Hinweis:

```java
double preis = Double.parseDouble(preisText);
```

---

### Aufgabe 4 – Produkt erzeugen

Erzeuge aus der CSV-Zeile ein `Produkt`-Objekt.

Auftrag:

1. Lies den Namen aus der ersten Spalte.
2. Parse den Preis aus der zweiten Spalte.
3. Erzeuge ein neues `Produkt`.
4. Gib Name und Preis über Getter aus.

Ziel:

```text
Aus Textdaten entsteht ein Objekt.
```

---

## Aufbau

### Aufgabe 5 – Methode für eine Zeile schreiben

Erstelle in `CsvProduktLeser` eine Methode:

```java
public Produkt parseProdukt(String zeile)
```

Vereinbarung:

```text
gültige Zeile -> Produkt
ungültige Zeile -> null
```

Auftrag:

1. Zerlege die Zeile mit `split(";")`.
2. Lies Name und Preis aus.
3. Erzeuge ein `Produkt`.
4. Gib das Produkt zurück.

Teste die Methode mit:

```text
Tastatur;79.90
```

---

### Aufgabe 6 – Mehrere Produkte laden

Erstelle in `CsvProduktLeser` eine Methode:

```java
public ArrayList<Produkt> ladeProdukte(String dateipfad)
```

Auftrag:

1. Lies alle Zeilen aus `data/produkte.csv`.
2. Erzeuge für jede gültige Zeile ein `Produkt`.
3. Füge jedes Produkt einer `ArrayList<Produkt>` hinzu.
4. Gib die Liste zurück.

Prüfe in `Main`:

```text
Anzahl Produkte: 3
```

---

### Aufgabe 7 – Produkte ausgeben

Lade die Produkte aus der Datei.

Auftrag:

1. Durchlaufe die `ArrayList<Produkt>` mit einer Schleife.
2. Gib pro Produkt Name und Preis aus.
3. Achte darauf, dass die Ausgabe nicht direkt im `CsvProduktLeser` passiert.

Erwartung:

```text
Tastatur: 79.9
Monitor: 249.0
Maus: 39.5
```

---

### Aufgabe 8 – Fachlogik wiederverwenden

Nutze die geladene Liste mit deiner `ProduktVerwaltung`.

Auftrag:

1. Zähle die geladenen Produkte.
2. Berechne den Gesamtwert aller Produkte.
3. Gib beide Resultate aus.

Erwartung:

```text
Anzahl Produkte: 3
Gesamtwert: 368.4
```

---

## Vertiefung

### Aufgabe 9 – Leere Zeilen ignorieren

Erweitere `data/produkte.csv`:

```text
Tastatur;79.90

Monitor;249.00
Maus;39.50
```

Auftrag:

1. Prüfe jede Zeile mit `trim()`.
2. Überspringe leere Zeilen.
3. Stelle sicher, dass weiterhin drei Produkte geladen werden.

---

### Aufgabe 10 – Fehlende Spalten erkennen

Ergänze eine fehlerhafte Zeile:

```text
Kabel
Kabel;9.90;Aktion
```

Auftrag:

1. Prüfe nach `split(";")`, ob genau zwei Spalten vorhanden sind.
2. Gib bei falscher Spaltenzahl eine einfache Fehlermeldung aus.
3. Überspringe die fehlerhafte Zeile.

Beispielmeldung:

```text
Fehlerhafte Zeile übersprungen: Kabel
```

---

### Aufgabe 11 – Ungültigen Preis erkennen

Ergänze eine fehlerhafte Zeile:

```text
Monitor;abc
```

Auftrag:

1. Fange den Fehler beim Parsen des Preises ab.
2. Gib eine einfache Fehlermeldung aus.
3. Lade die übrigen gültigen Produkte weiter.

Hinweis:

```java
catch (NumberFormatException e)
```

Beispielmeldung:

```text
Ungültiger Preis in Zeile: Monitor;abc
```

---

### Aufgabe 12 – Datei nicht gefunden behandeln

Teste einen falschen Dateipfad:

```text
data/fehlt.csv
```

Auftrag:

1. Starte den Ladevorgang mit diesem Pfad.
2. Gib eine einfache Fehlermeldung aus.
3. Das Programm soll nicht unkontrolliert abbrechen.

Beispielmeldung:

```text
Datei nicht gefunden: data/fehlt.csv
```

---

### Aufgabe 13 – Verantwortung prüfen

Prüfe deinen Code.

Beantworte schriftlich:

1. Welche Klasse liest die Datei?
2. Welche Klasse berechnet den Gesamtwert?
3. Welche Klasse startet den Ablauf?
4. Welche Logik steht noch in `main`, die besser in eine Methode gehört?

---

## Transfer optional

Bearbeite eine oder mehrere Aufgaben, wenn der Pflichtteil funktioniert.

### Aufgabe 14 – Leerzeichen bereinigen

Die Datei enthält:

```text
 Tastatur ; 79.90
```

Auftrag:

1. Bereinige Name und Preistext mit `trim()`.
2. Prüfe, ob trotzdem ein korrektes Produkt entsteht.

---

### Aufgabe 15 – Kommentare ignorieren

Die Datei enthält Kommentarzeilen:

```text
# Standardprodukte
Tastatur;79.90
```

Auftrag:

1. Ignoriere Zeilen, die mit `#` beginnen.
2. Lade nur echte Produktzeilen.

---

### Aufgabe 16 – Fehlerhafte Zeilen zählen

Auftrag:

1. Zähle, wie viele Zeilen übersprungen wurden.
2. Gib die Anzahl am Ende aus.

Beispiel:

```text
Übersprungene Zeilen: 2
```

---

### Aufgabe 17 – Zusätzliches Attribut

Erweitere das CSV-Format optional:

```text
Tastatur;79.90;12
```

Auftrag:

1. Entscheide, welches zusätzliche Attribut sinnvoll ist.
2. Passe `Produkt` und den CSV-Leser an.
3. Prüfe, ob bestehende Aufgaben weiterhin verständlich bleiben.

---

## Fehleranalyse

Prüfe diese typischen Fehler bewusst:

| Fehler | Mögliche Folge |
|---|---|
| `split(",")` statt `split(";")` | Die Zeile wird nicht korrekt zerlegt |
| `Double.parseDouble(...)` fehlt | Der Preis bleibt Text |
| `ArrayList` nicht initialisiert | Beim Hinzufügen entsteht ein Fehler |
| keine Prüfung auf leere Zeilen | Leere Zeilen führen zu fehlerhaften Produkten |
| falscher Dateipfad | Datei wird nicht gefunden |
| alles steht in `main` | Code wird schwer testbar |

---

## Reflexion

Beantworte kurz:

1. Warum ist CSV für einfache Produktdaten praktisch?
2. Warum ist Persistenz wichtig?
3. Warum sollten Datei- und Fachlogik getrennt werden?
4. Welche Fehler können bei Dateien auftreten?
5. Welche dieser Fehler können mit Tests gut geprüft werden?
