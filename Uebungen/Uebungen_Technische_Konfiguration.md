# Übungen – Technische Konfiguration in Java

## Vorwissen

Du brauchst:

- bekannte Lagerverwaltung
- Maven-Projektstruktur
- `Main`
- `LagerService`
- `ProduktRepository`
- `AenderungsRepository`
- JDBC mit H2
- Grundidee von technischem Logging
- Grundidee von Verantwortlichkeiten

Nicht verwendet werden:

- Spring
- Dependency Injection
- YAML
- Docker
- Kubernetes
- komplexe Konfigurationsframeworks
- I18N mit `ResourceBundle`

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
Du lagerst technische Einstellungen aus dem Java-Code aus
und lädst sie aus einer einfachen .properties-Datei.
```

---

## Vorbereitung

Arbeite mit der bekannten Lagerverwaltung mit Repositorys.

Beispielstruktur:

```text
lagerverwaltung-db/
  pom.xml
  config/
    app.properties
  data/
  src/main/java/
    ch/allianz/youngoitv/lager/
      Main.java
      LagerService.java
      config/AppConfig.java
      config/KonfigurationLaden.java
      repository/ProduktRepository.java
      repository/AenderungsRepository.java
      model/Produkt.java
      model/PreisAenderung.java
      model/BestandsAenderung.java
```

Falls dein Projekt leicht anders aufgebaut ist, passe die Package-Namen sinnvoll an.

---

## Basis

### Aufgabe 1 – Hartcodierte technische Werte finden

Suche in deinem Projekt technische Werte, die direkt im Code stehen.

Typische Beispiele:

```text
jdbc:h2:./data/lager
data/produkte.csv
INFO
embedded
```

Auftrag:

1. Notiere mindestens drei technische Werte.
2. Markiere, in welcher Klasse sie stehen.
3. Entscheide, ob der Wert technische Konfiguration oder Fachlogik ist.

Erwartung:

```text
DB-URL, Dateipfade und technische Modi sind technische Konfiguration.
Preisregeln und Bestandsregeln sind Fachlogik.
```

---

### Aufgabe 2 – `app.properties` erstellen

Erstelle den Ordner `config` und darin die Datei `app.properties`.

Inhalt:

```properties
db.url=jdbc:h2:./data/lager
db.user=sa
db.password=
produkt.datei=data/produkte.csv
logging.level=INFO
h2.mode=embedded
```

Auftrag:

1. Schreibe jeden Wert als Schlüssel-Wert-Paar.
2. Verwende keine YAML-Datei.
3. Lege keine Spring-Konfiguration an.

---

### Aufgabe 3 – Properties-Datei lesen

Erstelle eine Klasse `KonfigurationLaden`.

```java
package ch.allianz.youngoitv.lager.config;

import java.io.IOException;
import java.io.InputStream;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.Properties;

public class KonfigurationLaden {

    public static Properties ladeProperties(String pfad) {
        Properties properties = new Properties();

        try (InputStream input = Files.newInputStream(Path.of(pfad))) {
            properties.load(input);
            return properties;
        } catch (IOException exception) {
            throw new IllegalStateException("Konfiguration konnte nicht geladen werden: " + pfad, exception);
        }
    }
}
```

Auftrag:

1. Passe das Package an dein Projekt an.
2. Verwende `try-with-resources`.
3. Verschlucke die Exception nicht.

---

### Aufgabe 4 – Konfigurationswerte ausgeben

Lade in `Main` die Datei `config/app.properties` und gib die wichtigsten Werte aus.

```java
Properties properties = KonfigurationLaden.ladeProperties("config/app.properties");

System.out.println("DB-URL: " + properties.getProperty("db.url"));
System.out.println("Produktdatei: " + properties.getProperty("produkt.datei"));
System.out.println("H2-Modus: " + properties.getProperty("h2.mode"));
System.out.println("Logging-Level: " + properties.getProperty("logging.level"));
```

Auftrag:

1. Ergänze die nötigen Imports.
2. Starte die Anwendung mit Maven oder baue sie mit `mvn package`.
3. Prüfe, ob die Werte aus der Datei angezeigt werden.

Wichtig:

```text
Gib db.password nicht aus.
Diese Ausgabe dient nur zur Kontrolle beim Lernen.
```

---

### Aufgabe 5 – DB-URL aus Konfiguration laden

Suche die bisher hartcodierte H2-URL.

Beispiel vorher:

```java
private final String dbUrl = "jdbc:h2:./data/lager";
```

Beispiel nachher:

```java
private final String dbUrl;

