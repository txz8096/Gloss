# Gloss — PRD (OpenAI Build Week, July 13–21, 2026)

**Tagline:** Humans see it. Machines read it. Gloss translates.

**Track:** Developer tools (agentic workflows)  
**Builder:** Melissa Tang, solo  
**Deadline:** July 21, 5:00pm PDT  
**Judged on:** technical implementation, design and UX, potential impact, and quality of idea (per the Build Week FAQ, supplied in the project brief).

## 1. Product thesis

Most AI builders have visual judgment before they have design vocabulary. They can say “this feels off,” choose one reference over another, and reject a generic dashboard. They cannot reliably turn those reactions into directions that an agent can apply to a screen it has not yet seen.

Gloss turns visual judgment into a portable, evidence-backed design memory. It begins with curation, exposes the consequential trade-offs through small visual comparisons, and exports instructions an implementation agent can follow.

The product is not a moodboard generator or a theme picker. It is a **taste-calibration system**:

```text
References + anti-references
          ↓
Intent and candidate design principles
          ↓
Taste Lab: inspect evidence and trade-offs
          ↓
Calibration: choose A or B on a meaningful visual tension
          ↓
Decision memory: principles, boundaries, trade-offs, provenance
          ↓
Tokens + DESIGN.md + AGENTS.md + MCP context
```

## 2. Problem

AI builders using v0, Lovable, and Codex often know when an interface misses the mark but lack a way to make that reaction durable. The usual workflow is a cycle of vague prompts such as “more premium” or “less generic,” followed by fresh output that loses the lesson from the last iteration. The result converges on familiar defaults: equal card rows, blue-purple accents, interchangeable type, and decoration used as hierarchy.

Existing tools solve parts of the problem:

- Token extractors turn a reference into values but usually discard the reasoning that makes the values transferable.
- Moodboard protocols turn images into written direction but leave the user to imagine the result and correct the agent later.
- Curation products help people collect references but do not make that curation executable.
- Frontend prompt skills counter generic output with forceful defaults, but the defaults are the skill author’s taste rather than the project’s own design logic.

Gloss closes the loop: **curate → interpret → see → choose → remember → commit.**

## 3. User

**Beachhead:** a non-designer building a real product with AI coding tools. They have strong visual reactions, can gather examples, and need an agent to carry those decisions into future screens.

**Secondary:** a designer who wants their curation and judgment to survive handoff into an AI-assisted build workflow.

## 4. Positioning

| Alternative | What it does | Gloss’s difference |
|---|---|---|
| tweakcn / StyleGlide | A prompt or image becomes a theme or component preview | Gloss starts with a weighted reference board, adds anti-references and choice-based calibration, then exports standing design instructions instead of CSS alone. |
| mood-protocol | A moodboard becomes a `mood.md` perceptual brief | Gloss uses this upstream idea, then renders the direction, lets the user correct it, and stores decisions before export. It can emit a compatible perceptual section. |
| Sen Lin’s taste-skill | A website becomes tokens plus inferred design principles | Gloss adopts its evidence-and-trade-off structure, but applies it to the user’s own reference set and turns disputed principles into user-facing decisions. |
| Leonxlnx’s taste-skill | A coding agent receives anti-generic frontend rules | Gloss supplies project-specific direction to the implementation layer. It uses anti-slop checks as guardrails, not universal visual doctrine. |
| Savee / Cosmos | People collect and revisit references | Gloss treats the board as an input surface for decisions and agent context. |

## 5. Source methodology

Gloss is an original synthesis of three useful ideas. Each occupies a different point in the workflow.

### 5.1 Perceptual intent from mood-protocol

`mood.md` is a perceptual brief built from images, designer notes, and anti-references. It captures intent before a formal design system exists: essence, colour, typography, space, material, emotional register, principles, exclusions, and instructions for an agent.

