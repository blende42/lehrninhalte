# Repetition Java Intro – Lehrpersonen-Version

Lernenden-Version: [Repetition_Java_Intro.md](../Lernende/Repetition_Java_Intro.md)

Diese Lehrpersonen-Version enthält denselben Aufgabenkern wie die Lernenden-Version und ergänzt didaktische Hinweise, Diagnosehinweise, Zeitangaben, Beobachtungspunkte und mögliche Hilfestellungen.

## Didaktische Einordnung

Diese Repetition kombiniert bekannte Konzepte aus Methoden, Klassen und Objekten, Kapselung und `ArrayList`. Sie führt keine neuen Konzepte ein. Die Aufgaben sind bewusst klein gehalten, damit sichtbar wird, ob die Grundlagen wirklich verinnerlicht wurden.

Zentrale Diagnosefrage: Können Lernende eine kleine Produktverwaltung strukturieren, ohne alle Logik in `main` zu schreiben?

## Grobe Zeitplanung

| Abschnitt | Zeit |
| --- | --- |
| Einstieg und Auftrag klären | 5-10 Minuten |
| Pflichtteil, Aufgaben 1-10 | 45-60 Minuten |
| Vertiefung, Aufgaben 11-13 | 25-35 Minuten |
| Optional / Transfer, Aufgaben 14-15 | 15-25 Minuten |
| Reflexion und kurze Besprechung | 10-15 Minuten |

Die Repetition kann in einer längeren Lektion oder verteilt auf zwei kürzere Sequenzen eingesetzt werden.

## Aufgabenkern

### Vorgaben

- Arbeite mit der bekannten Domäne `Produktverwaltung`.
- Verwende eine Klasse `Produkt`.
- Verwende `private` Attribute, Getter und einen geprüften Setter für den Preis.
- Verwende `ArrayList<Produkt>`.
- Schreibe kleine Methoden mit klaren Parametern und Rückgabewerten.
- Halte `main` übersichtlich. Dort sollen keine Berechnungsschleifen stehen.

### Startdaten

Verwende diese Produkte für deine Tests:

```text
Tastatur, 49.90
Monitor, 179.00
Maus, 24.50
Webcam, 79.00
```

## Pflichtteil

### Aufgabe 1 – Klasse anlegen

Erstelle eine Klasse `Produkt`.

Vorgaben:

- `private String name`
- `private double preis`
- Konstruktor mit `name` und `preis`

---

### Aufgabe 2 – Getter ergänzen

Ergänze die Getter:

- `getName()`
- `getPreis()`

Teste in `main`, ob beide Werte gelesen und ausgegeben werden können.

---

### Aufgabe 3 – Preis kontrolliert ändern

Ergänze einen Setter `setPreis`.

Vorgaben:

- Der Preis darf nur geändert werden, wenn er `>= 0` ist.
- Ein negativer Preis darf den bestehenden Preis nicht überschreiben.

Teste:

- Preis von `49.90` auf `59.90` ändern
- Preis danach mit `-10.0` ändern
- Erwartung: Der Preis bleibt `59.90`

---

### Aufgabe 4 – Produkt ausgeben

Schreibe in `Produkt` eine Methode `ausgeben`.

Erwartete Ausgabe für die Tastatur:

```text
Tastatur: 49.9
```

---

### Aufgabe 5 – Produktliste erstellen

Erstelle in `main` eine `ArrayList<Produkt>` und füge die vier Startprodukte hinzu.

Vorgaben:

- Verwende `java.util.ArrayList`.
- Verwende `add`.
- Greife nicht direkt auf Attribute zu.

---

### Aufgabe 6 – Alle Produkte ausgeben

Schreibe eine Methode `gibAlleAus`.

Vorgaben:

- Parameter: `ArrayList<Produkt> produkte`
- Rückgabewert: keiner
- Verwende eine Schleife über die Liste.
- Rufe pro Produkt `ausgeben()` auf.

---

