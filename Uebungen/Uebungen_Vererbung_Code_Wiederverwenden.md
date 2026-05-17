# Übungen – Gemeinsamen Code mit Vererbung wiederverwenden

## Vorwissen

Du brauchst:

- Klassen und Objekte
- Methoden mit Parametern und Rückgabewerten
- `ArrayList`
- einfache Schleifen
- Maven-Projektstruktur
- `ProduktSpeicher` als Interface
- `CsvProduktSpeicher`
- `KonsolenProduktSpeicher`
- kleine Hilfsmethoden aus dem vorherigen Refactoring-Block

Nicht verwendet werden:

- tiefe Vererbungshierarchien
- abstrakte Klassen als Vertiefung
- `instanceof`
- Downcasting
- Template Method
- Factory
- Dependency Injection
- Spring
- Datenbank

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
      CsvProduktSpeicher.java
      KonsolenProduktSpeicher.java
      ProduktSpeicher.java
      ProduktSpeicherBasis.java
      model/Produkt.java
```

Ausgangspunkt ist dieselbe Interface-Signatur wie in den vorherigen Einheiten:

```java
void speichern(ArrayList<Produkt> produkte, String dateipfad);
```

Ziel dieser Übung:

```text
Gemeinsamen Code erkennen.
Eine kleine Basisklasse erstellen.
Konkrete Klassen mit extends anpassen.
Verhalten nach dem Refactoring prüfen.
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

### Aufgabe 1 – Doppelte Hilfsmethoden markieren

Öffne:

- `CsvProduktSpeicher`
- `KonsolenProduktSpeicher`

Auftrag:

1. Markiere Hilfsmethoden, die gleich oder fast gleich sind.
2. Markiere Stellen mit `produkt.getName()`.
3. Markiere Stellen mit `produkt.getPreis()`.
4. Notiere, welche Teile wirklich gemeinsam sind.
5. Notiere, welche Teile unterschiedlich bleiben müssen.

Hilfstabelle:

| Beobachtung | Gemeinsam oder unterschiedlich? | Begründung |
|---|---|---|
| Produktname lesen | | |
| Produktpreis lesen | | |
| CSV-Zeile mit `;` erzeugen | | |
| Konsolenzeile mit `:` erzeugen | | |
| Datei schreiben | | |
| Konsole ausgeben | | |

---

### Aufgabe 2 – Gemeinsame Methode zur Produktformatierung erkennen

Betrachte diese beiden Zeilen:

```java
produkt.getName() + ";" + produkt.getPreis()
```

```java
produkt.getName() + ": " + produkt.getPreis()
```

Auftrag:

1. Beschreibe, was daran gleich ist.
2. Beschreibe, was daran unterschiedlich ist.
3. Entscheide, ob eine gemeinsame Hilfsmethode mit einem Trennzeichen sinnvoll wäre.
4. Begründe deine Entscheidung in zwei Sätzen.

Mögliche gemeinsame Methode:

```java
protected String produktZeile(Produkt produkt, String trennzeichen) {
    return produkt.getName() + trennzeichen + produkt.getPreis();
}
```

Wichtig: Diese Methode ist nur sinnvoll, solange beide Klassen wirklich denselben Grundaufbau aus Name, Trennzeichen und Preis verwenden.

---

### Aufgabe 3 – `ProduktSpeicherBasis` erstellen

Erstelle eine neue Klasse:

```java
public class ProduktSpeicherBasis {
    protected String produktZeile(Produkt produkt, String trennzeichen) {
        return produkt.getName() + trennzeichen + produkt.getPreis();
    }
}
```

Auftrag:

1. Lege die Klasse im gleichen Package wie die Speicherklassen an.
2. Ergänze den passenden Import für `Produkt`, falls dein Projekt ihn braucht.
3. Prüfe, ob die Klasse kompiliert.

Wichtig:

```text
ProduktSpeicherBasis implementiert das Interface ProduktSpeicher nicht.
Die Basisklasse enthält nur gemeinsame Hilfsmethoden.
```

