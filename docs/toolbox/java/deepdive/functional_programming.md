---
title: Functional Programming
description: Theory for functional programming in Java
layout: default
nav_order: 1
parent: Java
grand_parent: Toolbox
permalink: /toolbox/java/functional-programming/
---

# Functional Programming

## **Definition of Functional Programming**

**Functional programming** is a **programming paradigm** where programs are written using functions as the primary building blocks. Instead of focusing on **state** and **sequential instructions** (as in imperative programming), functional programming emphasizes **declarative** approaches, describing **what to do** rather than **how to do it**.

---

## **Key Characteristics of Functional Programming**

1. **Functions as First-Class Citizens**

   - Functions are treated as **data**. They can be assigned to variables, passed as arguments, and returned from other functions.
   - Example in Java:

     ```java
     Function<Integer, Integer> square = x -> x * x;
     System.out.println(square.apply(5)); // Output: 25
     ```

2. **Immutability**

   - Data is **immutable**, meaning it cannot be changed after it’s created. Instead, new copies are created whenever data is "modified."
   - Example:

     ```java
     List<Integer> numbers = List.of(1, 2, 3);
     List<Integer> doubled = numbers.stream()
                                    .map(n -> n * 2)
                                    .toList();
     System.out.println(doubled); // [2, 4, 6]
     ```

3. **Side-Effect-Free Functions**

   - Functions in functional programming are often **pure functions**, meaning they have no **side effects** (they don’t modify anything outside of the function).
   - Pure functions:
     - Always return the same output for the same input.
     - Don’t change global variables or state.
   - Example:

     ```java
     int add(int a, int b) {
         return a + b; // No side effects
     }
     ```

4. **Declarative Style**

   - Programs describe **what** needs to be done, rather than specifying **how** to do it.
   - Example:
     - Imperative (procedural):

       ```java
       List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
       List<Integer> evens = new ArrayList<>();
       for (int n : numbers) {
           if (n % 2 == 0) {
               evens.add(n);
           }
       }
       System.out.println(evens);
       ```

     - Declarative (functional):

       ```java
       List<Integer> evens = numbers.stream()
                                    .filter(n -> n % 2 == 0)
                                    .toList();
       System.out.println(evens);
       ```

5. **Higher-Order Functions**
   - Functions that either **take other functions as arguments** or **return functions**.
   - Example in Java:

     ```java
     Function<Integer, Function<Integer, Integer>> adder = x -> (y -> x + y);
     System.out.println(adder.apply(3).apply(5)); // Output: 8
     ```

6. **Laziness (Lazy Evaluation)**

   - Computations are only performed when the results are actually needed.
   - Streams in Java are a great example of this feature:

     ```java
     Stream<Integer> infiniteStream = Stream.iterate(1, n -> n + 1);
     List<Integer> firstFive = infiniteStream.limit(5).toList();
     System.out.println(firstFive); // [1, 2, 3, 4, 5]
     ```

---

## **Advantages of Functional Programming**

1. **More Readable and Concise**
   - Less boilerplate code and a focus on declarative solutions make code easier to read.
2. **Easier to Debug and Maintain**
   - Immutability and pure functions reduce complexity since state doesn’t change unpredictably.
3. **Better for Parallelism**
   - Functional programming makes it easier to implement **parallel computations** because data isn’t modified by multiple threads simultaneously.
   - Example with parallel streams:

     ```java
     List<Integer> numbers = List.of(1, 2, 3, 4, 5);
     numbers.parallelStream()
            .map(n -> n * n)
            .forEach(System.out::println);
     ```

4. **Reduces Errors**
   - Pure functions and immutable data structures reduce the possibility of unintended side effects and bugs.

---

## **Examples of Functional Programming in Java**

### **Stream API**

One practical application of functional programming in Java is the **Streams API**, which allows you to work with data in a declarative manner.

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
List<String> uppercaseNames = names.stream()
                                   .map(String::toUpperCase)
                                   .filter(name -> name.startsWith("A"))
                                   .toList();
System.out.println(uppercaseNames); // [ALICE]
```

### **Using Functional Interfaces**

The key functional interfaces from the `java.util.function` package support functional programming:

- **Consumer**: Performs an action on a given input but doesn’t return anything.
- **Supplier**: Produces (returns) a value without taking any input.
- **Function**: Transforms input into output.
- **Predicate**: Tests a condition and returns `true`/`false`.

Example with `Predicate` and `Function`:

```java
Predicate<String> isShortName = name -> name.length() <= 3;
Function<String, String> greet = name -> "Hello, " + name;

System.out.println(isShortName.test("Bob")); // true
System.out.println(greet.apply("Alice"));   // Hello, Alice
```

---

## **Summary**

Functional programming in Java is about writing **cleaner**, more **declarative**, and **efficient** code using tools like **lambda expressions**, the **Streams API**, and **functional interfaces**. It introduces a new way of thinking that complements object-oriented programming and is especially powerful for handling modern, data-intensive applications.