### Aufgabe 7 – Gesamtwert berechnen

Schreibe eine Methode `berechneGesamtwert`.

Vorgaben:

- Parameter: `ArrayList<Produkt> produkte`
- Rückgabewert: `double`
- Verwende `getPreis()`.

Erwartetes Resultat mit den Startdaten: `332.4`

---

### Aufgabe 8 – Teure Produkte zählen

Schreibe eine Methode `zaehleTeureProdukte`.

Vorgaben:

- Parameter: `ArrayList<Produkt> produkte`
- Rückgabewert: `int`
- Teuer bedeutet: Preis mindestens `100.0`.

Erwartetes Resultat mit den Startdaten: `1`

---

### Aufgabe 9 – Produkt suchen

Schreibe eine Methode `findeProdukt`.

Vorgaben:

- Parameter: `ArrayList<Produkt> produkte`, `String name`
- Rückgabewert: `Produkt`
- Wenn kein Produkt gefunden wird, gib `null` zurück.
- Prüfe in `main`, ob das Resultat `null` ist, bevor du es ausgibst.

Teste:

- Suche nach `Monitor`
- Suche nach `Drucker`

---

### Aufgabe 10 – Teuerstes Produkt finden

Schreibe eine Methode `findeTeuerstesProdukt`.

Vorgaben:

- Parameter: `ArrayList<Produkt> produkte`
- Rückgabewert: `Produkt`
- Wenn die Liste leer ist, gib `null` zurück.
- Verwende `getPreis()`.

Erwartung mit den Startdaten: `Monitor`

## Vertiefung

### Aufgabe 11 – Preis eines Produkts ändern

Schreibe eine Methode `aenderePreis`.

Vorgaben:

- Parameter: `ArrayList<Produkt> produkte`, `String name`, `double neuerPreis`
- Rückgabewert: `boolean`
- Suche das Produkt über den Namen.
- Verwende `setPreis(neuerPreis)`.
- Gib `true` zurück, wenn ein Produkt mit diesem Namen gefunden wurde.
- Gib `false` zurück, wenn kein Produkt gefunden wurde.

Teste:

- `aenderePreis(produkte, "Maus", 29.90)` ergibt `true`
- `aenderePreis(produkte, "Drucker", 99.00)` ergibt `false`

---

### Aufgabe 12 – Produkt entfernen

Schreibe eine Methode `entferneProdukt`.

Vorgaben:

- Parameter: `ArrayList<Produkt> produkte`, `String name`
- Rückgabewert: `boolean`
- Entferne das erste Produkt mit passendem Namen.
- Gib nach dem Entfernen direkt `true` zurück.
- Gib `false` zurück, wenn nichts gefunden wurde.

Teste:

- Entferne `Webcam`
- Gib danach alle Produkte aus.

---

### Aufgabe 13 – Leere Liste prüfen

Teste deine Methoden mit einer leeren `ArrayList<Produkt>`.

Prüfe:

- `berechneGesamtwert` ergibt `0.0`
- `zaehleTeureProdukte` ergibt `0`
- `findeProdukt` ergibt `null`
- `findeTeuerstesProdukt` ergibt `null`

## Optional / Transfer

### Aufgabe 14 – Alle Preise erhöhen

Schreibe eine Methode `erhoeheAllePreise`.

Vorgaben:

- Parameter: `ArrayList<Produkt> produkte`, `double betrag`
- Rückgabewert: keiner
- Ein negativer Betrag soll nichts ändern.
- Verwende `getPreis()` und `setPreis(...)`.

Hinweis: Diese Aufgabe ist optional und zählt nicht zum Pflichtteil.

---

### Aufgabe 15 – Produkte bis Preisgrenze zählen

Schreibe eine Methode `zaehleBisPreis`.

Vorgaben:

- Parameter: `ArrayList<Produkt> produkte`, `double grenze`
- Rückgabewert: `int`
- Zähle alle Produkte, deren Preis höchstens `grenze` ist.

