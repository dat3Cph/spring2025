---
title: JPA One-To-One
description: crud examples 
layout: default
nav_order: 5
parent: ORM
grand_parent: Toolbox
permalink: /toolbox/java/jpa/one-to-one/
---

# JPA - One-To-One associations explained

In JPA (Java Persistence API), a one-to-one association is a type of relationship between two entities where each instance of one entity is associated with exactly one instance of another entity. This relationship is represented using the `@OneToOne` annotation.

## Key Points to Understand

1. **Cardinality**:
   - In a one-to-one relationship, each entity has a single corresponding entity. For example, if you have a `Person` entity and a `Passport` entity, each `Person` can have only one `Passport`, and each `Passport` can be assigned to only one `Person`.

2. **Owning vs. Non-Owning Side**:
   - **Owning Side**: The entity that contains the foreign key is considered the owning side of the relationship. This entity's table will have the column that refers to the primary key of the other entity.
   - **Non-Owning (Inverse) Side**: The other entity that does not contain the foreign key. This entity maps the relationship using the `mappedBy` attribute in the `@OneToOne` annotation.

3. **Bidirectional and Unidirectional Relationships**:
   - **Unidirectional**: Only one entity is aware of the relationship. This means only one entity has the `@OneToOne` annotation, and the other entity has no reference to the relationship.
   - **Bidirectional**: Both entities are aware of the relationship. Each entity will have a reference to the other entity, and both will use the `@OneToOne` annotation.

4. **Cascade Type**:
   - Cascade operations can be applied to propagate operations (like persist, remove) from one entity to another. This is often used in one-to-one relationships to manage both entities together.

5. **Fetch Type**:
   - By default, one-to-one relationships use `FetchType.EAGER`, meaning the related entity is fetched immediately along with the owner entity. However, you can change this to `FetchType.LAZY` if you want to load the related entity on demand.

## Example

Let's consider an example where we have two entities: `Person` and `Passport`.

We wille be using the `@MapsId` annotation, where a `Person` entity has a **one-to-one** relationship with a `Passport` entity.

### Explanation of `@MapsId`

- The `@MapsId` annotation maps the primary key of the child (`Passport`) to the primary key of the parent (`Person`).
- This enforces that **both entities share the same primary key**.
- The `Passport` entity doesn't have its own generated ID but instead **inherits the ID from `Person`**.

Here's the same **JPA One-to-One relationship** using `@MapsId`, but now with **Lombok** to simplify the entities. This reduces boilerplate code by automatically generating constructors, getters, setters, `toString()`, `equals()`, and `hashCode()`.

### **Person.java**

```java
import jakarta.persistence.*;
import lombok.*;

@Entity
@Table(name = "person")
@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
@ToString(exclude = "passport") // Avoid circular reference in toString()
public class Person {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @OneToOne(mappedBy = "person", cascade = CascadeType.ALL, orphanRemoval = true)
    private Passport passport;

    public Person(String name) {
        this.name = name;
    }

    public void setPassport(Passport passport) {
        this.passport = passport;
        passport.setPerson(this); // Maintain bidirectional relationship
    }
}
```

### **Explanation**

1. **JPA Annotations**
   - `@Entity`: Marks this class as a JPA entity.
   - `@Table(name = "person")`: Maps this entity to the **person** table in the database.
   - `@Id`: Marks the `id` field as the **primary key**.
   - `@GeneratedValue(strategy = GenerationType.IDENTITY)`:
     - Uses the database's identity column for **automatic primary key generation**.
     - Suitable for databases like MySQL and PostgreSQL.
   - `@OneToOne(mappedBy = "person", cascade = CascadeType.ALL, orphanRemoval = true)`:
     - Declares a **one-to-one** relationship with `Passport`.
     - `mappedBy = "person"`: The **`person` field** in `Passport` owns the relationship.
     - `cascade = CascadeType.ALL`: Any operations (persist, remove, merge) on `Person` **cascade to `Passport`**.
     - `orphanRemoval = true`: If a `Person` loses its `Passport`, the `Passport` **is automatically deleted**.

2. **Lombok Annotations**
   - `@Getter @Setter`: Automatically generates **getter and setter methods**.
   - `@NoArgsConstructor`: Generates a **default constructor**.
   - `@AllArgsConstructor`: Generates a **constructor with all fields**.
   - `@ToString(exclude = "passport")`: **Prevents infinite recursion** in `toString()` (since `Person` and `Passport` reference each other).

3. **Custom `setPassport()` Method**
   - Ensures **both entities maintain a bidirectional relationship**.
   - `passport.setPerson(this);` ensures that the `Passport` correctly references its `Person`.

