# Übungen – Maven-Projekte mit einfachen Tests vorbereiten

## Vorwissen

Du brauchst:

- Maven-Grundstruktur mit `pom.xml` und `src/main/java`
- Klassen, Objekte, Arrays und einfache Methoden
- `if`/`else`, Rückgabewerte und Schleifen
- Produktverwaltung mit `Produkt` und `ProduktVerwaltung`

Noch nicht verwendet werden:

- JUnit
- externe Dependencies
- Maven Central
- Test-Annotationen
- Assertions-Bibliotheken
- Plugin-Details

---

## Basis

### Aufgabe 1 – Ausgabe oder Prüfung?

Lies die Beispiele und entscheide jeweils:

- Ist es nur eine Ausgabe?
- Oder wird erwartet mit tatsächlich verglichen?

Beispiel A:

```java
System.out.println(verwaltung.berechneRabattpreis(10000, 10));
```

Beispiel B:

```java
int erwartet = 9000;
int tatsaechlich = verwaltung.berechneRabattpreis(10000, 10);

if (erwartet == tatsaechlich) {
    System.out.println("OK");
} else {
    System.out.println("FEHLER");
}
```

Beispiel C:

```java
int gesamtwert = verwaltung.berechneGesamtwert(produkte);
System.out.println("Gesamtwert: " + gesamtwert);
```

Beantworte:

1. Welches Beispiel ist am besten prüfbar?
2. Warum reicht eine sichtbare Ausgabe allein nicht?
3. Wo steht im Code das erwartete Resultat?

---

### Aufgabe 2 – Erwartete Resultate formulieren

Ergänze die erwarteten Resultate.

Methode:

```java
public int berechneRabattpreis(int preisInRappen, int rabattProzent)
```

Tabelle:

| Eingabe `preisInRappen` | Eingabe `rabattProzent` | Erwartetes Resultat |
|---:|---:|---:|
| `10000` | `10` | |
| `10000` | `0` | |
| `10000` | `100` | |
| `2500` | `20` | |

Beantworte zusätzlich:

1. Welcher Fall ist ein Normalfall?
2. Welche Fälle sind Edge Cases?

---

### Aufgabe 3 – Eine Methode manuell prüfen

Gegeben ist diese Methode:

```java
public int berechneRabattpreis(int preisInRappen, int rabattProzent) {
    int rabattBetrag = preisInRappen * rabattProzent / 100;
    return preisInRappen - rabattBetrag;
}
```

Schreibe in `main` eine einfache Prüfung mit:

- `erwartet`
- `tatsaechlich`
- `if`/`else`
- einer `OK`-Ausgabe
- einer `FEHLER`-Ausgabe mit erwartetem und tatsächlichem Resultat

Verwende diesen Testfall:

```text
preisInRappen: 10000
rabattProzent: 10
erwartet: 9000
```

---

## Aufbau

### Aufgabe 4 – Mehrere Testfälle mit `if`/`else`

Erstelle eine Hilfsmethode:

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

Nutze sie für diese drei Prüfungen:

| Name | Aufruf | Erwartet |
|---|---|---:|
| `Rabatt 10 Prozent` | `berechneRabattpreis(10000, 10)` | `9000` |
| `Kein Rabatt` | `berechneRabattpreis(10000, 0)` | `10000` |
| `Voller Rabatt` | `berechneRabattpreis(10000, 100)` | `0` |

Beantworte danach:

1. Warum ist die Hilfsmethode besser als drei einzelne `System.out.println`-Ausgaben?
2. Welche Information hilft bei einem Fehler besonders?

---

### Aufgabe 5 – Suche nach Produkt prüfen

Gegeben ist diese Methode:

```java
public Produkt findeProdukt(Produkt[] produkte, String name) {
    for (Produkt produkt : produkte) {
        if (produkt.getName().equals(name)) {
            return produkt;
        }
    }

    return null;
}
```

Erstelle ein kleines Produktarray:

```java
Produkt[] produkte = {
    new Produkt("Maus", 2500, 3),
    new Produkt("Tastatur", 7000, 2),
    new Produkt("Monitor", 19900, 1)
};
```

Prüfe zwei Fälle:

1. `findeProdukt(produkte, "Tastatur")` soll ein Produkt zurückgeben.
2. `findeProdukt(produkte, "Webcam")` soll `null` zurückgeben.

Hinweis: Für diese Aufgabe darfst du mit `if` prüfen, ob der Rückgabewert `null` ist.

---

### Aufgabe 6 – Gesamtwert prüfen

Gegeben ist diese Methode:

```java
public int berechneGesamtwert(Produkt[] produkte) {
    int summe = 0;

    for (Produkt produkt : produkte) {
        summe = summe + produkt.getPreisInRappen() * produkt.getAnzahl();
    }

    return summe;
}
```

Verwende dieses Array:

```java
Produkt[] produkte = {
    new Produkt("Maus", 2500, 3),
    new Produkt("Tastatur", 7000, 2),
    new Produkt("Monitor", 19900, 1)
};
```

