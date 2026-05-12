# Lösungen – Wenn automatisierte Tests fehlschlagen

## Aufgabe 1 – Fehlgeschlagenen Test lesen

Meldung:

```text
expected: <9000> but was: <9500>
```

Antworten:

1. Erwartet wurde `9000`.
2. Tatsächlich geliefert wurde `9500`.
3. Geprüft wurde vermutlich `berechneRabattpreis(10000, 10)`.
4. Die Meldung ist hilfreich, weil sie den erwarteten und den tatsächlichen Wert zeigt. Dadurch ist klar, dass Erwartung und Ergebnis nicht zusammenpassen.

Typischer Fehler: Nur sehen, dass der Test rot ist, aber die Werte nicht lesen.

---

## Aufgabe 2 – Falsche Berechnung korrigieren

Fehlerhafte Methode:

```java
public int berechneRabattpreis(int preisInRappen, int rabattProzent) {
    return preisInRappen - 500;
}
```

Bei `berechneRabattpreis(10000, 10)` ergibt das `9500`. Erwartet ist aber `9000`.

Korrekte Methode:

```java
public int berechneRabattpreis(int preisInRappen, int rabattProzent) {
    int rabattBetrag = preisInRappen * rabattProzent / 100;
    return preisInRappen - rabattBetrag;
}
```

Interpretation:

```text
expected: <9000> = fachlich erwarteter Rabattpreis
actual:   <9500> = fehlerhaft berechneter Wert
```

Nach der Korrektur sollte `mvn test` wieder erfolgreich sein.

---

## Aufgabe 3 – Falsche Erwartung erkennen

Fehlerhafter Test:

```java
assertEquals(9500, verwaltung.berechneRabattpreis(10000, 10));
```

Der Test ist falsch, weil `10` Prozent Rabatt auf `10000` Rappen nicht `9500`, sondern `9000` ergibt.

Korrektur:

```java
assertEquals(9000, verwaltung.berechneRabattpreis(10000, 10));
```

Hinweis: Nicht jeder rote Test bedeutet, dass der Produktivcode falsch ist. Manchmal ist die Erwartung im Test falsch.

---

## Aufgabe 4 – Stacktrace grob einordnen

Ausschnitt:

```text
ProduktVerwaltungTest.berechneGesamtwert_mitDreiProdukten_liefertSumme
expected: <41400> but was: <38900>
at ProduktVerwaltungTest.java:31
```

Lösung:

| Information | Wert |
|---|---|
| Testklasse | `ProduktVerwaltungTest` |
| Testmethode | `berechneGesamtwert_mitDreiProdukten_liefertSumme` |
| Erwartet | `41400` |
| Tatsächlich | `38900` |
| Zeile | `ProduktVerwaltungTest.java:31` |

Zuerst sinnvoll prüfen:

1. Testdaten: Stimmen Preise und Anzahl?
2. Erwartung: Wurde `41400` korrekt berechnet?
3. Fachlogik: Addiert die Methode alle Produkte korrekt?

---

## Aufgabe 5 – Mehrere Testfehler unterscheiden

| Meldung | Vermutete Ursache |
|---|---|
| Rabatt ohne Rabatt | Rabattlogik zieht immer einen festen Betrag ab |
| Gesamtwert leeres Array | Gesamtwert startet mit einem falschen Anfangswert |
| Suche unbekannter Name | Suche gibt ein Produkt zurück, obwohl der Name nicht passt |

Hinweis: Mehrere rote Tests können verschiedene Ursachen haben. Deshalb immer Testmethode und Werte einzeln lesen.

---

## Aufgabe 6 – Edge Case ergänzen

Test:

```java
@Test
void berechneRabattpreis_mitVollemRabatt_liefertNull() {
    ProduktVerwaltung verwaltung = new ProduktVerwaltung();

    assertEquals(0, verwaltung.berechneRabattpreis(10000, 100));
}
```

Erwartung:

```text
100 Prozent Rabatt auf 10000 Rappen ergibt 0 Rappen.
```

Wenn der Test fehlschlägt, zuerst `expected` und `actual` lesen. Danach prüfen, ob die Rabattberechnung oder die Erwartung falsch ist.

---

## Aufgabe 7 – Regression bewusst erzeugen und korrigieren

