Perform an edge-case and error-handling audit.

Identify:

Places where errors are swallowed or logged inconsistently

Unchecked null/undefined/empty states

Missing loading or failure states

Normalize error handling using existing patterns only.

❗ Preserve API/UI behavior
❗ Do not invent new error types unless already implied

Add comments where behavior is unclear.