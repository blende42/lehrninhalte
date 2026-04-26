# Lösungen – Kapselung, Getter und Setter

## Aufgabe 1 – Problem erkennen

Mögliche Antworten:

- Bei `preis` könnte ein negativer Wert gespeichert werden.
- Direkter Zugriff ist problematisch, weil keine Prüfung stattfindet.
- `private` verhindert, dass fremder Code Attribute direkt verändert.

## Aufgabe 2 bis 6 – Produkt mit Kapselung

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

Hinweis: Für `name` gibt es bewusst keinen Setter. Der Name soll nach dem Erstellen nicht geändert werden.

## Aufgabe 7 und 8 – Bankkonto

```java
class Bankkonto {
    private String inhaber;
    private double saldo;

    Bankkonto(String inhaber, double startsaldo) {
        this.inhaber = inhaber;
        if (startsaldo >= 0) {
            this.saldo = startsaldo;
        }
    }

    public String getInhaber() {
        return inhaber;
    }

    public double getSaldo() {
        return saldo;
    }

    public void einzahlen(double betrag) {
        if (betrag > 0) {
            saldo += betrag;
        }
    }

    public boolean abheben(double betrag) {
        if (betrag > 0 && betrag <= saldo) {
            saldo -= betrag;
            return true;
        }

        return false;
    }
}
```

## Aufgabe 9 – Produktarray mit gekapselten Attributen

```java
public class Main {
    public static Produkt findeTeuerstesProdukt(Produkt[] produkte) {
        Produkt teuerstesProdukt = produkte[0];

        for (int i = 1; i < produkte.length; i++) {
            if (produkte[i].getPreis() > teuerstesProdukt.getPreis()) {
                teuerstesProdukt = produkte[i];
            }
        }

        return teuerstesProdukt;
    }

    public static void main(String[] args) {
        Produkt[] produkte = {
            new Produkt("Tastatur", 49.90),
            new Produkt("Monitor", 179.00),
            new Produkt("Maus", 24.50)
        };

        Produkt teuerstesProdukt = findeTeuerstesProdukt(produkte);
        teuerstesProdukt.ausgeben();
    }
}
```

## Aufgabe 10 – Reflexionsauftrag im Code

```java
class Produkt {
    // private, damit der Preis nicht ungeprüft negativ gesetzt werden kann.
    private double preis;

    // Kein setName: Der Produktname soll nach dem Erstellen gleich bleiben.
    private String name;
}
```

Hinweis: Kommentare sollen kurz erklären, warum eine Entscheidung getroffen wurde. Sie sollen nicht nur den Code wiederholen.