**Gloss adaptation:** the Board captures likes, anti-likes, and optional notes. Distill begins by writing a short intent statement and boundaries. Anti-references are first-class evidence, not a secondary filter.

### 5.2 Evidence and trade-offs from taste-skill

Sen Lin’s taste-skill separates a practical Design Map from Taste DNA. Its useful unit is not “radius: 6px,” but a causal statement:

```text
Trigger → Decision → Reason → Evidence → Trade-off
```

**Gloss adaptation:** each candidate direction contains 3–4 principles in that form. Evidence links back to the specific references and user notes that informed it. A principle that cannot name evidence is only a hypothesis and must not be exported as a hard rule.

### 5.3 Implementation guardrails from Leonxlnx’s taste-skill

Leonxlnx’s project uses controllable dimensions such as visual variance, motion intensity, and density, along with concrete frontend checks. Its value is treating implementation quality as more than a palette choice: spacing, typography, motion, interaction states, responsiveness, and performance all carry the visual language.

**Gloss adaptation:** Gloss provides an implementation section that names what to avoid and how to apply the active direction. It does not impose a fixed font, motion style, or asymmetric layout on every product. Project-specific principles win.

### 5.4 The missing step: preference elicitation

The source methods infer or describe taste. Gloss adds **calibration**. When a principle is plausible but ambiguous, show two controlled variants and ask the user to choose.

The product learns from revealed judgment, not only from the user’s ability to describe it. An optional explanation records the user’s reasoning in their own language.

## 6. Core loop

The demo is the loop:

1. **Curate.** Paste 8–12 image URLs or drop files. For each reference, mark like or anti-like and optionally add a one-line note. A mixed reaction is valid: “love the type, reject the colour.”
2. **Distill.** One model call produces an intent statement, boundaries, three named directions, candidate principles, and evidence references.
3. **Taste Lab.** Select a direction and inspect it on the template dashboard. The interface shows a compact Design Map, Taste DNA cards, provenance chips, and the trade-off each principle accepts.
4. **Calibrate.** Answer up to three A/B questions for the active direction. Each comparison isolates one design tension. The user can choose A, B, both, neither, or skip; explanation is optional.
5. **Review the preference ladder.** Gloss ranks every explored direction as a provisional preference, retains the alternatives, and lets the user reopen, shortlist, or directly compare any two.
6. **Correct.** Change a Board reaction, revisit a comparison, or tune a detail. Gloss updates the active decision memory and rerenders the template without another model call when the change is a local token or principle decision. Re-Distill only when the reference set changes materially.
7. **Commit.** Export tokens, a human-readable design brief, agent instructions, and MCP context.
8. **Validate.** Ask Codex for a screen absent from the template. It reads the exported guidance and applies the direction to a new problem.

## 7. Taste Lab and calibration

### 7.1 The Design Map

The Design Map is the concrete layer: palette roles, type character and scale, spacing rhythm, radii, borders and shadows, grid, and motion. It gives an implementation agent usable values.

### 7.2 Taste DNA

Taste DNA is the judgment layer. Each principle includes:

| Field | Meaning |
|---|---|
| Trigger | The design choice being made, such as “how should primary action stand out?” |
| Decision | The chosen response. |
| Reason | Why this response fits the project intent. |
| Evidence | References, notes, and calibration decisions supporting it. |
| Trade-off | The benefit knowingly given up to preserve the principle. |
| Confidence | High, medium, or low, based on evidence and user confirmation. |

Example:

```md
## Principle: Presence through restraint

Trigger: How should hierarchy work on the main dashboard?
Decision: Use warm paper, ink-like type, and one muted accent. Prefer spacing and
type weight to elevated containers.
Reason: The product should feel considered and human, rather than perform a
generic SaaS aesthetic.
Evidence: Reference 03 and 07; user chose the warm-paper A/B variant and noted
that it “feels calm without trying to look expensive.”
Trade-off: Some dense scanning speed is sacrificed; task-heavy views need a
more compact working surface.
Confidence: High
```

