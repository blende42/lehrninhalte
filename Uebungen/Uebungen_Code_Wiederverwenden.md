# Übungen – Code-Duplikate vermeiden und gemeinsamen Code wiederverwenden

## Vorwissen

Du brauchst:

- Klassen und Objekte
- Methoden mit Parametern und Rückgabewerten
- `ArrayList`
- einfache Schleifen
- Maven-Projektstruktur
- `ProduktSpeicher` als Interface
- `CsvProduktSpeicher`
- `KonsolenProduktSpeicher`

Nicht verwendet werden:

- tiefe Vererbungshierarchien
- abstrakte Klassen
- `instanceof`
- Downcasting
- Factory
- Dependency Injection
- Spring
- Datenbank

---

## Vorbereitung

Arbeite mit der bekannten Produktverwaltung.

Beispielstruktur:

```text
produktverwaltung-maven/
  pom.xml
  data/
    produkte.csv
  src/main/java/
    ch/allianz/youngoitv/produktverwaltung/
      Main.java
      CsvProduktSpeicher.java
      KonsolenProduktSpeicher.java
      ProduktSpeicher.java
      model/Produkt.java
```

Ziel dieser Übung:

```text
Zuerst Duplikate erkennen.
Dann kleine Hilfsmethoden einsetzen.
Danach prüfen, ob das Verhalten gleich geblieben ist.
```

Ausgangspunkt ist dieselbe Interface-Signatur wie in den vorherigen Einheiten:

```java
void speichern(ArrayList<Produkt> produkte, String dateipfad);
```

Prüfe nach praktischen Änderungen:

```bash
mvn test
```

Wenn keine Tests vorhanden sind:

```bash
mvn package
```

---

## Basis

### Aufgabe 1 – Doppelte oder ähnliche Codeabschnitte markieren

Öffne:

- `CsvProduktSpeicher`
- `KonsolenProduktSpeicher`

Auftrag:

1. Markiere die Schleifen über `produkte`.
2. Markiere alle Stellen mit `produkt.getName()`.
3. Markiere alle Stellen mit `produkt.getPreis()`.
4. Notiere, was wirklich gleich ist.
5. Notiere, was nur ähnlich ist.

Hilfstabelle:

| Beobachtung | Gleich oder nur ähnlich? |
|---|---|
| Produkte durchlaufen | |
| Namen lesen | |
| Preis lesen | |
| CSV-Zeile mit `;` erzeugen | |
| Konsolenzeile mit `:` erzeugen | |

---

### Aufgabe 2 – Gemeinsamkeiten beschreiben

Beantworte schriftlich:

1. Welche Schritte kommen in beiden Klassen vor?
2. Welche Schritte sind unterschiedlich?
3. Warum darf man nicht einfach alles in eine gemeinsame Methode verschieben?

Verwende diesen Satzanfang:

```text
Beide Klassen lesen Name und Preis eines Produkts. Unterschiedlich ist ...
```

---

### Aufgabe 3 – Produktformatierung im KonsolenProduktSpeicher auslagern

Ausgangscode:

```java
for (Produkt produkt : produkte) {
    System.out.println(produkt.getName() + ": " + produkt.getPreis());
}
```

Auftrag:

1. Erstelle im `KonsolenProduktSpeicher` eine private Hilfsmethode.
2. Gib der Methode einen klaren Namen.
3. Verwende die Methode in der Schleife.

Zielcode:

```java
for (Produkt produkt : produkte) {
    System.out.println(produktAlsKonsolenZeile(produkt));
}
```

```java
private String produktAlsKonsolenZeile(Produkt produkt) {
    return produkt.getName() + ": " + produkt.getPreis();
}
```

---

### Aufgabe 4 – Produktformatierung im CsvProduktSpeicher auslagern

Ausgangscode:

```java
for (Produkt produkt : produkte) {
    zeilen.add(produkt.getName() + ";" + produkt.getPreis());
}
```

Auftrag:

1. Erstelle im `CsvProduktSpeicher` eine private Hilfsmethode.
2. Gib der Methode einen Namen, der zum CSV-Ziel passt.
3. Verwende die Methode in der Schleife.

Zielcode:

```java
for (Produkt produkt : produkte) {
    zeilen.add(produktAlsCsvZeile(produkt));
}
```

```java
private String produktAlsCsvZeile(Produkt produkt) {
    return produkt.getName() + ";" + produkt.getPreis();
}
```

---

### Aufgabe 5 – Verhalten erneut prüfen

Prüfe nach dem Umbau:

```bash
mvn package
```

Wenn Tests vorhanden sind:

```bash
mvn test
```

Auftrag:

1. Prüfe, ob das Projekt kompiliert.
2. Führe `Main` aus, wenn das in deinem Projekt vorgesehen ist.
3. Vergleiche die Ausgabe oder CSV-Datei mit dem vorherigen Verhalten.
4. Notiere, ob sich das gewünschte Verhalten geändert hat.

Erwartung:

```text
Die Struktur ist etwas klarer.
Das Verhalten bleibt gleich.
```

---

## Vertiefung

### Aufgabe 6 – Hilfsmethode an einer Stelle ändern

