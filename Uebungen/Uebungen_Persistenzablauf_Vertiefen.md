# Übungen – Persistenzablauf vertiefen

## Vorwissen

Du brauchst:

- Klassen und Objekte
- Getter und Setter
- `ArrayList`
- Methoden mit Rückgabewerten
- CSV-Laden mit `split(";")`
- `Double.parseDouble(...)`
- CSV-Speichern mit `Files.write(...)`
- Maven-Projektstruktur
- einfache JUnit-Tests oder manuelle Prüfungen

Nicht verwendet werden:

- Datenbanken
- JSON
- Streams API
- generische CSV-Frameworks
- ORM
- GUI
- Spring
- komplexe Exception-Strukturen
- formales Repository-Pattern

---

## Vorbereitung

Nutze die bekannte Produktverwaltung mit CSV-Leser und CSV-Speicher.

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
```

Lege `data/produkte.csv` an:

```text
name;preis
Tastatur;79.90
Monitor;249.00
Maus;39.50
```

Prüfe regelmässig:

```bash
mvn test
```

Wenn noch keine passenden Tests vorhanden sind, prüfe mit kleinen Ausgaben in `Main`.

---

## Basis

### Aufgabe 1 – Ablauf einordnen

Schreibe den Persistenzablauf in eigenen Worten auf:

```text
produkte.csv
-> laden
-> ArrayList<Produkt>
-> bearbeiten
-> speichern
-> erneut laden
-> prüfen
```

Beantworte:

1. Wo liegen die Daten vor dem Laden?
2. Wo liegen die Daten nach dem Laden?
3. Wann wird eine Änderung dauerhaft?

---

### Aufgabe 2 – Produkte laden

Nutze deinen `CsvProduktLeser`.

Auftrag:

1. Lade `data/produkte.csv`.
2. Überspringe die Kopfzeile `name;preis`.
3. Speichere die Produkte in einer `ArrayList<Produkt>`.
4. Gib die Anzahl geladener Produkte aus.

Erwartung:

```text
Geladene Produkte: 3
```

---

### Aufgabe 3 – Produkte ausgeben

Gib alle geladenen Produkte aus.

Auftrag:

1. Durchlaufe die `ArrayList<Produkt>`.
2. Gib pro Produkt Name und Preis aus.
3. Schreibe die Ausgabe nicht in den `CsvProduktLeser`.

Beispiel:

```text
Tastatur: 79.9
Monitor: 249.0
Maus: 39.5
```

---

### Aufgabe 4 – Neues Produkt hinzufügen

Füge nach dem Laden ein neues Produkt hinzu:

```text
Webcam;89.90
```

Auftrag:

1. Erzeuge ein neues `Produkt`.
2. Füge es zur Produktverwaltung oder zur Produktliste hinzu.
3. Gib die neue Anzahl Produkte aus.

Erwartung:

```text
Anzahl nach Hinzufügen: 4
```

---

### Aufgabe 5 – Preis ändern

Ergänze in `ProduktVerwaltung` eine Methode:

```java
public boolean aenderePreis(String name, double neuerPreis)
```

Auftrag:

1. Suche das Produkt mit dem übergebenen Namen.
2. Ändere den Preis, wenn das Produkt gefunden wurde.
3. Gib `true` zurück, wenn eine Änderung passiert ist.
4. Gib `false` zurück, wenn kein passendes Produkt existiert.

Teste mit:

```text
Maus -> 34.90
```

---

### Aufgabe 6 – Produkte speichern

Nutze deinen `CsvProduktSpeicher`.

Auftrag:

1. Speichere die geänderte Produktliste nach `data/produkte.csv`.
2. Verwende weiterhin `;` als Trennzeichen.
3. Achte darauf, dass `name` vor `preis` steht.
4. Öffne die Datei im Editor und prüfe den Inhalt.

---

### Aufgabe 7 – Datei erneut laden

Lade `data/produkte.csv` nach dem Speichern erneut.

Auftrag:

1. Erzeuge eine neue `ArrayList<Produkt>` durch erneutes Laden.
2. Prüfe, ob `Webcam` vorhanden ist.
3. Prüfe, ob `Maus` den neuen Preis hat.
4. Gib die Anzahl erneut geladener Produkte aus.

Erwartung:

```text
Erneut geladene Produkte: 4
```

---

### Aufgabe 8 – Änderungen nachweisen

Beantworte schriftlich:

1. Welche Änderung wäre verloren gegangen, wenn du nicht gespeichert hättest?
2. Warum reicht es nicht, nur die ursprüngliche `ArrayList` anzuschauen?
3. Welche Datei enthält jetzt den neuen Zustand?

---

## Vertiefung

### Aufgabe 9 – Gesamtwert vergleichen

Berechne den Gesamtwert vor und nach der Änderung.

Auftrag:

1. Berechne den Gesamtwert direkt nach dem Laden.
2. Füge `Webcam` hinzu und ändere den Preis von `Maus`.
3. Speichere und lade erneut.
4. Berechne den Gesamtwert der erneut geladenen Liste.
5. Gib die Veränderung aus.

Beispielausgabe:

```text
Gesamtwert vorher: 368.4
Gesamtwert nachher: 453.7
Veränderung: 85.3
```

---

### Aufgabe 10 – Ungültige CSV-Zeilen zählen

Erweitere `data/produkte.csv` testweise:

```text
name;preis
Tastatur;79.90
Kabel
Monitor;abc
Maus;39.50
```

Auftrag:

1. Überspringe ungültige Zeilen.
2. Zähle jede übersprungene Zeile.
3. Gib die Anzahl am Ende aus.

Beispiel:

```text
Fehlerhafte CSV-Zeilen: 2
```

---

### Aufgabe 11 – Leere Produktliste speichern und laden

Erstelle eine leere `ArrayList<Produkt>`.

Auftrag:

1. Speichere die leere Liste in eine Testdatei, zum Beispiel `data/leere-produkte.csv`.
2. Lade diese Datei erneut.
3. Prüfe, ob null Produkte geladen werden.
4. Gib eine ruhige Meldung aus.

Wenn dein Speicher bereits eine Kopfzeile schreibt, enthält die Datei nur die Kopfzeile `name;preis`. Das ist weiterhin eine leere Produktliste.

Beispiel:

```text
Leere Produktliste geladen: 0 Produkte
```

---

### Aufgabe 12 – Nicht vorhandenes Produkt behandeln

Teste die Methode `aenderePreis(...)` mit einem Namen, der nicht existiert:

```text
Drucker
```

Auftrag:

1. Ändere keinen Preis, wenn kein Produkt gefunden wurde.
2. Gib `false` zurück.
3. Gib in `Main` eine verständliche Meldung aus.

Beispiel:

```text
Produkt nicht gefunden: Drucker
```

---

### Aufgabe 13 – Speicher- und Ladeformat vergleichen

Prüfe dein Format bewusst.

Auftrag:

1. Notiere, welche Zeile der Speicher für ein Produkt erzeugt.
2. Notiere, was der Leser beim Laden erwartet.
3. Vergleiche Trennzeichen, Spaltenreihenfolge und Kopfzeile.
4. Korrigiere Unterschiede.

Check:

```text
Kopfzeile: name;preis
Produktzeile: Tastatur;79.9
Trennzeichen: ;
Preis lesbar mit Double.parseDouble(...): ja
```

---

### Aufgabe 14 – Verantwortung prüfen

Prüfe deinen Code.

Beantworte:

1. Welche Klasse liest Dateien?
2. Welche Klasse schreibt Dateien?
3. Welche Klasse ändert Preise?
4. Welche Klasse berechnet den Gesamtwert?
5. Welche Logik steht noch in `Main`, die besser in eine andere Klasse gehört?

---

## Transfer

Diese Aufgaben gehören fest zur Einheit. Sie sind anspruchsvoller als Basis und Vertiefung.

### Transfer 1 – Backup vor dem Überschreiben

Erweitere den Speicherablauf.

Auftrag:

1. Prüfe vor dem Speichern, ob `data/produkte.csv` bereits existiert.
2. Kopiere die bestehende Datei nach `data/produkte-backup.csv`.
3. Speichere erst danach die neue Produktliste.
4. Prüfe beide Dateien im Editor.

Ziel:

```text
Backup-Datei enthält den alten Zustand.
Hauptdatei enthält den neuen Zustand.
```

Hinweis:

```java
Files.copy(Path.of("data/produkte.csv"), Path.of("data/produkte-backup.csv"), StandardCopyOption.REPLACE_EXISTING);
```

Benötigte Imports:

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardCopyOption;
```

