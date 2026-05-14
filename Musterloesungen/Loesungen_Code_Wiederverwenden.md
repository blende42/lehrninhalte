# Lösungen – Code-Duplikate vermeiden und gemeinsamen Code wiederverwenden

Diese Musterlösung zeigt eine einfache Standardlösung. Ziel ist nicht eine neue Architektur, sondern ein kleiner Refactoring-Schritt: doppelte oder ähnliche Formatierungslogik wird in Hilfsmethoden ausgelagert.

Nicht verwendet werden:

- abstrakte Klassen
- tiefe Vererbungshierarchien
- `instanceof`
- Downcasting
- Factory
- Dependency Injection

---

## Basis

### Aufgabe 1 – Doppelte oder ähnliche Codeabschnitte erkennen

| Beobachtung | Gleich oder nur ähnlich? |
|---|---|
| Produkte durchlaufen | gleich |
| Namen lesen | gleich |
| Preis lesen | gleich |
| CSV-Zeile mit `;` erzeugen | nur in `CsvProduktSpeicher` |
| Konsolenzeile mit `:` erzeugen | nur in `KonsolenProduktSpeicher` |

Wichtig: Gleich ist nicht die ganze Methode. Gleich ist vor allem, dass beide Klassen Produkte durchlaufen und Name sowie Preis verwenden.

### Aufgabe 2 – Gemeinsamkeiten beschreiben

Beide Klassen lesen Name und Preis eines Produkts. Unterschiedlich ist, was daraus gemacht wird:

- `CsvProduktSpeicher` erzeugt eine CSV-Zeile für eine Datei.
- `KonsolenProduktSpeicher` erzeugt eine lesbare Ausgabe für die Konsole.

Man darf nicht alles in eine gemeinsame Methode verschieben, weil CSV-Datei und Konsolenausgabe unterschiedliche Verantwortlichkeiten haben.

### Aufgaben 3 und 4 – Formatierung in Hilfsmethoden auslagern

`CsvProduktSpeicher`:

```java
package ch.allianz.youngoitv.produktverwaltung;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;

import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.ArrayList;

public class CsvProduktSpeicher implements ProduktSpeicher {

    @Override
    public void speichern(ArrayList<Produkt> produkte, String dateipfad) {
        ArrayList<String> zeilen = new ArrayList<>();

        for (Produkt produkt : produkte) {
            zeilen.add(produktAlsCsvZeile(produkt));
        }

        try {
            Files.write(Path.of(dateipfad), zeilen);
        } catch (IOException e) {
            System.out.println("Datei konnte nicht gespeichert werden: " + dateipfad);
        }
    }

    private String produktAlsCsvZeile(Produkt produkt) {
        return produkt.getName() + ";" + produkt.getPreis();
    }
}
```

`KonsolenProduktSpeicher`:

```java
package ch.allianz.youngoitv.produktverwaltung;

import ch.allianz.youngoitv.produktverwaltung.model.Produkt;

import java.util.ArrayList;

public class KonsolenProduktSpeicher implements ProduktSpeicher {

    @Override
    public void speichern(ArrayList<Produkt> produkte, String dateipfad) {
        for (Produkt produkt : produkte) {
            System.out.println(produktAlsKonsolenZeile(produkt));
        }
    }

    private String produktAlsKonsolenZeile(Produkt produkt) {
        return produkt.getName() + ": " + produkt.getPreis();
    }
}
```

Hinweis: `dateipfad` wird im `KonsolenProduktSpeicher` nicht verwendet. Der Parameter bleibt vorhanden, weil die Signatur zum Interface passen muss.

Die Schleifen bleiben einfach. Die Formatierung ist klar benannt und an einer Stelle änderbar.

### Aufgabe 5 – Verhalten prüfen

Erwartetes Resultat:

- Das Projekt kompiliert weiterhin.
- Die CSV-Datei enthält weiterhin Zeilen wie `Maus;34.9`.
- Die Konsolenausgabe enthält weiterhin Zeilen wie `Maus: 34.9`.
- Das Verhalten bleibt gleich, aber der Code ist klarer strukturiert.

---

## Vertiefung

### Aufgabe 6 – Konsolenformat an einer Stelle ändern

Nur die Hilfsmethode wird geändert:

```java
private String produktAlsKonsolenZeile(Produkt produkt) {
    return "Produkt: " + produkt.getName() + " (" + produkt.getPreis() + ")";
}
```

Die Schleife bleibt unverändert:

```java
for (Produkt produkt : produkte) {
    System.out.println(produktAlsKonsolenZeile(produkt));
}
```

Das ist wartbarer, weil die Formatierung nicht an mehreren Stellen gesucht und angepasst werden muss.

### Aufgabe 7 – Schleifen vergleichen

| Klasse | Was bleibt in der Schleife? | Was ist ausgelagert? |
|---|---|---|
| `CsvProduktSpeicher` | Produkte durchlaufen und Zeilen sammeln | CSV-Formatierung |
| `KonsolenProduktSpeicher` | Produkte durchlaufen und ausgeben | Konsolenformatierung |

Die Schleifen sind verständlicher, weil sie nur noch den Ablauf zeigen. Die Unterschiede bleiben bewusst erhalten: Datei schreiben ist nicht dasselbe wie Konsole ausgeben.

### Aufgabe 8 – CSV-Format an einer Stelle ändern

Testweise kann nur die Hilfsmethode angepasst werden:

