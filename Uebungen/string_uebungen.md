# Übungen – String-Klasse (Java)

## 1. Vergleich

```java
String a = "Hallo";
String b = "Hallo";

if (a == b) {
    System.out.println("gleich");
}
```

**Auftrag:**
- Ergebnis erklären

---

## 2. equals()

```java
String input = "exit";
```

- mit equals prüfen

---

## 3. Gross / Klein

```java
String text = "Hallo Welt";
```

- upper / lower

---

## 4. Immutable

```java
String text = "Hallo";
text.toUpperCase();
System.out.println(text);
```

---

## 5. Umlaute

```java
String text = "grüsse aus zürich";
System.out.println(text.toUpperCase());
```

---

## 6. Eingabe

```java
Scanner scanner = new Scanner(System.in);
```

- exit robust prüfen

---

## Zusatz

- quit / by mit if
- danach switch
