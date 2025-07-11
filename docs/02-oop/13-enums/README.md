# Enums

Enums in Java (`enum` keyword) are a powerful and type-safe mechanism for representing a fixed set of constants. However, beyond simple constants, enums in Java can encapsulate fields, methods, and implement interfaces—offering many features useful in advanced backend systems.

This guide will explain enums in a structured and deep way, including constructors, parameters, usage of getters, `toString()`, and common best practices.

---

## 🧱 Definition

An `enum` in Java is a special Java type used to define collections of constants. Unlike simple `public static final` constants, enums are actual class types with the ability to have fields, methods, and constructors.

```java
public enum Status {
    PENDING,
    APPROVED,
    REJECTED
}
```

---

## 🔧 Constructors in Enums

Enums can have constructors, but they are always `private` or package-private (implicitly private). These constructors are used to assign custom values to enum constants.

```java
public enum OrderStatus {
    NEW("New Order", 1),
    PROCESSING("Being Processed", 2),
    SHIPPED("Order Shipped", 3),
    DELIVERED("Delivered to Client", 4);

    private final String label;
    private final int code;

    // Constructor
    OrderStatus(String label, int code) {
        this.label = label;
        this.code = code;
    }

    // Getters
    public String getLabel() {
        return label;
    }

    public int getCode() {
        return code;
    }
}
```

Each enum value calls the constructor like: `NEW("New Order", 1)`.

---

## 📦 Multiple Parameters in Enums

Enums can accept multiple parameters of various types, just like a regular class.

```java
public enum HttpStatus {
    OK(200, "Success"),
    NOT_FOUND(404, "Not Found"),
    INTERNAL_ERROR(500, "Internal Server Error");

    private final int code;
    private final String description;

    HttpStatus(int code, String description) {
        this.code = code;
        this.description = description;
    }

    public int getCode() {
        return code;
    }

    public String getDescription() {
        return description;
    }
}
```

This is particularly useful in backends that handle API responses or error handling.

---

## 📤 When to Use Getters

Use getters when:

- You need to access internal values stored in enum fields.
- You want to expose values in a type-safe, encapsulated way.
- You want to use the values outside the enum (e.g., for database mapping, UI, logs, APIs).

```java
System.out.println(OrderStatus.NEW.getLabel()); // Output: New Order
```

**Best Practice:** Always keep enum fields `private final` and expose them with `getters` instead of making them public.

---

## 🧾 When to Override `toString()`

Override `toString()` when:

- You want a custom string representation (e.g., for logging, UI, JSON).
- You don't want to expose raw enum names (`name()`), which might be less readable or subject to change.

```java
@Override
public String toString() {
    return label + " (" + code + ")";
}
```

**Usage Example:**

```java
System.out.println(OrderStatus.SHIPPED); // Output: Order Shipped (3)
```

---

## ✅ Best Practices

- **Immutable Fields:** Always use `private final` for enum fields.
- **Avoid Public Fields:** Never expose fields directly.
- **Use Getters for Mapping:** Use getters when mapping enums to DB values or external formats.
- **toString vs name():** Use `toString()` for readable output. Use `name()` only when you need the exact declared enum constant.
- **Switch Statements:** Prefer `switch` on enums when handling behavior for each value explicitly.
- **EnumSet and EnumMap:** Use these for optimal performance and clarity over regular collections.

---

## ⚠️ Common Pitfalls

- **Mutable State:** Don’t add mutable fields to enums—enums are meant to be constant and shared.
- **Confusing name() vs toString():** `name()` returns the literal enum constant name, `toString()` can be overridden for a custom string.
- **Serialization Issues:** If using enums across systems (e.g., JSON), ensure that your serialization strategy uses safe values (usually `name()` or a custom getter).

---

## 🧠 Professional Insight

Enums aren't just constants—they're **type-safe classes**. You can:

- Use interfaces with enums.
- Add abstract methods in enums with constant-specific implementations.
- Replace verbose switch/case logic with polymorphic enum behaviors.

### Example: Abstract Method per Constant

```java
public enum Operation {
    ADD {
        public double apply(double x, double y) { return x + y; }
    },
    SUBTRACT {
        public double apply(double x, double y) { return x - y; }
    };

    public abstract double apply(double x, double y);
}
```

This avoids complex conditionals and embraces OOP polymorphism.

---

## 🧪 Final Example: Full Enum in Action

```java
public enum PaymentStatus {
    PENDING("Pending Approval", false),
    COMPLETED("Payment Completed", true),
    FAILED("Transaction Failed", false);

    private final String message;
    private final boolean successful;

    PaymentStatus(String message, boolean successful) {
        this.message = message;
        this.successful = successful;
    }

    public String getMessage() {
        return message;
    }

    public boolean isSuccessful() {
        return successful;
    }

    @Override
    public String toString() {
        return message + " (Success: " + successful + ")";
    }
}
```

---

## 📌 Summary

| Feature         | Recommendation                           |
| --------------- | ---------------------------------------- |
| Fields          | Use `private final`, never public        |
| Getters         | Always use for external access           |
| `toString()`    | Override for human-readable output       |
| Constructors    | Private, used for initializing constants |
| Multiple Params | Fully supported                          |
| Advanced Use    | Abstract methods, interfaces             |

Enums are more than constants—they are **first-class objects** and can be powerful tools in clean, safe, and maintainable backend systems.