---

### Aufgabe 4 – `CsvProduktSpeicher` mit `extends` anpassen

Passe den Klassennamen an:

```java
public class CsvProduktSpeicher extends ProduktSpeicherBasis implements ProduktSpeicher {
```

Nutze die geerbte Methode:

```java
for (Produkt produkt : produkte) {
    zeilen.add(produktZeile(produkt, ";"));
}
```

Auftrag:

1. Ergänze `extends ProduktSpeicherBasis`.
2. Lasse `implements ProduktSpeicher` stehen.
3. Ersetze die doppelte Formatierung durch `produktZeile(...)`.
4. Prüfe, ob die CSV-Klasse noch kompiliert.

---

### Aufgabe 5 – `KonsolenProduktSpeicher` mit `extends` anpassen

Passe auch die Konsolenklasse an:

```java
public class KonsolenProduktSpeicher extends ProduktSpeicherBasis implements ProduktSpeicher {
```

Nutze die geerbte Methode:

```java
for (Produkt produkt : produkte) {
    System.out.println(produktZeile(produkt, ": "));
}
```

Auftrag:

1. Ergänze `extends ProduktSpeicherBasis`.
2. Lasse `implements ProduktSpeicher` stehen.
3. Verwende `produktZeile(...)` für die Konsolenausgabe.
4. Prüfe, ob die Konsolenklasse noch kompiliert.

---

### Aufgabe 6 – Verhalten erneut prüfen

Führe aus:

```bash
mvn package
```

Wenn Tests vorhanden sind:

```bash
mvn test
```

Auftrag:

1. Prüfe, ob das Projekt kompiliert.
2. Führe `Main` aus, wenn das in deinem Projekt vorgesehen ist.
3. Vergleiche CSV-Datei und Konsolenausgabe mit dem Verhalten vor dem Umbau.
4. Notiere, ob sich das gewünschte Verhalten geändert hat.

Erwartung:

```text
Die Struktur verwendet eine kleine Basisklasse.
Das Verhalten bleibt gleich.
```

---

## Vertiefung

### Aufgabe 7 – Entscheiden, was in die Basisklasse gehört

Ordne die folgenden Methoden zu.

| Methode oder Logik | Interface | Basisklasse | konkrete Klasse |
|---|---|---|---|
| `speichern(...)` | | | |
| `produktZeile(...)` | | | |
| Datei mit `Files.write(...)` schreiben | | | |
| `System.out.println(...)` verwenden | | | |
| `istProduktListeLeer(...)` | | | |
| CSV-Trennzeichen festlegen | | | |

Begründe zwei deiner Entscheidungen schriftlich.

---

### Aufgabe 8 – Interface und Basisklasse vergleichen

Fülle die Tabelle aus.

| Element | Aufgabe | Beispiel im Projekt |
|---|---|---|
| Interface | | |
| Basisklasse | | |
| konkrete Klasse | | |

Nutze diese Begriffe:

- Vertrag
- gemeinsame Implementierung
- spezifisches Verhalten
- `implements`
- `extends`

---

### Aufgabe 9 – Kleine Prüfung nach dem Refactoring

Erstelle eine einfache manuelle Prüfung oder nutze vorhandene Tests.

Prüfidee:

1. Lege zwei Produkte an.
2. Speichere sie mit `CsvProduktSpeicher`.
3. Speichere sie mit `KonsolenProduktSpeicher`.
4. Prüfe, ob beide Klassen weiterhin ihr eigenes Ziel verwenden.

Beispielprodukte:

```text
Maus;34.9
Tastatur;79.9
```

Auftrag:

1. Führe `mvn test` oder `mvn package` aus.
2. Notiere den Befehl.
3. Notiere das Ergebnis.
4. Beschreibe, was du zusätzlich manuell geprüft hast.

---

### Aufgabe 10 – Lesbarkeit und Wartbarkeit beschreiben

Beantworte schriftlich:

