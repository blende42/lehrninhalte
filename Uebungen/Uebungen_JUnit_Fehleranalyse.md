# Übungen – Wenn automatisierte Tests fehlschlagen

## Vorwissen

Du brauchst:

- Maven-Projekt mit `pom.xml`
- Produktivcode unter `src/main/java`
- Testcode unter `src/test/java`
- JUnit Jupiter mit `@Test` und `assertEquals`
- `mvn test`
- Produktverwaltung mit `Produkt` und `ProduktVerwaltung`

Nicht verwendet werden:

- Mocking
- Parameterized Tests
- komplexe Assertions
- Coverage
- Integrationstests
- technische CI/CD-Pipeline

---

## Vorbereitung

Nutze die Produktverwaltung aus der JUnit-Einheit.

Wichtige Methoden:

```java
public int berechneRabattpreis(int preisInRappen, int rabattProzent)
public int berechneGesamtwert(Produkt[] produkte)
public Produkt findeProdukt(Produkt[] produkte, String name)
```

Starte Tests immer im Ordner mit der passenden `pom.xml`:

```bash
mvn test
```

---

## Basis

### Aufgabe 1 – Fehlgeschlagenen Test lesen

Gegeben ist dieser Test:

```java
@Test
void berechneRabattpreis_mitZehnProzent_liefertReduziertenPreis() {
    ProduktVerwaltung verwaltung = new ProduktVerwaltung();

    assertEquals(9000, verwaltung.berechneRabattpreis(10000, 10));
}
```

Maven meldet sinngemäss:

```text
expected: <9000> but was: <9500>
```

Beantworte:

1. Welcher Wert wurde erwartet?
2. Welcher Wert wurde tatsächlich geliefert?
3. Welche Methode wurde vermutlich geprüft?
4. Warum ist diese Fehlermeldung hilfreich?

---

### Aufgabe 2 – Falsche Berechnung korrigieren

Baue diesen Fehler absichtlich in `ProduktVerwaltung` ein:

```java
public int berechneRabattpreis(int preisInRappen, int rabattProzent) {
    return preisInRappen - 500;
}
```

Führe aus:

```bash
mvn test
```

Auftrag:

1. Lies die Fehlermeldung.
2. Notiere `expected` und `actual`.
3. Korrigiere die Methode.
4. Führe `mvn test` erneut aus.

Korrekte Berechnung:

```java
int rabattBetrag = preisInRappen * rabattProzent / 100;
return preisInRappen - rabattBetrag;
```

---

## Aufbau

### Aufgabe 3 – Falsche Erwartung erkennen

Gegeben ist dieser Test:

```java
@Test
void berechneRabattpreis_mitZehnProzent_liefertReduziertenPreis() {
    ProduktVerwaltung verwaltung = new ProduktVerwaltung();

    assertEquals(9500, verwaltung.berechneRabattpreis(10000, 10));
}
```

Die Fachlogik ist korrekt.

Auftrag:

1. Erkläre, warum der Test falsch ist.
2. Korrigiere den erwarteten Wert.
3. Führe `mvn test` aus.

Hinweis:

```text
10 Prozent Rabatt auf 10000 Rappen ergibt 9000 Rappen.
```

---

### Aufgabe 4 – Stacktrace grob einordnen

Gegeben ist dieser vereinfachte Ausschnitt:

```text
ProduktVerwaltungTest.berechneGesamtwert_mitDreiProdukten_liefertSumme
expected: <41400> but was: <38900>
at ProduktVerwaltungTest.java:31
```

Markiere oder notiere:

1. Name der Testklasse
2. Name der Testmethode
3. erwarteter Wert
4. tatsächlicher Wert
5. Zeile, in der die Prüfung steht

Beantworte danach:

```text
In welcher Reihenfolge würdest du nachsehen: Testdaten, Erwartung, Fachlogik?
```

---

### Aufgabe 5 – Mehrere Testfehler unterscheiden

Gegeben sind drei Meldungen:

```text
berechneRabattpreis_ohneRabatt_liefertOriginalpreis
expected: <10000> but was: <9500>
```

```text
berechneGesamtwert_mitLeeremArray_liefertWertNull
expected: <0> but was: <1000>
```

```text
findeProdukt_mitUnbekanntemNamen_liefertNull
expected: <null> but was: <Produkt>
```

Ordne zu:

| Meldung | Vermutete Ursache |
|---|---|
| Rabatt ohne Rabatt | |
| Gesamtwert leeres Array | |
| Suche unbekannter Name | |

