# Lösungen – Java-Packages

## Aufgabe 1 – Package und Ordner zuordnen

Korrekt ist:

```text
src/ch/allianz/youngoitv/produktverwaltung/model/
```

Die Package-Deklaration

```java
package ch.allianz.youngoitv.produktverwaltung.model;
```

entspricht der Ordnerstruktur `ch/allianz/youngoitv/produktverwaltung/model`.

## Aufgabe 2 – Package-Deklarationen

```java
package ch.allianz.youngoitv.produktverwaltung;
```

```java
package ch.allianz.youngoitv.produktverwaltung.model;
```

```java
package ch.allianz.youngoitv.produktverwaltung.service;
```

## Aufgabe 3 – Konvention prüfen

Passend sind:

```text
ch.allianz.youngoitv.produktverwaltung
ch.allianz.youngoitv.produktverwaltung.service
```

Nicht passend:

- `ch.Allianz.YoungOITV.Produktverwaltung`, weil Package-Namen klein geschrieben werden.
- `ch.allianz.youngoitv.produkt-verwaltung`, weil Bindestriche in Package-Namen nicht verwendet werden.

## Aufgabe 4 – Produkt.java

Datei:

```text
src/ch/allianz/youngoitv/produktverwaltung/model/Produkt.java
```

```java
package ch.allianz.youngoitv.produktverwaltung.model;

public class Produkt {
    private String name;
    private double preis;

    public Produkt(String name, double preis) {
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

## Aufgabe 5 – ProduktVerwaltung.java

Datei:

```text
src/ch/allianz/youngoitv/produktverwaltung/service/ProduktVerwaltung.java
```

```java
package ch.allianz.youngoitv.produktverwaltung.service;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;
import java.util.ArrayList;

public class ProduktVerwaltung {
    private ArrayList<Produkt> produkte = new ArrayList<>();

    public void hinzufuegen(Produkt produkt) {
        produkte.add(produkt);
    }

    public void gibAlleAus() {
        for (int i = 0; i < produkte.size(); i++) {
            produkte.get(i).ausgeben();
        }
    }

    public double berechneGesamtwert() {
        double summe = 0.0;

        for (int i = 0; i < produkte.size(); i++) {
            summe += produkte.get(i).getPreis();
        }

        return summe;
    }

    public Produkt findeProdukt(String name) {
        for (int i = 0; i < produkte.size(); i++) {
            if (produkte.get(i).getName().equals(name)) {
                return produkte.get(i);
            }
        }

        return null;
    }
}
```

## Aufgabe 6 – Main.java

Datei:

```text
src/ch/allianz/youngoitv/produktverwaltung/Main.java
```

```java
package ch.allianz.youngoitv.produktverwaltung;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;
import ch.allianz.youngoitv.produktverwaltung.service.ProduktVerwaltung;

public class Main {
    public static void main(String[] args) {
        ProduktVerwaltung verwaltung = new ProduktVerwaltung();

        verwaltung.hinzufuegen(new Produkt("Tastatur", 49.90));
        verwaltung.hinzufuegen(new Produkt("Monitor", 179.00));
        verwaltung.hinzufuegen(new Produkt("Maus", 24.50));

        verwaltung.gibAlleAus();
        System.out.println("Gesamtwert: " + verwaltung.berechneGesamtwert());

        Produkt gefunden = verwaltung.findeProdukt("Maus");
        if (gefunden != null) {
            System.out.println("Gefunden:");
            gefunden.ausgeben();
        }
    }
}
```

## Aufgabe 7 – Fehler finden

Die Datei liegt im Ordner `model`, deshalb muss die Package-Deklaration so lauten:

```java
package ch.allianz.youngoitv.produktverwaltung.model;
```

## Aufgabe 8 – Ohne Maven kompilieren

Aus dem Projektordner:

```bash
mkdir -p out
javac -d out $(find src -name "*.java")
java -cp out ch.allianz.youngoitv.produktverwaltung.Main
```

`-d out` sorgt dafür, dass die `.class`-Dateien nicht in `src`, sondern in `out` entstehen.

## Aufgabe 9 – Classpath erklären

`-cp out` sagt Java, dass die kompilierten Klassen im Ordner `out` gesucht werden.

Am Schluss steht kein Dateipfad, sondern der vollständige Klassenname:

```text
ch.allianz.youngoitv.produktverwaltung.Main
```

`java Main` reicht nicht, weil `Main` in einem Package liegt. Der Package-Name gehört zum vollständigen Klassennamen.

## Aufgabe 10 – Kundenverwaltung

Eine mögliche Lösung verwendet dieselbe Struktur wie die Produktverwaltung.

```text
src/ch/allianz/youngoitv/kundenverwaltung/
  Main.java
  model/Kunde.java
  service/KundenVerwaltung.java