Absichtlich fehlerhafte Zeile:

```java
int rabattBetrag = preisInRappen * rabattProzent / 10;
```

Problem:

```text
Der Rabatt wird zehnmal zu gross berechnet.
```

Korrektur:

```java
int rabattBetrag = preisInRappen * rabattProzent / 100;
```

Warum ist der Test ein Sicherheitsnetz?

Der Test fällt sofort auf rot, wenn die Berechnung nach einer Änderung wieder falsch wird. So wird eine Regression früh sichtbar.

---

## Aufgabe 8 – Produktsuche absichern

Fehlerhafte Methode:

```java
public Produkt findeProdukt(Produkt[] produkte, String name) {
    return produkte[0];
}
```

Problem:

Diese Methode gibt immer das erste Produkt zurück. Sie prüft den Namen nicht.

Korrekte Methode:

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

Passende Tests:

Hinweis: `assertTrue` braucht wie `assertEquals` den passenden statischen JUnit-Import.

```java
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
```

---

## Aufgabe 9 – Gesamtwert prüfen

Fehlerhafte Methode:

```java
public int berechneGesamtwert(Produkt[] produkte) {
    int summe = 1000;

    for (Produkt produkt : produkte) {
        summe = summe + produkt.getPreisInRappen() * produkt.getAnzahl();
    }

    return summe;
}
```

Problem:

Die Summe startet bei `1000`. Bei einem leeren Array wird deshalb `1000` zurückgegeben. Erwartet ist `0`.

Korrektur:

```java
public int berechneGesamtwert(Produkt[] produkte) {
    int summe = 0;

    for (Produkt produkt : produkte) {
        summe = summe + produkt.getPreisInRappen() * produkt.getAnzahl();
    }

    return summe;
}
```

Passender Test:

```java
@Test
void berechneGesamtwert_mitLeeremArray_liefertWertNull() {
    ProduktVerwaltung verwaltung = new ProduktVerwaltung();

    assertEquals(0, verwaltung.berechneGesamtwert(new Produkt[0]));
}
```

---

## Aufgabe 10 – Fehlerbilder zuordnen

| Fehlerbild | Sinnvolle Reaktion |
|---|---|
| `expected` und `actual` sind verwechselt | `assertEquals(erwartet, tatsaechlich)` verwenden |
| Rückgabewert ist fachlich falsch | Fachlogik korrigieren |
| Test erwartet den falschen Wert | erwarteten Wert im Test korrigieren |
| Edge Case fehlt | neuen Test für Randfall ergänzen |
| Maven findet keine `pom.xml` | Maven im Projektordner starten |
| Fachlogik steckt in `main` | Berechnung in eine Methode mit Rückgabewert verschieben |
| Fehlermeldung wird ignoriert | Fehlermeldung zuerst lesen und notieren |

---

## Reflexion

1. Fehlgeschlagene Tests sind hilfreich, weil sie zeigen, welche Erwartung nicht erfüllt wurde.
2. Automatisierte Tests sind bei Refactoring wichtig, weil sie nach einer Änderung prüfen, ob das Verhalten gleich geblieben ist.
3. Build-Server stoppen bei fehlerhaften Tests, damit fehlerhafter Code nicht unbemerkt weitergegeben wird.
4. Ein roter Test soll nicht gelöscht werden, weil er auf ein Problem hinweist. Zuerst muss die Ursache verstanden werden.
5. Zuerst lese ich Testklasse, Testmethode, `expected`, `actual` und die Zeile mit der fehlgeschlagenen Prüfung.

---

## Verifikation

Die korrekten Endzustände der Produktverwaltung und der JUnit-Tests wurden in einem temporären Maven-Projekt geprüft.

Ausgeführter Befehl:

```bash
mvn test
```

Ergebnis:

```text
Tests run: 7, Failures: 0, Errors: 0, Skipped: 0
BUILD SUCCESS
```

Diese Zusammenfassung passt zu den technischen Berichten unter `target/surefire-reports`. Das Format dieser Dateien wird hier nicht vertieft.

Hinweis: Die absichtlich fehlerhaften Codebeispiele in den Aufgaben wurden nicht als Endzustand verifiziert. Sie dienen dazu, rote Tests zu erzeugen und Fehlermeldungen zu analysieren.
