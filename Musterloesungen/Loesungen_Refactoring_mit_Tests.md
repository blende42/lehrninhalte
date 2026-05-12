# Lösungen – Refactoring mit Tests absichern

## Aufgabe 1 – Grünen Ausgangszustand herstellen

Ausgeführter Befehl:

```bash
mvn test
```

Erwartetes Ergebnis:

```text
Tests run: ..., Failures: 0, Errors: 0
BUILD SUCCESS
```

Warum ist das wichtig?

Ein Refactoring soll nur die Struktur verbessern. Wenn die Tests schon vorher rot sind, ist nicht klar, ob ein späterer Fehler durch das Refactoring entstanden ist.

Typischer Fehler: Direkt umbauen, ohne den Ausgangszustand zu kennen.

---

## Aufgabe 2 – Verhalten und Struktur unterscheiden

Methode:

```java
public int berechneRabattpreis(int preisInRappen, int rabattProzent) {
    int rabattBetrag = preisInRappen * rabattProzent / 100;
    return preisInRappen - rabattBetrag;
}
```

Antworten:

1. Verhalten: Bei gleichen Eingaben kommt das gleiche Resultat zurück, zum Beispiel `berechneRabattpreis(10000, 10)` liefert `9000`.
2. Struktur: Die Berechnung ist in einer Methode gekapselt, Variablen haben Namen und die Formel ist in einzelne Schritte aufgeteilt.
3. Das erwartete Resultat darf sich nicht ändern, weil Refactoring keine neue Funktion ist.

---

## Aufgabe 3 – Logik aus `main` verschieben

Fachlogik in `ProduktVerwaltung`:

```java
public class ProduktVerwaltung {
    public int berechneRabattpreis(int preisInRappen, int rabattProzent) {
        int rabattBetrag = preisInRappen * rabattProzent / 100;
        return preisInRappen - rabattBetrag;
    }
}
```

`main` bleibt klein:

```java
public class Main {
    public static void main(String[] args) {
        ProduktVerwaltung verwaltung = new ProduktVerwaltung();
        int rabattpreis = verwaltung.berechneRabattpreis(10000, 10);

        System.out.println(rabattpreis);
    }
}
```

Passender Test bleibt möglich:

```java
@Test
void berechneRabattpreis_mitZehnProzent_liefertReduziertenPreis() {
    ProduktVerwaltung verwaltung = new ProduktVerwaltung();

    assertEquals(9000, verwaltung.berechneRabattpreis(10000, 10));
}
```

Nach dem Verschieben:

```bash
mvn test
```

Typischer Fehler: Nur die Ausgabe in `main` verschönern, aber die Berechnung dort lassen.

---

## Aufgabe 4 – Lange Methode aufteilen

Vorher war die Rabattberechnung direkt in der Schleife.

Besser:

```java
public int berechneGesamtwertMitRabatt(Produkt[] produkte, int rabattProzent) {
    int summe = 0;

    for (Produkt produkt : produkte) {
        int rabattpreis = berechneRabattpreis(produkt.getPreisInRappen(), rabattProzent);
        summe = summe + rabattpreis * produkt.getAnzahl();
    }

    return summe;
}

public int berechneRabattpreis(int preisInRappen, int rabattProzent) {
    int rabattBetrag = preisInRappen * rabattProzent / 100;
    return preisInRappen - rabattBetrag;
}
```

Das Verhalten bleibt gleich. Die Struktur ist klarer, weil die Rabattberechnung nur noch an einer Stelle steht.

Nach dem Schritt:

```bash
mvn test
```

---

## Aufgabe 5 – Sprechenden Methodennamen wählen

Ungünstig:

```java
public int rechne(int preis, int rabatt) {
    return preis - preis * rabatt / 100;
}
```

Besser:

```java
public int berechneRabattpreis(int preisInRappen, int rabattProzent) {
    return preisInRappen - preisInRappen * rabattProzent / 100;
}
```

Warum ist das besser?

- Der Methodenname sagt, was berechnet wird.
- Die Parameter sagen, welche Werte erwartet werden.
- Tests und Aufrufe werden leichter lesbar.

Typischer Fehler: Einen kurzen Namen wählen, der fachlich nichts erklärt.

---

## Aufgabe 6 – Duplikate reduzieren

Vorher:

```java
int rabattpreisTastatur = tastaturPreis - tastaturPreis * rabattProzent / 100;
int rabattpreisMaus = mausPreis - mausPreis * rabattProzent / 100;
```

Nachher:

```java
int rabattpreisTastatur = berechneRabattpreis(tastaturPreis, rabattProzent);
int rabattpreisMaus = berechneRabattpreis(mausPreis, rabattProzent);
```

