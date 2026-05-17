# Übungen – Fachlogik in Services bündeln

## Vorwissen

Du brauchst:

- Klassen und Objekte
- Kapselung mit Gettern und Settern
- Methoden mit Rückgabewerten
- `ArrayList`
- Maven-Projektstruktur
- einfache JUnit-Tests
- `ProduktSpeicher` als Interface
- `CsvProduktSpeicher` als konkrete Speicherklasse
- die Idee, dass `Main` nicht alles machen soll

Nicht verwendet werden:

- Frameworks
- Datenbank
- komplexe Architekturmodelle
- automatische Objekterzeugung
- Web-Anwendungen
- grosse Paketstrukturen

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

Ein Produkt besitzt mindestens:

```text
Name
Preis
Bestand
```

Ziel dieser Übung:

```text
Fachliche Regeln aus Main herauslösen.
LagerService erstellen.
Main vereinfachen.
Speichern und Fachlogik getrennt halten.
Verhalten erneut prüfen.
```

Prüfe nach praktischen Änderungen:

```bash
mvn test
```

Wenn noch keine Tests vorhanden sind:

```bash
mvn package
```

---

## Basis

### Aufgabe 1 – Fachliche Regeln im bestehenden Code markieren

Öffne `Main`.

Markiere jede Stelle mit einer der folgenden Kategorien:

- Ablaufsteuerung
- Fachlogik
- Persistenz
- Ausgabe

Hilfstabelle:

| Code oder Handlung | Kategorie | Begründung |
|---|---|---|
| Produktliste laden | | |
| Verkauf prüfen | | |
| Bestand reduzieren | | |
| Produkte speichern | | |
| Erfolgsmeldung ausgeben | | |
| Warnung bei tiefem Bestand prüfen | | |

Notiere danach:

1. Welche Regeln sind fachlich?
2. Welche Teile gehören weiterhin in `Main`?
3. Welche Teile gehören zum Speichern?

---

### Aufgabe 2 – `LagerService` erstellen

Erstelle eine neue Klasse:

```java
public class LagerService {
}
```

Auftrag:

1. Lege die Klasse im gleichen Package wie `Main` an oder in einem passenden Unterpackage.
2. Ergänze keine Speicherlogik.
3. Ergänze keine Konsolenmenüs.
4. Prüfe, ob das Projekt noch kompiliert.

Erwartung:

```text
LagerService ist eine normale Java-Klasse für fachliche Regeln.
```

---

### Aufgabe 3 – `bestandPruefen(...)` ergänzen

Ergänze im `LagerService`:

```java
public boolean bestandPruefen(Produkt produkt, int menge) {
    return menge > 0 && produkt.getBestand() >= menge;
}
```

Auftrag:

1. Ergänze den passenden Import für `Produkt`, falls nötig.
2. Prüfe `menge > 0`.
3. Prüfe, ob genug Bestand vorhanden ist.
4. Kompiliere das Projekt.

Testideen:

| Bestand | Menge | Erwartung |
|---:|---:|---|
| 10 | 3 | `true` |
| 10 | 10 | `true` |
| 10 | 11 | `false` |
| 10 | 0 | `false` |

---

### Aufgabe 4 – `verkaufen(...)` aus `Main` verschieben

Verschiebe die Verkaufsregel in den `LagerService`:

```java
public boolean verkaufen(Produkt produkt, int menge) {
    if (!bestandPruefen(produkt, menge)) {
        return false;
    }

    produkt.setBestand(produkt.getBestand() - menge);
    return true;
}
```

Auftrag:

1. Suche die Verkaufslogik in `Main`.
2. Entferne dort die direkte Bestandsänderung.
3. Rufe stattdessen `lagerService.verkaufen(produkt, menge)` auf.
4. Prüfe, ob der Bestand nach einem erfolgreichen Verkauf korrekt sinkt.
5. Prüfe, ob der Bestand bei einem abgelehnten Verkauf gleich bleibt.

---

### Aufgabe 5 – `bestandErhoehen(...)` ergänzen

Ergänze im `LagerService`:

```java
public void bestandErhoehen(Produkt produkt, int menge) {
    if (menge <= 0) {
        return;
    }

    produkt.setBestand(produkt.getBestand() + menge);
}
```

