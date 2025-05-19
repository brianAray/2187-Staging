# **Java-Specific Features**

---

## **Collections Framework**
The Java Collections Framework provides a set of classes and interfaces to handle data structures like lists, sets, maps, and queues efficiently.

### **1. `ArrayList`**
A resizable array that allows random access and is efficient for search operations.
```java
import java.util.ArrayList;

public class ArrayListExample {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();
        list.add("Apple");
        list.add("Banana");
        list.add("Cherry");

        System.out.println("ArrayList: " + list);

        // Access by index
        System.out.println("Element at index 1: " + list.get(1));
    }
}
```

### **2. `LinkedList`**
A doubly linked list that is efficient for insertion and deletion operations.
```java
import java.util.LinkedList;

public class LinkedListExample {
    public static void main(String[] args) {
        LinkedList<String> list = new LinkedList<>();
        list.add("Red");
        list.add("Blue");
        list.add("Green");

        list.addFirst("Yellow");
        list.removeLast();

        System.out.println("LinkedList: " + list);
    }
}
```

### **3. `HashMap`**
A map that stores key-value pairs and allows constant time lookups.
```java
import java.util.HashMap;

public class HashMapExample {
    public static void main(String[] args) {
        HashMap<Integer, String> map = new HashMap<>();
        map.put(1, "One");
        map.put(2, "Two");
        map.put(3, "Three");

        System.out.println("HashMap: " + map);
        System.out.println("Value for key 2: " + map.get(2));
    }
}
```

### **4. `TreeMap`**
A map that sorts keys in natural order or using a custom comparator.
```java
import java.util.TreeMap;

public class TreeMapExample {
    public static void main(String[] args) {
        TreeMap<Integer, String> map = new TreeMap<>();
        map.put(3, "C");
        map.put(1, "A");
        map.put(2, "B");

        System.out.println("TreeMap: " + map);
    }
}
```

### **5. `HashSet`**
A set that does not allow duplicate elements and offers constant time operations.
```java
import java.util.HashSet;

public class HashSetExample {
    public static void main(String[] args) {
        HashSet<String> set = new HashSet<>();
        set.add("Dog");
        set.add("Cat");
        set.add("Dog"); // Duplicate

        System.out.println("HashSet: " + set);
    }
}
```

### **6. `TreeSet`**
A set that sorts elements in natural order or using a custom comparator.
```java
import java.util.TreeSet;

public class TreeSetExample {
    public static void main(String[] args) {
        TreeSet<String> set = new TreeSet<>();
        set.add("Apple");
        set.add("Banana");
        set.add("Cherry");

        System.out.println("TreeSet: " + set);
    }
}
```

### **7. Comparators for Sorting**
Custom sorting using `Comparator`.
```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;

public class ComparatorExample {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();
        list.add("Banana");
        list.add("Apple");
        list.add("Cherry");

        // Sort in reverse order
        Collections.sort(list, Comparator.reverseOrder());
        System.out.println("Sorted List: " + list);
    }
}
```

---

## **Streams and Lambdas**

### **1. Functional Programming Basics**
Using lambdas to define concise operations.
```java
import java.util.ArrayList;

public class LambdaExample {
    public static void main(String[] args) {
        ArrayList<Integer> numbers = new ArrayList<>();
        numbers.add(1);
        numbers.add(2);
        numbers.add(3);

        // Print all elements using a lambda
        numbers.forEach(n -> System.out.println(n));
    }
}
```

### **2. Stream Operations**
Perform transformations and filters on collections.
```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class StreamExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        // Filter even numbers and square them
        List<Integer> result = numbers.stream()
            .filter(n -> n % 2 == 0)
            .map(n -> n * n)
            .collect(Collectors.toList());

        System.out.println("Filtered and Squared: " + result);
    }
}
```

### **3. Reduce Operation**
Aggregate elements of a stream.
```java
import java.util.Arrays;

public class ReduceExample {
    public static void main(String[] args) {
        int sum = Arrays.stream(new int[]{1, 2, 3, 4, 5})
            .reduce(0, Integer::sum);

        System.out.println("Sum: " + sum);
    }
}
```

---

## **Concurrency**

### **1. Threads**
Basic thread creation and execution.
```java
public class ThreadExample {
    public static void main(String[] args) {
        Thread thread = new Thread(() -> System.out.println("Thread is running"));
        thread.start();
    }
}
```

### **2. Synchronized Block**
Ensures thread safety by locking a critical section.
```java
public class SynchronizedExample {
    private int count = 0;

    public synchronized void increment() {
        count++;
    }

    public static void main(String[] args) {
        SynchronizedExample example = new SynchronizedExample();
        Thread t1 = new Thread(example::increment);
        Thread t2 = new Thread(example::increment);

        t1.start();
        t2.start();
    }
}
```

### **3. ExecutorService**
Manage threads using a thread pool.
```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class ExecutorServiceExample {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(2);

        Runnable task = () -> System.out.println("Task executed by " + Thread.currentThread().getName());
        executor.execute(task);
        executor.shutdown();
    }
}
```

---

## **File Handling**

### **1. Reading Files**
Using `BufferedReader` for efficient reading.
```java
import java.io.*;

public class FileReadExample {
    public static void main(String[] args) {
        try (BufferedReader br = new BufferedReader(new FileReader("example.txt"))) {
            String line;
            while ((line = br.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### **2. Writing Files**
Using `BufferedWriter` to write to a file.
```java
import java.io.*;

public class FileWriteExample {
    public static void main(String[] args) {
        try (BufferedWriter bw = new BufferedWriter(new FileWriter("example.txt"))) {
            bw.write("Hello, World!");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

---