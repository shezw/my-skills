# Swift Stack Defaults

These defaults are mandatory when a project has no stronger local convention. Existing coherent project choices take priority only when they still satisfy the five core goals.

## Project Shape

- New app work must separate entry points, features, shared code, infrastructure, resources, and tests.
- New package work must separate public API, internal implementation, tests, and resources.
- Feature code must be grouped by product capability or domain.
- Shared code must be promoted only after at least two real consumers or a clear platform boundary exists.

## Language And Toolchain

- New projects must target Swift 6 language mode when dependency constraints allow it.
- Legacy projects must avoid adding new strict-concurrency violations.
- Swift Package Manager is the default dependency system.
- Deployment target increases require product or owner approval.

## UI

- SwiftUI is the default for new UI when it supports the required interaction, performance, and platform behavior.
- UIKit/AppKit remains valid for existing surfaces, advanced platform controls, mature custom components, or risk reduction.
- Bridges between SwiftUI and UIKit/AppKit must be small and explicit.
- Design tokens such as colors, typography, spacing, and animation values must be centralized.

## State And Architecture

- Start with explicit local state and dependencies.
- Add observable models, use cases, clients, repositories, coordinators, or reducers only when they clarify ownership, testability, or state transitions.
- Global service locators are prohibited unless the project already standardizes on one and its boundary is documented.
- Dependency injection must be explicit through initializers, environment values, composition roots, or a documented project mechanism.

## Networking

- Use `URLSession` with `async`/`await` unless the project already has a mature networking layer.
- Request construction, decoding, authentication, retries, and error mapping must live outside UI code.
- External API DTOs must be separated from domain models when schemas do not match product language or stability needs.

## Persistence

- Use the smallest persistence mechanism that satisfies product needs.
- Use SwiftData or Core Data only when relationships, migrations, object graph management, or platform integration justify the cost.
- Persistence models must not leak into UI or domain boundaries unless the project intentionally uses them as domain models.

## Testing And Quality Gates

- XCTest or Swift Testing must cover meaningful domain behavior.
- XCUITest must cover critical flows when UI behavior is the change.
- Normal tests must not depend on live production services.
- Non-trivial changes must build the relevant target or scheme and run related tests when the toolchain is available.
