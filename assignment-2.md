# Assignment 2 — Shared State & Routing (Weeks 3–4)

ACS 4320 — State Management for JavaScript Apps

## Overview

In Phase 2 you will refactor your Phase 1 Task Tracker into a multi-page single-page application (SPA) using client-side routing. Your job is not to add lots of new features. Your job is to make the same app work correctly when the UI is split across routes.

Routing forces you to answer: **Where does state live when components no longer share the same parent view?**

## Goal

Refactor your Phase 1 application so it supports:

- a Task List page
- a Task Detail page
- a Task Create page

Navigation must work without losing data or duplicating state.

---

## Data Model (Unchanged)

Use the same task model from Phase 1:

- id — string
- title — string
- status — "todo" | "doing" | "done"
- createdAt — string
- updatedAt — string

Do **not** add new fields in Phase 2.

---

## Routes (Required)

Your app must include these routes:

1. `/tasks` — Task List
2. `/tasks/new` — Create Task
3. `/tasks/:id` — Task Detail

---

## Page Requirements

### 1) `/tasks` — Task List Page

Must display:

- A list of tasks showing title + status
- Total task count
- A link/button to Create (`/tasks/new`)
- Each task should link to Detail (`/tasks/:id`)

Optional:

- Delete button (allowed here or on detail)

---

### 2) `/tasks/new` — Create Task Page

Must include:

- A form to create a task (title + status)
- Validation: title must be 3–60 characters
- Cancel returns to `/tasks` without creating anything
- Save creates the task and then navigates to either:
  - `/tasks`, or
  - the new task’s detail page (`/tasks/:id`)

Choose one behavior and keep it consistent.

---

### 3) `/tasks/:id` — Task Detail Page

Must display:

- Title
- Status
- createdAt
- updatedAt

Include controls for:

- Back to list (`/tasks`)
- Edit (inline or separate route)
- Delete (optional but recommended)

Required behavior:

If the URL contains an unknown id, show:

```
Task not found
Return to task list
```

---

## Shared State Expectations

What must be shared across routes:

- The **tasks array** (the source of truth)

What must **not** happen:

- No separate `tasks` state per page
- No `selectedTask` stored as its own copy

The **URL represents selection state**.

Example:

`/tasks/:id` determines which task is selected.

Use the id param to look up the task from the shared tasks array.

Correct pattern:

- Shared tasks live in a common parent above routes (often `App`)
- Pages receive tasks and callbacks via props

---

## Technical Requirements

You must use:

- React
- React Router (or equivalent)
- React components and hooks

You may **not** use:

- Redux or any global store
- Context
- Server APIs or async data
- LocalStorage or persistence

---

## Implementation Guidance (Recommended Structure)

A typical structure might look like:

```
App
 ├─ TaskList
 ├─ TaskNew
 └─ TaskDetail
```

`App` owns:

- `tasks`
- `addTask(task)`
- `updateTask(task)`
- `deleteTask(id)`

Routes render pages such as:

```
<TaskList tasks={tasks} onDelete={...} />
<TaskNew onCreate={addTask} />
<TaskDetail tasks={tasks} onUpdate={...} onDelete={...} />
```

You do not have to match these names exactly, but the architecture should follow the same idea.

---

## Common Mistakes (Avoid These)

Duplicating the tasks array in multiple pages.

If you have `useState([...])` in more than one page, your architecture is probably incorrect.

Copying task objects into state just to edit them creates **mirrored state** that drifts out of sync.

Routing is not just a UI feature — it changes how your state must be organized.

---

## Stretch Challenges (Optional but Recommended)

After completing the required version, you may implement one or more stretch challenges. These intentionally add complexity so you can see how routing increases pressure on your state architecture.

### 1. Edit Route

Add:

`/tasks/:id/edit`

Requirements:

- Pre-fill form with task data
- Save updates the task
- Cancel returns to `/tasks/:id`

---

### 2. Previous / Next Task Navigation

On the task detail page add:

- Previous Task
- Next Task

Disable buttons when at the beginning or end.

---

### 3. Search via URL Query

Example:

`/tasks?q=meeting`

Requirements:

- Filter tasks by title
- Query parameter updates as user types
- Refresh preserves filter

---

### 4. Status Filter via URL

Examples:

```
/tasks?status=todo
/tasks?status=doing
/tasks?status=done
```

Filtering must be controlled by the URL.

---

### 5. Delete Confirmation Route

Add:

`/tasks/:id/delete`

Display confirmation before deleting.

---

### 6. Duplicate Task

Add a **Duplicate Task** button on the detail page.

The duplicate should:

- Copy title
- Generate new id
- Generate new timestamps

---

### 7. Recently Updated Tasks

On `/tasks`, show the **3 most recently updated tasks**.

This must be **derived state**, not stored separately.

---

## Stretch Challenge Rules

- Complete required features first
- Do not duplicate the tasks array
- Do not introduce global stores
- Do not modify the task model

---

## Deliverables

You must submit:

1. A working routed application with:

- `/tasks`
- `/tasks/new`
- `/tasks/:id`

2. Refactored state that works consistently across routes

3. A short written explanation (1–2 paragraphs) describing:

- What state became shared
- Where that state now lives
- One design decision you changed because of routing

---

## Important Notes

- Do not add a global store to "make routing easier."
- Do not copy task data into multiple components.
- If navigation breaks your app, your state design is incorrect.

This phase exists to show that **routing is a state problem, not just a UI feature.**