```

Wichtig ist nicht der genaue Inhalt der Verwaltung, sondern dass Package-Deklarationen, Ordnerstruktur, Imports und Startbefehl zusammenpassen.

Startbefehl:

```bash
java -cp out ch.allianz.youngoitv.kundenverwaltung.Main
```

Hinweis: Bei mehrdateiligen Projekten trennt `src` den Quellcode von `out`, den erzeugten `.class`-Dateien. Dadurch bleibt sichtbar, welche Dateien von Menschen geschrieben und welche vom Compiler erzeugt wurden.

## Aufgabe 11 – Algorithmen in Packages aufteilen

### ArrayAlgorithmen.java

Datei:

```text
src/ch/allianz/youngoitv/algorithmen/algorithms/ArrayAlgorithmen.java
```

```java
package ch.allianz.youngoitv.algorithmen.algorithms;

public class ArrayAlgorithmen {
    public static boolean enthaelt(int[] zahlen, int gesucht) {
        for (int i = 0; i < zahlen.length; i++) {
            if (zahlen[i] == gesucht) {
                return true;
            }
        }

        return false;
    }

    public static int findeMinimum(int[] zahlen) {
        int minimum = zahlen[0];

        for (int i = 1; i < zahlen.length; i++) {
            if (zahlen[i] < minimum) {
                minimum = zahlen[i];
            }
        }

        return minimum;
    }

    public static int findeMaximum(int[] zahlen) {
        int maximum = zahlen[0];

        for (int i = 1; i < zahlen.length; i++) {
            if (zahlen[i] > maximum) {
                maximum = zahlen[i];
            }
        }

        return maximum;
    }

    public static int zaehleMindestens(int[] zahlen, int grenze) {
        int anzahl = 0;

        for (int i = 0; i < zahlen.length; i++) {
            if (zahlen[i] >= grenze) {
                anzahl++;
            }
        }

        return anzahl;
    }
}
```

### SortierAlgorithmen.java

Datei:

```text
src/ch/allianz/youngoitv/algorithmen/algorithms/SortierAlgorithmen.java
```

```java
package ch.allianz.youngoitv.algorithmen.algorithms;

public class SortierAlgorithmen {
    public static void bubbleSort(int[] zahlen) {
        for (int durchlauf = 0; durchlauf < zahlen.length - 1; durchlauf++) {
            for (int i = 0; i < zahlen.length - 1 - durchlauf; i++) {
                if (zahlen[i] > zahlen[i + 1]) {
                    int temp = zahlen[i];
                    zahlen[i] = zahlen[i + 1];
                    zahlen[i + 1] = temp;
                }
            }
        }
    }

    public static void selectionSort(int[] zahlen) {
        for (int start = 0; start < zahlen.length - 1; start++) {
            int indexMinimum = start;

            for (int i = start + 1; i < zahlen.length; i++) {
                if (zahlen[i] < zahlen[indexMinimum]) {
                    indexMinimum = i;
                }
            }

            int temp = zahlen[start];
            zahlen[start] = zahlen[indexMinimum];
            zahlen[indexMinimum] = temp;
        }
    }
}
```

### Main.java

Datei:

```text
src/ch/allianz/youngoitv/algorithmen/Main.java
```

```java
package ch.allianz.youngoitv.algorithmen;

import ch.allianz.youngoitv.algorithmen.algorithms.ArrayAlgorithmen;
import ch.allianz.youngoitv.algorithmen.algorithms.SortierAlgorithmen;

