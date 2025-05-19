#  **Algorithms**

---

## **Sorting**

### **1. QuickSort**
Divide-and-conquer algorithm that partitions the array and sorts each partition recursively.
```java
public class QuickSort {
    public void quickSort(int[] arr, int low, int high) {
        // Base case: if low is not less than high, array is already sorted
        if (low < high) {
            // Partition the array and get the pivot index
            int pi = partition(arr, low, high);

            // Recursively sort elements before and after the partition
            quickSort(arr, low, pi - 1);
            quickSort(arr, pi + 1, high);
        }
    }

    private int partition(int[] arr, int low, int high) {
        // Choose the last element as the pivot
        int pivot = arr[high];

        // Index of smaller element
        int i = low - 1;

        // Traverse the array and move elements smaller than the pivot to the left
        for (int j = low; j < high; j++) {
            if (arr[j] <= pivot) {
                i++;
                swap(arr, i, j); // Swap elements to position smaller elements before the pivot
            }
        }

        // Place the pivot element at its correct position
        swap(arr, i + 1, high);
        return i + 1; // Return the pivot index
    }

    private void swap(int[] arr, int i, int j) {
        // Swap two elements in the array
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    public static void main(String[] args) {
        int[] arr = {10, 7, 8, 9, 1, 5};
        new QuickSort().quickSort(arr, 0, arr.length - 1);
        // Print the sorted array
        System.out.println(Arrays.toString(arr));
    }
}

```

### **2. MergeSort**
Divide-and-conquer algorithm that splits the array into halves, sorts each half, and merges them.
```java
public class MergeSort {
    public void mergeSort(int[] arr, int left, int right) {
        // Base case: if the array has more than one element
        if (left < right) {
            // Find the middle point
            int mid = (left + right) / 2;

            // Recursively sort the first and second halves
            mergeSort(arr, left, mid);
            mergeSort(arr, mid + 1, right);

            // Merge the sorted halves
            merge(arr, left, mid, right);
        }
    }

    private void merge(int[] arr, int left, int mid, int right) {
        // Find sizes of the two subarrays to be merged
        int n1 = mid - left + 1;
        int n2 = right - mid;

        // Create temporary arrays
        int[] L = new int[n1];
        int[] R = new int[n2];

        // Copy data to temporary arrays
        System.arraycopy(arr, left, L, 0, n1);
        System.arraycopy(arr, mid + 1, R, 0, n2);

        // Initial indices of subarrays and the merged array
        int i = 0, j = 0, k = left;

        // Merge the temporary arrays back into the original array
        while (i < n1 && j < n2) {
            if (L[i] <= R[j]) {
                arr[k++] = L[i++];
            } else {
                arr[k++] = R[j++];
            }
        }

        // Copy remaining elements of L[], if any
        while (i < n1) {
            arr[k++] = L[i++];
        }

        // Copy remaining elements of R[], if any
        while (j < n2) {
            arr[k++] = R[j++];
        }
    }

    public static void main(String[] args) {
        int[] arr = {12, 11, 13, 5, 6, 7};
        new MergeSort().mergeSort(arr, 0, arr.length - 1);
        // Print the sorted array
        System.out.println(Arrays.toString(arr));
    }
}

```

---

## **Searching**

### **Binary Search**
Efficiently search a sorted array.
```java
public class BinarySearch {
    public int binarySearch(int[] arr, int target) {
        // Initialize the search range
        int low = 0, high = arr.length - 1;

        // Perform binary search
        while (low <= high) {
            // Calculate the middle index
            int mid = low + (high - low) / 2;

            // Check if the target is at the mid index
            if (arr[mid] == target) return mid;

            // If target is greater, ignore the left half
            if (arr[mid] < target) low = mid + 1;
            // If target is smaller, ignore the right half
            else high = mid - 1;
        }

        // Target is not present in the array
        return -1;
    }

    public static void main(String[] args) {
        int[] arr = {2, 3, 4, 10, 40};
        int result = new BinarySearch().binarySearch(arr, 10);
        // Print the result
        System.out.println(result != -1 ? "Element found at index " + result : "Element not found");
    }
}

```

---

## **Dynamic Programming**

### **1. Fibonacci Sequence**
Solve Fibonacci using a bottom-up approach.
```java
public class FibonacciDP {
    public int fibonacci(int n) {
        // Handle base cases
        if (n <= 1) return n;

        // Create a DP array to store Fibonacci numbers
        int[] dp = new int[n + 1];
        dp[0] = 0;
        dp[1] = 1;

        // Fill the DP array with Fibonacci numbers
        for (int i = 2; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }

        // Return the nth Fibonacci number
        return dp[n];
    }

    public static void main(String[] args) {
        System.out.println(new FibonacciDP().fibonacci(10)); // Output: 55
    }
}

```

