# Theorie – String (Java)

## 🎯 Ziel

- Ich verstehe, was ein String ist
- Ich kann einfache String-Operationen anwenden
- Ich kann Methoden selbst in der IDE finden

---

## 🧠 Grundidee

```java
String text = "Hallo";
```

👉 Strings sind Objekte

---

## 🔒 Wichtig

Strings sind unveränderlich (immutable)

```java
text = text + " Welt";
```

---

## 🔧 Methoden

```java
text.length()
text.toUpperCase()
text.toLowerCase()
text.equals("Hallo")
```

👉 Weitere Methoden in der IDE suchen

---

## ⚠️ Vergleich

```java
String a = "Hallo";
String b = "Hallo";

a == b        // Referenz
a.equals(b)   // Inhalt
```

---

## 🔄 Eingabe

```java
Scanner scanner = new Scanner(System.in);
String input = scanner.nextLine();
```

---

## 🔍 Arbeitsauftrag

Finde in deiner IDE:
- Länge eines Strings
- Teilstring
- Prüfen, ob Text enthalten ist

---

## 💡 Merksätze

- Strings sind Objekte
- Strings sind unveränderlich
- Vergleiche mit equals()
