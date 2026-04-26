# Arbeitsblatt – Objektarrays und Verwaltungslogik

## Lernziele

- Arrays mit Objekten erstellen und durchlaufen
- bekannte Array-Muster auf Objekte übertragen
- Getter bei gekapselten Objekten verwenden
- Methoden schreiben, die Objektarrays verarbeiten
- einfache Verwaltungslogik ohne `ArrayList` strukturieren

---

## Ausgangslage

Bisher wurden einzelne Objekte erstellt.

```java
Produkt maus = new Produkt("Maus", 24.50);
maus.ausgeben();
```

In einer kleinen Verwaltung braucht man meistens mehrere Objekte.

```java
Produkt[] produkte = {
    new Produkt("Tastatur", 49.90),
    new Produkt("Monitor", 179.00),
    new Produkt("Maus", 24.50)
};
```

Das ist ein Array von `Produkt`-Objekten.

---

## Objektarray durchlaufen

Objektarrays werden mit einer Schleife durchlaufen, genau wie Arrays mit Zahlen.

```java
for (int i = 0; i < produkte.length; i++) {
    produkte[i].ausgeben();
}
```

`produkte[i]` ist jeweils ein einzelnes `Produkt`-Objekt.

---

## Kapselung beachten

Wenn Attribute `private` sind, wird über Getter gelesen.

```java
double preis = produkte[i].getPreis();
String name = produkte[i].getName();
```

Nicht so:

```java
double preis = produkte[i].preis;
```

Der direkte Zugriff passt nicht mehr zur Kapselung.

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

## Muster 1 – Zählen

Wie viele Produkte kosten mindestens `100.0`?

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

---

## Muster 2 – Suchen

Gibt es ein Produkt mit einem bestimmten Namen?

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

Wenn das Produkt selbst gebraucht wird, kann die Methode ein `Produkt` zurückgeben.

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

Wichtig: `null` bedeutet hier, dass nichts gefunden wurde.

---

## Muster 3 – Maximum

Welches Produkt ist am teuersten?

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

Die Methode gibt das ganze Produkt zurück, nicht nur den Preis. So kann man danach Name und Preis ausgeben.

---

## Mini-Verwaltungslogik

Eine kleine Verwaltung besteht aus mehreren Hilfsmethoden.

```java
public static void gibAlleAus(Produkt[] produkte) { ... }
public static Produkt findeProdukt(Produkt[] produkte, String name) { ... }
public static Produkt findeTeuerstesProdukt(Produkt[] produkte) { ... }
public static double berechneGesamtwert(Produkt[] produkte) { ... }
```

`main` bleibt dadurch übersichtlich.

---

## Typische Stolpersteine

- Direkt auf private Attribute zugreifen statt Getter verwenden.
- Bei einer Suche `null` nicht prüfen.
- Beim Maximum nur den Preis zurückgeben, obwohl das ganze Objekt gebraucht wird.
- Alles in `main` schreiben statt Hilfsmethoden zu verwenden.
- Leere Arrays nicht bedenken, obwohl `produkte[0]` verwendet wird.

---

## Reflexion

- Welche bekannten Array-Muster erkennst du wieder?
- Warum ist die Rückgabe `Produkt` manchmal besser als `double`?
- Wo muss auf `null` geprüft werden?
- Warum bleibt `main` mit Hilfsmethoden einfacher lesbar?