public class Main {
    public static void main(String[] args) {
        int[] zahlen = {5, 2, 8, 1};

        System.out.println("Minimum: " + ArrayAlgorithmen.findeMinimum(zahlen));
        System.out.println("Maximum: " + ArrayAlgorithmen.findeMaximum(zahlen));
        System.out.println("Enthaelt 8: " + ArrayAlgorithmen.enthaelt(zahlen, 8));
        System.out.println("Mindestens 5: " + ArrayAlgorithmen.zaehleMindestens(zahlen, 5));

        SortierAlgorithmen.bubbleSort(zahlen);
        gibAus(zahlen);
    }

    public static void gibAus(int[] zahlen) {
        for (int i = 0; i < zahlen.length; i++) {
            System.out.print(zahlen[i] + " ");
        }

        System.out.println();
    }
}
```

Kompilieren und starten:

```bash
mkdir -p out
javac -d out $(find src -name "*.java")
java -cp out ch.allianz.youngoitv.algorithmen.Main
```

Erwartete Ausgabe:

```text
Minimum: 1
Maximum: 8
Enthaelt 8: true
Mindestens 5: 2
1 2 5 8
```

## Aufgabe 12 – Pensionskassen-Simulation in Packages aufteilen

### Beitragssaetze.java

Datei:

```text
src/ch/allianz/youngoitv/pensionskasse/service/Beitragssaetze.java
```

```java
package ch.allianz.youngoitv.pensionskasse.service;

public class Beitragssaetze {
    public static double ermittleArbeitnehmerSatz(int alter, String variante) {
        if (alter >= 20 && alter <= 24) {
            return variante.equals("Maxi") ? 6.00 : 4.00;
        } else if (alter >= 25 && alter <= 29) {
            return variante.equals("Maxi") ? 6.35 : 4.35;
        } else if (alter >= 30 && alter <= 34) {
            return variante.equals("Maxi") ? 6.70 : 4.70;
        } else if (alter >= 35 && alter <= 39) {
            return variante.equals("Maxi") ? 7.80 : 5.80;
        } else if (alter >= 40 && alter <= 44) {
            return variante.equals("Maxi") ? 8.90 : 6.90;
        } else if (alter >= 45 && alter <= 49) {
            if (variante.equals("Mini")) {
                return 7.60;
            } else if (variante.equals("Standard")) {
                return 8.00;
            }
            return 10.00;
        } else if (alter >= 50 && alter <= 54) {
            if (variante.equals("Mini")) {
                return 7.60;
            } else if (variante.equals("Standard")) {
                return 9.10;
            }
            return 11.10;
        } else if (alter >= 55 && alter <= 59) {
            if (variante.equals("Mini")) {
                return 7.60;
            } else if (variante.equals("Standard")) {
                return 10.20;
            }
            return 12.20;
        } else if (alter >= 60 && alter <= 65) {
            if (variante.equals("Mini")) {
                return 7.60;
            } else if (variante.equals("Standard")) {
                return 11.30;
            }
            return 13.30;
        }

        return 0.0;
    }

    public static double ermittleArbeitgeberSatz(int alter) {
        if (alter >= 20 && alter <= 24) {
            return 6.00;
        } else if (alter >= 25 && alter <= 29) {
            return 6.40;
        } else if (alter >= 30 && alter <= 34) {
            return 7.80;
        } else if (alter >= 35 && alter <= 39) {
            return 9.20;
        } else if (alter >= 40 && alter <= 44) {
            return 10.60;
        } else if (alter >= 45 && alter <= 49) {
            return 12.00;
        } else if (alter >= 50 && alter <= 54) {
            return 13.40;
        } else if (alter >= 55 && alter <= 59) {
            return 14.80;
        } else if (alter >= 60 && alter <= 65) {
            return 16.20;
        }

        return 0.0;
    }
}
```

### PensionskassenSimulation.java

Datei:

```text
src/ch/allianz/youngoitv/pensionskasse/simulation/PensionskassenSimulation.java
```

```java
package ch.allianz.youngoitv.pensionskasse.simulation;

import ch.allianz.youngoitv.pensionskasse.service.Beitragssaetze;

