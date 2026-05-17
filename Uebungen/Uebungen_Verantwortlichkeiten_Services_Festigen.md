# Übungen – Verantwortlichkeiten und Services festigen

## Vorwissen

Du brauchst:

- Klassen und Objekte
- Getter und Setter
- `ArrayList`
- Maven-Projektstruktur
- einfache JUnit-Tests
- CSV-Laden und CSV-Speichern
- `ProduktSpeicher` als Interface
- `CsvProduktSpeicher` als konkrete Speicherklasse
- `LagerService` als Klasse für Fachlogik

Nicht verwendet werden:

- grosse Frameworks
- Datenbanken
- Web-APIs
- grosse Architekturtheorie

---

## Vorbereitung

Arbeite mit der bekannten Lagerverwaltung.

Beispielstruktur:

```text
lagerverwaltung/
  pom.xml
  data/
    produkte.csv
  src/main/java/
    ch/allianz/youngoitv/lager/
      Main.java
      LagerService.java
      ProduktSpeicher.java
      CsvProduktSpeicher.java
      model/Produkt.java
  src/test/java/
    ch/allianz/youngoitv/lager/
      LagerServiceTest.java
```

Prüfe nach praktischen Änderungen:

```bash
mvn test
```

Wenn noch keine Tests vorhanden sind:

```bash
mvn package
```

Ziel:

```text
Verantwortlichkeiten erkennen.
Fachlogik bewusst platzieren.
Main vereinfachen.
Persistenz und Fachlogik trennen.
Service-Methoden testen.
Struktur begründen.
```

---

## Basis

### Aufgabe 1 – Verantwortlichkeiten vorhandener Methoden zuordnen

Ordne jede Methode oder Handlung einer Klasse zu.

| Methode oder Handlung | Passende Klasse | Begründung |
|---|---|---|
| Produktname speichern | | |
| Produktpreis speichern | | |
| Bestand nach Verkauf reduzieren | | |
| prüfen, ob eine Verkaufsmenge gültig ist | | |
| Laden und Speichern als Vertrag beschreiben | | |
| Produkte aus CSV-Datei konkret laden | | |
| Produkte in CSV-Datei konkret speichern | | |
| Programmablauf starten | | |
| `LagerService` und `ProduktSpeicher` verwenden | | |
| CSV-Zeile mit `split(";")` zerlegen | | |
| Warnung bei tiefem Bestand prüfen | | |

Verwende diese Klassen:

- `Produkt`
- `LagerService`
- `ProduktSpeicher`
- `CsvProduktSpeicher`
- `Main`

---

### Aufgabe 2 – Problematische Logik in Main erkennen

Öffne deine aktuelle `Main.java`.

Markiere jede relevante Stelle mit einer Kategorie:

- Ablaufsteuerung
- Fachlogik
- Persistenzlogik
- Ausgabe

Hilfstabelle:

| Codeausschnitt | Kategorie | Soll bleiben? | Falls nein: Wohin? |
|---|---|---|---|
| Produkte laden | | | |
| Verkauf prüfen | | | |
| Bestand ändern | | | |
| CSV-Zeilen schreiben | | | |
| Erfolgsmeldung ausgeben | | | |
| Warnung prüfen | | | |

Notiere danach zwei Stellen, an denen `Main` zu viel Verantwortung trägt.

---

### Aufgabe 3 – Fachlogik und Persistenzlogik markieren

Markiere im folgenden Ausschnitt:

- `F` für Fachlogik
- `P` für Persistenzlogik
- `A` für Ablaufsteuerung

```java
ProduktSpeicher speicher = new CsvProduktSpeicher();
ArrayList<Produkt> produkte = speicher.ladeProdukte("data/produkte.csv");

Produkt produkt = produkte.get(0);
int menge = 3;

if (menge > 0 && produkt.getBestand() >= menge) {
    produkt.setBestand(produkt.getBestand() - menge);
}

speicher.speichereProdukte(produkte, "data/produkte.csv");
```

Beantworte:

1. Welche Zeilen gehören in `Main`?
2. Welche Zeilen gehören besser in den `LagerService`?
3. Welche Zeilen gehören zur Persistenz?

---

### Aufgabe 4 – Kleine Logikverschiebung durchführen

Verschiebe diese Logik aus `Main` in `LagerService`:

```java
if (menge > 0 && produkt.getBestand() >= menge) {
    produkt.setBestand(produkt.getBestand() - menge);
}
```

Zielmethode:

```java
public boolean verkaufen(Produkt produkt, int menge) {
    if (menge <= 0 || produkt.getBestand() < menge) {
        return false;
    }

    produkt.setBestand(produkt.getBestand() - menge);
    return true;
}
```

Passe `Main` danach an:

```java
boolean verkauft = lagerService.verkaufen(produkt, menge);
```

