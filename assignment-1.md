# Assignment 1 — Local State Only (Weeks 1–2)

ACS 4320 — State Management for JavaScript Apps

## Overview

In this phase, you will build a Task Tracker using only local React state. The goal is to get a working application on screen quickly, even if the structure feels awkward or repetitive. To make the project more engaging, you will also choose optional challenge features that let you personalize the app without introducing new architecture before we are ready for it.

## Goal

Build a working Task Tracker using:
- React components
- Props
- useState

All data will live in memory while the app is running.

If your code begins to feel uncomfortable or fragile, that is expected.

## What You Will Build

Your app must allow a user to:
- View a list of tasks
- Create a new task
- Edit an existing task
- Delete a task

The app should be a single page with no routing.

Think of the base assignment as the minimum working product. After that is working, you will choose challenge features to make the project more interesting and to create useful pressure that exposes the limits of local state.

## Task Model

For this phase, every task must have exactly the following fields:
- id — string (unique identifier)
- title — string (required)
- status — "todo" | "doing" | "done"
- createdAt — string (timestamp)
- updatedAt — string (timestamp)

## Required Features

1. View Tasks
   - Display a list of tasks showing:
     - title
     - status
   - Display the total number of tasks

2. Create a Task
   - Provide a form with inputs for:
     - title
     - status
   - Validation rules:
     - title must be 3–60 characters
     - whitespace-only titles are invalid

3. Edit a Task
   - Clicking “Edit” should load the task into the form
   - Saving updates the task and sets updatedAt

4. Delete a Task
   - Removes the task from the list
   - Confirmation is optional in Phase 1

## Technical Constraints

You may use:
- React
- Vite
- useState
- Props

You may not use:
- Redux or any global store
- Context
- Routing
- Async data or APIs
- LocalStorage or persistence

## Implementation Guidelines

- Store all tasks in a single array in state:

```js
const [tasks, setTasks] = useState([...])
```

- Do not store derived data (such as filtered lists) in state
- Keep the UI simple and functional

## Challenge Features

After you complete the required version, choose **at least two** challenge features from the list below. These should still be built with only local state, props, and simple React patterns.

The purpose of these challenges is not just to make the app “cooler.” They are meant to reveal where local state works well, where it becomes awkward, and where state starts spreading across too many components.

Choose features that interest you, but do not add routing, Context, Redux, APIs, or persistence.

### Challenge Options

- **Task Filter Bar**
  - Add buttons or tabs that let the user view only tasks with status: todo, doing, or done
  - Include a way to return to viewing all tasks

- **Search Tasks**
  - Add a text input that filters tasks by title as the user types
  - Search should be case-insensitive

- **Sort Tasks**
  - Let the user sort by title, createdAt, or updatedAt
  - The UI should clearly show which sort is active

- **Task Counters by Status**
  - Show how many tasks are in todo, doing, and done
  - These values should be derived from state, not stored separately

- **Inline Status Update**
  - Allow the user to change a task’s status directly from the task list without opening the edit form

- **Duplicate Task**
  - Add a control that clones an existing task with a new id and fresh timestamps

- **Clear Completed Tasks**
  - Add a button that removes all tasks with status `done`
  - This should be implemented as a single state update

- **Simple Progress Display**
  - Display progress such as `3 of 8 tasks completed`
  - You may also show this visually with a simple bar if you want

- **Form Mode Indicator**
  - Make it very clear when the form is in Create mode vs Edit mode
  - Include a Cancel Edit button

- **Seed Data Theme**
  - Give your tasks a theme such as game quests, study goals, job applications, buy tickets, chores, workout plan, or music practice
  - Start with 5–7 meaningful sample tasks that fit your chosen theme

### Rules for Challenge Features

- You must complete all required features before starting challenges
- Your challenge features must not change the task model
- Do not add extra libraries just to implement a challenge
- Keep your UI understandable; complexity without clarity is not an improvement

### Reflection Prompt Add-On

In your written reflection, also answer:

- Which challenge features did you choose, and why?
- Which feature created the most state-management friction?
- What part of your app now feels hardest to maintain?

## Deliverables

You must submit:
1. A working React application that meets all required feature requirements  
2. At least two completed challenge features  
3. A short written reflection (1–2 paragraphs, written in the readme) answering:  
   - What state exists in your app?  
   - Where does that state live?  
   - Where does the design feel strained or unclear?  
   - Which challenge features did you choose?  
   - What became harder once the app grew?

## Important Notes

- Do not try to “solve ahead” by adding architecture you haven’t learned yet
- Do not over-optimize or refactor prematurely
- This app will be refactored in later phases
- The challenge features are intentionally chosen to make state harder to manage—this is part of the lesson

A correct but awkward solution is better than a clever one.
