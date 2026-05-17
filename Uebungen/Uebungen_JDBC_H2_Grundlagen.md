# Übungen – JDBC mit eingebetteter H2-Datenbank

## Vorwissen

Du brauchst:

- Maven-Projektstruktur
- Klassen und Objekte
- einfache Packages
- `ArrayList`
- `Produkt`, `LagerService` und `ProduktSpeicher`
- CSV-Persistenz als bekannte Vergleichsbasis
- einfache JUnit- oder Konsolenprüfungen

Nicht verwendet werden:

- ORM
- Hibernate
- JPA
- Spring Data
- formales Repository Pattern
- Connection Pooling
- komplexe SQL-Joins
- vertiefte Transaktionen

---

## Vorbereitung

Arbeite mit einer kleinen Lagerverwaltung.

Beispielstruktur:

```text
lagerverwaltung-jdbc/
  pom.xml
  data/
  src/main/java/
    ch/allianz/youngoitv/lager/
      Main.java
      LagerService.java
      ProduktSpeicher.java
      CsvProduktSpeicher.java
      DbDemo.java
      model/Produkt.java
```

Für diese Übungen darfst du zuerst mit `DbDemo` arbeiten. Danach kannst du die Idee in einen `DbProduktSpeicher` übertragen.

Hinweis zu H2 Embedded:

```text
Die Datenbank bleibt in data/lager.mv.db gespeichert.
Wenn du neu beginnen willst, stoppe das Programm und lösche diese Datei.
```

Für die Basisaufgaben mit festen IDs ist eine frische Datenbank am einfachsten. Sonst können IDs höher sein oder Produkte aus früheren Läufen erneut erscheinen.

Prüfe nach praktischen Änderungen:

```bash
mvn package
```

Wenn Tests vorhanden sind:

```bash
mvn test
```

---

## Basis

### Aufgabe 1 – H2-Dependency ergänzen

Ergänze in `pom.xml` im Abschnitt `<dependencies>`:

```xml
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <version>2.2.224</version>
</dependency>
```

Auftrag:

1. Speichere die `pom.xml`.
2. Führe `mvn package` aus.
3. Prüfe, ob Maven die Dependency akzeptiert.
4. Prüfe bei einem neuen Projekt, ob Java 21 in der `pom.xml` konfiguriert ist.

Erwartung:

```text
BUILD SUCCESS
```

Hinweis:

```text
Wenn Maven mit Source option 5 oder Target option 5 fehlschlägt,
fehlt wahrscheinlich eine aktuelle Compiler-Konfiguration.
```

---

### Aufgabe 2 – Embedded-H2 starten

Erstelle eine Klasse `DbDemo`.

```java
package ch.allianz.youngoitv.lager;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class DbDemo {
    private static final String URL = "jdbc:h2:./data/lager";

    public static void main(String[] args) throws SQLException {
        try (Connection connection = DriverManager.getConnection(URL)) {
            System.out.println("Verbindung hergestellt");
        }
    }
}
```

Auftrag:

1. Starte die Klasse über deine IDE oder über Maven.
2. Prüfe, ob die Ausgabe erscheint.
3. Schaue nach, ob im Ordner `data` eine H2-Datei entsteht.

Start nach `mvn package`, falls du nicht über die IDE startest:

```bash
java -cp target/classes:$HOME/.m2/repository/com/h2database/h2/2.2.224/h2-2.2.224.jar ch.allianz.youngoitv.lager.DbDemo
```

---

### Aufgabe 3 – Tabelle `PRODUKT` erstellen

Ergänze in `DbDemo` eine Methode:

```java
private static void tabelleErstellen(Connection connection) throws SQLException {
    String sql = """
            CREATE TABLE IF NOT EXISTS PRODUKT (
                ID INT AUTO_INCREMENT PRIMARY KEY,
                NAME VARCHAR(100) NOT NULL,
                PREIS DOUBLE NOT NULL,
                BESTAND INT NOT NULL
            )
            """;

    try (PreparedStatement statement = connection.prepareStatement(sql)) {
        statement.executeUpdate();
    }
}
```

Auftrag:

