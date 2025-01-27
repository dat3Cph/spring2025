---
title: Map and Filter
description: Streams in Java
layout: default
nav_order: 11
parent: Java
grand_parent: Toolbox
permalink: /toolbox/java/map-filter/
---

# Map and Filter functions in Java

The **`map`** and **`filter`** methods in Java are part of the **Streams API**, introduced in Java 8. These methods are used for processing collections in a functional and declarative manner.

## Map

- The `map` method is used to transform each element in a stream by applying a function to it.
- It produces a new stream with the transformed elements.

**Example 1: Convert a list of strings to their lengths**

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class MapExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
        
        // Transform names to their lengths
        List<Integer> lengths = names.stream()
                                     .map(String::length) // Get the length of each string
                                     .collect(Collectors.toList());
        
        System.out.println(lengths); // Output: [5, 3, 7]
    }
}
```

**Example 2: Multiply a list of numbers by 2**

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class MapExample2 {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        // Double each number
        List<Integer> doubledNumbers = numbers.stream()
                                              .map(n -> n * 2) // Multiply each number by 2
                                              .collect(Collectors.toList());

        System.out.println(doubledNumbers); // Output: [2, 4, 6, 8, 10]
    }
}
```

---

## Filter

- The `filter` method is used to select elements from a stream that match a given condition (predicate).
- It produces a new stream with only the elements that pass the test.

**Example 1: Filter even numbers from a list**

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class FilterExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);

        // Filter even numbers
        List<Integer> evenNumbers = numbers.stream()
                                           .filter(n -> n % 2 == 0) // Keep numbers divisible by 2
                                           .collect(Collectors.toList());

        System.out.println(evenNumbers); // Output: [2, 4, 6]
    }
}
```

**Example 2: Filter names starting with 'A'**

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class FilterExample2 {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Andrew", "Charlie");

        // Filter names starting with 'A'
        List<String> filteredNames = names.stream()
                                          .filter(name -> name.startsWith("A"))
                                          .collect(Collectors.toList());

        System.out.println(filteredNames); // Output: [Alice, Andrew]
    }
}
```

---

## Combining `map` and `filter`

You can chain `map` and `filter` together to perform complex operations in one pipeline.

**Example: Find the square of even numbers**

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class MapFilterExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);

        // Filter even numbers and square them
        List<Integer> squaresOfEvenNumbers = numbers.stream()
                                                    .filter(n -> n % 2 == 0) // Keep even numbers
                                                    .map(n -> n * n) // Square the even numbers
                                                    .collect(Collectors.toList());

        System.out.println(squaresOfEvenNumbers); // Output: [4, 16, 36]
    }
}
```
