# Programming Paradigms

Programming paradigms are fundamental styles or approaches to programming that influence how developers design, structure, and write code. Understanding paradigms is crucial for mastering Object-Oriented Programming (OOP), as it allows developers to appreciate OOP in the broader context of software engineering.

---

## 📚 Key Programming Paradigms

### 1. Imperative Programming

- **Definition**: A paradigm based on explicitly instructing the computer _how_ to perform tasks.
- **Main idea**: Code is a sequence of statements that change a program's state.
- **Example (Java)**:

```java
int sum = 0;
for (int i = 0; i <= 10; i++) {
    sum += i;
}
System.out.println("Sum: " + sum);
```

### 2. Declarative Programming

- **Definition**: Focuses on _what_ the program should accomplish, rather than how.
- **Used in**: SQL, functional programming, HTML, etc.
- **Example (SQL-like pseudocode)**:

```sql
SELECT SUM(value) FROM numbers;
```

---

### 3. Functional Programming

- **Definition**: Emphasizes the use of pure functions and immutability.
- **Key traits**: No side effects, first-class functions, higher-order functions.
- **Example (Java with Streams)**:

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
int sum = numbers.stream().reduce(0, Integer::sum);
System.out.println("Sum: " + sum);
```

---

### 4. Object-Oriented Programming (OOP)

- **Definition**: Models software as a collection of interacting objects.
- **Core principles**:
  - **Encapsulation**
  - **Abstraction**
  - **Inheritance**
  - **Polymorphism**
- **Example**:

```java
class Animal {
    void speak() {
        System.out.println("Some sound");
    }
}

class Dog extends Animal {
    @Override
    void speak() {
        System.out.println("Bark");
    }
}

Animal dog = new Dog();
dog.speak();  // Output: Bark
```

---

### 5. Procedural Programming

- **Definition**: A subtype of imperative programming that uses procedures/functions to organize code.
- **Often used in**: C, Pascal, early Java.
- **Example**:

```java
public static int add(int a, int b) {
    return a + b;
}
```

---

### 6. Logic Programming

- **Definition**: Programs are written as a set of logical statements, and execution involves queries against these statements.
- **Used in**: Prolog, CLIPS.
- **Concept**: Describe _facts_ and _rules_, let the system infer results.

---

## 🔍 Why Paradigms Matter

- Understanding paradigms helps developers choose the right tool and approach for each problem.
- Mastery of paradigms increases code readability, testability, and scalability.

---

## ✅ Best Practices

- **Know when to use OOP vs Functional vs Procedural styles.**
- **Mix paradigms thoughtfully** (e.g., functional style inside OOP code via Java Streams).
- **Don’t force OOP when a procedural or functional approach is more natural.**

---

## ⚠️ Common Pitfalls

| Pitfall              | Description                                                      |
| -------------------- | ---------------------------------------------------------------- |
| Overusing OOP        | Creating too many classes/abstractions without clear need.       |
| Ignoring paradigms   | Writing "spaghetti code" by mixing styles incoherently.          |
| Misusing inheritance | Violating Liskov Substitution Principle by improper subclassing. |

---

## 🎯 Professional Insights

- Top-tier developers **understand trade-offs** between paradigms and apply them pragmatically.
- Use paradigms not as dogma, but as **powerful tools** to enhance code quality and maintainability.

---

## 📌 Summary Table

| Paradigm    | Key Trait              | Common Use Case                     |
| ----------- | ---------------------- | ----------------------------------- |
| Imperative  | Step-by-step logic     | Low-level control, performance code |
| Declarative | Focus on what, not how | Queries, UI layout                  |
| Functional  | Pure functions         | Data pipelines, parallelism         |
| OOP         | Objects and classes    | Enterprise apps, modeling systems   |
| Procedural  | Functions/procedures   | Simple apps, embedded systems       |
| Logic       | Rules & inference      | AI, rule-based systems              |

---
