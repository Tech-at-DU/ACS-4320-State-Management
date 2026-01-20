# Assignment 4 — State Audit & Architecture Justification

ACS 4320 — State Management for JavaScript Apps
Week 7

⸻

Overview

This assignment is the final phase of the semester-long project. You are not adding new features and not introducing new libraries. Instead, you will step back and evaluate the state architecture you’ve built over the term.

At this point, your app should already work. Your task now is to make your state decisions explicit, defensible, and intentional.

⸻

Goal

Demonstrate that you understand:
	•	what state exists in your application,
	•	where that state lives,
	•	why it lives there,
	•	and how the pieces fit together.

This assignment is about judgment and reasoning, not implementation speed.

⸻

What You Will Do

You will:
	1.	Review your current application (after Phase 3 / Redux).
	2.	Identify unnecessary, duplicated, or unclear state.
	3.	Perform one small refactor to improve clarity or correctness.
	4.	Write a short technical document explaining your state architecture.

⸻

Constraints (Strict)

You may:
	•	Refactor existing code
	•	Remove unnecessary state
	•	Simplify Redux usage
	•	Improve selectors or component boundaries

You may not:
	•	Add new features
	•	Add new libraries
	•	Add async/server behavior
	•	Add persistence
	•	Redesign the UI

If the user-visible behavior changes, you have gone too far.

⸻

Required Deliverables

1. Final Application

Submit the final version of your app with:
	•	the same routes
	•	the same features
	•	improved state clarity

⸻

2. STATE.md (Required)

Create a file named STATE.md in the root of your project.

It must answer the following questions clearly and concisely:

A. What state exists?
List all meaningful pieces of state in your app.
Examples:
	•	tasks collection
	•	form input state
	•	selected task (if any)
	•	UI flags

B. Where does each piece of state live?
For each item above, specify:
	•	local component state
	•	lifted state
	•	Redux store
	•	derived (not stored)

C. Why does it live there?
Explain the reasoning behind each placement.
You are graded on justification, not correctness alone.

D. What state is derived?
Identify state that is calculated rather than stored, and explain how it is derived.

E. What state is intentionally not global?
Describe at least one piece of state you deliberately kept out of Redux, and why.

⸻

3. One Focused Refactor

Perform one meaningful improvement, such as:
	•	removing duplicated state
	•	moving state out of Redux into local components
	•	simplifying a reducer or selector
	•	eliminating unnecessary flags

Describe this refactor briefly in STATE.md.

⸻

In-Class Focus (This Week)

We will:
	•	review common state mistakes across projects
	•	practice drawing state maps
	•	critique Redux usage (what belongs vs what doesn’t)
	•	discuss when not to refactor further

Be prepared to explain your app verbally.

⸻

Grading Emphasis

You will be evaluated on:
	•	clarity of state reasoning
	•	correctness of state boundaries
	•	quality of explanation
	•	restraint in refactoring

You will not be graded on:
	•	feature count
	•	clever abstractions
	•	visual polish

⸻

Final Note

Most real frontend work involves inheriting existing code and making it more understandable without breaking it. This assignment mirrors that reality.

If you cannot explain why a piece of state exists, it probably shouldn’t.

⸻

If you want next, I can:
	•	provide a STATE.md template students fill in,
	•	write a grading rubric for Assignment 4,
	•	or help you fill in the Lesson column for the full schedule table