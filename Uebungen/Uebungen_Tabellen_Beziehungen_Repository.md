# Übungen – Mehrere Tabellen, Beziehungen und Repository

## Vorwissen

Du brauchst:

- bekannte Lagerverwaltung
- `Produkt`
- `LagerService`
- H2 Embedded
- JDBC mit `Connection`, `PreparedStatement` und `ResultSet`
- Mapping zwischen Objekt und Datenbankzeile
- einfache SQL-Befehle
- Grundidee von Verantwortlichkeiten

Nicht verwendet werden:

- ORM
- Hibernate
- JPA
- Spring Data
- Generic Repository
- automatische Query-Generierung
- Dependency Injection
- komplexe SQL-Theorie
- komplexe Joins

---

## Vorbereitung

Arbeite mit der bekannten Lagerverwaltung.

Beispielstruktur:

```text
lagerverwaltung-db/
  pom.xml
  data/
  src/main/java/
    ch/allianz/youngoitv/lager/
      Main.java
      LagerService.java
      repository/ProduktRepository.java
      repository/AenderungsRepository.java
      model/Produkt.java
      model/PreisAenderung.java
      model/BestandsAenderung.java
```

Prüfe nach praktischen Änderungen:

```bash
mvn package
```

Wenn Tests vorhanden sind:

```bash
mvn test
```

Ziel dieser Übungen:

```text
Du strukturierst wachsenden JDBC- und Mapping-Code in Repository-Klassen.
```

---

## Basis

### Aufgabe 1 – Beziehung skizzieren

Zeichne oder notiere die Beziehung zwischen den drei Tabellen:

```text
PRODUKT
PREISAENDERUNG
BESTANDSAENDERUNG
```

Auftrag:

1. Markiere `PRODUKT.ID`.
2. Markiere `PREISAENDERUNG.PRODUKT_ID`.
3. Markiere `BESTANDSAENDERUNG.PRODUKT_ID`.
4. Schreibe je einen Satz zur Beziehung.

Erwartung:

```text
Eine Preisänderung gehört zu einem Produkt.
Eine Bestandsänderung gehört zu einem Produkt.
Ein Produkt kann mehrere Änderungen haben.
```

---

### Aufgabe 2 – Tabelle `PREISAENDERUNG` erstellen

Ergänze in deiner Datenbank-Initialisierung die Tabelle für Preisänderungen.

```sql
CREATE TABLE IF NOT EXISTS PREISAENDERUNG (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    PRODUKT_ID INT NOT NULL,
    ALTER_PREIS DOUBLE NOT NULL,
    NEUER_PREIS DOUBLE NOT NULL,
    GRUND VARCHAR(200),
    ZEITPUNKT VARCHAR(30) NOT NULL,
    FOREIGN KEY (PRODUKT_ID) REFERENCES PRODUKT(ID)
);
```

Auftrag:

1. Füge die SQL-Anweisung an einer passenden Persistenzstelle ein.
2. Erkläre, warum `PRODUKT` zuerst existieren muss.
3. Führe `mvn package` aus.

---

### Aufgabe 3 – Tabelle `BESTANDSAENDERUNG` erstellen

Ergänze die Tabelle für Bestandsänderungen.

```sql
CREATE TABLE IF NOT EXISTS BESTANDSAENDERUNG (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    PRODUKT_ID INT NOT NULL,
    ALTER_BESTAND INT NOT NULL,
    NEUER_BESTAND INT NOT NULL,
    GRUND VARCHAR(200),
    ZEITPUNKT VARCHAR(30) NOT NULL,
    FOREIGN KEY (PRODUKT_ID) REFERENCES PRODUKT(ID)
);
```

Auftrag:

1. Ergänze die Tabelle neben `PREISAENDERUNG`.
2. Prüfe, ob die Namen der Spalten zu deinen Java-Klassen passen.
3. Notiere, welche Spalte die Verbindung zu `PRODUKT` herstellt.

---

### Aufgabe 4 – Modellklassen ergänzen

