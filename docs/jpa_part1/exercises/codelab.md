---
title: CodeLab
description: JPA part 1 CodeLab Exercise
layout: default
nav_order: 2
parent: Exercises
grand_parent: JPA Part 1
permalink: /jpa-part-1/exercises/codelab/
---

# JPA part I - CodeLab Exercise

This CodeLab exercise is designed to help you practice the concepts you have learned in the JPA 1 module on day 1. You will be working on a series of tasks that involve Java Persistence API, with Entities and DAOs. We will also practice [pair programming](../../toolbox/sys/projectmanagement/pairprogramming.md) if possible.

![Pair programming](../../deepdive-1/exercises/images/pairprogramming.gif)

## Exercise Overview

## Instructions

### 1. Team up with a buddy

- Help each other working together in pairs

### 2. Setup the development environment (everyone)

1. Create a new Maven project getting ready for JPA with Hibernate. Use the [JPA setup in IntelliJ](../../toolbox/java/orm/jpa_setup.md) guide to help you - or use your own starter project / template.
2. Make sure your `.gitignore` file is set up correctly and then initialize a new Git repository in your project folder. Add and commit your files.
3. Create a new repository on GitHub, link them up, and push your project to the repository.

### 3. Connecting to the database

1. Each person should create a database in your docker environment with Postgres called `jpademo`.
2. Set up the Hibernate to connect to the database. Use the `config.properties` file to store the database name - and credentials.
3. Create a new Entity class called `Person` with the following fields:
   - id (int)
   - name (String)
   - age (int)
4. Create a new DAO class called `PersonDAO` with the following methods:

- `createPerson(Person person)`

5. Create a new Main class and test that you can add a new person to your database.

### 4. The assignment

You are going to create a new student management system. We need to be able to persist data about students and their courses.
We need to have information about each student such as their name, phone number, email, address, status, date of birth, date of enrollment and whatever you think is relevant. We also need to have information about the courses they are taking such as the name of the course, the teacher, the semester, the classroom, the time of the course and whatever you think is relevant.
Since we have not yet learned how to create relationships/references between entities, you can choose to just store the id of the courses in the student entity for now (we will learn how to do it the right way in **JPA week 2**).

### 5. Identify tasks, break them down and assign to pair programmers as Issues in Github

The following tasks are suggestions for the first round of tasks. You can add more tasks as you go along.

1. Create new student
2. Create new course
3. Update student information
4. Update course information
5. Delete student
6. Delete course
7. List all students
8. List all courses
9. List all courses for a specific student
10. List all students for a specific course (use streams and filters for this one)
11. Come up with more tasks as you go along ...

### 6. Start working on the tasks (round 1)

1. Create a feature branch off the `main` branch for each task
2. Work on the tasks in pairs

### 7. Merge your feature branch in to the `main` branch

1. After completing the task, add, commit, and push your changes to the repository
2. Switch to the main branch - and merge the latest changes from the feature branch.

### 8. Repeat

1. Identify the next tasks
2. Repeat steps 6-7 for the next tasks
