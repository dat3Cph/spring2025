---
title: Day 2
description: Exercise for day 2
layout: default
nav_order: 3
parent: Exercises
grand_parent: Java Deep Dive I
permalink: /deepdive-1/exercises/day-2
---

# Day 2: Generics and functional interfaces

## 1. Generics

In this exercise, you will create a generic data storage system using interfaces and classes. Your goal is to design a flexible solution that can store and retrieve data of various types while maintaining type safety.

1.1 **Create a Generic Storage Interface:**
Create a generic interface called `DataStorage<T>` that defines methods for storing and retrieving data of type `T`.

```java
interface DataStorage<T> {
    String store(T data); // return a unique ID for the stored data or the filename
    T retrieve(String source); // retrieve data from the specified source (like a file or database table or ID)
}
```

1.2 **Implement Storage Classes:**
Implement three classes that implement the `DataStorage` interface:

- `MemoryStorage<T>`: Stores data in memory.
- `FileStorage<T>`: Stores data in a file.
- `DatabaseStorage<T>`: Stores data in a database. (Only do this if you have time)

Implement the classes using appropriate data structures (e.g., instance variable, files, or database connections).

In the first instance, you can just use a String to store the data and retrieve it. If you have time, then your implementation should ensure type safety by only allowing data of the specified type to be stored and retrieved. Hint: See [this file](./day-2-hints.md#how-to-serialize-objects-in-java-and-write-them-to-a-file) for help on how to read and write objects to a file.

1.3 **Main Application:**

In the main application, create instances of each storage class and demonstrate their usage by storing and retrieving data of different types.

```java
public class DataStorageApp {
    public static void main(String[] args) {
        DataStorage<String> memoryStorage = new MemoryStorage<>();
        memoryStorage.store("Hello, world!");
        String retrievedString = memoryStorage.retrieve(null);

        DataStorage<Employee> fileStorage = new FileStorage<>();
        String filename = fileStorage.store(new Employee("John", 30));
        Employee retrievedInt = fileStorage.retrieve(filename);

        // Create and demonstrate DatabaseStorage
    }
}
```

This exercise will challenge you to design a generic solution that allows for the storage and retrieval of various types of data while maintaining type safety. It will also give you hands-on experience in working with generics in both interface declarations and class implementations.

## 2. Functional Interfaces

Now we will apply the functional interfaces from the `java.util.function` package: `Predicate`, `Consumer`, `Supplier`, `Function`:

2.1 Explain to your nabour what the following functional interfaces do: `Predicate`, `Consumer`, `Supplier`, `Function`.

2.2 Use `Predicate` to filter a list of integers, so only those divisible by 7 remain.

2.3 Use `Supplier` to create a list of Employee objects based on a list of names like `Arrays.asList("John", "Jane", "Jack", "Joe", "Jill")`.
Hint: Check these explanations and examples on [Supplier](./day-2-hints.md#supplier).

2.4 Use `Consumer` to print the list of Employee objects.

2.5 Use `Function` to convert a list of Employee objects to a list of names.

2.6 Use `Predicate`to check if a given employee is older than 18.

Check these hints for [explanations of the built-in functional interfaces](./day-2-hints.md).
