# Übungen – ArrayList

## Basis

### Aufgabe 1 – ArrayList erstellen

Erstelle eine `ArrayList<Produkt>`.

Vorgaben:

- Importiere `java.util.ArrayList`.
- Füge drei Produkte hinzu:
  - `Tastatur`, Preis `49.90`
  - `Monitor`, Preis `179.00`
  - `Maus`, Preis `24.50`

---

### Aufgabe 2 – Alle Produkte ausgeben

Schreibe eine Methode `gibAlleAus`.

Vorgaben:

- Parameter: `ArrayList<Produkt> produkte`
- Rückgabewert: keiner
- Verwende `size()` und `get(i)`.

---

### Aufgabe 3 – Gesamtwert berechnen

Schreibe eine Methode `berechneGesamtwert`.

Vorgaben:

- Parameter: `ArrayList<Produkt> produkte`
- Rückgabewert: `double`
- Addiere alle Preise mit `getPreis()`.

Erwartetes Resultat für die Testdaten: `253.4`

---

## Aufbau

### Aufgabe 4 – Produkt hinzufügen

Füge nachträglich ein weiteres Produkt hinzu:

- `Webcam`, Preis `79.00`

Gib danach alle Produkte aus.

---

### Aufgabe 5 – Produkt suchen

Schreibe eine Methode `findeProdukt`.

Vorgaben:

- Parameter: `ArrayList<Produkt> produkte`, `String name`
- Rückgabewert: `Produkt`
- Wenn nichts gefunden wird, gib `null` zurück.
- Prüfe den Rückgabewert vor dem Ausgeben auf `null`.

---

### Aufgabe 6 – Teure Produkte zählen

Schreibe eine Methode `zaehleTeureProdukte`.

Vorgaben:

- Teuer bedeutet: Preis mindestens `100.0`.
- Verwende `getPreis()`.

---

## Vertiefung

### Aufgabe 7 – Teuerstes Produkt finden

Schreibe eine Methode `findeTeuerstesProdukt`.

Vorgaben:

- Parameter: `ArrayList<Produkt> produkte`
- Rückgabewert: `Produkt`
- Wenn die Liste leer ist, gib `null` zurück.

---

### Aufgabe 8 – Produkt entfernen

Schreibe eine Methode `entferneProdukt`.

Vorgaben:

- Parameter: `ArrayList<Produkt> produkte`, `String name`
- Rückgabewert: `boolean`
- Entferne das erste Produkt mit passendem Namen.
- `true`, wenn etwas entfernt wurde
- `false`, wenn nichts gefunden wurde

Hinweis: Nach `remove(i)` soll die Methode direkt beendet werden.

---

### Aufgabe 9 – Preise erhöhen

Schreibe eine Methode `erhoeheAllePreise`.

Vorgaben:

- Parameter: `ArrayList<Produkt> produkte`, `double betrag`
- Wenn der Betrag negativ ist, soll nichts geändert werden.
- Verwende `getPreis()` und `setPreis(...)`.

---

## Transfer

### Aufgabe 10 – Kleine Verwaltung mit ArrayList

Schreibe ein Programm mit folgender Logik:

- Liste erstellen
- Produkte hinzufügen
- alle Produkte ausgeben
- Gesamtwert ausgeben
- teuerstes Produkt ausgeben
- Produkt nach Name suchen
- Produkt entfernen
- alle Produkte nochmals ausgeben

Vorgaben:

- Verwende `ArrayList`, kein normales Array.
- In `main` sollen keine Berechnungsschleifen stehen.
- Greife nicht direkt auf private Attribute zu.

---

## Reflexion

- Was ist bei `ArrayList` einfacher als bei Arrays?
- Welche Schreibweisen haben sich geändert?
- Wo kann `null` zurückgegeben werden?
- Was passiert mit den Indizes nach `remove`?
