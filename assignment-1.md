# Assignment 1 — Local State Only (Weeks 1–2)

ACS 4320 — State Management for JavaScript Apps

Overview

In this phase, you will build a small Task Tracker using only local React state. The goal is to get a working application on screen quickly, even if the structure feels awkward or repetitive.

You are not expected to design a clean or final architecture yet. This project will be refactored in later phases.

**Goal**

Build a working Task Tracker using:
	•	React components
	•	Props
	•	useState

All data will live in memory while the app is running.

If your code begins to feel uncomfortable or fragile, that is expected.

**What You Will Build**

Your app must allow a user to:
	•	View a list of tasks
	•	Create a new task
	•	Edit an existing task
	•	Delete a task

The app should be a single page with no routing.

**Task Model**

For this phase, every task must have exactly the following fields:
	•	id — string (unique identifier)
	•	title — string (required)
	•	status — "todo" | "doing" | "done"
	•	createdAt — string (timestamp)
	•	updatedAt — string (timestamp)

Do not add:
	•	descriptions
	•	priorities
	•	due dates
	•	tags
	•	assignees

These may be added in later phases.

**Required Features**

1. View Tasks
	•	Display a list of tasks showing:
    •	title
    •	status
    •	Display the total number of tasks

2. Create a Task
	•	Provide a form with inputs for:
    •	title
    •	status
    •	Validation rules:
    •	title must be 3–60 characters
    •	whitespace-only titles are invalid

3. Edit a Task
	•	Clicking “Edit” should load the task into the form
	•	Saving updates the task and sets updatedAt

4. Delete a Task
	•	Removes the task from the list
	•	Confirmation is optional in Phase 1

**Technical Constraints**

You may use:
	•	React
	•	Vite
	•	useState
	•	Props

You may not use:
	•	Redux or any global store
	•	Context
	•	Routing
	•	Async data or APIs
	•	LocalStorage or persistence

Implementation Guidelines
	•	Store all tasks in a single array in state:

```js
const [tasks, setTasks] = useState([...])
```

	•	Do not store derived data (such as filtered lists) in state
	•	Keep the UI simple and functional

**Deliverables**

You must submit:
	1. A working React application that meets all feature requirements
	2. A short written reflection (1–2 paragraphs, written in the readme) answering:
	•	What state exists in your app?
	•	Where does that state live?
	•	Where does the design feel strained or unclear?

Important Notes
	•	Do not try to “solve ahead” by adding architecture you haven’t learned yet
	•	Do not over-optimize or refactor prematurely
	•	This app will be refactored in later phases

A correct but awkward solution is better than a clever one.
