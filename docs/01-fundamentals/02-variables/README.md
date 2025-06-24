# Variables

This document provides a **complete, professional, and senior-level** explanation of variables in Java, covering all key concepts with examples and best practices.

---

## ✅ What Are Variables?

A **variable** is a **named memory location** that stores a value which can change during program execution.

In Java, **every variable must be declared with a data type**, which tells the compiler how much memory it needs and what operations are allowed.

```java
int age = 30;
String name = "Manuel";
```

---

## ✅ Primitive vs Reference Data Types

### 🔹 Primitive Types

These are the most basic types. They are not objects and store values directly.

| Type      | Bits | Range                     | Wrapper Class | Default Value |
| --------- | ---- | ------------------------- | ------------- | ------------- |
| `byte`    | 8    | -128 to 127               | `Byte`        | 0             |
| `short`   | 16   | -32,768 to 32,767         | `Short`       | 0             |
| `int`     | 32   | -2³¹ to 2³¹-1             | `Integer`     | 0             |
| `long`    | 64   | -2⁶³ to 2⁶³-1             | `Long`        | 0L            |
| `float`   | 32   | ±1.4×10⁻⁴⁵ to ±3.4×10³⁸   | `Float`       | 0.0f          |
| `double`  | 64   | ±4.9×10⁻³²⁴ to ±1.8×10³⁰⁸ | `Double`      | 0.0d          |
| `char`    | 16   | 'null' to '￿'             | `Character`   | 'null'        |
| `boolean` | 1\*  | true / false              | `Boolean`     | false         |

> \* Technically not defined in bits; JVM may use 1 byte.

### 🔹 Reference Types

These store **references to objects** in heap memory.

```java
String text = "Hello";
int[] numbers = {1, 2, 3};
List<String> names = new ArrayList<>();
```

---

## ✅ Rules for Defining a Variable

- Must be **declared before use**.
- Name must start with a **letter, `$`, or `_`** (not a digit).
- Cannot be a **reserved keyword**.
- Use **camelCase** convention (`myName`, `totalSales`).
- Best practices:
  - Use **descriptive names**.
  - Avoid cryptic abbreviations.
  - Use `final` for constants.

```java
final double PI = 3.14159;
```

---

## ✅ Variable Scope (Context)

Defines where a variable can be accessed:

- **Local**: defined inside a method.
- **Instance**: belongs to an object.
- **Static**: belongs to the class.

```java
public class Person {
    static String species = "Human";    // class variable
    String name;                        // instance variable

    public void greet() {
        String greeting = "Hello";      // local variable
        System.out.println(greeting + " " + name);
    }
}
```

---

## ✅ Type Inference (`var`) and Dynamic Typing

Since Java 10, `var` allows **type inference at compile time**:

```java
var number = 10; // inferred as int
var list = new ArrayList<String>(); // inferred as ArrayList<String>
```

### ❌ Is Java dynamically typed like Python or JS?

**No. Java is statically typed**:

- Variable types are **known at compile time**.
- **Type cannot change** once assigned.

Advantages:

- Better performance.
- Errors caught at compile time.
- More robust refactoring tools.

---

## ✅ Scientific Notation

Used with `float` and `double`:

```java
double number = 1.2e3; // 1.2 × 10^3 = 1200.0
float small = 5.6e-4f; // 5.6 × 10^-4 = 0.00056
```

> To interpret:

- Positive exponent → **move decimal to the right**.
- Negative exponent → **move to the left**.

---

## ✅ Escape Characters

Used to represent special characters in `String` or `char`:

| Escape | Meaning         |
| ------ | --------------- |
| `\n`   | New line        |
| `\t`   | Tab             |
| `\\`   | Backslash       |
| `\"`   | Double quote    |
| `\'`   | Single quote    |
| `\r`   | Carriage return |
| `\b`   | Backspace       |

```java
String example = "Hello,\n\t\"Manuel\"";
```

---

## ✅ Number Systems in Java

Java supports numeric literals in different bases:

```java
int decimal = 42;       // base 10
int binary = 0b101010;  // base 2
int octal = 052;        // base 8
int hex = 0x2A;         // base 16
```

---

## ✅ Type Conversion

### 🔹 String to Primitives

Use `parseXxx` from wrapper classes:

```java
int i = Integer.parseInt("123");
double d = Double.parseDouble("3.14");
boolean b = Boolean.parseBoolean("true");
```

### 🔹 Primitives to String

Use `String.valueOf()` or concatenation:

```java
String s1 = String.valueOf(123);
String s2 = 123 + ""; // not recommended
```

### 🔹 Between Primitives

#### Widening (automatic, safe)

```java
int i = 100;
long l = i;
double d = l;
```

#### Narrowing (explicit, may lose data)

```java
double d = 3.14;
int i = (int) d; // result: 3
```

---
