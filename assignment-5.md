---

ACS 4320 — State Management for JavaScript Apps  
Weeks 10–11

---

## Overview

In Assignment 4, you manually handled server state using `fetch`, `useEffect`, and/or async thunks. You likely experienced:

- repetitive loading/error logic
- manual refetching after mutations
- stale UI bugs
- awkward state boundaries

In this assignment, you will refactor your app using **TanStack Query** to manage server state correctly.

This is not about adding features. It is about **replacing manual server state management with a proper abstraction**.

---

## Goal

Demonstrate that you can:

- Separate **client state** from **server state**
- Use TanStack Query for fetching and mutations
- Leverage caching and invalidation correctly
- Remove unnecessary Redux logic related to server data
- Simplify your state architecture

Your app should behave exactly the same from the user's perspective.

---

## What Is Changing

In Assignment 4:
- You manually fetched and refetched server data
- You managed loading/error state yourself

In Assignment 5:
- TanStack Query becomes the source of truth for server data
- Redux should no longer mirror server data
- Loading and error state come from query status

---

## Technical Requirements

You must:

- Install and configure TanStack Query
- Wrap your app in `QueryClientProvider`
- Replace manual fetch logic with:
  - `useQuery` for loading tasks
  - `useMutation` for create/update/delete
- Use `invalidateQueries` (or equivalent) after mutations
- Remove duplicated server state from Redux

You may not:

- Keep a copy of server tasks in Redux
- Manually refetch data inside components after every mutation
- Mix manual fetch logic with TanStack Query for the same data

---

## Required Refactors

### 1. Remove Server Data from Redux

If your Redux slice currently stores tasks fetched from the API, that data must be removed.

Redux may remain responsible for:
- UI state
- local-only flags
- non-server client state

But **server data must belong to TanStack Query**.

---

### 2. Loading and Error State

Your UI must use query status:

- `isLoading`
- `isError`
- `error`
- `isFetching`

You should not maintain duplicate loading flags in Redux.

---

### 3. Cache Invalidation

After creating, updating, or deleting a task:

- The list must update correctly
- No stale data should remain visible
- You must use query invalidation or mutation callbacks correctly

---

## Deliverables

1. A working application using TanStack Query
2. Removal of server-state duplication from Redux
3. A short written explanation (1–2 paragraphs) describing:
   - What moved from Redux to TanStack Query
   - How loading/error handling changed
   - One improvement in clarity compared to Assignment 4

---

## Comparison Reflection (Required)

Add a section to `STATE.md` answering:

- What felt awkward in Assignment 4?
- What improved with TanStack Query?
- When might Redux still be appropriate for state?

---

## Common Mistakes to Avoid

- Keeping tasks in Redux and TanStack Query simultaneously
- Manually refetching after mutations instead of invalidating queries
- Storing derived query results in local state
- Treating TanStack Query like a fetch wrapper instead of a server-state manager

---

## Grading Emphasis

You will be evaluated on:

- Proper separation of server and client state
- Correct use of queries and mutations
- Elimination of duplicated state
- Quality of architectural reasoning

You will not be graded on visual changes.

---

## Final Note

At this point in the course, you should clearly understand:

- Local UI state
- Shared state
- Global client state (Redux)
- Server state (TanStack Query)

This assignment completes the state taxonomy.

If you still have duplicated or unclear state boundaries, this is the time to fix them.
# Assignment 5 — Server State Refactor (TanStack Query)

ACS 4320 — State Management for JavaScript Apps  
Weeks 10–11

---

## Overview

In Assignment 4, you replaced in-memory Redux data with a real API (JSON Server) and handled async logic manually using `fetch`, `useEffect`, and/or Redux async thunks.

You likely experienced:

- repetitive loading and error handling
- manual refetching after mutations
- stale UI bugs
- awkward state boundaries between Redux and server data

In this assignment, you will refactor your app using **TanStack Query** to properly manage server state.

