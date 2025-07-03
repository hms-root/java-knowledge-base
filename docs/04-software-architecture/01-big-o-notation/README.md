## 🧠 What Is Time Complexity?

When we write a program, it takes time to run. But we don’t always want to measure that time in seconds — because seconds depend on your computer, how busy the CPU is, etc.

**Time complexity** is a way to measure _how many steps_ your code takes based on how big the input is.

We don’t count real time. We count **how the number of operations grows** as the input grows.

---

## 🧮 Big O Notation – What Does O(...) Mean?

Big O notation is a way to describe the _speed_ of an algorithm using a letter and a math expression. For example:

- `O(1)` means "constant time"
- `O(n)` means "time grows with size of input"
- `O(n^2)` means "time grows with the square of the input"

Let’s say:

```java
int[] numbers = new int[1000];
```

The `n` here is the number of elements (1000).

If you loop over the array:

```java
for (int i = 0; i < numbers.length; i++) {
    System.out.println(numbers[i]);
}
```

That’s `O(n)`, because you do 1 operation per item.

If you have two nested loops:

```java
for (int i = 0; i < numbers.length; i++) {
    for (int j = 0; j < numbers.length; j++) {
        System.out.println(numbers[i] + numbers[j]);
    }
}
```

That’s `O(n^2)`, because for each of the `n` items, you do `n` more operations.

---

## 🪜 Time Complexity Examples (from Easiest to Hardest)

### ✅ O(1) – Constant Time

```java
int getFirst(int[] arr) {
    return arr[0];
}
```

---

### ✅ O(n) – Linear Time

```java
int sum(int[] arr) {
    int total = 0;
    for (int i = 0; i < arr.length; i++) {
        total += arr[i];
    }
    return total;
}
```

---

### ✅ O(n²) – Quadratic Time

```java
void printAllPairs(int[] arr) {
    for (int i = 0; i < arr.length; i++) {
        for (int j = 0; j < arr.length; j++) {
            System.out.println(arr[i] + "," + arr[j]);
        }
    }
}
```

---

### ✅ O(log n) – Logarithmic Time

```java
int binarySearch(int[] arr, int target) {
    int left = 0, right = arr.length - 1;
    while (left <= right) {
        int mid = (left + right) / 2;
        if (arr[mid] == target) return mid;
        if (arr[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}
```

---

### ✅ O(n log n) – Linearithmic Time

```java
void mergeSort(int[] arr, int left, int right) {
    if (left < right) {
        int mid = (left + right) / 2;
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);
        merge(arr, left, mid, right);
    }
}
```

---

### ✅ O(2^n) – Exponential Time

```java
int fib(int n) {
    if (n <= 1) return n;
    return fib(n - 1) + fib(n - 2);
}
```

---

### ✅ O(n!) – Factorial Time

```java
void permute(String str, String out) {
    if (str.length() == 0) {
        System.out.println(out);
        return;
    }
    for (int i = 0; i < str.length(); i++) {
        permute(str.substring(0, i) + str.substring(i+1), out + str.charAt(i));
    }
}
```

---

---

---

## 🔟 Time Complexity Examples – Full Explanations

### 🟢 Constant Time – O(1)

```java
int getFirst(int[] arr) {
    return arr[0];
}
```

This operation accesses the first element of the array, which takes the same time no matter how large the array is. It does not depend on input size.

---

### 🔵 Linear Time – O(n)

```java
int sum(int[] arr) {
    int total = 0;
    for (int i = 0; i < arr.length; i++) {
        total += arr[i];
    }
    return total;
}
```

We go through the array once. If there are 5 elements, we do 5 additions. If there are 5 million, we do 5 million. Time grows linearly.

---

### 🟣 Quadratic Time – O(n²)

```java
void printAllPairs(int[] arr) {
    for (int i = 0; i < arr.length; i++) {
        for (int j = 0; j < arr.length; j++) {
            System.out.println(arr[i] + "," + arr[j]);
        }
    }
}
```

Every element is paired with every other element. If there are 10 elements, we make 100 (10x10) combinations.

---

### 🟡 Logarithmic Time – O(log n)

```java
int binarySearch(int[] arr, int target) {
    int left = 0, right = arr.length - 1;
    while (left <= right) {
        int mid = (left + right) / 2;
        if (arr[mid] == target) return mid;
        if (arr[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}
```

Each step eliminates half the elements, so the number of steps is proportional to log(n). Very efficient for large sorted arrays.

---

### 🟠 Linearithmic Time – O(n log n)

```java
void mergeSort(int[] arr, int left, int right) {
    if (left < right) {
        int mid = (left + right) / 2;
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);
        merge(arr, left, mid, right);
    }
}
```

The array is split in half repeatedly (log n times), and each level requires processing all elements (n), making total time O(n log n).

---

### 🔴 Exponential Time – O(2^n)

```java
int fib(int n) {
    if (n <= 1) return n;
    return fib(n - 1) + fib(n - 2);
}
```

Each function call creates two more calls, forming a tree of size 2ⁿ. Very slow for big numbers unless optimized with memoization.

---

### ⚫ Factorial Time – O(n!)

```java
void permute(String str, String out) {
    if (str.length() == 0) {
        System.out.println(out);
        return;
    }
    for (int i = 0; i < str.length(); i++) {
        permute(str.substring(0, i) + str.substring(i+1), out + str.charAt(i));
    }
}
```

We try every possible ordering of characters, which grows as n!. This becomes unusable very quickly as n increases.

---

### 🔶 Square Root Loop – O(√n)

```java
void squareRootLoop(int n) {
    for (int i = 1; i * i <= n; i++) {
        System.out.println(i);
    }
}
```

The loop only runs up to the square root of n. If n is 100, we go up to 10 steps.

