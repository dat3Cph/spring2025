---
title: DAO integration test
description: How to set up a DAO test
layout: default
parent: Test
grand_parent: Toolbox
nav_order: 2
permalink: /toolbox/test/dao-test
---

# DAO Integration Test with test containers

Use this [demo code as a guideline](https://github.com/jonbertelsen/codelab_1_3sem_spring2025/tree/integrationtest) for how to setup DAO integration tests with test containers. Notice that the integration test is in the "integrationtest" branch of the repository. If you wish to follow this tutorial, then clone the main branch and go from there.

The project is setup in accordance with the [JPA setup guidelines](../java/orm/jpa_setup.md) and the example is based on this [JPA CodeLab exercise](../../jpa_part1/exercises/codelab.md).

## Video tutorial

You are welcome to follow this guided video tutorial - which contains a run-through of what comes below:

## 1. Update your `pom.xml` file

## 2. Setup a `StudentDAOTest` class skeleton

## 3. Add class variables

- EntityManagerFactory
- StudentDAO
- Testdata (s1 and s2)

## 4. Setup @BeforeEach

## 5. Setup a populator class

## 6. Fix up the `HibernateConfig` file

## 7. Add a logger to limit the log output

## 8. Create your tests one by one