```java
private String produktAlsCsvZeile(Produkt produkt) {
    return produkt.getName() + ";" + produkt.getPreis() + " CHF";
}
```

Die Schleife in `speichern(...)` bleibt gleich. Dadurch ist klar, wo das Ausgabeformat geändert wird.

### Aufgabe 9 – Basisklasse nur als Idee

Eine gemeinsame Basisklasse könnte später helfen, wenn mehrere Speicherklassen wirklich dieselbe Hilfslogik brauchen.

Beispiel als Idee, noch nicht umsetzen:

```java
protected String produktNameUndPreis(Produkt produkt) {
    return produkt.getName() + " " + produkt.getPreis();
}
```

Warum jetzt noch nicht?

- Es gibt erst wenig gemeinsamen Code.
- CSV und Konsole haben unterschiedliche Aufgaben.
- Zu frühe Vererbung macht die Struktur schwerer verständlich.

---

## Transfer

### Aufgabe 10 – Weitere mögliche Duplikate suchen

Mögliche Beobachtungen:

| Stelle | Bewertung |
|---|---|
| Produktanzahl für Meldungen | könnte später wiederverwendet werden |
| Preisformatierung | nur wiederverwenden, wenn wirklich gleiches Format gewünscht ist |
| Schleifen über Produkte | ähnlich, aber nicht automatisch ein echtes Duplikat |

Eine Hilfsmethode lohnt sich nur, wenn sie die Lesbarkeit verbessert oder spätere Änderungen an einer Stelle bündelt.

### Aufgabe 11 – Logging-Ausgabe wiederverwenden

Mögliche Methode:

```java
private String erstelleSpeicherMeldung(ArrayList<Produkt> produkte) {
    return "Speichere " + produkte.size() + " Produkte";
}
```

Diese Methode gehört nicht direkt ins Interface `ProduktSpeicher`, weil das Interface nur den Vertrag zum Speichern beschreibt. Eine Logging-Meldung ist eine konkrete Hilfsaufgabe.

### Aufgabe 12 – Statistik-Hilfsmethode überlegen

Mögliche Methode:

```java
private int anzahlProdukte(ArrayList<Produkt> produkte) {
    return produkte.size();
}
```

Für einfache Meldungen reicht das lokal. Wenn später mehrere Statistiken gebraucht werden, kann eine eigene Verantwortung sinnvoll sein. Das ist aber noch kein Grund, jetzt eine zusätzliche Architektur einzubauen.

### Aufgabe 13 – Wann ist Wiederverwendung sinnvoll?

| Wiederverwendung ist sinnvoll, wenn ... | Wiederverwendung ist problematisch, wenn ... |
|---|---|
| dieselbe Änderung sonst mehrfach nötig wäre | nur ähnlich aussehender Code unterschiedliche Aufgaben hat |
| ein klarer Name die Lesbarkeit verbessert | die Hilfsmethode zu allgemein wird |
| das Verhalten gleich bleiben soll | dadurch versteckte Abhängigkeiten entstehen |

### Aufgabe 14 – Gemeinsame Basisklasse abwägen

| Vorteil | Nachteil oder Risiko |
|---|---|
| gemeinsamer Code muss nicht kopiert werden | zu frühe Vererbung macht den Code schwerer verständlich |
| gleiche Hilfsmethoden sind an einem Ort | Klassen können unnötig eng gekoppelt werden |

Für diese Einheit reicht eine einfache Hilfsmethode. Vererbung wird nur vorbereitet, nicht vertieft.

---

## Typische Fehlerhinweise

| Fehler | Korrektur |
|---|---|
| Hilfsmethode ins Interface schreiben | Interface bleibt Vertrag, Hilfslogik bleibt in der konkreten Klasse |
| CSV-Format und Konsolenformat vermischen | Jede Klasse behält ihre eigene Verantwortung |
| Verhalten beim Refactoring verändern | Nach jedem kleinen Schritt mit Maven prüfen |
| Duplikat nur kopieren und umbenennen | Gemeinsame Idee wirklich an einer Stelle bündeln |
| sofort eine Basisklasse bauen | zuerst prüfen, ob genug echter gemeinsamer Code vorhanden ist |
| alles in eine Hilfsklasse verschieben | Verantwortung der Klassen beachten |

---

## Kurze Reflexion

Code-Duplikate sind problematisch, weil spätere Änderungen mehrfach gemacht werden müssen. Wiederverwendung lohnt sich, wenn dieselbe Logik wirklich mehrfach gebraucht wird und ein klarer Methodenname den Code verständlicher macht.

Nicht jeder ähnliche Code ist automatisch ein Duplikat. `CsvProduktSpeicher` und `KonsolenProduktSpeicher` dürfen unterschiedlich bleiben, weil sie unterschiedliche Ausgaben erzeugen.

Eine gemeinsame Basisklasse kann später helfen, wenn mehrere Klassen wirklich denselben Code brauchen. In dieser Einheit reicht die Vorbereitung: Vererbung ist kein Selbstzweck.

---

## Verifikation

Die Java-Beispiele wurden mit einem temporären Maven-Projekt geprüft:

```bash
mvn package
java -cp target/classes ch.allianz.youngoitv.produktverwaltung.Main
```

Ergebnis:

- `mvn package` war erfolgreich.
- Es waren keine Testklassen vorhanden.
- `Main` gab die Produkte auf der Konsole aus.
- Die CSV-Datei enthielt die erwarteten Produktzeilen.
