Act as a senior engineer performing a dead-code and surface-area reduction pass.

Identify:

Unused files, exports, functions, types

Code paths no longer reachable

Over-abstracted utilities used only once

Safely remove or inline where appropriate.

❗ Preserve behavior
❗ Prefer deletion over abstraction
❗ If uncertain, leave a comment instead of guessing

Goal: fewer files, fewer concepts, same behavior.