---

### **Passport.java**

```java
import jakarta.persistence.*;
import lombok.*;

@Entity
@Table(name = "passport")
@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
@ToString(exclude = "person") // Avoid circular reference in toString()
public class Passport {

    @Id
    private Long id; // Uses the same ID as the Person entity

    private String passportNumber;

    @OneToOne
    @MapsId // Uses the same primary key as Person
    @JoinColumn(name = "id")
    private Person person;

    public Passport(String passportNumber) {
        this.passportNumber = passportNumber;
    }
}
```

### **Explanation**

1. **JPA Annotations**
   - `@Entity`: Marks `Passport` as a JPA entity.
   - `@Table(name = "passport")`: Maps to the **passport** table.
   - `@Id private Long id;`: Uses the **same primary key as Person**.
   - `@OneToOne`:
     - Defines a **one-to-one** relationship with `Person`.
   - `@MapsId`: **Maps `id` to the primary key of `Person`**.
     - `Passport` does **not** have its own ID.
     - Instead, it **shares the same ID as its `Person`**.
   - `@JoinColumn(name = "id")`:
     - Specifies that the `id` column **links to the primary key of Person**.

2. **Lombok Annotations**
   - `@Getter @Setter`: Automatically generates **getter and setter methods**.
   - `@NoArgsConstructor`: Generates a **default constructor**.
   - `@AllArgsConstructor`: Generates a **constructor with all fields**.
   - `@ToString(exclude = "person")`: Prevents **infinite recursion** in `toString()`.

---

## **3. Creating and Persisting Data**

### **Main.java**

```java
public class Main {
    public static void main(String[] args) {
      EntityManagerFactory emf = HibernateConfig.createEntityManagerFactory();
        EntityManager em = emf.createEntityManager();
        EntityTransaction tx = em.getTransaction();

        try {
            tx.begin();

            // Create Person
            Person person = new Person("John Doe");

            // Create Passport
            Passport passport = new Passport("ABC123456");

            // Establish relationship
            person.setPassport(passport);

            // Persist Person (Passport will be automatically persisted due to CascadeType.ALL)
            em.persist(person);

            tx.commit();

            // Fetch and print data
            Person retrievedPerson = em.find(Person.class, person.getId());
            System.out.println("Person: " + retrievedPerson);
            System.out.println("Passport Number: " + retrievedPerson.getPassport().getPassportNumber());

        } catch (Exception e) {
            if (tx != null && tx.isActive()) {
                tx.rollback();
            }
            e.printStackTrace();
        } finally {
            em.close();
            emf.close();
        }
    }
}
```

### **Explanation**

1. **EntityManager Setup**
   - `EntityManagerFactory emf = HibernateConfig.createEntityManagerFactory();`
   - `EntityManager em = emf.createEntityManager();`
   - Manages **database operations**.

2. **Transaction Handling**
   - `tx.begin();`: Starts a new **transaction**.
   - `tx.commit();`: Commits changes to the database.
   - If an exception occurs, `tx.rollback();` is executed.

3. **Creating and Persisting Entities**
   - Creates a `Person` named `"John Doe"`.
   - Creates a `Passport` with number `"ABC123456"`.
   - Calls `person.setPassport(passport);` to **establish the relationship**.
   - Calls `em.persist(person);` to save `Person` (automatically persists `Passport` due to **CascadeType.ALL**).

4. **Retrieving and Printing Data**
   - Retrieves the `Person` from the database.
   - Prints `Person` and their **associated `Passport` number**.

---

## **4. Database Schema (Generated by Hibernate)**

The generated schema will look like this:

### **Person Table**

| id  | name     |
|-----|---------|
| 1   | John Doe |

### **Passport Table**

| id  | passport_number |
|-----|----------------|
| 1   | ABC123456      |

- The **`id` of `passport` is the same as the `id` of `person`** (due to `@MapsId`).
- This ensures a **One-to-One relationship with shared primary keys**.

---

## **Key Takeaways**

1. **One-to-One Relationship**:
   - `@OneToOne(mappedBy = "person")` in `Person.java`.
   - `@OneToOne @MapsId` in `Passport.java` to share **the same primary key**.

2. **Cascade & Orphan Removal**:
   - `CascadeType.ALL`: Automatically saves/deletes the associated `Passport` when `Person` is modified.
   - `orphanRemoval = true`: If a `Person` is deleted or loses their `Passport`, the `Passport` is also deleted.

3. **Lombok Simplifications**:
   - `@Getter`, `@Setter`, `@NoArgsConstructor`, `@AllArgsConstructor`, and `@ToString