public class PensionskassenSimulation {
    public static void starte() {
        int startAlter = 20;
        int endAlter = 65;

        double[] jahresloehne = erstelleJahresloehne(startAlter, endAlter);
        double[] zinssaetze = erstelleZinssaetze(startAlter, endAlter);

        double kapitalMini = 0.0;
        double kapitalStandard = 0.0;
        double kapitalMaxi = 0.0;

        System.out.println("Alter;Lohn;Zins;Mini;Standard;Maxi");

        for (int alter = startAlter; alter <= endAlter; alter++) {
            int index = alter - startAlter;
            double lohn = jahresloehne[index];
            double zins = zinssaetze[index];

            kapitalMini = berechneNeuesKapital(kapitalMini, lohn, zins, alter, "Mini");
            kapitalStandard = berechneNeuesKapital(kapitalStandard, lohn, zins, alter, "Standard");
            kapitalMaxi = berechneNeuesKapital(kapitalMaxi, lohn, zins, alter, "Maxi");

            System.out.println(alter + ";" + lohn + ";" + zins + ";"
                    + kapitalMini + ";" + kapitalStandard + ";" + kapitalMaxi);
        }
    }

    public static double berechneNeuesKapital(
            double kapital,
            double lohn,
            double zins,
            int alter,
            String variante
    ) {
        kapital = kapital + kapital * zins / 100;

        double arbeitnehmerSatz = Beitragssaetze.ermittleArbeitnehmerSatz(alter, variante);
        double arbeitgeberSatz = Beitragssaetze.ermittleArbeitgeberSatz(alter);

        double arbeitnehmerBeitrag = lohn * arbeitnehmerSatz / 100;
        double arbeitgeberBeitrag = lohn * arbeitgeberSatz / 100;

        return kapital + arbeitnehmerBeitrag + arbeitgeberBeitrag;
    }

    public static double[] erstelleJahresloehne(int startAlter, int endAlter) {
        double[] jahresloehne = new double[endAlter - startAlter + 1];

        for (int i = 0; i < jahresloehne.length; i++) {
            jahresloehne[i] = 52000.0 + i * 900.0;
        }

        return jahresloehne;
    }

    public static double[] erstelleZinssaetze(int startAlter, int endAlter) {
        double[] zinssaetze = new double[endAlter - startAlter + 1];

        for (int i = 0; i < zinssaetze.length; i++) {
            if (i % 3 == 0) {
                zinssaetze[i] = 1.0;
            } else if (i % 3 == 1) {
                zinssaetze[i] = 1.5;
            } else {
                zinssaetze[i] = 2.0;
            }
        }

        return zinssaetze;
    }
}
```

### Main.java

Datei:

```text
src/ch/allianz/youngoitv/pensionskasse/Main.java
```

```java
package ch.allianz.youngoitv.pensionskasse;

import ch.allianz.youngoitv.pensionskasse.simulation.PensionskassenSimulation;

public class Main {
    public static void main(String[] args) {
        PensionskassenSimulation.starte();
    }
}
```

Kompilieren:

```bash
mkdir -p out
javac -d out $(find src -name "*.java")
```

Starten und CSV erzeugen:

```bash
java -cp out ch.allianz.youngoitv.pensionskasse.Main > pensionskasse.csv
```

Die CSV-Datei enthält eine Kopfzeile und je eine Zeile für Alter `20` bis `65`.

### Sichtbarkeit

`Main` muss `public` sein, weil sie die Startklasse ist.

`PensionskassenSimulation` muss `public` sein, weil `Main` sie aus einem anderen Package verwendet.

`Beitragssaetze` muss `public` sein, weil `PensionskassenSimulation` sie aus einem anderen Package importiert.

Diese Methoden müssen in der gezeigten Lösung `public` sein:

- `PensionskassenSimulation.starte()`
- `Beitragssaetze.ermittleArbeitnehmerSatz(...)`
- `Beitragssaetze.ermittleArbeitgeberSatz(...)`

Hilfsmethoden wie `berechneNeuesKapital`, `erstelleJahresloehne` und `erstelleZinssaetze` könnten auch `private` sein, wenn sie nur innerhalb von `PensionskassenSimulation` verwendet werden.

Kein Modifier wäre möglich, wenn eine Klasse oder Methode nur innerhalb desselben Packages verwendet wird. Sobald eine andere Klasse aus einem anderen Package zugreifen muss, reicht package-private nicht mehr.
