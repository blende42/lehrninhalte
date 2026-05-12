# Lösungen – Von manuellen Tests zu automatisierten Tests mit JUnit

## Vorbereitung – Projektstruktur

Mögliche Struktur:

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

Wichtig: Produktivcode liegt unter `src/main/java`, Testcode unter `src/test/java`.

---

## Vorbereitung – `pom.xml`

Kompakte Lösung:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>ch.allianz.youngoitv</groupId>
    <artifactId>produktverwaltung</artifactId>
    <version>1.0.0</version>

    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter</artifactId>
            <version>6.0.3</version>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
                <version>3.5.4</version>
            </plugin>
        </plugins>
    </build>
</project>
```

Hinweis: `scope test` bedeutet, dass JUnit nur für Tests gebraucht wird.

---

## Produktivcode

### `Produkt.java`

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

### `ProduktVerwaltung.java`

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

### `Main.java`

```java
package ch.allianz.youngoitv.produktverwaltung;

import ch.allianz.youngoitv.produktverwaltung.service.ProduktVerwaltung;

public class Main {
    public static void main(String[] args) {
        ProduktVerwaltung verwaltung = new ProduktVerwaltung();
        int rabattpreis = verwaltung.berechneRabattpreis(10000, 10);

        System.out.println("Rabattpreis: " + rabattpreis);
    }
}
```

Hinweis: `main` startet das Programm und gibt aus. Die Berechnung steckt in `ProduktVerwaltung`.

---

## Aufgaben 1 bis 3 – Erste JUnit-Tests

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

        assertEquals(erwartet, tatsaechlich);
    }

    @Test
    void berechneRabattpreis_ohneRabatt_liefertOriginalpreis() {
        ProduktVerwaltung verwaltung = new ProduktVerwaltung();

        assertEquals(10000, verwaltung.berechneRabattpreis(10000, 0));
    }

    @Test
    void berechneRabattpreis_mitVollemRabatt_liefertNull() {
        ProduktVerwaltung verwaltung = new ProduktVerwaltung();

        assertEquals(0, verwaltung.berechneRabattpreis(10000, 100));
    }
}
```

Antwort zu Aufgabe 2:

1. `erwartet` enthält das fachlich erwartete Resultat.
2. `tatsaechlich` kommt aus der Methode.
3. Die Unterscheidung ist wichtig, weil der Test klar zeigt, was stimmen sollte und was die Methode wirklich geliefert hat.

Typischer Fehler: `assertEquals(tatsaechlich, erwartet)` ist technisch oft lauffähig, macht Fehlermeldungen aber weniger klar.

---

## Aufgabe 4 – Testcode am richtigen Ort

1. `ProduktVerwaltung.java` liegt unter `src/main/java/ch/allianz/youngoitv/produktverwaltung/service`.
2. `ProduktVerwaltungTest.java` liegt unter `src/test/java/ch/allianz/youngoitv/produktverwaltung/service`.
3. Die Testklasse gehört nicht unter `src/main/java`, weil sie nicht Teil des normalen Programms ist.
4. Wenn `mvn test` aus einem falschen Ordner gestartet wird, findet Maven keine passende `pom.xml`.

---

## Aufgaben 5 bis 8 – Edge Cases, Transfer und Regression

Kompakte Testklasse mit allen wichtigen Fällen:

```java
package ch.allianz.youngoitv.produktverwaltung.service;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;
import org.junit.jupiter.api.Test;

import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.junit.jupiter.api.Assertions.assertTrue;

class ProduktVerwaltungTest {

    @Test
    void berechneRabattpreis_mitZehnProzent_liefertReduziertenPreis() {
        ProduktVerwaltung verwaltung = new ProduktVerwaltung();

        assertEquals(9000, verwaltung.berechneRabattpreis(10000, 10));
    }

    @Test
    void berechneRabattpreis_ohneRabatt_liefertOriginalpreis() {
        ProduktVerwaltung verwaltung = new ProduktVerwaltung();

        assertEquals(10000, verwaltung.berechneRabattpreis(10000, 0));
    }

    @Test
    void berechneRabattpreis_mitVollemRabatt_liefertNull() {
        ProduktVerwaltung verwaltung = new ProduktVerwaltung();

        assertEquals(0, verwaltung.berechneRabattpreis(10000, 100));
    }

    @Test
    void berechneGesamtwert_mitDreiProdukten_liefertSumme() {
        ProduktVerwaltung verwaltung = new ProduktVerwaltung();
        Produkt[] produkte = {
                new Produkt("Maus", 2500, 3),
                new Produkt("Tastatur", 7000, 2),
                new Produkt("Monitor", 19900, 1)
        };

        assertEquals(41400, verwaltung.berechneGesamtwert(produkte));
    }

    @Test
    void berechneGesamtwert_mitLeeremArray_liefertWertNull() {
        ProduktVerwaltung verwaltung = new ProduktVerwaltung();

        assertEquals(0, verwaltung.berechneGesamtwert(new Produkt[0]));
    }

    @Test
    void findeProdukt_mitVorhandenemNamen_liefertProdukt() {
        ProduktVerwaltung verwaltung = new ProduktVerwaltung();
        Produkt[] produkte = {
                new Produkt("Maus", 2500, 3),
                new Produkt("Tastatur", 7000, 2)
        };

        Produkt produkt = verwaltung.findeProdukt(produkte, "Tastatur");

        assertTrue(produkt != null);
        assertEquals("Tastatur", produkt.getName());
    }

    @Test
    void findeProdukt_mitUnbekanntemNamen_liefertNull() {
        ProduktVerwaltung verwaltung = new ProduktVerwaltung();
        Produkt[] produkte = {
                new Produkt("Maus", 2500, 3),
                new Produkt("Tastatur", 7000, 2)
        };

        Produkt produkt = verwaltung.findeProdukt(produkte, "Webcam");

        assertEquals(null, produkt);
    }
}
```

Hinweise:

- `assertTrue` wird nur einmal sparsam verwendet, um zu prüfen, ob ein Produkt gefunden wurde.
- Für `null` reicht in dieser Einstiegseinheit `assertEquals(null, produkt)`.
- Später können speziellere JUnit-Prüfungen für `null` eingeführt werden.
- Der Test `berechneRabattpreis_mitVollemRabatt_liefertNull` ist auch ein einfacher Regressionstest: Wenn dieser Fehler später wieder auftaucht, fällt `mvn test` fehl.

---

## Aufgabe 9 – Fehlerdiagnose

| Beobachtung | Mögliche Ursache |
|---|---|
| Maven findet keine Tests | Testklasse liegt falsch oder `@Test` fehlt |
| `@Test` wird rot markiert | JUnit-Dependency fehlt oder Import fehlt |
| `assertEquals` wird nicht gefunden | statischer Import für `assertEquals` fehlt oder Dependency fehlt |
| Tests laufen, aber Fachlogik wird nicht geprüft | Berechnung steckt weiterhin direkt in `main` oder der Test prüft nur Ausgaben |
| `mvn test` meldet keine `pom.xml` | Maven wurde im falschen Ordner gestartet |

---

## Reflexion

1. JUnit ersetzt die manuelle `if`/`else`-Auswertung durch `assertEquals`.
2. Ein Test soll nicht von `System.out.println` abhängen, weil eine Ausgabe nur sichtbar ist, aber nicht automatisch bewertet wird.
3. `mvn test` hilft im Team, weil alle denselben Befehl verwenden und dieselben Tests ausführen können.
4. Für Build-Server und CI/CD ist `mvn test` wichtig, weil derselbe Befehl automatisch ohne manuelle Auswertung ausgeführt werden kann.
5. Bewusst nicht behandelt wurden Mocking, Parameterized Tests, Test Doubles, Spring Tests, Lifecycle-Methoden und komplexe Maven-Konfiguration.

---

## Verifikation

Die Beispielstruktur wurde in einem temporären Maven-Projekt geprüft.

Ausgeführter Befehl:

```bash
mvn test
```

Ergebnis:

```text
Tests run: 7, Failures: 0, Errors: 0, Skipped: 0
BUILD SUCCESS
```

Damit sind `pom.xml`, Package-Struktur, Produktivcode und JUnit-Testklasse technisch geprüft.
