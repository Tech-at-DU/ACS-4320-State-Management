# Assignment 2 — Shared State & Routing (Weeks 3–4)

ACS 4320 — State Management for JavaScript Apps

**Overview**

In Phase 2 you will refactor your Phase 1 Task Tracker into a multi-page single-page application (SPA) using client-side routing. Your job is not to add lots of new features. Your job is to make the same app work correctly when the UI is split across routes.

Routing forces you to answer: Where does state live when components no longer share the same parent view?

**Goal**

Refactor your Phase 1 application so it supports:
  - a Task List page
  - a Task Detail page
  - a Task Create page

Navigation must work without losing data or duplicating state.

**Data Model (Unchanged)**

Use the same task model from Phase 1:
	- id — string
	- title — string
	- status — "todo" | "doing" | "done"
	- createdAt — string
	- updatedAt — string

Do not add new fields in Phase 2.

**Routes (Required)**

Your app must include these routes:
	1. /tasks — Task List
	2. /tasks/new — Create Task
	3. /tasks/:id — Task Detail

**Page Requirements**

1) /tasks — Task List Page

Must display:
	- A list of tasks showing title + status
	- Total task count
	- A link/button to Create (/tasks/new)
	- Each task should link to Detail (/tasks/:id)

Optional:
	- Delete button (allowed here or on detail)

2) /tasks/new — Create Task Page

Must include:
	- A form to create a task (title + status)
	- Validation: title must be 3–60 characters
	- Cancel returns to /tasks without creating anything
	- Save creates the task and then navigates to:
	- either /tasks or
	- the new task’s detail page (/tasks/:id)
(choose one and keep it consistent)

3) /tasks/:id — Task Detail Page

Must display:
	- Title, status, createdAt, updatedAt
	- Buttons/links for:
	- Edit (can be inline or link to edit mode)
	- Back to list (/tasks)
	- Delete (optional but recommended)

Required behavior
	- If the URL contains an unknown id, show a clear message:
	- “Task not found” + link back to /tasks

**Shared State Expectations**

What must be shared across routes
	- The tasks array (the source of truth)

What must not happen
	- No separate “tasks” state per page
	- No “selectedTask” stored as its own copy of the task object

The URL is the selection state
	- The selected task is defined by the route: /tasks/:id
	- Use the id param to look up the task from the shared tasks array

Correct pattern
	- Shared tasks lives in a common parent above routes (often App)
	- Pages receive tasks and callbacks via props

**Technical Requirements**

You must use:
	- React Router (or equivalent client-side router)
	- React components and hooks
	- Props and lifted state where appropriate

You may not use:
	- Redux or any global store
	- Context
	- Server APIs or async data
	- LocalStorage or persistence

**Implementation Guidance (Recommended Structure)**

A typical structure looks like:
	- App owns:
    - `tasks`
    - `addTask(task)`
    - `updateTask(task)`
    - `deleteTask(id)`
	- Routes render pages like:
    - `<TaskList tasks={tasks} onDelete={...} />`
    - `<TaskNew onCreate={addTask} />`
    - `<TaskDetail tasks={tasks} onUpdate={...} onDelete={...} />`

You don’t have to match these names exactly, but your architecture should reflect the same idea.

Common Mistakes (Avoid These)
	- Duplicating the tasks array in multiple pages
If you have `useState([...])` in more than one page, you’re probably wrong.
	- Copying task objects into state just to edit them
This creates “mirrored state” that drifts out of sync.
	- Using routing as a UI trick only
Routing changes your state problem—treat it as such.

**Deliverables**

You must submit:
	1.	A working routed application with:
	    - `/tasks`
	    - `/tasks/new`
	    - `/tasks/:id`
	2.	Refactored state that works consistently across routes
	3.	A short written explanation (1–2 paragraphs) describing:
	    - What state became shared
	    - Where that state now lives
	    - One design decision you changed because of routing

Important Notes
	•	Do not add a global store to “make routing easier.”
	•	Do not copy task data into multiple components.
	•	If navigation breaks your app, your state design is incorrect.

This phase exists to show that routing is a state problem, not just a UI feature.
