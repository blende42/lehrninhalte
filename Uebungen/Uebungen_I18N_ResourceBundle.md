# Übungen – Mehrsprachigkeit mit Locale und ResourceBundle

## Vorwissen

Du brauchst:

- bekannte Lagerverwaltung
- Maven-Projektstruktur
- `Main`
- Grundidee von technischer Konfiguration mit `.properties`
- einfache Konsolenausgabe
- Grundidee von Verantwortlichkeiten

Nicht verwendet werden:

- Spring
- Web-I18N
- Angular-I18N
- ICU
- automatische Übersetzungsdienste
- datenbankbasierte Übersetzungen
- komplexe Übersetzungsframeworks

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
Du lagerst sichtbare Texte aus dem Java-Code aus
und lädst sie abhängig von einer Locale.
```

---

## Vorbereitung

Arbeite mit der bekannten Lagerverwaltung.

Beispielstruktur:

```text
lagerverwaltung-db/
  pom.xml
  src/main/java/
    ch/allianz/youngoitv/lager/
      Main.java
      LagerService.java
      repository/ProduktRepository.java
      model/Produkt.java
  src/main/resources/
    messages_de.properties
    messages_fr.properties
    messages_it.properties
```

Falls dein Projekt leicht anders aufgebaut ist, passe die Package-Namen sinnvoll an.

---

## Basis

### Aufgabe 1 – Hartcodierte Texte finden

Suche in deinem Projekt sichtbare Texte, die direkt im Java-Code stehen.

Typische Beispiele:

```text
Produkt wurde gespeichert.
Produkt wurde nicht gefunden.
Willkommen in der Lagerverwaltung.
Fehler beim Laden.
```

Auftrag:

1. Notiere mindestens vier hartcodierte Texte.
2. Markiere, in welcher Klasse sie stehen.
3. Entscheide, ob der Text für Benutzerinnen und Benutzer sichtbar ist.

Erwartung:

```text
Sichtbare Texte sollen später aus ResourceBundle geladen werden.
Technische Werte wie db.url bleiben technische Konfiguration.
```

---

### Aufgabe 2 – `messages_de.properties` erstellen

Erstelle die Datei `src/main/resources/messages_de.properties`.

Inhalt:

```properties
app.title=Lagerverwaltung
app.welcome=Willkommen in der Lagerverwaltung.
produkt.gespeichert=Produkt wurde gespeichert.
produkt.nichtGefunden=Produkt wurde nicht gefunden.
fehler.allgemein=Ein Fehler ist aufgetreten.
```

Auftrag:

1. Lege die Datei unter `src/main/resources` ab.
2. Verwende genau diese Schlüssel.
3. Lege keine technische Konfiguration in diese Datei.

---

### Aufgabe 3 – `messages_fr.properties` erstellen

Erstelle die Datei `src/main/resources/messages_fr.properties`.

Inhalt:

```properties
app.title=Gestion du stock
app.welcome=Bienvenue dans la gestion du stock.
produkt.gespeichert=Produit enregistré.
produkt.nichtGefunden=Produit introuvable.
fehler.allgemein=Une erreur est survenue.
```

Auftrag:

1. Verwende dieselben Schlüssel wie in der deutschen Datei.
2. Ändere nur die Werte.
3. Prüfe die Dateiendung `.properties`.

---

### Aufgabe 4 – `messages_it.properties` erstellen

Erstelle die Datei `src/main/resources/messages_it.properties`.

Inhalt:

```properties
app.title=Gestione magazzino
app.welcome=Benvenuto nella gestione magazzino.
produkt.gespeichert=Prodotto salvato.
produkt.nichtGefunden=Prodotto non trovato.
fehler.allgemein=Si è verificato un errore.
```

Auftrag:

1. Verwende dieselben Schlüssel wie in den anderen Sprachdateien.
2. Prüfe, dass alle drei Dateien gleich viele Schlüssel enthalten.
3. Prüfe mit `mvn package`, ob das Projekt weiterhin baut.

---

### Aufgabe 5 – Begrüssungstext aus ResourceBundle laden

Lade in `Main` die deutschen Texte.

```java
import java.util.Locale;
import java.util.ResourceBundle;

Locale locale = Locale.GERMAN;
ResourceBundle texte = ResourceBundle.getBundle("messages", locale);

