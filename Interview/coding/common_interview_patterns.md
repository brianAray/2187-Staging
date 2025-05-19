# **Common Interview Patterns**

---

## **Sliding Window**

The **sliding window** technique is used to solve problems involving contiguous subarrays or substrings. It involves maintaining a "window" of elements within the array that slides forward to find the solution efficiently.

### **Example 1: Maximum Sum Subarray of Size K**
Find the maximum sum of any subarray of size \( k \) in an array.
```java
public class SlidingWindowMaxSum {
    public int maxSum(int[] arr, int k) {
        int maxSum = 0, windowSum = 0;

        // Initialize the first window
        for (int i = 0; i < k; i++) {
            windowSum += arr[i];
        }

        maxSum = windowSum;

        // Slide the window
        for (int i = k; i < arr.length; i++) {
            windowSum += arr[i] - arr[i - k]; // Add next element, remove first element of previous window
            maxSum = Math.max(maxSum, windowSum);
        }

        return maxSum;
    }

    public static void main(String[] args) {
        int[] arr = {2, 1, 5, 1, 3, 2};
        int k = 3;
        System.out.println(new SlidingWindowMaxSum().maxSum(arr, k)); // Output: 9
    }
}
```

### **Example 2: Longest Substring Without Repeating Characters**
Find the length of the longest substring without repeating characters.
```java
import java.util.HashSet;

public class LongestSubstring {
    public int lengthOfLongestSubstring(String s) {
        HashSet<Character> set = new HashSet<>();
        int left = 0, maxLength = 0;

        // Iterate over the string with a sliding window
        for (int right = 0; right < s.length(); right++) {
            while (set.contains(s.charAt(right))) {
                set.remove(s.charAt(left++)); // Shrink the window from the left
            }
            set.add(s.charAt(right)); // Add the current character to the set
            maxLength = Math.max(maxLength, right - left + 1); // Update the max length
        }

        return maxLength;
    }

    public static void main(String[] args) {
        String s = "abcabcbb";
        System.out.println(new LongestSubstring().lengthOfLongestSubstring(s)); // Output: 3
    }
}
```

---

## **Two Pointers**

The **two-pointer** technique is useful for problems that require evaluating elements at both ends of a collection or efficiently iterating over sorted arrays.

### **Example 1: Pair with Target Sum**
Find two numbers in a sorted array that add up to a target sum.
```java
public class TwoSumSorted {
    public int[] twoSum(int[] nums, int target) {
        int left = 0, right = nums.length - 1;

        while (left < right) {
            int sum = nums[left] + nums[right];
            if (sum == target) {
                return new int[]{left, right}; // Indices of the two numbers
            } else if (sum < target) {
                left++; // Increase the left pointer to increase the sum
            } else {
                right--; // Decrease the right pointer to decrease the sum
            }
        }

        return new int[]{-1, -1}; // No solution
    }

    public static void main(String[] args) {
        int[] nums = {2, 7, 11, 15};
        int target = 9;
        int[] result = new TwoSumSorted().twoSum(nums, target);
        System.out.println("Indices: " + result[0] + ", " + result[1]); // Output: Indices: 0, 1
    }
}
```

### **Example 2: Remove Duplicates from Sorted Array**
Remove duplicates in-place from a sorted array and return the length of the modified array.
```java
public class RemoveDuplicates {
    public int removeDuplicates(int[] nums) {
        if (nums.length == 0) return 0;

        int uniqueIndex = 0;

        for (int i = 1; i < nums.length; i++) {
            if (nums[i] != nums[uniqueIndex]) {
                uniqueIndex++;
                nums[uniqueIndex] = nums[i]; // Move the unique element forward
            }
        }

        return uniqueIndex + 1; // Length of the unique subarray
    }

    public static void main(String[] args) {
        int[] nums = {1, 1, 2, 2, 3};
        int length = new RemoveDuplicates().removeDuplicates(nums);
        System.out.println("Length of unique array: " + length); // Output: 3
    }
}
```

---

## **Divide and Conquer**

The **divide and conquer** strategy involves breaking down a problem into smaller subproblems, solving them recursively, and then combining the results.

### **Example 1: Quicksort**
Divide and conquer sorting algorithm.
```java
public class QuickSort {
    public void quickSort(int[] arr, int low, int high) {
        if (low < high) {
            int pi = partition(arr, low, high); // Partition the array
            quickSort(arr, low, pi - 1);       // Sort the left half
            quickSort(arr, pi + 1, high);      // Sort the right half
        }
    }

    private int partition(int[] arr, int low, int high) {
        int pivot = arr[high]; // Choose the last element as the pivot
        int i = low - 1;

        for (int j = low; j < high; j++) {
            if (arr[j] < pivot) {
                i++;
                swap(arr, i, j); // Swap elements smaller than the pivot
            }
        }

        swap(arr, i + 1, high); // Place pivot in its correct position
        return i + 1;
    }

    private void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    public static void main(String[] args) {
        int[] arr = {10, 7, 8, 9, 1, 5};
        new QuickSort().quickSort(arr, 0, arr.length - 1);
        System.out.println("Sorted Array: " + Arrays.toString(arr)); // Output: [1, 5, 7, 8, 9, 10]
    }
}
```

### **Example 2: Merge Sort**
Divide and conquer sorting algorithm.
```java
public class MergeSort {
    public void mergeSort(int[] arr, int left, int right) {
        if (left < right) {
            int mid = (left + right) / 2;

            mergeSort(arr, left, mid);         // Sort the left half
            mergeSort(arr, mid + 1, right);   // Sort the right half
            merge(arr, left, mid, right);     // Merge the sorted halves
        }
    }

    private void merge(int[] arr, int left, int mid, int right) {
        int n1 = mid - left + 1;
        int n2 = right - mid;

        int[] L = new int[n1];
        int[] R = new int[n2];

        System.arraycopy(arr, left, L, 0, n1);
        System.arraycopy(arr, mid + 1, R, 0, n2);

        int i = 0, j = 0, k = left;
        while (i < n1 && j < n2) {
            if (L[i] <= R[j]) {
                arr[k++] = L[i++];
            } else {
                arr[k++] = R[j++];
            }
        }

        while (i < n1) arr[k++] = L[i++];
        while (j < n2) arr[k++] = R[j++];
    }

    public static void main(String[] args) {
        int[] arr = {12, 11, 13, 5, 6, 7};
        new MergeSort().mergeSort(arr, 0, arr.length - 1);
        System.out.println("Sorted Array: " + Arrays.toString(arr)); // Output: [5, 6, 7, 11, 12, 13]
    }
}
```

---