---
title: ISBN Validation in JPA
description: How to perform a unique constraint validation on an ISBN field in JPA
layout: default
nav_order: 12
parent: ORM
grand_parent: Toolbox
permalink: /toolbox/java/jpa/isbn-validation/
---

# How to Validate an ISBN in JPA?

An **ISBN (International Standard Book Number)** is a **10-digit or 13-digit number** that uniquely identifies books.  
To validate an ISBN, we need to check **its length and checksum**.

## **📌 Rules for ISBN Validation**

1. **ISBN-10 Rules:**
   - Contains **10 digits** (`0-9`).
   - The **last digit** (checksum) can be a digit (`0-9`) or `X`.
   - **Checksum formula:**  
     \[
     (1×d_1 + 2×d_2 + … + 10×d_{10}) \mod 11 = 0
     \]
   - Example: `0-306-40615-2` ✅ (valid)

2. **ISBN-13 Rules:**
   - Contains **13 digits** (`0-9`).
   - **Checksum formula:**  
     \[
     (1×d_1 + 3×d_2 + 1×d_3 + 3×d_4 + … + 3×d_{12} + d_{13}) \mod 10 = 0
     \]
   - Example: `978-3-16-148410-0` ✅ (valid)

## 📌 Java Implementation: Validate ISBN-10 and ISBN-13

```java
public class ISBNValidator {

    public static boolean isValidISBN(String isbn) {
        if (isbn == null) {
            return false;
        }
        
        isbn = isbn.replace("-", "").replace(" ", ""); // Remove hyphens and spaces

        if (isbn.length() == 10) {
            return isValidISBN10(isbn);
        } else if (isbn.length() == 13) {
            return isValidISBN13(isbn);
        } else {
            return false; // Invalid length
        }
    }

    private static boolean isValidISBN10(String isbn) {
        if (!isbn.matches("\\d{9}[\\dX]")) {
            return false; // Must be 9 digits + 1 digit/X
        }

        int sum = 0;
        for (int i = 0; i < 9; i++) {
            sum += (isbn.charAt(i) - '0') * (i + 1);
        }

        char lastChar = isbn.charAt(9);
        int lastDigit = (lastChar == 'X') ? 10 : (lastChar - '0');

        sum += lastDigit * 10;

        return sum % 11 == 0;
    }

    private static boolean isValidISBN13(String isbn) {
        if (!isbn.matches("\\d{13}")) {
            return false; // Must be exactly 13 digits
        }

        int sum = 0;
        for (int i = 0; i < 12; i++) {
            int digit = isbn.charAt(i) - '0';
            sum += (i % 2 == 0) ? digit : digit * 3;
        }

        int checksum = (10 - (sum % 10)) % 10;

        return checksum == (isbn.charAt(12) - '0');
    }

    public static void main(String[] args) {
        System.out.println(isValidISBN("0-306-40615-2")); // true (valid ISBN-10)
        System.out.println(isValidISBN("978-3-16-148410-0")); // true (valid ISBN-13)
        System.out.println(isValidISBN("123456789X")); // true (valid ISBN-10)
        System.out.println(isValidISBN("9783161484100")); // true (valid ISBN-13)
        System.out.println(isValidISBN("1234567890")); // false (invalid ISBN-10)
        System.out.println(isValidISBN("9783161484105")); // false (invalid ISBN-13)
    }
}
```

## 📌 How to Use This in a JPA Entity?

Add the validation logic in the `Book` entity:

```java
@Entity
@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
@Builder
public class Book {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String title;
    private String author;

    @Column(unique = true)
    private String isbn;

    private int publishedYear;

    @PrePersist
    @PreUpdate
    private void validateISBN() {
        if (!ISBNValidator.isValidISBN(this.isbn)) {
            throw new IllegalArgumentException("Invalid ISBN: " + this.isbn);
        }
    }
}
```
