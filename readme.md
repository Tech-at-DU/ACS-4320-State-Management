

# ACS 4320 - State Management

## Course Description

This course explores how modern applications manage state as complexity grows. Students will study the patterns and tools used to coordinate application data, user interactions, and UI updates.

The course focuses on state management in JavaScript applications built with React. Students will learn how local component state evolves into shared application state and how to organize that state using modern patterns and tools such as reducers and centralized stores.

Throughout the course students will build progressively more complex applications while refactoring earlier designs to improve clarity, maintainability, and scalability.

### Why you should know this

Managing state is one of the hardest problems in modern software development.

Small applications can often rely on simple local state, but as applications grow, state quickly becomes difficult to reason about. Data must be shared between components, synchronized with the UI, and updated predictably when users interact with the application.

Without clear patterns for managing state, applications become fragile, hard to maintain, and difficult to extend.

Understanding state management allows you to:

- build scalable front-end architectures
- reason about complex UI behavior
- organize application data in predictable ways
- collaborate effectively on large codebases

State management is a core skill for professional front-end developers.

---

## Prerequisites

- [ACS 3330](https://github.com/Tech-at-DU/ACS-3330-Single-Page-Applications)

---

## Learning Outcomes

By the end of the course, you will be able to:

1. Identify different types of state within a web application
2. Manage component state using React hooks
3. Refactor local state into shared application state
4. Implement predictable state updates using reducer patterns
5. Use centralized state management libraries
6. Design maintainable state architectures for medium-sized applications
7. Debug state-related bugs and reason about UI state flow

---

## Schedule

**Course Dates:** _(update to match semester)_

**Class Times:** Monday, Wednesday 1:00 PM – 3:45 PM Virtual online.

| Class | Date | Topics | Assignment |
|:------|:-----|:-------|:-----------|
|  -    | **Week 1** | - | - |
| 1 | Mon, Mar 23| What is State? | |
| 2 | Wed, Mar 25 | Local Component State | [Assignment 1 – Local State Task App] |
|  -    | **Week 2** | - | - |
| 3 | Mon, Mar 30 | Derived State | |
| 4 | Wed, Apr  1 | State and Component Architecture | |
|  -    | **Week 3** | - | - |
| 5 | Mon, Apr  6 | Lifting State | |
| 6 | Wed, Apr  8 | Prop Drilling and Data Flow | [Assignment 2 – Refactor State Architecture] |
|  -    | **Week 4** | - | - |
| 7 | Mon, Apr 13 | Reducer Pattern | |
| 8 | Wed, Apr 15 | useReducer | |
|  -    | **Week 5** | - | - |
| 9 | Mon, Apr 20 | Global State Concepts | |
|10 | Wed, Apr 22 | Context API | [Assignment 3 – Shared State App] |
|  -    | **Week 6** | - | - |
|11 | Mon, Apr 27 | Redux and State Stores | |
|12 | Wed, Apr 29 | Redux Toolkit | |
|  -    | **Week 7** | - | - |
|13 | Mon, May  4 | State Architecture Patterns | |
|14 | Wed, May  6 | Debugging and Refactoring State | |
|  -    | **Week 8** | - | - |
|15 | Mon, May 11 | Final Project Work | |
|16 | Mon, May 13 | Final Presentations | Final Project |

---

## Homework

During the course you will build and refactor several applications focused on managing state complexity.

1. **Assignment 1 – Local State Application**  
   Build a React application using only local component state.

2. **Assignment 2 – Refactoring State Architecture**  
   Refactor your application to reduce duplication and improve data flow.

3. **Assignment 3 – Shared State Application**  
   Implement shared state using Context or reducer patterns.

4. **Final Project – Application State Architecture**  
   Design and implement a medium-sized application demonstrating clear state organization.

Assignments should be submitted through GradeScope.

Each assignment builds on previous work and introduces new architectural challenges.

---

## Evaluation

To pass this course you must meet the following requirements:

- Score an average of **at least 2 on the rubric** overall for each assignment
- Pass the **final summative assessment** according to the rubric
- Actively participate in class and follow the attendance policy
- Make up all classwork from absences

---

## Course Philosophy

This course emphasizes **iteration and refactoring**.

Your early solutions will often feel awkward or messy. This is intentional. As the course progresses you will revisit earlier designs and improve them using new patterns and tools.

Learning to recognize when a state architecture is failing — and how to improve it — is a central goal of the course.