Mögliche Ursachen:

- Rabattlogik zieht immer einen festen Betrag ab
- Gesamtwert startet mit einem falschen Anfangswert
- Suche gibt ein Produkt zurück, obwohl der Name nicht passt

---

## Vertiefung

### Aufgabe 6 – Edge Case ergänzen

Ergänze einen Test für `100` Prozent Rabatt:

```java
@Test
void berechneRabattpreis_mitVollemRabatt_liefertNull() {
    ProduktVerwaltung verwaltung = new ProduktVerwaltung();

    assertEquals(0, verwaltung.berechneRabattpreis(10000, 100));
}
```

Auftrag:

1. Füge den Test in `ProduktVerwaltungTest` ein.
2. Führe `mvn test` aus.
3. Falls der Test fehlschlägt, lies `expected` und `actual`.
4. Korrigiere die Fachlogik oder den Test.

---

### Aufgabe 7 – Regression bewusst erzeugen und korrigieren

Eine Regression ist ein Fehler, der nach einer Änderung wieder auftaucht.

Auftrag:

1. Sorge zuerst dafür, dass alle Tests grün sind.
2. Ändere die Rabattberechnung absichtlich falsch:

```java
int rabattBetrag = preisInRappen * rabattProzent / 10;
```

3. Führe `mvn test` aus.
4. Notiere, welcher Test fehlschlägt.
5. Korrigiere die Berechnung wieder auf `/ 100`.
6. Führe `mvn test` erneut aus.

Beantworte:

```text
Warum war der Test hier ein Sicherheitsnetz?
```

---

## Transfer

### Aufgabe 8 – Produktsuche absichern

Gegeben ist diese fehlerhafte Methode:

```java
public Produkt findeProdukt(Produkt[] produkte, String name) {
    return produkte[0];
}
```

Schreibe oder nutze Tests für:

| Fall | Erwartung |
|---|---|
| Suche nach `Tastatur` | Produkt wird gefunden |
| Suche nach `Webcam` | `null` |

Auftrag:

1. Führe `mvn test` aus.
2. Lies die Fehlermeldung.
3. Korrigiere `findeProdukt`.
4. Führe `mvn test` erneut aus.

Korrekturidee:

```java
for (Produkt produkt : produkte) {
    if (produkt.getName().equals(name)) {
        return produkt;
    }
}

return null;
```

---

### Aufgabe 9 – Gesamtwert prüfen

Gegeben ist diese fehlerhafte Methode:

```java
public int berechneGesamtwert(Produkt[] produkte) {
    int summe = 1000;

    for (Produkt produkt : produkte) {
        summe = summe + produkt.getPreisInRappen() * produkt.getAnzahl();
    }

    return summe;
}
```

Tests:

```java
@Test
void berechneGesamtwert_mitLeeremArray_liefertWertNull() {
    ProduktVerwaltung verwaltung = new ProduktVerwaltung();

    assertEquals(0, verwaltung.berechneGesamtwert(new Produkt[0]));
}
```

Auftrag:

1. Führe `mvn test` aus.
2. Erkläre, warum der Test fehlschlägt.
3. Korrigiere den Anfangswert.
4. Führe `mvn test` erneut aus.

---

## Fehlerdiagnose

### Aufgabe 10 – Fehlerbilder zuordnen

Ordne jedem Fehlerbild eine sinnvolle Reaktion zu.

| Fehlerbild | Sinnvolle Reaktion |
|---|---|
| `expected` und `actual` sind verwechselt | |
| Rückgabewert ist fachlich falsch | |
| Test erwartet den falschen Wert | |
| Edge Case fehlt | |
| Maven findet keine `pom.xml` | |
| Fachlogik steckt in `main` | |
| Fehlermeldung wird ignoriert | |

Mögliche Reaktionen:

- `assertEquals(erwartet, tatsaechlich)` verwenden
- Fachlogik korrigieren
- erwarteten Wert im Test korrigieren
- neuen Test für Randfall ergänzen
- Maven im Projektordner starten
- Berechnung in eine Methode mit Rückgabewert verschieben
- Fehlermeldung zuerst lesen und notieren

---

## Reflexion

Beantworte schriftlich:

1. Warum sind fehlgeschlagene Tests hilfreich?
2. Warum sind automatisierte Tests bei Refactoring wichtig?
3. Warum stoppen Build-Server bei fehlerhaften Tests?
4. Warum soll ein roter Test nicht einfach gelöscht werden?
5. Welche Informationen liest du zuerst aus einer JUnit-Fehlermeldung?
