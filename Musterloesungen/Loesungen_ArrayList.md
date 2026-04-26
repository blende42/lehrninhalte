# Lösungen – ArrayList

## Produktklasse

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

## Aufgabe 1 und 2 – ArrayList erstellen und ausgeben

```java
import java.util.ArrayList;

public static void gibAlleAus(ArrayList<Produkt> produkte) {
    for (int i = 0; i < produkte.size(); i++) {
        produkte.get(i).ausgeben();
    }
}
```

## Aufgabe 3 – Gesamtwert berechnen

```java
public static double berechneGesamtwert(ArrayList<Produkt> produkte) {
    double summe = 0.0;

    for (int i = 0; i < produkte.size(); i++) {
        summe += produkte.get(i).getPreis();
    }

    return summe;
}
```

## Aufgabe 5 – Produkt suchen

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

## Aufgabe 6 – Teure Produkte zählen

```java
public static int zaehleTeureProdukte(ArrayList<Produkt> produkte) {
    int anzahl = 0;

    for (int i = 0; i < produkte.size(); i++) {
        if (produkte.get(i).getPreis() >= 100.0) {
            anzahl++;
        }
    }

    return anzahl;
}
```

## Aufgabe 7 – Teuerstes Produkt finden

```java
public static Produkt findeTeuerstesProdukt(ArrayList<Produkt> produkte) {
    if (produkte.size() == 0) {
        return null;
    }

    Produkt teuerstesProdukt = produkte.get(0);

    for (int i = 1; i < produkte.size(); i++) {
        if (produkte.get(i).getPreis() > teuerstesProdukt.getPreis()) {
            teuerstesProdukt = produkte.get(i);
        }
    }

    return teuerstesProdukt;
}
```

## Aufgabe 8 – Produkt entfernen

```java
public static boolean entferneProdukt(ArrayList<Produkt> produkte, String name) {
    for (int i = 0; i < produkte.size(); i++) {
        if (produkte.get(i).getName().equals(name)) {
            produkte.remove(i);
            return true;
        }
    }

    return false;
}
```

## Aufgabe 9 – Preise erhöhen

```java
public static void erhoeheAllePreise(ArrayList<Produkt> produkte, double betrag) {
    if (betrag < 0) {
        return;
    }

    for (int i = 0; i < produkte.size(); i++) {
        Produkt produkt = produkte.get(i);
        produkt.setPreis(produkt.getPreis() + betrag);
    }
}
```

## Aufgabe 10 – Kleine Verwaltung mit ArrayList

```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        ArrayList<Produkt> produkte = new ArrayList<>();
        produkte.add(new Produkt("Tastatur", 49.90));
        produkte.add(new Produkt("Monitor", 179.00));
        produkte.add(new Produkt("Maus", 24.50));
        produkte.add(new Produkt("Webcam", 79.00));

        gibAlleAus(produkte);
        System.out.println("Gesamtwert: " + berechneGesamtwert(produkte));
        System.out.println("Teure Produkte: " + zaehleTeureProdukte(produkte));

        Produkt teuerstesProdukt = findeTeuerstesProdukt(produkte);
        if (teuerstesProdukt != null) {
            System.out.println("Teuerstes Produkt:");
            teuerstesProdukt.ausgeben();
        }

        Produkt gefunden = findeProdukt(produkte, "Maus");
        if (gefunden != null) {
            gefunden.ausgeben();
        }

        entferneProdukt(produkte, "Maus");
        erhoeheAllePreise(produkte, 5.0);
        gibAlleAus(produkte);
    }
}
```

Hinweis: Die Verwaltungslogik bleibt ähnlich wie bei Objektarrays. Neu sind vor allem `add`, `get`, `size`, `set` und `remove`.
