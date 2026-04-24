# Arbeitsblatt – Arrays (2D, Vertiefung)

## Lernziele
- 2D-Arrays als „Array von Arrays“ verstehen
- mit zwei Indizes arbeiten
- verschachtelte Schleifen einsetzen
- Messwerte strukturiert auswerten
- Edge Cases korrekt behandeln

---

## Theorie (kurz)

Ein 2D-Array besteht aus mehreren 1D-Arrays.

- messwerte[i] → eine Messreihe  
- messwerte[i][j] → ein konkreter Messwert  

Zugriff erfolgt über zwei Indizes.

---

## Beispiel

```java
int[][] messwerte = {
    {12, 15, 18},
    {21, 19, 14},
    {16, 17, 20}
};
```

---

## Aufgabe 1 – Verstehen

- Was ist messwerte[0]?
- Was ist messwerte[1][2]?
- Wie viele Zeilen gibt es?
- Wie viele Werte hat die erste Zeile?

---

## Aufgabe 2 – Ausgabe

Gib alle Messwerte aus.

Hinweis:
- Du brauchst zwei Schleifen

---

## Aufgabe 3 – Summe pro Zeile

Berechne die Summe jeder Messreihe.

---

## Aufgabe 4 – Durchschnitt pro Zeile

Berechne den Durchschnitt jeder Messreihe.

---

## Aufgabe 5 – Gesamtmaximum

Finde den grössten Wert im gesamten Array.

---

## Aufgabe 6 – Gesamt-Durchschnitt

Berechne den Durchschnitt aller Werte.

---

## Aufgabe 7 – Anspruchsvoll (E)

Finde die Messreihe mit dem höchsten Durchschnitt.

Hinweis:
- Vergleiche die Durchschnitte
- Speichere den Index der besten Reihe

---

## Aufgabe 8 – Edge Case: unterschiedliche Längen

```java
int[][] messwerte = {
    {12, 15},
    {21, 19, 14},
    {16}
};
```

- Gib alle Werte aus
- Funktioniert deine Schleife noch?

---

## Aufgabe 9 – Edge Case: leere Zeile

```java
int[][] messwerte = {
    {12, 15},
    {},
    {16, 17}
};
```

- Was passiert bei der Berechnung?
- Wie kannst du Fehler vermeiden?

---

## Reflexion

- Was ist der Unterschied zu 1D-Arrays?
- Warum brauchst du zwei Schleifen?
- Wo passieren typische Fehler?
- Was musst du bei Edge Cases beachten?
