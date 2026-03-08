Perform a security-focused audit.

Identify:

Hardcoded secrets, API keys, or credentials

Missing or inconsistent input validation and sanitization

Injection risks (raw SQL, eval, unsanitized user content in HTML)

Auth and authorization: missing checks, inconsistent permission logic

CORS, CSRF, and public vs protected routes—ensure they are deliberate

Sensitive data in logs or error messages

Fix or document each finding. Prefer existing patterns (e.g. existing auth middleware, validation lib).

❗ Preserve behavior
❗ Do not add new auth mechanisms—use what the repo already has
❗ If unsure, add a NOTE: comment instead of guessing

Goal: no obvious footguns; unknowns documented.