1. Ergänze den Import für `PreparedStatement`.
2. Rufe die Methode nach dem Verbindungsaufbau auf.
3. Starte das Programm zweimal.
4. Erkläre, warum `IF NOT EXISTS` hilfreich ist.

---

### Aufgabe 4 – Produkt einfügen

Ergänze:

```java
private static void produktEinfuegen(Connection connection, String name, double preis, int bestand)
        throws SQLException {
    String sql = "INSERT INTO PRODUKT (NAME, PREIS, BESTAND) VALUES (?, ?, ?)";

    try (PreparedStatement statement = connection.prepareStatement(sql)) {
        statement.setString(1, name);
        statement.setDouble(2, preis);
        statement.setInt(3, bestand);
        statement.executeUpdate();
    }
}
```

Auftrag:

1. Füge `Maus`, `24.90`, `10` ein.
2. Füge `Tastatur`, `79.90`, `5` ein.
3. Verwende keine String-Verkettung für die Werte.

---

### Aufgabe 5 – Produkte lesen

Ergänze:

```java
private static void produkteAusgeben(Connection connection) throws SQLException {
    String sql = "SELECT ID, NAME, PREIS, BESTAND FROM PRODUKT ORDER BY ID";

    try (PreparedStatement statement = connection.prepareStatement(sql);
         ResultSet resultSet = statement.executeQuery()) {

        while (resultSet.next()) {
            int id = resultSet.getInt("ID");
            String name = resultSet.getString("NAME");
            double preis = resultSet.getDouble("PREIS");
            int bestand = resultSet.getInt("BESTAND");

            System.out.println(id + ": " + name + " / " + preis + " / " + bestand);
        }
    }
}
```

Auftrag:

1. Ergänze den Import für `ResultSet`.
2. Rufe die Methode nach dem Einfügen auf.
3. Erkläre, warum `while (resultSet.next())` nötig ist.

Erwartete Ausgabe bei frischer Datenbank sinngemäss:

```text
1: Maus / 24.9 / 10
2: Tastatur / 79.9 / 5
```

---

### Aufgabe 6 – Produkt aktualisieren

Ergänze:

```java
private static void bestandAktualisieren(Connection connection, int id, int neuerBestand)
        throws SQLException {
    String sql = "UPDATE PRODUKT SET BESTAND = ? WHERE ID = ?";

    try (PreparedStatement statement = connection.prepareStatement(sql)) {
        statement.setInt(1, neuerBestand);
        statement.setInt(2, id);
        statement.executeUpdate();
    }
}
```

Auftrag:

1. Ändere den Bestand von Produkt `1` auf `7`.
2. Lies danach alle Produkte erneut.
3. Prüfe, ob die Änderung sichtbar ist.

---

### Aufgabe 7 – Produkt löschen

Ergänze:

```java
private static void produktLoeschen(Connection connection, int id) throws SQLException {
    String sql = "DELETE FROM PRODUKT WHERE ID = ?";

    try (PreparedStatement statement = connection.prepareStatement(sql)) {
        statement.setInt(1, id);
        statement.executeUpdate();
    }
}
```

Auftrag:

1. Lösche ein Produkt nach ID.
2. Lies danach alle Produkte erneut.
3. Prüfe, ob nur das gewünschte Produkt entfernt wurde.

---

## Vertiefung

### Aufgabe 8 – Mehrere Produkte speichern

Erstelle eine `ArrayList<Produkt>` mit mindestens drei Produkten.

Auftrag:

1. Durchlaufe die Liste mit einer Schleife.
2. Speichere jedes Produkt mit `produktEinfuegen(...)`.
3. Lies die Produkte danach aus der Datenbank.
4. Vergleiche die Ausgabe mit der ursprünglichen Liste.

---

### Aufgabe 9 – Produkt nach ID suchen

Schreibe eine Methode:

```java
private static void produktNachIdAusgeben(Connection connection, int id) throws SQLException {
    // SELECT mit WHERE ID = ?
}
```

Auftrag:

1. Verwende `PreparedStatement`.
2. Setze die ID mit `statement.setInt(1, id)`.
3. Verwende `if (resultSet.next())`.
4. Gib eine Meldung aus, wenn kein Produkt gefunden wurde.

---

### Aufgabe 10 – Ungültige Werte behandeln

