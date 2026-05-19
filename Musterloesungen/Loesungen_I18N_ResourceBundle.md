# Lösungen – Mehrsprachigkeit mit Locale und ResourceBundle

Diese Musterlösung zeigt eine kompakte Standardlösung für einfache Mehrsprachigkeit in der bekannten Lagerverwaltung.

Kernidee:

```text
Sichtbare Texte stehen in messages_*.properties.
Java lädt die passende Sprachdatei mit ResourceBundle.
Fachlogik und technische Konfiguration bleiben getrennt.
```

Bewusst nicht verwendet werden Frameworks, Web-I18N, Spring I18N, ICU, automatische Übersetzungsdienste oder komplexe Formatierungsframeworks.

---

## 1. Hartcodierte Texte erkennen

Typische sichtbare Texte aus `Main`:

| Text | Einordnung |
|---|---|
| `Willkommen in der Lagerverwaltung.` | I18N |
| `Produkt wurde gespeichert.` | I18N |
| `Produkt wurde nicht gefunden.` | I18N |
| `Ein Fehler ist aufgetreten.` | I18N |

Keine I18N-Texte sind technische Werte wie:

- `jdbc:h2:./data/lager`
- `data/produkte.csv`
- `INFO`
- `embedded`

Diese Werte gehören zur technischen Konfiguration, nicht in `messages_*.properties`.

---

## 2. Deutsche Sprachdatei

Datei `src/main/resources/messages_de.properties`:

```properties
app.title=Lagerverwaltung
app.welcome=Willkommen in der Lagerverwaltung.
produkt.gespeichert=Produkt wurde gespeichert.
produkt.nichtGefunden=Produkt wurde nicht gefunden.
fehler.allgemein=Ein Fehler ist aufgetreten.
fehler.produktSpeichern=Produkt konnte nicht gespeichert werden.
```

---

## 3. Französische Sprachdatei

Datei `src/main/resources/messages_fr.properties`:

```properties
app.title=Gestion du stock
app.welcome=Bienvenue dans la gestion du stock.
produkt.gespeichert=Produit enregistré.
produkt.nichtGefunden=Produit introuvable.
fehler.allgemein=Une erreur est survenue.
fehler.produktSpeichern=Le produit n'a pas pu être enregistré.
```

---

## 4. Italienische Sprachdatei

Datei `src/main/resources/messages_it.properties`:

```properties
app.title=Gestione magazzino
app.welcome=Benvenuto nella gestione magazzino.
produkt.gespeichert=Prodotto salvato.
produkt.nichtGefunden=Prodotto non trovato.
fehler.allgemein=Si è verificato un errore.
fehler.produktSpeichern=Impossibile salvare il prodotto.
```

Wichtig: Alle drei Dateien verwenden dieselben Schlüssel. Nur die Werte sind unterschiedlich.

---

## 5. `Locale` verwenden

Einfache Auswahl:

```java
Locale locale = Locale.GERMAN;
```

Andere Sprachen werden als Alternative zur deutschen Locale gesetzt.

```java
Locale locale = Locale.FRENCH;
```

oder:

```java
Locale locale = Locale.ITALIAN;
```

`Locale` beschreibt nicht nur eine Sprache, sondern kann auch eine Region enthalten. Für diese Übung reicht die einfache Sprachwahl.

---

## 6. `ResourceBundle` laden

```java
ResourceBundle texte = ResourceBundle.getBundle("messages", locale);
```

Bei `Locale.GERMAN` sucht Java zum Beispiel `messages_de.properties`. Die Dateien müssen im Maven-Projekt unter `src/main/resources` liegen.

---

## 7. Kleine `Main`

Datei `src/main/java/ch/allianz/youngoitv/lager/Main.java`:

```java
package ch.allianz.youngoitv.lager;

import java.util.Locale;
import java.util.ResourceBundle;

public class Main {

    public static void main(String[] args) {
        Locale locale = Locale.GERMAN;
        if (args.length > 0) {
            locale = localeAusArgument(args[0]);
        }

        ResourceBundle texte = ResourceBundle.getBundle("messages", locale);

        System.out.println(texte.getString("app.title"));
        System.out.println(texte.getString("app.welcome"));
        System.out.println(texte.getString("produkt.gespeichert"));
        System.out.println(texte.getString("fehler.produktSpeichern"));
    }

    private static Locale localeAusArgument(String sprache) {
        if (sprache.equals("fr")) {
            return Locale.FRENCH;
        }
        if (sprache.equals("it")) {
            return Locale.ITALIAN;
        }
        return Locale.GERMAN;
    }
}
```

