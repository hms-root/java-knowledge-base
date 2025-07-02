# Arrays

This guide explains how to use arrays in Java efficiently, including advanced manipulations, best practices, and clear examples.

---

## 🔹 What Are Arrays?

An array is a **fixed-size** collection of elements of the **same type**, stored in **contiguous memory**.  
✅ Use arrays when:

- You know the number of elements in advance.
- Performance is important (fast access by index).
- You need compact storage of homogeneous data.

---

## 🔹 Declaration and Instantiation

```java
int[] numbers;                 // declaration
numbers = new int[5];         // instantiation (default = 0)

String[] names = new String[] {"Ana", "Bob", "Cleo"}; // inline

int[] other = {1, 2, 3, 4};   // shorthand
```

---

## 🔹 Access, Modify, and Delete Elements

```java
int[] arr = {10, 20, 30};

int first = arr[0];     // Access
arr[1] = 99;            // Modify

// "Delete" (no real delete — overwrite or shift manually)
arr[2] = 0;
```

⚠️ Arrays in Java have **fixed size**. Deleting or inserting requires copying/shifting elements.

---

## 🔹 Useful Methods (`Arrays` class)

```java
import java.util.Arrays;

// Sorting
Arrays.sort(arr);

// Compare arrays
Arrays.equals(arr1, arr2);     // true if same content
Arrays.compare(arr1, arr2);    // 0 if equal, <0 if arr1 < arr2

// Copying
int[] copy = Arrays.copyOf(arr, arr.length);       // copy full
int[] sub = Arrays.copyOfRange(arr, 1, 3);         // copy part

// Print array
System.out.println(Arrays.toString(arr));
```

---

## 🔹 Traversing an Array

### Forward:

```java
for (int i = 0; i < arr.length; i++) {
    System.out.println(arr[i]);
}
```

### Enhanced for-each:

```java
for (int val : arr) {
    System.out.println(val);
}
```

### Reverse:

```java
for (int i = arr.length - 1; i >= 0; i--) {
    System.out.println(arr[i]);
}
```

---

## 🔹 Combine Arrays

```java
int[] a = {1, 2};
int[] b = {3, 4};
int[] combined = new int[a.length + b.length];

System.arraycopy(a, 0, combined, 0, a.length);
System.arraycopy(b, 0, combined, a.length, b.length);
```

---

## 🔹 Resize an Array (Create New One)

```java
int[] original = {1, 2, 3};
int[] resized = Arrays.copyOf(original, 5); // size = 5
```

---

## 🔹 Get Maximum and Minimum

```java
int max = Arrays.stream(arr).max().getAsInt();
int min = Arrays.stream(arr).min().getAsInt();
```

---

## 🔹 Search in Array

### Linear Search:

```java
int target = 99;
for (int val : arr) {
    if (val == target) {
        // found
    }
}
```

### Binary Search (sorted arrays only):

```java
Arrays.sort(arr);
int index = Arrays.binarySearch(arr, 20);
```

---

## 🔹 Shift Elements (Manual)

### Right Shift from Index:

```java
for (int i = arr.length - 1; i > index; i--) {
    arr[i] = arr[i - 1];
}
```

---

## 🔹 Insert Element at Index (with shift)

```java
int[] arr = new int[6];
arr[0] = 1; arr[1] = 2; arr[2] = 4;

int insertPos = 2;
int value = 3;

for (int i = arr.length - 1; i > insertPos; i--) {
    arr[i] = arr[i - 1];
}
arr[insertPos] = value;
```

---

## 🔹 Insert into Sorted Array (Keep Sorted)

```java
int[] sorted = {1, 3, 5, 7, 0}; // last slot empty
int value = 4;
int pos = 0;

// Find position
while (pos < sorted.length - 1 && value > sorted[pos]) {
    pos++;
}

// Shift and insert
for (int i = sorted.length - 1; i > pos; i--) {
    sorted[i] = sorted[i - 1];
}
sorted[pos] = value;
```

---

## 🔹 Remove Element and Shift Left

```java
int[] arr = {1, 2, 3, 4, 5};
int removeIndex = 2;

for (int i = removeIndex; i < arr.length - 1; i++) {
    arr[i] = arr[i + 1];
}
arr[arr.length - 1] = 0; // optional reset
```

---

## 🟦 Best Practices Summary

- ✅ Use arrays for fixed-size, fast-access structures.
- ✅ Use `Arrays.copyOf` to resize.
- ✅ Use `System.arraycopy()` for efficient merging or shifting.
- ✅ Use enhanced `for` loop for readability.
- ✅ Always check bounds: `IndexOutOfBoundsException` is common.
- ⚠️ Consider using `ArrayList` for dynamic sizes and easier manipulation.