Berechne zuerst von Hand den erwarteten Gesamtwert.

Prüfe danach mit `pruefeInt`:

```java
int erwartet = ...;
int tatsaechlich = verwaltung.berechneGesamtwert(produkte);
pruefeInt("Gesamtwert", erwartet, tatsaechlich);
```

---

## Vertiefung

### Aufgabe 7 – Fachlogik aus `main` herauslösen

Ausgangscode:

```java
public class Main {
    public static void main(String[] args) {
        int preisInRappen = 10000;
        int rabattProzent = 10;

        int rabattBetrag = preisInRappen * rabattProzent / 100;
        int rabattpreis = preisInRappen - rabattBetrag;

        System.out.println(rabattpreis);
    }
}
```

Auftrag:

1. Erstelle in `ProduktVerwaltung` eine Methode `berechneRabattpreis`.
2. Die Methode erhält `preisInRappen` und `rabattProzent` als Parameter.
3. Die Methode gibt den Rabattpreis zurück.
4. `main` ruft nur noch die Methode auf und gibt das Resultat aus.
5. Ergänze eine einfache Prüfung mit erwartetem und tatsächlichem Resultat.

Ziel:

```text
Die Berechnung ist nicht mehr direkt in main versteckt.
```

---

### Aufgabe 8 – Testmethoden mit Rückgabewert schreiben

Schreibe zwei Testmethoden:

```java
public static boolean testeRabattberechnung()
```

```java
public static boolean testeGesamtwert()
```

Jede Testmethode soll:

- die benötigten Objekte erstellen
- erwartete Resultate festlegen
- tatsächliche Resultate berechnen
- mit `if`/`else` vergleichen
- `true` bei Erfolg zurückgeben
- `false` bei Fehler zurückgeben

In `main` sollen beide Testmethoden aufgerufen werden. Am Schluss soll ausgegeben werden:

```text
Alle Prüfungen erfolgreich.
```

oder:

```text
Anzahl Fehler: ...
```

---

### Aufgabe 9 – Typischen Fehler finden

Ein Lernender schreibt:

```java
public void berechneGesamtwert(Produkt[] produkte) {
    int summe = 0;

    for (Produkt produkt : produkte) {
        summe = summe + produkt.getPreisInRappen() * produkt.getAnzahl();
    }

    System.out.println(summe);
}
```

Beantworte:

1. Warum ist diese Methode schlechter prüfbar?
2. Welcher Rückgabetyp wäre passender?
3. Wie müsste die letzte Zeile geändert werden?
4. Was sollte `main` danach tun?

---

## Transfer

### Aufgabe 10 – Edge Cases bewusst ergänzen

Ergänze mindestens vier Edge Cases für die Produktverwaltung.

Nutze diese Tabelle:

| Methode | Edge Case | Erwartetes Resultat | Warum ist der Fall wichtig? |
|---|---|---|---|
| `berechneRabattpreis` | | | |
| `berechneRabattpreis` | | | |
| `berechneGesamtwert` | | | |
| `findeProdukt` | | | |

Mögliche Ideen:

- `0` Prozent Rabatt
- `100` Prozent Rabatt
- leeres Produktarray
- Produktname nicht vorhanden
- Produkt steht an erster Stelle
- Produkt steht an letzter Stelle

---

### Aufgabe 11 – Produktverwaltung prüfbar machen

Überarbeite eine bestehende Produktverwaltung so, dass diese Methoden prüfbar sind:

Falls du kein eigenes Projekt vorliegen hast, verwende die Struktur aus dem Arbeitsblatt:

```text
produktverwaltung-maven/
  pom.xml
  src/main/java/
    ch/allianz/youngoitv/produktverwaltung/
      Main.java
      model/Produkt.java
      service/ProduktVerwaltung.java
```

```java
public int berechneRabattpreis(int preisInRappen, int rabattProzent)
```

```java
public int berechneGesamtwert(Produkt[] produkte)
```

```java
public Produkt findeProdukt(Produkt[] produkte, String name)
```

Regeln:

- Die Methoden geben Resultate zurück.
- Die Methoden geben nicht direkt mit `System.out.println` aus.
- `main` darf Resultate anzeigen.
- Prüfcode vergleicht erwartete und tatsächliche Resultate.

Führe danach im Projektordner aus:

```bash
mvn compile
```

Beantworte:

1. Wurde der Code erfolgreich kompiliert?
2. Welche Methode war am einfachsten zu prüfen?
3. Welche Methode braucht einen Edge Case?

---

## Reflexion

### Aufgabe 12 – Vorbereitung für spätere Testautomatisierung

Beantworte in eigenen Worten:

1. Warum ist diese Struktur später hilfreich, wenn Tests automatisiert werden?
2. Warum soll Fachlogik nicht direkt in `main` stehen?
3. Warum sind klare Rückgabewerte wichtiger als schöne Konsolenausgaben?
4. Was wird später automatisiert, das wir hier noch von Hand mit `if`/`else` machen?
5. Warum ist Maven als standardisiertes Werkzeug dafür eine gute Grundlage?