public ProduktRepository(String dbUrl) {
    this.dbUrl = dbUrl;
}
```

Auftrag:

1. Entferne die hartcodierte DB-URL aus der Repository-Klasse.
2. Lies `db.url` in `Main` aus der Konfiguration.
3. Übergib die DB-URL an das Repository.
4. Prüfe mit `mvn package`.

Erwartung:

```text
Das Repository verwendet eine konfigurierte DB-URL.
```

---

### Aufgabe 6 – Dateipfad aus Konfiguration laden

Lies `produkt.datei` aus der Konfiguration.

Auftrag:

1. Suche eine Stelle, an der ein Dateipfad im Code steht.
2. Ersetze den hartcodierten Pfad durch den Wert aus `produkt.datei`.
3. Prüfe, dass die Anwendung weiterhin startet.

Falls dein Projekt aktuell keine CSV-Datei mehr verwendet, ergänze nur eine Ausgabe in `Main` und erkläre kurz, wofür der Wert später verwendet werden könnte.

---

### Aufgabe 7 – Bestehende H2-Konfiguration auslagern

Verschiebe alle H2-bezogenen Startwerte in `app.properties`.

Mindestens:

```properties
db.url=jdbc:h2:./data/lager
db.user=sa
db.password=
h2.mode=embedded
```

Auftrag:

1. Entferne feste H2-Werte aus `Main` oder Repositorys, soweit sie dort stehen.
2. Lies die Werte aus der Konfiguration.
3. Übergib sie an die technische Infrastruktur.

---

### Aufgabe 8 – Logging-Level vorbereiten

Lies `logging.level` aus der Konfiguration.

Auftrag:

1. Verwende als Standardwert `INFO`.
2. Gib den Wert beim Start aus.
3. Ändere den Wert in der Datei auf `DEBUG` und starte erneut.

Erwartung:

```text
Die Anwendung liest den neuen Wert, ohne dass Java-Code geändert wird.
```

Hinweis: Die eigentliche Logback-Konfiguration wird hier nicht vertieft.

---

### Aufgabe 9 – `Main` vereinfachen

Prüfe deine `Main`-Klasse.

Auftrag:

1. `Main` darf die Konfiguration laden.
2. `Main` soll nicht überall einzelne technische Strings hartcodieren.
3. `Main` soll Fachlogik weiterhin nicht selbst ausführen.

Kurze Kontrolle:

```text
Main startet die Anwendung.
Service enthält Fachlogik.
Repository enthält Datenzugriff.
Konfiguration liefert technische Einstellungen.
```

---

## Vertiefung

### Aufgabe 10 – Fehlende Properties behandeln

Entferne testweise `db.url` aus `app.properties`.

Auftrag:

1. Starte die Anwendung.
2. Beobachte die Fehlermeldung.
3. Verbessere den Code so, dass klar gemeldet wird:

```text
Pflichtwert fehlt: db.url
```

Erwartung:

```text
Ein fehlender Pflichtwert führt zu einer verständlichen Fehlermeldung.
```

---

### Aufgabe 11 – Standardwerte ergänzen

Verwende für Werte, die fehlen dürfen, Standardwerte.

Beispiele:

```java
String dbUser = properties.getProperty("db.user", "sa");
String loggingLevel = properties.getProperty("logging.level", "INFO");
String h2Mode = properties.getProperty("h2.mode", "embedded");
```

Auftrag:

1. Entscheide, welche Werte Pflichtwerte sind.
2. Entscheide, welche Werte sinnvolle Standardwerte haben.
3. Begründe deine Entscheidung kurz.

---

### Aufgabe 12 – Embedded vs. Server-H2 umschalten

Erstelle zwei Konfigurationsvarianten.

`config/app-embedded.properties`:

```properties
db.url=jdbc:h2:./data/lager
db.user=sa
db.password=
produkt.datei=data/produkte.csv
logging.level=INFO
h2.mode=embedded
```

`config/app-server.properties`:

```properties
db.url=jdbc:h2:tcp://localhost/./data/lager
db.user=sa
db.password=
produkt.datei=data/produkte.csv
logging.level=INFO
h2.mode=server
```

Auftrag:

1. Vergleiche die beiden DB-URLs.
2. Erkläre den Unterschied zwischen `embedded` und `server`.
3. Starte nur die Variante, die in deiner Umgebung realistisch vorbereitet ist.

Wichtig:

```text
Wenn kein H2-Server läuft, muss die Server-Variante nicht erfolgreich starten.
Der Unterschied soll aber fachlich erklärt werden können.
```

---

### Aufgabe 13 – Konfiguration zentral bündeln

Erstelle eine Klasse `AppConfig`.

```java
package ch.allianz.youngoitv.lager.config;

import java.util.Properties;

public class AppConfig {

    private final Properties properties;

    public AppConfig(Properties properties) {
        this.properties = properties;
    }

    public String dbUrl() {
        return pflichtwert("db.url");
    }

    public String dbUser() {
        return properties.getProperty("db.user", "sa");
    }

