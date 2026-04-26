# Übungen – Methoden festigen und Refactoring

## Basis

### Aufgabe 1 – Methoden erkennen

Gegeben ist folgender Code:

```java
int[] werte = {4, 7, 2, 9};

int summe = 0;
for (int i = 0; i < werte.length; i++) {
    summe += werte[i];
}

System.out.println(summe);
```

Beantworte:

- Welche Aufgabe erfüllt die Schleife?
- Welcher Methodenname passt?
- Welche Parameter braucht die Methode?
- Welchen Rückgabewert braucht die Methode?

---

### Aufgabe 2 – Methode auslagern

Lagere die Berechnung aus Aufgabe 1 in eine Methode `summe` aus.

Erwartetes Resultat:

```text
22
```

---

### Aufgabe 3 – Testausgaben schreiben

Teste deine Methode `summe` mit diesen Daten:

```java
int[] a = {1, 2, 3};
int[] b = {10, -5, 2};
int[] c = {};
```

Erwartete Resultate:

- `a` ergibt `6`
- `b` ergibt `7`
- `c` ergibt `0`

---

## Aufbau

### Aufgabe 4 – Punkte auswerten

Gegeben ist folgender Code:

```java
int[] punkte = {8, 12, 7, 15, 10};

int bestanden = 0;
for (int i = 0; i < punkte.length; i++) {
    if (punkte[i] >= 10) {
        bestanden++;
    }
}

System.out.println(bestanden);
```

Lagere die Berechnung in eine Methode `zaehleBestanden` aus.

Vorgaben:

- Parameter: `int[] punkte`
- Rückgabewert: `int`
- Grenze für bestanden: `10`

Erwartetes Resultat: `3`

---

### Aufgabe 5 – Grenze als Parameter

Erweitere Aufgabe 4.

Schreibe eine Methode `zaehleMindestens`.

Vorgaben:

- Parameter: `int[] werte`, `int grenze`
- Rückgabewert: `int`
- Die Grenze wird nicht mehr fest in der Methode geschrieben.

Beispiele:

- `zaehleMindestens(punkte, 10)` ergibt `3`
- `zaehleMindestens(punkte, 12)` ergibt `2`

---

### Aufgabe 6 – String bereinigen

Schreibe eine Methode `normalisiere`.

Vorgaben:

- Parameter: `String text`
- Rückgabewert: `String`
- Die Methode entfernt Leerzeichen am Anfang und Ende.
- Die Methode wandelt den Text in Kleinbuchstaben um.

Beispiel:

```java
normalisiere("  Java Lernen  ")
```

Erwartetes Resultat:

```text
java lernen
```

---

## Vertiefung

### Aufgabe 7 – String prüfen

Schreibe eine Methode `enthaeltWort`.

Vorgaben:

- Parameter: `String text`, `String wort`
- Rückgabewert: `boolean`
- Gross- und Kleinschreibung soll keine Rolle spielen.
- Leerzeichen am Anfang und Ende sollen keine Rolle spielen.

Beispiele:

- `enthaeltWort("  Ich lerne Java  ", "java")` ergibt `true`
- `enthaeltWort("  Ich lerne Java  ", "python")` ergibt `false`

---

### Aufgabe 8 – Refactoring einer Textauswertung

Baue den folgenden Code in Methoden um.

```java
String input = "  Java ist toll  ";

String text = input.trim().toLowerCase();
boolean gueltig = !text.isEmpty();
boolean enthaeltJava = text.contains("java");

System.out.println("Text: " + text);
System.out.println("Gueltig: " + gueltig);
System.out.println("Enthaelt Java: " + enthaeltJava);
```

Vorgaben:

- Verwende `normalisiere`.
- Schreibe eine Methode `istGueltig`.
- Verwende `enthaeltWort`.

---

### Aufgabe 9 – 2D-Array refaktorieren

Gegeben ist folgender Code:

```java
int[][] messwerte = {
    {12, 15, 18},
    {21, 19, 14},
    {16, 17, 20}
};

for (int i = 0; i < messwerte.length; i++) {
    int summe = 0;
    for (int j = 0; j < messwerte[i].length; j++) {
        summe += messwerte[i][j];
    }
    System.out.println(summe);
}
```

Lagere die Berechnung einer Zeilensumme in eine Methode `zeilensumme` aus.

Erwartete Ausgaben:

```text
45
54
53
```

---

## Transfer

### Aufgabe 10 – Kleine Auswertung strukturieren

Schreibe ein kleines Programm mit diesen Daten:

```java
String[] namen = {"Lea", "Noah", "Mia", "Tim"};
int[] punkte = {14, 9, 16, 10};
```

Das Programm soll ausgeben:

- alle Namen mit Punkten
- die höchste Punktzahl
- wie viele Lernende bestanden haben

Vorgaben:

- Schreibe eine Methode `ausgeben`.
- Schreibe eine Methode `maximum`.
- Schreibe eine Methode `zaehleMindestens`.
- In `main` sollen keine Berechnungsschleifen stehen.

---

## Reflexion

- Welche Methode hat nur berechnet?
- Welche Methode hat nur ausgegeben?
- Welche Methode war am besten wiederverwendbar?
- Welche Testausgabe hat dir am meisten geholfen?
