# Arbeitsblatt – Sortieralgorithmen

## Lernziele

- Sortieren als wiederholtes Vergleichen und Tauschen erklären
- Bubble Sort Schritt für Schritt nachvollziehen
- Selection Sort Schritt für Schritt nachvollziehen
- Schleifengrenzen bei einfachen Sortieralgorithmen begründen
- typische Fehler beim Tauschen und Sortieren erkennen

---

## Warum zuerst mit `int[]`?

Sortieren ist am Anfang anspruchsvoll genug:

- Werte vergleichen
- Werte tauschen
- verschachtelte Schleifen verstehen
- mehrere Durchläufe verfolgen

Darum wird hier zuerst mit `int[]` gearbeitet.

Später kann dasselbe Prinzip auf Objekte übertragen werden, zum Beispiel auf `Produkt[]` nach Preis.

---

## Tauschen mit Hilfsvariable

Zwei Werte in einem Array werden mit einer Hilfsvariable getauscht.

```java
int temp = zahlen[i];
zahlen[i] = zahlen[j];
zahlen[j] = temp;
```

Ohne Hilfsvariable geht ein Wert verloren.

---

## Bubble Sort

Bubble Sort vergleicht immer zwei benachbarte Werte.

Wenn sie in der falschen Reihenfolge stehen, werden sie getauscht.

```java
public static void bubbleSort(int[] zahlen) {
    for (int durchlauf = 0; durchlauf < zahlen.length - 1; durchlauf++) {
        for (int i = 0; i < zahlen.length - 1 - durchlauf; i++) {
            if (zahlen[i] > zahlen[i + 1]) {
                int temp = zahlen[i];
                zahlen[i] = zahlen[i + 1];
                zahlen[i + 1] = temp;
            }
        }
    }
}
```

Nach jedem äusseren Durchlauf steht der grösste noch unsortierte Wert weiter hinten.

Darum wird die innere Schleife mit `zahlen.length - 1 - durchlauf` kürzer.

---

## Bubble Sort Schritt für Schritt

Start:

```text
[5, 2, 8, 1]
```

Erster Durchlauf:

```text
[2, 5, 8, 1]
[2, 5, 1, 8]
```

Die `8` ist am Ende angekommen.

Zweiter Durchlauf:

```text
[2, 1, 5, 8]
```

Dritter Durchlauf:

```text
[1, 2, 5, 8]
```

---

## Selection Sort

Selection Sort sucht zuerst den kleinsten Wert im noch unsortierten Bereich.

Dieser kleinste Wert wird danach an die richtige Position getauscht.

```java
public static void selectionSort(int[] zahlen) {
    for (int start = 0; start < zahlen.length - 1; start++) {
        int indexMinimum = start;

        for (int i = start + 1; i < zahlen.length; i++) {
            if (zahlen[i] < zahlen[indexMinimum]) {
                indexMinimum = i;
            }
        }

        int temp = zahlen[start];
        zahlen[start] = zahlen[indexMinimum];
        zahlen[indexMinimum] = temp;
    }
}
```

Nach jedem äusseren Durchlauf ist vorne ein weiteres Element fertig sortiert.

---

## Bubble Sort und Selection Sort vergleichen

| Frage | Bubble Sort | Selection Sort |
| --- | --- | --- |
| Was wird gesucht? | benachbarte falsche Reihenfolge | kleinster Wert im Rest |
| Wie wird getauscht? | oft benachbarte Werte | einmal pro Durchlauf |
| Was ist nach einem Durchlauf sicher? | grosser Wert ist weiter hinten | kleinster Restwert ist vorne |
| Gut zum Lernen von | benachbarten Vergleichen | Minimum-Suche und gezieltem Tauschen |

---

## Typische Stolpersteine

- Beim Vergleich `zahlen[i + 1]` verwenden, aber die Schleife zu weit laufen lassen.
- Beim Tauschen die Hilfsvariable vergessen.
- `indexMinimum` nicht bei jedem äusseren Durchlauf neu setzen.
- Nach einem Tausch mit alten Werten weiterdenken.
- Sortieren mit Suche verwechseln: Sortieren verändert die Reihenfolge im Array.

---

## Reflexion

- Warum braucht Bubble Sort zwei Schleifen?
- Warum wird die innere Bubble-Sort-Schleife kürzer?
- Warum merkt sich Selection Sort zuerst den Index des kleinsten Werts?
- Welche Sortieridee kannst du leichter erklären?
