# Arbeitsblatt – ArrayList in Java

## Lernziele

- Unterschied zwischen Array und `ArrayList` erklären
- `ArrayList` erstellen und mit Objekten verwenden
- Elemente hinzufügen, lesen, ändern und entfernen
- mit `size()` und Schleifen über eine `ArrayList` laufen
- bekannte Verwaltungslogik von Objektarrays auf `ArrayList` übertragen

---

## Warum ArrayList?

Ein Array hat eine feste Länge.

```java
Produkt[] produkte = new Produkt[3];
```

Wenn später ein weiteres Produkt dazukommt, ist das Array zu klein.

Eine `ArrayList` kann wachsen und schrumpfen.

```java
ArrayList<Produkt> produkte = new ArrayList<>();
```

---

## Import

`ArrayList` gehört nicht automatisch zum Grundumfang jeder Java-Datei. Deshalb braucht es oben in der Datei einen Import.

```java
import java.util.ArrayList;
```

---

## ArrayList erstellen

```java
ArrayList<Produkt> produkte = new ArrayList<>();
```

`Produkt` in den spitzen Klammern bedeutet: Diese Liste speichert `Produkt`-Objekte.

---

## Elemente hinzufügen

```java
produkte.add(new Produkt("Tastatur", 49.90));
produkte.add(new Produkt("Monitor", 179.00));
produkte.add(new Produkt("Maus", 24.50));
```

Die Liste wächst mit jedem `add`.

---

## Elemente lesen

Bei einem Array:

```java
produkte[i]
```

Bei einer `ArrayList`:

```java
produkte.get(i)
```

Beispiel:

```java
Produkt erstesProdukt = produkte.get(0);
erstesProdukt.ausgeben();
```

---

## Länge bestimmen

Bei einem Array:

```java
produkte.length
```

Bei einer `ArrayList`:

```java
produkte.size()
```

---

## Schleife über eine ArrayList

```java
for (int i = 0; i < produkte.size(); i++) {
    produkte.get(i).ausgeben();
}
```

Das Muster bleibt gleich:

- Start bei `0`
- solange `i < produkte.size()`
- Zugriff mit `produkte.get(i)`

---

## Elemente ändern und entfernen

Element ersetzen:

```java
produkte.set(1, new Produkt("Bildschirm", 199.00));
```

Element entfernen:

```java
produkte.remove(2);
```

Wichtig: Nach `remove` verschieben sich die folgenden Indizes.

---

## Beispielklasse

```java
class Produkt {
    private String name;
    private double preis;

    Produkt(String name, double preis) {
        this.name = name;
        setPreis(preis);
    }

    public String getName() {
        return name;
    }

    public double getPreis() {
        return preis;
    }

    public void setPreis(double preis) {
        if (preis >= 0) {
            this.preis = preis;
        }
    }

    public void ausgeben() {
        System.out.println(name + ": " + preis);
    }
}
```

---

## Verwaltungslogik mit ArrayList

```java
public static Produkt findeProdukt(ArrayList<Produkt> produkte, String name) {
    for (int i = 0; i < produkte.size(); i++) {
        if (produkte.get(i).getName().equals(name)) {
            return produkte.get(i);
        }
    }

    return null;
}
```

Die Methode sieht fast gleich aus wie bei Arrays. Nur Zugriff und Länge ändern sich.

---

## Array vs. ArrayList

| Aufgabe | Array | ArrayList |
| --- | --- | --- |
| Länge | `array.length` | `liste.size()` |
| Element lesen | `array[i]` | `liste.get(i)` |
| Element setzen | `array[i] = wert` | `liste.set(i, wert)` |
| Element hinzufügen | nicht direkt möglich | `liste.add(wert)` |
| Element entfernen | nicht direkt möglich | `liste.remove(i)` |

---

## Typische Stolpersteine

- `import java.util.ArrayList;` fehlt.
- `length` wird statt `size()` verwendet.
- `produkte[i]` wird statt `produkte.get(i)` verwendet.
- Nach `remove` wird mit alten Indizes weitergedacht.
- Beim Suchen wird `null` zurückgegeben, aber später nicht geprüft.

---

## Reflexion

- Wann reicht ein Array?
- Wann ist eine `ArrayList` praktischer?
- Welche Teile der alten Objektarray-Logik bleiben gleich?
- Welche Schreibweisen ändern sich?
