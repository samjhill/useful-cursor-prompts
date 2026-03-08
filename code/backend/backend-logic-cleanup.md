Cursor Prompt: Backend Logic Cleanup (Business Logic / Correctness / Maintainability)

You are a senior backend engineer performing a logic-focused refactor.
Objective: make the backend’s business logic easier to understand, safer, and more testable while preserving behavior.

Hard Constraints

❗ Preserve external behavior: API contract, auth rules, response shapes, side-effects

❗ No new features

❗ No DB schema changes (unless required for correctness and isolated behind a migration plan—otherwise comment)

✅ Refactor internals freely if behavior remains the same

Step 1: Map the System’s Logic Flow

Identify and briefly document (in comments or a short docs/logic-map.md):

Main request flows (top 5 endpoints or jobs)

Where business rules live today (controllers/routes, services, models, helpers)

What the “core domain” seems to be (entities + invariants)

Hotspots: duplicated logic, complex conditionals, inconsistent state handling

Step 2: Extract & Centralize Business Rules

Refactor to enforce a clean separation:

Controllers / Routes

Should only: parse input, call domain/service layer, translate errors → HTTP responses

Remove complex branching and DB logic from handlers

Domain / Service Layer

Put business rules here

Make rules explicit and named (e.g., canUserCancelOrder, calculateInvoiceTotal)

Prefer small pure functions where possible

Data Access Layer

Encapsulate DB queries so business logic doesn’t depend on ORM details

Avoid query duplication across endpoints

Step 3: Reduce Complexity in Hotspots

For each module with complex logic:

Break long functions into smaller ones with intention-revealing names

Replace nested conditionals with guard clauses

Replace “boolean soup” with descriptive predicates

Introduce small value objects / helpers if they reduce repeated parsing/formatting

Eliminate hidden coupling (e.g., functions that rely on external mutable state)

Step 4: Standardize Error Handling Semantics

Without changing response formats:

Define a small set of domain errors (e.g., NotFound, ValidationError, Conflict, Unauthorized, InvariantViolation)

Ensure each business rule failure maps consistently to the existing HTTP status + error shape

Ensure errors are thrown/returned once and handled centrally

Remove ad-hoc try/catch blocks unless they add real value

Step 5: Ensure Correctness of State Transitions

For stateful entities (orders, jobs, accounts, etc.):

Identify allowed states and transitions

Enforce transitions in one place (domain/service)

Add assertions/invariants for “should never happen” cases

Ensure idempotency where the system already expects it (don’t invent new behavior)

Step 6: Add Targeted Tests for Business Logic

Minimal but high value:

Focus on pure functions and service-layer rules

Add “table-driven” tests for edge cases

Cover:

permission checks

boundary values

state transitions

calculation correctness

error cases (expected error types)

Do not overbuild integration tests unless the repo already uses them.

Step 7: Output Requirements

Implement changes in small, reviewable chunks

For each chunk, write a short explanation in a REFRACTOR_NOTES.md:

what changed

why it’s safer/clearer

how behavior was verified (tests run, manual checks)

If you encounter ambiguous intent, add a NOTE: comment and choose the least risky option.

Success Criteria

After refactor:

Business rules are named and centralized

Handlers are thin

State transitions are explicit and enforced

Error semantics are consistent

Logic is testable with small unit tests

No behavior changes