Auftrag:

1. Erhöhe einen Bestand mit gültiger Menge.
2. Prüfe eine Menge `0`.
3. Prüfe eine negative Menge.
4. Notiere, warum die Methode keine CSV-Datei schreiben soll.

---

### Aufgabe 6 – `Main` vereinfachen

Passe `Main` so an, dass sie den Ablauf zeigt:

```java
LagerService lagerService = new LagerService();

boolean verkauft = lagerService.verkaufen(produkt, 3);

if (verkauft) {
    System.out.println("Verkauf erfolgreich");
} else {
    System.out.println("Zu wenig Bestand");
}

ProduktSpeicher speicher = new CsvProduktSpeicher();
// Produkte speichern
```

Auftrag:

1. Entferne fachliche Detailprüfungen aus `Main`.
2. Lasse Laden und Speichern bei den passenden Speicherklassen.
3. Lasse einfache Ausgaben in `Main`, wenn sie nur den Ablauf sichtbar machen.
4. Prüfe das Verhalten erneut.

---

### Aufgabe 7 – Verhalten erneut prüfen

Führe aus:

```bash
mvn test
```

Wenn noch keine Tests vorhanden sind:

```bash
mvn package
```

Prüfe mindestens:

| Prüfung | Erwartung |
|---|---|
| Verkauf mit genug Bestand | Bestand sinkt |
| Verkauf mit zu hoher Menge | Bestand bleibt gleich |
| Bestand erhöhen mit gültiger Menge | Bestand steigt |
| Bestand erhöhen mit ungültiger Menge | Bestand bleibt gleich |
| Speichern | läuft weiterhin über `ProduktSpeicher` |

---

## Vertiefung

### Aufgabe 8 – Warnung bei tiefem Bestand ergänzen

Ergänze im `LagerService`:

```java
public boolean warnungPruefen(Produkt produkt, int grenze) {
    return produkt.getBestand() < grenze;
}
```

Auftrag:

1. Verwende eine Grenze, zum Beispiel `5`.
2. Prüfe ein Produkt mit Bestand `3`.
3. Prüfe ein Produkt mit Bestand `5`.
4. Prüfe ein Produkt mit Bestand `8`.
5. Entscheide, ob die Warnmeldung selbst im Service stehen soll.

Hinweis:

```text
Der Service kann true oder false liefern.
Main kann entscheiden, welche Meldung angezeigt wird.
```

Service-Methoden sollen möglichst fachliche Werte zurückgeben. Texte für die Konsole bleiben besser in `Main`.

---

### Aufgabe 9 – Weitere fachliche Methoden ergänzen

Wähle eine Methode aus:

```java
public boolean istAusverkauft(Produkt produkt) {
    return produkt.getBestand() == 0;
}
```

```java
public double lagerwert(Produkt produkt) {
    return produkt.getPreis() * produkt.getBestand();
}
```

Auftrag:

1. Implementiere eine Methode im `LagerService`.
2. Begründe, warum sie Fachlogik ist.
3. Schreibe eine kleine Prüfung oder einen Test.

---

### Aufgabe 10 – Service und Persistenz vergleichen

Fülle die Tabelle aus.

| Aufgabe | `LagerService` | `ProduktSpeicher` oder `CsvProduktSpeicher` | Begründung |
|---|---|---|---|
| Verkauf prüfen | | | |
| CSV-Zeile schreiben | | | |
| Bestand erhöhen | | | |
| Datei speichern | | | |
| Warnung bei tiefem Bestand prüfen | | | |
| Speichervertrag beschreiben | | | |

---

### Aufgabe 11 – Verantwortlichkeiten begründen

Beantworte schriftlich:

1. Warum soll `Main` nicht selbst den Bestand prüfen?
2. Warum soll `CsvProduktSpeicher` keine Verkaufsregeln kennen?
3. Warum soll `Produkt` nicht die ganze Lagerverwaltung steuern?
4. Warum ist `LagerService` ein passender Name?

Verwende mindestens vier dieser Begriffe:

- Ablauf
- Fachlogik
- Persistenz
- Verantwortung
- testen
- ändern
- lesbar

---

### Aufgabe 12 – Kleine Tests für Service-Methoden

