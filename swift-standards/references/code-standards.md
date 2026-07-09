# Swift Code Standards

This document defines a mature engineering baseline for Swift apps, Swift packages, frameworks, and Apple-platform features. Default to Swift 6 language mode for new work when dependencies allow it; for older codebases, use strict concurrency checking as a migration target and avoid adding new concurrency debt.

## Goals

- Keep module boundaries clear, state flow understandable, and behavior verifiable.
- Prefer Swift and Apple-platform practices that are boring, safe, and maintainable: structured concurrency, small public API surfaces, explicit errors, doc comments on public APIs, automated formatting, and focused tests.
- Separate UI, domain logic, networking, persistence, dependency wiring, and concurrency isolation so each layer can evolve without hidden coupling.

## Default Baseline

- Use Swift Package Manager by default for packages and third-party dependencies.
- Prefer SwiftUI for new Apple-platform UI unless UIKit/AppKit is clearly better for the target, existing codebase, or required control.
- Keep module depth to three meaningful levels by default; deeper structures need a clear domain, platform, or build reason.
- Preserve existing project conventions when they are coherent and actively used.

## Project Layout And Module Boundaries

- Prefer feature-first or domain-first layout over global buckets such as `Views`, `Models`, `Services`, and `Helpers`.
- Keep `App`, `Scene`, app delegate, and package entry points thin; they should compose dependencies, lifecycle, routing, and top-level configuration.
- Split a Swift package or framework only for real release, reuse, compile-time, platform, or ownership boundaries.
- Put tightly related view, state, use-case, client, and model code inside the same feature boundary until reuse or ownership pressure justifies promotion.
- Avoid empty protocols, facade layers, pure forwarding files, and directory nesting that only exists to look architectural.

## File Size And Split Heuristics

- Keep Swift files around 150 to 300 lines when practical; review files over 400 lines for mixed responsibilities.
- Review SwiftUI view files over 220 lines for extracted subviews, view state, formatters, or interaction handlers.
- Keep functions around 20 to 60 lines when practical; review functions over 80 lines for multiple decision blocks.
- Do not extract one-line helpers or single-use abstractions when they make the call site less clear.

## Readability And Naming

- Use `PascalCase` for types and `camelCase` for variables, functions, enum cases, and properties.
- Prefer domain language over vague names like `data`, `item`, `manager`, `helper`, `util`, or `processor`.
- Use `guard`, early returns, small local scopes, and exhaustive `switch` statements to keep the happy path clear.
- Make public APIs feel native to Swift rather than mirroring backend fields, JSON names, or Objective-C style.
- Use custom operators, property wrappers, result builders, and macros only when they materially improve call-site clarity.

## SwiftUI And UI State

- Keep SwiftUI `View` types declarative. Move heavy branching, formatting, IO, and domain decisions into state, use cases, or model layers.
- Use `@State` for local UI state only; use observable models, environment values, or explicit dependency injection for broader state.
- Do not start network requests, write databases, or perform expensive work directly in `body`.
- Represent loading, empty, error, permission, offline, and refreshing states explicitly.
- Add previews or preview fixtures for key states, not only the happy path.

## UIKit And AppKit

- Keep view controllers and coordinators focused on lifecycle, binding, navigation, and platform integration.
- Move business logic out of view controllers into use cases, models, reducers, or services with testable boundaries.
- Keep imperative UI updates centralized and predictable; avoid scattering state mutation across delegate callbacks.
- Bridge SwiftUI and UIKit/AppKit through small adapters with clear ownership and lifecycle rules.

## Concurrency And Data-Race Safety

- Prefer `async`/`await`, structured tasks, actors, and immutable values over callback chains and shared mutable state.
- Mark UI-facing models, controllers, and mutation points with `@MainActor` when their state is main-thread bound.
- Make values crossing concurrency boundaries `Sendable` where appropriate; document any unchecked sendability.
- Avoid global mutable singletons. If shared state is necessary, isolate it behind an actor, serial executor, lock wrapper, or clearly documented main-actor boundary.
- Use unstructured `Task`, `Task.detached`, locks, caches, manual cancellation, and retry loops only with an explicit reason and nearby comment.

## API, Protocols, And Abstraction

- Keep `public` and `open` API surfaces minimal. Prefer `internal`, `fileprivate`, or `private` until a stable boundary exists.
- Introduce protocols only for multiple implementations, platform variation, extension points, or stable test seams.
- Prefer concrete implementation first; extract protocols, generics, or builders after variation becomes real.
- Use value types for domain values where practical, and create explicit domain types instead of passing bare `String`, `Int`, or `UUID` across important boundaries.
- Use configuration structs for complex construction rather than long initializer parameter lists.

## Error Handling

- Return structured `Error` values for recoverable failures.
- Map lower-level errors to user-facing state at app boundaries; do not couple domain or client modules to UI copy.
- Avoid force unwraps and force tries in production paths. If an invariant truly makes them safe, make the failure message specific.
- Cover networking, parsing, storage, permission, cancellation, timeout, and migration errors in tests where behavior matters.

## Documentation And Comments

- Document all `public` and `open` types, functions, protocols, and properties.
- Use module or type documentation to explain responsibility, ownership, thread/actor expectations, and important limits.
- Explain why for non-obvious concurrency isolation, locks, caches, performance tradeoffs, compatibility workarounds, dependency choices, and unchecked `Sendable`.
- Do not use comments to repeat code that is already clear; prefer better names and smaller scopes.

## Testing And Tooling

- Add tests for new behavior, edge cases, error paths, concurrency fixes, migrations, and bug fixes.
- Keep domain logic testable without UI frameworks or live services.
- Use XCTest or Swift Testing according to the project baseline; use XCUITest for critical user flows when UI behavior is the subject.
- Run formatting, linting, relevant tests, and a target build before finishing non-trivial changes.
- Prefer swift-format or the project's existing formatter; SwiftLint is useful when configured to reinforce readability rather than ceremony.

## Dependencies

- Prefer the standard library, Apple frameworks, and small, actively maintained packages with stable APIs.
- Avoid multiple libraries for the same foundation capability, such as networking, dependency injection, image loading, persistence, or reactive state.
- When adding a dependency, record the problem solved, alternatives considered, platform impact, maintenance state, and binary or compile-time cost when relevant.

## Pending Project Decisions

- Whether Swift 6 language mode is a hard requirement or a migration target for legacy code.
- Whether SwiftUI is the default UI layer for all new surfaces or only for greenfield features.
- Whether the team standardizes on swift-format, SwiftLint, both, or existing Xcode formatting only.
