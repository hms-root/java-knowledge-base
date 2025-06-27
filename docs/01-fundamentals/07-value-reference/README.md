# Pass-by-Value vs Pass-by-Reference

This guide explains how Java handles method arguments in the simplest way possible.

---

## 🔹 Java Always Passes by Value

Java **always** passes arguments **by value**.  
That means Java **copies** the variable and sends that copy to the method.

There are two cases:

---

## ✅ Case 1: Primitive Types (int, double, etc.)

Primitives hold real values. When you pass a primitive to a method, Java sends a **copy of that value**.

```java
void change(int x) {
    x = 10;
}

int a = 5;
change(a);
System.out.println(a); // Output: 5
```

🔍 Why?  
Because `x` is just a **copy** of `a`. Changing `x` does **not** change `a`.

---

## ✅ Case 2: Objects (e.g., String, Array, Class)

Objects are stored by reference (like an address).  
Java still sends a **copy**, but this time it's a **copy of the reference** (address).

```java
class Person {
    String name;
}

void rename(Person p) {
    p.name = "Alice";
}

Person person = new Person();
person.name = "Bob";
rename(person);
System.out.println(person.name); // Output: Alice
```

🔍 Why?  
You copied the reference (address) to `person`. Both `person` and `p` point to the **same object**, so changes are visible.

---

## ⚠️ Changing the Reference Inside a Method

If you try to make the object point to **a new object**, it won't work outside the method.

```java
void reset(Person p) {
    p = new Person();   // p now points to a new object
    p.name = "Charlie";
}

Person person = new Person();
person.name = "Bob";
reset(person);
System.out.println(person.name); // Output: Bob
```

🔍 Why?  
Only the **copy of the reference** changed. The original reference stayed the same.

---

## 🧠 Simple Analogy

- Think of an object as a **house**.
- A reference is the **address** of that house.
- You give someone a **copy** of the address.
- They can **change things inside** the house, but if they **move to a new house**, your original address is **unchanged**.

---

## 🟦 Best Practices Summary

- ✅ Java passes **copies** of variables to methods.
- ✅ For primitives: the value is copied, no effect outside.
- ✅ For objects: the **reference** is copied, so internal changes affect the original.
- ❌ You cannot change which object the original variable points to inside a method.
