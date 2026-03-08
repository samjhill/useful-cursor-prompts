Perform a logging and observability audit.

Identify:

Inconsistent log levels (when to use info vs warn vs error)

Errors logged multiple times (e.g. in handler and in global middleware)

Missing request or correlation IDs where the repo already uses them

Sensitive data in log messages (passwords, tokens, PII)

No logging for critical paths (auth failures, payment steps, destructive actions)

Ad-hoc console.log or print statements that should use the app logger

Standardize on the existing logging mechanism. Add minimal context (request id, user id) where it already exists elsewhere. Remove or redact sensitive fields.

❗ Preserve behavior
❗ Do not introduce a new logging framework—use what the repo has
❗ Do not add verbose logging everywhere; focus on consistency and critical paths

Goal: predictable log levels, no double-logging, no secrets in logs.