### 7.3 A/B prompts: the design optometrist

Calibration is not “which is prettier?” It is a lightweight preference-elicitation loop: people who cannot name a visual style can still say which of two versions feels more like their product. Every pair must test one named tension, use the same product content, and make the difference legible in one view. The first version uses the existing dashboard template and CSS-variable variants. It does not generate new interface concepts during the interaction.

| Tension | Variant A | Variant B | What Gloss can learn |
|---|---|---|---|
| Hierarchy | Accent-colour CTA | Type and position create emphasis | Whether colour is for persuasion or reserved for status. |
| Density | Compact tool surface | Spacious editorial surface | Whether understanding or scanning speed is the default priority. |
| Grouping | Floating card containers | Dividers and negative space | Whether structure should feel elevated or embedded. |
| Personality | Neutral system type | Distinctive display moments | Where character belongs in the interface. |
| Proof | Product screenshots lead | Atmospheric art direction leads | Whether the product should demonstrate value or establish a mood first. |

After a selection, Gloss asks: **“What made you choose this?”** The user may skip. If they answer, Gloss stores the raw sentence beside its normalized principle. The raw sentence remains visible because it carries context that a compressed rule can lose.

Choices are deliberately richer than a forced vote:

- **A** or **B** records a relative preference.
- **Both** records that the tension is not decisive or that the directions can be combined.
- **Neither** is negative evidence: generate or rank away from both expressions of the tension.
- **Skip** means no preference data was collected; it must not be interpreted as indifference.
- **Something else…** opens a short text field for the user's own correction, such as “A's type, but B's density.”

Gloss should begin with broad, visibly distinct comparisons, then select later comparisons that clarify the closest candidates. It should never claim a user has made a permanent choice from a single click.

### 7.4 Preference ladder and revisitability

The A/B interaction is the input method, not the destination. The result is a living **Preference Ladder**: a ranked, expandable record of every explored direction. A direction that loses one comparison is not eliminated.

```text
Your current taste ranking                         based on choices so far

Strong match       1. Quiet Editorial             [preview]
                   2. Warm Studio                 [preview]
Worth revisiting   3. Playful Graphic              [preview]
Less aligned so far 4. Dense Product UI            [preview]

                         [Show all explored directions]
```

Avoid a falsely precise 1–12 score. Group directions into **Strong match**, **Worth revisiting**, and **Less aligned so far**, with a small confidence label only where it changes the next action: for example, “not compared enough yet.” A user can expand any direction to see its larger preview, traits, comparison history, and derived rationale; pin up to three to a shortlist; or choose **Compare with current favourite**.

The ladder supports revision without restarting the session. Users can reopen an abandoned option, compare any two directions again, move a direction manually, or choose a lower-ranked direction as the active one. Manual ordering and explicit user statements outrank inferred ranking.

### 7.5 Decision memory

The decision memory is the product’s lasting asset. It contains confirmed principles, explicit boundaries, preference evidence, preserved alternatives, evidence, trade-offs, and confidence. It lets a user revisit why a decision exists rather than re-litigating it with each new screen.

When evidence conflicts, Gloss shows the conflict instead of silently averaging it. For example: “You chose an editorial, spacious shell but also need fast bulk review.” The export can resolve this by distinguishing **brand shell** from **task surface**. The user-facing synthesis is framed as an observation—“You seem to prefer…”—and names the choices that support it rather than presenting an opaque AI verdict.

## 8. Information architecture

One Next.js app with two views and one export panel:

| View | Contents | Not building |
|---|---|---|
| **Board** | Image grid, like/anti-like/mixed reaction, one-line notes, Distill button | Masonry canvas, collections, social, search |
| **Design Mode** | Three named directions, live template dashboard, Taste Lab cards, provenance chips, five sliders, up to three A/B calibration prompts, Preference Ladder with expandable previews and a shortlist, advanced token disclosure | Multiple templates, imported product artifact, open-ended semantic chat |
| **Export** (panel in Design Mode) | `tokens.json`, `DESIGN.md`, `mood.md`-compatible perceptual section, `AGENTS.md` block, MCP connection instructions | A third tab. Export is a moment, not a place. |

