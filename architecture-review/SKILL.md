---
name: architecture-review
description: 'Review architecture to markdown & graphic'
argument-hint: 'Describe the repo design or architecture'
user-invocable: true
disable-model-invocation: false
---

# Architecture Review

## When To Use

Review architecture to markdown & graphic for specific part, such as a feature, a module, or a component.

> User may provide specific part or just describe the part in natural language, then the agent will find the corresponding part and review its architecture.

> User may specific the depth or detail level of the review, such as function level, variants level, line level, etc. default function level with key lines.

## What This Skill Produces

- Markdown documentation of the architecture or designing (including but not limited to the components, their relationships, and interactions) with code references, output to docs/architecture-review-${part}.md, where ${part} is the specific part provided by user or identified by agent.
- Graphic representation of the architecture or designing using Mermaid diagrams, output to docs/architecture-review-${part}.md as well.

## Limitations

- Do not write any content that is not in real code comments or documentation, or not directly inferred from the code. The review should be based on the actual code and comments, not assumptions or external knowledge.
- Do not write any suggestion or judgment about the design or architecture, just describe and document what is there. The review should be objective and factual, not subjective or opinionated.

## Steps

1. Analyze the repository structure and identify key components.
2. Document the relationships and interactions between components.
3. Create visual diagrams to represent the architecture.