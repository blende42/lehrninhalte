# Tag 4 – String-Klasse (Version 3: Mini-Projekt Parser – erweitert)

## Lernziele

- Ich kann Strings systematisch analysieren und verarbeiten
- Ich kann einen einfachen Parser selbstständig entwerfen
- Ich kann Zeichen gezielt entfernen und zählen
- Ich kann Ergebnisse strukturiert ausgeben

---

## Mini-Projekt – Wort-Parser (erweitert)

### Aufgabe

Schreibe ein Java-Programm, das einen Text analysiert und auswertet.

---

## Anforderungen

### 1. Eingabe

```java
String text = "Hallo, Welt! DAS ist ein \"Test\". Java, Parser und XML sind COOL.";
```

---

### 2. Delimiter definieren

```java
String delimiters = " .,;:!?()[]{}'\"";
```

👉 Diese Zeichen gelten **nicht als Teil eines Wortes**

---

### 3. Verarbeitung

Das Programm soll:

- den Text in Teile zerlegen
- Delimiter am Anfang und Ende entfernen
- zählen, wie viele Delimiter entfernt wurden
- leere Resultate ignorieren
- nur gültige Wörter weiterverarbeiten

---

### 4. Klassifikation der Wörter

Ein Wort wird wie folgt bewertet:

- vollständig klein (z. B. `ist`)
- beginnt mit Grossbuchstabe (z. B. `Hallo`)
- nur Grossbuchstaben (z. B. `XML`, `COOL`)

👉 Hinweis: Kategorien können sich überschneiden

---

## Ausgabe

### Bereinigte Wörter

```text
Hallo
Welt
DAS
...
```

---

### Statistik

```text
Total Wörter: X
Kleingeschrieben: X
Beginnt mit Grossbuchstabe: X
Nur Grossbuchstaben: X
Entfernte Delimiter: X
```

---

## Hinweise zur Umsetzung

- Verwende den String `delimiters`, um Zeichen zu erkennen
- Prüfe Zeichen einzeln (z. B. mit Schleifen)
- Entferne Zeichen am Anfang und Ende eines Wortes
- Zähle jedes entfernte Zeichen

---

## Leitfragen

- Wie erkenne ich, ob ein Zeichen ein Delimiter ist?
- Wie kann ich ein Wort „von aussen nach innen“ bereinigen?
- Wie kann ich zählen, wie viele Zeichen entfernt wurden?
- Was passiert, wenn ein Wort nur aus Delimitern besteht?

---

## Zusatzaufgaben

- Zähle zusätzlich, wie viele Delimiter insgesamt im Text vorkommen
- Teste mit eigenen Beispielen (inkl. vielen Sonderzeichen)
- Überlege: Wie könnte man auch Zahlen sinnvoll behandeln?

---

## Reflexion

- Was war schwierig an der Umsetzung?
- Wie bin ich beim Entfernen der Zeichen vorgegangen?
- Welche String-Methoden waren hilfreich?
