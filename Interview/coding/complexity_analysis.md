# **Complexity Analysis**

Complexity analysis evaluates the efficiency of an algorithm in terms of **time complexity** and **space complexity** using Big O notation.

- **Time Complexity**: How the runtime of an algorithm scales with the input size \( n \).
- **Space Complexity**: How the memory usage of an algorithm scales with the input size \( n \).

---

### **Understanding Big O Notation**

| Notation    | Description              | Example Algorithm                |
|-------------|--------------------------|-----------------------------------|
| \( O(1) \)  | Constant time            | Accessing an element in an array |
| \( O(\log n) \) | Logarithmic time      | Binary search                    |
| \( O(n) \)  | Linear time              | Iterating through an array       |
| \( O(n \log n) \) | Log-linear time     | Merge sort, quicksort (average)  |
| \( O(n^2) \) | Quadratic time          | Nested loops                     |
| \( O(2^n) \) | Exponential time        | Recursive Fibonacci              |

---

### **Example 1: Time Complexity Analysis**

#### **Code: Find the Maximum Element in an Array**
```java
public int findMax(int[] arr) {
    int max = arr[0]; // O(1)
    for (int i = 1; i < arr.length; i++) { // O(n)
        if (arr[i] > max) { // O(1)
            max = arr[i]; // O(1)
        }
    }
    return max; // O(1)
}
```

#### **Time Complexity:**
- The loop runs \( n - 1 \) times (for an array of size \( n \)).
- Total complexity: \( O(1) + O(n) \approx O(n) \).

#### **Space Complexity:**
- No extra space is used beyond the input array.
- Space complexity: \( O(1) \).

---

### **Example 2: Space Complexity Analysis**

#### **Code: Reverse an Array In-Place**
```java
public void reverseArray(int[] arr) {
    int left = 0, right = arr.length - 1;
    while (left < right) { // O(n/2)
        int temp = arr[left];
        arr[left] = arr[right];
        arr[right] = temp;
        left++;
        right--;
    }
}
```

#### **Time Complexity:**
- The loop iterates \( n/2 \) times.
- Total complexity: \( O(n/2) \approx O(n) \).

#### **Space Complexity:**
- The algorithm reverses the array in place without using additional memory.
- Space complexity: \( O(1) \).

---

### **Example 3: Nested Loops**

#### **Code: Find All Pairs in an Array**
```java
public void findPairs(int[] arr) {
    for (int i = 0; i < arr.length; i++) { // O(n)
        for (int j = i + 1; j < arr.length; j++) { // O(n)
            System.out.println("(" + arr[i] + ", " + arr[j] + ")");
        }
    }
}
```

#### **Time Complexity:**
- Outer loop runs \( n \) times.
- Inner loop runs approximately \( n/2 \) times on average.
- Total complexity: \( O(n \times n) = O(n^2) \).

#### **Space Complexity:**
- No additional space is used.
- Space complexity: \( O(1) \).

---

### **Example 4: Recursive Fibonacci**

#### **Code: Fibonacci Using Recursion**
```java
public int fibonacci(int n) {
    if (n <= 1) return n; // O(1)
    return fibonacci(n - 1) + fibonacci(n - 2); // Recursive calls
}
```

#### **Time Complexity:**
- Each call splits into two more calls.
- Total number of calls is roughly \( 2^n \).
- Complexity: \( O(2^n) \).

#### **Space Complexity:**
- The recursion stack grows linearly with \( n \).
- Space complexity: \( O(n) \).

---

### **Optimizing Algorithms**

#### **Code: Optimizing Fibonacci with Dynamic Programming**
```java
public int fibonacciDP(int n) {
    if (n <= 1) return n; // O(1)

    int[] dp = new int[n + 1]; // O(n) space
    dp[0] = 0; // O(1)
    dp[1] = 1; // O(1)

    for (int i = 2; i <= n; i++) { // O(n)
        dp[i] = dp[i - 1] + dp[i - 2];
    }
    return dp[n]; // O(1)
}
```

#### **Time Complexity:**
- Iterates \( n \) times.
- Complexity: \( O(n) \).

#### **Space Complexity:**
- Uses an array of size \( n + 1 \).
- Complexity: \( O(n) \).

---

### **Practice Steps**

1. **Understand the Code:**
   - Break down each part of the algorithm.
   - Identify loops, recursion, and function calls.

2. **Count Operations:**
   - Count the dominant operations (e.g., loop iterations, recursive calls).

3. **Focus on Dominant Terms:**
   - Drop lower-order terms and constants (e.g., \( O(n + 1) \approx O(n) \)).

4. **Compare Efficiency:**
   - Use Big O to compare algorithms (e.g., \( O(n) \) is better than \( O(n^2) \)).

5. **Optimize:**
   - Reduce unnecessary operations.
   - Use efficient data structures (e.g., HashMap for \( O(1) \) lookups).

---