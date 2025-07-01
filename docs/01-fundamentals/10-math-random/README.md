# Math and Random Classes

This guide explains how to use the `Math` and `Random` classes in Java, covering the most important methods and how to generate values within ranges.

---

## 🔹 `Math` Class (java.lang.Math)

The `Math` class provides utility methods for math operations. All methods are `static`.

### ✅ Common Methods:

```java
Math.abs(-5);            // 5 (absolute value)
Math.max(10, 20);        // 20
Math.min(10, 20);        // 10

Math.ceil(4.2);          // 5.0 (round up)
Math.floor(4.9);         // 4.0 (round down)
Math.round(4.6);         // 5 (round to nearest)
Math.round(4.4);         // 4
```

### ✅ Constants and Trigonometry:

```java
Math.PI;                // 3.14159...
Math.E;                 // 2.71828...

Math.toDegrees(Math.PI); // 180.0
Math.toRadians(180);     // 3.14159...

Math.sin(Math.PI / 2);   // 1.0
Math.cos(0);             // 1.0
```

### ✅ Exponentials and Roots:

```java
Math.pow(2, 3);         // 8.0 (2^3)
Math.sqrt(16);          // 4.0
Math.exp(1);            // e^1 ≈ 2.718
Math.log(Math.E);       // 1.0 (natural log)
```

### ✅ Generate Random Numbers:

```java
double r = Math.random();        // [0.0, 1.0)
int num = (int)(Math.random() * 10); // [0, 9]
```

### ✅ Create a Range (Inclusive Start, Exclusive End):

```java
int min = 5;
int max = 10;
int random = (int)(Math.random() * (max - min)) + min; // [5, 9]
```

---

## 🔹 `Random` Class (java.util.Random)

Use `Random` for more control and repeatability (with seeds).

### ✅ Example:

```java
import java.util.Random;

Random rand = new Random();

int intVal = rand.nextInt();             // Any int
int tenVal = rand.nextInt(10);           // 0 to 9
boolean boolVal = rand.nextBoolean();    // true or false
double dblVal = rand.nextDouble();       // 0.0 to 1.0
float fltVal = rand.nextFloat();         // 0.0 to 1.0
long lngVal = rand.nextLong();           // Any long
```

### ✅ Generate Integer in Range [min, max)

```java
int min = 5;
int max = 10;
int random = rand.nextInt(max - min) + min; // [5, 9]
```

### ✅ Use Seed for Repeatable Results:

```java
Random seeded = new Random(1234);
int val = seeded.nextInt(); // Always same output
```

---

## 🟦 Best Practices Summary

- ✅ Use `Math` for simple, stateless operations.
- ✅ Use `Math.random()` for quick doubles in [0, 1).
- ✅ Use `Random` for more flexible, testable randomness.
- ✅ For ranges, use formula: `rand.nextInt(max - min) + min`
- ⚠️ `Random` is not secure. For secure random values, use `SecureRandom`.
