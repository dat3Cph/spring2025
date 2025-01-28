---
title: CodeLab
description: Deep Dive I CodeLab Exercise
layout: default
nav_order: 4
parent: Exercises
grand_parent: Java Deep Dive I
permalink: /deepdive-1/exercises/codelab/
---

# Deep Dive I CodeLab Exercise

Work in progress ....

This CodeLab exercise is designed to help you practice the concepts you have learned in the Java Deep Dive I module on day-1. You will be working on a series of tasks that involve Java Streams, Java Time API, and Lambdas. We will also practice [pair programming](../../toolbox/sys/projectmanagement/pairprogramming.md) and using Git and Github. Make an effort to use Git on the command line as much as possible (Git Bash / Terminal) to get more comfortable with it. Check git help in the bottom of this page for more information.

![Pair programming](./images/pairprogramming.gif)

## Exercise Overview

## Instructions

### 1. Team up

1. Team up in pairs of 2

### 2. Setup the development environment (one per team)

1. One team member should fork [Flight data Repo](https://github.com/dat3Cph/flightapp) onto their own Github account. The **Flight data Repo** is a simple application that reads a CSV file with flight data and calculates the total flight time for each airline.
2. Add the other team member as collaborators to the forked repository
3. Both team members should clone the forked repository to their local machine
4. Open the project in IntelliJ IDEA
5. Make sure that the project builds and runs without errors. If you have issues, make sure that all Maven dependencies are downloaded and that the project SDK is set to Java 17

### 3. Get aqainted with the code

1. Run the application (find the Main class in `FlightReader`) and see how it works
2. Look at the code and understand how it works. How does the duration of the flights get calculated and more? You might want to
know more about the [Lombok library](../../toolbox/java/deepdive/lombok.md) and how it is used in the code to simplify getters, setters etc.
3. Look at the `json` file and discuss the structure of the data with your team
4. Make sure that the data in the `json` file correlates with the data printed in the console
5. Find the unit-test and run it.
6. See if you can understand the test and what it is testing. Could it be improved?

### 4. Identify tasks, break them down and prioritize

Inspiration for first round tasks:

1. Add a new feature (e.g. calculate the **total flight time** for a specifc airline. For example, calculate the total flight time for all flights operated by Lufthansa)

### 5. Start working on the tasks (round 1)

1. Create a branch off the `main` branch for each task. Call it something like `round-1`
2. Work on the tasks together using pair programming. Let one person code and the other navigate and ask questions

### 6. Merge the code

1. Merge the `round-1` branch into the main branch:
   - On the `round-1` branch: add the changes to the staging area, then you commit the changes
   - Checkout the main branch and merge the `round-1` branch into it.
2. Remove the `round-1` branch
3. Add, commit, and push the changes from `main` to the remote repository and let the other team member pull the changes. Make sure that the code works as expected
4. Check that both team members have the latest changes

### 7. Repeat

1. Identify the next tasks (get inspiration from the list below)
2. Repeat steps 5-7 for the next tasks and swap roles each round

## Inspiration for tasks

1. Add a new feature (e.g. calculate the **average flight time** for a specific airline. For example, calculate the average flight time for all flights operated by Lufthansa)
2. Add a new feature (make a list of flights that are operated between two specific airports. For example, all flights between Fukuoka and Haneda Airport)
3. Add a new feature (make a list of flights that leaves before a specific time in the day/night. For example, all flights that leave before 01:00)
4. Add a new feature (calculate the average flight time for each airline)
5. Add a new feature (make a list of all flights sorted by arrival time)
6. Add a new feature (calculate the total flight time for each airline)
7. Add a new feature (make a list of all flights sorted by duration)
8. Refactor the code where needed. Make sure that the code is clean and easy to read.

## How to use git in the terminal for round-1

### Create a branch and switch to it

```bash
    git branch round-1
    git checkout round-1
```

### Add the changes to the staging area and commit the changes

```bash
    git add .
    git commit -m "Add feature to calculate the total flight time for a specific airline"
```

### Merge the `round-1` branch into the `main` branch

```bash
    git checkout main
    git merge round-1
```

### Remove the `round-1` branch (no longer needed)

```bash
    git branch -d round-1
```

### Push the changes to the remote repository

```bash
    git push
```
