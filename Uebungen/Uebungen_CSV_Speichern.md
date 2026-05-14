# Übungen – Produktdaten als CSV-Dateien speichern

## Vorwissen

Du brauchst:

- Klassen und Objekte
- Getter und Setter
- `ArrayList`
- Methoden
- einfache String-Verarbeitung
- CSV-Laden mit `split(";")`
- `Double.parseDouble(...)`
- einfache Dateioperationen
- Maven-Projektstruktur
- einfache JUnit-Tests oder manuelle Prüfungen

Nicht verwendet werden:

- Datenbanken
- JSON
- Streams API
- generische CSV-Frameworks
- ORM
- Serialisierung
- Multi-Threading
- komplexe Exception-Strukturen

---

## Vorbereitung

Nutze die bekannte Produktverwaltung und den bestehenden CSV-Leser.

Ergänze neu eine Klasse `CsvProduktSpeicher`.

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

Prüfe regelmässig:

```bash
mvn test
```

Wenn noch keine passenden Tests vorhanden sind, prüfe mit kleinen Ausgaben in `main`.

---

## Basis

### Aufgabe 1 – Produkt als CSV-Zeile darstellen

Gegeben ist:

```java
Produkt produkt = new Produkt("Tastatur", 79.90);
```

Auftrag:

1. Erzeuge daraus einen `String` im CSV-Format.
2. Verwende `;` als Trennzeichen.
3. Gib die Zeile aus.

Erwartete Ausgabe:

```text
Tastatur;79.9
```

---

### Aufgabe 2 – Methode für eine CSV-Zeile schreiben

Erstelle in `CsvProduktSpeicher` eine Methode:

```java
public String produktAlsCsvZeile(Produkt produkt)
```

Auftrag:

1. Lies Name und Preis über Getter.
2. Verbinde beide Werte mit `;`.
3. Gib die fertige CSV-Zeile zurück.
4. Prüfe die Methode mit einem Produkt.

---

### Aufgabe 3 – Mehrere Produkte in Zeilen umwandeln

Erstelle in `Main` eine `ArrayList<Produkt>` mit drei Produkten:

```text
Tastatur;79.90
Monitor;249.00
Maus;39.50
```

Auftrag:

1. Durchlaufe die Liste mit einer Schleife.
2. Wandle jedes Produkt in eine CSV-Zeile um.
3. Speichere die Zeilen in einer `ArrayList<String>`.
4. Gib alle Zeilen aus.

---

## Aufbau

### Aufgabe 4 – Produkte in Datei speichern

Erstelle in `CsvProduktSpeicher` eine Methode:

```java
public void speichereProdukte(ArrayList<Produkt> produkte, String dateipfad)
```

Auftrag:

1. Erzeuge eine neue `ArrayList<String>` für die CSV-Zeilen.
2. Wandle jedes Produkt in eine CSV-Zeile um.
3. Schreibe die Zeilen mit `Files.write(...)` in die Datei.
4. Gib bei einem Fehler eine einfache Meldung aus.

Hinweis:

```java
Files.write(Path.of(dateipfad), zeilen);
```

---

### Aufgabe 5 – CSV-Datei erzeugen

Speichere die drei Produkte nach:

```text
data/produkte.csv
```

Auftrag:

1. Starte das Programm.
2. Öffne die Datei im Editor.
3. Prüfe, ob jede Produktzeile vorhanden ist.
4. Prüfe, ob `;` als Trennzeichen verwendet wird.

---

### Aufgabe 6 – Produkte erneut laden

Nutze deinen bestehenden `CsvProduktLeser`.

Auftrag:

1. Lade die gespeicherte Datei erneut.
2. Gib die Anzahl Produkte aus.
3. Prüfe, ob wieder drei Produkte geladen werden.

Erwartung:

```text
Anzahl Produkte: 3
```

---

### Aufgabe 7 – Gesamtwert nach erneutem Laden prüfen

Nutze die geladene Liste mit deiner `ProduktVerwaltung`.

Auftrag:

1. Berechne den Gesamtwert nach dem erneuten Laden.
2. Gib den Gesamtwert aus.
3. Vergleiche mit dem erwarteten Wert.

Erwartung:

```text
Gesamtwert: 368.4
```

---