1. Ist die Wiederverwendung jetzt besser sichtbar?
2. Ist die Basisklasse noch klein genug?
3. Welche Änderung wäre nun einfacher?
4. Welche Änderung wäre immer noch in den konkreten Klassen nötig?

Verwende diesen Satzanfang:

```text
Die Basisklasse hilft hier, weil ...
Sie wäre problematisch, wenn ...
```

---

## Transfer

### Aufgabe 11 – Weitere mögliche Hilfsmethoden prüfen

Prüfe, ob eine der folgenden Methoden sinnvoll in `ProduktSpeicherBasis` passen würde.

```java
protected boolean istLeer(ArrayList<Produkt> produkte) {
    return produkte.isEmpty();
}
```

```java
protected String anzahlMeldung(ArrayList<Produkt> produkte) {
    return "Anzahl Produkte: " + produkte.size();
}
```

Auftrag:

1. Wähle eine Methode aus.
2. Entscheide, ob sie wirklich von beiden Speicherklassen gebraucht wird.
3. Begründe deine Entscheidung.
4. Implementiere sie nur, wenn sie den Code tatsächlich klarer macht.

---

### Aufgabe 12 – Ungeeignete Auslagerung erkennen

Jemand schlägt vor, diese Methode in `ProduktSpeicherBasis` zu verschieben:

```java
public void speichern(ArrayList<Produkt> produkte, String ziel) {
    // schreibt manchmal in eine Datei und manchmal auf die Konsole
}
```

Auftrag:

1. Erkläre, warum diese Auslagerung problematisch ist.
2. Nenne zwei Unterschiede zwischen CSV-Speichern und Konsolenausgabe.
3. Beschreibe, welche Verantwortung in den konkreten Klassen bleiben soll.

---

### Aufgabe 13 – Wann ist Vererbung nicht sinnvoll?

Beschreibe je ein Beispiel.

| Vererbung ist sinnvoll, wenn ... | Vererbung ist nicht sinnvoll, wenn ... |
|---|---|
| | |
| | |
| | |

Nutze mindestens drei dieser Begriffe:

- gemeinsamer Code
- klare Verantwortung
- zufällige Ähnlichkeit
- zu starke Kopplung
- Verhalten bleibt gleich
- Basisklasse bleibt klein

---

### Aufgabe 14 – Alternative mit Hilfsklasse diskutieren

Statt Vererbung könnte eine Hilfsklasse verwendet werden:

```java
public class ProduktFormatierer {
    public String produktZeile(Produkt produkt, String trennzeichen) {
        return produkt.getName() + trennzeichen + produkt.getPreis();
    }
}
```

Auftrag:

1. Beschreibe, wie `CsvProduktSpeicher` diese Hilfsklasse verwenden könnte.
2. Beschreibe, wie `KonsolenProduktSpeicher` diese Hilfsklasse verwenden könnte.
3. Nenne einen Vorteil gegenüber Vererbung.
4. Nenne einen Nachteil gegenüber Vererbung.

---

## Typische Fehler prüfen

Prüfe deinen Code bewusst auf diese Fehler:

| Prüfung | Erfüllt? |
|---|---|
| `implements ProduktSpeicher` ist weiterhin vorhanden | |
| `extends ProduktSpeicherBasis` steht nur bei den konkreten Speicherklassen | |
| `ProduktSpeicherBasis` enthält nur kleine Hilfsmethoden | |
| `speichern(...)` bleibt in den konkreten Klassen | |
| CSV-Datei und Konsole werden nicht vermischt | |
| Verhalten wurde nach dem Umbau geprüft | |
| Es wird kein `instanceof` verwendet | |
| Es wird kein Downcasting verwendet | |
| Die Basisklasse hat einen klaren Namen | |

---

## Reflexion

Beantworte zum Schluss:

1. Welcher Code war wirklich gemeinsam?
2. Was sollte bewusst in der konkreten Klasse bleiben?
3. Warum ist Vererbung nicht immer die richtige Lösung?
4. Was ist der Unterschied zwischen Interface und Vererbung?
5. Wie helfen Tests beim Umbau?
