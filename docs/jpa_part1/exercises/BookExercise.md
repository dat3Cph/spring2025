---
title: Books
description: books exercise
layout: default
nav_order: 1
parent: Exercises
grand_parent: JPA Part 1
permalink: /jpa-part-1/exercises/books/
---

# JPA Book Exercise

## Exercise 1: Mapping Entities and Annotations

**Objective:** Apply JPA annotations to map Java classes to database tables and understand entity lifecycle.

1. **Set Up a Java Project:**  
   - Create a new **Maven** project. Use [JPA starter](../../toolbox/java/orm/jpa_setup.md) if needed.

2. **Define the `Book` Entity:**  
   - Create a simple entity class called **`Book`** with the following attributes:
     - `id` (primary key)
     - `title`
     - `author`
     - `isbn` (must be unique)
     - `publishedYear`
   - Use JPA annotations to **map the entity class to a database table** named **`books`**.
   - Ensure the `isbn` field is **unique**.
   - Include **a no-arg constructor** (`@NoArgsConstructor`).
   - Add **Lombok annotations** like `@Getter`, `@Setter`, `@ToString`, and `@Builder`.

3. **Add JPA Annotations:**
   - Use `@Entity`, `@Table`, `@Id`, `@GeneratedValue`, and `@Column` to define the primary key and attribute mappings.

4. **Set Up the `Main` Class:**
   - Add a **static property**: `EntityManagerFactory`.
   - Create methods for **CRUD operations** in a `BookDAO` class:

   - `public static void createBook(Book book)`  
     - This method **persists** a new book to the database.

   - `public static Book readBook(int id)`  
     - This method retrieves a **book by ID**.

   - `public static Book updateBook(Book updatedBook)`  
     - This method **updates** an existing book.

   - `public static void deleteBook(int id)`  
     - This method **deletes** a book by ID.

   - `public static List<Book> readAllBooks()`  
     - This method retrieves **all books** from the database using a `TypedQuery`.

5. **Use `try-with-resources` or `finally` blocks** to properly close `EntityManager` objects.

6. **Add JPA Entity Lifecycle Comments**  
   - Add comments explaining **when an entity is in**:
     - **Transient State** (before persist)
     - **Managed State** (after persist)
     - **Detached State** (after transaction commit)
     - **Removed State** (before deletion)

   Example:

   ```java
   public static void main(String[] args) {
       // Entity is in transient state
       Book book = new Book("Effective Java", "Joshua Bloch", "9780134685991", 2018);
   }

   public static void createBook(Book book) {
       try (EntityManager em = emf.createEntityManager()) {
           em.getTransaction().begin();
           // Entity is in managed state after persist()
           em.persist(book);
           // Entity becomes detached after transaction is committed
           em.getTransaction().commit();
       }
   }
   ```

7. **Validate ISBN Before Persisting a Book**
   - Add a method in the `Book` class to verify that the **ISBN is valid**.
   - Use `@PrePersist` to **validate ISBN** before saving a book.
   - If ISBN is invalid, throw an **exception**.
   - Add a `@PreUpdate` method to **validate ISBN before updating**.
   - Hint: Use the `ISBNValidator` class from the [ISBN validation exercise](../../toolbox/java/orm/jpa_isbn_validation.md)

8. **Create a Test Class**
   - Add a test class that contains a **test method for each CRUD operation**.

9. **Populate the Database with Books**
   - Add 10 books to the database
   - At least 3 books should be authored by "J.K. Rowling"
   - At least 4 books should be authored by "George Orwell"
   - The oldest book should be from 1945
   - The most recent book should be from 2024

10. **Aggregate Data with Queries**
    - Calculate the average publication year of all books
    - Find the average publication year of books authored by "George Orwell"
    - Count how many books are authored by "J.K. Rowling"
    - Find the title of the oldest book** in the database.
    - Retrieve the most recently published book
    - Sum the publication years of all books

## Exercise 2: Q & A

1. Why do we need a **no-arg constructor** in an entity class?
2. Investigate where in the code we can:
   - Specify the **database dialect**?
   - Define **JDBC connection properties**?
   - Add **annotated classes**?
3. What is the purpose of `@GeneratedValue`?  
   - What are the **different primary key generation strategies** in JPA?
4. What is **`try-with-resources`**, and how can we use it in JPA?
5. What is the difference between `persist()` and `merge()` in JPA?
6. What is the difference between `TypedQuery` and `Query`?
7. What is the difference between `getSingleResult()` and `getResultList()`?
8. What are the **different states** of an entity in JPA?
