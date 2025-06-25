# String

In Java, a `String` is an **immutable object** that represents a **sequence of Unicode characters**. It is part of the `java.lang` package, so no import is needed.

---

## 🔹 Instantiating Strings: Literal vs `new`

### ✅ Literal form

```java
String name = "Manuel";
String nameCopy = "Manuel";
```

📌 Both variables point to the **same object** in the **String Pool**. Java maintains a string pool to save memory. If a literal already exists, the reference is reused.

### ❌ Using `new`

```java
String name = new String("Manuel");
```

🧠 This creates a **new object in heap memory**, even if the content is the same. It does **not** reuse the string pool.

### Example:

```java
String a = "Manuel";
String b = "Manuel";
System.out.println(a == b); // true

String c = new String("Manuel");
System.out.println(a == c); // false
System.out.println(a.equals(c)); // true
```

💡 **Best practices**:

- Use **literals** whenever possible to leverage pooling.
- Use `equals()` to compare contents, not `==`.

---

## 🔹 Concatenation: `+`, `concat`, `StringBuilder`

### `+` Operator

```java
String result = "Hello " + "World";
```

✔️ Very readable and commonly used.  
❌ Internally creates a `StringBuilder` in compiled code, **but only for simple cases**.

⚠️ Inefficient when used repeatedly in **loops**:

```java
String text = "";
for (int i = 0; i < 1000; i++) {
    text += i;  // Creates many intermediate objects!
}
```

### `concat()` Method

```java
String result = "Hello".concat(" World");
```

✔️ Slightly more efficient than `+`, but only works with other `String` objects.  
❌ Not as readable, and not used in complex concatenations or loops.

```java
String a = "Hello";
String b = "World";
String result = a.concat(" ").concat(b); // OK but verbose
```

### `StringBuilder`

```java
StringBuilder sb = new StringBuilder();
sb.append("Hello");
sb.append(" ");
sb.append("World");
String result = sb.toString();
```

✔️ ✅ Most **efficient** for many concatenations, especially in **loops or methods with dynamic content**.  
✔️ Avoids creating multiple intermediate `String` objects.

#### Summary Comparison Table

| Method          | Thread-safe | Efficient in Loops | Readability        | Use Case                                         |
| --------------- | ----------- | ------------------ | ------------------ | ------------------------------------------------ |
| `+`             | No          | ❌                 | ✅                 | Simple concatenations outside of loops           |
| `concat()`      | No          | ❌                 | Moderate           | Basic string concatenation                       |
| `StringBuilder` | No          | ✅                 | ✅ (with practice) | Repeated or dynamic concatenation ✅ Recommended |

> 🧠 Tip: Use `StringBuilder` when concatenating inside `for`, `while`, or recursive methods for better performance.

---

## 🔹 Operator Precedence

```java
int age = 30;
System.out.println("Age: " + age + 5);      // Age: 305
System.out.println("Age: " + (age + 5));    // Age: 35
```

✅ `+` is left-associative. When a `String` is involved, everything is treated as a string.

---

## 🔹 Immutability

```java
String original = "hello";
String modified = original.toUpperCase();
```

📌 `String` is **immutable**: its content cannot be changed. Methods like `toUpperCase()` return a **new object**.

🔐 Advantages:

- Thread-safe
- Secure
- Cacheable (pooling)

💡 Always reassign the result if you want changes:

```java
str = str.trim(); // Without this, nothing changes!
```

---

## 🔹 String Validation

```java
String str = " ";
str.isEmpty();   // false → checks only if length == 0
str.isBlank();   // true  → also considers whitespace
```

✅ Use `isBlank()` to check for meaningful content.  
⚠️ Does **not** handle `null` — will throw `NullPointerException`.

> 🛡️ Best practice: Always validate strings for `null` before using methods like `isEmpty()`, `isBlank()`, or `length()` to avoid runtime exceptions.

---

## 🔹 Useful String Methods

### 🔠 General info

```java
str.length();          // Length
str.toUpperCase();     // "manuel" → "MANUEL"
str.toLowerCase();     // "MANUEL" → "manuel"
```

### 🔍 Comparisons

```java
str.equals("text");             // exact content match
str.equalsIgnoreCase("Text");  // case-insensitive match
str.compareTo("other");        // 0 if equal, <0 if less, >0 if greater (lexical order)
```

### 🔎 Access / Substrings

```java
str.charAt(2);           // char at position 2
str.substring(2, 5);     // from 2 (inclusive) to 5 (exclusive)
```

### 🔄 Replace / Search

```java
str.replace("a", "o");     // replaces all "a" with "o"
str.indexOf("a");          // index of first occurrence
str.lastIndexOf("a");      // index of last occurrence
str.contains("abc");       // true if contains "abc"
```

### 🚩 Start/End Check

```java
str.startsWith("pre");     // starts with "pre"
str.endsWith("end");       // ends with "end"
```

### 🔧 Cleanup & Conversion

```java
str.trim();                // trims whitespace
str.isEmpty();             // ""
str.isBlank();             // "", " ", "	"…
str.toCharArray();         // converts to char array
```

### 📐 Splitting

```java
String[] parts = str.split(" ");
```

### 🧠 `.transform(Function<String, R>)` (Java 12+)

Applies a lambda directly:

```java
String result = " hello ".transform(s -> s.trim().toUpperCase()); // "HELLO"
```

---

## 🟦 Pro-Level Best Practices

- ✅ Prefer **string literals** over `new String()`.
- ✅ Use `equals()` to compare content, **not `==`**.
- ✅ Use `StringBuilder` inside loops or repeated operations.
- ✅ Remember: strings are **immutable**.
- ✅ Always null-check before using `isEmpty()` or `isBlank()`.
- ✅ Be aware of **precedence** in mixed expressions.

---