Edge-Case-Test für `0` Prozent Rabatt:

```java
@Test
void berechneRabattpreis_ohneRabatt_liefertOriginalpreis() {
    ProduktVerwaltung verwaltung = new ProduktVerwaltung();

    assertEquals(10000, verwaltung.berechneRabattpreis(10000, 0));
}
```

Hinweis: Duplikate reduzieren ist nur dann ein gutes Refactoring, wenn die Tests danach weiterhin grün sind.

---

## Aufgabe 7 – Regression bewusst erzeugen

Absichtlich falsch:

```java
int rabattBetrag = preisInRappen * rabattProzent / 10;
```

Mögliche Fehlermeldung:

```text
expected: <9000> but was: <0>
```

Ursache:

```text
Durch 10 statt durch 100: Der Rabatt wird zu gross berechnet.
```

Korrektur:

```java
int rabattBetrag = preisInRappen * rabattProzent / 100;
```

Warum war der Test ein Sicherheitsnetz?

Der Test zeigt sofort, dass eine bekannte Erwartung nicht mehr erfüllt ist. So wird die Regression früh sichtbar.

---

## Aufgabe 8 – Edge Case nach Refactoring beibehalten

Test bleibt unverändert:

```java
@Test
void berechneRabattpreis_mitVollemRabatt_liefertNull() {
    ProduktVerwaltung verwaltung = new ProduktVerwaltung();

    assertEquals(0, verwaltung.berechneRabattpreis(10000, 100));
}
```

Korrekte Methode:

```java
public int berechneRabattpreis(int preisInRappen, int rabattProzent) {
    int rabattBetrag = preisInRappen * rabattProzent / 100;
    return preisInRappen - rabattBetrag;
}
```

Erwartung:

```text
100 Prozent Rabatt auf 10000 Rappen liefert 0.
```

Typischer Fehler: Beim Refactoring nur den Normalfall prüfen und den Edge Case verlieren.

---

## Aufgabe 9 – Produktverwaltung schrittweise refaktorieren

Mögliche Lösungstabelle:

| Schritt | Was geändert? | Testresultat |
|---|---|---|
| 1 | `mvn test` vor Start ausgeführt | grün |
| 2 | Rabattberechnung in `berechneRabattpreis` zentralisiert | grün |
| 3 | Gesamtwertberechnung liest Rabattpreis über Methode | grün |
| 4 | Suche nach Produkt lesbarer formatiert | grün |
| 5 | `main` ruft nur noch Methoden auf und gibt Resultate aus | grün |

Beispiel für lesbare Suche:

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

Wichtig: Nach jedem Schritt wird `mvn test` ausgeführt. Wenn ein Schritt rot wird, zuerst diese letzte Änderung prüfen.

---

## Aufgabe 10 – Fehlerbilder zuordnen

| Fehlerbild | Sinnvolle Reaktion |
|---|---|
| Verhalten wurde versehentlich geändert | letzte Änderung prüfen und Verhalten wieder herstellen |
| Zu viele Änderungen auf einmal | kleinere Refactoring-Schritte wählen |
| Tests wurden vorher nicht ausgeführt | zuerst grünen Ausgangszustand herstellen |
| Testfehler wird ignoriert | Fehlermeldung lesen und Ursache suchen |
| `main` bleibt überladen | Fachlogik in Methode oder Service-Klasse verschieben |
| Test prüft `System.out.println` | Rückgabewerte testen |
| Methodenname ist zu allgemein | sprechenden Namen wählen |

---

## Reflexion

1. Ein Refactoring war erfolgreich, wenn die Struktur klarer ist und die Tests weiterhin grün sind.
2. Kleine Schritte sind sicherer, weil bei einem roten Test die Ursache leichter gefunden wird.
3. Automatisierte Tests helfen, bekannte Erwartungen nach Änderungen erneut zu prüfen.
4. In Teams ist Refactoring wichtig, weil Code von mehreren Personen gelesen, geändert und weiterentwickelt wird.
5. Tests vor dem Refactoring zeigen den Ausgangszustand. Tests danach zeigen, ob das geprüfte Verhalten gleich geblieben ist.

---

## Verifikation

Die zentralen Produktverwaltungs-Tests wurden mit dem vorhandenen temporären Maven-Projekt geprüft.

Ausgeführter Befehl:

```bash
mvn test
```

Ergebnis:

```text
Tests run: 7, Failures: 0, Errors: 0, Skipped: 0
BUILD SUCCESS
```

Hinweis: Die absichtlich fehlerhafte Regression mit `/ 10` wurde nicht als Endzustand verifiziert. Sie dient dazu, rote Tests sichtbar zu machen.
