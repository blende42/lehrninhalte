# Übungen – Methoden in Java

## Basis

### Aufgabe 1 – Methode ausführen

Gegeben ist folgende Methode:

```java
public static void begruessen(String name) {
    System.out.println("Hallo " + name);
}
```

Rufe die Methode in `main` dreimal mit verschiedenen Namen auf.

---

### Aufgabe 2 – Rückgabewert verwenden

Schreibe eine Methode `verdoppeln`.

Vorgaben:

- Parameter: `int zahl`
- Rückgabewert: `int`
- Beispiel: `verdoppeln(4)` ergibt `8`

Gib das Ergebnis in `main` aus.

---

### Aufgabe 3 – Boolean zurückgeben

Schreibe eine Methode `istGerade`.

Vorgaben:

- Parameter: `int zahl`
- Rückgabewert: `boolean`
- `4` ergibt `true`
- `7` ergibt `false`

---

## Aufbau

### Aufgabe 4 – Array ausgeben

Schreibe eine Methode `ausgeben`, die alle Werte eines `int[]` ausgibt.

Testdaten:

```java
int[] werte = {4, 7, 2, 9};
```

---

### Aufgabe 5 – Summe als Methode

Schreibe eine Methode `summe`, die die Summe eines `int[]` zurückgibt.

Testdaten:

```java
int[] werte = {4, 7, 2, 9};
```

Erwartetes Resultat: `22`

---

### Aufgabe 6 – Durchschnitt als Methode

Schreibe eine Methode `durchschnitt`, die den Durchschnitt eines `int[]` zurückgibt.

Vorgaben:

- Rückgabewert: `double`
- Bei `{4, 7, 2, 9}` ist das Resultat `5.5`

---

## Vertiefung

### Aufgabe 7 – Maximum

Schreibe eine Methode `maximum`, die den grössten Wert eines Arrays zurückgibt.

Testdaten:

```java
int[] werte = {-4, -7, -2, -9, -1};
```

Erwartetes Resultat: `-1`

---

### Aufgabe 8 – Suche

Schreibe eine Methode `enthaelt`, die prüft, ob ein Wert im Array vorkommt.

Vorgaben:

- Parameter: `int[] werte`, `int gesucht`
- Rückgabewert: `boolean`
- Brich die Schleife ab, sobald der Wert gefunden wurde.

---

### Aufgabe 9 – Anzahl Treffer

Schreibe eine Methode `zaehle`, die zählt, wie oft ein bestimmter Wert vorkommt.

Testdaten:

```java
int[] werte = {4, 7, 7, 2, 7, 1};
```

Für den Suchwert `7` ist das erwartete Resultat `3`.

---

## Transfer

### Aufgabe 10 – 2D-Array: Zeilensumme

Schreibe eine Methode `zeilensumme`, die die Summe einer einzelnen Zeile zurückgibt.

```java
int[][] messwerte = {
    {12, 15, 18},
    {21, 19, 14},
    {16, 17, 20}
};
```

Beispiel: `zeilensumme(messwerte[0])` ergibt `45`.

---

### Aufgabe 11 – 2D-Array: Beste Zeile

Schreibe eine Methode `besteZeile`, die den Index der Zeile mit der höchsten Summe zurückgibt.

Vorgaben:

- Verwende deine Methode `zeilensumme`.
- Bei gleichen Summen darf die erste passende Zeile zurückgegeben werden.
- Das 2D-Array ist nicht leer.

---

## Edge Cases

### Aufgabe 12 – Leeres Array

Passe `summe`, `durchschnitt` und `maximum` bewusst an.

Entscheide:

- Was soll bei einem leeren Array zurückgegeben werden?
- Wo ist `0` sinnvoll?
- Wo kann `0` ein irreführendes Resultat sein?

Halte deine Entscheidung als kurzen Kommentar im Code fest.

---

## Reflexion

- Welche Methoden haben einen Rückgabewert?
- Welche Methoden verändern nichts, sondern berechnen nur ein Ergebnis?
- Wo steht `return` innerhalb oder ausserhalb der Schleife?
- Welche Methode würdest du zuerst testen?
