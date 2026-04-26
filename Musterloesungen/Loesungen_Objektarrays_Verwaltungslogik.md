# Lösungen – Objektarrays und Verwaltungslogik

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

## Aufgabe 1 und 2 – Array erstellen und ausgeben

```java
public static void gibAlleAus(Produkt[] produkte) {
    for (int i = 0; i < produkte.length; i++) {
        produkte[i].ausgeben();
    }
}
```

## Aufgabe 3 – Gesamtwert berechnen

```java
public static double berechneGesamtwert(Produkt[] produkte) {
    double summe = 0.0;

    for (int i = 0; i < produkte.length; i++) {
        summe += produkte[i].getPreis();
    }

    return summe;
}
```

## Aufgabe 4 – Teure Produkte zählen

```java
public static int zaehleTeureProdukte(Produkt[] produkte) {
    int anzahl = 0;

    for (int i = 0; i < produkte.length; i++) {
        if (produkte[i].getPreis() >= 100.0) {
            anzahl++;
        }
    }

    return anzahl;
}
```

## Aufgabe 5 – Produktname suchen

```java
public static boolean enthaeltProdukt(Produkt[] produkte, String name) {
    for (int i = 0; i < produkte.length; i++) {
        if (produkte[i].getName().equals(name)) {
            return true;
        }
    }

    return false;
}
```

## Aufgabe 6 – Produkt zurückgeben

```java
public static Produkt findeProdukt(Produkt[] produkte, String name) {
    for (int i = 0; i < produkte.length; i++) {
        if (produkte[i].getName().equals(name)) {
            return produkte[i];
        }
    }

    return null;
}
```

Beispiel für die `null`-Prüfung:

```java
Produkt gefunden = findeProdukt(produkte, "Maus");

if (gefunden != null) {
    gefunden.ausgeben();
} else {
    System.out.println("Produkt nicht gefunden.");
}
```

## Aufgabe 7 – Teuerstes Produkt finden

```java
public static Produkt findeTeuerstesProdukt(Produkt[] produkte) {
    Produkt teuerstesProdukt = produkte[0];

    for (int i = 1; i < produkte.length; i++) {
        if (produkte[i].getPreis() > teuerstesProdukt.getPreis()) {
            teuerstesProdukt = produkte[i];
        }
    }

    return teuerstesProdukt;
}
```

## Aufgabe 8 – Preise erhöhen

```java
public static void erhoeheAllePreise(Produkt[] produkte, double betrag) {
    if (betrag < 0) {
        return;
    }

    for (int i = 0; i < produkte.length; i++) {
        double neuerPreis = produkte[i].getPreis() + betrag;
        produkte[i].setPreis(neuerPreis);
    }
}
```

## Aufgabe 9 – Durchschnittspreis

```java
public static double berechneDurchschnittspreis(Produkt[] produkte) {
    if (produkte.length == 0) {
        return 0.0;
    }

    return berechneGesamtwert(produkte) / produkte.length;
}
```

## Aufgabe 10 – Kleine Produktverwaltung

```java
public class Main {
    public static void main(String[] args) {
        Produkt[] produkte = {
            new Produkt("Tastatur", 49.90),
            new Produkt("Monitor", 179.00),
            new Produkt("Maus", 24.50)
        };

        gibAlleAus(produkte);
        System.out.println("Gesamtwert: " + berechneGesamtwert(produkte));
        System.out.println("Teure Produkte: " + zaehleTeureProdukte(produkte));

        Produkt gefunden = findeProdukt(produkte, "Maus");
        if (gefunden != null) {
            gefunden.ausgeben();
        }

        Produkt teuerstesProdukt = findeTeuerstesProdukt(produkte);
        System.out.println("Teuerstes Produkt:");
        teuerstesProdukt.ausgeben();

        erhoeheAllePreise(produkte, 5.0);
        gibAlleAus(produkte);
    }
}
```

Hinweis: Die Methoden arbeiten mit gekapselten Objekten. Preise werden über `getPreis()` gelesen und über `setPreis(...)` verändert.