This is not about adding features. It is about replacing manual server-state management with a correct abstraction.

---

## Goal

Demonstrate that you can:

- Clearly separate **client state** from **server state**
- Use TanStack Query for data fetching and mutations
- Leverage caching and invalidation correctly
- Remove Redux async thunks that were used only for server data
- Simplify your state architecture

Your app should behave exactly the same from the user's perspective as Assignment 4.

---

## What Is Changing

In Assignment 4:

- JSON Server was the source of truth
- You manually fetched data
- You manually tracked loading and error state
- You likely used Redux async thunks for network calls

In Assignment 5:

- TanStack Query becomes the source of truth for server data
- Redux must no longer mirror server data
- Loading and error state come from query status
- Async thunks for server operations should be removed

---

## Technical Requirements

You must:

- Install and configure TanStack Query
- Wrap your app in `QueryClientProvider`
- Replace manual fetch logic and server-related thunks with:
  - `useQuery` for loading tasks
  - `useMutation` for create/update/delete
- Use `invalidateQueries` (or mutation callbacks) correctly
- Remove duplicated server state from Redux

You may not:

- Keep a copy of server tasks in Redux
- Continue using async thunks for server data
- Manually refetch inside components after every mutation
- Mix manual fetch logic with TanStack Query for the same resource

---

## API Consistency

You must continue using the same JSON Server backend from Assignment 4.

If using the Vite proxy setup:

```js
const API_URL = '/api/tasks'
```

Your TanStack Query calls should use the same endpoint structure.

You are refactoring the client architecture — not changing the backend.

---

## Required Refactors

### 1. Remove Server Data from Redux

If your Redux slice currently stores tasks fetched from the API, that data must be removed.

Redux may remain responsible for:

- UI state
- local-only flags
- non-server client state

But **server data must belong exclusively to TanStack Query**.

---

### 2. Replace Async Thunks

If you created thunks like:

- `fetchTasks`
- `createTask`
- `updateTask`
- `deleteTask`

These must be removed and replaced with:

- `useQuery`
- `useMutation`

Network logic should no longer live inside Redux slices.

---

### 3. Loading and Error State

Your UI must use TanStack Query status values:

- `isLoading`
- `isError`
- `error`
- `isFetching`

You must not maintain duplicate loading flags in Redux.

---

### 4. Cache Invalidation

After creating, updating, or deleting a task:

- The list must update correctly
- No stale data should remain visible
- Query invalidation must be used intentionally

If the UI updates only because you manually forced a refetch, your implementation is incomplete.

---

## Deliverables

1. A working application using TanStack Query
2. Removal of server-state duplication from Redux
3. A short written explanation (1–2 paragraphs) describing:
   - What moved from Redux to TanStack Query
   - What code was removed during the refactor
   - How loading/error handling changed
   - One architectural improvement compared to Assignment 4

---

## Comparison Reflection (Required)

Add a section to `STATE.md` answering:

- What felt awkward in Assignment 4?
- What improved with TanStack Query?
- What state still belongs in Redux?
- When would Redux be inappropriate for server state?

---

## Common Mistakes to Avoid

- Keeping tasks in Redux and TanStack Query simultaneously
- Leaving old async thunks in place
- Manually refetching instead of invalidating queries
- Storing derived query results in local component state
- Treating TanStack Query as a fetch wrapper instead of a server-state manager

---

## Grading Emphasis

You will be evaluated on:

- Proper separation of server and client state
- Correct use of queries and mutations
- Removal of unnecessary Redux logic
- Architectural clarity
- Quality of reasoning in your written explanation

Visual polish is not a grading factor.

---

## Final Note

At this point in the course, you should clearly understand the full state taxonomy:

- Local UI state
- Shared state
- Global client state (Redux)
- Server state (TanStack Query)

This assignment completes that taxonomy.

If your app still contains duplicated or unclear state boundaries, this is the time to fix them.