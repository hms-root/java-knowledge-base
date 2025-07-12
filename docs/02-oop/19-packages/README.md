# Packages

In Java, **packages** are namespaces used to group related classes and interfaces. They help:

- Avoid class name conflicts.
- Organize code in a logical manner.
- Control access with visibility modifiers.

Think of packages like folders in a filesystem: they encapsulate and structure your codebase meaningfully.

---

## 🧭 Package Naming Conventions

### ✅ Standard Naming Rules:

- Always **lowercase**.
- Use **reverse domain names** to ensure uniqueness (e.g., `com.companyname.projectname`).
- Avoid underscores or capital letters.

### 🔁 Examples:

| Usage        | Package Name               |
| ------------ | -------------------------- |
| Utility code | `com.clayandcode.utils`    |
| Models       | `com.clayandcode.models`   |
| Services     | `com.clayandcode.services` |

---

## ✍️ Defining a Package

Declare a package at the very **top** of the `.java` file:

```java
package com.clayandcode.utils;

public class StringUtils {
    public static String capitalize(String input) {
        return input.substring(0, 1).toUpperCase() + input.substring(1);
    }
}
```

---

## 🛠️ Creating a Package in IntelliJ IDEA

1. **Right-click** `src` folder → `New` → `Package`
2. Enter full package name: `com.clayandcode.utils`
3. IntelliJ will auto-create folder structure and associate classes.

---

## 📥 Import vs Fully Qualified Name

### 📌 Fully Qualified Name

```java
public class Test {
    com.clayandcode.utils.StringUtils.capitalize("hello");
}
```

Pros:

- No ambiguity  
  Cons:
- Verbose
- Reduces readability

### 📌 Import Statement

```java
import com.clayandcode.utils.StringUtils;

public class Test {
    StringUtils.capitalize("hello");
}
```

✅ Preferred: clean, readable, easier to maintain.

---

## 🌐 Wildcard Import vs Explicit Import

### Wildcard (`*`):

```java
import com.clayandcode.utils.*;
```

Imports **all classes** from the package.

### Explicit:

```java
import com.clayandcode.utils.StringUtils;
```

Imports **only** the used class.

### 💡 Performance?

- **No difference at runtime**: the compiler only loads used classes.
- **Best Practice**: use explicit imports to **improve clarity** and **avoid conflicts**.

---

## 🔒 Access Control via Modifiers

Java provides four access levels to control visibility across packages:

| Modifier    | Same Class | Same Package | Subclass | Everywhere |
| ----------- | ---------- | ------------ | -------- | ---------- |
| `public`    | ✅         | ✅           | ✅       | ✅         |
| `protected` | ✅         | ✅           | ✅       | ❌         |
| _(default)_ | ✅         | ✅           | ❌       | ❌         |
| `private`   | ✅         | ❌           | ❌       | ❌         |

---

## 🧠 Access Scope Insights

- Use `public` sparingly: only for APIs intended for broad use.
- Prefer package-private (default) for internal helpers.
- Use `protected` when building extensible frameworks.
- `private` is best for encapsulation.

---

## 🔁 Static Imports

### Purpose:

Allows usage of static members without class qualification.

### Example:

```java
import static java.lang.Math.*;

public class Circle {
    public double area(double radius) {
        return PI * pow(radius, 2);
    }
}
```

### ✅ Best Use Cases:

- Constants (`PI`, `E`)
- Utility methods (`assertEquals`, `max`, `min`)
- Improves readability in **test code** or **math-heavy logic**

### ⚠️ Pitfalls:

- Can reduce clarity if overused
- Avoid wildcard static imports (`import static ...*`) in production code

---

## ✅ Best Practices Summary

- Structure packages around **domain functionality**, not technical tiers.
- Use **explicit imports** to increase clarity.
- Leverage **default (package-private)** access where possible.
- Keep package hierarchies **shallow and meaningful**.
- Avoid **cyclic dependencies** between packages.

---
