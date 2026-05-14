# Useful Cursor Prompts

A **code auditing system** built from Cursor prompts. Each prompt is a focused, repeatable audit you can run against a codebase so Cursor acts like a senior engineer doing a specific kind of pass—without changing behavior unless you intend to.

**How to use:** Open a prompt file, copy its contents into Cursor (e.g. in Chat or Composer), and run it in the repo you want to audit. Run from the repo root so Cursor sees the full project.

---

## Running with Cursor Automations

You can run these audits automatically using [Cursor Automations](https://cursor.com/docs/cloud-agent/automations) (cloud agents triggered by schedule, GitHub events, webhooks, etc.).

1. **Create an automation** at [cursor.com/automations/new](https://cursor.com/automations/new).
2. **Choose a trigger** (e.g. scheduled weekly, or when a pull request is opened).
3. **Set the target repo and branch** in the trigger (the codebase you want to audit).
4. **Write the automation prompt.** In the prompt, tell the agent to run one of the audits. Either:
   - **Inline:** Paste the full contents of the prompt file (e.g. `code/boundaries.md`) and add: *“Run these instructions against the codebase in this repo. Apply the changes. Preserve behavior.”*
   - **Reference this repo:** *“Clone or read from https://github.com/samjhill/useful-cursor-prompts. Run the audit in `code/boundaries.md` (or [other path](code/)) on this repository. Apply the changes. Preserve behavior.”*
5. **Enable “Open pull request”** in the automation’s tools if you want the agent to create a branch and open a PR with the changes.
6. **Save and run.** The automation will run when the trigger fires (or you can trigger manually if the trigger type supports it).

**Tips:** Use one automation per audit type (e.g. “dead-code audit”) so each run is focused. For a full pass, run automations in the [suggested order](#suggested-order) and merge each PR before triggering the next, or use a webhook trigger and pass the audit name in the payload so one automation can run different audits.

Automations use cloud agents and are [billed accordingly](https://cursor.com/docs/models-and-pricing#model-pricing).

---

## Suggested order

Run audits in this order when doing a full pass. Earlier passes clarify structure and surface area; later ones refactor logic and polish.

| Order | Prompt | When to use |
|-------|--------|-------------|
| 1 | [boundaries](code/boundaries.md) | First. Tighten module/layer boundaries so later audits don’t cross unclear lines. |
| 2 | [dead-code](code/dead-code.md) | Remove unused code and shrink surface area before renaming or refactoring. |
| 3 | [dependencies](code/dependencies.md) | Trim unused and duplicate deps; check for outdated or insecure packages. |
| 4 | [naming-clarity](code/naming-clarity.md) | Improve names so complexity and state passes are easier to reason about. |
| 5 | [type-safety](code/type-safety.md) | For TypeScript/typed codebases. Tighten types and reduce `any` / loose types. |
| 6 | [complexity](code/complexity.md) | Reduce accidental complexity (long functions, nested conditionals, unclear flow). |
| 7 | [state-ownership](code/state-ownership.md) | Clarify state ownership and data flow (especially for frontend/stateful code). |
| 8 | [edge-case](code/edge-case.md) | Audit error handling, null/empty states, and loading/failure states. |
| 9 | [security-audit](code/security-audit.md) | Secrets, injection, auth, input validation; document or fix footguns. |
| 10 | [test-suite](code/test-suite.md) | Trim low-value tests and add a few high-signal tests where risk is highest. |
| 11 | [github-actions-ci-cost](code/github-actions-ci-cost.md) | When CI is slow or costly: audit workflows for waste; safe YAML and CI-script fixes (concurrency, caching, path filters, gates). |
| 12 | **Frontend** [code cleanup](code/frontend/frontend-code-cleanup.md) → [logic cleanup](code/frontend/frontend-logic-cleanup.md) → [a11y](code/frontend/a11y.md) | If the repo has a frontend: structure, then state/effects/forms, then accessibility. |
| 13 | **Backend** [code cleanup](code/backend/backend-code-cleanup.md) → [logic cleanup](code/backend/backend-logic-cleanup.md) → [logging](code/backend/logging.md) | If the repo has a backend: structure, then business logic, then logging consistency. |
| 14 | [performance](code/performance.md) | After main cleanups. Obvious inefficiencies (N+1, re-renders, bundle size); document bigger wins. |
| 15 | [engineer-onboarding](code/engineer-onboarding.md) | Last. Improve README, entry points, and inline comments so a new engineer can be productive quickly. |

**Quick passes:** For a single concern, run only the prompt you need (e.g. just [dead-code](code/dead-code.md) or [naming-clarity](code/naming-clarity.md)). Order matters less when you’re not doing a full pass.

---

## Prompts by category

### Cross-cutting (any stack)

| Prompt | One-line description |
|--------|------------------------|
| [boundaries](code/boundaries.md) | Audit module and layer boundaries; keep UI, business logic, and data layer clearly separated. |
| [dead-code](code/dead-code.md) | Find and safely remove unused files, exports, functions, and unreachable code. |
| [dependencies](code/dependencies.md) | Audit deps: unused, duplicate, outdated, or insecure; trim and document. |
| [naming-clarity](code/naming-clarity.md) | Improve names for functions, variables, components, and files so they describe intent. |
| [type-safety](code/type-safety.md) | For TypeScript/typed code. Tighten types, reduce `any`, clarify public API types. |
| [complexity](code/complexity.md) | Break long functions, use guard clauses, name boolean expressions; reduce accidental complexity. |
| [state-ownership](code/state-ownership.md) | Review state ownership and data flow; one clear owner per piece of state, prefer derived over stored. |
| [edge-case](code/edge-case.md) | Audit error handling, null/undefined/empty states, and missing loading/failure states. |
| [security-audit](code/security-audit.md) | Secrets, injection, auth, input validation; fix or document footguns. |
| [performance](code/performance.md) | Frontend and backend: re-renders, N+1, bundle size; low-risk fixes and documented wins. |
| [test-suite](code/test-suite.md) | Evaluate test value; remove duplicates and implementation-detail tests, add high-signal tests where risk is high. |
| [github-actions-ci-cost](code/github-actions-ci-cost.md) | Audit GitHub Actions for slow or wasteful CI/CD; concurrency, caching, path filters, gates, timeouts—without changing app behavior unless needed for CI reliability. |
| [engineer-onboarding](code/engineer-onboarding.md) | Improve README, entry points, and comments so a new engineer can be productive in about an hour. |

### Frontend

| Prompt | One-line description |
|--------|------------------------|
| [frontend-code-cleanup](code/frontend/frontend-code-cleanup.md) | Repo cleanup: structure, consistency, tooling, formatting; no behavior change. |
| [frontend-logic-cleanup](code/frontend/frontend-logic-cleanup.md) | Deeper refactor: state, derived state, side effects, forms, event handling; thin components, extract logic. |
| [a11y](code/frontend/a11y.md) | Accessibility: ARIA, keyboard focus, labels, contrast; semantic HTML and existing a11y patterns. |

### Backend

| Prompt | One-line description |
|--------|------------------------|
| [backend-code-cleanup](code/backend/backend-code-cleanup.md) | Repo cleanup: structure, API hygiene, error handling, security footguns; no external behavior change. |
| [backend-logic-cleanup](code/backend/backend-logic-cleanup.md) | Deeper refactor: business rules, services, state transitions, error semantics; thin handlers, testable logic. |
| [logging](code/backend/logging.md) | Log levels, request IDs, no double-logging or secrets in logs; use existing logging mechanism. |
