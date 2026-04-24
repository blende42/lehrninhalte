# Lösungen – Arrays

## Aufgabe 3 – Summe
```java
int summe = 0;
for (int i = 0; i < zahlen.length; i++) {
    summe += zahlen[i];
}
```

## Aufgabe 4 – Maximum
```java
int max = zahlen[0];
for (int i = 1; i < zahlen.length; i++) {
    if (zahlen[i] > max) {
        max = zahlen[i];
    }
}
```

## Aufgabe 5 – Zählen
```java
int count = 0;
for (int i = 0; i < zahlen.length; i++) {
    if (zahlen[i] > 5) {
        count++;
    }
}
```

## Aufgabe 6 – Suche
```java
boolean gefunden = false;
for (int i = 0; i < zahlen.length; i++) {
    if (zahlen[i] == 7) {
        gefunden = true;
    }
}
```

## Aufgabe 7 – Index
```java
int index = -1;
for (int i = 0; i < zahlen.length; i++) {
    if (zahlen[i] == 7) {
        index = i;
    }
}
```

## Aufgabe 8 – Temperaturen
```java
int max = temperaturen[0];
int min = temperaturen[0];
int summe = 0;

for (int i = 0; i < temperaturen.length; i++) {
    if (temperaturen[i] > max) max = temperaturen[i];
    if (temperaturen[i] < min) min = temperaturen[i];
    summe += temperaturen[i];
}

double durchschnitt = (double) summe / temperaturen.length;
```

## Aufgabe 9 – Noten
```java
int summe = 0;
int count = 0;

for (int i = 0; i < noten.length; i++) {
    summe += noten[i];
    if (noten[i] >= 5) {
        count++;
    }
}

double durchschnitt = (double) summe / noten.length;
```
