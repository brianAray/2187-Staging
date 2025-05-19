# **Data Structures**

## **Arrays and Strings**
- **Manipulation**
  - **Reversing:**
    Reverse an array or string in place.
    ```java
    public void reverseArray(int[] arr) {
        int start = 0, end = arr.length - 1;
        while (start < end) {
            int temp = arr[start];
            arr[start] = arr[end];
            arr[end] = temp;
            start++;
            end--;
        }
    }
    ```
  - **Rotating:**
    Rotate an array to the right by `k` steps.
    ```java
    public void rotateArray(int[] nums, int k) {
        k = k % nums.length;
        reverse(nums, 0, nums.length - 1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, nums.length - 1);
    }

    private void reverse(int[] nums, int start, int end) {
        while (start < end) {
            int temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;
            start++;
            end--;
        }
    }
    ```
  - **Merging:**
    Merge two sorted arrays into one sorted array.
    ```java
    public int[] mergeSortedArrays(int[] nums1, int[] nums2) {
        int[] result = new int[nums1.length + nums2.length];
        int i = 0, j = 0, k = 0;

        while (i < nums1.length && j < nums2.length) {
            if (nums1[i] < nums2[j]) {
                result[k++] = nums1[i++];
            } else {
                result[k++] = nums2[j++];
            }
        }

        while (i < nums1.length) result[k++] = nums1[i++];
        while (j < nums2.length) result[k++] = nums2[j++];

        return result;
    }
    ```

- **Common Algorithms**
  - **Two-pointer technique:**  
    Solve problems like finding pairs in a sorted array that sum to a target.
    ```java
    public boolean hasPairWithSum(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        while (left < right) {
            int sum = nums[left] + nums[right];
            if (sum == target) return true;
            if (sum < target) left++;
            else right--;
        }
        return false;
    }
    ```
  - **Sliding window:**  
    Find the maximum sum of a subarray of size `k`.
    ```java
    public int maxSubArraySum(int[] nums, int k) {
        int maxSum = 0, windowSum = 0;
        for (int i = 0; i < nums.length; i++) {
            windowSum += nums[i];
            if (i >= k - 1) {
                maxSum = Math.max(maxSum, windowSum);
                windowSum -= nums[i - (k - 1)];
            }
        }
        return maxSum;
    }
    ```

---

## **Linked Lists**
- **Implementation**
  - **Singly Linked List:**
    ```java
    class Node {
        int data;
        Node next;

        Node(int data) {
            this.data = data;
        }
    }

    public void addNode(Node head, int data) {
        Node current = head;
        while (current.next != null) {
            current = current.next;
        }
        current.next = new Node(data);
    }
    ```
  - **Doubly Linked List:**
    ```java
    class DoublyNode {
        int data;
        DoublyNode prev, next;

        DoublyNode(int data) {
            this.data = data;
        }
    }
    ```

- **Common Problems**
  - **Reversing a list:**
    ```java
    public Node reverseList(Node head) {
        Node prev = null, current = head, next = null;
        while (current != null) {
            next = current.next;
            current.next = prev;
            prev = current;
            current = next;
        }
        return prev;
    }
    ```
---

## **Stacks and Queues**
- **Implementation**
  - **Stack using an array:**
    ```java
    class Stack {
        int[] stack;
        int top = -1;

        Stack(int size) {
            stack = new int[size];
        }

        public void push(int value) {
            stack[++top] = value;
        }

        public int pop() {
            return stack[top--];
        }
    }
    ```

  - **Queue using a linked list:**
    ```java
    class Queue {
        LinkedList<Integer> list = new LinkedList<>();

        public void enqueue(int value) {
            list.addLast(value);
        }

        public int dequeue() {
            return list.removeFirst();
        }
    }
    ```

- **Applications**
  - **Balancing parentheses:**
    ```java
    public boolean isValidParentheses(String s) {
        Stack<Character> stack = new Stack<>();
        for (char c : s.toCharArray()) {
            if (c == '(') stack.push(c);
            else if (c == ')' && (stack.isEmpty() || stack.pop() != '(')) return false;
        }
        return stack.isEmpty();
    }
    ```

---

## **Binary Trees and Binary Search Trees**
- **Traversals:**
  - **Inorder (left, root, right):**
    ```java
    public void inorderTraversal(TreeNode root) {
        if (root != null) {
            inorderTraversal(root.left);
            System.out.print(root.val + " ");
            inorderTraversal(root.right);
        }
    }
    ```

- **Operations:**
  - **Insertion in BST:**
    ```java
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if (root == null) return new TreeNode(val);
        if (val < root.val) root.left = insertIntoBST(root.left, val);
        else root.right = insertIntoBST(root.right, val);
        return root;
    }
    ```

---

## **Graphs**
- **Representations**
  - **Adjacency List:**
    ```java
    Map<Integer, List<Integer>> graph = new HashMap<>();
    graph.put(1, Arrays.asList(2, 3));
    graph.put(2, Arrays.asList(4));
    graph.put(3, Arrays.asList(4));
    ```

- **Traversals**
  - **BFS:**
    ```java
    public void bfs(Map<Integer, List<Integer>> graph, int start) {
        Queue<Integer> queue = new LinkedList<>();
        Set<Integer> visited = new HashSet<>();
        queue.add(start);
        visited.add(start);

        while (!queue.isEmpty()) {
            int node = queue.poll();
            System.out.print(node + " ");
            for (int neighbor : graph.getOrDefault(node, new ArrayList<>())) {
                if (!visited.contains(neighbor)) {
                    visited.add(neighbor);
                    queue.add(neighbor);
                }
            }
        }
    }
    ```

