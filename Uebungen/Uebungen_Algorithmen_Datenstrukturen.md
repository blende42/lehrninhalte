# Übungen – Algorithmen und Datenstrukturen

## Basis

### Aufgabe 1 – Array ausgeben

Schreibe eine Methode `gibAus`.

Vorgaben:

- Parameter: `int[] zahlen`
- Rückgabewert: keiner
- Gib alle Werte in einer Zeile aus.

Beispiel:

```text
5 2 8 1
```

---

### Aufgabe 2 – Lineare Suche

Schreibe eine Methode `enthaelt`.

Vorgaben:

- Parameter: `int[] zahlen`, `int gesucht`
- Rückgabewert: `boolean`
- Gib `true` zurück, wenn der Wert vorkommt.
- Gib `false` zurück, wenn der Wert nicht vorkommt.

Testdaten:

```java
int[] zahlen = {5, 2, 8, 1};
```

Erwartete Resultate:

- `enthaelt(zahlen, 8)` ergibt `true`
- `enthaelt(zahlen, 7)` ergibt `false`

---

### Aufgabe 3 – Minimum und Maximum

Schreibe zwei Methoden:

```java
public static int findeMinimum(int[] zahlen)
public static int findeMaximum(int[] zahlen)
```

Vorgaben:

- Das Array enthält mindestens ein Element.
- Starte nicht mit `0`, sondern mit dem ersten Arraywert.

---

### Aufgabe 4 – Werte zählen

Schreibe eine Methode `zaehleMindestens`.

Vorgaben:

- Parameter: `int[] zahlen`, `int grenze`
- Rückgabewert: `int`
- Zähle alle Werte, die mindestens so gross wie `grenze` sind.

Beispiel:

```java
int[] zahlen = {5, 120, 8, 100, 1};
```

`zaehleMindestens(zahlen, 100)` ergibt `2`.

---

## Aufbau

### Aufgabe 5 – Bubble Sort ergänzen

Ergänze die fehlenden Stellen.

```java
public static void bubbleSort(int[] zahlen) {
    for (int durchlauf = 0; durchlauf < zahlen.length - 1; durchlauf++) {
        for (int i = 0; i < zahlen.length - 1 - durchlauf; i++) {
            if (__________) {
                int temp = zahlen[i];
                zahlen[i] = __________;
                zahlen[i + 1] = __________;
            }
        }
    }
}
```

Teste mit:

```java
int[] zahlen = {5, 2, 8, 1};
```

Erwartetes Resultat:

```text
1 2 5 8
```

---

### Aufgabe 6 – Selection Sort ergänzen

Ergänze die fehlenden Stellen.

```java
public static void selectionSort(int[] zahlen) {
    for (int start = 0; start < zahlen.length - 1; start++) {
        int indexMinimum = start;

        for (int i = start + 1; i < zahlen.length; i++) {
            if (__________) {
                indexMinimum = i;
            }
        }

        int temp = zahlen[start];
        zahlen[start] = __________;
        zahlen[indexMinimum] = __________;
    }
}
```

Teste mit:

```java
int[] zahlen = {9, 3, 7, 3, 1};
```

Erwartetes Resultat:

```text
1 3 3 7 9
```

---

## Vertiefung

### Aufgabe 7 – Absteigend sortieren

Passe Bubble Sort so an, dass das Array absteigend sortiert wird.

Beispiel:

```java
int[] zahlen = {5, 2, 8, 1};
```

Erwartetes Resultat:

```text
8 5 2 1
```

---

### Aufgabe 8 – Sortierung prüfen

Schreibe eine Methode `istAufsteigendSortiert`.

Vorgaben:

- Parameter: `int[] zahlen`
- Rückgabewert: `boolean`
- Ein leeres Array gilt als sortiert.
- Ein Array mit einem Element gilt als sortiert.

Beispiele:

- `{1, 2, 5, 8}` ergibt `true`
- `{1, 5, 2, 8}` ergibt `false`

---

### Aufgabe 9 – Vergleiche zählen

Erweitere Bubble Sort so, dass die Anzahl Vergleiche gezählt und zurückgegeben wird.

Vorgabe:

```java
public static int bubbleSortUndZaehleVergleiche(int[] zahlen)
```

Für ein Array mit `4` Elementen ergibt die einfache Version `6` Vergleiche.

---

## Transfer

### Aufgabe 10 – Preise sortieren

Sortiere Produktpreise mit Selection Sort.

Vorgaben:

- Verwende `double[]`.
- Sortiere aufsteigend.
- Verwende dieselbe Idee wie bei `int[]`.

Testdaten:

