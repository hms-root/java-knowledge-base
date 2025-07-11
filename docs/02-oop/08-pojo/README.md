# POJO

POJO stands for **Plain Old Java Object**. It refers to a simple Java class that adheres to a few specific conventions and serves as a fundamental building block in many Java-based enterprise and backend systems.

A POJO is a Java object that does **not**:

- Extend or implement any specialized classes/interfaces (like `EJB`, `Serializable`, `Remote`, etc.).
- Contain business logic or behavior tied to any framework.

Instead, it:

- Encapsulates data.
- Provides getter/setter methods for accessing fields.
- May override `equals()`, `hashCode()`, and `toString()` as needed.

---

## Characteristics of a POJO

- No special restrictions other than those forced by the Java Language Specification.
- Uses private fields and public getter/setter methods.
- May include constructors.
- May override methods like `equals`, `hashCode`, and `toString` for value comparison and debugging.

---

## Example: A Typical POJO

```java
public class Product {
    private String name;
    private double price;
    private int quantity;

    public Product() {
        // Default constructor
    }

    public Product(String name, double price, int quantity) {
        this.name = name;
        this.price = price;
        this.quantity = quantity;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public double getPrice() {
        return price;
    }

    public void setPrice(double price) {
        this.price = price;
    }

    public int getQuantity() {
        return quantity;
    }

    public void setQuantity(int quantity) {
        this.quantity = quantity;
    }

    @Override
    public String toString() {
        return "Product{name='" + name + "', price=" + price + ", quantity=" + quantity + "}";
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof Product)) return false;
        Product product = (Product) o;
        return Double.compare(product.price, price) == 0 &&
               quantity == product.quantity &&
               name.equals(product.name);
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, price, quantity);
    }
}
```

---

## Use Cases

- **Data Transfer Objects (DTOs)**: POJOs are commonly used to transfer data between layers (e.g., controller to service).
- **ORM (Object-Relational Mapping)**: POJOs are the foundation of entity classes in frameworks like Hibernate or JPA.
- **Configuration Models**: Represent structured config in Spring Boot (`@ConfigurationProperties`).
- **API Models**: Serve as request/response bodies in RESTful APIs.

---

## Best Practices

### ✅ Follow JavaBeans Naming Convention

Always use `getX` and `setX` naming for consistency with libraries and frameworks.

### ✅ Ensure Immutability When Appropriate

Use final fields and omit setters for immutable objects.

```java
public class ImmutableUser {
    private final String username;
    private final String email;

    public ImmutableUser(String username, String email) {
        this.username = username;
        this.email = email;
    }

    public String getUsername() {
        return username;
    }

    public String getEmail() {
        return email;
    }
}
```

### ✅ Override `equals()` and `hashCode()` Properly

Essential for correct behavior in collections and caching.

### ✅ Use `@Override` Annotation

Helps catch mistakes at compile time.

---

## Common Pitfalls

### ❌ Adding Business Logic

Keep POJOs simple. Avoid service logic inside POJOs.

### ❌ Breaking Encapsulation

Avoid public fields — always use private fields with accessors.

### ❌ Overriding Only `equals()` Without `hashCode()`

Violates the general contract of `hashCode`, leading to issues in hash-based collections.

---

## Professional Tips

- **Java Records (Java 14+)** offer a concise alternative to POJOs for immutable data carriers.
- **Use Lombok** to reduce boilerplate in large models, but understand what it generates.
- **Serialization Concerns**: If a POJO must be serialized (e.g., in distributed systems), ensure it implements `Serializable` and follows best practices for versioning.
- **Thread Safety**: Immutable POJOs are naturally thread-safe. Mutable POJOs require defensive copying or synchronization if accessed concurrently.

---