Erstelle oder prüfe die Klassen `PreisAenderung` und `BestandsAenderung`.

Auftrag für `PreisAenderung`:

```text
id
produktId
alterPreis
neuerPreis
grund
zeitpunkt
```

Auftrag für `BestandsAenderung`:

```text
id
produktId
alterBestand
neuerBestand
grund
zeitpunkt
```

Erwartung:

1. Die Klassen enthalten passende Attribute.
2. Die Konstruktoren sind klein und nachvollziehbar.
3. Getter sind vorhanden, wenn sie für Mapping oder Ausgabe gebraucht werden.

---

### Aufgabe 5 – `ProduktRepository` erstellen

Erstelle eine Klasse `ProduktRepository`.

Auftrag:

1. Verschiebe oder plane den bisherigen JDBC-Zugriff für Produkte in diese Klasse.
2. Lasse dort Methoden wie `ladeProdukte`, `speichereProdukt` oder `aktualisiereProdukt`.
3. Lasse Mapping-Hilfsmethoden für `Produkt` in dieser Klasse.
4. Schreibe keinen SQL-Code in `Main`.

Kurze Kontrolle:

```text
ProduktRepository kennt PRODUKT.
ProduktRepository mappt ResultSet zu Produkt.
LagerService kennt keine PRODUKT-Spaltennamen.
```

---

### Aufgabe 6 – `AenderungsRepository` erstellen

Erstelle eine Klasse `AenderungsRepository`.

Auftrag:

1. Die Klasse kennt `PREISAENDERUNG` und `BESTANDSAENDERUNG`.
2. Sie enthält Methoden zum Speichern von Preisänderungen.
3. Sie enthält Methoden zum Speichern von Bestandsänderungen.
4. Sie enthält Methoden zum Laden von Änderungen zu einem Produkt.

Mögliche Methodennamen:

```java
public void speicherePreisAenderung(PreisAenderung aenderung)
public void speichereBestandsAenderung(BestandsAenderung aenderung)
public ArrayList<PreisAenderung> ladePreisAenderungen(int produktId)
public ArrayList<BestandsAenderung> ladeBestandsAenderungen(int produktId)
```

---

### Aufgabe 7 – Preisänderung speichern

Implementiere das Speichern einer Preisänderung.

```java
String sql = """
        INSERT INTO PREISAENDERUNG
        (PRODUKT_ID, ALTER_PREIS, NEUER_PREIS, GRUND, ZEITPUNKT)
        VALUES (?, ?, ?, ?, ?)
        """;
```

Auftrag:

1. Verwende ein `PreparedStatement`.
2. Setze `PRODUKT_ID` an Position `1`.
3. Setze danach alten Preis, neuen Preis, Grund und Zeitpunkt.
4. Prüfe die Reihenfolge der Platzhalter.

---

### Aufgabe 8 – Bestandsänderung speichern

Implementiere das Speichern einer Bestandsänderung.

```java
String sql = """
        INSERT INTO BESTANDSAENDERUNG
        (PRODUKT_ID, ALTER_BESTAND, NEUER_BESTAND, GRUND, ZEITPUNKT)
        VALUES (?, ?, ?, ?, ?)
        """;
```

Auftrag:

1. Verwende ein `PreparedStatement`.
2. Setze `PRODUKT_ID` an Position `1`.
3. Setze danach alten Bestand, neuen Bestand, Grund und Zeitpunkt.
4. Führe `mvn package` aus.

---

### Aufgabe 9 – Preisänderungen zu einem Produkt laden

Implementiere eine Methode `ladePreisAenderungen(int produktId)`.

```sql
SELECT ID, PRODUKT_ID, ALTER_PREIS, NEUER_PREIS, GRUND, ZEITPUNKT
FROM PREISAENDERUNG
WHERE PRODUKT_ID = ?
ORDER BY ZEITPUNKT
```

Auftrag:

