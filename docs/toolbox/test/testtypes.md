---
title: Test Types
description: Theory about test types
layout: default
parent: Test
grand_parent: Toolbox
nav_order: 6
permalink: /toolbox/test/types
---

# Test types

## 🔲 **Black-box Testing**

**Definition**:  
Black-box testing is a method of software testing that focuses on **what the software does**, without any knowledge of the internal code or logic.

**Key points**:

- The tester only knows the **inputs and expected outputs**.
- Tests are based on **requirements and functionality**.
- Common techniques: **boundary value analysis**, **equivalence partitioning**, **state transition testing**.
- Used for **system testing**, **acceptance testing**, and often **integration testing**.

**Example**:  
Testing a login form by entering valid and invalid usernames/passwords to see if the system behaves correctly, without knowing how the authentication is implemented internally.

---

## ⚪ **White-box Testing**

**Definition**:  
White-box testing (also called **clear-box** or **glass-box** testing) is a method where the tester **has access to the internal code**, and tests are based on the internal logic and structure of the code.

**Key points**:

- The tester uses knowledge of the **source code** to design test cases.
- Focuses on **code paths**, **conditions**, **loops**, and **branches**.
- Common techniques: **statement coverage**, **branch coverage**, **path testing**.
- Often used for **unit testing** and **security testing**.

**Example**:  
Testing each possible branch of an `if` statement in a function to make sure every line of code is executed at least once.

## Comparison Black vs White testing

| Feature                      | **Black-box Testing**                           | **White-box Testing**                            |
|-----------------------------|--------------------------------------------------|--------------------------------------------------|
| **Focus**                   | Functionality / behavior                         | Internal logic / code structure                  |
| **Tester knows code?**      | ❌ No knowledge of internal code                 | ✅ Full knowledge of internal code               |
| **Test basis**              | Requirements and specifications                 | Source code, control flow, and logic             |
| **Typical use**             | System, integration, and acceptance testing     | Unit testing, sometimes integration              |
| **Test techniques**         | - Equivalence partitioning<br>- Boundary value analysis<br>- State transition | - Statement coverage<br>- Branch coverage<br>- Path testing |
| **Tools**                   | UI test frameworks, API testing tools           | Unit test frameworks, static code analyzers     |
| **Examples**                | Testing a form submission, login page, or API response | Testing all code paths in a sorting function     |
| **Best for detecting**      | Missing or incorrect functionality              | Logic errors, unreachable code, security issues  |
