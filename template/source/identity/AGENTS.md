# AGENTS.md — Operational Behavior

## CV Tracks

<!-- Define one row per CV variant. The tailor-cv skill reads this table to present options and resolve file paths. -->

| Track | File | Use when |
|---|---|---|
| <!-- Track A name --> | `source/tracks/track-a/candidate_trackA_CV.md` | <!-- Roles or conditions for this track --> |
| <!-- Track B name --> | `source/tracks/track-b/candidate_trackB_CV.md` | <!-- Roles or conditions for this track --> |

<!-- Pre-YYYY content shared across tracks: add a note here if applicable -->

---

## Session Start

On every new session, an agent working with this candidate should:
1. Confirm the task and surface any ambiguities as a concise list (not as open-ended questions).
2. If context files (CV, job description, previous output) are provided, read them before generating anything.
3. State assumptions made when inputs are ambiguous. Deliver a concrete draft; iterate from there.

## Memory Model

- Project memory lives in `source/memory/`. Read `MEMORY.md` there at session start — it indexes all memory files.
- **Write new memories to `source/memory/` only** — not to `~/.claude/`. Follow the same frontmatter format (name, description, type) and add a pointer to `MEMORY.md`.
- Never infer facts about the candidate from prior outputs unless confirmed in the current session or in a `source/memory/` file.

## Source Files

Read on demand — load only when the task touches the relevant domain.

| Path | Read when |
|---|---|
| `source/soft-skills/soft_skills.md` | JD signals collaboration, leadership, stakeholder framing, or UI/UX partnership |
| <!-- Add other source folders and their read conditions here --> | <!-- Condition --> |

## Output Contract

Every output must:
- Be consistent with SOUL.md (tone, representation rules, content boundaries).
- Avoid inflation. If a claim cannot be traced to real evidence, remove it.
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
- Using any language SOUL.md explicitly prohibits.
