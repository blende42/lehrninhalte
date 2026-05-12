# Übungen – Von manuellen Tests zu automatisierten Tests mit JUnit

## Vorwissen

Du brauchst:

- Maven-Grundstruktur mit `pom.xml`, `src/main/java` und Package-Struktur
- Produktverwaltung mit `Produkt` und `ProduktVerwaltung`
- kleine Methoden mit Rückgabewerten
- manuelle Prüfungen mit erwartetem und tatsächlichem Resultat

Neu in diesen Übungen:

- JUnit Jupiter
- `src/test/java`
- `@Test`
- `assertEquals`
- `mvn test`

Nicht verwendet werden:

- Mocking
- Parameterized Tests
- Test Doubles
- Spring Tests
- Lifecycle-Methoden
- komplexe Plugin-Konfiguration

---

## Vorbereitung

Lege in deinem Maven-Projekt diese Struktur an:

```text
produktverwaltung-maven/
  pom.xml
  src/main/java/
    ch/allianz/youngoitv/produktverwaltung/
      Main.java
      model/Produkt.java
      service/ProduktVerwaltung.java
  src/test/java/
    ch/allianz/youngoitv/produktverwaltung/
      service/ProduktVerwaltungTest.java
```

Ergänze in `pom.xml` die JUnit-Dependency und die einfache Surefire-Versionseintragung aus dem Arbeitsblatt.

Starte Maven immer im Ordner, in dem die passende `pom.xml` liegt.

---

## Basis

### Aufgabe 1 – Manuelle Prüfung in JUnit umwandeln

Gegeben ist diese manuelle Prüfung:

```java
ProduktVerwaltung verwaltung = new ProduktVerwaltung();

int erwartet = 9000;
int tatsaechlich = verwaltung.berechneRabattpreis(10000, 10);

if (erwartet == tatsaechlich) {
    System.out.println("Test erfolgreich");
} else {
    System.out.println("Test fehlgeschlagen");
}
```

Schreibe daraus eine JUnit-Testmethode:

- Testklasse: `ProduktVerwaltungTest`
- Methode: `berechneRabattpreis_mitZehnProzent_liefertReduziertenPreis`
- Annotation: `@Test`
- Prüfung: `assertEquals(erwartet, tatsaechlich)`

Startgerüst:

```java
package ch.allianz.youngoitv.produktverwaltung.service;

import org.junit.jupiter.api.Test;

import static org.junit.jupiter.api.Assertions.assertEquals;

class ProduktVerwaltungTest {

    @Test
    void berechneRabattpreis_mitZehnProzent_liefertReduziertenPreis() {
        ProduktVerwaltung verwaltung = new ProduktVerwaltung();

        int erwartet = 9000;
        int tatsaechlich = verwaltung.berechneRabattpreis(10000, 10);

        // hier pruefen
    }
}
```

Erwartung:

```text
mvn test läuft erfolgreich durch.
```

---

### Aufgabe 2 – Erwartet und tatsächlich sichtbar machen

Ergänze in deiner Testmethode bewusst zwei Variablen:

```java
int erwartet = ...;
int tatsaechlich = ...;
```

Beantworte danach schriftlich:

1. Welcher Wert steht für das fachlich erwartete Resultat?
2. Welcher Wert kommt aus der Methode?
3. Warum ist diese Unterscheidung wichtig?

---

## Aufbau

### Aufgabe 3 – Mehrere einfache Testmethoden schreiben

Schreibe drei JUnit-Tests für:

| Testfall | Aufruf | Erwartet |
|---|---|---:|
| Normalfall | `berechneRabattpreis(10000, 10)` | `9000` |
| kein Rabatt | `berechneRabattpreis(10000, 0)` | `10000` |
| voller Rabatt | `berechneRabattpreis(10000, 100)` | `0` |

Vorgaben:

- Jede Prüfung ist eine eigene Testmethode.
- Jede Testmethode hat einen sprechenden Namen.
- Jede Testmethode hat `@Test`.
- Verwende `assertEquals`.

Führe danach aus:

```bash
mvn test
```

Prüfe zusätzlich:

- Wird ein Fehler angezeigt, wenn du absichtlich ein falsches erwartetes Resultat einträgst?
- Ist in der Fehlermeldung erkennbar, welcher Test fehlgeschlagen ist?

---

### Aufgabe 4 – Testcode am richtigen Ort ablegen

Prüfe deine Projektstruktur.

Beantworte:

1. Wo liegt `ProduktVerwaltung.java`?
2. Wo liegt `ProduktVerwaltungTest.java`?
3. Warum gehört die Testklasse nicht unter `src/main/java`?
4. Was passiert, wenn du `mvn test` aus einem Ordner ohne passende `pom.xml` startest?

