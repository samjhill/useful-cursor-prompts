Perform a dependencies audit.

Identify:

Unused dependencies in package.json (or equivalent)

Duplicate or overlapping packages (e.g. two date libs, two HTTP clients)

Outdated major or minor versions with known security or compatibility issues

Missing or stale lockfiles; inconsistent versions across workspaces or apps

Optional: security advisories for direct dependencies (if tooling exists)

Remove unused deps. Prefer upgrading in range over major upgrades unless necessary. Document any major upgrade or removal that needs manual testing.

❗ Preserve behavior
❗ Do not upgrade to breaking major versions unless you document and scope the change
❗ If a dep is "maybe unused," leave a comment instead of removing

Goal: fewer, up-to-date dependencies; no obvious duplicates or dead weight.
