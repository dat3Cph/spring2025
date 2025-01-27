---
title: Lamdas and Streams
description: Lamda and Streams exercises
layout: default
nav_order: 1
parent: Exercises
grand_parent: Java Deep Dive I
permalink: /deepdive-1/exercises/lamdas-streams/
---

# Exercises for Introducing Lambdas and streams in Java

These exercises are designed to gradually introduce students to **lambdas** in Java, starting from the basics and progressing to more practical use cases like the Streams API and functional interfaces.

## **1. Basic Lambda Syntax**

### **Exercise 1: Write Your First Lambda**

Rewrite the following code using a lambda expression:

```java
Runnable runnable = new Runnable() {
    @Override
    public void run() {
        System.out.println("Hello, world!");
    }
};
runnable.run();
```

**Goal**: Replace the anonymous class with a lambda expression.  
**Hint**: Use the `Runnable` functional interface.

---

### **Exercise 2: Lambda with Parameters**

Write a lambda expression that takes a string as input and prints it in uppercase. Use this functional interface:

```java
@FunctionalInterface
interface Printer {
    void print(String message);
}

public class Main {
    public static void main(String[] args) {
        Printer printer = ...; // Write the lambda here
        printer.print("hello");
    }
}
```

**Goal**: Replace the `...` with a lambda to convert and print the input in uppercase.

---

## **2. Functional Interfaces**

### **Exercise 3: Using `Consumer`**

Use the `Consumer<T>` functional interface to create a lambda that prints each element in a list:

```java
import java.util.function.Consumer;
import java.util.Arrays;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

        Consumer<String> printer = ...; // Write the lambda here

        names.forEach(printer);
    }
}
```

**Goal**: Replace `...` with a lambda that prints each name.

---

### **Exercise 4: Using `Function`**

Use the `Function<T, R>` functional interface to create a lambda that doubles an integer:

```java
import java.util.function.Function;

public class Main {
    public static void main(String[] args) {
        Function<Integer, Integer> doubler = ...; // Write the lambda here

        System.out.println(doubler.apply(5)); // Should print 10
    }
}
```

**Goal**: Replace `...` with a lambda that doubles the input.

---

### **Exercise 5: Using `Predicate`**

Use the `Predicate<T>` functional interface to filter a list of numbers:

```java
import java.util.function.Predicate;
import java.util.Arrays;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);

        Predicate<Integer> isEven = ...; // Write the lambda here

        numbers.stream()
               .filter(isEven)
               .forEach(System.out::println); // Should print 2, 4, 6
    }
}
```

**Goal**: Replace `...` with a lambda that checks if a number is even.

---

## **3. Lambdas in Practice**

### **Exercise 6: Sorting with Lambdas**

Sort a list of strings by their lengths using a lambda expression:

```java
import java.util.Arrays;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<String> words = Arrays.asList("apple", "banana", "kiwi", "cherry");

        // Write the lambda inside the sort method
        words.sort(...);

        System.out.println(words); // Should print [kiwi, apple, banana, cherry]
    }
}
```

**Goal**: Replace `...` with a lambda that sorts the words by length.

[Hints for soring with lambdas](https://www.baeldung.com/java-8-sort-lambda)

---

### **Exercise 7: Map and Transform**

Use a lambda expression with the `map` method to convert a list of integers to their squares:

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class Main {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        List<Integer> squares = numbers.stream()
                                       .map(...) // Write the lambda here
                                       .collect(Collectors.toList());

        System.out.println(squares); // Should print [1, 4, 9, 16, 25]
    }
}
```

**Goal**: Replace `...` with a lambda that calculates the square of each number.

[Hint: map](../../toolbox/java/deepdive/map_and_filter.md#map)

---

### **Exercise 8: Combine `filter` and `map`**

Filter all even numbers from a list and double them using lambdas:

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class Main {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);

        List<Integer> result = numbers.stream()
                                      .filter(...) // Filter even numbers
                                      .map(...)    // Double the numbers
                                      .collect(Collectors.toList());

        System.out.println(result); // Should print [4, 8, 12]
    }
}
```

[Hint: filter](../../toolbox/java/deepdive/map_and_filter.md#filter)

**Goal**: Replace `...` in `filter` and `map` with appropriate lambdas.

---

## **4. Advanced Exercises**

### **Exercise 9: Custom Functional Interface**

Create a custom functional interface to calculate the area of a rectangle:

```java
@FunctionalInterface
interface AreaCalculator {
    int calculate(int length, int width);
}

public class Main {
    public static void main(String[] args) {
        AreaCalculator calculator = ...; // Write the lambda here

        System.out.println(calculator.calculate(5, 3)); // Should print 15
    }
}
```

**Goal**: Replace `...` with a lambda to compute the area of a rectangle.

---

### **Exercise 10: Chain Functions**

Chain two functions using `andThen` to first double a number and then add 5:

```java
import java.util.function.Function;

public class Main {
    public static void main(String[] args) {
        Function<Integer, Integer> doubler = ...; // Lambda to double a number
        Function<Integer, Integer> addFive = ...; // Lambda to add 5

        Function<Integer, Integer> combined = doubler.andThen(addFive);

        System.out.println(combined.apply(10)); // Should print 25
    }
}
```

**Goal**: Write lambdas for `doubler` and `addFive`, then combine them using `andThen`.

---

### **Exercise 11: Parallel Streams with Lambdas**

Use a parallel stream to calculate the sum of squares of a list of integers:

```java
import java.util.Arrays;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        int sumOfSquares = numbers.parallelStream()
                                  .mapToInt(...) // Write the lambda here
                                  .sum();

        System.out.println(sumOfSquares); // Should print 55
    }
}
```

**Goal**: Replace `...` with a lambda that squares each number.
