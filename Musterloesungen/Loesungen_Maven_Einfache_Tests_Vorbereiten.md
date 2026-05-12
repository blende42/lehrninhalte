# Lösungen – Maven-Projekte mit einfachen Tests vorbereiten

## Aufgabe 1 – Ausgabe oder Prüfung?

- Beispiel A ist nur eine Ausgabe.
- Beispiel B ist eine Prüfung, weil `erwartet` mit `tatsaechlich` verglichen wird.
- Beispiel C ist nur eine Ausgabe.

Antworten:

1. Beispiel B ist am besten prüfbar.
2. Eine sichtbare Ausgabe reicht nicht, weil eine Person selbst erkennen muss, ob der Wert stimmt.
3. Das erwartete Resultat steht in Beispiel B in der Variable `erwartet`.

Typischer Fehler: Eine Ausgabe wie `9000` sieht korrekt aus, beweist aber ohne Vergleich noch nichts.

---

## Aufgabe 2 – Erwartete Resultate formulieren

| Eingabe `preisInRappen` | Eingabe `rabattProzent` | Erwartetes Resultat |
|---:|---:|---:|
| `10000` | `10` | `9000` |
| `10000` | `0` | `10000` |
| `10000` | `100` | `0` |
| `2500` | `20` | `2000` |

Antworten:

1. `10000` und `10` ist ein Normalfall.
2. `0` Prozent und `100` Prozent Rabatt sind Edge Cases.

---

## Aufgabe 3 – Eine Methode manuell prüfen

Mögliche Lösung in `main`:

```java
ProduktVerwaltung verwaltung = new ProduktVerwaltung();

int erwartet = 9000;
int tatsaechlich = verwaltung.berechneRabattpreis(10000, 10);

if (erwartet == tatsaechlich) {
    System.out.println("OK: Rabatt 10 Prozent");
} else {
    System.out.println("FEHLER: Rabatt 10 Prozent");
    System.out.println("Erwartet: " + erwartet);
    System.out.println("Tatsächlich: " + tatsaechlich);
}
```

Hinweis: Entscheidend ist nicht die genaue Meldung, sondern der Vergleich von erwartetem und tatsächlichem Resultat.

---

## Aufgabe 4 – Mehrere Testfälle mit `if`/`else`

Mögliche Lösung:

```java
public static boolean pruefeInt(String name, int erwartet, int tatsaechlich) {
    if (erwartet == tatsaechlich) {
        System.out.println("OK: " + name);
        return true;
    } else {
        System.out.println("FEHLER: " + name);
        System.out.println("Erwartet: " + erwartet);
        System.out.println("Tatsächlich: " + tatsaechlich);
        return false;
    }
}
```

Verwendung:

```java
ProduktVerwaltung verwaltung = new ProduktVerwaltung();

pruefeInt("Rabatt 10 Prozent", 9000, verwaltung.berechneRabattpreis(10000, 10));
pruefeInt("Kein Rabatt", 10000, verwaltung.berechneRabattpreis(10000, 0));
pruefeInt("Voller Rabatt", 0, verwaltung.berechneRabattpreis(10000, 100));
```

Antworten:

1. Die Hilfsmethode ist besser, weil jede Prüfung gleich aufgebaut ist und Fehler klarer ausgegeben werden.
2. Besonders hilfreich sind Name der Prüfung, erwarteter Wert und tatsächlicher Wert.

---

## Aufgabe 5 – Suche nach Produkt prüfen

Mögliche Lösung:

```java
ProduktVerwaltung verwaltung = new ProduktVerwaltung();

Produkt[] produkte = {
    new Produkt("Maus", 2500, 3),
    new Produkt("Tastatur", 7000, 2),
    new Produkt("Monitor", 19900, 1)
};

Produkt gefunden = verwaltung.findeProdukt(produkte, "Tastatur");

if (gefunden != null) {
    System.out.println("OK: Tastatur gefunden");
} else {
    System.out.println("FEHLER: Tastatur wurde nicht gefunden");
}

Produkt nichtGefunden = verwaltung.findeProdukt(produkte, "Webcam");

if (nichtGefunden == null) {
    System.out.println("OK: Webcam nicht gefunden");
} else {
    System.out.println("FEHLER: Webcam sollte nicht gefunden werden");
}
```