### **2. Knapsack Problem**
Given weights and values, find the maximum value that fits within the weight limit.
```java
public class Knapsack {
    public int knapsack(int W, int[] weights, int[] values, int n) {
        // Create a DP table where dp[i][w] stores the max value for the first i items with weight limit w
        int[][] dp = new int[n + 1][W + 1];

        // Build the DP table
        for (int i = 1; i <= n; i++) {
            for (int w = 1; w <= W; w++) {
                // Check if the weight of the current item is less than or equal to the current weight limit
                if (weights[i - 1] <= w) {
                    // Maximize value: include or exclude the item
                    dp[i][w] = Math.max(values[i - 1] + dp[i - 1][w - weights[i - 1]], dp[i - 1][w]);
                } else {
                    // Exclude the item
                    dp[i][w] = dp[i - 1][w];
                }
            }
        }

        // Return the maximum value for the given weight limit
        return dp[n][W];
    }

    public static void main(String[] args) {
        int[] weights = {1, 2, 3};
        int[] values = {6, 10, 12};
        System.out.println(new Knapsack().knapsack(5, weights, values, weights.length)); // Output: 22
    }
}

```

---

## **Greedy Algorithms**

### **Interval Scheduling**
Find the maximum number of non-overlapping intervals.
```java
import java.util.*;

public class IntervalScheduling {
    public int maxNonOverlappingIntervals(int[][] intervals) {
        // Sort the intervals based on their end times
        Arrays.sort(intervals, Comparator.comparingInt(a -> a[1]));

        int count = 0;       // Count of non-overlapping intervals
        int end = Integer.MIN_VALUE; // Tracks the end time of the last added interval

        for (int[] interval : intervals) {
            // If the current interval does not overlap with the last added interval
            if (interval[0] >= end) {
                count++;        // Include the current interval
                end = interval[1]; // Update the end time
            }
        }
        return count; // Return the maximum count of non-overlapping intervals
    }

    public static void main(String[] args) {
        int[][] intervals = {{1, 2}, {2, 3}, {3, 4}, {1, 3}};
        // Expected Output: 3 (e.g., intervals [1,2], [2,3], [3,4])
        System.out.println(new IntervalScheduling().maxNonOverlappingIntervals(intervals));
    }
}

```

---

## **Recursion and Backtracking**

### **Permutations**
Find all permutations of an array.
```java
import java.util.*;

public class Permutations {
    public void permute(int[] nums, List<Integer> current, boolean[] used, List<List<Integer>> result) {
        // Base case: If the current permutation is of the same length as the input array
        if (current.size() == nums.length) {
            result.add(new ArrayList<>(current)); // Add a copy of the current permutation to the result
            return;
        }

        // Iterate through the elements of the array
        for (int i = 0; i < nums.length; i++) {
            // Skip elements that are already used in the current permutation
            if (used[i]) continue;

            // Mark the current element as used
            used[i] = true;
            current.add(nums[i]); // Add the element to the current permutation

            // Recursively generate permutations for the remaining elements
            permute(nums, current, used, result);

            // Backtrack: Remove the last element and mark it as unused
            used[i] = false;
            current.remove(current.size() - 1);
        }
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 3};
        List<List<Integer>> result = new ArrayList<>();
        new Permutations().permute(nums, new ArrayList<>(), new boolean[nums.length], result);
        // Output: [[1, 2, 3], [1, 3, 2], [2, 1, 3], [2, 3, 1], [3, 1, 2], [3, 2, 1]]
        System.out.println(result);
    }
}

```

### **N-Queens Problem**
Solve the N-Queens problem using backtracking.
```java
public class NQueens {
    public void solveNQueens(int n) {
        // Create an empty chessboard represented by a 2D character array
        char[][] board = new char[n][n];
        for (char[] row : board) Arrays.fill(row, '.'); // Fill the board with '.'

        solve(board, 0); // Start placing queens from the first row
    }

    private void solve(char[][] board, int row) {
        // Base case: If all queens are placed, print the board
        if (row == board.length) {
            printBoard(board);
            return;
        }

        // Try placing a queen in each column of the current row
        for (int col = 0; col < board.length; col++) {
            if (isSafe(board, row, col)) {
                board[row][col] = 'Q'; // Place the queen
                solve(board, row + 1); // Recur for the next row
                board[row][col] = '.'; // Backtrack: Remove the queen
            }
        }
    }

    private boolean isSafe(char[][] board, int row, int col) {
        // Check the column for any other queen
        for (int i = 0; i < row; i++) {
            if (board[i][col] == 'Q') return false;
        }

        // Check the upper left diagonal
        for (int i = row - 1, j = col - 1; i >= 0 && j >= 0; i--, j--) {
            if (board[i][j] == 'Q') return false;
        }

        // Check the upper right diagonal
        for (int i = row - 1, j = col + 1; i >= 0 && j < board.length; i--, j++) {
            if (board[i][j] == 'Q') return false;
        }

        return true; // The position is safe for the queen
    }

    private void printBoard(char[][] board) {
        // Print the chessboard configuration
        for (char[] row : board) {
            System.out.println(new String(row));
        }
        System.out.println();
    }

    public static void main(String[] args) {
        new NQueens().solveNQueens(4);
        // Output: All possible solutions for placing 4 queens on a 4x4 board
    }
}

```

--- 