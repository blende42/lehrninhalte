# Lösungen – 2D Arrays

## Aufgabe 1 – Ausgabe
```java
for (int i = 0; i < messwerte.length; i++) {
    for (int j = 0; j < messwerte[i].length; j++) {
        System.out.println(messwerte[i][j]);
    }
}
```

## Aufgabe 2 – Summe pro Zeile
```java
for (int i = 0; i < messwerte.length; i++) {
    int summe = 0;
    for (int j = 0; j < messwerte[i].length; j++) {
        summe += messwerte[i][j];
    }
    System.out.println(summe);
}
```

## Aufgabe 3 – Durchschnitt pro Zeile
```java
for (int i = 0; i < messwerte.length; i++) {
    int summe = 0;
    for (int j = 0; j < messwerte[i].length; j++) {
        summe += messwerte[i][j];
    }
    double avg = (double) summe / messwerte[i].length;
    System.out.println(avg);
}
```

## Aufgabe 4 – Gesamtmaximum
```java
int max = messwerte[0][0];

for (int i = 0; i < messwerte.length; i++) {
    for (int j = 0; j < messwerte[i].length; j++) {
        if (messwerte[i][j] > max) {
            max = messwerte[i][j];
        }
    }
}
```

## Aufgabe 5 – Gesamtdurchschnitt
```java
int summe = 0;
int count = 0;

for (int i = 0; i < messwerte.length; i++) {
    for (int j = 0; j < messwerte[i].length; j++) {
        summe += messwerte[i][j];
        count++;
    }
}

double avg = (double) summe / count;
```

## Aufgabe 6 – Beste Messreihe
```java
int bestIndex = -1;
double bestAvg = 0;

for (int i = 0; i < messwerte.length; i++) {
    int summe = 0;
    for (int j = 0; j < messwerte[i].length; j++) {
        summe += messwerte[i][j];
    }
    double avg = (double) summe / messwerte[i].length;

    if (bestIndex == -1 || avg > bestAvg) {
        bestAvg = avg;
        bestIndex = i;
    }
}
```

## Aufgabe 8 – Edge Case lösen
```java
for (int i = 0; i < messwerte.length; i++) {
    if (messwerte[i].length == 0) continue;

    int summe = 0;
    for (int j = 0; j < messwerte[i].length; j++) {
        summe += messwerte[i][j];
    }
}
```
