Audit this repository’s GitHub Actions workflows for expensive, slow, wasteful, or redundant CI/CD behavior, then implement safe fixes.

**Scope**

- Inspect all workflow files under `.github/workflows/**`
- Inspect related scripts and package files used by CI, including `package.json`, lockfiles, test scripts, build scripts, Dockerfiles, Makefiles, and deploy scripts
- Do not change application behavior unless required to fix CI reliability

**Look for**

- Workflows running on too many events, branches, or paths
- Missing `paths` / `paths-ignore` filters
- Duplicate workflows doing the same install/build/test work
- Jobs that should be skipped for docs-only or config-only changes
- Missing `concurrency` cancellation for pull requests
- Matrix jobs that are excessive or not justified
- Slow dependency installs without caching
- Cache keys that are too broad, too narrow, or never hit
- Rebuilding Docker images unnecessarily
- Running full E2E/integration tests on every push when smoke/unit tests would be enough
- Deploy jobs running on PRs or non-main branches
- Jobs that run serially but could safely run in parallel
- Jobs with unnecessarily large runners
- Long-running steps without timeout limits
- Artifacts/logs retained longer than needed
- Expensive third-party setup steps repeated across jobs
- Unpinned or outdated actions causing instability
- Missing fail-fast behavior where appropriate
- Jobs that fetch full git history when shallow checkout is enough

**Implement fixes**

- Add workflow-level and job-level `concurrency` where appropriate
- Add `timeout-minutes` to workflows, jobs, and steps with sane limits
- Add dependency caching for npm/yarn/pnpm/pip/bundler/gradle/maven, etc., as applicable
- Add path filters so irrelevant changes do not trigger expensive jobs
- Split cheap checks from expensive checks if needed
- Gate deploys to main/release branches only
- Add conditional execution for expensive jobs
- Use `actions/checkout` with minimal `fetch-depth` unless full history is required
- Reduce artifact retention to a practical minimum
- Consolidate duplicate jobs or workflows
- Prefer built-in setup action caching where available
- Keep security in mind: do not run privileged, deploy, or secrets-dependent jobs on untrusted PRs

**Deliverables**

1. A concise audit report listing each expensive or slow issue found
2. The exact files changed
3. A short explanation of each fix and expected impact
4. Any risks or behavior changes
5. A validation checklist

**Acceptance criteria**

- Existing CI intent remains intact
- PR workflows are cheaper and cancel stale runs
- Deploy/release workflows do not run unnecessarily
- Dependency installs use appropriate caching
- Expensive jobs are gated, path-filtered, or moved to manual, scheduled, or main-only triggers where reasonable
- Workflows remain valid GitHub Actions YAML
- No secrets are exposed
- No broad destructive rewrites without explanation

**Process**

Before editing, inspect the current workflows and summarize the planned changes. Then make the changes.

❗ Preserve application behavior except where required for CI reliability
❗ Do not expose secrets or broaden untrusted PR access to privileged jobs

Goal: cheaper, faster CI with the same safety intent.
