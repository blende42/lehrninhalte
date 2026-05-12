# Übungen – Refactoring mit Tests absichern

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
- Test Doubles
- komplexe Patterns
- Clean Architecture
- Coverage
- Spring
- Datenbanken

---

## Vorbereitung

Nutze die Produktverwaltung aus den JUnit-Einheiten.

Wichtige Methoden:

```java
public int berechneRabattpreis(int preisInRappen, int rabattProzent)
public int berechneGesamtwert(Produkt[] produkte)
public Produkt findeProdukt(Produkt[] produkte, String name)
```

In einzelnen Aufgaben wird zusätzlich eine Variante mit Rabatt verwendet:

```java
public int berechneGesamtwertMitRabatt(Produkt[] produkte, int rabattProzent)
```

Starte vor jeder Aufgabe im Projektordner:

```bash
mvn test
```

Notiere jeweils:

```text
Vor der Änderung: grün oder rot?
Nach der Änderung: grün oder rot?
```

---

## Basis

### Aufgabe 1 – Grünen Ausgangszustand herstellen

Führe im Projektordner aus:

```bash
mvn test
```

Auftrag:

1. Prüfe, ob alle Tests grün sind.
2. Wenn ein Test rot ist, korrigiere zuerst den bestehenden Fehler.
3. Beginne erst danach mit Refactoring.
4. Notiere kurz, warum dieser Schritt wichtig ist.

Erwartung:

```text
Refactoring startet mit einem bekannten grünen Stand.
```

---

### Aufgabe 2 – Verhalten und Struktur unterscheiden

Gegeben ist diese Methode:

```java
public int berechneRabattpreis(int preisInRappen, int rabattProzent) {
    int rabattBetrag = preisInRappen * rabattProzent / 100;
    return preisInRappen - rabattBetrag;
}
```

Beantworte schriftlich:

1. Was ist hier das Verhalten?
2. Was gehört zur Struktur?
3. Warum darf sich das erwartete Resultat nach einem Refactoring nicht ändern?

Beispiel:

```text
berechneRabattpreis(10000, 10) soll weiterhin 9000 liefern.
```

---

## Aufbau

### Aufgabe 3 – Logik aus `main` verschieben

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

1. Führe zuerst `mvn test` aus.
2. Verschiebe die Rabattberechnung in `ProduktVerwaltung`.
3. Gib der Methode den Namen `berechneRabattpreis`.
4. `main` soll die Methode nur noch aufrufen und das Resultat ausgeben.
5. Führe `mvn test` erneut aus.

Ziel:

```text
Die Berechnung ist testbar, `main` bleibt klein.
```

---

### Aufgabe 4 – Lange Methode aufteilen

Gegeben ist diese Methode:

```java
public int berechneGesamtwertMitRabatt(Produkt[] produkte, int rabattProzent) {
    int summe = 0;

    for (Produkt produkt : produkte) {
        int preis = produkt.getPreisInRappen();
        int rabattBetrag = preis * rabattProzent / 100;
        int rabattpreis = preis - rabattBetrag;
        summe = summe + rabattpreis * produkt.getAnzahl();
    }

    return summe;
}
```

Auftrag:

1. Führe `mvn test` aus.
2. Ersetze die direkte Rabattberechnung durch einen Aufruf von `berechneRabattpreis`.
3. Ändere nur diesen einen Schritt.
4. Führe `mvn test` erneut aus.

Hinweis:

```java
int rabattpreis = berechneRabattpreis(produkt.getPreisInRappen(), rabattProzent);
```

---

### Aufgabe 5 – Sprechenden Methodennamen wählen

Gegeben ist diese Methode:

```java
public int rechne(int preis, int rabatt) {
    return preis - preis * rabatt / 100;
}
```

Auftrag:

1. Wähle einen besseren Methodennamen.
2. Benenne auch die Parameter klarer.
3. Passe die Aufrufe im Code an.
4. Führe `mvn test` aus.

Erwartung:

```text
Der Name zeigt, dass ein Rabattpreis in Rappen berechnet wird.
```

---

## Vertiefung

### Aufgabe 6 – Duplikate reduzieren

Gegeben ist doppelter Code:

