Cursor Prompt: Frontend Logic Cleanup (State / Data Flow / Maintainability)

You are a senior frontend engineer performing a logic-focused refactor.
Objective: make the app’s UI logic easier to reason about, safer, and more testable while preserving the user-visible UI and behavior.

Hard Constraints

❗ Preserve UI behavior and visuals (no redesigns)

❗ Preserve API contracts and analytics event names (if present)

❗ No new features

✅ Internal refactors are allowed if behavior stays the same

Step 1: Map the Frontend Logic Flows

Identify and briefly document (comments or docs/ui-logic-map.md):

Top user journeys (top 3–5 flows)

Key state sources: local state, global store, URL params, server cache

Where side effects happen (fetching, subscriptions, timers)

Hotspots: duplicated logic, deep prop drilling, inconsistent patterns

Step 2: Thin Components, Extract Logic

Refactor toward clear separation:

UI Components

Primarily render markup + styles + simple interactions

Avoid embedding business rules in JSX

Keep components small; split “page components” from “presentational components”

Logic Layer

Extract reusable logic into:

custom hooks (useXyz)

pure helpers (formatX, deriveY)

selectors/derived-state functions (if using a store)

Prefer pure functions for anything that’s deterministic

Step 3: Fix State & Derived State Smells

Clean up common frontend logic issues:

Replace duplicated derived state with useMemo/selectors (or compute inline if cheap)

Eliminate “state mirrors props” unless necessary

Replace multiple loosely related useState calls with useReducer when state transitions are complex

Avoid inconsistent state ownership (pick one owner for each piece of state)

Prevent stale closure bugs (effects and callbacks)

Step 4: Standardize Side Effects & Data Fetching

Without changing behavior:

Ensure fetch logic is consistent (one pattern across app)

Handle loading/error/success states consistently

Prevent duplicate requests and race conditions (abort, request keys, latest-only patterns)

Move side effects out of render and into hooks/effects

Ensure effect dependency arrays are correct (no accidental infinite loops)

If the repo uses React Query / SWR / Apollo / RTK Query, follow that library’s best practices and avoid reinventing caching.

Step 5: Normalize Form & Validation Logic

If forms exist:

Centralize validation rules and error display patterns

Remove ad-hoc validation sprinkled across components

Ensure submit logic is consistent (disable states, error handling, success handling)

Keep input parsing/sanitizing in one place

Step 6: Make Event Handling Predictable

Clean up interaction logic:

Replace inline complex handlers with named functions

Ensure keyboard/mouse interactions are consistent

Ensure debouncing/throttling is centralized and reused (not copied around)

Remove console.logs and debug UI logic

Step 7: Add Targeted Tests for Logic

Minimal, high-value tests:

Prefer unit tests for:

pure helpers

reducers

selectors

custom hooks (if test setup exists)

Add a small number of RTL/Cypress tests only if the repo already uses them

Focus on edge cases and regressions from the refactor

Do not introduce a whole new testing framework unless one already exists.

Output Requirements

Implement changes in small, reviewable chunks

For each chunk, write a short note in REFRACTOR_NOTES.md:

what changed

why it’s clearer/safer

how you verified no behavior changes (tests/manual)

If intent is ambiguous, add a NOTE: comment and choose the least risky refactor.

Success Criteria

After refactor:

Components are easier to read (less branching in JSX)

State ownership is clear

Derived state is not duplicated

Side effects are centralized and predictable

Logic is testable via small units

UI behavior remains unchanged