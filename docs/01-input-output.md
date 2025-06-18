# Input & Output

## 1. 🔸 Output in Java

### A. 📤 Console Output with `System.out`

#### ✅ Description

`System.out` is a built-in output stream used for printing to the console.

#### ✅ Usage

```java
System.out.print("Hello");       // Without newline
System.out.println("World");     // With newline
System.out.printf("Score: %d%n", 95); // Formatted output
```

#### ✅ Example

```java
System.out.println("Welcome!");
System.out.printf("Port: %d%n", 8080);
```

#### 🟢 Best Practices

- Prefer `printf` for readability.
- Use `println` to ensure proper line breaks.

### B. 📤 GUI Output with `JOptionPane.showMessageDialog`

#### ✅ Description

Displays a graphical message dialog to the user.

#### ✅ Usage

```java
JOptionPane.showMessageDialog(null, "Hello, user!");
```

#### ✅ Example

```java
import javax.swing.JOptionPane;

public class SwingOutput {
    public static void main(String[] args) {
        JOptionPane.showMessageDialog(null, "Operation completed.");
    }
}
```

#### 🟢 Best Practices

- Suitable for small or user-facing desktop apps.
- Avoid in backend or server-side environments.

## 2. 🔸 Input in Java

### A. 📥 Console Input with `Scanner`

#### ✅ Description

The `Scanner` class reads input from the console using `System.in`.

#### ✅ Usage

```java
Scanner scanner = new Scanner(System.in);
String name = scanner.nextLine();
int age = scanner.nextInt();
```

#### ✅ Example

```java
Scanner scanner = new Scanner(System.in);
System.out.print("Enter your name: ");
String name = scanner.nextLine();

System.out.print("Enter your age: ");
int age = scanner.nextInt();
scanner.nextLine(); // Consume the newline

System.out.println("Name: " + name + ", Age: " + age);
scanner.close();
```

#### ⚠️ Important: Mixing `nextInt()` and `nextLine()`

##### ❌ Problem:

Using `nextLine()` after `nextInt()` without consuming the newline causes the next input to be skipped.

##### ✅ Fix:

```java
int age = scanner.nextInt();
scanner.nextLine(); // Discard leftover newline
String name = scanner.nextLine();
```

### B. 📥 GUI Input with `JOptionPane.showInputDialog`

#### ✅ Description

Prompts the user for input using a dialog and returns a `String`.

#### ✅ Example

```java
String input = JOptionPane.showInputDialog("Enter your age:");
if (input != null) {
    try {
        int age = Integer.parseInt(input);
    } catch (NumberFormatException e) {
        JOptionPane.showMessageDialog(null, "Invalid number.");
    }
}
```

## 3. 🔸 Parsing String Input into Primitive Types

| Type      | Parsing Method              | Exception |
| --------- | --------------------------- | --------- |
| `int`     | `Integer.parseInt(str)`     | Yes       |
| `double`  | `Double.parseDouble(str)`   | Yes       |
| `boolean` | `Boolean.parseBoolean(str)` | No        |

## 4. 🔸 Console vs Swing I/O Comparison

| Feature        | Console I/O           | Swing I/O                |
| -------------- | --------------------- | ------------------------ |
| Interface Type | Text-based            | Graphical dialogs        |
| Use Case       | Backend, CLI tools    | Simple desktop GUIs      |
| Input Parsing  | Built-in with Scanner | Manual parsing needed    |
| Portability    | Headless OK           | Requires GUI environment |
| Debugging      | Easier                | More visual              |

## 5. 🔸 Best Practices Summary

- Always close `Scanner` objects.
- Use `try-catch` for input parsing.
- Consume newlines when mixing input methods.
- Avoid GUI dialogs in backend services.
- Validate user input from both console and GUI.

## 6. 🔴 Common Errors and Fixes

| Error                                      | Fix                                         |
| ------------------------------------------ | ------------------------------------------- |
| `nextLine()` after `nextInt()` skips input | Use `scanner.nextLine()` after numeric read |
| Crash on bad number input                  | Wrap parsing in `try-catch`                 |
| `null` input from dialog                   | Check `if (input != null)`                  |
| Using dialogs in server code               | Avoid GUI in backend                        |
