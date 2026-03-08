Perform a performance audit.

Identify:

**Frontend:** Unnecessary re-renders, missing memoization where props/state change often; large lists without virtualization; duplicate or redundant fetches; heavy work on the main thread during interaction.

**Backend:** N+1 queries, missing indexes for hot queries, unbounded result sets, expensive work in request path that could be deferred.

**Both:** Oversized bundles or dependencies; duplicate dependencies; synchronous work that could be async or batched.

Apply low-risk fixes: add keys, memoize where clearly beneficial, cap list sizes, use existing patterns. Document bigger wins (e.g. "consider virtualizing this list") in comments.

❗ Preserve behavior
❗ Prefer measurement over speculation—if you can't verify, note it instead of changing
❗ Do not introduce new perf tooling unless the repo already uses it

Goal: remove obvious inefficiencies; document likely wins for later.