Ändere die Konsolenausgabe leicht:

```text
Produkt: Maus (34.9)
```

Auftrag:

1. Ändere nur die Hilfsmethode `produktAlsKonsolenZeile(...)`.
2. Lasse die Schleife unverändert.
3. Prüfe das Programm erneut.
4. Erkläre, warum die Änderung nun einfacher ist.

---

### Aufgabe 7 – Ähnliche Schleifen vergleichen

Vergleiche die Schleifen in beiden Speicherklassen nach dem Umbau.

| Klasse | Was bleibt in der Schleife? | Was ist ausgelagert? |
|---|---|---|
| `CsvProduktSpeicher` | | |
| `KonsolenProduktSpeicher` | | |

Beantworte:

```text
Sind die Schleifen jetzt verständlicher?
Welche Unterschiede bleiben bewusst bestehen?
```

---

### Aufgabe 8 – Änderung an einer Stelle durchführen

Passe die CSV-Formatierung testweise so an, dass hinter dem Preis ` CHF` steht:

```text
Maus;34.9 CHF
```

Auftrag:

1. Prüfe, ob die Änderung nur in `produktAlsCsvZeile(...)` nötig ist.
2. Lasse die Schleife gleich.
3. Prüfe das Projekt mit Maven.
4. Beschreibe, warum diese Änderung wartbarer ist als kopierter Code.

---

### Aufgabe 9 – Kleine Basisklasse als Idee vorbereiten

Noch nichts umbauen.

Stelle dir vor, beide Speicherklassen brauchen später dieselbe Methode:

```java
protected String produktNameUndPreis(Produkt produkt) {
    return produkt.getName() + " " + produkt.getPreis();
}
```

Auftrag:

1. Beschreibe, warum eine gemeinsame Basisklasse später helfen könnte.
2. Beschreibe, warum wir sie jetzt noch nicht sofort einführen.
3. Notiere ein Risiko, wenn man Vererbung zu früh verwendet.

Wichtig: In dieser Aufgabe wird noch kein `extends` programmiert.

---

## Transfer

### Aufgabe 10 – Weitere mögliche Duplikate suchen

Suche im Projekt nach weiteren ähnlichen Stellen.

Auftrag:

1. Notiere zwei Stellen, die ähnlich aussehen.
2. Entscheide, ob es echte Duplikate sind.
3. Begründe deine Entscheidung.

Hilfsfragen:

- Ist dieselbe Änderung später mehrfach nötig?
- Haben die Stellen dieselbe Verantwortung?
- Würde eine Hilfsmethode den Code klarer machen?

---

### Aufgabe 11 – Logging-Ausgabe wiederverwenden

Stelle dir vor, mehrere Klassen sollen eine einfache Meldung ausgeben:

```text
Speichere 2 Produkte
```

Auftrag:

1. Skizziere eine Methode `erstelleSpeicherMeldung(...)`.
2. Entscheide, welche Parameter sie braucht.
3. Erkläre, warum diese Methode nicht direkt ins Interface `ProduktSpeicher` gehört.

---

### Aufgabe 12 – Gemeinsame Statistik-Hilfsmethode überlegen

Stelle dir vor, mehrere Klassen brauchen die Anzahl Produkte.

Auftrag:

1. Skizziere eine Methode, die die Anzahl Produkte liefert.
2. Entscheide, ob diese Methode in eine Speicherklasse gehört.
3. Begründe, ob dafür später eher eine eigene Verantwortung sinnvoll wäre.

---

### Aufgabe 13 – Wann ist Wiederverwendung sinnvoll?

Erstelle eine kurze Pro-/Contra-Liste.

| Wiederverwendung ist sinnvoll, wenn ... | Wiederverwendung ist problematisch, wenn ... |
|---|---|
| | |
| | |
| | |

---

### Aufgabe 14 – Vor- und Nachteile einer gemeinsamen Basisklasse

Sammle je zwei Punkte.

| Vorteil | Nachteil oder Risiko |
|---|---|
| | |
| | |

Nutze diese Begriffe:

- gemeinsamer Code
- klare Verantwortung
- zu frühe Vererbung
- schwer verständliche Struktur

---

## Typische Fehler prüfen

Prüfe deinen Code bewusst auf diese Fehler:

| Prüfung | Erfüllt? |
|---|---|
| Verhalten bleibt nach dem Umbau gleich | |
| Hilfsmethoden haben klare Namen | |
| CSV-Format und Konsolenformat werden nicht vermischt | |
| Das Interface `ProduktSpeicher` wurde nicht mit Hilfslogik gefüllt | |
| Es wurde keine unnötige Basisklasse eingeführt | |
| Es wird kein `instanceof` verwendet | |
| Es wird kein Downcasting verwendet | |
| Code wurde nicht nur kopiert und umbenannt | |

---

## Reflexion

Beantworte zum Schluss:

1. Warum sind Code-Duplikate problematisch?
2. Wann lohnt sich Wiederverwendung?
3. Warum sollte nicht alles in dieselbe Klasse verschoben werden?
4. Was könnte eine gemeinsame Basisklasse später vereinfachen?
5. Warum führen wir Vererbung noch nicht sofort vollständig ein?
