# Command Line and IntelliJ Arguments

This guide explains how to compile and run Java programs from the command line, how to pass arguments (including special characters and accents), and how to set up arguments in IntelliJ IDEA.

---

## 🔹 Compile and Run Java from Command Line

### ✅ 1. Compile a Java File

```bash
javac MyProgram.java
```

This creates a `MyProgram.class` file.

### ✅ 2. Run the Program

```bash
java MyProgram
```

---

## 🔹 Run with Command-Line Arguments

Arguments are passed after the class name and accessed via `main(String[] args)`.

### ✅ Example:

```java
public class MyProgram {
    public static void main(String[] args) {
        for (String arg : args) {
            System.out.println("Arg: " + arg);
        }
    }
}
```

### ✅ Run:

```bash
java MyProgram hello world 123
```

### ✅ Output:

```
Arg: hello
Arg: world
Arg: 123
```

---

## 🔹 Handling Special Characters and Accents

If your program uses **accents or special symbols**, always:

1. **Save the `.java` file with UTF-8 encoding.**
2. **Use quotes in the terminal** to protect special characters:

```bash
java MyProgram "José" "¡Hola!" "mañana"
```

✅ Works well on Unix/macOS.  
⚠️ On Windows CMD, use `chcp 65001` to enable UTF-8 first.

```bash
chcp 65001
java MyProgram "café" "niño"
```

---

## 🔹 IntelliJ IDEA: Passing Command-Line Arguments (Step-by-Step)

### ✅ Step-by-Step:

1. Open your Java class with `main`.
2. Click the dropdown next to the green **Run** button (top-right).
3. Select **Edit Configurations**.
4. In the **Run/Debug Configurations** window:
   - Select your class on the left.
   - In the **Program arguments** field, type the arguments (space-separated), e.g.:
     ```
     hola mundo 123 "con acento"
     ```
5. Click **Apply**, then **OK**.
6. Run the program — `args[]` will contain those values.

---

## 🟦 Best Practices Summary

- ✅ Always wrap multi-word or accented arguments in quotes.
- ✅ Use UTF-8 for source files and terminal encoding.
- ✅ Use `args.length` to check how many arguments were passed.
- ✅ IntelliJ makes it easy to test different sets of arguments via configuration.
