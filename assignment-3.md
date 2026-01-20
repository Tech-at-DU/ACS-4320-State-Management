# Assignment 3 — Global State with Redux Toolkit (Weeks 5–6)

ACS 4320 — State Management for JavaScript Apps

**Overview**

In Phase 3 you will refactor your application to introduce a global state store using Redux Toolkit. This phase is not about rewriting your app or “Redux-ifying everything.” It is about learning when global state helps and when it actively makes your code worse.

You will move a limited, well-defined portion of state into Redux and leave the rest where it belongs.

**Goal**

Refactor your Phase 2 application so that shared, long-lived domain state is managed in Redux, while UI and workflow state remains local.

Your app should behave exactly the same as Phase 2 from a user’s perspective.

What Changes from Phase 2
	•	Introduce a Redux store using Redux Toolkit
	•	Move the tasks collection into Redux
	•	Refactor components to read/write task data via Redux
	•	Keep routing, UI state, and forms out of Redux

**State Rules (Read Carefully)**

Redux must manage:
	•	The list of tasks
	•	Creating, updating, and deleting tasks
	•	Access to task data via selectors

Redux must not manage:
	•	Form input values
	•	Which page or route is active
	•	Temporary UI flags (edit mode, modal open, etc.)
	•	Derived state (filtered lists, counts stored as arrays)

If Redux contains UI state “because it was convenient,” your design is incorrect.

**Technical Requirements**

You must use:
	•	Redux Toolkit (configureStore, createSlice)
	•	React Redux (Provider, useSelector, useDispatch)
	•	Selectors to access task data

You may not use:
	•	Server APIs or async fetching
	•	TanStack Query / SWR
	•	LocalStorage or persistence
	•	Context as a substitute for Redux

**Required Redux Structure**

At minimum, your project must include:
	•	A Redux store configured with configureStore
	•	A tasks slice responsible only for task data
	•	Reducers for:
    •	add task
    •	update task
    •	delete task
  •	Selectors for:
    •	all tasks
    •	task by id

Normalization is optional, but your state shape must be intentional and documented.

**App Behavior (Unchanged)**

Your app must still support:
	•	/tasks — list view
	•	/tasks/new — create view
	•	/tasks/:id — detail view

Routing behavior should not change. Redux should make state clearer, not magically fix navigation bugs.

**Deliverables**

You must submit:
	1.	A working application using Redux Toolkit
	2.	A clearly organized store/ (or equivalent) directory
	3.	A short written explanation (1–2 paragraphs) answering:
    •	What state moved into Redux, and why?
    •	What state explicitly stayed out of Redux, and why?
    •	One example of derived state handled with a selector instead of stored state

Common Mistakes (Avoid These)
	•	Putting form state into Redux
	•	Storing filtered task lists in Redux state
	•	Accessing Redux state directly without selectors
	•	Adding Redux “just in case” instead of for a clear reason

The best Phase 3 solutions usually involve less Redux than expected, not more.

Important Notes
	•	Redux is a tool, not a requirement for correctness.
	•	If your Redux store grows quickly, that is a warning sign.
	•	A smaller, well-justified store will score higher than a large one.