```java
double[] preise = {49.90, 179.00, 24.50, 79.00};
```

Erwartetes Resultat:

```text
24.5 49.9 79.0 179.0
```

---

### Aufgabe 11 – Produktarray nach Preis sortieren

Diese Aufgabe ist ein Ausblick.

Sortiere ein `Produkt[]` nach Preis.

Vorgaben:

- Verwende `getPreis()` zum Vergleichen.
- Tausche ganze `Produkt`-Objekte, nicht nur Preise.
- Verwende Selection Sort.

---

### Aufgabe 12 – Zinseszins mit Schleife

Schreibe eine Methode `berechneKapital`.

Vorgaben:

- Parameter: `double startkapital`, `double zinssatz`, `int jahre`
- Rückgabewert: `double`
- Verwende keine Potenzrechnung.
- Verwende eine Schleife.
- Wende pro Jahr die normale Zinsformel an:

```java
double zins = kapital * zinssatz / 100;
kapital = kapital + zins;
```

Testfall:

```java
berechneKapital(1000.0, 2.0, 3)
```

Erwartete Zwischenschritte:

```text
Jahr 1: 1020.0
Jahr 2: 1040.4
Jahr 3: 1061.208
```

---

### Aufgabe 13 – Pensionskassenkapital simulieren

In der beruflichen Vorsorge leisten Arbeitnehmer und Arbeitgeber Beiträge. In dieser vereinfachten Aufgabe wird das Alterskapital von Alter `20` bis `65` simuliert.

Verwende die Sparbeiträge aus dem Reglement:

| Alter | Arbeitnehmer Mini | Arbeitnehmer Standard | Arbeitnehmer Maxi | Arbeitgeber |
| --- | ---: | ---: | ---: | ---: |
| 20-24 | 4.00 | 4.00 | 6.00 | 6.00 |
| 25-29 | 4.35 | 4.35 | 6.35 | 6.40 |
| 30-34 | 4.70 | 4.70 | 6.70 | 7.80 |
| 35-39 | 5.80 | 5.80 | 7.80 | 9.20 |
| 40-44 | 6.90 | 6.90 | 8.90 | 10.60 |
| 45-49 | 7.60 | 8.00 | 10.00 | 12.00 |
| 50-54 | 7.60 | 9.10 | 11.10 | 13.40 |
| 55-59 | 7.60 | 10.20 | 12.20 | 14.80 |
| 60-65 | 7.60 | 11.30 | 13.30 | 16.20 |

Vereinfachungen:

- Es werden nur Sparbeiträge berücksichtigt.
- Risikobeiträge werden ignoriert.
- Das vorhandene Kapital wird am Anfang jedes Jahres verzinst.
- Danach werden Arbeitgeber- und Arbeitnehmerbeiträge gutgeschrieben.
- Der versicherte Jahreslohn und der Zinssatz können pro Jahr unterschiedlich sein.

Vorgaben:

- Verwende Arrays für die Jahreslöhne und Zinssätze.
- Simuliere alle Jahre von Alter `20` bis `65`.
- Berechne parallel die Varianten `Mini`, `Standard` und `Maxi`.
- Gib pro Jahr eine Tabellenzeile aus.

Beispiel für den Tabellenkopf:

```text
Alter;Lohn;Zins;Mini;Standard;Maxi
```

Beispiel für eine Zeile:

```text
20;52000.0;1.0;5200.0;5200.0;6240.0
```

Die Ausgabe soll mit Semikolon getrennt sein, damit sie in Excel einfach importiert werden kann.

Starte das Programm danach mit stdout-Weiterleitung:

```bash
java PensionskassenSimulation > pensionskasse.csv
```

Öffne `pensionskasse.csv` in Excel und erstelle ein Liniendiagramm mit den drei Varianten `Mini`, `Standard` und `Maxi`.

Hinweise:

- Die Methode `ermittleArbeitnehmerSatz(int alter, String variante)` kann den Beitragssatz zurückgeben.
- Die Methode `ermittleArbeitgeberSatz(int alter)` kann den Arbeitgeberbeitrag zurückgeben.
- Die Methode `berechneNeuesKapital(...)` kann Zins und Beiträge für ein Jahr berechnen.

---

## Reflexion

- Welche Aufgaben verändern das Array?
- Welche Aufgaben lesen das Array nur?
- Wo braucht es einen Randfall für leere Arrays?
- Was ist der wichtigste Unterschied zwischen Bubble Sort und Selection Sort?
- Warum ist die Pensionskassenaufgabe eine Simulation?
- Warum hilft eine CSV-Ausgabe bei der Auswertung in Excel?
