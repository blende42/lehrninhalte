# Musterlösungen – Mini-Projekt String Parser

## 🧩 Lösung 1: Einfache (naive) Lösung

```java
String text = "Hallo, Welt! DAS ist ein \"Test\".";
String delimiters = " .,;:!?()[]{}'\"";

int total = 0;
int lower = 0;
int upperStart = 0;
int upperOnly = 0;
int removed = 0;

String[] parts = text.split(" ");

for (String part : parts) {
    String word = part;

    // vorne entfernen
    while (word.length() > 0 && delimiters.contains("" + word.charAt(0))) {
        word = word.substring(1);
        removed++;
    }

    // hinten entfernen
    while (word.length() > 0 && delimiters.contains("" + word.charAt(word.length() - 1))) {
        word = word.substring(0, word.length() - 1);
        removed++;
    }

    if (word.isEmpty()) continue;

    System.out.println(word);
    total++;

    if (word.equals(word.toLowerCase())) lower++;
    if (Character.isUpperCase(word.charAt(0))) upperStart++;
    if (word.equals(word.toUpperCase())) upperOnly++;
}

System.out.println("Total: " + total);
System.out.println("Lower: " + lower);
System.out.println("UpperStart: " + upperStart);
System.out.println("UpperOnly: " + upperOnly);
System.out.println("Removed delimiters: " + removed);
```

👉 Vorteil: einfach verständlich  
👉 Nachteil: wenig Struktur

---

## 🧩 Lösung 2: Strukturierte Lösung

```java
public static boolean isDelimiter(char c, String delimiters) {
    return delimiters.indexOf(c) >= 0;
}

public static String cleanWord(String word, String delimiters, int[] counter) {
    int start = 0;
    int end = word.length() - 1;

    while (start <= end && isDelimiter(word.charAt(start), delimiters)) {
        start++;
        counter[0]++;
    }

    while (end >= start && isDelimiter(word.charAt(end), delimiters)) {
        end--;
        counter[0]++;
    }

    return (start <= end) ? word.substring(start, end + 1) : "";
}
```

👉 Vorteil: sauber, wiederverwendbar  
👉 Nachteil: etwas anspruchsvoller

---

## 🧩 Lösung 3: Erweiterte Lösung (mit mehr Kontrolle)

Idee:
- Zeichen einzeln durchlaufen
- Wörter selbst zusammensetzen
- maximale Kontrolle über Parsing

👉 geeignet für stärkere Lernende

---

# 📊 Bewertungsskala (Rubric)

## Kriterien

### 1. Funktionalität (0–4 Punkte)
- 0: funktioniert nicht
- 2: teilweise korrekt
- 4: vollständig korrekt

### 2. String-Verarbeitung (0–4 Punkte)
- 0: kaum String-Methoden genutzt
- 2: grundlegende Methoden korrekt
- 4: sinnvoll kombiniert

### 3. Umgang mit Delimitern (0–4 Punkte)
- 0: nicht korrekt entfernt
- 2: teilweise korrekt
- 4: sauber erkannt und gezählt

### 4. Code-Struktur (0–4 Punkte)
- 0: unübersichtlich
- 2: teilweise strukturiert
- 4: klar strukturiert

### 5. Verständlichkeit (0–4 Punkte)
- 0: schwer nachvollziehbar
- 2: teilweise verständlich
- 4: gut lesbar und logisch

---

## Gesamtbewertung

| Punkte | Bewertung |
|------|----------|
| 0–8  | ungenügend |
| 9–14 | genügend |
| 15–18| gut |
| 19–20| sehr gut |

---

## 💡 Lehrerhinweis

Achte besonders auf:
- Denkprozess, nicht nur Ergebnis
- Umgang mit Randfällen
- ob der Lernende selbstständig Lösungen findet
