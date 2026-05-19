# Lösungen – Technische Konfiguration in Java

Diese Musterlösung zeigt eine kompakte Standardlösung für einfache technische Konfiguration in der bekannten Lagerverwaltung mit JDBC/H2 und Repositorys.

Kernidee:

```text
Technische Einstellungen stehen in .properties-Dateien.
Java lädt diese Werte beim Start.
Fachlogik bleibt im Service und wird nicht zur Konfiguration.
```

Bewusst nicht verwendet werden Spring, Dependency Injection, YAML-Dateien, Docker, Kubernetes oder komplexe Konfigurationsframeworks.

---

## 1. Hartcodierte Werte erkennen

Typische technische Werte aus der Lagerverwaltung:

| Wert | Einordnung |
|---|---|
| `jdbc:h2:./data/lager` | technische Konfiguration |
| `data/produkte.csv` | technische Konfiguration |
| `INFO` | vorbereiteter technischer Logging-Wert |
| `embedded` | technischer H2-Modus |

Keine technische Konfiguration sind fachliche Regeln wie:

- Preis darf nicht negativ sein
- Bestand darf nicht unkontrolliert verändert werden
- eine Preisänderung wird fachlich protokolliert

---

## 2. `app.properties`

Datei `config/app.properties`:

```properties
db.url=jdbc:h2:./data/lager
db.user=sa
db.password=
produkt.datei=data/produkte.csv
logging.level=INFO
h2.mode=embedded
```

Hinweis: `db.password` wird in dieser einfachen Übung gezeigt, aber nicht ausgegeben oder geloggt.

---

## 3. Properties-Datei laden

Datei `src/main/java/ch/allianz/youngoitv/lager/config/KonfigurationLaden.java`:

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

Wichtig:

- `try-with-resources` schliesst die Datei.
- Die Exception wird nicht verschluckt.
- Diese Klasse lädt nur technische Werte und enthält keine Fachlogik.

---

## 4. Einfache Konfigurationsklasse

