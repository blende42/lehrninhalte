# Lösungen – Algorithmen und Datenstrukturen

## Aufgabe 1 – Array ausgeben

```java
public static void gibAus(int[] zahlen) {
    for (int i = 0; i < zahlen.length; i++) {
        System.out.print(zahlen[i] + " ");
    }

    System.out.println();
}
```

## Aufgabe 2 – Lineare Suche

```java
public static boolean enthaelt(int[] zahlen, int gesucht) {
    for (int i = 0; i < zahlen.length; i++) {
        if (zahlen[i] == gesucht) {
            return true;
        }
    }

    return false;
}
```

## Aufgabe 3 – Minimum und Maximum

```java
public static int findeMinimum(int[] zahlen) {
    int minimum = zahlen[0];

    for (int i = 1; i < zahlen.length; i++) {
        if (zahlen[i] < minimum) {
            minimum = zahlen[i];
        }
    }

    return minimum;
}
```

```java
public static int findeMaximum(int[] zahlen) {
    int maximum = zahlen[0];

    for (int i = 1; i < zahlen.length; i++) {
        if (zahlen[i] > maximum) {
            maximum = zahlen[i];
        }
    }

    return maximum;
}
```

## Aufgabe 4 – Werte zählen

```java
public static int zaehleMindestens(int[] zahlen, int grenze) {
    int anzahl = 0;

    for (int i = 0; i < zahlen.length; i++) {
        if (zahlen[i] >= grenze) {
            anzahl++;
        }
    }

    return anzahl;
}
```

## Aufgabe 5 – Bubble Sort

```java
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
```

## Aufgabe 6 – Selection Sort

```java
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
```

## Aufgabe 7 – Absteigend sortieren

```java
public static void bubbleSortAbsteigend(int[] zahlen) {
    for (int durchlauf = 0; durchlauf < zahlen.length - 1; durchlauf++) {
        for (int i = 0; i < zahlen.length - 1 - durchlauf; i++) {
            if (zahlen[i] < zahlen[i + 1]) {
                int temp = zahlen[i];
                zahlen[i] = zahlen[i + 1];
                zahlen[i + 1] = temp;
            }
        }
    }
}
```

## Aufgabe 8 – Sortierung prüfen

```java
public static boolean istAufsteigendSortiert(int[] zahlen) {
    for (int i = 0; i < zahlen.length - 1; i++) {
        if (zahlen[i] > zahlen[i + 1]) {
            return false;
        }
    }

    return true;
}
```

Ein leeres Array und ein Array mit einem Element ergeben automatisch `true`, weil die Schleife nicht ausgeführt wird.

## Aufgabe 9 – Vergleiche zählen

```java
public static int bubbleSortUndZaehleVergleiche(int[] zahlen) {
    int vergleiche = 0;

    for (int durchlauf = 0; durchlauf < zahlen.length - 1; durchlauf++) {
        for (int i = 0; i < zahlen.length - 1 - durchlauf; i++) {
            vergleiche++;

            if (zahlen[i] > zahlen[i + 1]) {
                int temp = zahlen[i];
                zahlen[i] = zahlen[i + 1];
                zahlen[i + 1] = temp;
            }
        }
    }

    return vergleiche;
}
```

## Aufgabe 10 – Preise sortieren

```java
public static void selectionSort(double[] preise) {
    for (int start = 0; start < preise.length - 1; start++) {
        int indexMinimum = start;

        for (int i = start + 1; i < preise.length; i++) {
            if (preise[i] < preise[indexMinimum]) {
                indexMinimum = i;
            }
        }

        double temp = preise[start];
        preise[start] = preise[indexMinimum];
        preise[indexMinimum] = temp;
    }
}
```

## Aufgabe 11 – Produktarray nach Preis sortieren

```java
public static void sortiereNachPreis(Produkt[] produkte) {
    for (int start = 0; start < produkte.length - 1; start++) {
        int indexMinimum = start;

        for (int i = start + 1; i < produkte.length; i++) {
            if (produkte[i].getPreis() < produkte[indexMinimum].getPreis()) {
                indexMinimum = i;
            }
        }

        Produkt temp = produkte[start];
        produkte[start] = produkte[indexMinimum];
        produkte[indexMinimum] = temp;
    }
}
```

Hinweis: Beim Sortieren von Objekten wird das ganze Objekt getauscht. Sonst passen Name und Preis nicht mehr zuverlässig zusammen.

## Aufgabe 12 – Zinseszins mit Schleife

```java
public static double berechneKapital(double startkapital, double zinssatz, int jahre) {
    double kapital = startkapital;

    for (int jahr = 1; jahr <= jahre; jahr++) {
        double zins = kapital * zinssatz / 100;
        kapital = kapital + zins;
    }

    return kapital;
}
```

Test mit Zwischenausgabe:

```java
double kapital = 1000.0;

for (int jahr = 1; jahr <= 3; jahr++) {
    double zins = kapital * 2.0 / 100;
    kapital = kapital + zins;
    System.out.println("Jahr " + jahr + ": " + kapital);
}
```

## Aufgabe 13 – Pensionskassenkapital simulieren

```java
public class PensionskassenSimulation {
    public static void main(String[] args) {
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

        double arbeitnehmerSatz = ermittleArbeitnehmerSatz(alter, variante);
        double arbeitgeberSatz = ermittleArbeitgeberSatz(alter);

        double arbeitnehmerBeitrag = lohn * arbeitnehmerSatz / 100;
        double arbeitgeberBeitrag = lohn * arbeitgeberSatz / 100;

        return kapital + arbeitnehmerBeitrag + arbeitgeberBeitrag;
    }

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

Das Programm kann so ausgeführt werden:

```bash
javac PensionskassenSimulation.java
java PensionskassenSimulation > pensionskasse.csv
```

Die Datei `pensionskasse.csv` kann danach in Excel geöffnet werden. Für das Diagramm eignen sich `Alter` als X-Achse und `Mini`, `Standard`, `Maxi` als Datenreihen.