Typischer Fehler: Nur den gefundenen Fall prüfen. Der Fall «nicht vorhanden» ist bei Suchmethoden wichtig.

---

## Aufgabe 6 – Gesamtwert prüfen

Berechnung:

```text
Maus:      2500 * 3 = 7500
Tastatur: 7000 * 2 = 14000
Monitor: 19900 * 1 = 19900
Gesamt:   41400
```

Mögliche Lösung:

```java
ProduktVerwaltung verwaltung = new ProduktVerwaltung();

Produkt[] produkte = {
    new Produkt("Maus", 2500, 3),
    new Produkt("Tastatur", 7000, 2),
    new Produkt("Monitor", 19900, 1)
};

int erwartet = 41400;
int tatsaechlich = verwaltung.berechneGesamtwert(produkte);

pruefeInt("Gesamtwert", erwartet, tatsaechlich);
```

---

## Aufgabe 7 – Fachlogik aus `main` herauslösen

Fachlogik in `ProduktVerwaltung`:

```java
public int berechneRabattpreis(int preisInRappen, int rabattProzent) {
    int rabattBetrag = preisInRappen * rabattProzent / 100;
    return preisInRappen - rabattBetrag;
}
```

`main` ruft nur noch auf und prüft:

```java
ProduktVerwaltung verwaltung = new ProduktVerwaltung();

int rabattpreis = verwaltung.berechneRabattpreis(10000, 10);
System.out.println("Rabattpreis: " + rabattpreis);

pruefeInt("Rabatt 10 Prozent", 9000, rabattpreis);
```

Hinweis: Die Berechnung ist jetzt wiederverwendbar. `main` ist nur noch Startpunkt und Anzeigeort.

---

## Aufgabe 8 – Testmethoden mit Rückgabewert schreiben

Mögliche kompakte Lösung:

```java
public static boolean testeRabattberechnung() {
    ProduktVerwaltung verwaltung = new ProduktVerwaltung();
    int tatsaechlich = verwaltung.berechneRabattpreis(10000, 10);
    return pruefeInt("Rabattberechnung", 9000, tatsaechlich);
}

public static boolean testeGesamtwert() {
    ProduktVerwaltung verwaltung = new ProduktVerwaltung();

    Produkt[] produkte = {
        new Produkt("Maus", 2500, 3),
        new Produkt("Tastatur", 7000, 2),
        new Produkt("Monitor", 19900, 1)
    };

    int tatsaechlich = verwaltung.berechneGesamtwert(produkte);
    return pruefeInt("Gesamtwert", 41400, tatsaechlich);
}
```

Zusammenfassung in `main`:

```java
int fehler = 0;

if (!testeRabattberechnung()) {
    fehler++;
}

if (!testeGesamtwert()) {
    fehler++;
}

if (fehler == 0) {
    System.out.println("Alle Prüfungen erfolgreich.");
} else {
    System.out.println("Anzahl Fehler: " + fehler);
}
```

---

## Aufgabe 9 – Typischen Fehler finden

Antworten:

1. Die Methode ist schlechter prüfbar, weil sie keinen Wert zurückgibt. Sie schreibt nur auf die Konsole.
2. Passender Rückgabetyp ist `int`.
3. Die letzte Zeile sollte `return summe;` sein.
4. `main` darf den Rückgabewert anzeigen oder mit einem erwarteten Wert vergleichen.

Korrigierte Methode:

