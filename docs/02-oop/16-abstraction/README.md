# Abstraction

**Abstraction** is a core pillar of Object-Oriented Programming (OOP). It refers to the process of hiding the internal implementation details of a system and exposing only the necessary parts to the user. In Java, abstraction is achieved primarily through **abstract classes** and **interfaces**.

Abstraction is not only a tool for hiding complexity, but also a design principle that enables **decoupling**, **modularity**, **testability**, and **long-term maintainability**.

---

## Goals of Abstraction

- Hide implementation complexity
- Expose essential behavior only
- Enable scalability and maintainability
- Facilitate testing and mocking
- Support the Open/Closed Principle (OCP) from SOLID

---

## Real-World Analogy

Think of a **coffee machine**: as a user, you press a button to get coffee. You don’t need to know how the water is heated or how the pressure is managed — that’s abstracted away.

---

## Abstraction in Java

### 1. Using Abstract Classes

```java
// Abstract class defining the abstraction
public abstract class PaymentProcessor {
    public abstract void processPayment(double amount);

    public void validateAmount(double amount) {
        if (amount <= 0) {
            throw new IllegalArgumentException("Invalid payment amount.");
        }
    }
}

// Concrete implementation
public class CreditCardProcessor extends PaymentProcessor {
    @Override
    public void processPayment(double amount) {
        validateAmount(amount);
        System.out.println("Processing credit card payment of $" + amount);
    }
}
```

### 2. Using Interfaces

```java
// Interface defining contract
public interface ReportGenerator {
    void generateSummary();
    void export(String format);
}

// Implementation
public class PDFReportGenerator implements ReportGenerator {
    @Override
    public void generateSummary() {
        System.out.println("Generating PDF summary...");
    }

    @Override
    public void export(String format) {
        System.out.println("Exporting PDF in format: " + format);
    }
}
```

---

## Best Practices

- **Design for abstraction early**: Design your system in terms of abstract behaviors, not concrete classes.
- **Use interfaces for behavior, abstract classes for partial implementations.**
- **Favor composition over inheritance**: Abstract behavior should often be shared via interfaces and composed, not inherited blindly.
- **Name wisely**: Abstractions should be named after what they do, not how they do it. E.g., `NotificationService`, not `EmailSender`.

---

## Common Pitfalls

- **Leaky abstractions**: When implementation details leak into the abstraction. E.g., exposing database queries in service interfaces.
- **Over-abstraction**: Creating too many layers without real need, making systems harder to navigate and debug.
- **Inflexible design**: Tying abstract classes to specific business rules, violating OCP.

---

## Advanced Notes

- **Abstract classes** can have constructors, fields, and default method implementations.
- **Interfaces (Java 8+)** can also have `default` and `static` methods.
- Use abstraction to isolate **domain logic** from **infrastructure** (e.g., using interfaces for persistence logic to allow mocking in tests).

---

## Interview-Ready Insight

- Describe abstraction not only as a language feature but as a **design mindset**.
- Explain how you’ve used abstraction to **improve code reuse**, **replace dependencies**, or **test components independently**.
- Be prepared to show how abstract contracts helped evolve a system over time without breaking existing implementations.

---

## Summary

| Aspect               | Abstract Class      | Interface                 |
| -------------------- | ------------------- | ------------------------- |
| Purpose              | Partial abstraction | Full abstraction          |
| Multiple inheritance | Not supported       | Supported                 |
| Constructors         | Yes                 | No                        |
| Fields               | Yes                 | Static final only         |
| Method types         | Abstract, concrete  | Abstract, default, static |

Abstraction is **not just about hiding code**, but about **exposing clean and stable APIs**, enabling systems to evolve safely.