    public String dbPassword() {
        return properties.getProperty("db.password", "");
    }

    public String produktDatei() {
        return pflichtwert("produkt.datei");
    }

    public String loggingLevel() {
        return properties.getProperty("logging.level", "INFO");
    }

    public String h2Mode() {
        return properties.getProperty("h2.mode", "embedded");
    }

    private String pflichtwert(String key) {
        String value = properties.getProperty(key);
        if (value == null || value.isBlank()) {
            throw new IllegalStateException("Pflichtwert fehlt: " + key);
        }
        return value;
    }
}
```

Auftrag:

1. Passe das Package an dein Projekt an.
2. Verwende `AppConfig` in `Main`.
3. Vermeide direkte `getProperty(...)`-Aufrufe in mehreren Klassen.

---

### Aufgabe 14 – Konfiguration validieren

Ergänze in `AppConfig` eine Methode:

```java
public void validiere() {
    dbUrl();
    produktDatei();

    String mode = h2Mode();
    if (!mode.equals("embedded") && !mode.equals("server")) {
        throw new IllegalStateException("Ungültiger h2.mode: " + mode);
    }
}
```

Auftrag:

1. Rufe `config.validiere()` beim Start auf.
2. Teste `h2.mode=cloud`.
3. Prüfe, ob eine verständliche Fehlermeldung erscheint.

---

### Aufgabe 15 – Properties-Datei bewusst fehlerhaft testen

Teste nacheinander diese Fehler:

```properties
db.url=
```

```properties
h2.mode=cloud
```

```properties
produkt.datei=
```

Auftrag:

1. Notiere pro Fehler die beobachtete Meldung.
2. Verbessere unklare Meldungen.
3. Stelle am Schluss wieder eine gültige `app.properties` her.
4. Prüfe mit `mvn package`.

---

## Transfer

### Aufgabe 16 – Warum ist Konfiguration keine Fachlogik?

Erkläre an zwei Beispielen:

```text
db.url
produkt.datei
```

Warum sind diese Werte technische Konfiguration und keine Fachlogik?

---

### Aufgabe 17 – Warum wird Hardcoding problematisch?

Beschreibe, was passiert, wenn diese Werte im Code verteilt sind:

- DB-URL
- Dateipfad
- Logging-Level
- H2-Modus

Beantworte:

```text
Was muss geändert werden, wenn die Anwendung mit einer Testdatenbank laufen soll?
```

---

### Aufgabe 18 – Welche Werte sollten konfigurierbar sein?

Entscheide für jeden Wert:

| Wert | Konfiguration oder Fachlogik? |
|---|---|
| `jdbc:h2:./data/lager` |  |
| `data/produkte.csv` |  |
| maximal erlaubter negativer Bestand |  |
| `DEBUG` |  |
| Mindestpreis eines Produkts |  |
| `server` oder `embedded` |  |

Begründe mindestens drei Entscheidungen.

---

### Aufgabe 19 – Weitere technische Konfigurationen diskutieren

Diskutiere, welche weiteren technischen Werte später konfigurierbar sein könnten.

Mögliche Beispiele:

- Exportpfad
- Backup-Pfad
- maximale Anzahl Verbindungen
- technischer Timeout
- Name einer Logdatei

Wichtig:

```text
Diskutiere nur die Idee.
Baue kein komplexes Konfigurationsframework.
```

---

### Aufgabe 20 – Warum wird Konfiguration für grössere Anwendungen wichtig?

Schreibe eine kurze Antwort mit diesen Begriffen:

```text
Entwicklungsumgebung
Testumgebung
Produktivumgebung
gleicher Java-Code
andere technische Einstellungen
```

Erwartung:

```text
Die Anwendung kann in verschiedenen Umgebungen laufen,
ohne dass der Java-Code für jede Umgebung geändert wird.
```

---

## Typische Fehler prüfen

Prüfe dein Ergebnis anhand dieser Liste:

- Ist die DB-URL noch irgendwo hartcodiert?
- Wird die Properties-Datei mit `try-with-resources` geschlossen?
- Werden fehlende Pflichtwerte verständlich behandelt?
- Ist Konfiguration nicht in Fachobjekte wie `Produkt` gemischt?
- Werden sensible Werte wie `db.password` nicht direkt geloggt oder ausgegeben?
- Wird Konfiguration nicht in jeder Repository-Methode neu geladen?
- Wird `.properties` hier nicht mit I18N verwechselt?

---

## Reflexion

Beantworte zum Abschluss:

1. Welche Werte waren bisher hartcodiert?
2. Welche Vorteile bringt technische Konfiguration?
3. Welche Konfiguration gehört nicht in Fachlogik?
4. Welche Probleme entstehen ohne Konfiguration?
5. Warum hilft zentrale Konfiguration?
