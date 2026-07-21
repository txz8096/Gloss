# Gloss

**Humans can feel when an interface is right. Coding agents need that judgment written down.**

Gloss turns visual taste into clear instructions that Codex can use when it builds the next screen.

## The problem

People often know what they like when they see it. They can point to a reference and say, “this feels right,” or reject a screen that looks generic. But that reaction is hard to hand to an AI coding agent.

A colour palette alone is not enough. An agent also needs to know what the product should emphasize, where character belongs, and what to avoid.

Without that context, each new screen can drift back toward the same generic defaults.

## What Gloss does

Gloss creates a reusable **Design DNA** for one product. It helps a builder move from visual reactions to decisions an agent can apply consistently.

```text
Curate → Calibrate → Commit → Apply
```

1. **Curate** — Collect references and anti-references. Mark what should carry forward and what should be avoided.
2. **Calibrate** — Compare two controlled directions. Choose the option that better expresses the product’s intended feeling and explain why when useful.
3. **Commit** — Save the result as Design DNA: principles, anti-principles, trade-offs, and tokens.
4. **Apply** — Use the included `gloss-apply` Codex skill to turn that Design DNA into a real new or updated screen in a codebase.

Gloss is not trying to generate a different product concept each time. It preserves the product’s task and structure, then gives the implementation a consistent visual point of view.

## Concrete example

Imagine a builder is creating a project-management tool for a small team.

### What they give Gloss

**Product context**

> Help a small team understand what needs attention today. It should feel calm, capable, and direct — never like a flashy productivity app.

**Visual choices**

- Reference: a warm, editorial interface with clear type and generous space.
- Reference: a practical dashboard with strong task hierarchy.
- Anti-reference: glossy gradient cards and decorative charts with no job.
- Calibration choice: use typography and position to establish hierarchy before adding accent colour.

### What Gloss produces

`design-dna.md`

```md
# Design DNA

## Intent
Make daily work feel calm and legible, while keeping the next action obvious.

## Principles
- Let hierarchy come from type, spacing, and position before colour.
- Keep the working surface quiet; reserve warmth for meaningful choices.
- Put useful task evidence close to the decision it supports.

## Anti-principles
- Do not use glossy gradients, decorative charts, or floating cards without a task-related purpose.

## Trade-offs
- Dense task views may reduce editorial spacing, but must keep one clear primary action.
```

`tokens.json`

```json
{
  "color": {
    "background": "#F2E9DF",
    "foreground": "#28211C",
    "accent": "#E3705E"
  },
  "surface": {
    "radius": "12px"
  }
}
```

### What Codex produces with the skill

The builder asks:

```text
Use $gloss-apply to create an empty state for the team’s task dashboard.
Read gloss/design-dna.md and gloss/tokens.json. Preserve the existing task flow.
```

Codex then produces working UI code for the empty state. It applies the hierarchy, spacing, surfaces, and boundaries in the Design DNA to a screen that was not part of the original curation.

## Install `gloss-apply` in Codex

The skill is a local Codex skill: install it once, then invoke it in any compatible project with `$gloss-apply`.

1. Clone this repository:

   ```bash
   git clone https://github.com/txz8096/Gloss.git
   ```

2. Copy the skill into Codex's local skills directory:

   ```bash
   mkdir -p ~/.codex/skills
   cp -R Gloss/.agents/skills/gloss-apply ~/.codex/skills/gloss-apply
   ```

3. Restart Codex, or begin a new task so it discovers the skill.

To update the skill later, pull the repository changes and repeat step 2. The source is [`.agents/skills/gloss-apply`](.agents/skills/gloss-apply).

### What you provide

Put the exported Gloss files in the project you want Codex to change:

```text
your-project/
├── gloss/
│   ├── design-dna.md  # Required: intent, principles, boundaries, trade-offs
│   └── tokens.json    # Optional: colour, type, surface values
└── src/
```

Then give Codex a specific implementation target: a component, route, or screen to create or restyle. `design-dna.md` tells Codex how to make visual decisions; `tokens.json` supplies reusable values. The schema is defined in [the export contract](.agents/skills/gloss-apply/references/export-contract.md).

### What you get back

| Output | What to expect |
|---|---|
| Working code | A changed component, route, or new screen in the target project. |
| Applied direction | Hierarchy, density, type, grouping, surfaces, and boundaries reflect the Design DNA, not only its colours. |
| Brief rationale | A concise account of which principles informed the main decisions and any trade-off that could not be preserved. |
| Validation | A rendered or tested result when the target project provides a local validation path. |

The skill preserves existing product behavior, content, accessibility, and information architecture unless you explicitly ask to change them. It does not invent a product concept or promise pixel-perfect reproduction from a screenshot.

### Copy-and-paste requests

Restyle an existing screen:

```text
Use $gloss-apply to restyle src/routes/ProjectOverview.tsx.
Read gloss/design-dna.md and gloss/tokens.json. Preserve the existing task flow,
copy, and data states. Render the result locally if this project supports it.
```

Create a new state within an existing product:

```text
Use $gloss-apply to create the empty state for the team task dashboard.
Read gloss/design-dna.md and gloss/tokens.json. Reuse existing components and
preserve the dashboard's navigation and task flow.
```

Review a screen that feels visually inconsistent:

```text
Use $gloss-apply to review and improve src/components/ActivityFeed.tsx.
Read gloss/design-dna.md. Keep the interaction behavior unchanged. Explain which
Gloss principles the current screen violates, then implement the highest-impact fixes.
```

## Try the prototype

Open [`prototype.html`](prototype.html) in a browser. It demonstrates the Gloss flow from product context through curation, calibration, and a final visual-system handoff.

For a working handoff you can copy, see [`examples/project-dashboard`](examples/project-dashboard).

## Current scope

This repository contains the interactive Gloss prototype and the agent handoff contract. The next implementation step is connecting the prototype’s final choices to downloadable `design-dna.md` and `tokens.json` files, then using `gloss-apply` against a small sample application.

## Repository layout

```text
.
├── prototype.html                 # Interactive product prototype
├── .agents/skills/gloss-apply/    # Reusable Codex skill
├── examples/project-dashboard/    # Copyable Design DNA handoff
└── docs/                          # Product and architecture notes
```
