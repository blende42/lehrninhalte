# Lösungen – Methoden festigen und Refactoring

## Aufgabe 1 – Methoden erkennen

Mögliche Antworten:

- Die Schleife berechnet die Summe aller Werte.
- Passender Methodenname: `summe`
- Parameter: `int[] werte`
- Rückgabewert: `int`

## Aufgabe 2 – Methode auslagern

```java
public static int summe(int[] werte) {
    int summe = 0;

    for (int i = 0; i < werte.length; i++) {
        summe += werte[i];
    }

    return summe;
}
```

## Aufgabe 3 – Testausgaben schreiben

```java
System.out.println(summe(new int[]{1, 2, 3}));    // erwartet: 6
System.out.println(summe(new int[]{10, -5, 2}));  // erwartet: 7
System.out.println(summe(new int[]{}));           // erwartet: 0
```

## Aufgabe 4 – Punkte auswerten

```java
public static int zaehleBestanden(int[] punkte) {
    int bestanden = 0;

    for (int i = 0; i < punkte.length; i++) {
        if (punkte[i] >= 10) {
            bestanden++;
        }
    }

    return bestanden;
}
```

## Aufgabe 5 – Grenze als Parameter

```java
public static int zaehleMindestens(int[] werte, int grenze) {
    int anzahl = 0;

    for (int i = 0; i < werte.length; i++) {
        if (werte[i] >= grenze) {
            anzahl++;
        }
    }

    return anzahl;
}
```

## Aufgabe 6 – String bereinigen

```java
public static String normalisiere(String text) {
    return text.trim().toLowerCase();
}
```

## Aufgabe 7 – String prüfen

```java
public static boolean enthaeltWort(String text, String wort) {
    String normalisierterText = normalisiere(text);
    String normalisiertesWort = normalisiere(wort);

    return normalisierterText.contains(normalisiertesWort);
}
```

## Aufgabe 8 – Refactoring einer Textauswertung

```java
public static boolean istGueltig(String text) {
    return !normalisiere(text).isEmpty();
}

public static void main(String[] args) {
    String input = "  Java ist toll  ";

    String text = normalisiere(input);
    boolean gueltig = istGueltig(input);
    boolean enthaeltJava = enthaeltWort(input, "java");

    System.out.println("Text: " + text);
    System.out.println("Gueltig: " + gueltig);
    System.out.println("Enthaelt Java: " + enthaeltJava);
}
```

Hinweis: Die Methode `istGueltig` nutzt ebenfalls `normalisiere`, damit Eingaben mit nur Leerzeichen als ungültig erkannt werden.

## Aufgabe 9 – 2D-Array refaktorieren

```java
public static int zeilensumme(int[] zeile) {
    int summe = 0;

    for (int i = 0; i < zeile.length; i++) {
        summe += zeile[i];
    }

    return summe;
}

public static void main(String[] args) {
    int[][] messwerte = {
        {12, 15, 18},
        {21, 19, 14},
        {16, 17, 20}
    };

    for (int i = 0; i < messwerte.length; i++) {
        System.out.println(zeilensumme(messwerte[i]));
    }
}
```

## Aufgabe 10 – Kleine Auswertung strukturieren

```java
public static void ausgeben(String[] namen, int[] punkte) {
    for (int i = 0; i < namen.length; i++) {
        System.out.println(namen[i] + ": " + punkte[i]);
    }
}

public static int maximum(int[] werte) {
    int max = werte[0];

    for (int i = 1; i < werte.length; i++) {
        if (werte[i] > max) {
            max = werte[i];
        }
    }

    return max;
}

public static int zaehleMindestens(int[] werte, int grenze) {
    int anzahl = 0;

    for (int i = 0; i < werte.length; i++) {
        if (werte[i] >= grenze) {
            anzahl++;
        }
    }

    return anzahl;
}

public static void main(String[] args) {
    String[] namen = {"Lea", "Noah", "Mia", "Tim"};
    int[] punkte = {14, 9, 16, 10};

    ausgeben(namen, punkte);
    System.out.println("Maximum: " + maximum(punkte));
    System.out.println("Bestanden: " + zaehleMindestens(punkte, 10));
}
```

Hinweis: Die Methode `ausgeben` gibt direkt auf die Konsole aus. Die Methoden `maximum` und `zaehleMindestens` berechnen nur ein Ergebnis und sind dadurch einfacher testbar.