---

### Transfer 2 – Exportdatei mit anderem Namen

Ergänze eine Exportfunktion.

Auftrag:

1. Speichere die Produktliste zusätzlich nach `data/produkte-export.csv`.
2. Die Hauptdatei `data/produkte.csv` soll dabei nicht verändert werden.
3. Lade die Exportdatei erneut und prüfe die Anzahl Produkte.

---

### Transfer 3 – Kopfzeile `name;preis` ergänzen

Passe Leser und Speicher an.

Auftrag:

1. Der Speicher schreibt als erste Zeile:

```text
name;preis
```

2. Der Leser überspringt diese Kopfzeile.
3. Normale Produktzeilen werden weiterhin geladen.
4. Prüfe, ob nach dem erneuten Laden kein falsches Produkt `name` entsteht.

---

### Transfer 4 – Einfache Änderungsstatistik

Gib am Ende des Ablaufs eine Statistik aus.

Sie soll enthalten:

- Anzahl geladene Produkte
- Anzahl geänderte Produkte
- Anzahl gespeicherte Produkte
- Anzahl fehlerhafte CSV-Zeilen

Beispiel:

```text
Geladene Produkte: 3
Geänderte Produkte: 1
Gespeicherte Produkte: 4
Fehlerhafte CSV-Zeilen: 2
```

---

## Typische Fehler prüfen

Prüfe deine Lösung bewusst auf diese Punkte:

- Wird nach einer Änderung wirklich gespeichert?
- Wird nach dem Speichern erneut geladen?
- Passen Speicher- und Ladeformat zusammen?
- Bleibt der Preis ein `double` und nicht nur Text?
- Wird die richtige Liste gespeichert?
- Werden fehlerhafte CSV-Zeilen gezählt?
- Wird eine leere Produktliste ruhig behandelt?
- Existiert der Zielordner `data`?
- Bleiben Datei- und Fachlogik getrennt?
- Ist `Main` nur Ablaufsteuerung und nicht Sammelort für alle Logik?

---

## Reflexion

Beantworte kurz:

1. Warum reicht Laden alleine nicht?
2. Warum müssen Änderungen bewusst gespeichert werden?
3. Warum ist ein Backup vor dem Überschreiben sinnvoll?
4. Warum sollten Datei- und Fachlogik getrennt bleiben?
5. Was bedeutet Zustand einer Anwendung?
