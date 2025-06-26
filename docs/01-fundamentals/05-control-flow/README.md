# Control Flow Statements

This guide explains the core control flow structures in Java with clean syntax, detailed explanation, and best practices for each.

---

## 🔹 `if` / `else if` / `else` Statement

Used to execute code conditionally.

```java
if (score >= 90) {
    System.out.println("Excellent");
} else if (score >= 60) {
    System.out.println("Pass");
} else {
    System.out.println("Fail");
}
```

✅ Use `else if` for multiple conditions.  
⚠️ Always use `{}` even for one-line blocks to prevent logic errors.

---

## 🔹 `switch` / `case` Statement

Efficient alternative to multiple `if-else` conditions on the same variable.

```java
int day = 2;
switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    default:
        System.out.println("Other day");
}
```

- `break` prevents fall-through (mandatory unless intentional).
- `default` is optional, acts as a fallback.
- Since Java 14, enhanced syntax:

```java
switch (day) {
    case 1 -> System.out.println("Monday");
    case 2 -> System.out.println("Tuesday");
    default -> System.out.println("Other day");
}
```

---

## 🔹 `for` Loop

Used when the number of iterations is known.

```java
for (int i = 0; i < 5; i++) {
    System.out.println(i);
}
```

✅ Ideal for index-based iteration.

---

## 🔹 `while` Loop

Runs as long as the condition is true.

```java
int i = 0;
while (i < 5) {
    System.out.println(i);
    i++;
}
```

✅ Use when the number of iterations is unknown and the condition is evaluated **before** each loop.

---

## 🔹 `do-while` Loop

Executes at least once, condition is checked **after** the body.

```java
int i = 0;
do {
    System.out.println(i);
    i++;
} while (i < 5);
```

✅ Guarantees at least one execution of the loop.

---

## 🔹 Enhanced `for` Loop (for-each)

Used to iterate collections or arrays.

```java
String[] names = {"Ana", "Bob", "Cleo"};
for (String name : names) {
    System.out.println(name);
}
```

✅ Cleaner syntax, no index management.  
❌ You can't modify the collection structure (e.g., remove items).

---

## 🔹 `break` and `continue`

### `break`:

Exits the loop immediately.

```java
for (int i = 0; i < 10; i++) {
    if (i == 5) break;
    System.out.println(i);
}
```

### `continue`:

Skips current iteration and continues with the next.

```java
for (int i = 0; i < 5; i++) {
    if (i == 2) continue;
    System.out.println(i); // Skips 2
}
```

---

## 🔹 Labeled `break` / `continue`

Used in **nested loops** to control flow more precisely.

```java
outer:
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        if (i == j) continue outer;
        System.out.println(i + " " + j);
    }
}
```

- `break label;` exits **the labeled loop**.
- `continue label;` skips to **next iteration of the labeled loop**.

🧠 Labels give you fine-grained control in nested structures. Use with care — overuse can reduce readability.

---

## 🟦 Best Practices Summary

- ✅ Always use `{}` brackets for control structures — avoid bugs with one-line blocks.
- ✅ Use `switch` for fixed, known values; prefer enhanced `switch` for readability.
- ✅ Prefer `for-each` for read-only iteration over collections.
- ✅ Use `break` and `continue` to simplify loop logic — but keep it clear.
- ✅ Labeled loops are powerful but can hurt readability. Use only when really needed.
