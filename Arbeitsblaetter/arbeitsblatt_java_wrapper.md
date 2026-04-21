# Tag 1 – Primitive Datentypen & Wrapper (Java)

## Lernziele

- Ich verstehe den Unterschied zwischen primitiven Datentypen und Wrapper-Klassen
- Ich weiss, warum `null` zu Fehlern führen kann
- Ich kann Strings in Zahlen umwandeln
- Ich kann einfache Fehler in Java nachvollziehen und erklären
- Ich kann eine sichere Eingabe implementieren

---

## Theorie

### Primitive Datentypen vs. Wrapper

| Typ        | Beispiel | Eigenschaften |
|------------|----------|--------------|
| primitiver Typ | `int` | hat immer einen Wert |
| Wrapper-Klasse | `Integer` | ist ein Objekt, kann `null` sein |

### Visualisierung

```
int a = 5
→ Wert direkt gespeichert

Integer b = 5
→ Objekt → enthält Wert 5

Integer c = null
→ kein Objekt vorhanden
```

---

### Autounboxing (wichtig!)

```
Integer zahl = null;
int x = zahl;
```

👉 Ablauf:

```
Integer (null)
   ↓ wird automatisch umgewandelt
int (braucht Wert)
   ❌ Fehler (NullPointerException)
```

---

### String → Zahl

```
String input = "42";
int value = Integer.parseInt(input);
```

```
"42"   → 42 ✅
"abc"  → ❌ Fehler (Exception)
```

---

### Vergleich

```
Integer a = 100;
Integer b = 100;
```

- `==` → vergleicht Referenz
- `.equals()` → vergleicht Wert

---

## Übungen

### 1. Warum crasht mein Programm?

```java
Integer zahl = null;
int x = zahl;

System.out.println(x);
```

**Auftrag:**
- Führe den Code aus
- Notiere die Fehlermeldung
- Erkläre:
  - Was passiert?
  - Warum passiert es?

---

### 2. Primitive vs. Wrapper

```java
int a = 5;
Integer b = 5;

System.out.println(a);
System.out.println(b);
```

**Auftrag:**
- Erkläre den Unterschied zwischen `int` und `Integer`

**Zusatz:**

```java
Integer c = null;
System.out.println(c);
```

- Was passiert hier?

---

### 3. String → Zahl

```java
String input = "42";
```

**Auftrag:**
- Wandle den String in einen `int` um
- Gib das Resultat aus

**Erweiterung:**

```java
String input = "abc";
```

- Was passiert?
- Warum?

---

### 4. == oder equals?

```java
Integer a = 100;
Integer b = 100;

System.out.println(a == b);
System.out.println(a.equals(b));
```

**Auftrag:**
- Sage die Ausgabe voraus
- Führe den Code aus
- Erkläre den Unterschied

---

### 5. Sichere Eingabe (erweitert)

```java
public static Integer parseOrNull(String s) {
    // TODO
}
```

**Auftrag:**
- Wenn gültige Zahl → zurückgeben
- Wenn Fehler → `null` zurückgeben

**Testfälle:**

```java
parseOrNull("42")   → 42
parseOrNull("abc")  → null
parseOrNull("")     → null
parseOrNull(null)   → null
```

---

### 6. Benutzereingabe mit Schleife

```java
Scanner scanner = new Scanner(System.in);

while (true) {
    System.out.print("Zahl eingeben (oder 'exit'): ");
    String input = scanner.nextLine();

    // TODO
}
```

**Auftrag:**
- Programm läuft so lange, bis `"exit"` eingegeben wird
- Verwende `parseOrNull(...)`
- Wenn Zahl gültig → ausgeben
- Wenn ungültig → Fehlermeldung ausgeben

---

## Zusatzaufgaben

- Verhindere, dass das Programm bei `null` abstürzt
- Gib eine verständlichere Fehlermeldung aus
- Zähle, wie viele gültige Zahlen eingegeben wurden

---

## Reflexion

- Was habe ich heute gelernt?
- Wo hatte ich Schwierigkeiten?
- Was ist der Unterschied zwischen `int` und `Integer`?
- Warum kann `null` gefährlich sein?
