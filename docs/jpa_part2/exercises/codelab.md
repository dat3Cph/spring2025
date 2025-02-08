---
title: CodeLab
description: JPA part 2 CodeLab Exercise
layout: default
nav_order: 2
parent: Exercises
grand_parent: JPA Part 2
permalink: /jpa-part-2/exercises/codelab/
---

# JPA part II - CodeLab Exercise

This CodeLab exercise is designed to help you practice the concepts you have learned on the first day of JPA part 2. You will be working on a series of tasks that involve Java Persistence API, with Entities and DAOs. We will also practice [pair programming](../../toolbox/sys/projectmanagement/pairprogramming.md) and using Git and GitHub for version control.

![Pair programming](../../deepdive-1/exercises/images/pairprogramming.gif)

## Exercise Overview

![codelab_school_exercise](codelab_school_exercise.drawio.png)

## Instructions

### 1. Team up (2 x 2)

### 2. Remember to mark your attendance in Moodle (for getting study points)

### 3. Set up the development environment (one per team of 2 x 2)

1. Create a new Maven project getting ready for JPA with Hibernate. Use the [JPA setup in IntelliJ](../../toolbox/java/orm/jpa_setup.md) guide to help you - or use your own starter project / template.
2. Make sure your `.gitignore` file is set up correctly and then initialize a new Git repository in your project folder. Add and commit your files.
3. Create a new branch: `develop`.
4. Create a new repository on GitHub, link them up, and push your project to the repository.
5. Every team member should clone the new repository to their local machine
6. Checkout the develop branch (each member).

### 3. Connecting to the database

1. Each member should create a database in your docker environment with postgres called `university`.
2. Set up `config.properties` with the database name, so Hibernate can connect to the database.

### 4. The assignment

You are going to create a simple application for a university. The application should be able to manage students, courses and teachers. This time around we are going to add relationships between the entities. The relationships can be seen in the diagram above.
Most of the code is already written for you. You need to implement the missing parts. Make sure to use the correct annotations for the relationships and try to understand how the relationships work.

**Remember to write integration tests for the DAO classes.**

Ask yourself the following questions before you start implementing the relationships:

- What are the relationship between the entities?
- Which one should be the owning side of the relationship and what does that mean?
- Should the relationship be unidirectional or bidirectional?
- What cascade type should be used or should we use them at all? What are the implications?
- Should we use fetch type eager or lazy and why?

### 5. Identify tasks, break them down and assign to pair programmers as Issues in Github

The following tasks are suggestions for the first round of tasks. You can add more tasks as you go along.

1. Create an Enum for the Course class as shown in the diagram and add the correct annotations to the Course class.
2. Add the correct annotations to the Teacher class as shown in the diagram.
3. Add the correct annotations to the Student class as shown in the diagram.
4. Implement the GenericDAO interface for the CourseDAO class and implement the methods.
5. Implement the GenericDAO interface for the TeacherDAO class and implement the methods.
6. Implement the GenericDAO interface for the StudentDAO class and implement the methods.
7. Add the relations between the entities as shown in the diagram.
   - a) student can attend many courses
   - b) a course can have many students
   - c) course can have only one teacher
   - d) a teacher can teach many courses
8. Look at the [DTO](../../toolbox/designpatterns/dto.md) diagram below and implement the methods in the DAO classes to get the data as shown in the diagram.

![codelab_school_dto](codelab_school_dto.drawio.png)

### 6. Start working on the tasks (round 1)

1. Create a branch off the `develop` branch for each task
2. Work on the tasks in pairs

### 7. Reviewing and merging the feature branch

1. When you tiny team is happy with the implementation of the feature, merge the feature branch into the `develop` branch and push it to the repository and Github.

### 8. Repeat

1. Identify the next tasks
2. Repeat steps 5-7 for the next tasks
