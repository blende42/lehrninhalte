# Übungen – Klassen und Objekte

## Basis

### Aufgabe 1 – Klasse lesen

Gegeben ist folgende Klasse:

```java
class Person {
    String name;
    int alter;
}
```

Beantworte:

- Wie heisst die Klasse?
- Welche Attribute hat die Klasse?
- Welche Datentypen haben die Attribute?

---

### Aufgabe 2 – Objekt erstellen

Erstelle in `main` zwei `Person`-Objekte.

Vorgaben:

- erste Person: Name `Lea`, Alter `17`
- zweite Person: Name `Noah`, Alter `18`
- Gib Name und Alter beider Personen aus.

---

### Aufgabe 3 – Methode ergänzen

Ergänze die Klasse `Person` um eine Methode `ausgeben`.

Erwartete Ausgabe für Lea:

```text
Lea ist 17 Jahre alt.
```

---

## Aufbau

### Aufgabe 4 – Konstruktor schreiben

Passe `Person` so an, dass Name und Alter über einen Konstruktor gesetzt werden.

Beispiel:

```java
Person lea = new Person("Lea", 17);
```

---

### Aufgabe 5 – Produktklasse

Schreibe eine Klasse `Produkt`.

Attribute:

- `String name`
- `double preis`

Vorgaben:

- Schreibe einen Konstruktor.
- Schreibe eine Methode `ausgeben`.
- Erstelle zwei Produkte in `main`.

---

### Aufgabe 6 – Methode mit Rückgabewert

Ergänze `Produkt` um eine Methode `istTeuer`.

Vorgaben:

- Rückgabewert: `boolean`
- Ein Produkt ist teuer, wenn der Preis mindestens `100.0` ist.

---

## Vertiefung

### Aufgabe 7 – Preis ändern

Ergänze `Produkt` um eine Methode `setzePreis`.

Vorgaben:

- Parameter: `double neuerPreis`
- Wenn der neue Preis negativ ist, soll der Preis nicht geändert werden.
- Teste beide Fälle.

---

### Aufgabe 8 – Array von Produkten

Erstelle ein Array mit drei Produkten.

Gib alle Produkte mit einer Schleife aus.

---

### Aufgabe 9 – Teuerstes Produkt

Schreibe eine Methode `findeTeuerstesProdukt`.

Vorgaben:

- Parameter: `Produkt[] produkte`
- Rückgabewert: `Produkt`
- Das Array ist nicht leer.

---

## Transfer

### Aufgabe 10 – Mini-Verwaltung

Erstelle eine kleine Produktverwaltung.

Vorgaben:

- Klasse `Produkt` mit `name`, `preis`, Konstruktor und `ausgeben`
- Methode `findeTeuerstesProdukt`
- Methode `zaehleTeureProdukte`
- In `main`: drei Produkte erstellen, alle ausgeben, teuerstes Produkt ausgeben, Anzahl teurer Produkte ausgeben

Teuer bedeutet: Preis mindestens `100.0`.

---

## Reflexion

- Was ist in der Klasse definiert?
- Was gehört zu einem einzelnen Objekt?
- Welche Methoden geben nur aus?
- Welche Methoden berechnen ein Ergebnis?
