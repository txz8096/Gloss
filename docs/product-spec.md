# Gloss product specification

## Purpose

Gloss turns a builder's visual judgment into durable instructions that an AI coding agent can apply to future product screens.

## Core loop

```text
Curate references → calibrate visual trade-offs → commit Design DNA → apply it in code
```

1. **Curate** reference and anti-reference signals alongside product context.
2. **Calibrate** with controlled comparisons that each test one visual tension.
3. **Commit** a Design DNA export: intent, principles, anti-principles, trade-offs, and optional tokens.
4. **Apply** the export with the included `gloss-apply` skill to a real component or screen.

## Product boundaries

- Preserve the product's information architecture and task flow.
- Treat anti-principles as hard boundaries, not optional styling suggestions.
- Use tokens as values and Design DNA as the decision-making layer.
- Do not infer pixel-perfect implementation details from a screenshot-only reference.

## Export contract

Every minimal handoff includes:

- A one-sentence intent describing the product feeling and job.
- Imperative visual principles with reasons.
- Anti-principles that state what the implementation must avoid.
- Trade-offs that explain how principles adapt on dense or task-heavy surfaces.
- Optional tokens for colour, typography, and component surfaces.

The complete machine-facing schema is in [the export contract](../.agents/skills/gloss-apply/references/export-contract.md).
