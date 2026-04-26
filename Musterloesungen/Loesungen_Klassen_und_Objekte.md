# Lösungen – Klassen und Objekte

## Aufgabe 1 – Klasse lesen

Mögliche Antworten:

- Die Klasse heisst `Person`.
- Die Attribute heissen `name` und `alter`.
- `name` hat den Typ `String`, `alter` hat den Typ `int`.

## Aufgabe 2 bis 4 – Person mit Konstruktor und Methode

```java
class Person {
    String name;
    int alter;

    Person(String name, int alter) {
        this.name = name;
        this.alter = alter;
    }

    void ausgeben() {
        System.out.println(name + " ist " + alter + " Jahre alt.");
    }
}

public class Main {
    public static void main(String[] args) {
        Person lea = new Person("Lea", 17);
        Person noah = new Person("Noah", 18);

        lea.ausgeben();
        noah.ausgeben();
    }
}
```

## Aufgabe 5 bis 7 – Produktklasse

```java
class Produkt {
    String name;
    double preis;

    Produkt(String name, double preis) {
        this.name = name;
        this.preis = preis;
    }

    void ausgeben() {
        System.out.println(name + ": " + preis);
    }

    boolean istTeuer() {
        return preis >= 100.0;
    }

    void setzePreis(double neuerPreis) {
        if (neuerPreis >= 0) {
            preis = neuerPreis;
        }
    }
}
```

## Aufgabe 8 bis 10 – Array und Auswertung

```java
class Produkt {
    String name;
    double preis;

    Produkt(String name, double preis) {
        this.name = name;
        this.preis = preis;
    }

    void ausgeben() {
        System.out.println(name + ": " + preis);
    }

    boolean istTeuer() {
        return preis >= 100.0;
    }

    void setzePreis(double neuerPreis) {
        if (neuerPreis >= 0) {
            preis = neuerPreis;
        }
    }
}

public class Main {
    public static Produkt findeTeuerstesProdukt(Produkt[] produkte) {
        Produkt teuerstesProdukt = produkte[0];

        for (int i = 1; i < produkte.length; i++) {
            if (produkte[i].preis > teuerstesProdukt.preis) {
                teuerstesProdukt = produkte[i];
            }
        }

        return teuerstesProdukt;
    }

    public static int zaehleTeureProdukte(Produkt[] produkte) {
        int anzahl = 0;

        for (int i = 0; i < produkte.length; i++) {
            if (produkte[i].istTeuer()) {
                anzahl++;
            }
        }

        return anzahl;
    }

    public static void main(String[] args) {
        Produkt[] produkte = {
            new Produkt("Tastatur", 49.90),
            new Produkt("Monitor", 179.00),
            new Produkt("Maus", 24.50)
        };

        for (int i = 0; i < produkte.length; i++) {
            produkte[i].ausgeben();
        }

        Produkt teuerstesProdukt = findeTeuerstesProdukt(produkte);
        System.out.println("Teuerstes Produkt:");
        teuerstesProdukt.ausgeben();
        System.out.println("Teure Produkte: " + zaehleTeureProdukte(produkte));
    }
}
```

Hinweis: `findeTeuerstesProdukt` gibt ein Objekt zurück. Danach kann mit diesem Objekt weitergearbeitet werden, zum Beispiel mit `teuerstesProdukt.ausgeben()`.
