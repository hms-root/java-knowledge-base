# Matrices (2D Arrays)

This guide explains how to declare, use, and manipulate 2D arrays (matrices) in Java, with professional examples and best practices.

---

## 🔹 What Are Matrices?

A **matrix** in Java is a **2D array**: an array of arrays.  
Use matrices when you need to store tabular data like grids, tables, or matrices in math.

---

## 🔹 Declaration and Instantiation

```java
int[][] matrix = new int[3][4]; // 3 rows, 4 columns

// Inline initialization
int[][] matrix2 = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
```

✅ All inner arrays must be of the same type.

---

## 🔹 Get Matrix Dimensions

```java
int rows = matrix.length;
int cols = matrix[0].length;
```

⚠️ For variable column sizes, check each row's length individually.

---

## 🔹 Initialize Matrix with Values

```java
int[][] m = new int[2][3];
for (int i = 0; i < m.length; i++) {
    for (int j = 0; j < m[i].length; j++) {
        m[i][j] = i + j;
    }
}
```

---

## 🔹 Access and Modify Elements

```java
int val = matrix[1][2];    // get value
matrix[0][0] = 10;         // set value
```

---

## 🔹 Traverse a Matrix

```java
for (int i = 0; i < matrix.length; i++) {
    for (int j = 0; j < matrix[i].length; j++) {
        System.out.print(matrix[i][j] + " ");
    }
    System.out.println();
}
```

---

## 🔹 Matrices with Variable Column Sizes (Jagged Arrays)

```java
int[][] jagged = new int[3][];
jagged[0] = new int[2];
jagged[1] = new int[4];
jagged[2] = new int[1];
```

✅ Useful when rows have different column counts.

---

## 🔹 Search with Label and `break`

```java
int target = 7;
boolean found = false;

search:
for (int i = 0; i < matrix.length; i++) {
    for (int j = 0; j < matrix[i].length; j++) {
        if (matrix[i][j] == target) {
            found = true;
            break search;
        }
    }
}
```

---

## 🔹 Check If Matrix Is Symmetric

A matrix is symmetric if it is square and `matrix[i][j] == matrix[j][i]`.

```java
boolean isSymmetric = true;
for (int i = 0; i < matrix.length; i++) {
    for (int j = 0; j < matrix[i].length; j++) {
        if (matrix[i][j] != matrix[j][i]) {
            isSymmetric = false;
            break;
        }
    }
}
```

---

## 🔹 Transpose a Matrix

```java
int rows = matrix.length;
int cols = matrix[0].length;
int[][] transposed = new int[cols][rows];
for (int i = 0; i < rows; i++) {
    for (int j = 0; j < cols; j++) {
        transposed[j][i] = matrix[i][j];
    }
}
```

---

## 🔹 Diagonal and Triangular Sections

### Principal Diagonal

```java
for (int i = 0; i < matrix.length; i++) {
    System.out.print(matrix[i][i] + " ");
}
```

### Upper Triangle

```java
for (int i = 0; i < matrix.length; i++) {
    for (int j = i; j < matrix[i].length; j++) {
        System.out.print(matrix[i][j] + " ");
    }
}
```

### Lower Triangle

```java
for (int i = 0; i < matrix.length; i++) {
    for (int j = 0; j <= i; j++) {
        System.out.print(matrix[i][j] + " ");
    }
}
```

---

## 🟦 Best Practices Summary

- ✅ Use consistent dimensions unless you need jagged arrays.
- ✅ Always check bounds: `matrix[i].length` may vary.
- ✅ Use nested loops or enhanced `for` for readability.
- ✅ For square matrix algorithms, always check dimensions first.
- ✅ Label loops only when nested breaks are necessary.