Schreibe Tests für den `LagerService`.

Beispiel:

```java
@Test
void verkaufenReduziertBestand() {
    Produkt produkt = new Produkt("Maus", 24.90, 10);
    LagerService service = new LagerService();

    boolean verkauft = service.verkaufen(produkt, 3);

    assertTrue(verkauft);
    assertEquals(7, produkt.getBestand());
}
```

Weitere Testideen:

- Verkauf mit zu hoher Menge gibt `false` zurück.
- Verkauf mit zu hoher Menge verändert den Bestand nicht.
- Bestandserhöhung mit gültiger Menge erhöht den Bestand.
- Warnung bei tiefem Bestand gibt `true` zurück.

Hinweis: `@Test` kommt aus JUnit Jupiter. `assertTrue`, `assertFalse` und `assertEquals` kommen aus den JUnit Assertions.

Führe danach aus:

```bash
mvn test
```

---

## Transfer

### Aufgabe 13 – Weitere mögliche Services diskutieren

Diskutiere, ob diese Klassen sinnvoll wären.

| Idee | Sinnvoll? | Begründung |
|---|---|---|
| `PreisService` | | |
| `BestellService` | | |
| `CsvService` | | |
| `AusgabeService` | | |

Hinweis:

```text
Ein neuer Service ist nur sinnvoll, wenn er eine klare fachliche Aufgabe bündelt.
```

---

### Aufgabe 14 – Ungeeignete Verantwortlichkeiten erkennen

Ordne die folgenden Methoden einer passenden Klasse zu oder markiere sie als problematisch.

| Methode | Passende Klasse | Warum? |
|---|---|---|
| `verkaufen(Produkt produkt, int menge)` | | |
| `speichern(ArrayList<Produkt> produkte, String pfad)` | | |
| `csvZeileErzeugen(Produkt produkt)` | | |
| `zeigeMenue()` | | |
| `warnungPruefen(Produkt produkt, int grenze)` | | |
| `verkaufenUndCsvSchreiben(...)` | | |

---

### Aufgabe 15 – Vorteile kleiner Schichten beschreiben

Beschreibe drei Vorteile der neuen Struktur.

Nutze diese Satzanfänge:

```text
Main wird einfacher, weil ...
Der LagerService ist besser testbar, weil ...
Der ProduktSpeicher bleibt klar, weil ...
```

---

### Aufgabe 16 – Warum Persistenz nicht in `Main` gehört

Beantworte:

1. Was würde passieren, wenn `Main` selbst CSV-Zeilen erzeugt?
2. Was müsste angepasst werden, wenn später anders gespeichert wird?
3. Warum hilft das Interface `ProduktSpeicher`?
4. Welche Aufgabe bleibt trotzdem in `Main`?

---

### Aufgabe 17 – Wann werden zu viele Services problematisch?

Beschreibe ein Beispiel, in dem zu viele kleine Services den Code schlechter machen.

Leitfragen:

1. Muss man zu viele Dateien öffnen, um eine einfache Regel zu verstehen?
2. Haben die Services klare Namen?
3. Enthält jeder Service wirklich zusammengehörige Fachlogik?
4. Wäre eine einfache Methode in `LagerService` verständlicher?

---

## Typische Fehler prüfen

Prüfe deinen Code bewusst auf diese Fehler:

| Prüfung | Erfüllt? |
|---|---|
| Fachlogik ist nicht mehr breit in `Main` verteilt | |
| `LagerService` enthält keine CSV-Dateilogik | |
| `CsvProduktSpeicher` enthält keine Verkaufsregeln | |
| `Produkt` bleibt eine überschaubare Datenklasse | |
| Es wurden nicht unnötig viele Services erzeugt | |
| `Main` zeigt weiterhin den Ablauf | |
| Verhalten wurde nach dem Refactoring geprüft | |
| Service-Methoden haben kleine Tests oder klare Prüfungen | |

---

## Reflexion

Beantworte zum Schluss:

1. Welche Logik gehört in den `LagerService`?
2. Welche Verantwortung bleibt bei `ProduktSpeicher`?
3. Warum wird `Main` einfacher?
4. Welche Vorteile bringt die Trennung?
5. Wann wäre die Struktur zu komplex?
