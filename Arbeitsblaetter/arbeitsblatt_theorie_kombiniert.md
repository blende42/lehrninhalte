# Tag 1 – Primitive Datentypen & Wrapper (Java)

---

## Lernziele

- Unterschied zwischen primitiven Datentypen und Wrapper-Klassen verstehen
- null und dessen Risiken verstehen
- Strings in Zahlen umwandeln
- Sichere Eingaben implementieren

---

# Theorie – Wrapper-Klassen

## Grundidee

```java
int a = 5;
Integer b = 5;
```

- int → primitiver Typ (immer Wert)
- Integer → Objekt (kann null sein)

---

## Autoboxing / Unboxing

```java
Integer x = 5;   // Autoboxing
int y = x;       // Unboxing
```

Problem:

```java
Integer x = null;
int y = x; // ❌ NullPointerException
```

---

## Wichtige Methoden (selbst erkunden)

```java
Integer.parseInt("42")
Integer.valueOf("42")
Integer.toString(42)
```

👉 Öffne die Klasse in der IDE und finde weitere Methoden

---

# Theorie – String

## Grundidee

```java
String text = "Hallo";
```

- String ist ein Objekt

---

## Immutable

```java
text = text + " Welt";
```

→ neues Objekt wird erstellt

---

## Methoden

```java
text.length()
text.toUpperCase()
text.equals("Hallo")
```

---

## Vergleich

```java
String a = "Hallo";
String b = "Hallo";

a == b
a.equals(b)
```

---

## Eingabe

```java
Scanner scanner = new Scanner(System.in);
String input = scanner.nextLine();
```

---

# Visualisierungen

## Wrapper vs Primitive

```
int a        → [5]
Integer b    → [Objekt → 5]
Integer c    → [null]
```

---

## Autounboxing Fehler

```
Integer(null)
   ↓
int benötigt Wert
   ❌ Fehler
```

---

## Parsing

```
"42"  → 42
"abc" → Fehler
```

---

# Hinweise

- Nutze deine IDE aktiv (Strg + Klick auf Klassen)
- Lies Methodenbeschreibungen
- Probiere Dinge direkt im Code aus

---

# Reflexion

- Was habe ich gelernt?
- Wo hatte ich Schwierigkeiten?
- Was ist mir noch unklar?