Datei `src/main/java/ch/allianz/youngoitv/lager/config/AppConfig.java`:

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

    public void validiere() {
        dbUrl();
        produktDatei();

        String mode = h2Mode();
        if (!mode.equals("embedded") && !mode.equals("server")) {
            throw new IllegalStateException("Ungültiger h2.mode: " + mode);
        }
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

Die Klasse bündelt die Schlüssel. Dadurch steht `"db.url"` nicht an vielen Stellen im Projekt.

---

## 5. DB-URL im Repository verwenden

Beispiel für ein Repository mit konfigurierter DB-URL:

```java
package ch.allianz.youngoitv.lager.repository;

public class ProduktRepository {

    private final String dbUrl;
    private final String dbUser;
    private final String dbPassword;

    public ProduktRepository(String dbUrl, String dbUser, String dbPassword) {
        this.dbUrl = dbUrl;
        this.dbUser = dbUser;
        this.dbPassword = dbPassword;
    }

    public String beschreibeVerbindung() {
        return "DB-URL: " + dbUrl + ", Benutzer: " + dbUser;
    }
}
```

In einer echten JDBC-Methode würde der Verbindungsaufbau dann mit diesen Werten arbeiten:

```java
DriverManager.getConnection(dbUrl, dbUser, dbPassword);
```

Das Passwort wird nicht ausgegeben und nicht geloggt.

---

## 6. `Main` mit zentraler Konfiguration

Datei `src/main/java/ch/allianz/youngoitv/lager/Main.java`:

```java
package ch.allianz.youngoitv.lager;

import ch.allianz.youngoitv.lager.config.AppConfig;
import ch.allianz.youngoitv.lager.config.KonfigurationLaden;
import ch.allianz.youngoitv.lager.repository.ProduktRepository;

import java.util.Properties;

public class Main {

    public static void main(String[] args) {
        String configPfad = "config/app.properties";
        if (args.length > 0) {
            configPfad = args[0];
        }

        Properties properties = KonfigurationLaden.ladeProperties(configPfad);
        AppConfig config = new AppConfig(properties);
        config.validiere();

        System.out.println("Produktdatei: " + config.produktDatei());
        System.out.println("H2-Modus: " + config.h2Mode());
        System.out.println("Logging-Level: " + config.loggingLevel());

        // Kontrollausgabe für diese Übung: sensible Werte wie Passwörter nicht ausgeben.
        ProduktRepository produktRepository = new ProduktRepository(
                config.dbUrl(),
                config.dbUser(),
                config.dbPassword()
        );

        System.out.println(produktRepository.beschreibeVerbindung());
    }
}
```

`Main` lädt die Konfiguration und baut die technischen Objekte zusammen. Die Fachlogik bleibt weiterhin im `LagerService`.

---

## 7. Dateipfade konfigurieren

Der Wert aus `produkt.datei` kann später an eine CSV- oder Exportklasse übergeben werden:

```java
String produktDatei = config.produktDatei();
```

Beispiele:

```properties
produkt.datei=data/produkte.csv
```

```properties
produkt.datei=data/produkte-test.csv
```

Der Java-Code bleibt gleich. Nur die Konfigurationsdatei ändert sich.

---

## 8. Standardwerte

Sinnvolle Standardwerte:

```java
public String dbUser() {
    return properties.getProperty("db.user", "sa");
}

public String dbPassword() {
    return properties.getProperty("db.password", "");
}

public String loggingLevel() {
    return properties.getProperty("logging.level", "INFO");
}

public String h2Mode() {
    return properties.getProperty("h2.mode", "embedded");
}
```

Pflichtwerte ohne Standardwert:

- `db.url`, weil ohne DB-URL keine Datenbankverbindung möglich ist
- `produkt.datei`, wenn die Anwendung diesen Dateipfad braucht

---

## 9. Embedded vs. Server-H2

Embedded-Konfiguration:

```properties
db.url=jdbc:h2:./data/lager
db.user=sa
db.password=
produkt.datei=data/produkte.csv
logging.level=INFO
h2.mode=embedded
```

Server-Konfiguration:

```properties
db.url=jdbc:h2:tcp://localhost/./data/lager
db.user=sa
db.password=
produkt.datei=data/produkte.csv
logging.level=INFO
h2.mode=server
```

Unterschied:

- `embedded`: Die Anwendung öffnet die H2-Datenbank direkt als eingebettete Datenbank.
- `server`: Die Anwendung verbindet sich zu einem laufenden H2-Server.

Wenn kein H2-Server läuft, muss die Server-Variante nicht erfolgreich starten. Für diese Einheit reicht, dass der Unterschied über die Konfiguration sichtbar wird.

---

## 10. Fehlerfälle

Fehlende DB-URL:

```properties
db.url=
```

Erwartete Meldung:

```text
Pflichtwert fehlt: db.url
```

Ungültiger H2-Modus:

```properties
h2.mode=cloud
```

Erwartete Meldung:

```text
Ungültiger h2.mode: cloud
```

Fehlender Produktdateipfad:

```properties
produkt.datei=
```

Erwartete Meldung:

```text
Pflichtwert fehlt: produkt.datei
```

---

## 11. Typische Fehlerhinweise

- DB-URL bleibt im Repository hartcodiert.
- Properties-Datei wird ohne `try-with-resources` geöffnet.
- Fehlende Pflichtwerte werden erst später als unklare Fehler sichtbar.
- `db.password` wird auf der Konsole ausgegeben oder geloggt.
- `properties.getProperty(...)` wird in vielen Klassen verteilt.
- Konfiguration wird in jeder Repository-Methode neu geladen.
- Fachregeln werden in `.properties` ausgelagert.
- `.properties` für technische Konfiguration wird mit I18N und `ResourceBundle` verwechselt.

---

## 12. Kurze Reflexionsantworten

**Welche Werte waren bisher hartcodiert?**

Typisch sind DB-URL, Dateipfade, H2-Modus und vorbereitete Logging-Werte.

**Welche Vorteile bringt technische Konfiguration?**

Die Anwendung kann mit anderen technischen Einstellungen laufen, ohne Java-Code zu ändern.

**Welche Konfiguration gehört nicht in Fachlogik?**

DB-URL, Dateipfade, Benutzername, Passwort, Logging-Level und H2-Modus gehören nicht in den `LagerService` und nicht in Fachobjekte wie `Produkt`.

**Welche Probleme entstehen ohne Konfiguration?**

Technische Werte verteilen sich im Code. Änderungen werden fehleranfällig, weil mehrere Klassen angepasst werden müssen.

**Warum hilft zentrale Konfiguration?**

Schlüssel wie `db.url` stehen an einem Ort. Fehler können beim Start erkannt werden. Repositorys bekommen fertige technische Werte und laden die Datei nicht selbst.

---

## 13. Verifikation

Die Java-Beispiele aus dieser Musterlösung wurden in einem temporären Maven-Projekt geprüft.

Ausgeführt:

```bash
mvn package
```

Zusätzlich wurde `Main` mit zwei gültigen Konfigurationsdateien ausgeführt:

```bash
java -cp target/classes ch.allianz.youngoitv.lager.Main
java -cp target/classes ch.allianz.youngoitv.lager.Main config/app-server.properties
```

Ergebnis:

```text
BUILD SUCCESS
Main liest die Konfigurationswerte aus .properties-Dateien.
Embedded- und Server-Konfiguration werden als unterschiedliche Werte sichtbar.
```

Einschränkung: Es wurde keine echte H2-Verbindung geöffnet, weil der Fokus dieser Musterlösung auf dem Laden und Weitergeben technischer Konfiguration liegt.