## 9. Perceptual sliders

Sliders are relative to the selected direction. Moving “Editorial Calm” warmer must preserve its density, type logic, and boundaries instead of turning it into another direction. Defaults include an evidence label such as “9 of 12 references lean airy.” Raw token editing sits behind Advanced.

| Slider | Poles | Compiles to |
|---|---|---|
| Density | Compact ↔ Airy | spacing scale, line-height, padding, max-width, gaps |
| Temperature | Cool/technical ↔ Warm/human | hue bias, saturation, neutral tint |
| Contrast | Soft/muted ↔ Bold/dramatic | contrast ratios, weight range, shadows, borders |
| Shape | Sharp/geometric ↔ Rounded/soft | radius scale, controls, icon stroke |
| Motion | Calm/instant ↔ Expressive/springy | duration, easing, spring parameters, hover and press states |

## 10. Taste spec schema

The spec is the contract between Board, Taste Lab, preview, and export.

```json
{
  "version": "0.2",
  "project": "string",
  "intent": "A short statement of the desired emotional and strategic effect.",
  "references": [
    {
      "id": "ref_01",
      "url": "https://…",
      "reaction": "like | anti | mixed",
      "note": "love the type, reject the colour"
    }
  ],
  "directions": [
    {
      "id": "dir_01",
      "name": "Editorial Calm",
      "summary": "one sentence a human reads",
      "provenance": ["ref_03", "ref_07", "ref_11"],
      "boundaries": ["No glossy gradients", "No equal three-card feature rows"],
      "dimensions": {
        "density": { "value": 72, "evidence": "9 of 12 references lean airy" },
        "temperature": { "value": 38, "evidence": "…" },
        "contrast": { "value": 55, "evidence": "…" },
        "shape": { "value": 61, "evidence": "…" },
        "motion": { "value": 30, "evidence": "…" }
      },
      "principles": [
        {
          "id": "principle_01",
          "name": "Presence through restraint",
          "trigger": "How should hierarchy work?",
          "decision": "Use typography and spacing before colour or elevation.",
          "reason": "…",
          "evidence": ["ref_03", "calibration_01"],
          "tradeoff": "Less immediate scanability in dense views.",
          "confidence": "high"
        }
      ],
      "tokens": {
        "color": { "primary": "#…", "surface": "#…", "text": "#…", "accent": "#…" },
        "type": { "family": "…", "scaleRatio": 1.25, "weightRange": [400, 700], "tracking": "-0.01em" },
        "space": { "unit": 4, "scale": [4, 8, 12, 16, 24, 32, 48] },
        "radius": { "sm": 4, "md": 8, "lg": 16 },
        "motion": { "durationMs": 180, "easing": "cubic-bezier(0.2, 0, 0, 1)", "spring": { "stiffness": 300, "damping": 30 } },
        "elevation": { "card": "0 1px 3px rgba(0,0,0,.08)" }
      }
    }
  ],
  "calibrations": [
    {
      "id": "calibration_01",
      "directionId": "dir_01",
      "tension": "Hierarchy",
      "optionA": "Accent-colour CTA",
      "optionB": "Typography-led emphasis",
      "choice": "A | B | both | neither | skip",
      "rationale": "feels calm without trying to look expensive",
      "derivedPrincipleId": "principle_01",
      "comparisonStatus": "answered | skipped | revisited"
    }
  ],
  "preferenceLadder": {
    "tiers": [
      { "name": "strong_match", "directionIds": ["dir_01"], "confidence": "medium" },
      { "name": "worth_revisiting", "directionIds": ["dir_02"] },
      { "name": "less_aligned_so_far", "directionIds": ["dir_03"] }
    ],
    "shortlist": ["dir_01", "dir_02"],
    "manualOrder": []
  },
  "active": { "directionId": "dir_01", "overrides": { "density": 80 } }
}
```

