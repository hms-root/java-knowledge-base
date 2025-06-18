# Input & Output

Input and Output (I/O) are fundamental pillars in software development. In Java, these operations enable interaction between a program and the external world, whether through the console, graphical interface, files, network, or databases.

This guide focuses on:

- Console input and output
- Input and output using graphical windows via **Swing**

---

## 📤 Output

### ✅ Console Output (`System.out`)

**Definition:**  
The console is the most basic and direct method for displaying textual information.

```java
System.out.print("Without newline");
System.out.println("With newline");
```

**Example:**

```java
System.out.print("Enter your name: ");
System.out.println("Thank you for using the system.");
```

**Best Practices:**

- Prefer `System.out.println()` for clarity.
- Use `System.out.printf()` for formatted output.

**Common Mistakes:**

- Expecting a newline with `print()` without using `\n`.

---

### ✅ Swing Output (`JOptionPane`)

**Definition:**  
`JOptionPane` allows you to show popup message windows.

```java
import javax.swing.JOptionPane;
JOptionPane.showMessageDialog(null, "Simple message");
```

**Advanced Example:**

```java
JOptionPane.showMessageDialog(null, "Operation successful", "Info", JOptionPane.INFORMATION_MESSAGE);
```

**Best Practices:**

- Use in small or educational applications.
- For real-world apps, prefer architectures with view separation.

---

## 📥 Input

### ✅ Console Input (`Scanner` class)

```java
import java.util.Scanner;
Scanner sc = new Scanner(System.in);
```

**Read different data types:**

```java
String name = sc.nextLine();
int age = sc.nextInt();
double height = sc.nextDouble();
boolean active = sc.nextBoolean();
```

**Full Example:**

```java
System.out.print("Enter age: ");
int age = sc.nextInt();
System.out.println("Entered age: " + age);
```

**Common Mistakes:**

- `InputMismatchException` when entering incorrect types.
- Mixing `nextInt()` with `nextLine()` incorrectly.

**Best Practices:**

- Validate input before conversion.
- Close the `Scanner` with `sc.close()` when done.

---

### ✅ Swing Input (`JOptionPane.showInputDialog`)

```java
String value = JOptionPane.showInputDialog("Enter a number:");
int number = Integer.parseInt(value);
```

**Example with error handling:**

```java
try {
    int age = Integer.parseInt(value);
} catch (NumberFormatException e) {
    JOptionPane.showMessageDialog(null, "Invalid age");
}
```

**Best Practices:**

- Validate the string before converting.
- Handle `NumberFormatException`.

---

## 🔍 Key Differences

| Feature            | Console (`Scanner`) | Swing (`JOptionPane`) |
| ------------------ | ------------------- | --------------------- |
| Interface          | Command line        | Graphical (window)    |
| Returned Type      | Concrete types      | Always `String`       |
| Testability        | High                | Low                   |
| Professional Usage | Common              | Rare in backend       |

---

## 💡 Analogy

> Think of I/O as a kitchen:
>
> - Input = Ingredients you receive
> - Output = Dish you serve
>
> The way ingredients arrive (console, window) and how the dish is served (text, pop-up) may vary, but the "chef" (your business logic) must handle them properly.

---

## 🧭 General Best Practices

- Always validate user input.
- Use `try-catch` for invalid conversions.
- Comment I/O blocks for maintenance.
- Do not mix business logic with I/O logic.
- In real projects, separate I/O into dedicated classes.

---