---

### 🔷 Nested Log Loops – O(log² n)

```java
void nestedLog(int n) {
    int i = n;
    while (i > 1) {
        int j = i;
        while (j > 1) {
            j = j / 2;
        }
        i = i / 2;
    }
}
```

Each loop divides the value by 2. Outer and inner both take log n → total complexity is log²(n).

---

### 🟤 Triple Nested Loop – O(n³)

```java
void printTriplets(int[] arr) {
    for (int i : arr)
        for (int j : arr)
            for (int k : arr)
                System.out.println(i + j + k);
}
```

For each combination of i, j, and k, we run the innermost line. The work grows as n × n × n = n³.

### ✅ Example 1: Return first element — O(1)

```java
int f(int[] arr) {
  return arr[0];
}
```

### ✅ Example 2: Sum all elements — O(n)

```java
int sum(int[] arr) {
  int total = 0;
  for (int i = 0; i < arr.length; i++) total += arr[i];
  return total;
}
```

### ✅ Example 3: Two loops in sequence — O(n)

```java
for (int i = 0; i < n; i++) System.out.println(i);
for (int j = 0; j < n; j++) System.out.println(j);
```

### ✅ Example 4: Nested loop — O(n²)

```java
for (int i = 0; i < n; i++)
  for (int j = 0; j < n; j++)
    System.out.println(i + j);
```

### ✅ Example 5: Halving loop — O(log n)

```java
int x = n;
while (x > 1) x = x / 2;
```

### ✅ Example 6: Linear loop with inner log loop — O(n log n)

```java
for (int i = 0; i < n; i++) {
    int x = n;
    while (x > 1) x = x / 2;
}
```

### ✅ Example 7: Merge sort recursive structure — O(n log n)

(see mergeSort implementation above)

### ✅ Example 8: Recursive Fibonacci — O(2^n)

```java
int fib(int n) {
    if (n <= 1) return n;
    return fib(n - 1) + fib(n - 2);
}
```

### ✅ Example 9: Generate subsets — O(2^n)

```java
void generateSubsets(int[] arr, int index, List<Integer> current) {
    if (index == arr.length) {
        System.out.println(current);
        return;
    }
    generateSubsets(arr, index + 1, current);
    current.add(arr[index]);
    generateSubsets(arr, index + 1, current);
    current.remove(current.size() - 1);
}
```

### ✅ Example 10: Permutations — O(n!)

```java
void permute(String str, String result) {
    if (str.length() == 0) {
        System.out.println(result);
        return;
    }
    for (int i = 0; i < str.length(); i++) {
        String rem = str.substring(0, i) + str.substring(i + 1);
        permute(rem, result + str.charAt(i));
    }
}
```

---

## 🧪 10 More Step-by-Step Big O Examples (Advanced)

### ✅ Example 11: Loop with Square Root — O(√n)

```java
void squareRootLoop(int n) {
    for (int i = 1; i * i <= n; i++) {
        System.out.println(i);
    }
}
```

---

### ✅ Example 12: Halving Loop — O(log n)

```java
void halfUntilZero(int n) {
    while (n > 0) {
        System.out.println("Still halving");
        n = n / 2;
    }
}
```

---

### ✅ Example 13: Nested Log Loops — O(log² n)

```java
void nestedLog(int n) {
    int i = n;
    while (i > 1) {
        int j = i;
        while (j > 1) {
            j = j / 2;
        }
        i = i / 2;
    }
}
```

---

### ✅ Example 14: Triple Nested Loops — O(n³)

```java
void printTriplets(int[] arr) {
    for (int i : arr)
        for (int j : arr)
            for (int k : arr)
                System.out.println(i + j + k);
}
```

---

### ✅ Example 15: Array Reversal — O(n)

```java
void reverseArray(int[] arr) {
    int left = 0, right = arr.length - 1;
    while (left < right) {
        int temp = arr[left];
        arr[left++] = arr[right];
        arr[right--] = temp;
    }
}
```

---

### ✅ Example 16: Linear Loop + Binary Search — O(n log n)

```java
void linearWithBinarySearch(int[] arr, int[] queries) {
    for (int q : queries) {
        int left = 0, right = arr.length - 1;
        while (left <= right) {
            int mid = (left + right) / 2;
            if (arr[mid] == q) break;
            else if (arr[mid] < q) left = mid + 1;
            else right = mid - 1;
        }
    }
}
```

---

### ✅ Example 17: Fibonacci with Memoization — O(n)

```java
int fibMemo(int n, int[] memo) {
    if (n <= 1) return n;
    if (memo[n] != 0) return memo[n];
    return memo[n] = fibMemo(n - 1, memo) + fibMemo(n - 2, memo);
}
```

---

### ✅ Example 18: Combinations — O(2^n)

```java
void generateCombinations(int[] arr, int i, List<Integer> current) {
    if (i == arr.length) {
        System.out.println(current);
        return;
    }
    generateCombinations(arr, i + 1, current);
    current.add(arr[i]);
    generateCombinations(arr, i + 1, current);
    current.remove(current.size() - 1);
}
```

---

### ✅ Example 19: Permutations — O(n!)

```java
void permute(int[] arr, int start) {
    if (start == arr.length) {
        System.out.println(Arrays.toString(arr));
        return;
    }
    for (int i = start; i < arr.length; i++) {
        swap(arr, i, start);
        permute(arr, start + 1);
        swap(arr, i, start);
    }
}
```

---

### ✅ Example 20: Sort and Scan — O(n log n)

```java
void sortAndScan(int[] arr) {
    Arrays.sort(arr); // O(n log n)
    for (int x : arr) {
        System.out.println(x); // O(n)
    }
}
```

---
