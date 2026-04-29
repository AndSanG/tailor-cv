# AGENTS.md — Operational Behavior

## CV Tracks

Two CV variants exist. Always confirm which track applies before editing or tailoring:

| Track | File | Use when |
|---|---|---|
| Apple Platforms | `source/tracks/apple-platforms/John_Appleseed_AppleCV.md` | iOS/macOS/SwiftUI-first roles; highlights native platform depth |
| Developer Tooling | `source/tracks/dev-tools/John_Appleseed_ToolingCV.md` | Roles focused on SDKs, frameworks, Xcode toolchain, or demo engineering |

Pre-2018 content (mid-level Contacts framework work, Core Data migrations) is the same across both tracks.

---

## Session Start

On every new session, an agent working with John should:
1. Confirm the task and surface any ambiguities as a concise list (not as open-ended questions).
2. If context files (CV, job description, previous output) are provided, read them before generating anything.
3. State assumptions made when inputs are ambiguous. Deliver a concrete draft; iterate from there.

## Memory Model

- Project memory lives in `source/memory/`. Read `MEMORY.md` there at session start — it indexes all memory files.
- **Write new memories to `source/memory/` only** — not to `~/.claude/`. Follow the same frontmatter format (name, description, type) and add a pointer to `MEMORY.md`.
- Never infer facts about John from prior outputs unless confirmed in the current session or in a `source/memory/` file.

## Source Files

Read on demand — load only when the task touches the relevant domain.

| Path | Read when |
|---|---|
| `source/soft-skills/soft_skills.md` | JD signals collaboration, accessibility advocacy, cross-team platform work, or demo engineering |
| `source/continuous-education/WWDC/` | JD mentions specific Apple frameworks, APIs, or recent platform capabilities |

## Output Contract

Every output must:
- Be consistent with SOUL.md (tone, representation rules, content boundaries).
- Avoid inflation. If a claim cannot be traced to a concrete artifact, remove it.
- Add a "Next steps" or "Acceptance criteria" section only when the task explicitly requires follow-up action.

## Preferred Workflow

1. Receive task + context files.
2. Clarify blockers (max 3 questions, only if truly ambiguous).
3. Deliver a concrete draft.
4. Accept targeted feedback and iterate.
5. Finalize with a changelog entry summarizing changes made.

## Anti-patterns to Reject

- Generating content without provided context about the target role or company.
- Adding metrics not grounded in evidence from context files.
- Softening honest gaps rather than framing them accurately.
- Using any language SOUL.md explicitly prohibits — especially Apple marketing speak.
