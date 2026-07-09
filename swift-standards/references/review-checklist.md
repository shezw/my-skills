# Swift Review Checklist

Use this checklist as an acceptance gate. A Swift standardization, refactor, or review is not complete until every in-scope item is either satisfied or explicitly reported as remaining work.

## 1. Project Structure Is Navigable

- Does the directory structure reveal entry points, features, shared code, infrastructure, resources, and tests?
- Are feature, domain, platform, or module boundaries visible from file locations?
- Are app, scene, delegate, package, and framework entry points thin?
- Are new or moved files placed where their responsibility is clear?
- Has Codex reported any structure violations that remain out of scope?

## 2. Responsibility Boundaries Are Clear

- Are UI, state coordination, domain rules, services, clients, resources, and tests separated?
- Are views free of networking, persistence, complex business rules, and long-running orchestration?
- Are controllers, view models, reducers, or coordinators focused on state transitions and user intent?
- Are services and clients free of UI dependencies?
- Does every major type have one primary responsibility?

## 3. State And Concurrency Are Safe

- Are UI-bound mutations isolated to `MainActor`, main thread, or another explicit boundary?
- Are async operations structured, cancellable where needed, and not hidden behind uncontrolled callbacks?
- Are shared mutable states isolated by actor, lock, queue, main actor, or equivalent?
- Are loading, empty, error, permission, offline, refreshing, and cancellation states explicit where they matter?
- Are `Task.detached`, unstructured tasks, unchecked sendability, caches, locks, retries, and timeouts justified?

## 4. Code Quality Is Verifiable

- Are new behavior, bug fixes, edge cases, error paths, migrations, and concurrency fixes tested or explicitly marked untestable with a reason?
- Are public/open APIs documented?
- Do comments explain non-obvious decisions instead of restating code?
- Did Codex run relevant build, test, format, and lint commands?
- If verification could not run, is the blocker and residual risk reported?

## 5. Agent Execution Has A Delivery Loop

- Did Codex inspect the current structure before editing?
- Did Codex identify which core goals were violated?
- Did Codex define or confirm the target organization?
- Did Codex implement the required structural and responsibility changes rather than only local style edits?
- Did Codex report file movement, responsibility changes, key code changes, verification results, and remaining non-compliance?

## Hard Failure Conditions

Any of these means the task is not complete:

- No project structure inspection occurred.
- No target organization was defined or confirmed for an architectural or standardization task.
- Structural or responsibility violations remain in scope but are ignored.
- Verification results are absent.
- The final report does not explain what changed and why it satisfies the standard.
