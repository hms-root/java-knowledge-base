# Date

This guide explains how to work with dates in Java using the legacy classes: `Date`, `SimpleDateFormat`, and `Calendar`, along with the most common operations.

---

## 🔹 `Date` Class (java.util.Date)

Represents a specific moment in time.

### Common Methods:

```java
Date now = new Date();

now.getTime();        // Returns milliseconds since Jan 1, 1970
now.toString();       // Converts date to string
now.after(otherDate); // true if after otherDate
now.before(otherDate);// true if before otherDate
```

⚠️ Most `Date` methods are deprecated. Use it mainly to represent timestamps, not manipulate dates.

---

## 🔹 `SimpleDateFormat` (java.text.SimpleDateFormat)

Used to format and parse dates into strings.

### Example: Format Date to String

```java
Date now = new Date();
SimpleDateFormat sdf = new SimpleDateFormat("dd/MM/yyyy");
String formatted = sdf.format(now);
System.out.println(formatted); // e.g. "25/06/2025"
```

### Example: Parse String to Date

```java
String dateStr = "15-06-2025";
SimpleDateFormat sdf = new SimpleDateFormat("dd-MM-yyyy");
Date date = sdf.parse(dateStr);
```

### Most Common Patterns:

| Pattern | Meaning             | Example |
| ------- | ------------------- | ------- |
| `dd`    | Day (2 digits)      | 05      |
| `MM`    | Month (2 digits)    | 06      |
| `yyyy`  | Year (4 digits)     | 2025    |
| `HH`    | Hour (24h)          | 14      |
| `mm`    | Minute              | 30      |
| `ss`    | Seconds             | 45      |
| `EEE`   | Day of week (short) | Tue     |
| `MMMM`  | Full month name     | June    |

🧠 Use `format(Date)` and `parse(String)` for conversions.

---

## 🔹 `Calendar` Class (java.util.Calendar)

Used to manipulate date/time values (add, subtract, set fields).

### Create Calendar Instance:

```java
Calendar cal = Calendar.getInstance();
```

### Common Methods:

```java
int year = cal.get(Calendar.YEAR);
int month = cal.get(Calendar.MONTH); // 0-based: Jan = 0
int day = cal.get(Calendar.DAY_OF_MONTH);

cal.set(Calendar.YEAR, 2026); // Change year
cal.add(Calendar.DAY_OF_MONTH, 5); // Add 5 days
Date date = cal.getTime(); // Convert to Date
```

✅ More powerful than `Date` for date math.  
❌ Verbose and replaced by `java.time` in modern Java.

---

## 🔹 Comparing Dates

```java
Date d1 = new SimpleDateFormat("dd/MM/yyyy").parse("01/06/2025");
Date d2 = new SimpleDateFormat("dd/MM/yyyy").parse("15/06/2025");

boolean isBefore = d1.before(d2); // true
boolean isAfter = d1.after(d2);   // false
boolean isEqual = d1.equals(d2);  // false
```

🧠 You can also compare using `getTime()`:

```java
if (d1.getTime() < d2.getTime()) {
    System.out.println("d1 is before d2");
}
```

---

## 🟦 Best Practices Summary

- ✅ Use `SimpleDateFormat` to format/parse strings with `Date`.
- ✅ Use `Calendar` to add/subtract time from dates.
- ✅ Always check if months are 0-based when using `Calendar`.
- ✅ Compare dates with `.before()`, `.after()` or `.getTime()`.
- ⚠️ Consider using `java.time` (Java 8+) in new projects for cleaner code.
