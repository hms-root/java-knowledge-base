# Wrapper Classes and Metadata

This guide explains wrapper classes, autoboxing/unboxing, conversions, and metadata access using `getClass()` with clean examples and best practices.

---

## 🔹 What Are Wrapper Classes?

Java provides **wrapper classes** to treat primitive types as objects. Each primitive has a corresponding wrapper:

| Primitive | Wrapper Class |
| --------- | ------------- |
| `int`     | `Integer`     |
| `double`  | `Double`      |
| `char`    | `Character`   |
| `boolean` | `Boolean`     |
| `byte`    | `Byte`        |
| `short`   | `Short`       |
| `long`    | `Long`        |
| `float`   | `Float`       |

✅ Wrapper classes allow use in **collections**, **generics**, and provide **utility methods**.

---

## 🔹 Methods and Conversions

Each wrapper class offers methods for parsing, converting, and inspecting values.

### Example with `Integer`:

```java
int i = Integer.parseInt("42");           // String to int
String s = Integer.toString(42);          // int to String
Integer obj = Integer.valueOf("42");      // String to Integer
int value = obj.intValue();               // Integer to int
```

### Example with `Double`:

```java
double d = Double.parseDouble("3.14");
Double obj = Double.valueOf("3.14");
String str = obj.toString();
```

🧠 **Key Difference**:

- `parseXxx()` → returns primitive
- `valueOf()` → returns wrapper object
- `xxxValue()` → extracts primitive from wrapper

---

## 🔹 Autoboxing and Unboxing

Java automatically converts between primitives and wrappers.

### Autoboxing:

```java
Integer a = 5; // int → Integer
```

### Unboxing:

```java
int b = a;     // Integer → int
```

✅ Reduces boilerplate.  
⚠️ Can cause performance issues in tight loops or unnecessary boxing/unboxing.

---

## 🔹 Wrapper Classes with Relational Operators

Only primitives can be compared with `==`, `<`, `>` etc.

```java
Integer a = 100;
Integer b = 100;
System.out.println(a == b);         // true (cached)

Integer x = 1000;
Integer y = 1000;
System.out.println(x == y);         // false (outside cache)
System.out.println(x.equals(y));    // true
```

📌 `==` compares **references**, not values (except for small integers due to caching).  
✅ Use `.equals()` to compare **values**.

---

## 🔹 `getClass()` for Reflection and Metadata

Used to inspect runtime type information.

```java
String text = "Hello";
System.out.println(text.getClass().getName()); // java.lang.String
```

### Example with wrapper:

```java
Integer num = 10;
Class<?> clazz = num.getClass();
System.out.println(clazz.getSimpleName()); // Integer
```

✅ Useful for debugging, logging, or reflection.  
🔍 Can be combined with `.getDeclaredMethods()`, `.getFields()`, etc. for full reflection.

---

## 🟦 Best Practices Summary

- ✅ Use wrapper classes when working with collections or generics.
- ✅ Prefer `valueOf()` over `new Wrapper()` — uses caching.
- ✅ Avoid using `==` for wrapper comparisons — use `.equals()`.
- ✅ Autoboxing improves readability, but watch performance in critical loops.
- ✅ Use `getClass()` to access metadata and support reflective programming.
