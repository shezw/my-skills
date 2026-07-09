# Swift Review Checklist

## Structure

- Is the code organized by feature or domain boundary rather than broad technical buckets?
- Are app, scene, delegate, and package entry points thin?
- Is each package, framework, or module split justified by reuse, release, platform, ownership, or build isolation?
- Are there empty protocols, facades, pure forwarding files, or directories that add navigation cost without clarity?

## UI And State

- Are SwiftUI views declarative and free of heavy IO, business logic, and expensive work in `body`?
- Are loading, empty, error, permission, offline, and refreshing states explicit?
- Is state kept close to its owner, with broader state passed through clear observable models or dependencies?
- Are key UI states covered by previews, fixtures, unit tests, or UI tests where appropriate?

## Concurrency

- Are UI-bound mutations isolated to `MainActor` or another explicit boundary?
- Are cross-task values `Sendable` where appropriate, with any unchecked cases documented?
- Are unstructured `Task`, `Task.detached`, locks, caches, cancellation, timeout, and retry logic justified and easy to reason about?
- Is global mutable state avoided or isolated behind an actor, lock, or documented main-actor boundary?

## API And Errors

- Is the `public` or `open` surface minimal and documented?
- Are protocols, generics, property wrappers, macros, and builders used for real variation rather than speculative abstraction?
- Are recoverable failures represented as structured errors and mapped to user-facing state at the right boundary?
- Are force unwraps, force tries, and silent error swallowing avoided in production paths?

## Documentation And Dependencies

- Do public APIs explain responsibility, parameters, return values, errors, actor/thread expectations, and important limits?
- Do comments explain why for concurrency, caches, locks, compatibility workarounds, and performance tradeoffs?
- Are new dependencies necessary, maintained, platform-compatible, and not duplicating an existing foundation library?
- Is any dependency cost or architectural impact noted when relevant?

## Verification

- Are new behavior, edge cases, error paths, migrations, concurrency fixes, and bug fixes covered by tests?
- Can domain logic be tested without UI frameworks or live services?
- Has the relevant target or scheme been built?
- Have formatting, linting, and related tests been run or explicitly deferred with a reason?

## Confirm With Project Owner

- Is Swift 6 language mode mandatory, or is strict concurrency a migration target for now?
- Is SwiftUI the default for new UI, or should UIKit/AppKit remain primary for this project?
- Should the project standardize on swift-format, SwiftLint, both, or existing local tooling?
