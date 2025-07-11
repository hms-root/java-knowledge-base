# Access Modifiers

Access modifiers in Java control the **visibility** and **accessibility** of classes, methods, constructors, and variables. They are essential for implementing **encapsulation**, one of the core principles of Object-Oriented Programming (OOP).

Understanding when and how to use each modifier is fundamental for writing clean, secure, and maintainable code — especially at an enterprise or framework level.

---

## Types of Access Modifiers

There are **four** access modifiers in Java:

| Modifier    | Class | Package | Subclass | World |
| ----------- | :---: | :-----: | :------: | :---: |
| `public`    |  ✅   |   ✅    |    ✅    |  ✅   |
| `protected` |  ❌   |   ✅    |    ✅    |  ❌   |
| _(default)_ |  ❌   |   ✅    |    ❌    |  ❌   |
| `private`   |  ❌   |   ❌    |    ❌    |  ❌   |

> 🔸 `Class` here refers to **top-level** classes. Only `public` and _default_ (package-private) are allowed for top-level classes.

---

## 1. `public`

Accessible **from anywhere**. Suitable for API methods, core models, and constants.

```java
public class User {
    public String name;

    public void greet() {
        System.out.println("Hello, " + name);
    }
}
```

### Use Cases:

- Top-level API classes or interfaces.
- Constants (`public static final`).
- Methods designed for external use.

---

## 2. `private`

Accessible **only within the same class**. Not allowed for top-level classes.

```java
public class Account {
    private double balance;

    private void logAccess() {
        // internal logic
    }

    public double getBalance() {
        return balance;
    }
}
```

### Use Cases:

- Internal state encapsulation.
- Helper methods.
- Implementation hiding.

---

## 3. `protected`

Accessible **within the same package** and by **subclasses** in any package.

```java
public class Vehicle {
    protected void startEngine() {
        System.out.println("Engine started.");
    }
}

public class Car extends Vehicle {
    public void drive() {
        startEngine(); // Allowed: subclass access
    }
}
```

### Use Cases:

- Frameworks that expect subclassing.
- Extensible classes with overridable hooks.

---

## 4. _Default_ (Package-Private)

When no modifier is specified. Accessible **only within the same package**.

```java
class Order {
    void calculateTotal() {
        // Package-private method
    }
}
```

### Use Cases:

- Utility classes.
- Internal logic that should not leak outside the package.

---

## Best Practices

| Element             | Suggested Modifier    | Reason                      |
| ------------------- | --------------------- | --------------------------- |
| Fields              | `private`             | Enforces encapsulation      |
| Constants           | `public static final` | Safe to expose              |
| Getters/Setters     | `public`              | External controlled access  |
| Helper Methods      | `private`             | Internal logic              |
| Overridable Methods | `protected`           | Supports inheritance safely |
| Internal APIs       | _(default)_           | Keeps API surface minimal   |

---

## Common Pitfalls

| Pitfall                              | Description                                             |
| ------------------------------------ | ------------------------------------------------------- |
| Using `private` on top-level class   | Not allowed. Use only `public` or no modifier.          |
| Overusing `public`                   | Leaks internal implementation, reduces encapsulation.   |
| Misusing `protected`                 | Encourages subclassing where composition may be better. |
| Confusing `default` with `protected` | Default has no subclass access outside the package.     |

---

## Expert Insights

- **Design for least privilege** — expose only what’s necessary.
- **Use package-private** to separate public API from internal implementation.
- In frameworks (e.g., Spring), using `private` methods may bypass AOP proxies.
- Avoid `protected` fields; prefer `private` with protected accessors.

---

## Summary Table

| Modifier    | Visible To                  | Top-Level Class Allowed? |
| ----------- | --------------------------- | ------------------------ |
| `public`    | All classes in all packages | ✅                       |
| `private`   | Declaring class only        | ❌                       |
| `protected` | Same package + subclasses   | ❌                       |
| _default_   | Same package only           | ✅                       |

---

> “Access control is not just about security — it’s about clarity of design. Make your API intentions explicit.” — Senior Java Architects