Teste mit der Grenze `80.0`.

Hinweis: Diese Aufgabe ist optional und zählt nicht zum Pflichtteil.

## Reflexion

- Welche Logik steht noch in `main`?
- Welche Methoden haben einen Rückgabewert?
- Wo verwendest du Getter statt direktem Attributzugriff?
- Wo schützt `setPreis` den Objektzustand?
- Welche Methode war am einfachsten zu testen?
- Bei welcher Methode war `null` wichtig?

## Diagnosehinweise

Diese Repetition eignet sich zur Beobachtung während der Bearbeitung. Nicht nur das Endresultat ist wichtig.

| Aufgabe | Geprüftes Konzept | Beobachtungspunkt | Möglicher Anschluss |
| --- | --- | --- | --- |
| 1-2 | Klasse, Attribute, Getter | Werden Klasse und Objekt unterschieden? | Klassenaufbau nochmals visualisieren |
| 3-4 | Kapselung, Setter, Objektlogik | Wird der Objektzustand kontrolliert geändert? | Setter-Regeln mit ungültigen Werten üben |
| 5-6 | `ArrayList`, Schleifen | Wird die Liste korrekt gefüllt und durchlaufen? | `add`, `size`, `get` wiederholen |
| 7-8 | Methoden mit Rückgabewert | Werden Berechnungen aus `main` ausgelagert? | Methoden mit klaren Rückgabewerten üben |
| 9-10 | Suche, `null`, Vergleich | Wird ein nicht gefundenes Produkt sauber behandelt? | `null`-Prüfung und `equals` wiederholen |
| 11-12 | Kombination von Suche und Änderung | Wird bekannte Logik kombiniert statt neu erfunden? | Kleine Methodenketten besprechen |
| 13 | Edge Cases | Werden leere Listen bewusst geprüft? | Edge Cases vor dem Programmieren sammeln |
| 14-15 | Optionaler Transfer | Können bekannte Muster in einen leicht anderen Kontext übertragen werden? | Stärkere Lernende erklären ihr Vorgehen |

## Typische Beobachtungspunkte

- Wird weiterhin alles in `main` geschrieben?
- Werden Methoden mit Rückgabewerten sinnvoll verwendet?
- Werden `ArrayList`, Schleifen und Getter korrekt eingesetzt?
- Werden Klassen, Getter/Setter und Objektlogik verstanden?
- Werden Edge Cases wie leere Listen erkannt?
- Wird `null` nach einer Suche sauber geprüft?
- Wird Kapselung eingehalten oder direkt auf Attribute zugegriffen?

## Mögliche Hilfestellungen

- Bei Aufgaben 1-4: Klassengerüst gemeinsam an der Tafel sammeln.
- Bei Aufgaben 5-6: An `add`, `size()` und `get(i)` aus der ArrayList-Einheit erinnern.
- Bei Aufgaben 7-8: Rückgabewert zuerst sprachlich formulieren lassen.
- Bei Aufgaben 9-10: Den Fall „nicht gefunden“ vor dem Code besprechen.
- Bei Aufgaben 11-12: Suche und Änderung als zwei kleine Schritte markieren.
- Bei Aufgabe 13: Leere Liste zuerst mit erwarteten Resultaten notieren lassen.
- Bei Transferaufgaben: Nur Hinweise auf bestehende Muster geben, keine neue Lösungstechnik einführen.

## Erwartbare Schwierigkeiten

- Lernende schreiben Berechnungsschleifen direkt in `main`.
- `private` wird gesetzt, danach fehlen Getter oder Setter.
- Der Setter überschreibt den Preis auch bei negativen Werten.
- `findeProdukt` gibt kein `null` zurück oder `null` wird ungeprüft verwendet.
- Beim Entfernen aus der Liste wird nach `remove(i)` weiter iteriert.
- Leere Listen werden nicht getestet.
- Optional-Aufgaben werden als Pflicht missverstanden; vorab klar abgrenzen.