```java
public int berechneGesamtwert(Produkt[] produkte) {
    int summe = 0;

    for (Produkt produkt : produkte) {
        summe = summe + produkt.getPreisInRappen() * produkt.getAnzahl();
    }

    return summe;
}
```

---

## Aufgabe 10 – Edge Cases bewusst ergänzen

Mögliche Lösung:

| Methode | Edge Case | Erwartetes Resultat | Warum ist der Fall wichtig? |
|---|---|---|---|
| `berechneRabattpreis` | `10000`, `0` | `10000` | Kein Rabatt darf den Preis nicht verändern. |
| `berechneRabattpreis` | `10000`, `100` | `0` | Voller Rabatt ist ein Randfall. |
| `berechneGesamtwert` | leeres Array | `0` | Keine Produkte dürfen keinen Fehler erzeugen. |
| `findeProdukt` | Name nicht vorhanden | `null` | Suchmethoden müssen nicht gefundene Werte sauber behandeln. |

Weitere sinnvolle Fälle:

- Produkt steht an erster Stelle
- Produkt steht an letzter Stelle
- Gesamtwert mit genau einem Produkt

---

## Aufgabe 11 – Produktverwaltung prüfbar machen

Eine vollständige, kleine Standardlösung kann so aussehen.

`Produkt.java`:

```java
package ch.allianz.youngoitv.produktverwaltung.model;

public class Produkt {
    private String name;
    private int preisInRappen;
    private int anzahl;

    public Produkt(String name, int preisInRappen, int anzahl) {
        this.name = name;
        this.preisInRappen = preisInRappen;
        this.anzahl = anzahl;
    }

    public String getName() {
        return name;
    }

    public int getPreisInRappen() {
        return preisInRappen;
    }

    public int getAnzahl() {
        return anzahl;
    }
}
```

`ProduktVerwaltung.java`:

```java
package ch.allianz.youngoitv.produktverwaltung.service;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;

public class ProduktVerwaltung {
    public int berechneRabattpreis(int preisInRappen, int rabattProzent) {
        int rabattBetrag = preisInRappen * rabattProzent / 100;
        return preisInRappen - rabattBetrag;
    }

    public int berechneGesamtwert(Produkt[] produkte) {
        int summe = 0;

        for (Produkt produkt : produkte) {
            summe = summe + produkt.getPreisInRappen() * produkt.getAnzahl();
        }

        return summe;
    }

    public Produkt findeProdukt(Produkt[] produkte, String name) {
        for (Produkt produkt : produkte) {
            if (produkt.getName().equals(name)) {
                return produkt;
            }
        }

        return null;
    }
}
```

`Main.java`:

