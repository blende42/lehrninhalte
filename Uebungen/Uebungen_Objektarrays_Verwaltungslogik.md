# Übungen – Objektarrays und Verwaltungslogik

## Basis

### Aufgabe 1 – Produktarray erstellen

Erstelle ein Array mit drei Produkten.

Vorgaben:

- `Tastatur`, Preis `49.90`
- `Monitor`, Preis `179.00`
- `Maus`, Preis `24.50`

Verwende weiterhin normale Arrays, keine `ArrayList`.

---

### Aufgabe 2 – Alle Produkte ausgeben

Schreibe eine Methode `gibAlleAus`.

Vorgaben:

- Parameter: `Produkt[] produkte`
- Rückgabewert: keiner
- Die Methode ruft für jedes Produkt `ausgeben()` auf.

---

### Aufgabe 3 – Gesamtwert berechnen

Schreibe eine Methode `berechneGesamtwert`.

Vorgaben:

- Parameter: `Produkt[] produkte`
- Rückgabewert: `double`
- Addiere alle Preise mit `getPreis()`.

Erwartetes Resultat für die Testdaten: `253.4`

---

## Aufbau

### Aufgabe 4 – Teure Produkte zählen

Schreibe eine Methode `zaehleTeureProdukte`.

Vorgaben:

- Parameter: `Produkt[] produkte`
- Rückgabewert: `int`
- Teuer bedeutet: Preis mindestens `100.0`.

Erwartetes Resultat für die Testdaten: `1`

---

### Aufgabe 5 – Produktname suchen

Schreibe eine Methode `enthaeltProdukt`.

Vorgaben:

- Parameter: `Produkt[] produkte`, `String name`
- Rückgabewert: `boolean`
- Vergleiche Namen mit `equals`.

Beispiele:

- Suche nach `Maus` ergibt `true`
- Suche nach `Drucker` ergibt `false`

---

### Aufgabe 6 – Produkt zurückgeben

Schreibe eine Methode `findeProdukt`.

Vorgaben:

- Parameter: `Produkt[] produkte`, `String name`
- Rückgabewert: `Produkt`
- Wenn nichts gefunden wird, gib `null` zurück.

Teste den Rückgabewert vor dem Ausgeben auf `null`.

---

## Vertiefung

### Aufgabe 7 – Teuerstes Produkt finden

Schreibe eine Methode `findeTeuerstesProdukt`.

Vorgaben:

- Parameter: `Produkt[] produkte`
- Rückgabewert: `Produkt`
- Das Array ist nicht leer.
- Vergleiche mit `getPreis()`.

---

### Aufgabe 8 – Preise erhöhen

Schreibe eine Methode `erhoeheAllePreise`.

Vorgaben:

- Parameter: `Produkt[] produkte`, `double betrag`
- Rückgabewert: keiner
- Erhöhe jeden Preis um den Betrag.
- Verwende `getPreis()` und `setPreis(...)`.
- Wenn der Betrag negativ ist, soll nichts geändert werden.

---

### Aufgabe 9 – Durchschnittspreis

Schreibe eine Methode `berechneDurchschnittspreis`.

Vorgaben:

- Parameter: `Produkt[] produkte`
- Rückgabewert: `double`
- Wenn das Array leer ist, gib `0.0` zurück.

---

## Transfer

### Aufgabe 10 – Kleine Produktverwaltung

Schreibe ein Programm, das diese Verwaltungslogik nutzt:

- alle Produkte ausgeben
- Gesamtwert ausgeben
- Anzahl teurer Produkte ausgeben
- Produkt nach Name suchen
- teuerstes Produkt ausgeben
- alle Preise um `5.0` erhöhen
- Produkte nochmals ausgeben

Vorgaben:

- In `main` sollen keine Berechnungsschleifen stehen.
- Verwende nur normale Arrays.
- Greife nicht direkt auf private Attribute zu.

---

## Reflexion

- Welche Methoden geben ein einzelnes Objekt zurück?
- Welche Methoden geben nur eine Zahl zurück?
- Wo ist `null` ein sinnvolles Ergebnis?
- Welche Methoden verändern die Produkte?
