# Assignment 4 — Introducing Server State (Manual Async)

ACS 4320 — State Management for JavaScript Apps  
Weeks 8–9

---

## Overview

Up to this point, your application has used in-memory data stored in Redux.  
In this assignment, you will replace that data with a **real API** and manage it using **manual async logic**.

You will not use TanStack Query (or any server-state library) yet.

---

## Backend Setup (Express)

For this assignment, you will run a small Express server locally.

- **Frontend (Vite):** `http://localhost:5173`
- **API (Express):** `http://localhost:3001`

### Minimum server requirements

Your server must:
- respond with JSON
- support basic CRUD routes for tasks
- allow requests from your Vite dev server (CORS)

### Suggested folder layout

Keep the backend in the same repo:

```
/
  /server
    index.js
    package.json
  /src
    ...your React app...
```

### Starter Express server (copy/paste)

Create `server/index.js`:

```js
import express from 'express'
import cors from 'cors'

const app = express()
app.use(cors({ origin: 'http://localhost:5173' }))
app.use(express.json())

// In-memory data (Phase 4 starts here). You may replace this later.
let tasks = [
  {
    id: '1',
    title: 'Example task',
    status: 'todo',
    createdAt: new Date().toISOString(),
    updatedAt: new Date().toISOString(),
  },
]

// Use an API prefix so it never conflicts with React Router routes.
const base = '/api/tasks'

app.get(base, (req, res) => {
  res.json(tasks)
})

app.get(`${base}/:id`, (req, res) => {
  const task = tasks.find(t => t.id === req.params.id)
  if (!task) return res.status(404).json({ message: 'Task not found' })
  res.json(task)
})

app.post(base, (req, res) => {
  const { title, status } = req.body
  if (!title || title.trim().length < 3) {
    return res.status(400).json({ message: 'Title must be at least 3 characters' })
  }
  const now = new Date().toISOString()
  const task = {
    id: String(Date.now()),
    title: title.trim(),
    status: status ?? 'todo',
    createdAt: now,
    updatedAt: now,
  }
  tasks = [task, ...tasks]
  res.status(201).json(task)
})

app.put(`${base}/:id`, (req, res) => {
  const idx = tasks.findIndex(t => t.id === req.params.id)
  if (idx === -1) return res.status(404).json({ message: 'Task not found' })

  const { title, status } = req.body
  const now = new Date().toISOString()
  const updated = {
    ...tasks[idx],
    title: title?.trim() ?? tasks[idx].title,
    status: status ?? tasks[idx].status,
    updatedAt: now,
  }

  tasks = tasks.map(t => (t.id === req.params.id ? updated : t))
  res.json(updated)
})

app.delete(`${base}/:id`, (req, res) => {
  const exists = tasks.some(t => t.id === req.params.id)
  if (!exists) return res.status(404).json({ message: 'Task not found' })
  tasks = tasks.filter(t => t.id !== req.params.id)
  res.status(204).send()
})

app.listen(3001, () => {
  console.log('API running on http://localhost:3001')
})
```

Install and run (from `/server`):

```bash
npm init -y
npm i express cors
npm i -D nodemon
```

Add a `server/package.json` script:

```json
{
  "type": "module",
  "scripts": {
    "dev": "nodemon index.js"
  }
}
```

Run the API:

```bash
npm run dev
```

**Note:** This is intentionally a minimal server. Your focus is client-side state boundaries, not backend architecture.

---

## Goal

Demonstrate that you can:

- Fetch data from a server
- Handle loading and error states correctly
- Update server data through POST / PUT / DELETE
- Keep UI consistent after mutations
- Maintain clear separation between UI state and server data

You are expected to encounter edge cases and awkward patterns.

---

## What Is Changing

Your tasks data will no longer live in Redux as the source of truth.

Instead:

- Tasks must be fetched from an API
- Mutations must update the server
- The UI must reflect server updates correctly

Redux may still be used for **non-server client state**, but not as a duplicate store of server data.

---

## Technical Requirements

You must:

- Use `fetch` (or equivalent native async approach)
- Use `useEffect` to load data
- Use Redux Toolkit async thunks (createAsyncThunk) OR component-level async logic (useEffect + fetch) to load/mutate data
- Track:
  - loading state
  - error state
- Refetch or reconcile data after:
  - creating a task
  - updating a task
  - deleting a task

You may not:

- Use TanStack Query
- Use SWR
- Introduce caching libraries
- Store a duplicated copy of server data in multiple places
- Use RTK Query (this assignment is intentionally 'manual' server state)

---

## API Expectations

You will use a REST-style API that supports:

- `GET /api/tasks`
- `GET /api/tasks/:id`
- `POST /api/tasks`
- `PUT /api/tasks/:id`
- `DELETE /api/tasks/:id`

### API routes vs React Router routes (important)

Your **React Router routes** (examples: `/tasks`, `/tasks/new`, `/tasks/:id`) are *frontend URLs*.

Your **API routes** (examples: `/api/tasks`, `/api/tasks/:id`) are *backend endpoints*.

They should **not** be the same path.

- Good: `/tasks` (frontend) and `/api/tasks` (backend)
- Bad: `/tasks` used as both frontend route and API endpoint (easy to confuse, harder to debug)

In general, matching the *resource name* is fine ("tasks"), but keep the `/api` prefix so there is a clear boundary.

Your app must handle slow responses and server errors gracefully.

---

## Redux + Async Thunks (Expected Approach)

Since you already use Redux Toolkit, this assignment is a good place to introduce **async thunks**.

You may implement server calls in one of two acceptable ways:

### Option A (recommended): Thunks for server calls

- `fetchTasks` thunk loads tasks from the API
- `createTask`, `updateTask`, `deleteTask` thunks perform mutations
- Your slice tracks:
  - `status: 'idle' | 'loading' | 'succeeded' | 'failed'`
  - `error: string | null`

This keeps your network logic in one place and forces you to model loading/error explicitly.

### Option B: Component-level async (allowed)

- Use `useEffect` + `fetch` directly in your route components
- Track loading/error locally

This is acceptable, but it tends to spread async logic across the UI.

**Either way:** you are not using a server-state library yet. Expect some awkwardness.


---

## Required Behaviors

Your app must:

- Show a loading indicator while fetching tasks
- Show an error state if the request fails
- Prevent duplicate submissions while saving
- Reflect changes immediately after successful mutations
- Avoid stale UI after updates

If your UI shows outdated data after a mutation, your state design is incorrect.

---

## State Boundary Rules

- Server data must come from the API
- Redux must not act as a permanent mirror of server data
- Do not store filtered copies of server results in state
- Derived state should be computed, not stored

---

## Deliverables

1. A working app backed by the API
2. Clear loading and error handling
3. A short written explanation (1–2 paragraphs) describing:
   - What state is now server-controlled
   - What state remains client-only
   - Where awkwardness appeared in your design

---

## Common Mistakes to Avoid

- Fetching data but never refetching after mutations
- Storing server data in both Redux and component state
- Ignoring loading and error conditions
- Triggering infinite re-fetch loops

---

## Grading Emphasis

You will be evaluated on:

- Correct async handling
- Proper separation of client vs server state
- UI consistency
- Clarity of explanation

You will not be graded on visual polish.

---

## Important Note

This assignment is designed to show you the limitations of managing server data manually.

If your solution feels repetitive or fragile, that is part of the lesson.

In the next phase, you will refactor this using a server-state abstraction.