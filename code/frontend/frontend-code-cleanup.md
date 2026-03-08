Cursor Prompt: Frontend Repository Cleanup

You are acting as a senior frontend engineer doing a cleanup + quality pass on this repository.
Your goal is to improve clarity, consistency, and maintainability without changing user-visible behavior.

Scope & Constraints

❗ Do not introduce breaking changes

❗ Do not redesign the UI

❗ Do not add new features

✅ Small refactors are allowed if they reduce complexity

✅ Prefer incremental, reviewable changes

Step 1: High-Level Assessment

Start by scanning the repository and briefly summarize:

Framework(s) and tooling used

Project structure and intent

Any obvious smells or inconsistencies

Step 2: Code Organization

Improve structure where needed:

Normalize folder and file naming

Group related components, hooks, utils, and styles

Remove unused files, dead code, and commented-out blocks

Ensure imports are clean, ordered, and consistent

Step 3: Code Quality & Readability

Apply best practices:

Simplify overly complex components

Extract repeated logic into helpers or hooks

Improve variable, function, and component naming

Add missing types (if TypeScript) where ambiguity exists

Remove console.logs, TODOs, and debug artifacts

Step 4: Consistency Pass

Enforce consistency across the repo:

Formatting and style conventions

Component patterns (props, state, effects)

Error handling patterns

API/data-fetching patterns

CSS / styling approach

If conventions are unclear, infer and standardize on the most common existing pattern.

Step 5: Configuration & Tooling

Check and clean:

package.json scripts and dependencies

Remove unused dependencies

Verify ESLint / Prettier / TS config sanity

Ensure environment variables are documented or obvious

Step 6: Documentation

Lightweight improvements only:

Update README with accurate setup + run instructions

Add short comments where intent is non-obvious

No verbose documentation unless clearly needed

Output Instructions

Make changes directly in the code

Keep commits logically grouped (as if preparing a PR)

Explain why for any non-trivial refactor

If you’re unsure about a change, leave a comment instead of guessing

Success Criteria

At the end, the repo should feel:

Easier to read

Easier to extend

Less cluttered

More predictable

Do not aim for perfection — aim for clarity and calm.