System.out.println(texte.getString("app.welcome"));
```

Auftrag:

1. Ergänze die nötigen Imports.
2. Starte die Anwendung.
3. Prüfe, ob der deutsche Begrüssungstext erscheint.

---

### Aufgabe 6 – Locale wechseln

Ändere die Locale in `Main`.

```java
Locale locale = Locale.FRENCH;
```

Danach:

```java
Locale locale = Locale.ITALIAN;
```

Auftrag:

1. Starte die Anwendung mit Deutsch.
2. Starte die Anwendung mit Französisch.
3. Starte die Anwendung mit Italienisch.
4. Notiere die drei Ausgaben von `app.welcome`.

---

### Aufgabe 7 – Sprachabhängige Ausgabe erzeugen

Gib mehrere Texte aus dem ResourceBundle aus.

```java
System.out.println(texte.getString("app.title"));
System.out.println(texte.getString("app.welcome"));
System.out.println(texte.getString("produkt.gespeichert"));
```

Auftrag:

1. Verwende keine hartcodierten Ausgabetexte für diese drei Meldungen.
2. Prüfe die Ausgabe mit mindestens zwei Locales.
3. Prüfe mit `mvn package`.

---

### Aufgabe 8 – Harte Texte aus `Main` entfernen

Suche in `Main` hartcodierte Konsolentexte.

Auftrag:

1. Ersetze mindestens drei sichtbare Texte durch `texte.getString(...)`.
2. Verwende sprechende Schlüssel wie `produkt.gespeichert`.
3. Lasse technische Werte wie DB-URL und Dateipfade unverändert in der technischen Konfiguration.

Erwartung:

```text
Main enthält weniger sichtbare Texte.
Die Sprachdateien enthalten die sichtbaren Texte.
```

---

### Aufgabe 9 – Einfache Fehlermeldungen übersetzen

Ergänze eine einfache Fehlermeldung in allen drei Dateien.

Beispiel:

```properties
fehler.produktSpeichern=Produkt konnte nicht gespeichert werden.
```

Auftrag:

1. Ergänze den Schlüssel in allen drei Sprachdateien.
2. Verwende den Schlüssel im Java-Code.
3. Prüfe mit einer zweiten Locale, ob die Meldung wechselt.

Wichtig:

```text
Technische Details aus Exceptions werden hier nicht übersetzt.
Für diese Übung reicht eine einfache sichtbare Fehlermeldung.
```

---

## Vertiefung

### Aufgabe 10 – Fehlende Übersetzungen behandeln

Entferne testweise einen Schlüssel aus `messages_fr.properties`.

Auftrag:

1. Starte die Anwendung mit `Locale.FRENCH`.
2. Beobachte den Fehler.
3. Stelle den Schlüssel wieder her.

Erwartung:

```text
Fehlende Schlüssel fallen zur Laufzeit auf.
Alle Sprachdateien brauchen dieselben Schlüssel.
```

---

### Aufgabe 11 – Standard-Locale verwenden

Nutze die Standard-Locale des Systems.

```java
Locale locale = Locale.getDefault();
ResourceBundle texte = ResourceBundle.getBundle("messages", locale);
```

Auftrag:

1. Gib `Locale.getDefault()` aus.
2. Prüfe, welche Sprachdatei geladen wird.
3. Erkläre, warum das Ergebnis je nach Rechner unterschiedlich sein kann.
4. Erkläre, was passiert, wenn die Standard-Locale zum Beispiel Englisch ist, aber keine `messages_en.properties` existiert.

---

### Aufgabe 12 – Zusätzliche Sprache ergänzen

Ergänze eine weitere Sprache, zum Beispiel Englisch.

Datei:

```text
src/main/resources/messages_en.properties
```

Auftrag:

1. Kopiere die Schlüssel aus `messages_de.properties`.
2. Übersetze die Werte einfach.
3. Starte die Anwendung mit `Locale.ENGLISH`.

---

### Aufgabe 13 – Konsolenausgabe vollständig mehrsprachig machen

Prüfe deine Konsolenausgaben.

Auftrag:

1. Alle sichtbaren Texte für Benutzerinnen und Benutzer kommen aus `ResourceBundle`.
2. Technische Logmeldungen bleiben technisches Logging.
3. Fachlogik bleibt im `LagerService`.
4. Prüfe mit `mvn package`.

Kurze Kontrolle:

```text
ResourceBundle liefert sichtbare Texte.
AppConfig liefert technische Einstellungen.
LagerService enthält Fachlogik.
Repository enthält Datenzugriff.
```

---

### Aufgabe 14 – Sprachumschaltung per Konfiguration einordnen

Ordne ein, dass die Startsprache später aus `app.properties` gelesen werden könnte.

Beispiel:

```properties
app.language=de
```

Auftrag:

1. Erkläre, warum `app.language` technische Startkonfiguration ist.
2. Erkläre, warum die sichtbaren Texte trotzdem in `messages_*.properties` bleiben.
3. Skizziere höchstens kurz, wie daraus eine `Locale` gewählt werden könnte.
4. Implementiere keine Sprachverwaltung.

---

### Aufgabe 15 – Datums- oder Zahlenformatierung diskutieren

Diskutiere kurz, was sich je nach `Locale` zusätzlich ändern könnte.

Beispiele:

```text
Datum
Zahlen
Währung
```

Auftrag:

1. Notiere zwei Beispiele.
2. Erkläre, warum das später wichtig werden kann.
3. Implementiere keine komplexe Formatierung.

---

## Transfer

### Aufgabe 16 – Warum sind harte Texte problematisch?

Erkläre an zwei Beispielen aus deiner Lagerverwaltung:

```text
Produkt wurde gespeichert.
Produkt wurde nicht gefunden.
```

Warum wird es schwierig, wenn diese Texte direkt im Code stehen?

---

### Aufgabe 17 – Warum ist I18N nicht dasselbe wie Konfiguration?

Ordne die folgenden Werte zu:

| Wert | Technische Konfiguration oder I18N? |
|---|---|
| `db.url=jdbc:h2:./data/lager` |  |
| `logging.level=INFO` |  |
| `app.title=Lagerverwaltung` |  |
| `produkt.gespeichert=Produkt wurde gespeichert.` |  |
| `h2.mode=embedded` |  |

Begründe mindestens drei Entscheidungen.

---

### Aufgabe 18 – Welche Texte sollten übersetzt werden?

Entscheide für jeden Wert:

| Wert | Übersetzen? |
|---|---|
| Menütitel |  |
| sichtbare Fehlermeldung |  |
| DB-URL |  |
| technischer Logeintrag |  |
| Produktname aus der Datenbank |  |
| Begrüssungstext |  |

Begründe mindestens drei Entscheidungen.

---

### Aufgabe 19 – Mehrsprachigkeit in der Schweiz

Diskutiere kurz:

```text
Warum ist Mehrsprachigkeit in Schweizer Anwendungen besonders relevant?
```

Nutze mindestens zwei Beispiele aus Alltag oder Beruf.

---

### Aufgabe 20 – Warum wird I18N später für grössere Anwendungen wichtig?

Erkläre als Ausblick, warum die Idee später auch für grössere Anwendungen wichtig wird.

Wichtig:

```text
Hier wird keine Web-Umsetzung gebaut.
Es geht nur um die Grundidee: sichtbare Texte bleiben austauschbar.
```

Begriffe:

```text
Benutzeroberfläche
Fehlermeldung
gleiche Fachlogik
andere Sprache
```

Erwartung:

```text
Die Anwendung kann gleiche fachliche Abläufe in verschiedenen Sprachen anzeigen,
ohne die Fachlogik pro Sprache neu zu schreiben.
```

---

## Typische Fehler prüfen

Prüfe dein Ergebnis anhand dieser Liste:

- Sind sichtbare Texte noch hartcodiert?
- Liegen die Sprachdateien unter `src/main/resources`?
- Heissen die Dateien korrekt `messages_de.properties`, `messages_fr.properties` und `messages_it.properties`?
- Haben alle Sprachdateien dieselben Schlüssel?
- Werden technische Werte nicht in Sprachdateien gemischt?
- Wird die Sprache nicht überall mit `if` im Code verzweigt?
- Wird `ResourceBundle` nicht in jeder Methode neu geladen?

---

## Reflexion

Beantworte zum Abschluss:

1. Welche Texte waren bisher hartcodiert?
2. Welche Vorteile bringt I18N?
3. Warum sind `Locale` und Sprache nicht ganz dasselbe?
4. Welche Probleme entstehen ohne Mehrsprachigkeit?
5. Warum ist I18N besonders in der Schweiz relevant?