```java
package ch.allianz.youngoitv.produktverwaltung;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;
import ch.allianz.youngoitv.produktverwaltung.service.ProduktVerwaltung;

public class Main {
    public static void main(String[] args) {
        int fehler = 0;

        if (!testeRabattberechnung()) {
            fehler++;
        }

        if (!testeGesamtwert()) {
            fehler++;
        }

        if (!testeProduktsuche()) {
            fehler++;
        }

        if (fehler == 0) {
            System.out.println("Alle Prüfungen erfolgreich.");
        } else {
            System.out.println("Anzahl Fehler: " + fehler);
        }
    }

    public static boolean testeRabattberechnung() {
        ProduktVerwaltung verwaltung = new ProduktVerwaltung();
        boolean ok = true;

        if (!pruefeInt("Rabatt 10 Prozent", 9000,
                verwaltung.berechneRabattpreis(10000, 10))) {
            ok = false;
        }

        if (!pruefeInt("Kein Rabatt", 10000,
                verwaltung.berechneRabattpreis(10000, 0))) {
            ok = false;
        }

        if (!pruefeInt("Voller Rabatt", 0,
                verwaltung.berechneRabattpreis(10000, 100))) {
            ok = false;
        }

        return ok;
    }

    public static boolean testeGesamtwert() {
        ProduktVerwaltung verwaltung = new ProduktVerwaltung();

        Produkt[] produkte = {
            new Produkt("Maus", 2500, 3),
            new Produkt("Tastatur", 7000, 2),
            new Produkt("Monitor", 19900, 1)
        };

        boolean ok = true;

        if (!pruefeInt("Gesamtwert", 41400,
                verwaltung.berechneGesamtwert(produkte))) {
            ok = false;
        }

        if (!pruefeInt("Leeres Produktarray", 0,
                verwaltung.berechneGesamtwert(new Produkt[0]))) {
            ok = false;
        }

        return ok;
    }

    public static boolean testeProduktsuche() {
        ProduktVerwaltung verwaltung = new ProduktVerwaltung();

        Produkt[] produkte = {
            new Produkt("Maus", 2500, 3),
            new Produkt("Tastatur", 7000, 2),
            new Produkt("Monitor", 19900, 1)
        };

        boolean ok = true;

        Produkt gefunden = verwaltung.findeProdukt(produkte, "Tastatur");
        if (gefunden != null) {
            System.out.println("OK: Tastatur gefunden");
        } else {
            System.out.println("FEHLER: Tastatur wurde nicht gefunden");
            ok = false;
        }

        Produkt nichtGefunden = verwaltung.findeProdukt(produkte, "Webcam");
        if (nichtGefunden == null) {
            System.out.println("OK: Webcam nicht gefunden");
        } else {
            System.out.println("FEHLER: Webcam sollte nicht gefunden werden");
            ok = false;
        }

        return ok;
    }

    public static boolean pruefeInt(String name, int erwartet, int tatsaechlich) {
        if (erwartet == tatsaechlich) {
            System.out.println("OK: " + name);
            return true;
        } else {
            System.out.println("FEHLER: " + name);
            System.out.println("Erwartet: " + erwartet);
            System.out.println("Tatsächlich: " + tatsaechlich);
            return false;
        }
    }
}
```

Antworten:

1. Bei korrekter Umsetzung kompiliert der Code mit `mvn compile`.
2. `berechneRabattpreis` ist meist am einfachsten zu prüfen, weil nur Zahlen verglichen werden.
3. `findeProdukt` braucht besonders den Edge Case «Produkt nicht vorhanden».

Typischer Fehler: Prüfcode und Fachlogik vermischen. Die Fachlogik gehört in `ProduktVerwaltung`; `Main` darf anzeigen und einfache Prüfungen starten.

---

## Aufgabe 12 – Vorbereitung für spätere Testautomatisierung

Mögliche Antworten:

1. Die Struktur ist hilfreich, weil kleine Methoden mit Rückgabewerten später direkt geprüft werden können.
2. Fachlogik soll nicht direkt in `main` stehen, weil `main` vor allem startet und koordiniert.
3. Rückgabewerte sind wichtiger als schöne Ausgaben, weil man Rückgabewerte direkt vergleichen kann.
4. Später wird der Vergleich zwischen erwartetem und tatsächlichem Resultat automatisiert.
5. Maven ist eine gute Grundlage, weil alle mit derselben Projektstruktur und denselben Befehlen arbeiten.

Merksatz:

```text
Automatisierte Tests ersetzen nicht die Testidee. Sie automatisieren den Vergleich.
```

---

## Verifikation

Die vollständige Standardlösung aus Aufgabe 11 wurde in einem temporären Maven-Projekt geprüft.

Ausgeführte Befehle:

```bash
mvn -q compile
java -cp target/classes ch.allianz.youngoitv.produktverwaltung.Main
```

Ergebnis:

```text
OK: Rabatt 10 Prozent
OK: Kein Rabatt
OK: Voller Rabatt
OK: Gesamtwert
OK: Leeres Produktarray
OK: Tastatur gefunden
OK: Webcam nicht gefunden
Alle Prüfungen erfolgreich.
```

Es wurden keine externen Dependencies, kein JUnit und keine Testbibliothek verwendet.