1. Setze die `produktId` im `PreparedStatement`.
2. Lies das `ResultSet` mit `while (resultSet.next())`.
3. Erzeuge pro Zeile eine `PreisAenderung`.
4. Gib eine Liste zurück.

---

### Aufgabe 10 – Bestandsänderungen zu einem Produkt laden

Implementiere eine Methode `ladeBestandsAenderungen(int produktId)`.

```sql
SELECT ID, PRODUKT_ID, ALTER_BESTAND, NEUER_BESTAND, GRUND, ZEITPUNKT
FROM BESTANDSAENDERUNG
WHERE PRODUKT_ID = ?
ORDER BY ZEITPUNKT
```

Auftrag:

1. Arbeite gleich wie bei den Preisänderungen.
2. Verwende eine eigene Mapping-Methode.
3. Prüfe, ob nur Änderungen zum gewählten Produkt geladen werden.

---

## Vertiefung

### Aufgabe 11 – Mehrere Änderungen laden

Lege zu einem Produkt mehrere Preisänderungen und mehrere Bestandsänderungen an.

Auftrag:

1. Speichere mindestens zwei Preisänderungen.
2. Speichere mindestens zwei Bestandsänderungen.
3. Lade beide Listen wieder aus der Datenbank.
4. Gib die Änderungen aus.

Kontrolle:

```text
Die Ausgabe enthält nur Änderungen zum gewählten Produkt.
```

---

### Aufgabe 12 – Änderungen sortiert laden

Prüfe die Sortierung der Änderungen.

Auftrag:

1. Verwende `ORDER BY ZEITPUNKT`.
2. Lege Änderungen mit unterschiedlichen Zeitpunkten im ISO-Format an, zum Beispiel `2026-05-18T09:00`.
3. Prüfe, ob die Ausgabe in der erwarteten Reihenfolge erscheint.
4. Erkläre, warum eine sortierte Ausgabe für eine Änderungshistorie hilfreich ist.

---

### Aufgabe 13 – Mapping-Methoden auslagern

Lagere Mapping-Code in private Methoden aus.

Beispiele:

```java
private PreisAenderung lesePreisAenderung(ResultSet resultSet) throws SQLException
private BestandsAenderung leseBestandsAenderung(ResultSet resultSet) throws SQLException
```

Auftrag:

1. Suche doppelte oder lange Mapping-Blöcke.
2. Ersetze sie durch Methodenaufrufe.
3. Prüfe, ob das Verhalten gleich bleibt.
4. Führe `mvn package` aus.

---

### Aufgabe 14 – Doppelte JDBC-Logik reduzieren

Prüfe dein `AenderungsRepository`.

Auftrag:

1. Markiere wiederholte Schritte wie Verbindung herstellen, Statement vorbereiten und Exception behandeln.
2. Entscheide, welche Wiederholungen du akzeptierst.
3. Lagere nur einfache, gut verständliche Wiederholungen aus.
4. Vermeide eine zu allgemeine Lösung.

Ziel:

```text
Weniger Duplikate, aber weiterhin gut lesbarer EFZ-Code.
```

---

### Aufgabe 15 – Fehlerfälle behandeln

Teste oder diskutiere einfache Fehlerfälle.

Auftrag:

1. Was passiert, wenn eine Änderung mit unbekannter `PRODUKT_ID` gespeichert wird?
2. Was passiert, wenn `resultSet.next()` vergessen wird?
3. Was passiert, wenn `PRODUKT_ID` nicht im `PreparedStatement` gesetzt wird?
4. Notiere, ob der Fehler eher zu Datenbank, Mapping oder Fachlogik gehört.

---

### Aufgabe 16 – Repository-Namen diskutieren

Diskutiere die Namen deiner Repository-Klassen.

Auftrag:

1. Vergleiche `ProduktRepository` und `DbProduktRepository`.
2. Vergleiche `AenderungsRepository` und `DbAenderungsRepository`.
3. Notiere, welcher Name für deine aktuelle Lösung klarer ist.
4. Begründe deine Wahl in zwei bis drei Sätzen.

