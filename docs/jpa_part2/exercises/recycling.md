---
title: Recycling
description: recycling exercise
layout: default
nav_order: 1
parent: Exercises
grand_parent: JPA Part 2
permalink: part2/exercises/recycling/
---

# Recycling Exercise

### 1. Create a new JPA project using Maven

### 2. Create JPA entities for the database

- use diagram below as a reference
- the two entities should be called `Driver` and `WasteTruck`
- both entities should be placed in a package called `entities`
- the HibernateConfig class should be placed in a package called `config`
- for the salary use the type BigDecimal
- for the date use the type LocalDate
- the driver constructor should only take the name, surname and salary as a parameter
- the truck constructor should only take the brand, capacity and registration number as a parameter

![recycling erd](../../images/recycling1.png)

### 3. Validate the driver id

- Create a method in the Driver class to generate a String id with the following constrains
- The id for the driver should be a string with the format `ddMMyy-XX-XXXL`.
- `ddMMyy` is the date of employment, (Date: 2023-08-26 -> String: 230826)
- `XX` is the first letters of the name and of the surname (Name: John Doe -> String: JD)
- `XXX` is a random number between 100 and 999
- `L` is the last letter of the surname (Surname: Doe -> String: E)
- Use this method below to validate the id of the Driver class

```java
    public Boolean validateDriverId(String driverId) {
    return driverId.matches("[0-9][0-9][0-9][0-9][0-9][0-9]-[A-Z][A-Z]-[0-9][0-9][0-9][A-Z]");
    }
```

- The driver id and the employment date should be set in a @PrePersist annotated method

### 5. Create DAO interfaces for the entities

Create a new package called `daos` and add two interfaces called `IDriverDAO` and `IWasteTruckDAO` and add the following code to their interface

```java
        // Driver
        void saveDriver(String name, String surname, BigDecimal salary);
        Driver getDriverById(String id);
        Driver updateDriver(Driver driver);
        void deleteDriver(String id);
        List<Driver> findAllDriversEmployedAtTheSameYear(String year);
        List<Driver> fetchAllDriversWithSalaryGreaterThan10000();
        double fetchHighestSalary();
        List<String> fetchFirstNameOfAllDrivers();
        long calculateNumberOfDrivers();
        Driver fetchDriverWithHighestSalary();
```

```java
        // WasteTruck
        void saveWasteTruck(String brand, String registrationNumber, int capacity);
        WasteTruck getWasteTruckById(int id);
        void setWasteTruckAvailable(WasteTruck wasteTruck, boolean available);
        void deleteWasteTruck(int id);
        void addDriverToWasteTruck(WasteTruck wasteTruck, Driver driver);
        void removeDriverFromWasteTruck(WasteTruck wasteTruck, String id);
        List<WasteTruck> getAllAvailableTrucks();
```

### 6. Implement the DAO interfaces

Create a `daos/impl` package and implementent the interfaces as `DriverDAO` and `WasteTruckDAO` classes

### 7. Populate data

- Use this sql script to populate the database

```sql
-- Add 5 rows to the "truck" table
INSERT INTO truck (id, brand, capacity, is_available, registration_number)
VALUES
    (1, 'Volvo', 8000, true, 'A123-45-B6'),
    (2, 'Ford', 12000, false, 'C678-90-D1'),
    (3, 'Mercedes', 15000, true, 'E234-56-F7'),
    (4, 'BMW', 10000, false, 'G789-01-H2'),
    (5, 'Chevrolet', 17000, false, 'I345-67-J8');


-- Add 10 rows to the "driver" table
INSERT INTO driver (id, employment_date, name, surname, salary, truck_id)
VALUES
    ('230826-BD-398E', '2023-08-26', 'John', 'Doe', 12550, 1),
    ('200512-AD-786M', '1995-05-12', 'Alice', 'Smith', 18550, 2),
    ('211104-CE-572S', '1996-11-04', 'Charlie', 'Evans', 21800, 3),
    ('201217-GK-123D', '1997-12-17', 'Grace', 'Kelly', 52000, 4),
    ('220609-MP-456H', '1998-06-09', 'Michael', 'Parker', 31200, 5),
    ('200821-FR-892L', '1999-08-21', 'Frank', 'Roberts', 28500, 4),
    ('230531-WT-642B', '2023-05-31', 'William', 'Turner', 65800, 3),
    ('230304-LH-718R', '2023-03-04', 'Laura', 'Harris', 8500, 3),
    ('230925-SJ-599M', '2023-09-25', 'Sarah', 'Johnson', 16500, 5),
    ('211128-PT-347S', '2000-11-28', 'Peter', 'Taylor', 33000, 1);

```

### 8. Create a main method

In the root of the project, create a `Main` class with a main method that runs a few of your DAO methods to test that they work. Save your time for the next exercise. It's only to get started.

### 9. Create integration tests

This is a big deal. You need to test all the methods in the DAO classes using JUnit.

Use this [integration test tutorial](../../toolbox/test/dao_test.md) to help you get going.
