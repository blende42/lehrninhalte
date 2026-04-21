# Tag 4 – String-Klasse (Version 3: Mini-Projekt Parser)

## Lernziele

- Ich kann mehrere String-Methoden kombiniert anwenden
- Ich kann einen einfachen Parser schrittweise umsetzen
- Ich kann Wörter in einem Text erkennen und bereinigen
- Ich kann Wörter nach einfachen Regeln klassifizieren
- Ich kann selbst entscheiden, welche String-Methoden für ein Problem nützlich sind

---

## Ausgangslage

In den vorherigen Versionen hast du gelernt:

- Strings korrekt mit `.equals()` zu vergleichen
- Eingaben mit `trim()` und `toLowerCase()` zu normalisieren
- Teilstrings zu untersuchen
- Methoden wie `contains()`, `substring()` und `length()` anzuwenden
- dass Strings unveränderlich sind

In diesem Mini-Projekt verbindest du diese Kenntnisse in einer grösseren Aufgabe.

---

## Mini-Projekt – Einfacher Wort-Parser

### Aufgabe

Schreibe ein Java-Programm, das einen Text einliest und anschliessend auswertet.

Das Programm soll:

1. den Text in einzelne Wörter zerlegen
2. störende Zeichen am Anfang und Ende eines Wortes entfernen
3. nur die bereinigten Wörter ausgeben
4. am Schluss eine kleine Statistik ausgeben

---

## Ziel der Auswertung

Das Programm soll folgende Werte bestimmen:

- **Total aller Wörter**
- **Anzahl der vollständig kleingeschriebenen Wörter**
- **Anzahl der Wörter, die mit einem Grossbuchstaben beginnen**
- **Anzahl der Wörter, die nur aus Grossbuchstaben bestehen**

---

## Wichtige Vorgabe

Die Wort-Trennzeichen sollen **als ein String** abgelegt werden.

Beispiel:

```java
String delimiters = " .,;:!?()[]{}'\"";
```

👉 In diesem String sind Zeichen enthalten, die beim Zerlegen oder Bereinigen eines Wortes berücksichtigt werden sollen.

---

## Beispiel-Eingabe

```text
Hallo, Welt! DAS ist ein "Test". Java, Parser und XML sind COOL.
```

---

## Beispiel für bereinigte Ausgabe

```text
Hallo
Welt
DAS
ist
ein
Test
Java
Parser
und
XML
sind
COOL
```

---

## Beispiel für die Statistik

```text
Total Wörter: 12
Kleingeschrieben: 4
Beginnt mit Grossbuchstabe: 4
Nur Grossbuchstaben: 3
```

---

## Anforderungen

### 1. Text einlesen
Der Text kann zuerst direkt als String im Code stehen.

Beispiel:

```java
String text = "Hallo, Welt! DAS ist ein \"Test\". Java, Parser und XML sind COOL.";
```

---

### 2. Wortgrenzen beachten
Das Programm soll erkennen, wo ein Wort beginnt und endet.

Dabei gelten Satzzeichen und ähnliche Zeichen **nicht** als Teil des Wortes.

Beispiele für Zeichen, die entfernt werden sollen:

- Punkt `.`
- Komma `,`
- Doppelpunkt `:`
- Semikolon `;`
- Ausrufezeichen `!`
- Fragezeichen `?`
- Klammern `(` `)` `[` `]`
- Hochkomma `'`
- Anführungszeichen `"`

---

### 3. Bereinigte Wörter ausgeben
Vor der Ausgabe sollen störende Zeichen entfernt werden.

Beispiel:

```text
"Test"
```

soll ausgegeben werden als:

```text
Test
```

---

### 4. Wörter klassifizieren

Ein bereinigtes Wort soll einer oder mehreren der folgenden Gruppen zugeordnet werden:

#### a) kleingeschrieben
Beispiel:

```text
hallo
parser
ist
```

#### b) beginnt mit Grossbuchstaben
Beispiel:

```text
Hallo
Java
Parser
```

#### c) nur Grossbuchstaben
Beispiel:

```text
DAS
XML
COOL
```

---

## Hinweise zur Umsetzung

### Schritt 1
Lege einen Text und den String mit den Delimitern an.

### Schritt 2
Zerlege den Text in grobe Teile.

### Schritt 3
Bereinige jedes Teilstück:
- leere Teile überspringen
- Satzzeichen am Anfang und Ende entfernen

### Schritt 4
Gib jedes bereinigte Wort aus.

### Schritt 5
Zähle die verschiedenen Kategorien.

---

## Zusätzliche Hinweise

- Nicht jedes Teilstück ist automatisch ein gültiges Wort
- Nach dem Bereinigen kann ein leerer String entstehen
- Überlege dir, welche Methoden aus der Klasse `String` hilfreich sein könnten
- Nutze die IDE, um nach passenden Methoden zu suchen

---

## Mögliche Leitfragen

- Wie erkenne ich, ob ein Wort nur Grossbuchstaben enthält?
- Wie erkenne ich, ob ein Wort vollständig kleingeschrieben ist?
- Wie kann ich das erste Zeichen eines Wortes prüfen?
- Wie entferne ich Zeichen, die am Anfang oder Ende eines Wortes stehen?
- Welche Rolle spielt der String `delimiters`?

---

## Erwartete Struktur

Du musst keine perfekte Lösung schreiben. Wichtiger ist ein sinnvoller Aufbau.

Eine mögliche Struktur könnte sein:

1. Text definieren
2. Delimiter definieren
3. Text zerlegen
4. Wörter bereinigen
5. Wörter ausgeben
6. Statistik zählen
7. Resultat ausgeben

---

## Zusatzaufgaben

- Erweitere den Delimiter-String um weitere Zeichen
- Teste deinen Parser mit mehreren Beispieltexten
- Überlege, wie man Wörter mit Bindestrich behandeln könnte
- Überlege, ob Zahlen auch als Wörter gezählt werden sollen

---

## Reflexion

- Was war an dieser Aufgabe neu?
- Welche String-Methoden waren besonders hilfreich?
- Wo war die Erkennung von Wortgrenzen schwierig?
- Was würde ich an meinem Parser als Nächstes verbessern?
