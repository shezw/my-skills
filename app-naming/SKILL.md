---
name: app-naming
description: Use when naming an app, software product, developer tool, creative tool, AI product, feature suite, or productized workflow. Helps create durable brand names by extracting the real user action, semantic territory, style references, constraints, candidate names, rationale, and recommendation. Especially useful when the user wants names similar to products like Figma, Notion, Cursor, Linear, Raycast, Arc, Framer, or other concise modern software brands.
---

# App Naming

## Overview

Create names that feel like real app brands, not feature labels. Prefer names that are short, pronounceable, semantically suggestive, durable beyond the MVP, and close enough to the product's core action without spelling out every feature.

## Workflow

### 1. Build the Naming Brief

Before generating names, extract or infer:

- Product category
- Target users
- Core user action
- Transformation the product enables
- Desired language: English, Chinese, bilingual, or mixed
- Style references, such as Figma, Notion, Cursor, Linear, Arc, Raycast
- Functional closeness: abstract, balanced, or descriptive
- Forbidden words
- Words, tones, and prior candidates the user dislikes
- Existing product names or chosen candidates

If critical constraints are missing, ask one concise question. If enough context exists, proceed with stated assumptions.

### 2. Diagnose the Real Naming Target

Do not name the surface feature too early. Convert implementation details into deeper product behavior:

- "screenshot tool" -> visual intent capture
- "clipboard tool" -> handoff
- "prompt tool" -> translation of intent
- "annotation tool" -> pointing, marking, explaining, locating
- "AI editing tool" -> human-to-AI visual communication

Name the deeper product behavior, not the implementation detail.

### 3. Choose Naming Territories

Choose 2 to 4 semantic territories before creating candidates.

Useful territories:

- Visual language: graph, glyph, script, mark, form, notation
- Intent and clarity: signal, cue, lucid, plain, intent
- Pointing and location: locus, anchor, refer, vector, cursor
- Translation and handoff: relay, bridge, cast, send, pass
- Creation and editing: frame, forge, draft, shape, compose
- Cognition and understanding: parse, sense, read, infer, explain

Avoid staying only inside obvious words like screenshot, prompt, AI, clip, paste, annotate, or edit unless the user explicitly wants descriptive names.

### 4. Generate Candidates

For Figma, Notion, Cursor style names:

- Prefer one word.
- Prefer 2 to 3 syllables.
- Prefer real words, classical roots, or clean invented words.
- Avoid clunky compounds like `PromptShot`, `ClipBrief`, or `ImageMark`.
- Avoid names that sound like internal features.
- Avoid names that require long explanation to feel acceptable.
- Avoid trendy AI suffixes unless requested: `-AI`, `GPT`, `bot`, `copilot`.
- Make sure the name can survive product expansion.

Useful patterns:

- Real word with precise metaphor: `Cursor`, `Linear`, `Arc`
- Root-derived brand word: `Figma`, `Graphia`
- Abstract noun with product resonance: `Notion`
- Directional or action word: `Refer`, `Relay`, `Cast`
- Visual-symbolic word: `Glyph`, `Locus`, `Vector`

### 5. Evaluate the Shortlist

Score shortlisted names by:

- Product fit
- Brand feel
- Memorability
- Pronunciation
- Visual identity potential
- Semantic depth
- Expansion room
- Collision risk

Use web search for the final shortlist when the user asks for uniqueness, availability, trademark risk, domain checks, App Store checks, or when modern availability matters. State that lightweight search is not legal clearance.

## Output Format

Use this structure by default:

```markdown
## Naming Brief

- Product:
- Core action:
- Desired style:
- Naming direction:
- Avoid:

## Naming Strategy

- Territory 1:
- Territory 2:
- Territory 3:

## Candidates

1. **Name**
   - Why it works:
   - Risk:

2. **Name**
   - Why it works:
   - Risk:

## Recommendation

**Name**

Reason:

## Next Checks

- Trademark search
- Domain availability
- App Store / GitHub / npm name conflicts
```

Keep the list short unless the user asks for volume. Five strong candidates are better than thirty weak ones.

## Handling Negative Feedback

If the user rejects names strongly:

1. Stop generating more names immediately.
2. Summarize what was wrong with the previous direction.
3. Extract new constraints from the feedback.
4. Ask at most one clarifying question, or produce a much narrower next round.
5. Do not defend weak names.

## Quality Bar

Do not output a long list of mediocre names. Prefer one clear recommendation with reasoning over neutral dumping.

Before finalizing, ask:

- Does this sound like an app in a Dock, launcher, or browser tab?
- Is it a brand, or merely a feature label?
- Can it expand beyond the current MVP?
- Does it name the user's real action rather than the implementation detail?