---

## **Map Applications**

Here are some practical examples of using **Map** structures in Java to solve various problems:

---

### 1. **Frequency Count of Elements**
Count the frequency of each element in an array.

```java
import java.util.HashMap;
import java.util.Map;

public class FrequencyCount {
    public static void main(String[] args) {
        int[] nums = {1, 2, 2, 3, 3, 3, 4};

        Map<Integer, Integer> frequencyMap = new HashMap<>();
        for (int num : nums) {
            frequencyMap.put(num, frequencyMap.getOrDefault(num, 0) + 1);
        }

        System.out.println("Frequency Map: " + frequencyMap);
    }
}
```
**Output:**
```
Frequency Map: {1=1, 2=2, 3=3, 4=1}
```

---

### 2. **Find First Non-Repeating Character in a String**
Use a `Map` to track the frequency of characters and determine the first non-repeating one.

```java
import java.util.LinkedHashMap;
import java.util.Map;

public class FirstNonRepeating {
    public static void main(String[] args) {
        String str = "swiss";
        
        Map<Character, Integer> charCount = new LinkedHashMap<>();
        for (char c : str.toCharArray()) {
            charCount.put(c, charCount.getOrDefault(c, 0) + 1);
        }

        for (Map.Entry<Character, Integer> entry : charCount.entrySet()) {
            if (entry.getValue() == 1) {
                System.out.println("First non-repeating character: " + entry.getKey());
                break;
            }
        }
    }
}
```
**Output:**
```
First non-repeating character: w
```

---

### 3. **Group Anagrams**
Use a `Map` where the key is the sorted version of each word, and the value is a list of words belonging to that group.

```java
import java.util.*;

public class GroupAnagrams {
    public static void main(String[] args) {
        String[] words = {"eat", "tea", "tan", "ate", "nat", "bat"};
        
        Map<String, List<String>> anagramGroups = new HashMap<>();
        for (String word : words) {
            char[] chars = word.toCharArray();
            Arrays.sort(chars);
            String sorted = new String(chars);
            
            anagramGroups.putIfAbsent(sorted, new ArrayList<>());
            anagramGroups.get(sorted).add(word);
        }

        System.out.println("Anagram Groups: " + anagramGroups.values());
    }
}
```
**Output:**
```
Anagram Groups: [[eat, tea, ate], [tan, nat], [bat]]
```

---

### 4. **Two Sum Problem**
Find two numbers in an array that add up to a given target using a `Map` to store the complement of each number.

```java
import java.util.HashMap;
import java.util.Map;

public class TwoSum {
    public static void main(String[] args) {
        int[] nums = {2, 7, 11, 15};
        int target = 9;

        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            if (map.containsKey(complement)) {
                System.out.println("Indices: " + map.get(complement) + ", " + i);
                return;
            }
            map.put(nums[i], i);
        }
    }
}
```
**Output:**
```
Indices: 0, 1
```

---

### 5. **Word Count in a Paragraph**
Count the occurrences of each word in a paragraph, ignoring case and punctuation.

```java
import java.util.*;

public class WordCount {
    public static void main(String[] args) {
        String paragraph = "Hello world! Hello Java. Hello Maps.";
        paragraph = paragraph.toLowerCase().replaceAll("[^a-z ]", "");
        String[] words = paragraph.split(" ");

        Map<String, Integer> wordCount = new HashMap<>();
        for (String word : words) {
            wordCount.put(word, wordCount.getOrDefault(word, 0) + 1);
        }

        System.out.println("Word Count: " + wordCount);
    }
}
```
**Output:**
```
Word Count: {hello=3, world=1, java=1, maps=1}
```

---

### 6. **Find Duplicates in an Array**
Use a `Map` to identify duplicate elements and their counts.

```java
import java.util.HashMap;
import java.util.Map;

public class FindDuplicates {
    public static void main(String[] args) {
        int[] nums = {1, 2, 3, 2, 4, 1, 5, 2};

        Map<Integer, Integer> duplicates = new HashMap<>();
        for (int num : nums) {
            duplicates.put(num, duplicates.getOrDefault(num, 0) + 1);
        }

        System.out.println("Duplicate Counts:");
        for (Map.Entry<Integer, Integer> entry : duplicates.entrySet()) {
            if (entry.getValue() > 1) {
                System.out.println(entry.getKey() + ": " + entry.getValue());
            }
        }
    }
}
```
**Output:**
```
Duplicate Counts:
1: 2
2: 3
```

---

### 7. **Sort a Map by Value**
Sort a `Map` based on its values and store the result in a `LinkedHashMap`.

```java
import java.util.*;
import java.util.stream.Collectors;

public class SortMapByValue {
    public static void main(String[] args) {
        Map<String, Integer> map = new HashMap<>();
        map.put("Alice", 50);
        map.put("Bob", 40);
        map.put("Charlie", 60);

        Map<String, Integer> sortedMap = map.entrySet()
            .stream()
            .sorted(Map.Entry.comparingByValue())
            .collect(Collectors.toMap(
                Map.Entry::getKey,
                Map.Entry::getValue,
                (e1, e2) -> e1,
                LinkedHashMap::new
            ));

        System.out.println("Sorted Map: " + sortedMap);
    }
}
```
**Output:**
```
Sorted Map: {Bob=40, Alice=50, Charlie=60}
```

---

### Summary
`Map` structures are extremely versatile in solving problems related to:
- Frequency counting
- Grouping
- Finding complements
- Storing relationships (e.g., key-value pairs)