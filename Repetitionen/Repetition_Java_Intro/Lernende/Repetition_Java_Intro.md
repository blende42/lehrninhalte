# Repetition Java Intro

Lehrpersonen-Version: [Repetition_Java_Intro_LP.md](../Lehrperson/Repetition_Java_Intro_LP.md)

Diese Repetition kombiniert bekannte Konzepte aus Methoden, Klassen und Objekten, Kapselung und `ArrayList`. Es werden keine neuen Konzepte eingeführt.

Ziel: Sichtbar machen, ob die bisherigen Grundlagen in einer kleinen Produktverwaltung sicher angewendet werden können.

## Vorgaben

- Arbeite mit der bekannten Domäne `Produktverwaltung`.
- Verwende eine Klasse `Produkt`.
- Verwende `private` Attribute, Getter und einen geprüften Setter für den Preis.
- Verwende `ArrayList<Produkt>`.
- Schreibe kleine Methoden mit klaren Parametern und Rückgabewerten.
- Halte `main` übersichtlich. Dort sollen keine Berechnungsschleifen stehen.

## Startdaten

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

Beantworte kurz:

- Welche Logik steht noch in `main`?
- Welche Methoden haben einen Rückgabewert?
- Wo verwendest du Getter statt direktem Attributzugriff?
- Wo schützt `setPreis` den Objektzustand?
- Welche Methode war am einfachsten zu testen?
- Bei welcher Methode war `null` wichtig?