Damit sind sichtbare Texte nicht mehr hartcodiert. Der Java-Code kennt nur noch Schlüssel wie `produkt.gespeichert`.

---

## 8. Standard-Locale

Eine Variante verwendet die Standard-Locale des Systems:

```java
Locale locale = Locale.getDefault();
ResourceBundle texte = ResourceBundle.getBundle("messages", locale);
```

Das Ergebnis kann je nach Rechner unterschiedlich sein. Deshalb ist es für Übungen oft klarer, die Sprache bewusst zu setzen oder als Argument zu übergeben.

Wenn die Standard-Locale zum Beispiel Englisch ist, aber keine `messages_en.properties` existiert, kann `ResourceBundle` nicht die erwartete Sprachdatei laden. Deshalb müssen unterstützte Sprachen bewusst vorbereitet werden.

---

## 9. Einfache Sprachumschaltung per Konfiguration vorbereiten

In `app.properties` könnte später stehen:

```properties
app.language=de
```

Das ist Startkonfiguration. Die sichtbaren Texte bleiben trotzdem in `messages_de.properties`, `messages_fr.properties` und `messages_it.properties`.

Kurze Trennung:

| Datei | Aufgabe |
|---|---|
| `app.properties` | technische Startwerte |
| `messages_*.properties` | sichtbare Texte |

---

## 10. Typische Fehlerhinweise

- Sichtbare Texte bleiben in `Main` hartcodiert.
- Sprachdateien liegen nicht unter `src/main/resources`.
- Datei heisst `message_de.properties` statt `messages_de.properties`.
- Nicht alle Sprachdateien enthalten dieselben Schlüssel.
- `db.url` oder `logging.level` landen in `messages_de.properties`.
- Die Sprache wird überall mit `if` im Code verzweigt.
- `ResourceBundle` wird in jeder Methode neu geladen.
- Fehlende Schlüssel werden ignoriert, bis die Anwendung zur Laufzeit fehlschlägt.

---

## 11. Kurze Reflexionsantworten

**Welche Texte waren bisher hartcodiert?**

Typisch sind Titel, Begrüssungen, Erfolgsmeldungen und einfache sichtbare Fehlermeldungen.

**Welche Vorteile bringt I18N?**

Die Anwendung kann mehrere Sprachen anzeigen, ohne dass die Fachlogik pro Sprache geändert wird.

**Warum sind `Locale` und Sprache nicht ganz dasselbe?**

Eine `Locale` kann neben der Sprache auch eine Region enthalten, zum Beispiel `de-CH` für Deutsch in der Schweiz.

**Welche Probleme entstehen ohne Mehrsprachigkeit?**

Texte verteilen sich im Code. Übersetzungen werden fehleranfällig und jede Sprachänderung verlangt Codeänderungen.

**Warum ist I18N besonders in der Schweiz relevant?**

Schweizer Anwendungen müssen häufig Deutsch, Französisch und Italienisch unterstützen, zum Beispiel für Kundschaft, Teams oder Standorte in verschiedenen Sprachregionen.

**Warum ist I18N nicht dasselbe wie technische Konfiguration?**

Technische Konfiguration steuert Infrastruktur wie DB-URL oder Logging-Level. I18N liefert sichtbare Texte für Benutzerinnen und Benutzer.

---

## 12. Verifikation

Die Java-Beispiele aus dieser Musterlösung wurden in einem temporären Maven-Projekt geprüft.

Ausgeführt:

```bash
mvn package
```

Zusätzlich wurde `Main` mit drei Sprachen ausgeführt:

```bash
java -cp target/classes ch.allianz.youngoitv.lager.Main
java -cp target/classes ch.allianz.youngoitv.lager.Main fr
java -cp target/classes ch.allianz.youngoitv.lager.Main it
```

Ergebnis:

```text
BUILD SUCCESS
Main lädt Texte aus messages_de.properties, messages_fr.properties und messages_it.properties.
```

Einschränkung: Es wurde keine vollständige Lagerverwaltung ausgeführt. Der Fokus dieser Musterlösung liegt auf `Locale`, `ResourceBundle` und sprachabhängiger Konsolenausgabe.
