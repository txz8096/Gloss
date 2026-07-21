# Architecture

The current repository is intentionally dependency-free.

- `prototype.html` is a self-contained interactive demonstration of the Gloss flow.
- `.agents/skills/gloss-apply` is the Codex skill that reads a Gloss export and applies it to code.
- `examples/project-dashboard` is a generic handoff a user can inspect or copy into another project.

The prototype demonstrates the interaction model. The skill is the implementation handoff: it converts a chosen visual direction into working UI while preserving existing content, behavior, accessibility, and structure.
