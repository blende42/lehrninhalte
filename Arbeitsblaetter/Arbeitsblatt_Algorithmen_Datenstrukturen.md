# Arbeitsblatt – Algorithmen und Datenstrukturen

## Lernziele

- Algorithmus und Datenstruktur unterscheiden
- bekannte Array-Muster als einfache Algorithmen erkennen
- lineare Suche, Minimum, Maximum und Zählen erklären
- einfache Aussagen zum Aufwand eines Algorithmus machen
- Randfälle wie leere Arrays bewusst behandeln

---

## Algorithmus und Datenstruktur

Eine Datenstruktur speichert Daten in einer bestimmten Form.

Beispiele aus den bisherigen Themen:

- `int[]` speichert mehrere ganze Zahlen mit festem Index.
- `Produkt[]` speichert mehrere Objekte mit festem Index.
- `ArrayList<Produkt>` speichert mehrere Objekte dynamisch.

Ein Algorithmus beschreibt, wie Daten Schritt für Schritt verarbeitet werden.

Beispiele:

- das grösste Element suchen
- einen bestimmten Wert finden
- Werte zählen, die eine Bedingung erfüllen
- Werte sortieren

Kurz:

- Datenstruktur: Wo liegen die Daten?
- Algorithmus: Was machen wir mit den Daten?

---

## Beispiel: lineare Suche

Bei der linearen Suche wird ein Array von vorne nach hinten durchlaufen.

```java
public static boolean enthaelt(int[] zahlen, int gesucht) {
    for (int i = 0; i < zahlen.length; i++) {
        if (zahlen[i] == gesucht) {
            return true;
        }
    }

    return false;
}
```

Die Methode endet sofort, wenn der Wert gefunden wurde.

Mögliche Fälle:

- Der Wert steht ganz vorne: wenige Vergleiche.
- Der Wert steht ganz hinten: viele Vergleiche.
- Der Wert kommt nicht vor: alle Elemente müssen geprüft werden.

---

## Beispiel: Minimum finden

Um den kleinsten Wert zu finden, wird zuerst ein Startwert gewählt.

```java
public static int findeMinimum(int[] zahlen) {
    int minimum = zahlen[0];

    for (int i = 1; i < zahlen.length; i++) {
        if (zahlen[i] < minimum) {
            minimum = zahlen[i];
        }
    }

    return minimum;
}
```

Wichtig: Diese Methode funktioniert nur, wenn das Array mindestens ein Element enthält.

Für leere Arrays braucht es eine bewusste Entscheidung, zum Beispiel:

```java
public static Integer findeMinimumOderNull(int[] zahlen) {
    if (zahlen.length == 0) {
        return null;
    }

    int minimum = zahlen[0];

    for (int i = 1; i < zahlen.length; i++) {
        if (zahlen[i] < minimum) {
            minimum = zahlen[i];
        }
    }

    return minimum;
}
```

Hier wird `Integer` verwendet, weil `null` nur bei Objekten möglich ist.

---

## Beispiel: zählen

Wie viele Werte sind mindestens `100`?

```java
public static int zaehleGrosseWerte(int[] zahlen) {
    int anzahl = 0;

    for (int i = 0; i < zahlen.length; i++) {
        if (zahlen[i] >= 100) {
            anzahl++;
        }
    }

    return anzahl;
}
```

Das Muster ist bekannt:

- Zählvariable starten
- alle Elemente durchlaufen
- bei passender Bedingung erhöhen
- Zählwert zurückgeben

---

## Beispiel: wiederholte Berechnung

Manche Algorithmen wenden dieselbe Formel mehrfach an.

Beispiel: Kapital mit Jahreszins.

```java
public static double berechneKapital(double startkapital, double zinssatz, int jahre) {
    double kapital = startkapital;

    for (int jahr = 1; jahr <= jahre; jahr++) {
        double zins = kapital * zinssatz / 100;
        kapital = kapital + zins;
    }

    return kapital;
}
```

Hier wird keine spezielle Zinseszinsformel verwendet. Der Zinseszins entsteht dadurch, dass die normale Zinsformel jedes Jahr erneut auf das aktuelle Kapital angewendet wird.

Bei Simulationen kann sich der Zinssatz pro Jahr ändern. Dann wird der Zinssatz zum Beispiel aus einem Array gelesen.

```java
double[] zinssaetze = {1.0, 1.5, 2.0};
```

---

## Aufwand einfach betrachtet

Bei vielen Algorithmen ist wichtig, wie viele Elemente geprüft werden müssen.

Beispiel mit `10` Zahlen:

- Lineare Suche, Wert vorne: vielleicht nur `1` Vergleich.
- Lineare Suche, Wert fehlt: `10` Vergleiche.
- Minimum finden: alle `10` Werte müssen geprüft werden.

Für diese Einheit reicht die einfache Frage:

> Muss der Algorithmus alle Elemente anschauen oder kann er früher abbrechen?

---

## Typische Stolpersteine

- Bei leeren Arrays trotzdem `zahlen[0]` verwenden.
- `return` in einer Schleife zu früh setzen.
- Zählvariable nicht vor der Schleife starten.
- Beim Suchen `false` zu früh zurückgeben.
- Minimum oder Maximum mit `0` starten, obwohl auch negative Werte möglich sind.

---

## Reflexion

- Welche Datenstruktur verwendest du in deinen bisherigen Programmen am häufigsten?
- Welche Array-Muster sind eigentlich Algorithmen?
- Wann kann eine Suche früher abbrechen?
- Warum ist ein leeres Array ein wichtiger Randfall?
