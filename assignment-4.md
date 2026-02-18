# Assignment 4 — Introducing Server State (Manual Async)

ACS 4320 — State Management for JavaScript Apps  
Weeks 8–9

---

## Overview

Up to this point, your application has used in-memory data stored in Redux.
In this assignment, you will replace that data with a **real API** and manage it using **manual async logic**.

You will not use TanStack Query, RTK Query, or any server-state library yet.

This phase is intentionally uncomfortable. If parts of your solution feel repetitive or fragile, that is part of the lesson.

---

# Backend Setup — JSON Server

You will use **JSON Server** to create a simple REST API backed by a `db.json` file.

- Frontend (Vite): `http://localhost:5173`
- API (JSON Server): `http://localhost:3001`

JSON Server automatically:
- Creates REST endpoints
- Persists changes to `db.json`
- Mimics real server behavior

Your goal is to focus on **client vs server state**, not backend implementation.

---

## Setup

From your project root:

```bash
npm install -D json-server
```

Create a `db.json` file in the project root:

```json
{
  "tasks": []
}
```

Add this script to your root `package.json`:

```json
{
  "scripts": {
    "server": "json-server --watch db.json --port 3001"
  }
}
```

Start the API:

```bash
npm run server
```

Confirm it works:

Visit:
```
http://localhost:3001/tasks
```
You should see `[]`.

---

# (Optional but Recommended) Vite Proxy Setup

To avoid hardcoding `http://localhost:3001` everywhere, configure a Vite proxy.

Create or update `vite.config.js`:

```js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
  server: {
    proxy: {
      '/api': {
        target: 'http://localhost:3001',
        changeOrigin: true,
      },
    },
  },
})
```

Then create `routes.json` in the project root:

```json
{
  "/api/*": "/$1"
}
```

Update your server script:

```json
"server": "json-server --watch db.json --port 3001 --routes routes.json"
```

Now you can use:

```js
fetch('/api/tasks')
```

instead of hardcoding the full URL.

---

# API Expectations

JSON Server provides these endpoints:

- `GET /tasks`
- `GET /tasks/:id`
- `POST /tasks`
- `PUT /tasks/:id`
- `DELETE /tasks/:id`

If using the proxy setup, use:

- `GET /api/tasks`
- etc.

### Important Distinction

React Router routes:
- `http://localhost:5173/tasks`

API routes:
- `http://localhost:3001/tasks`

They may share the same resource name (`tasks`), but they are completely separate systems.

Never call your frontend routes with `fetch()`.

---

# Goal

You must demonstrate that you can:

- Fetch data from a server
- Handle loading and error states correctly
- Update server data through POST / PUT / DELETE
- Keep UI consistent after mutations
- Maintain clear separation between client and server state

---

# What Is Changing

Tasks are no longer stored permanently in Redux.

Instead:

- Tasks must be fetched from the API
- Mutations must update the API
- The UI must stay in sync with the server

Redux may still manage:
- UI state
- Local flags
- Non-server client state

Redux must not permanently mirror server data.

---

# Technical Requirements

You must:

- Use `fetch`
- Use `useEffect` OR Redux Toolkit `createAsyncThunk`
- Track loading state
- Track error state
- Refetch or reconcile after create/update/delete

You may not:

- Use TanStack Query
- Use RTK Query
- Use SWR
- Introduce caching libraries
- Store duplicated copies of server data in multiple places

---

# Redux + Async Thunks (Recommended)

Since you already use Redux Toolkit, this is a good place to introduce async thunks.

Recommended structure:

- `fetchTasks` thunk
- `createTask` thunk
- `updateTask` thunk
- `deleteTask` thunk

Your slice should track:

```js
status: 'idle' | 'loading' | 'succeeded' | 'failed'
error: null | string
```

Tip:

```js
const API_URL = '/api/tasks' // if using proxy
```

Keep network logic centralized.

---

# Required Behaviors

Your app must:

- Show a loading indicator while fetching
- Show an error state if a request fails
- Prevent duplicate submissions while saving
- Reflect changes immediately after successful mutations
- Avoid stale UI after updates

If the UI shows outdated data, your state design is incorrect.

---

# State Boundary Rules

- Server data must originate from the API
- Do not mirror server data in multiple stores
- Do not store derived lists in state
- Compute derived state from source data

---

# Deliverables

1. Working app backed by JSON Server
2. Proper loading + error handling
3. A short written explanation (1–2 paragraphs) describing:
   - What state is server-controlled
   - What state remains client-controlled
   - Where awkwardness appeared in your design

---

# Common Mistakes

- Never refetching after mutations
- Storing server data in both Redux and component state
- Ignoring loading or error states
- Creating infinite fetch loops

---

# Grading Emphasis

You will be graded on:

- Correct async handling
- Clear client vs server boundaries
- UI correctness
- Architectural reasoning

Visual polish is not a grading factor.

---

# Final Note

This assignment exposes the limitations of manual server-state handling.

In the next phase, you will refactor this using a proper server-state abstraction.