Prüfe:

- Verkauf mit genug Bestand reduziert den Bestand.
- Verkauf mit zu hoher Menge verändert den Bestand nicht.
- Verkauf mit `0` verändert den Bestand nicht.

---

### Aufgabe 5 – Main vereinfachen

Formuliere `Main` so, dass der Ablauf klar sichtbar ist.

Erwarteter Ablauf:

```text
1. ProduktSpeicher erstellen
2. Produkte laden
3. LagerService erstellen
4. Fachliche Änderung ausführen
5. Resultat ausgeben
6. Produkte speichern
```

In `Main` sollen keine direkten CSV-Details vorkommen:

- kein `split(";")`
- kein direktes Erzeugen von CSV-Zeilen
- kein `Files.write(...)`
- keine Verkaufsbedingung mit `produkt.getBestand() >= menge`

---

### Aufgabe 6 – Verhalten erneut prüfen

Führe nach dem Refactoring aus:

```bash
mvn test
```

Wenn noch keine Tests vorhanden sind:

```bash
mvn package
```

Ergänze zusätzlich eine kurze manuelle Prüfung:

| Fall | Erwartung | Ergebnis |
|---|---|---|
| Verkauf `3` bei Bestand `10` | Bestand wird `7` | |
| Verkauf `11` bei Bestand `10` | Bestand bleibt `10` | |
| Verkauf `0` bei Bestand `10` | Bestand bleibt `10` | |
| Speichern nach Verkauf | CSV-Speicherung läuft weiterhin über `ProduktSpeicher` | |

---

## Vertiefung

### Aufgabe 7 – Bewusst schlechte Struktur analysieren

Analysiere diese Klasse:

```java
public class CsvProduktSpeicher {
    public boolean verkaufenUndSpeichern(Produkt produkt, int menge, String pfad) {
        if (menge <= 0) {
            return false;
        }

        if (produkt.getBestand() < menge) {
            return false;
        }

        produkt.setBestand(produkt.getBestand() - menge);

        // Produkte als CSV speichern
        return true;
    }
}
```

Auftrag:

1. Markiere Fachlogik.
2. Markiere Persistenzlogik.
3. Erkläre, warum diese Verantwortung problematisch platziert ist.
4. Schlage eine bessere Aufteilung vor.

---

### Aufgabe 8 – Doppelte Logik erkennen

Suche in deinem Projekt doppelte Prüfungen.

Beispiele:

```java
menge > 0
produkt.getBestand() >= menge
produkt.getBestand() < grenze
```

Auftrag:

1. Notiere zwei doppelte oder sehr ähnliche Prüfungen.
2. Entscheide, ob sie fachlich zusammengehören.
3. Führe sie in einer passenden Service-Methode zusammen.
4. Passe die Aufrufer an.
5. Führe `mvn test` aus.

---

### Aufgabe 9 – Geeignete und ungeeignete Service-Methoden unterscheiden

Ordne jede Methode ein.

| Methode | Geeignet für `LagerService`? | Begründung |
|---|---|---|
| `verkaufen(Produkt produkt, int menge)` | | |
| `bestandErhoehen(Produkt produkt, int menge)` | | |
| `warnungPruefen(Produkt produkt, int grenze)` | | |
| `speichereCsvDatei(ArrayList<Produkt> produkte)` | | |
| `zeigeMenue()` | | |
| `berechneLagerwert(ArrayList<Produkt> produkte)` | | |
| `parseCsvZeile(String zeile)` | | |

Leitfrage:

```text
Beschreibt die Methode eine fachliche Lagerregel oder eine technische Aufgabe?
```

---

### Aufgabe 10 – Methodennamen verbessern

Prüfe deine Methodennamen.

Ungünstige Namen:

```text
mache()
check()
update()
save()
run()
```

Bessere Namen:

```text
verkaufen(...)
bestandErhoehen(...)
warnungPruefen(...)
speichereProdukte(...)
ladeProdukte(...)
```

Auftrag:

1. Suche drei unklare Namen.
2. Benenne sie so um, dass die Verantwortung klarer wird.
3. Passe Tests und Aufrufe an.
4. Führe `mvn test` aus.

---

### Aufgabe 11 – CSV-Schreiben aus fachlichen Klassen entfernen

Suche nach Dateioperationen oder CSV-Details ausserhalb von `CsvProduktSpeicher`.

Hinweise:

- `Files.write(...)`
- `String.join(";")`
- `produkt.getName() + ";" + ...`
- Dateipfade wie `"data/produkte.csv"` in fachlichen Methoden

Auftrag:

1. Markiere jede gefundene Stelle.
2. Entscheide, ob sie in `CsvProduktSpeicher` gehört.
3. Entferne CSV-Schreiben aus `LagerService` oder `Produkt`.
4. Lasse `Main` nur den Speicher aufrufen.
5. Prüfe das Verhalten erneut.

