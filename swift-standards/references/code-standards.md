# Swift Code Standards

This document is normative. Words such as must, required, prohibited, and not complete define acceptance criteria for Codex work. Existing project conventions may override these rules only when they are coherent, actively used, and do not violate the five core goals.

## Core Goals

Swift work must satisfy these goals:

1. Project structure is navigable.
2. Responsibility boundaries are clear.
3. State and concurrency are safe.
4. Code quality is verifiable.
5. Agent execution has a delivery loop.

## 1. Project Structure Is Navigable

### Required Outcome

Anyone opening the project must be able to determine where entry points, features, shared code, infrastructure, resources, and tests live without reading every file.

### Rules

- The project must have a deliberate directory structure that reflects feature, domain, platform, or module responsibility.
- App, scene, delegate, package, or framework entry points must be isolated from feature implementation.
- Feature code must be grouped by product capability or domain unless the project has a stronger documented architecture.
- Shared code must live behind a clear boundary and must not become a dumping ground.
- Infrastructure code such as networking, persistence, system integrations, analytics, logging, and dependency wiring must be identifiable.
- Resources and tests must be separated from production logic.
- A file's location must communicate its responsibility. File naming alone is not enough.

### Non-Compliant

- The project structure does not reveal business or module boundaries.
- New files are added to an already ambiguous location without improving the structure.
- Feature, shared, infrastructure, resource, and test files are mixed without a clear reason.
- App entry files contain substantial feature behavior.
- A refactor or standardization task leaves obvious structure violations untouched without reporting them as out of scope.

## 2. Responsibility Boundaries Are Clear

### Required Outcome

UI, state coordination, business rules, system capabilities, external services, and app composition must have separate responsibilities.

### Rules

- Views must express UI and user interactions. They must not own networking, persistence, complex business rules, or long-running orchestration.
- State, view models, controllers, reducers, or coordinators must handle UI state transitions and user intent coordination.
- Models and domain types must represent business concepts, invariants, and rules.
- Services, clients, repositories, and gateways must wrap networking, storage, system APIs, and external dependencies.
- App and scene entry points must handle startup, dependency composition, routing, lifecycle, and global configuration only.
- A type must have one primary responsibility. If it spans multiple layers, split it or explicitly document why it is a boundary object.

### Non-Compliant

- UI directly performs network, database, analytics, or complex domain decisions.
- Services depend on UI types or user-interface copy.
- Controllers, views, or view models become catch-all objects.
- Models are just untyped transport bags when domain rules are present.
- A refactor only changes style while leaving mixed responsibilities in place.

## 3. State And Concurrency Are Safe

### Required Outcome

UI state, asynchronous work, shared data, cancellation, and error states must be explicit and testable.

### Rules

- UI-bound state mutations must have an explicit main-thread or `MainActor` boundary.
- New asynchronous code must prefer `async`/`await` and structured concurrency over unbounded callbacks.
- Values crossing concurrency boundaries must be `Sendable` when applicable, or have documented isolation.
- Shared mutable state must be isolated by an actor, main actor, lock, serial queue, or another explicit mechanism.
- Loading, empty, error, permission, offline, refreshing, and cancellation states must be modeled explicitly when they affect behavior or UI.
- `Task.detached`, unstructured `Task`, locks, caches, manual retries, and manual cancellation must have a specific reason.

### Non-Compliant

- Code relies on implicit thread assumptions.
- Shared mutable state has no isolation boundary.
- Async work cannot be cancelled or reasoned about where cancellation matters.
- Error and loading states are scattered across unrelated booleans without a clear state model.
- `try?`, force unwraps, or silent failure hide meaningful runtime behavior.

## 4. Code Quality Is Verifiable

### Required Outcome

Every implementation, refactor, or standardization must leave evidence that behavior and structure were checked.

### Rules

- New behavior, bug fixes, edge cases, error paths, migrations, and concurrency fixes must have tests or a stated reason why tests cannot be added.
- Public and open APIs must have documentation comments explaining responsibility, inputs, outputs, errors, actor or thread expectations, and important limits.
- Non-obvious decisions must explain why, especially for concurrency isolation, caches, locks, compatibility workarounds, dependency choices, performance tradeoffs, and unchecked sendability.
- Relevant build, test, format, and lint commands must run before completion when available.
- If verification cannot run, Codex must report the blocker and the residual risk.

### Non-Compliant

- No verification result is reported.
- No tests are added for behavior changes and no reason is given.
- Public boundaries lack documentation.
- The change cannot be mapped to a concrete quality goal.
- Formatting, comments, or renames are presented as standardization while structural or responsibility violations remain in scope.

## 5. Agent Execution Has A Delivery Loop

### Required Outcome

When Codex uses this standard, the work must follow an inspect, decide, change, verify, report loop.

### Rules

- Codex must inspect the current structure and relevant Swift files before editing.
- Codex must identify which core goals are violated or explicitly confirm they are satisfied.
- Codex must define the target organization before broad file movement or architectural refactor.
- Codex must implement the structural and responsibility changes needed by the request.
- Codex must report file movement, responsibility changes, key code changes, verification commands, and remaining non-compliance.

### Non-Compliant

- Codex starts editing without understanding the structure.
- Codex only changes local code style when the request is architectural or standardization-oriented.
- Codex gives no before/after structure summary.
- Codex does not explain why the resulting organization satisfies the standard.
- Codex gives no verification result or residual-risk statement.

## Swift-Specific Rules

### SwiftUI

- SwiftUI `View` types must remain declarative.
- Heavy branching, formatting, IO, network calls, persistence, and domain decisions must move out of `body`.
- `@State` must be local UI state only. Broader state must use a clear observable model, environment value, dependency, or feature state object.
- Key UI states must be represented as explicit enum cases or equivalent structured state when boolean combinations become ambiguous.

### UIKit And AppKit

- View controllers must focus on lifecycle, binding, navigation, and platform integration.
- Business logic must live outside view controllers.
- Delegate callbacks must route to clear state or service boundaries instead of scattering mutation.
- SwiftUI and UIKit/AppKit bridges must be small adapters with clear ownership and lifecycle.

### API And Dependencies

- `public` and `open` surfaces must be minimal and documented.
- Protocols must exist for real variation, platform differences, extension points, or test seams. Empty speculative protocols are prohibited.
- New dependencies must have a clear reason and must not duplicate an existing foundation capability.
- Prefer Swift Package Manager unless the project has an existing enforced dependency system.
