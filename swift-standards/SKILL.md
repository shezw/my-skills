---
name: swift-standards
description: "Use when writing, reviewing, refactoring, or standardizing Swift apps, Swift packages, frameworks, Apple-platform features, SwiftUI/UIKit modules, async/await code, actors, Sendable boundaries, public APIs, tests, or dependency choices. This is an enforceable Swift engineering standard, not advisory guidance: Codex must inspect structure, classify responsibilities, apply the required architecture rules, reject non-compliant outcomes, and report verification results."
---

# Swift Standards

## Rule

This skill is an execution standard, not a suggestion list. When it is used, Codex must produce code and structure that can be checked against the required outcomes in the references.

## Procedure

1. Read [code standards](./references/code-standards.md) before changing Swift code.
2. Read [review checklist](./references/review-checklist.md) before declaring the task complete.
3. For new projects, unclear project shape, or dependency/tooling decisions, read [stack defaults](./references/stack-defaults.md).
4. Inspect the current project tree and Swift files before editing.
5. Classify the current project against the five required goals:
   - Project structure is navigable.
   - Responsibility boundaries are clear.
   - State and concurrency are safe.
   - Code quality is verifiable.
   - Agent execution has a delivery loop.
6. Fix violations that are in scope for the user request. Do not treat local formatting, renaming, or comment edits as sufficient when structural violations remain in scope.
7. Report what changed, what remains non-compliant if anything, and which verification commands ran.

## Completion Bar

Codex must not call a Swift standardization or refactor task complete unless it has:

- Inspected and summarized the relevant structure.
- Identified the target organization or confirmed the existing one is compliant.
- Moved, split, renamed, or rewired files when structure or responsibilities violate the standard and the request allows edits.
- Preserved buildability or clearly reported why verification could not run.
- Produced a short final report with structure changes, responsibility changes, and verification results.

## Resource Guide

- `references/code-standards.md`: Required Swift engineering rules and failure conditions.
- `references/stack-defaults.md`: Required defaults when the project has no stronger local convention.
- `references/review-checklist.md`: Required completion checklist for implementation and review.
