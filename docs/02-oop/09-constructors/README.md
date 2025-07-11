# Constructors

Constructors are special methods used to initialize objects. Unlike regular methods, constructors are invoked **automatically** when an object is created using the `new` keyword. They serve as the **entry point for object configuration**, ensuring each instance begins life in a valid state.

---

## What is a Constructor?

A constructor in Java is a block of code that is **automatically invoked** when a new object is created.

### Syntax

```java
class ClassName {
    ClassName() {
        // constructor body
    }
}
```

### Key Rules

- Must have the same name as the class.
- Cannot have a return type (not even `void`).
- Can be overloaded.
- Can call another constructor using `this(...)`.

---

## No-Argument Constructors

This constructor takes no parameters. It's used to initialize default values.

### Example:

```java
public class User {
    private String name;
    private int age;

    public User() {
        this.name = "Unknown";
        this.age = 0;
    }
}
```

### Usage:

```java
User u = new User(); // name = "Unknown", age = 0
```

---

## Parameterized Constructors

Parameterized constructors allow the instantiation of objects with custom initial values.

### Example:

```java
public class User {
    private String name;
    private int age;

    public User(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

### Usage:

```java
User u = new User("Alice", 30);
```

---

## Constructor Overloading

You can define multiple constructors with different parameter lists. This is known as **constructor overloading** and supports flexible object creation.

### Example:

```java
public class User {
    private String name;
    private int age;

    public User() {
        this("Unknown", 0); // delegate to another constructor
    }

    public User(String name) {
        this(name, 0); // partial initialization
    }

    public User(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

---

## Constructor Chaining (Calling Another Constructor)

Java allows you to call one constructor from another in the same class using `this(...)`. This avoids code duplication.

### Example:

```java
public class Product {
    private String name;
    private double price;
    private String currency;

    public Product(String name) {
        this(name, 0.0, "USD");
    }

    public Product(String name, double price) {
        this(name, price, "USD");
    }

    public Product(String name, double price, String currency) {
        this.name = name;
        this.price = price;
        this.currency = currency;
    }
}
```

---

## Best Practices

✅ **Use constructor overloading to provide multiple levels of initialization.**  
✅ **Use constructor chaining (`this(...)`) to avoid code duplication.**  
✅ **Validate inputs inside constructors to ensure consistent object state.**  
✅ **Make constructors explicit and easy to understand.**

### Example:

```java
public class Account {
    private String id;
    private double balance;

    public Account(String id, double balance) {
        if (id == null || id.isEmpty()) {
            throw new IllegalArgumentException("Account ID cannot be null or empty.");
        }
        if (balance < 0) {
            throw new IllegalArgumentException("Initial balance cannot be negative.");
        }
        this.id = id;
        this.balance = balance;
    }
}
```

---

## 7. Common Pitfalls

❌ **Calling another constructor after using `this.variable = value;`**

```java
public class Faulty {
    public Faulty() {
        // ❌ this call must be first
        System.out.println("Init");
        this("Error"); // COMPILATION ERROR
    }

    public Faulty(String msg) {
        System.out.println(msg);
    }
}
```

✅ Correct way:

```java
public class Correct {
    public Correct() {
        this("Safe"); // this must be the FIRST statement
    }

    public Correct(String msg) {
        System.out.println(msg);
    }
}
```

❌ **Code duplication across constructors instead of using `this(...)`.**  
❌ **Silent failure due to default constructor not being explicitly defined.**

---