---

## Testaufgaben

### Aufgabe 12 – Service-Methoden testen

Ergänze Tests für `LagerService`.

Pflichtfälle:

| Testfall | Erwartung |
|---|---|
| Verkauf mit genug Bestand | Methode gibt `true` zurück, Bestand sinkt |
| Verkauf mit zu hoher Menge | Methode gibt `false` zurück, Bestand bleibt gleich |
| Verkauf mit Menge `0` | Methode gibt `false` zurück, Bestand bleibt gleich |
| Verkauf mit negativer Menge | Methode gibt `false` zurück, Bestand bleibt gleich |
| Bestand erhöhen mit gültiger Menge | Bestand steigt |
| Bestand erhöhen mit ungültiger Menge | Bestand bleibt gleich |

Beispiel:

```java
@Test
void verkaufen_mitGenugBestand_reduziertBestand() {
    Produkt produkt = new Produkt("Maus", 24.90, 10);
    LagerService service = new LagerService();

    boolean verkauft = service.verkaufen(produkt, 3);

    assertTrue(verkauft);
    assertEquals(7, produkt.getBestand());
}
```

---

### Aufgabe 13 – Fehlerfälle testen

Ergänze Tests für ungültige Werte.

Prüfe mindestens:

- `menge` ist `0`
- `menge` ist negativ
- Bestand reicht nicht aus
- Warnbestand-Grenze ist genau erreicht

Beispiel für Warnbestand:

```text
Bestand 5, Grenze 5 -> keine Warnung
Bestand 4, Grenze 5 -> Warnung
```

---

### Aufgabe 14 – Bestehende Tests an neue Struktur anpassen

Wenn Tests vorher direkt `Main` oder alte Methoden geprüft haben, passe sie an.

Auftrag:

1. Verschiebe fachliche Tests zu `LagerServiceTest`.
2. Prüfe CSV-Verhalten separat über `CsvProduktSpeicher`.
3. Verwende für Service-Tests keine echte CSV-Datei.
4. Führe `mvn test` aus.

Notiere:

```text
Welche Tests wurden angepasst?
Welche Tests prüfen Fachlogik?
Welche Tests prüfen Persistenz?
```

---

## Transfer

### Aufgabe 15 – Weitere mögliche Services diskutieren

Diskutiert zu zweit:

1. Welche weiteren Services könnten in einer grösseren Lagerverwaltung sinnvoll sein?
2. Welche davon wären für die aktuelle kleine Anwendung übertrieben?
3. Woran erkennt man, dass ein Service eine klare Verantwortung hat?

Mögliche Ideen:

- `BestellService`
- `InventurService`
- `PreisService`
- `WarnService`

Ihr müsst diese Services nicht implementieren.

---

### Aufgabe 16 – Grenzen kleiner Strukturen beschreiben

Beantworte schriftlich:

1. Wann hilft ein `LagerService`?
2. Wann wird ein `LagerService` zu gross?
3. Wann sind mehrere Services sinnvoll?
4. Wann machen mehrere Services ein kleines Programm unnötig kompliziert?

---

### Aufgabe 17 – Zukünftige Erweiterungen einordnen

Wähle zwei mögliche Erweiterungen:

- Mindestbestand pro Produkt
- Rabatte bei grosser Verkaufsmenge
- Export als andere Datei
- zweite Speicherart
- automatische Nachbestellung
- Lagerwert pro Kategorie

Für jede Erweiterung:

1. Welche Klasse wäre betroffen?
2. Welche Klasse sollte nicht betroffen sein?
3. Welche Tests wären sinnvoll?
4. Wird die aktuelle Struktur dadurch eher bestätigt oder eher belastet?

---

## Abschlussreflexion

Beantworte am Ende:

1. Welche Verantwortung war schwierig zuzuordnen?
2. Warum hilft der `LagerService`?
3. Welche Klasse wurde zu gross oder wäre schnell zu gross geworden?
4. Welche Stelle war schwer testbar?
5. Wie würde sich die Struktur bei Erweiterungen verhalten?
6. Welche Fehlstruktur erkennst du bei dir am schnellsten?

---

## Checkliste

Vor der Abgabe:

- `Main` steuert hauptsächlich den Ablauf.
- Fachlogik liegt im `LagerService`.
- CSV-Details liegen im `CsvProduktSpeicher`.
- `ProduktSpeicher` bleibt der Vertrag für Persistenz.
- `Produkt` bleibt ein Datenobjekt.
- Doppelte Prüfungen wurden reduziert.
- Methodennamen beschreiben die Verantwortung.
- Service-Methoden sind getestet.
- `mvn test` oder mindestens `mvn package` wurde ausgeführt.