## Vertiefung

### Aufgabe 8 – Leere Produktliste speichern

Erstelle eine leere `ArrayList<Produkt>`.

Auftrag:

1. Speichere die leere Liste in `data/produkte.csv`.
2. Öffne die Datei im Editor.
3. Lade die Datei erneut.
4. Prüfe, ob null Produkte geladen werden.

Ziel:

```text
Eine leere Liste ist kein Programmfehler.
```

---

### Aufgabe 9 – Überschreiben bewusst prüfen

Auftrag:

1. Speichere zuerst drei Produkte.
2. Speichere danach nur ein Produkt in dieselbe Datei.
3. Öffne die Datei.
4. Prüfe, ob nur noch das eine Produkt vorhanden ist.

Erwartung:

```text
Die Datei enthält die zuletzt gespeicherte Liste.
```

---

### Aufgabe 10 – Ungültige Produkte überspringen

Erweitere den Speicherprozess um einfache Prüfungen.

Ungültig sind zum Beispiel:

- leerer Produktname
- Preis kleiner als 0

Auftrag:

1. Prüfe jedes Produkt vor dem Speichern.
2. Speichere nur gültige Produkte.
3. Gib bei einem ungültigen Produkt eine einfache Meldung aus.
4. Das Programm soll weiterlaufen.

Beispielmeldung:

```text
Produkt wird nicht gespeichert: leerer Name
```

---

### Aufgabe 11 – Speicherlogik aus `main` auslagern

Prüfe deine Klassen.

Auftrag:

1. `Main` soll nur den Ablauf starten.
2. `CsvProduktSpeicher` soll die Datei schreiben.
3. `ProduktVerwaltung` soll fachliche Auswertungen machen.
4. Verschiebe Code, der nicht zur passenden Klasse gehört.

---

## Optionaler Transfer

Diese Aufgaben sind freiwillig.

### Transfer 1 – Zusätzliches Produktattribut speichern

Erweitere das Produkt um ein einfaches Attribut, zum Beispiel `bestand`.

Auftrag:

1. Passe die CSV-Zeile an.
2. Passe das Laden und Speichern gleich an.
3. Prüfe, ob das Format weiterhin zusammenpasst.

---

### Transfer 2 – Kopfzeile speichern

Speichere am Anfang der Datei eine Kopfzeile:

```text
Name;Preis
```

Auftrag:

1. Ergänze die Kopfzeile beim Speichern.
2. Passe den Leser so an, dass diese Zeile nicht als Produkt geladen wird.

---

### Transfer 3 – Datei vor dem Überschreiben sichern

Diese Aufgabe ist ein freiwilliger Ausblick. Sie zeigt, warum Überschreiben bewusst passieren soll.

Auftrag:

1. Überlege, wie die bisherige Datei vor dem Speichern gesichert werden könnte.
2. Besprich kurz, welche Datei die alte und welche Datei die neue Liste enthält.
3. Prüfe beide Dateien im Editor, falls ihr die Sicherung praktisch umsetzt.

---

### Transfer 4 – Exportfunktion erweitern

Ergänze eine Methode, die unter einem frei wählbaren Dateinamen speichert.

Beispiel:

```text
data/export-produkte.csv
```

---

## Typische Fehler prüfen

Prüfe deine Lösung bewusst auf diese Punkte:

- Wurde das Trennzeichen `;` gespeichert?
- Passt das gespeicherte Format zum Leser?
- Wird jede Produktzeile in eine eigene Zeile geschrieben?
- Wird die Datei bewusst überschrieben?
- Wird die `ArrayList<Produkt>` mit einer Schleife durchlaufen?
- Bleibt die Speicherlogik ausserhalb von `main`?
- Wird eine leere Produktliste ruhig behandelt?
- Gibt es eine einfache Meldung, wenn die Datei nicht geschrieben werden kann?

---

## Reflexion

Beantworte kurz:

1. Warum ist Speichern für Persistenz wichtig?
2. Warum sind CSV-Dateien praktisch, obwohl sie einfach sind?
3. Warum müssen Laden und Speichern dasselbe Format verwenden?
4. Warum soll Dateilogik nicht in der Produktverwaltung stehen?
5. Welche Fehler können beim Speichern auftreten?
