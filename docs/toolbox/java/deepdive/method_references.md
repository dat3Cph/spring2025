---
title: Method References
description: Method references in Java
layout: default
nav_order: 12
parent: Java
grand_parent: Toolbox
permalink: /toolbox/java/method-refereces/
---

# Method References

In Java, **method references**, also known as **double colon (::)** operator, are a shorthand syntax for **lambda expressions** that refer to existing methods, constructors, or instance methods of a class or object. They make the code more concise and readable by eliminating the need for explicitly writing a lambda expression when a method can directly match the required functional interface.

### **Types of Method References**

There are four main types of method references in Java:

1. **Reference to a static method**
2. **Reference to an instance method of a particular object**
3. **Reference to an instance method of an arbitrary object of a particular type**
4. **Reference to a constructor**

## **1. Reference to a Static Method**

You can reference a static method of a class using the class name.

### Syntax

```java
ClassName::staticMethodName
```

### Example

```java
import java.util.function.Function;

public class Example {
    public static void main(String[] args) {
        Function<String, Integer> parseInt = Integer::parseInt; // Static method reference
        Integer result = parseInt.apply("123"); // Equivalent to: s -> Integer.parseInt(s)
        System.out.println(result); // Output: 123
    }
}
```

---

## **2. Reference to an Instance Method of a Particular Object**

You can reference an instance method of a specific object.

### Syntax

```java
instance::instanceMethodName
```

### Example

```java
import java.util.function.Supplier;

public class Example {
    public static void main(String[] args) {
        String str = "Hello, World!";
        Supplier<String> toUpperCase = str::toUpperCase; // Instance method reference
        System.out.println(toUpperCase.get()); // Output: HELLO, WORLD!
    }
}
```

## **3. Reference to an Instance Method of an Arbitrary Object of a Particular Type**

You can reference an instance method of any object of a particular type.

### Syntax

```java
ClassName::instanceMethodName
```

### Example

```java
import java.util.Arrays;
import java.util.List;

public class Example {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

        names.forEach(System.out::println); // Instance method reference
        // Equivalent to: names.forEach(name -> System.out.println(name))
    }
}
```

## **4. Reference to a Constructor**

You can reference a constructor to create a new object.

### Syntax

```java
ClassName::new
```

### Example

```java
import java.util.function.Supplier;

public class Example {
    public static void main(String[] args) {
        Supplier<Book> bookSupplier = Book::new; // Constructor reference
        Book book = bookSupplier.get(); // Equivalent to: () -> new Book()
    }
}

class Book {
    public Book() {
        System.out.println("A new book is created!");
    }
}
```

---

## **How Method References Work**

Method references are used in conjunction with functional interfaces (interfaces with a single abstract method, e.g., `Runnable`, `Supplier`, `Consumer`, etc.). The method being referenced must match the signature of the abstract method in the functional interface.

For example:

- A `Consumer<T>` has a single method `accept(T t)`. Any method with a matching signature (e.g., `void println(String s)`) can be referenced.

## **Advantages of Method References**

1. **Readability**: Code is shorter and easier to read.
2. **Reusability**: Instead of creating new lambda expressions, existing methods can be reused.
3. **Clarity**: Clearly shows intent when referring to existing methods.

## **Lambda vs Method Reference Example**

### Using Lambda

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
names.forEach(name -> System.out.println(name));
```

### Using Method Reference

```java
names.forEach(System.out::println);
```

Both are equivalent, but the method reference is more concise and expressive.

## **Key Takeaways**

- **Method references** are syntactic sugar for lambdas when the method matches the required functional interface.
- They make the code more concise while maintaining clarity.
- Use method references when possible, but ensure the method signature matches the functional interface's method.