Hinweis:

```text
Ein Name soll die Verantwortung verständlich machen.
```

---

### Aufgabe 17 – Bestehende Services stabil halten

Prüfe deinen `LagerService`.

Auftrag:

1. Suche nach SQL-Anweisungen im Service.
2. Suche nach `ResultSet` oder `PreparedStatement` im Service.
3. Entferne solche Stellen, falls sie dort gelandet sind.
4. Erkläre, welche Fachlogik im Service bleiben soll.

Erwartung:

```text
Der Service kennt fachliche Abläufe.
Die Repositorys kennen Datenbankdetails.
```

---

## Transfer

### Aufgabe 18 – Warum Repository hilfreich wird

Beantworte schriftlich:

1. Warum reicht eine einzige grosse Persistenzklasse irgendwann nicht mehr gut aus?
2. Welche Wiederholungen entstehen bei mehreren Tabellen?
3. Warum ist ein Repository eine passende Strukturidee?

---

### Aufgabe 19 – Warum Mapping repetitiv wird

Vergleiche das Mapping von `Produkt`, `PreisAenderung` und `BestandsAenderung`.

Auftrag:

1. Notiere Gemeinsamkeiten.
2. Notiere Unterschiede.
3. Erkläre, warum spätere Persistenzframeworks solche Wiederholungen reduzieren können.
4. Nenne bewusst keine konkrete Framework-Lösung für diese Übung.

---

### Aufgabe 20 – Weitere mögliche Repositorys diskutieren

Überlege, welche Repositorys später entstehen könnten.

Beispiele:

```text
LieferantenRepository
BenutzerRepository
BestellRepository
InventurRepository
```

Auftrag:

1. Wähle zwei Beispiele.
2. Notiere, welche Daten diese Repositorys laden und speichern würden.
3. Notiere, welche Fachlogik trotzdem nicht in diese Repositorys gehört.

---

### Aufgabe 21 – Fachlogik getrennt halten

Erkläre an einem Beispiel:

```text
Ein Produktpreis darf nicht negativ werden.
```

Auftrag:

1. Entscheide, wo diese Regel geprüft werden soll.
2. Erkläre, warum sie nicht in die Mapping-Methode gehört.
3. Erkläre, was das Repository trotzdem speichern darf.

---

### Aufgabe 22 – Ausblick auf Persistenzframeworks

Diskutiert in der Gruppe:

1. Welche Arbeit wiederholt sich bei JDBC und Mapping?
2. Welche Fehler können durch Wiederholung entstehen?
3. Warum könnten ORM, Hibernate, JPA oder Spring Data später interessant sein?
4. Warum werden sie in dieser Einheit noch nicht verwendet?

Ziel:

```text
Du erkennst das Problem, bevor du später Werkzeuge dafür kennenlernst.
```

---

## Typische Fehlerbilder prüfen

Nutze diese Liste als kurze Selbstkontrolle:

- Kein JDBC-Code in `Main`.
- Kein Mapping-Code im `LagerService`.
- SQL und Fachlogik sind getrennt.
- Mapping-Code ist nicht unnötig doppelt.
- Repositorys übernehmen keine Fachregeln.
- Verantwortlichkeiten sind klar benannt.
- `ResultSet` wird mit `next()` gelesen.
- `PRODUKT_ID` verweist auf das richtige Produkt.
- `PreparedStatement`-Platzhalter passen zur SQL-Reihenfolge.

---

## Reflexion

Beantworte zum Abschluss:

1. Welche Daten gehören in deiner Lösung fachlich zusammen?
2. Warum helfen Repository-Klassen bei mehreren Tabellen?
3. Welche Verantwortung besitzt dein `ProduktRepository`?
4. Welche Verantwortung besitzt dein `AenderungsRepository`?
5. Warum wächst Mapping-Code mit der Anwendung?
6. Welche Teile der Anwendung blieben trotz neuer Tabellen stabil?
7. Welche Wiederholungen fallen dir im JDBC-Code auf?
