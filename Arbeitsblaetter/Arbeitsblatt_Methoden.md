# Arbeitsblatt – Methoden in Java

## Lernziele
- Methoden mit Parametern und Rückgabewerten lesen und schreiben
- wiederholten Code in eine Methode auslagern
- Array-Auswertungen mit Methoden klar strukturieren
- typische Fehler bei `return`, Parametern und leeren Arrays erkennen

---

## Theorie kurz

Eine Methode fasst eine klar abgegrenzte Aufgabe zusammen. Sie bekommt bei Bedarf Eingaben über Parameter und liefert bei Bedarf ein Ergebnis mit `return` zurück.

```java
public static int summe(int[] werte) {
    int summe = 0;

    for (int i = 0; i < werte.length; i++) {
        summe += werte[i];
    }

    return summe;
}
```

Diese Methode:

- heisst `summe`
- erwartet ein `int[]` als Parameter
- liefert ein `int` zurück
- verändert das Array nicht

---

## Wichtige Begriffe

### Parameter

Parameter sind Werte, die eine Methode von aussen bekommt.

```java
public static boolean enthaelt(int[] werte, int gesucht) {
    for (int i = 0; i < werte.length; i++) {
        if (werte[i] == gesucht) {
            return true;
        }
    }

    return false;
}
```

`werte` und `gesucht` sind Parameter.

### Rückgabewert

Der Rückgabewert ist das Ergebnis der Methode.

```java
boolean gefunden = enthaelt(zahlen, 7);
```

Die Methode liefert hier `true` oder `false`.

### `void`

Wenn eine Methode nichts zurückliefert, verwendet sie `void`.

```java
public static void ausgeben(int[] werte) {
    for (int i = 0; i < werte.length; i++) {
        System.out.println(werte[i]);
    }
}
```

---

## Beispiel – vorher und nachher

### Ohne Methode

```java
int[] temperaturen = {12, 15, 18, 21, 19, 14};

int summe = 0;
for (int i = 0; i < temperaturen.length; i++) {
    summe += temperaturen[i];
}

System.out.println(summe);
```

### Mit Methode

```java
int[] temperaturen = {12, 15, 18, 21, 19, 14};
System.out.println(summe(temperaturen));
```

Der Vorteil: Die Auswertung kann wiederverwendet und separat getestet werden.

---

## Typische Fehler

### `return` fehlt

```java
public static int maximum(int[] werte) {
    int max = werte[0];
}
```

Die Methode verspricht ein `int`, liefert aber kein Ergebnis zurück.

### `return` steht zu früh

```java
public static int summe(int[] werte) {
    int summe = 0;

    for (int i = 0; i < werte.length; i++) {
        summe += werte[i];
        return summe;
    }

    return summe;
}
```

Diese Methode beendet sich bereits nach dem ersten Wert.

### Leeres Array nicht bedacht

```java
int max = werte[0];
```

Bei einem leeren Array gibt es keinen Index `0`. Die Methode muss vorher prüfen, wie sie damit umgehen soll.

---

## Auftrag 1 – Methode lesen

Lies die Methode und beantworte die Fragen.

```java
public static int zaehleGroesserAls(int[] werte, int grenze) {
    int anzahl = 0;

    for (int i = 0; i < werte.length; i++) {
        if (werte[i] > grenze) {
            anzahl++;
        }
    }

    return anzahl;
}
```

Fragen:

- Was sind die Parameter?
- Welchen Rückgabetyp hat die Methode?
- Was liefert die Methode für `{12, 15, 18, 21}` und Grenze `15`?
- Warum steht `return anzahl;` nach der Schleife?

---

## Auftrag 2 – Methode schreiben

Schreibe eine Methode `minimum`, die den kleinsten Wert in einem Array findet.

Vorgaben:

- Rückgabetyp: `int`
- Parameter: `int[] werte`
- Annahme: Das Array ist nicht leer

---

## Auftrag 3 – Methode verbessern

Passe deine Methode so an, dass sie ein leeres Array erkennt.

Mögliche Variante:

- Wenn das Array leer ist, gib `0` zurück.
- Dokumentiere im Code kurz, warum dieser Rückgabewert verwendet wird.

---

## Auftrag 4 – Refactoring

Lagere folgende Berechnungen je in eine eigene Methode aus:

- Summe berechnen
- Durchschnitt berechnen
- Maximum finden
- Prüfen, ob ein Wert vorkommt

Verwende danach in `main` nur noch Methodenaufrufe.

---

## Reflexion

- Wann ist eine eigene Methode sinnvoll?
- Was ist der Unterschied zwischen Parameter und Rückgabewert?
- Welche Fehler passieren besonders schnell bei `return`?
- Wie helfen Methoden beim Testen von Array-Auswertungen?
