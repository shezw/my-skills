---
name: swift-standards
description: Use when writing, reviewing, refactoring, or designing Swift apps, Swift packages, frameworks, Apple-platform features, SwiftUI/UIKit modules, async/await code, actors, Sendable boundaries, public APIs, tests, or dependency choices. Covers module boundaries, UI architecture, concurrency and data-race safety, errors, documentation, testing, formatting, linting, and app-quality engineering.
---

# Swift Standards

## Overview

Use this skill to apply a consistent Swift engineering standard across Apple-platform apps, Swift packages, frameworks, and feature modules. Prefer the current project's established architecture when it is mature; use these references to fill gaps, review tradeoffs, or set defaults for new work.

## Procedure

1. Read [code standards](./references/code-standards.md) before implementing or reviewing Swift code.
2. For new projects, unclear architecture, or library choices, read [stack defaults](./references/stack-defaults.md).
3. During review, use [review checklist](./references/review-checklist.md) to check structure, UI state, concurrency, API shape, errors, documentation, tests, and tooling.
4. For existing projects, treat local conventions and shipping constraints as authoritative when they conflict with these defaults.
5. If the task also requires traceable implementation workflow, combine this skill with [agent-baseline](../agent-baseline/SKILL.md).

## Resource Guide

- `references/code-standards.md`: Detailed Swift coding and architecture standards.
- `references/stack-defaults.md`: Default choices for SwiftUI/UIKit, SPM, persistence, networking, dependency injection, testing, and quality gates.
- `references/review-checklist.md`: Compact review checklist for implementation and PR review.
