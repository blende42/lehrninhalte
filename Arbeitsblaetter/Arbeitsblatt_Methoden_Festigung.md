# Arbeitsblatt – Methoden festigen und Refactoring

## Lernziele

- bestehenden Code in sinnvolle Methoden aufteilen
- Methoden gezielt benennen
- Parameter und Rückgabewerte passend wählen
- einfache Tests mit erwarteten Resultaten durchführen
- Array- und String-Aufgaben übersichtlicher strukturieren

---

## Ausgangslage

Viele Programme funktionieren zuerst in einer einzigen `main`-Methode. Das ist für den Einstieg in Ordnung. Mit der Zeit wird der Code aber schwer lesbar, weil mehrere Aufgaben vermischt werden.

Beispiel:

```java
public static void main(String[] args) {
    int[] werte = {12, 15, 18, 21, 19, 14};

    int summe = 0;
    for (int i = 0; i < werte.length; i++) {
        summe += werte[i];
    }

    double durchschnitt = (double) summe / werte.length;

    int max = werte[0];
    for (int i = 1; i < werte.length; i++) {
        if (werte[i] > max) {
            max = werte[i];
        }
    }

    System.out.println("Summe: " + summe);
    System.out.println("Durchschnitt: " + durchschnitt);
    System.out.println("Maximum: " + max);
}
```

Der Code funktioniert, aber er mischt mehrere Aufgaben:

- Summe berechnen
- Durchschnitt berechnen
- Maximum suchen
- Resultate ausgeben

---

## Refactoring

Refactoring bedeutet: Der Code wird verbessert, ohne dass sich das sichtbare Verhalten ändert.

Nach dem Refactoring könnte der Hauptteil so aussehen:

```java
public static void main(String[] args) {
    int[] werte = {12, 15, 18, 21, 19, 14};

    System.out.println("Summe: " + summe(werte));
    System.out.println("Durchschnitt: " + durchschnitt(werte));
    System.out.println("Maximum: " + maximum(werte));
}
```

Die Details stehen in eigenen Methoden.

---

## Gute Methodennamen

Ein Methodenname soll sagen, was die Methode macht.

| Gut | Weniger gut |
| --- | --- |
| `summe` | `rechne` |
| `maximum` | `machArray` |
| `istGueltigeEingabe` | `check` |
| `zaehleLeerzeichen` | `zaehle` |

Wenn eine Methode einen `boolean` zurückgibt, helfen Namen mit `ist`, `hat` oder `enthaelt`.

```java
public static boolean istLeer(String text) {
    return text.trim().isEmpty();
}
```

---

## Tests mit erwarteten Resultaten

Bevor Code umgebaut wird, braucht es eine einfache Kontrolle.

```java
int[] werte = {4, 7, 2, 9};

System.out.println(summe(werte));       // erwartet: 22
System.out.println(maximum(werte));     // erwartet: 9
System.out.println(enthaelt(werte, 7)); // erwartet: true
```

Wenn nach dem Refactoring dieselben Resultate erscheinen, ist das Verhalten gleich geblieben.

---

## Auftrag 1 – Code markieren

Markiere im folgenden Code, welche Zeilen zusammengehören.

```java
String input = "  Java macht Spass  ";

String bereinigt = input.trim();
String klein = bereinigt.toLowerCase();
boolean enthaeltJava = klein.contains("java");

System.out.println(klein);
System.out.println(enthaeltJava);
```

Fragen:

- Welche Zeilen bereinigen den Text?
- Welche Zeile prüft den Inhalt?
- Welche Teile könnten eigene Methoden werden?

---

## Auftrag 2 – Methoden planen

Plane passende Methoden für diese Aufgaben.

| Aufgabe | Methodenname | Parameter | Rückgabewert |
| --- | --- | --- | --- |
| Text trimmen und klein schreiben | | | |
| Prüfen, ob Text `java` enthält | | | |
| Anzahl Werte über Grenze zählen | | | |
| Durchschnitt eines Arrays berechnen | | | |

---

## Auftrag 3 – Refactoring durchführen

Baue den folgenden Code so um, dass die Berechnungen in Methoden stehen.

```java
int[] punkte = {8, 12, 7, 15, 10};

int bestanden = 0;
for (int i = 0; i < punkte.length; i++) {
    if (punkte[i] >= 10) {
        bestanden++;
    }
}

int summe = 0;
for (int i = 0; i < punkte.length; i++) {
    summe += punkte[i];
}

System.out.println("Bestanden: " + bestanden);
System.out.println("Summe: " + summe);
```

Vorgaben:

- Schreibe eine Methode `zaehleBestanden`.
- Schreibe eine Methode `summe`.
- `main` soll am Ende nur noch Methoden aufrufen und ausgeben.

---

## Auftrag 4 – Tests ergänzen

Ergänze mindestens drei Testausgaben mit erwarteten Resultaten als Kommentar.

Beispiel:

```java
System.out.println(zaehleBestanden(new int[]{8, 12, 7, 15, 10})); // erwartet: 3
```

---

## Typische Stolpersteine

- Eine Methode macht zu viele Dinge gleichzeitig.
- Ein Methodenname ist zu allgemein.
- Eine Methode gibt etwas aus, obwohl sie eigentlich etwas berechnen soll.
- `return` steht in der Schleife, obwohl alle Werte verarbeitet werden müssen.
- Nach dem Refactoring fehlen Testfälle.

---

## Reflexion

- Welche Methode ist nach dem Umbau am einfachsten zu testen?
- Welche Methode hat den klarsten Namen?
- Wo war die Entscheidung für den Rückgabewert schwierig?
- Was ist in `main` übersichtlicher geworden?
