# 🔍 Search Algorithms: Linear and Binary Search

## 📘 Introduction

Searching is a fundamental operation in software development. It involves finding the **position of a target element** in a collection (e.g., array, list). The two most common basic search algorithms are:

- **Linear Search**: Sequentially checks each element.
- **Binary Search**: Efficiently finds the element in a **sorted** array by dividing the search interval.

Mastering these is essential for any backend developer dealing with data structures, algorithms, APIs, databases, or low-level system behavior.

---

## 🔎 1. Linear Search

### ✅ Concept

Linear Search scans each element **from start to end**, comparing each with the target. It does **not require sorting**.

### 📈 Time & Space Complexity

| Case                 | Time Complexity | Space Complexity |
| -------------------- | --------------- | ---------------- |
| Best (first element) | O(1)            | O(1)             |
| Average              | O(n)            | O(1)             |
| Worst (last/missing) | O(n)            | O(1)             |

### ✅ Use Cases

- Unsorted or small datasets.
- Linked lists or non-random-access structures.
- When the cost of sorting outweighs the benefit of faster search.

### 🧠 Key Insights

- Works on **any collection** (arrays, lists, etc.).
- Easy to implement and debug.
- Not efficient for large datasets.

### 💡 Code Example: Linear Search in Java

```java
public class LinearSearch {
    public static int linearSearch(int[] arr, int target) {
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == target) {
                return i;
            }
        }
        return -1;
    }

    public static void main(String[] args) {
        int[] numbers = {4, 2, 5, 8, 1, 9, 3};
        int target = 8;

        int index = linearSearch(numbers, target);

        if (index != -1) {
            System.out.println("Target found at index: " + index);
        } else {
            System.out.println("Target not found.");
        }
    }
}
```

---

## 🔍 2. Binary Search

### ✅ Concept

Binary Search only works on **sorted** data. It repeatedly **divides the search range in half** and compares the middle element with the target.

### 📈 Time & Space Complexity

| Case    | Time Complexity | Space (Iterative) | Space (Recursive) |
| ------- | --------------- | ----------------- | ----------------- |
| Best    | O(1)            | O(1)              | O(log n)          |
| Average | O(log n)        | O(1)              | O(log n)          |
| Worst   | O(log n)        | O(1)              | O(log n)          |

### ✅ Use Cases

- Large, sorted datasets.
- Optimizing response time in systems with frequent queries.
- Searching in sorted files, indexes, memory pages, etc.

### ⚠️ Constraints

- Requires a **sorted** array.
- Must avoid integer overflow when calculating the midpoint.

### 🧠 Key Insights

- Often implemented iteratively for space efficiency.
- Safe midpoint calculation: `mid = low + (high - low) / 2`
- Faster than linear search for large datasets.

### 💡 Code Example: Binary Search (Iterative)

```java
public class BinarySearch {
    public static int binarySearch(int[] arr, int target) {
        int low = 0;
        int high = arr.length - 1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (arr[mid] == target) {
                return mid;
            } else if (arr[mid] < target) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }

        return -1;
    }

    public static void main(String[] args) {
        int[] numbers = {1, 3, 5, 7, 9, 11, 15};
        int target = 7;

        int index = binarySearch(numbers, target);

        if (index != -1) {
            System.out.println("Target found at index: " + index);
        } else {
            System.out.println("Target not found.");
        }
    }
}
```

### 💡 Code Example: Binary Search (Recursive)

```java
public class RecursiveBinarySearch {
    public static int binarySearch(int[] arr, int low, int high, int target) {
        if (low > high) return -1;

        int mid = low + (high - low) / 2;

        if (arr[mid] == target) return mid;
        else if (arr[mid] < target) return binarySearch(arr, mid + 1, high, target);
        else return binarySearch(arr, low, mid - 1, target);
    }

    public static void main(String[] args) {
        int[] sortedArray = {2, 4, 6, 8, 10, 12};
        int target = 10;

        int result = binarySearch(sortedArray, 0, sortedArray.length - 1, target);

        if (result != -1) {
            System.out.println("Found at index: " + result);
        } else {
            System.out.println("Not found.");
        }
    }
}
```

---

## 🔁 Comparison Table

| Feature                  | Linear Search  | Binary Search            |
| ------------------------ | -------------- | ------------------------ |
| Requires Sorted Data     | ❌ No          | ✅ Yes                   |
| Time (Worst Case)        | O(n)           | O(log n)                 |
| Simplicity               | ✅ Very Simple | ⚠️ Slightly Complex      |
| Data Size Recommendation | Small datasets | Medium to Large datasets |
| Performance              | Slower         | Much Faster              |

---

## 🧪 Test Scenarios & Edge Cases

| Scenario             | Result in Linear | Result in Binary                 |
| -------------------- | ---------------- | -------------------------------- |
| Target at beginning  | Fast             | May take time                    |
| Target at end        | Slow             | Fast (if sorted)                 |
| Target not present   | Full scan        | Log steps                        |
| Array is empty       | Return -1        | Return -1                        |
| Multiple occurrences | First match      | Any match (not guaranteed first) |

---

## 🛠 Tips for Backend Developers

- Use `Arrays.binarySearch()` if you don’t want to reimplement.
- Always validate sorting before applying binary search in production.
- Binary search is fundamental in databases (indexing), API pagination, time series analysis, etc.
- Benchmark both methods in real-world scenarios.
- Combine with custom comparator for advanced objects.

---

## 🚀 Advanced: Binary Search on Custom Objects

```java
import java.util.*;

class Product {
    String name;
    int price;

    Product(String name, int price) {
        this.name = name;
        this.price = price;
    }
}

public class CustomBinarySearch {
    public static void main(String[] args) {
        List<Product> products = new ArrayList<>(List.of(
            new Product("Coffee", 300),
            new Product("Honey", 400),
            new Product("Tea", 500)
        ));

        products.sort(Comparator.comparingInt(p -> p.price));

        int index = Collections.binarySearch(products, new Product("", 400), Comparator.comparingInt(p -> p.price));

        if (index >= 0) {
            System.out.println("Found: " + products.get(index).name);
        } else {
            System.out.println("Not found.");
        }
    }
}
```

---
