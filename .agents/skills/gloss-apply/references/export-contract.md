# Gloss export contract

Use this contract when reading or creating a minimal Gloss handoff.

## Required Design DNA fields

```md
# Design DNA

## Intent
One sentence describing the product feeling and job.

## Principles
- Imperative rule with a reason.

## Anti-principles
- Expression the implementation must avoid.

## Trade-offs
- Condition that changes how a principle applies on dense or task-heavy surfaces.
```

## Optional tokens

```json
{
  "color": {
    "background": "#F2E9DF",
    "foreground": "#28211C",
    "accent": "#E3705E"
  },
  "type": {
    "display": "Fraunces",
    "body": "DM Sans"
  },
  "surface": {
    "radius": "12px",
    "border": "1px solid #DDD4CA"
  }
}
```

Treat tokens as values and Design DNA as the decision-making layer. When they conflict, preserve an explicit user-confirmed Design DNA principle and report the conflict.