Slider changes write to `active.overrides`, recompile the token bundle, and update CSS variables instantly. Calibration choices update a local decision record and the corresponding active principle. Neither requires a model call.

## 11. Architecture

- **Next.js + Vercel** using the existing pipeline from melissatang.com.
- **One API route:** `/api/distill` receives image URLs or base64 images, reactions, and notes. A vision-capable OpenAI model with structured output returns the taste spec. The deployed model is configurable; use the Build Week model access available to the project.
- **Preview:** one template dashboard styled entirely through CSS variables derived from `tokens`. Calibration variants are deterministic theme states, so interaction stays instant.
- **Exports:** deterministic serializers write `tokens.json`, `DESIGN.md`, a `mood.md`-compatible perceptual section, and an `AGENTS.md` block. The export includes principles, boundaries, trade-offs, and implementation checks alongside tokens.
- **MCP:** `@gloss` returns the active spec and brief on request. The first version is read-only context retrieval, not a design-editing agent.
- **Build meta-requirement:** build with Codex and record sessions. The video frame: “I used Codex to build a tool that teaches Codex project-specific taste.”

### Agent instruction shape

The exported `AGENTS.md` block should use concrete, situational rules:

```md
## Gloss design direction

- Preserve the principle “Presence through restraint”: establish hierarchy with
  spacing and type before adding coloured buttons, shadows, or containers.
- Reserve the accent colour for status and focused interaction, not every CTA.
- Keep editorial shell views airy. For bulk-review flows, increase density while
  retaining the warm neutral ground and low-elevation grouping.
- Do not add glossy gradients, equal three-card feature rows, or decorative
  animation unless a screen-specific reason is stated.
- Include loading, empty, error, focus, hover, and pressed states. Prefer
  transform and opacity for motion.
```

## 12. Scope

**In:** URL/file board; like, anti-like, and mixed reactions; optional notes; Distill into three named directions; one dashboard template; five sliders; Design Map; 3–4 candidate Taste DNA principles per direction; provenance chips; three deterministic A/B calibration prompts for the active direction; A/B/both/neither/skip responses; an expandable tiered Preference Ladder and two-item shortlist; decision memory; re-Distill after material board changes; four exports; Codex round-trip demo.

**Out, described as roadmap:** taste that spans projects; ingesting a user’s own app; open-ended semantic iteration; model-generated variants during calibration; multiple templates; team sharing; learning from history across teams; automated visual regression or fidelity scoring.

## 13. Success criteria

| Criterion | Requirement |
|---|---|
| Technical implementation | The round trip works: board → spec → one calibration choice → `AGENTS.md` / MCP context → Codex generates an unseen screen that follows the active direction. README enables reproduction in under five minutes. |
| Design and UX | Gloss itself demonstrates its thesis: clear evidence labels, named directions, visible trade-offs, instant preview, low-friction calibration, and a polished export moment. |
| Potential impact | The narrative is a portable per-project taste layer. It gives non-designers a way to make good visual judgment repeatable and gives designers a way to preserve intent through agent workflows. |
| Quality of idea | The novelty claim is specific: existing tools produce themes, briefs, or static rules; Gloss turns curation into an inspectable and correctable decision memory that teaches an agent. |

## 14. Demo video (≤3 min)

