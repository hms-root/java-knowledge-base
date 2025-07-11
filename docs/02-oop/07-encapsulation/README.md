# Attribute Hiding Principle: Getters and Setters

Attribute hiding (also called **encapsulation**) is a foundational principle in Object-Oriented Programming (OOP). It aims to **restrict direct access to internal object data (fields/attributes)** and expose it only through controlled interfaces, typically using **getters and setters**.

This principle ensures that:

- Objects maintain control over their internal state.
- Unintended or invalid modifications are prevented.
- The internal implementation can change without breaking external code.

---

## 1. Technical Explanation

### Encapsulation in Java

In Java, fields are typically marked as `private` to prevent external access. Public **getter** and **setter** methods are then provided to allow controlled access and modification.

```java
public class User {
    private String name;  // Hidden attribute
    private int age;

    // Getter for name
    public String getName() {
        return name;
    }

    // Setter for name
    public void setName(String name) {
        if (name == null || name.isBlank()) {
            throw new IllegalArgumentException("Name cannot be null or blank.");
        }
        this.name = name;
    }

    // Getter for age
    public int getAge() {
        return age;
    }

    // Setter for age
    public void setAge(int age) {
        if (age < 0 || age > 150) {
            throw new IllegalArgumentException("Age must be between 0 and 150.");
        }
        this.age = age;
    }
}
```

In this example:

- Direct access to `name` and `age` is prohibited.
- Validation logic ensures state integrity.
- Behavior can evolve without exposing internal changes.

---

## 2. Why Use Getters and Setters?

### Benefits

| Feature         | Explanation                                                 |
| --------------- | ----------------------------------------------------------- |
| **Control**     | Centralize logic that validates or transforms data.         |
| **Security**    | Prevent unintended external interference.                   |
| **Flexibility** | Underlying representation can change without breaking APIs. |
| **Abstraction** | Encapsulation hides implementation details.                 |

### Example: Internal Refactor Without Breaking API

```java
// Original
private int age;

// New internal representation
private LocalDate birthDate;

public int getAge() {
    return Period.between(birthDate, LocalDate.now()).getYears();
}
```

Consumers still use `getAge()` — no external code needs to change.

---

## 3. Best Practices

### ✅ DO

- Validate data in setters to maintain invariants.
- Expose only necessary fields through getters/setters.
- Keep setters private when immutability or limited access is desired.
- Use meaningful names (`getFullName()` instead of `getName()` if needed).
- Prefer immutability for value objects when applicable.

### ❌ AVOID

- Making fields public (breaks encapsulation).
- Providing both getter and setter without need (use case must justify access).
- Writing boilerplate without logic — consider records or Lombok for POJOs.
- Allowing inconsistent state through unvalidated setters.

---

## 4. Advanced Patterns

### Immutability Pattern

```java
public final class ImmutableUser {
    private final String name;
    private final int age;

    public ImmutableUser(String name, int age) {
        if (name == null || name.isBlank() || age < 0) {
            throw new IllegalArgumentException("Invalid arguments.");
        }
        this.name = name;
        this.age = age;
    }

    public String getName() { return name; }
    public int getAge() { return age; }
}
```

- No setters = Immutable object.
- Promotes thread-safety and predictability.

### Lazy Initialization in Getters

```java
private List<String> logs;

public List<String> getLogs() {
    if (logs == null) {
        logs = new ArrayList<>();
    }
    return logs;
}
```

- Saves memory by delaying creation until needed.

---

## 5. Common Pitfalls

### 1. Leaking References

```java
private List<String> tags;

public List<String> getTags() {
    return tags; // ❌ returns internal list
}
```

This allows external modification:

```java
user.getTags().add("hacked");
```

**✅ Solution: Return a copy or unmodifiable list:**

```java
return Collections.unmodifiableList(tags);
```

### 2. Overexposing Setters

Setters should not always be public. Control mutability.

```java
public class Config {
    private final String environment;

    public Config(String environment) {
        this.environment = environment;
    }

    public String getEnvironment() {
        return environment;
    }
}
```

---

## 6. Summary

| Principle         | Application                                   |
| ----------------- | --------------------------------------------- |
| **Encapsulation** | Protects internal state.                      |
| **Getters**       | Expose state safely.                          |
| **Setters**       | Modify state with validation.                 |
| **Immutability**  | No setters, only constructors + final fields. |
| **Security**      | Prevent invalid/inconsistent object state.    |

---

## 7. Pro Tips

- **Use constructor injection** for required fields.
- **Avoid exposing mutable internal structures.**
- **Group related setters/getters** logically to improve code readability.
- **Document expected behavior and validation logic** clearly in setters.

---
