# Musterlösungen – StringBuilder & Parser

## 1. append()

```java
StringBuilder sb = new StringBuilder();
sb.append("Hallo");
sb.append(" ");
sb.append("Welt");
System.out.println(sb.toString());
```

---

## 2. insert()

```java
StringBuilder sb = new StringBuilder("Welt");
sb.insert(0, "Hallo ");
System.out.println(sb.toString());
```

---

## 3. delete()

```java
StringBuilder sb = new StringBuilder("Hallo Welt");
sb.delete(0, 6);
System.out.println(sb.toString());
```

---

## 4. replace()

```java
StringBuilder sb = new StringBuilder("Hallo Java");
sb.replace(6, 10, "Welt");
System.out.println(sb.toString());
```

---

## 5. reverse()

```java
StringBuilder sb = new StringBuilder("abc");
sb.reverse();
System.out.println(sb.toString());
```

---

## 6. Kombination

```java
StringBuilder sb = new StringBuilder("Hallo");
sb.insert(0, "Start: ");
String result = sb.toString().toUpperCase() + "!";
System.out.println(result);
```

---

## 7. Parser (vereinfacht)

```java
String text = "Hallo, Welt! DAS ist ein Test.";
String delimiters = " .,;:!?";

StringBuilder words = new StringBuilder();
int total = 0;

for (String raw : text.split(" ")) {
    String word = raw;

    // vorne bereinigen
    while (word.length() > 0 && delimiters.contains("" + word.charAt(0))) {
        word = word.substring(1);
    }

    // hinten bereinigen
    while (word.length() > 0 && delimiters.contains("" + word.charAt(word.length()-1))) {
        word = word.substring(0, word.length()-1);
    }

    if (!word.isEmpty()) {
        words.append(word).append("\n");
        total++;
    }
}

StringBuilder result = new StringBuilder();
result.append("Wörter:\n");
result.append(words);
result.append("\nTotal: ").append(total);

System.out.println(result.toString());
```

---

## 💡 Hinweis

- String für Verarbeitung
- StringBuilder für Ausgabe
