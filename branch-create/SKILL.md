---
name: branch-create
description: "Use when deciding whether to create a git branch or when creating, switching, preparing, isolating, or experimenting on a branch. Enforce conservative branch creation: create a branch only when explicitly requested, when work is experimental, or when the development goal may conflict with existing work that must remain stable. Name branches only from the development expectation or goal, without extra metadata."
---

# Branch Create

## Core Requirements

1. Create a branch only when one of these conditions is true:
   - The user explicitly asks to create or use a new branch.
   - The work is experimental, exploratory, risky, or likely to be discarded.
   - The development target may conflict with existing work, current behavior, release stability, or changes that must remain maintainable.

2. Do not create a branch for ordinary small edits, simple fixes, documentation updates, formatting, or low-risk work unless the user asks.

3. Name the branch only from the development expectation or goal.

4. Do not add extra metadata to the branch name.