```java
int rabattpreisTastatur = tastaturPreis - tastaturPreis * rabattProzent / 100;
int rabattpreisMaus = mausPreis - mausPreis * rabattProzent / 100;
```

Auftrag:

1. Ersetze die doppelte Berechnung durch Aufrufe von `berechneRabattpreis`.
2. Prüfe, ob bestehende Tests weiterhin grün sind.
3. Ergänze bei Bedarf einen Test für `0` Prozent Rabatt.
4. Führe `mvn test` aus.

Edge Case:

```text
0 Prozent Rabatt soll den Originalpreis liefern.
```

---

### Aufgabe 7 – Regression bewusst erzeugen

Sorge zuerst für grüne Tests.

Ändere danach absichtlich:

```java
int rabattBetrag = preisInRappen * rabattProzent / 10;
```

Auftrag:

1. Führe `mvn test` aus.
2. Notiere, welcher Test rot wird.
3. Lies `expected` und `actual`.
4. Korrigiere die Berechnung wieder auf `/ 100`.
5. Führe `mvn test` erneut aus.

Reflexion:

```text
Warum war der Test hier ein Sicherheitsnetz?
```

---

### Aufgabe 8 – Edge Case nach Refactoring beibehalten

Gegeben ist dieser Test:

```java
@Test
void berechneRabattpreis_mitVollemRabatt_liefertNull() {
    ProduktVerwaltung verwaltung = new ProduktVerwaltung();

    assertEquals(0, verwaltung.berechneRabattpreis(10000, 100));
}
```

Auftrag:

1. Refaktoriere die Rabattberechnung.
2. Behalte den Test unverändert.
3. Führe `mvn test` aus.
4. Wenn der Test rot ist, prüfe die letzte Änderung.

Erwartung:

```text
100 Prozent Rabatt liefert weiterhin 0.
```

---

## Transfer

### Aufgabe 9 – Produktverwaltung schrittweise refaktorieren

Refaktoriere die Klasse `ProduktVerwaltung` in kleinen Schritten.

Mögliche Schritte:

1. Methodennamen prüfen
2. doppelte Rabattberechnung entfernen
3. lange Gesamtwert-Methode aufteilen
4. Suche nach Produkt lesbarer machen
5. `main` nur noch für Eingabe und Ausgabe nutzen

Nach jedem Schritt:

```bash
mvn test
```

Notiere in einer Tabelle:

| Schritt | Was geändert? | Testresultat |
|---|---|---|
| 1 | | |
| 2 | | |
| 3 | | |

---

## Fehlerdiagnose

### Aufgabe 10 – Fehlerbilder zuordnen

Ordne jedem Fehlerbild eine sinnvolle Reaktion zu.

| Fehlerbild | Sinnvolle Reaktion |
|---|---|
| Verhalten wurde versehentlich geändert | |
| Zu viele Änderungen auf einmal | |
| Tests wurden vorher nicht ausgeführt | |
| Testfehler wird ignoriert | |
| `main` bleibt überladen | |
| Test prüft `System.out.println` | |
| Methodenname ist zu allgemein | |

Mögliche Reaktionen:

- letzte Änderung prüfen und Verhalten wieder herstellen
- kleinere Refactoring-Schritte wählen
- zuerst grünen Ausgangszustand herstellen
- Fehlermeldung lesen und Ursache suchen
- Fachlogik in Methode oder Service-Klasse verschieben
- Rückgabewerte testen
- sprechenden Namen wählen

---

## Reflexion

Beantworte schriftlich:

1. Woran erkennst du, dass ein Refactoring erfolgreich war?
2. Warum sind kleine Schritte sicherer?
3. Warum helfen automatisierte Tests bei späteren Änderungen?
4. Warum wird Refactoring in Teams besonders wichtig?
5. Warum sollen Tests vor und nach dem Refactoring ausgeführt werden?

---

## Kurzer Ausblick

Später wird Code stärker in Verantwortlichkeiten aufgeteilt. Dann entstehen Begriffe wie Service-Schicht oder Repository-Idee. Diese Einheit bereitet das vor, indem Fachlogik klarer von `main` getrennt und mit Tests abgesichert wird.