Vor dem Speichern sollen ungültige Werte abgelehnt werden.

Beispiele:

| Wert | Behandlung |
|---|---|
| leerer Name | nicht speichern |
| negativer Preis | nicht speichern |
| negativer Bestand | nicht speichern |

Auftrag:

1. Entscheide, ob diese Prüfung in `LagerService`, `Produkt` oder `DbDemo` gehört.
2. Begründe deine Entscheidung.
3. Ergänze eine einfache Prüfung vor dem Speichern.

Hinweis:

```text
Fachliche Regeln gehören nicht direkt in SQL-Code.
Die Begründung ist wichtiger als eine perfekte Zielstruktur.
```

---

### Aufgabe 11 – Ressourcen korrekt schliessen

Suche in deinem Code:

- `Connection`
- `PreparedStatement`
- `ResultSet`

Auftrag:

1. Prüfe, ob alle Ressourcen in `try (...)` stehen.
2. Notiere, was automatisch geschlossen wird.
3. Erkläre, warum das wichtig ist.

---

### Aufgabe 12 – CSV und Datenbank vergleichen

Fülle die Tabelle aus.

| Frage | CSV | H2-Datenbank |
|---|---|---|
| Wie werden Daten gespeichert? | | |
| Wie wird ein Produkt gelesen? | | |
| Wie wird ein Produkt geändert? | | |
| Wo liegt die Struktur der Daten? | | |
| Was ist einfacher? | | |
| Was ist gezielter abfragbar? | | |

---

## Transfer

### Aufgabe 13 – H2 im Server-Modus starten

Starte H2 testweise als separaten Prozess.

Beispiel:

```bash
java -cp ~/.m2/repository/com/h2database/h2/2.2.224/h2-2.2.224.jar org.h2.tools.Server -tcp -ifNotExists
```

Passe danach die JDBC-URL an:

```java
private static final String URL = "jdbc:h2:tcp://localhost/./data/lager";
```

Auftrag:

1. Erkläre, welcher Teil der URL neu ist.
2. Starte dein Java-Programm.
3. Vergleiche das Verhalten mit Embedded-H2.

---

### Aufgabe 14 – Embedded und Server vergleichen

Beantworte kurz:

1. Wo läuft H2 im Embedded-Modus?
2. Wo läuft H2 im Server-Modus?
3. Welche Variante ist für erste Übungen einfacher?
4. Welche Variante wirkt näher an einer echten Datenbankumgebung?

---

### Aufgabe 15 – `DbProduktSpeicher` als Idee diskutieren

Skizziere eine Klasse:

```text
DbProduktSpeicher implements ProduktSpeicher
```

Auftrag:

1. Welche Methoden müsste die Klasse aus `ProduktSpeicher` umsetzen?
2. Welche SQL-Befehle würden darin vorkommen?
3. Welche Klassen sollten keinen SQL-Code enthalten?
4. Warum bleibt `LagerService` unabhängig von CSV oder Datenbank?

---

### Aufgabe 16 – Vorteile und Grenzen beschreiben

Notiere je drei Punkte.

| Thema | Punkte |
|---|---|
| Vorteile einer Datenbank gegenüber CSV | |
| Vorteile von CSV gegenüber einer Datenbank | |
| Situationen, in denen H2 Embedded sinnvoll ist | |
| Situationen, in denen Server-Modus sinnvoller ist | |

---

## Typische Fehler als Diagnose

Ordne jedem Fehler eine Folge und eine Verbesserung zu.

| Fehler | Folge | Verbesserung |
|---|---|---|
| `Connection` nicht geschlossen | | |
| SQL mit `+` zusammengebaut | | |
| `ResultSet.next()` vergessen | | |
| Embedded-URL und Server-URL verwechselt | | |
| SQL in `LagerService` geschrieben | | |
| Exception leer abgefangen | | |

---

## Reflexion

- Wann ist CSV ausreichend?
- Wann hilft eine Datenbank?
- Welche Verantwortung bleibt beim `LagerService`?
- Warum ist Persistenz austauschbar?
- Was ist der Unterschied zwischen Embedded und Server-Modus?
- Welche Stelle war beim ersten JDBC-Code am fehleranfälligsten?
