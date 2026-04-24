# Arbeitsblatt – Arrays

## Lernziele
- Arrays als Sammlung gleichartiger Werte verstehen
- auf Elemente per Index zugreifen
- Arrays mit Schleifen verarbeiten
- typische Fehler vermeiden

## Theorie (kurz)

### Wozu dient ein Array?
- mehrere Werte unter einem Namen speichern
- alle Elemente haben denselben Datentyp

### Index
- der erste Index ist 0
- letzter Index = `length - 1`

### Zugriff auf Elemente
- Zugriff erfolgt mit eckigen Klammern
- Beispiel: `noten[0]`

### Arrays mit Schleifen
- mit einer `for`-Schleife alle Werte durchlaufen
- typische Form: `i < array.length`

## Beispiel

```java
int[] noten = {5, 4, 6, 5, 4};
```

```text
Index:   0   1   2   3   4
Wert:    5   4   6   5   4
```

```java
System.out.println(noten[0]);   // 5
System.out.println(noten.length); // 5

for (int i = 0; i < noten.length; i++) {
    System.out.println(noten[i]);
}
```

## Typische Fehler

- Index beginnt bei 1 → falsch
- `<=` statt `<` in der Schleife
- `length` mit letztem Index verwechseln
- Zugriff ausserhalb des Arrays

## Reflexion

- Wann ist ein Array sinnvoll?
- Warum beginnt der Index bei 0?
- Weshalb ist `length` nicht der letzte Index?
- Welche Fehler treten bei Schleifen schnell auf?
