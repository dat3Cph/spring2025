---
title: GLS Part 1
description: gls exercise part 1
layout: default
nav_order: 1
parent: Exercises
grand_parent: JPA Part 1
permalink: /jpa-part-1/exercises/gls-part1/
---

## Exercise: GLS Package Tracking System - Part 1

![](../../images/glsbear.png){: style="width:50%" }

### Scenario

GLS (Global Logistics Services) wants to develop a package tracking system to manage the delivery of packages. As part of the initial phase, they need to create a basic system using Java, JPA, and JPQL to manage package information.

### Requirements

1. Create an entity named "Package" using Lombok to manage package information. The "Package" entity should have the following attributes:
    - ID (auto-generated primary key)
    - Tracking number (String)
    - Sender name (String)
    - Receiver name (String)
    - Delivery status (Enum: PENDING, IN_TRANSIT, DELIVERED)
    - Updated (LocalDateTime) for last time the package was updated

2. Create a DAO (Data Access Object) class named "PackageDAO" to perform CRUD operations on the "Package" entity using JPA.

3. Implement methods in the "PackageDAO" to perform the following operations:
    - Persist a new package
    - Retrieve a package by its tracking number
    - Retrieve all packages in the system
    - Update the delivery status of a package
    - Remove a package from the system

4. Define pre-update and pre-persist life cycle methods in the "Package" entity to update the last updated timestamp automatically.

5. Write integration tests for the DAO methods to ensure they work correctly. Use test containers.

6. Use Maven for project management.

### Hints

- Use Jakarta Persistence (JPA) annotations to map the entity attributes to database columns.
- Implement JPQL queries for retrieving packages based on certain criteria, such as tracking number or delivery status.

### JUnit / Integration test example

On 3rd semester we will create integration tests for DAO methods. It's a bad idea to run tests on the production database itself. To
avoid that, we use a new Docker container with Postgresql. It called a "test container". We have made a [DAO integration test tutorial in the Toolbox](../../toolbox/test/dao_test.md).

### Expected Outcome

This exercise should provide a solid foundation for understanding JPA (ORM) and JPQL in the context of building a package tracking system. Also, you will get your first introduction to integration testing. Next week - in part 2, you will be introduced to more complex relationships between entities to further enhance the system.
