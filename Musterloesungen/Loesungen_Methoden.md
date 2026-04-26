# Lösungen – Methoden in Java

## Aufgabe 1 – Methode ausführen

```java
public static void begruessen(String name) {
    System.out.println("Hallo " + name);
}

public static void main(String[] args) {
    begruessen("Lea");
    begruessen("Noah");
    begruessen("Mia");
}
```

## Aufgabe 2 – Rückgabewert verwenden

```java
public static int verdoppeln(int zahl) {
    return zahl * 2;
}
```

## Aufgabe 3 – Boolean zurückgeben

```java
public static boolean istGerade(int zahl) {
    return zahl % 2 == 0;
}
```

## Aufgabe 4 – Array ausgeben

```java
public static void ausgeben(int[] werte) {
    for (int i = 0; i < werte.length; i++) {
        System.out.println(werte[i]);
    }
}
```

## Aufgabe 5 – Summe als Methode

```java
public static int summe(int[] werte) {
    int summe = 0;

    for (int i = 0; i < werte.length; i++) {
        summe += werte[i];
    }

    return summe;
}
```

## Aufgabe 6 – Durchschnitt als Methode

```java
public static double durchschnitt(int[] werte) {
    int summe = 0;

    for (int i = 0; i < werte.length; i++) {
        summe += werte[i];
    }

    return (double) summe / werte.length;
}
```

## Aufgabe 7 – Maximum

```java
public static int maximum(int[] werte) {
    int max = werte[0];

    for (int i = 1; i < werte.length; i++) {
        if (werte[i] > max) {
            max = werte[i];
        }
    }

    return max;
}
```

## Aufgabe 8 – Suche

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

## Aufgabe 9 – Anzahl Treffer

```java
public static int zaehle(int[] werte, int gesucht) {
    int anzahl = 0;

    for (int i = 0; i < werte.length; i++) {
        if (werte[i] == gesucht) {
            anzahl++;
        }
    }

    return anzahl;
}
```

## Aufgabe 10 – 2D-Array: Zeilensumme

```java
public static int zeilensumme(int[] zeile) {
    int summe = 0;

    for (int i = 0; i < zeile.length; i++) {
        summe += zeile[i];
    }

    return summe;
}
```

## Aufgabe 11 – 2D-Array: Beste Zeile

```java
public static int besteZeile(int[][] werte) {
    int besterIndex = 0;
    int besteSumme = zeilensumme(werte[0]);

    for (int i = 1; i < werte.length; i++) {
        int aktuelleSumme = zeilensumme(werte[i]);

        if (aktuelleSumme > besteSumme) {
            besteSumme = aktuelleSumme;
            besterIndex = i;
        }
    }

    return besterIndex;
}
```

## Aufgabe 12 – Leeres Array

Eine mögliche einfache Variante:

```java
public static int summe(int[] werte) {
    int summe = 0;

    for (int i = 0; i < werte.length; i++) {
        summe += werte[i];
    }

    return summe;
}

public static double durchschnitt(int[] werte) {
    if (werte.length == 0) {
        return 0.0; // Vereinbarung: Kein Wert ergibt Durchschnitt 0.0.
    }

    return (double) summe(werte) / werte.length;
}

public static int maximum(int[] werte) {
    if (werte.length == 0) {
        return 0; // Einfache Unterrichtsvariante; fachlich muss diese Vereinbarung bekannt sein.
    }

    int max = werte[0];

    for (int i = 1; i < werte.length; i++) {
        if (werte[i] > max) {
            max = werte[i];
        }
    }

    return max;
}
```

Hinweis: Bei `maximum` kann `0` irreführend sein, wenn alle echten Werte negativ wären. In späteren Themen kann dafür eine Fehlermeldung oder eine andere Rückgabeform verwendet werden.
