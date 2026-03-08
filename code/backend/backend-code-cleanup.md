Cursor Prompt: Backend Repository Cleanup

You are acting as a senior backend engineer doing a cleanup + maintainability pass on this repository.
Your goal is to improve clarity, correctness, consistency, and operability without changing external behavior.

Scope & Constraints

❗ Do not change API behavior, response formats, or auth semantics

❗ Do not change database schema (unless it’s clearly broken and you isolate it)

❗ Do not introduce new features

✅ Small refactors are allowed if they reduce risk/complexity

✅ Prefer incremental, reviewable changes with minimal surface area

Step 1: High-Level Assessment

Scan the repo and summarize:

Runtime/framework (Node/Express, FastAPI, Django, Rails, Go, etc.)

How it runs (entrypoint, server startup)

Where config lives (env vars, config files)

Data layer (DB, ORM, migrations)

Key modules (routes/controllers/services/jobs)

Call out obvious smells: duplicated logic, unclear structure, missing error handling, inconsistent patterns.

Step 2: Repository Structure

Make the structure predictable:

Normalize naming and directory layout (routes/controllers/services/repositories or equivalent)

Move misc logic out of route handlers into services

Consolidate shared utilities and constants

Remove dead code, unused files, and stale scripts

Ensure imports are clean and consistent

Step 3: API / Request Handling Hygiene

Without changing behavior:

Ensure input validation is consistent (schema validation, request parsing)

Ensure consistent error responses (central error handler / middleware)

Ensure HTTP status codes are used consistently

Remove console debugging, leftover test endpoints, commented code

If patterns differ, standardize on the most common existing pattern.

Step 4: Business Logic & Data Layer Cleanup

Improve maintainability:

Reduce “fat controllers” / route handlers

Extract repeated logic into services/helpers

Encapsulate DB operations (repository/data-access layer where appropriate)

Ensure transactions are used where needed (but don’t alter semantics)

Make naming precise (functions, variables, modules)

Step 5: Reliability & Observability (Light Touch)

Small, safe wins only:

Standardize logging (levels, structured fields if already used)

Ensure errors are logged once (avoid double-logging)

Add minimal context to logs where helpful (request id, user id if present)

Ensure timeouts/retries are not obviously dangerous (don’t invent new ones)

Step 6: Security & Secrets Hygiene

Do a quick pass for footguns:

Ensure secrets are not hardcoded

Ensure .env.example exists (or README documents required vars)

Validate CORS, auth middleware placement, and public routes are deliberate

Check for obvious injection risks (string SQL building, unsafe eval, etc.)
If you’re unsure, leave a comment rather than making speculative changes.

Step 7: Tests & Developer Experience

Keep it practical:

Ensure tests run reliably (fix broken imports/paths/setup)

Remove flaky or obsolete tests only if clearly dead

Add a few “golden path” tests only if the repo already has a test framework

Clean up scripts: dev, test, lint, typecheck, start

Step 8: Documentation

Update minimal docs:

README: setup, env vars, run, test, migrations (if applicable)

Add short inline comments where intent is non-obvious

Don’t write essays

Output Instructions

Make changes directly in code

Keep changes grouped logically (as if making a PR)

For any non-trivial refactor, explain:

what changed

why it’s safer/cleaner

how you verified behavior didn’t change (tests, manual run)

If uncertain, leave a // NOTE: or # NOTE: comment instead of guessing

Success Criteria

At the end, the repo should:

Be easier to navigate

Have consistent error handling and request flow

Have clearer separation of concerns

Be simpler to run locally and in production

Contain less clutter and fewer “mystery files”

Do not aim for perfection — aim for lower risk and higher clarity.