1. **0:00–0:20: Problem.** Show three AI-generated apps with the same visual defaults. “You can see the difference, but your coding agent cannot.”
2. **0:20–0:45: Curate.** Paste references, mark one anti-like, add a small note, and Distill.
3. **0:45–1:15: Taste Lab.** Three named directions arrive. Select one, inspect provenance and a principle with its trade-off.
4. **1:15–1:40: Calibrate.** Show a controlled A/B choice on the same dashboard. Select one and optionally explain why. The Taste DNA card updates.
5. **1:40–2:00: Preference Ladder and correction loop.** Expand the runner-up direction, show why it ranks closely, then compare it again or pin it to the shortlist. Anti-like a reference or change a response. The direction visibly shifts and the evidence trail remains legible.
6. **2:00–2:35: Commit and payoff.** Export `AGENTS.md`, ask Codex for a brand-new screen, and show the result carrying the chosen direction.
7. **2:35–3:00: Meta and roadmap.** “Built with Codex, teaching Codex.” End with the tagline and the portable-taste roadmap.

## 15. Build plan

| Day | Deliverable |
|---|---|
| Mon 13 | Register, request model access, feasibility spike: 10 images → three directions → candidate principles. Iterate prompt before the UI exists. |
| Tue 14 | Lock spec schema and scaffold app. Render the dashboard from a hardcoded direction. |
| Wed 15 | Build Board and wire `/api/distill` end to end. |
| Thu 16 | Add direction switcher, sliders, provenance, and Design Map / Taste DNA cards. |
| Fri 17 | Add three deterministic A/B calibration prompts, tiered Preference Ladder, decision-memory update, exports, MCP wrapper, and Codex round-trip test. |
| Sat 18 | Polish day. Gloss’s interface is evidence for the product’s claim. |
| Sun 19 | Write and record video; complete README and judge test instructions. |
| Mon 20 | Edit video, write Devpost description, and submit with a buffer. |
| Tue 21 | Buffer only. |

## 16. Risks and mitigations

1. **Generic Distill output.** Directions can sound interchangeable or invent reasons not supported by the board. Mitigation: day-one spike; require provenance and trade-off fields; reject principles without evidence; seed with two hand-labeled boards.
2. **Calibration becomes a preference quiz.** A/B prompts may test too many variables or offer decorative choices. Mitigation: each pair has one named tension, identical content, and one visual difference that the user can understand in seconds. Use both, neither, and skip rather than forcing an artificial vote.
3. **The ranking feels arbitrary or final.** A user may interpret a losing option as rejected. Mitigation: use tiers rather than precise scores, preserve every explored direction, show the evidence behind a rank, and support revisit, shortlist, and manual override.
4. **Conflicting user signals.** Curation, sliders, and choices can disagree. Mitigation: retain the conflict in decision memory, distinguish shell from task surface when appropriate, and let confirmed user choices outrank inferred output.
5. **Scope creep.** A board, a component library, and an autonomous design agent are separate products. Mitigation: one template, three prompts, deterministic variants, and a read-only MCP endpoint.
6. **Agent adherence.** Codex may apply tokens but omit the reasoning. Mitigation: export concrete imperative rules that cite boundaries and trade-offs; test the unseen-screen round trip early; use MCP retrieval in the demo if file-only context is weak.
7. **Video slippage.** The video is a judged artifact. Mitigation: script and record by day six; cut roadmap features before cutting video time.

## 17. Source notes

This PRD adapts the following sources. Their roles are stated above; Gloss is not presented as a clone of any one project.

1. Sen Lin, [taste-skill](https://github.com/senlindesign/taste-skill): URL-to-Design-Map/Taste-DNA workflow; measurement, evidence, trade-offs, and machine-readable export.
2. MC Dean / Owl-Listener, [mood-protocol](https://github.com/Owl-Listener/mood-protocol): `mood.md` as a perceptual context layer; moodboard inputs, anti-references, and agent-readable aesthetic intent.
3. Leonxlnx, [taste-skill](https://github.com/Leonxlnx/taste-skill): implementation-oriented design dials and anti-generic frontend guardrails.
4. User-supplied project brief: current competitor framing, Build Week timing, judge criteria, and original product scope.

The key product claim is an inference from these sources: curation plus a static brief is insufficient for most non-designers. A small, controlled correction loop can turn visual reactions into confirmed design principles and reusable agent context.
