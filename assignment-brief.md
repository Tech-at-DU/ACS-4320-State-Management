# Project: State Management Studio

Overview

In this course you will build a single React application—a task / issue tracker—that evolves over the entire term. You will not start over each unit. Instead, you will refactor the same application multiple times as new state-management concepts are introduced.

The goal of this project is not to add features quickly, but to design, analyze, and improve application state as complexity increases.

⸻

Project Structure
	•	One repository for the entire term
	•	Multiple milestone submissions
	•	Each milestone introduces a new state constraint
	•	Most milestones require refactoring existing code, not building from scratch

Breaking the app and rebuilding it to avoid refactoring defeats the purpose and will be penalized.

⸻

The Application

You will build a Task / Issue Tracker with:
	•	A list of tasks
	•	A detail/edit view
	•	Create, update, and delete actions
	•	Filtering and navigation
	•	Async data and persistence (later in the term)

The data model and core behavior will be provided and must not be changed unless explicitly instructed.

⸻

What This Assignment Is Really About

This project is designed to teach you how to:
	•	Decide where state should live
	•	Avoid duplicated or derived state
	•	Handle async and server data correctly
	•	Model workflows explicitly
	•	Change architecture without breaking behavior

You will be graded as much on what you remove and reorganize as on what you add.

⸻

Milestone Progression (High Level)

Over the term, you will incrementally refactor the application to support:
	1.	Local state only (props + useState)
	2.	Shared state and routing
	3.	Global state (Redux, limited scope)
	4.	Server state, async updates, and caching
	5.	Explicit workflow modeling (reducers / state machines)
	6.	URL-based and persistent state
	7.	Final refactor and architectural critique

Each phase introduces new constraints. Previous solutions may become invalid and must be revised.

⸻

Required Deliverables (Each Milestone)

Each submission must include:
	•	A working application
	•	Clean, readable commits (no single “final” commit)
	•	A short written explanation describing:
	•	What state exists
	•	Where it lives
	•	Why it lives there
	•	What state is derived

Some milestones will also require diagrams or transition models.

⸻

Rules and Constraints
	•	You may only use libraries introduced in the course and only when allowed
	•	You may not add features unless explicitly required
	•	You may not change the data model without permission
	•	You may not store derived state “for convenience”
	•	Unjustified global state will be treated as incorrect

⸻

Grading Emphasis

You will be evaluated on:
	•	Correctness of state behavior
	•	Clarity of state ownership
	•	Quality of refactors
	•	Ability to explain architectural decisions
	•	Discipline in following constraints

A working app with poor state design will not receive full credit.

⸻

Final Note

This project mirrors real frontend work: inheriting a codebase, discovering its weaknesses, and improving it without breaking users. If at any point the project feels uncomfortable or restrictive, that discomfort is part of the learning objective.
