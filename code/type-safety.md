Perform a type-safety audit (for TypeScript or typed JavaScript).

Identify:

Uses of `any`, `unknown` without narrowing, or loose types that hide bugs

Missing types on function parameters, return values, or exported APIs

Implicit type coercion or unsafe casts (e.g. `as` used to silence errors)

Public APIs with unclear or inconsistent types across the codebase

Types that duplicate runtime structure instead of describing intent

Tighten types incrementally. Prefer interfaces and type aliases that already exist. Add minimal types where ambiguity is high.

❗ Preserve behavior
❗ Do not rewrite working code for theoretical type purity
❗ If a type is genuinely hard to express, add a short comment and leave a focused type

Goal: fewer escape hatches; public surfaces and hot paths are clearly typed.