---

## Vertiefung

### Aufgabe 5 – Edge Cases testen

Ergänze Tests für diese Edge Cases:

| Methode | Edge Case | Erwartung |
|---|---|---|
| `berechneRabattpreis` | `0` Prozent Rabatt | Originalpreis |
| `berechneRabattpreis` | `100` Prozent Rabatt | `0` |
| `berechneGesamtwert` | leeres Produktarray | `0` |
| `findeProdukt` | Produktname existiert nicht | `null` |

Hinweis für den `null`-Fall:

```java
Produkt produkt = verwaltung.findeProdukt(produkte, "Webcam");
assertEquals(null, produkt);
```

Für diese Einheit reicht diese Schreibweise. Spezialisierte JUnit-Prüfungen für `null` kommen später.
Wichtig ist hier vor allem, dass der Rückgabewert automatisch geprüft wird.

---

### Aufgabe 6 – Fachlogik aus `main` herauslösen

Ausgangscode:

```java
public class Main {
    public static void main(String[] args) {
        int preisInRappen = 10000;
        int rabattProzent = 10;
        int rabattpreis = preisInRappen - preisInRappen * rabattProzent / 100;

        System.out.println(rabattpreis);
    }
}
```

Auftrag:

1. Verschiebe die Berechnung in `ProduktVerwaltung`.
2. Die Methode heisst `berechneRabattpreis`.
3. Die Methode erhält `preisInRappen` und `rabattProzent`.
4. Die Methode gibt den Rabattpreis zurück.
5. `main` ruft nur noch die Methode auf und gibt das Resultat aus.
6. Schreibe einen JUnit-Test für die Methode.

Kontrollfrage:

```text
Könnte der Test noch funktionieren, wenn main gar nicht gestartet wird?
```

Die Antwort soll ja sein.

---

## Transfer

### Aufgabe 7 – Produktverwaltung mit mehreren JUnit-Tests prüfen

Erstelle Tests für diese Methoden:

```java
public int berechneRabattpreis(int preisInRappen, int rabattProzent)
public int berechneGesamtwert(Produkt[] produkte)
public Produkt findeProdukt(Produkt[] produkte, String name)
```

Nutze dieses Produktarray:

```java
Produkt[] produkte = {
        new Produkt("Maus", 2500, 3),
        new Produkt("Tastatur", 7000, 2),
        new Produkt("Monitor", 19900, 1)
};
```

Pflichttests:

| Test | Erwartung |
|---|---|
| Gesamtwert mit drei Produkten | `41400` |
| Gesamtwert mit leerem Array | `0` |
| Suche nach `Tastatur` | Produkt wird gefunden |
| Suche nach `Webcam` | `null` |

Für die Suche nach `Tastatur` darfst du sparsam `assertTrue` verwenden:

```java
assertTrue(produkt != null);
assertEquals("Tastatur", produkt.getName());
```

---

### Aufgabe 8 – Regressionstest ergänzen

Stell dir vor, in der Rabattberechnung gab es einmal einen Fehler bei `100` Prozent Rabatt.

Auftrag:

1. Schreibe einen Test, der genau diesen Fall prüft.
2. Gib der Testmethode einen Namen, der den alten Fehler verständlich macht.
3. Führe `mvn test` aus.
4. Erkläre in zwei Sätzen, warum dieser Test ein Regressionstest ist.

---

## Fehlerdiagnose

### Aufgabe 9 – Typische Fehler erkennen

Ordne jedem Fehler eine mögliche Ursache zu.

| Beobachtung | Mögliche Ursache |
|---|---|
| Maven findet keine Tests | |
| `@Test` wird rot markiert | |
| `assertEquals` wird nicht gefunden | |
| Tests laufen, aber Fachlogik wird nicht geprüft | |
| `mvn test` meldet keine `pom.xml` | |

Mögliche Ursachen:

- Testklasse liegt unter `src/main/java`
- `@Test` fehlt
- Import für `assertEquals` fehlt
- JUnit-Dependency ist falsch oder fehlt
- Maven wurde im falschen Ordner gestartet
- Berechnung steckt weiterhin direkt in `main`

---

## Reflexion

Beantworte schriftlich:

1. Was ersetzt JUnit im Vergleich zur manuellen `if`/`else`-Prüfung?
2. Warum soll ein Test nicht von `System.out.println` abhängen?
3. Warum hilft `mvn test` in einem Team?
4. Warum ist `mvn test` für Build-Server und CI/CD wichtig, wenn Tests ohne manuelle Auswertung laufen sollen?
5. Welche Themen wurden in dieser Einheit bewusst noch nicht behandelt?
