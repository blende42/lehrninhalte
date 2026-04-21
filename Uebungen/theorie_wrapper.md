# Theorie – Wrapper-Klassen (Java)

## 🎯 Ziel

- Ich verstehe, was Wrapper-Klassen sind
- Ich weiss, wann ich sie verwende
- Ich kann wichtige Methoden selbst in der IDE finden

---

## 🧠 Grundidee

Primitive Datentypen:

```java
int zahl = 5;
```

Wrapper-Klassen:

```java
Integer zahl = 5;
```

👉 Wrapper-Klassen sind Objekte, die primitive Werte „verpacken“

---

## ⚠️ Unterschied

- int → hat immer einen Wert  
- Integer → kann null sein  

---

## 💥 Achtung: Autoboxing / Unboxing

```java
Integer x = 5;
int y = x;
```

Problem:

```java
Integer x = null;
int y = x; // Fehler
```

---

## 🔧 Methoden (selbst erkunden!)

```java
Integer.parseInt("42")
Integer.valueOf("42")
Integer.toString(42)
```

👉 Öffne die Klasse in der IDE und finde weitere Methoden

---

## 🔍 Arbeitsauftrag

Finde in deiner IDE:
- 3 Methoden der Klasse Integer
- Beschreibe kurz, was sie tun

---

## 💡 Merksätze

- Wrapper sind Objekte
- Wrapper können null sein
- Wrapper haben Methoden
