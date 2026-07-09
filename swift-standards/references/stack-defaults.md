# Swift Stack Defaults

Use these defaults for greenfield Swift work or when an existing project has no clear convention. Existing coherent project choices take priority.

## Language And Toolchain

- Prefer Swift 6 language mode for new projects when dependencies allow it.
- For legacy projects, enable strict concurrency checking as early as practical and avoid adding new unchecked concurrency debt.
- Use Swift Package Manager for packages and third-party dependencies by default.
- Keep deployment targets aligned with the product's actual support policy; do not raise them only for convenience without owner approval.

## UI

- Prefer SwiftUI for new iOS, macOS, watchOS, visionOS, and multiplatform screens when it covers the required interaction and performance.
- Use UIKit/AppKit for complex existing surfaces, advanced platform controls, mature custom components, or cases where SwiftUI introduces avoidable risk.
- Use small adapter layers when bridging SwiftUI with UIKit/AppKit.
- Keep design-system primitives centralized rather than hard-coding colors, typography, spacing, and animation values across features.

## State And Architecture

- Start with simple local state and explicit dependencies before introducing a framework.
- Use observable models, use cases, clients, and repositories only where they clarify ownership or testability.
- Avoid defaulting to global service locators. Prefer initializer injection, environment values, or a small composition root.
- Introduce reducer-style architectures only when complex state transitions, testability needs, or team consistency justify them.

## Networking

- Prefer `URLSession` and `async`/`await` unless the project has a mature networking layer.
- Keep request construction, response decoding, authentication, retry policy, and error mapping in client modules rather than UI code.
- Model API responses separately from domain models when the external schema is unstable or poorly aligned with product language.

## Persistence

- Use lightweight persistence for lightweight needs: `UserDefaults`, app storage, keychain, files, or SQLite wrappers as appropriate.
- Use SwiftData or Core Data when object graph management, relationships, migrations, or platform integration justify the cost.
- Keep persistence models from leaking into UI and domain boundaries unless the project intentionally uses them as domain models.

## Async Streams And Reactive Code

- Prefer Swift Concurrency for new asynchronous flows.
- Use Combine when maintaining existing Combine code, integrating with Apple APIs, or when its operators materially simplify a stream.
- Avoid mixing Combine, callbacks, and async/await inside one feature without a clear boundary.

## Testing

- Use XCTest unless the project has adopted Swift Testing as its standard.
- Use XCUITest for critical user flows and accessibility-sensitive interactions.
- Use fakes or local test doubles for clients and persistence boundaries; avoid live network or production service dependencies in normal tests.
- Keep snapshot testing optional and targeted at visual regression risk, not as a replacement for behavior tests.

## Quality Gates

- Run formatting and linting according to the project standard.
- Build the relevant target or scheme after non-trivial code changes.
- Run related unit tests for logic changes and UI tests for user-flow changes when available.
- Treat concurrency warnings, force unwraps in production paths, and broad `try?` swallowing as review triggers.
