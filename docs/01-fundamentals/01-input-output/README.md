# Input and Output

This guide covers how to perform **input and output operations** in Java, both via the **console** and using **Swing dialog windows**. It includes best practices and clear examples aimed at professional, senior-level code quality.

---

## ✅ Console

### 📥 Input using `Scanner`

Use the `Scanner` class to read user input from the console (`System.in`):

```java
import java.util.Scanner;

public class ConsoleInput {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter your name: ");
        String name = scanner.nextLine();

        System.out.print("Enter your age: ");
        int age = scanner.nextInt();

        scanner.close(); // Always close the Scanner when done

        System.out.println("Hello, " + name + ". You are " + age + " years old.");
    }
}
```

**Best Practices:**

- Always close the `Scanner` to free system resources.
- Use `nextLine()` to read full lines of input.
- When mixing `nextInt()` and `nextLine()`, call `nextLine()` after `nextInt()` to consume the leftover newline.

---

### 📤 Output using `System.out`

```java
System.out.print("Hello ");  // no newline
System.out.println("World"); // with newline
System.out.printf("Name: %s | Age: %d%n", "Manuel", 35); // formatted output
```

**Best Practices:**

- Use `printf()` for professional, formatted output.
- Use `System.err.println()` to separate error messages from standard output.

---

## 🪟 Dialogs (Swing)

### 📥 Input using `JOptionPane.showInputDialog()`

```java
import javax.swing.JOptionPane;

public class DialogInput {
    public static void main(String[] args) {
        String name = JOptionPane.showInputDialog("Enter your name:");
        String ageStr = JOptionPane.showInputDialog("Enter your age:");

        int age = Integer.parseInt(ageStr);

        JOptionPane.showMessageDialog(null, "Hello, " + name + ". You are " + age + " years old.");
    }
}
```

⚠️ **Important:** `JOptionPane.showInputDialog()` **always returns a `String`**.

- You must parse the value manually (e.g., `Integer.parseInt(...)`).
- If the user cancels the dialog, it returns `null`.

Example with validation:

```java
try {
    String input = JOptionPane.showInputDialog("Enter a number:");
    int number = Integer.parseInt(input);
    JOptionPane.showMessageDialog(null, "The number is: " + number);
} catch (NumberFormatException e) {
    JOptionPane.showMessageDialog(null, "Invalid number entered.", "Error", JOptionPane.ERROR_MESSAGE);
}
```

---

### 📤 Output using `JOptionPane.showMessageDialog()`

```java
JOptionPane.showMessageDialog(null, "This is a message.");
JOptionPane.showMessageDialog(null, "Error occurred", "Error", JOptionPane.ERROR_MESSAGE);
```

Available message types:

- `INFORMATION_MESSAGE`
- `WARNING_MESSAGE`
- `ERROR_MESSAGE`
- `PLAIN_MESSAGE`

**Best Practices:**

- Use `ERROR_MESSAGE` for errors, `PLAIN_MESSAGE` for neutral messages.
- Always provide a clear and descriptive title for each dialog.

---

## 🧠 Summary Table

| Method       | Input                                      | Output                                |
| ------------ | ------------------------------------------ | ------------------------------------- |
| Console      | `Scanner scanner = new Scanner(System.in)` | `System.out.print / println / printf` |
| Swing Dialog | `JOptionPane.showInputDialog(...)`         | `JOptionPane.showMessageDialog(...)`  |
