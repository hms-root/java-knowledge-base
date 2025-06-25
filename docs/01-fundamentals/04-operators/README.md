# Operators

This guide covers all core Java operators with pro-level detail and best practices.

---

## 🔹 Arithmetic Operators

Used for basic mathematical operations.

| Operator | Description        | Example |
| -------- | ------------------ | ------- |
| `+`      | Addition           | `a + b` |
| `-`      | Subtraction        | `a - b` |
| `*`      | Multiplication     | `a * b` |
| `/`      | Division           | `a / b` |
| `%`      | Modulo (remainder) | `a % b` |

🧠 **Note**: Division between integers discards decimals.

---

## 🔹 Assignment Operators

Assign values to variables.

| Operator | Description         | Example  |
| -------- | ------------------- | -------- |
| `=`      | Simple assignment   | `a = 5`  |
| `+=`     | Add and assign      | `a += 2` |
| `-=`     | Subtract and assign | `a -= 3` |
| `*=`     | Multiply and assign | `a *= 4` |
| `/=`     | Divide and assign   | `a /= 2` |
| `%=`     | Modulo and assign   | `a %= 3` |

---

## 🔹 Unary Operators

Operate on a single operand.

| Operator | Description | Example        |
| -------- | ----------- | -------------- |
| `+`      | Unary plus  | `+a`           |
| `-`      | Unary minus | `-a`           |
| `++`     | Increment   | `++a` or `a++` |
| `--`     | Decrement   | `--a` or `a--` |
| `!`      | Logical NOT | `!true`        |

---

## 🔹 Increment and Decrement (Pre vs Post)

```java
int a = 5;
int pre = ++a; // a = 6, pre = 6
int post = a++; // post = 6, a = 7
```

| Form  | Description                         |
| ----- | ----------------------------------- |
| `++a` | Pre-increment: increment, then use  |
| `a++` | Post-increment: use, then increment |
| `--a` | Pre-decrement                       |
| `a--` | Post-decrement                      |

> ✅ Use pre-increment in loops when performance is key (slightly more optimized).

---

## 🔹 Relational Operators

Compare two values.

| Operator | Description      | Example  |
| -------- | ---------------- | -------- |
| `==`     | Equal to         | `a == b` |
| `!=`     | Not equal to     | `a != b` |
| `>`      | Greater than     | `a > b`  |
| `<`      | Less than        | `a < b`  |
| `>=`     | Greater or equal | `a >= b` |
| `<=`     | Less or equal    | `a <= b` |

🔐 Use `.equals()` for objects like `String` instead of `==`.

---

## 🔹 Logical Operators

Used with boolean expressions.

- `&&` — **Logical AND**  
  Example: `a > 0 && b > 0`  
  Returns `true` only if **both** conditions are true.

- `||` — **Logical OR**  
  Example: `a > 0 || b > 0`  
  Returns `true` if **at least one** condition is true.

- `!` — **Logical NOT**  
  Example: `!(a > b)`  
  Inverts the boolean value of the expression.

> ✅ Use `&&` and `||` for compound conditions.

---

## 🔹 Ternary Operator

Compact `if-else` expression.

```java
String result = (score >= 60) ? "Pass" : "Fail";
```

📌 Syntax:

```java
(condition) ? valueIfTrue : valueIfFalse;
```

---

## 🔹 `instanceof` Operator

Checks if an object is an instance of a class or interface.

```java
if (obj instanceof String) {
    System.out.println("It's a string.");
}
```

### With abstract types and interfaces:

```java
List<String> list = new ArrayList<>();
if (list instanceof List) {
    System.out.println("It is a List.");
}
```

🧠 `instanceof` also works with abstract classes and interfaces.

### Since Java 16+: Pattern matching

```java
if (obj instanceof String s) {
    System.out.println(s.toUpperCase());
}
```

---

## 🔹 Operator Precedence

Determines evaluation order in complex expressions.

### Common Precedence Levels (High to Low)

1. Postfix: `expr++` `expr--`
2. Unary: `++expr` `--expr` `+` `-` `!`
3. Multiplicative: `*` `/` `%`
4. Additive: `+` `-`
5. Relational: `<` `>` `<=` `>=` `instanceof`
6. Equality: `==` `!=`
7. Logical AND: `&&`
8. Logical OR: `||`
9. Ternary: `? :`
10. Assignment: `=` `+=` `-=` etc.

### Example:

```java
int result = 10 + 5 * 2; // result = 20 (not 30)
```

> 🔍 Use parentheses `()` to enforce custom order.

---

## 🟦 Best Practices Summary

- ✅ Use `++a` instead of `a++` in loops for minor performance gain.
- ✅ Avoid using `==` for object comparison, prefer `.equals()`.
- ✅ Prefer `StringBuilder` for string concatenation in loops.
- ✅ Use `instanceof` safely to check types, including interfaces and abstract classes.
- ✅ Always use parentheses to clarify logic when mixing operators.
