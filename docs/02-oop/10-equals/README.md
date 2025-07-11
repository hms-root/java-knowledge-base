# equals()

The `equals()` method in Java is fundamental for comparing objects meaningfully, particularly in object-oriented systems where identity and equivalence often diverge. Understanding and properly overriding `equals()` is essential for writing correct, efficient, and maintainable Java code — especially when working with collections like `HashSet`, `HashMap`, and others that rely on object equality.

---

## 1. `equals()` in `java.lang.Object`

The `Object` class defines the method as:

```java
public boolean equals(Object obj)
```

By default, it compares **references**, not contents:

```java
Object a = new Object();
Object b = new Object();
System.out.println(a.equals(b)); // false
System.out.println(a.equals(a)); // true
```

---

## 2. Overriding `equals()` – The Right Way

### Use Case: A `User` Class

```java
public class User {
    private String username;
    private int age;

    public User(String username, int age) {
        this.username = username;
        this.age = age;
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true; // Reflexive
        if (obj == null || getClass() != obj.getClass()) return false; // Null-safe & Class match
        User other = (User) obj;
        return age == other.age && username.equals(other.username); // Field comparison
    }

    @Override
    public int hashCode() {
        return Objects.hash(username, age);
    }
}
```

---

## 3. The Contract of `equals()`

A robust `equals()` must fulfill **five conditions** (per the Java specification):

1. **Reflexive**: `x.equals(x)` is true.
2. **Symmetric**: `x.equals(y)` is true ⇔ `y.equals(x)` is true.
3. **Transitive**: If `x.equals(y)` and `y.equals(z)`, then `x.equals(z)` must be true.
4. **Consistent**: Repeated calls return same result if no fields change.
5. **Non-null**: `x.equals(null)` is always false.

Failing to follow these rules leads to subtle and critical bugs.

---

## 4. Common Pitfalls

| Pitfall                                        | Explanation                                                                  |
| ---------------------------------------------- | ---------------------------------------------------------------------------- |
| ❌ Not overriding `hashCode()` with `equals()` | Violates the general contract, breaks collections like `HashMap`, `HashSet`. |
| ❌ Using `==` for field comparison             | Only compares references. Use `equals()` for objects.                        |
| ❌ Forgetting `null` checks                    | Leads to `NullPointerException`.                                             |
| ❌ Asymmetric logic                            | Causes unexpected behavior in collections and equality checks.               |

---

## 5. Best Practices for Top-Level Developers

✅ Always override `hashCode()` when overriding `equals()`. Use `Objects.hash(...)` for clean code.

✅ Use `@Override` annotation — it ensures you're actually overriding a superclass method.

✅ Use `getClass()` instead of `instanceof` if strict class equality is required.

✅ Favor immutability for fields involved in equality (e.g., avoid mutable fields like lists/maps unless carefully handled).

✅ Leverage IDE or Lombok (`@EqualsAndHashCode`) when appropriate, but **know what is generated**.

---

## 6. Testing `equals()` Properly

Always write unit tests:

```java
User u1 = new User("john", 30);
User u2 = new User("john", 30);
User u3 = new User("john", 31);

assert u1.equals(u2);       // true
assert !u1.equals(u3);      // false
assert u1.equals(u1);       // reflexivity
assert !u1.equals(null);    // null check
assert !u1.equals("john");  // type check
```

---

## 7. Real-World Implications

- **Collections**: If `equals()` or `hashCode()` are broken, objects may **disappear from sets**, or map lookups may silently fail.

- **ORMs & Databases**: Hibernate and JPA depend on well-defined equality for entity identity.

- **Caching & Performance**: Poor implementations affect lookup speeds and cause memory leaks in caches.

---

## 8. Summary Table

| Rule/Tip                     | Why It Matters                           |
| ---------------------------- | ---------------------------------------- |
| Always override `hashCode()` | Collections integrity                    |
| Null-safe comparisons        | Avoids runtime exceptions                |
| Follow the contract strictly | Prevents logic bugs                      |
| Use `Objects.equals()`       | Simplifies null-safe equality            |
| Use `getClass()` carefully   | Decides between strict vs loose equality |

---

## 9. Final Example (Professional-Level)

```java
public class Product {
    private final String code;
    private final String name;

    public Product(String code, String name) {
        this.code = code;
        this.name = name;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof Product)) return false;
        Product other = (Product) o;
        return Objects.equals(code, other.code); // Assume 'code' is unique
    }

    @Override
    public int hashCode() {
        return Objects.hash(code);
    }
}
```

---
