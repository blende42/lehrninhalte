# Übungen – Primitive Datentypen & Wrapper (Java)

## 1. Warum crasht mein Programm?

```java
Integer zahl = null;
int x = zahl;

System.out.println(x);
```

**Auftrag:**
- Programm ausführen
- Fehlermeldung notieren
- Erklären, was passiert und warum

---

## 2. Primitive vs. Wrapper

```java
int a = 5;
Integer b = 5;

System.out.println(a);
System.out.println(b);
```

**Auftrag:**
- Unterschied zwischen `int` und `Integer` erklären

**Zusatz:**

```java
Integer c = null;
System.out.println(c);
```

- Was passiert hier?

---

## 3. String → Zahl

```java
String input = "42";
```

**Auftrag:**
- String in `int` umwandeln
- Ergebnis ausgeben

**Erweiterung:**

```java
String input = "abc";
```

- Was passiert?
- Warum?

---

## 4. == oder equals?

```java
Integer a = 100;
Integer b = 100;

System.out.println(a == b);
System.out.println(a.equals(b));
```

**Auftrag:**
- Ausgabe vorhersagen
- Unterschied erklären

---

## 5. Sichere Eingabe (parseOrNull)

```java
public static Integer parseOrNull(String s) {
    // TODO
}
```

**Auftrag:**
- Zahl → zurückgeben
- Fehler → `null`

**Testfälle:**

```java
parseOrNull("42")   → 42
parseOrNull("abc")  → null
parseOrNull("")     → null
parseOrNull(null)   → null
```

---

## 6. Benutzereingabe mit Schleife

```java
Scanner scanner = new Scanner(System.in);

while (true) {
    System.out.print("Zahl eingeben (oder 'exit'): ");
    String input = scanner.nextLine();

    // TODO
}
```

**Auftrag:**
- Schleife läuft bis "exit"
- parseOrNull verwenden
- gültige Zahl → ausgeben
- ungültig → Fehlermeldung

---

## Zusatzaufgaben

- Programm vor Absturz bei `null` schützen
- Bessere Fehlermeldung ausgeben
- Anzahl gültiger Eingaben zählen
