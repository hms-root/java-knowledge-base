# System

This guide explains how to work with system properties, environment variables, and runtime operations in Java.

---

## 🔹 Getting System Properties

Java provides built-in access to many system properties using `System.getProperty()`.

### Example:

```java
String javaVersion = System.getProperty("java.version");
String userHome = System.getProperty("user.home");
String osName = System.getProperty("os.name");

System.out.println("Java: " + javaVersion);
System.out.println("Home: " + userHome);
System.out.println("OS: " + osName);
```

### Common Property Keys:

| Key              | Description                 |
| ---------------- | --------------------------- |
| `java.version`   | Java Runtime version        |
| `os.name`        | Operating system name       |
| `user.name`      | User account name           |
| `user.home`      | User home directory         |
| `user.dir`       | Current working dir         |
| `file.separator` | `/` on Unix, `\` on Windows |

---

## 🔹 Setting Custom System Properties

You can add or change properties using `System.setProperty()`.

```java
System.setProperty("my.config", "debug");
String config = System.getProperty("my.config"); // "debug"
```

🧠 Useful for global app settings like mode, version, or file paths.

---

## 🔹 Passing Properties from Command Line

When launching a Java app, use `-D` to pass properties:

```bash
java -Denv=production -Ddebug=true MyApp
```

In code:

```java
String env = System.getProperty("env");     // "production"
String debug = System.getProperty("debug"); // "true"
```

---

## 🔹 Getting Environment Variables

Use `System.getenv()` to read OS environment variables.

```java
String path = System.getenv("PATH");
String home = System.getenv("HOME"); // or USERPROFILE on Windows

System.out.println("PATH: " + path);
```

⚠️ Environment variables are read-only. You cannot modify them at runtime.

---

## 🔹 Other Useful `System` Methods

```java
System.currentTimeMillis(); // Current time in ms since epoch
System.nanoTime();          // High-resolution time (nanoseconds)
System.exit(0);             // Terminates the JVM (0 = OK)
System.gc();                // Suggests garbage collection (not guaranteed)
```

### Redirect Output Streams

```java
System.setOut(new PrintStream("log.txt"));
System.out.println("This goes to log.txt");
```

---

## 🔹 `Runtime` Class: Execute OS Commands

Use `Runtime.getRuntime()` to run system-level commands.

### Example: Open a file or app

```java
Runtime rt = Runtime.getRuntime();
rt.exec("notepad"); // Windows
```

### Example: Run shell command

```java
Process process = Runtime.getRuntime().exec("ls -l");
```

⚠️ Always handle `IOException`. For full control, use `ProcessBuilder`.

---

## 🟦 Best Practices Summary

- ✅ Use `System.getProperty()` to access JVM and user settings.
- ✅ Use `System.setProperty()` to customize global config.
- ✅ Use `System.getenv()` for environment values (read-only).
- ✅ Use `Runtime.exec()` carefully — handle errors, prefer `ProcessBuilder` in complex cases.
- ✅ Avoid hardcoding paths — read from properties or environment instead.
