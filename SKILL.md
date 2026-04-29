---
name: tailor-cv
description: >
  Optimizes a candidate's CV for a specific job description using ATS keyword
  matching, honest experience framing, and voice guardrails from SOUL.md.
  Reads AGENTS.md at session start to discover available CV tracks and file paths.
  Use when the user provides a job posting and wants to tailor a CV track.
license: MIT
compatibility: |
  Enforced layout (paths are fixed, not configurable):
    source/identity/SOUL.md       — voice, tone, and content boundaries (required)
    source/identity/IDENTITY.md   — candidate name, role, handle, location (required)
    source/identity/AGENTS.md     — CV tracks table and session contract (required)
    source/memory/MEMORY.md       — memory index (required)
    source/memory/*.md            — individual memory files indexed by MEMORY.md
    source/soft-skills/           — cross-track soft skills (optional, skip if absent)
    source/tracks/<track>/<cv>.md — CV files; paths defined in AGENTS.md CV Tracks table
  See INSTALL.md for setup instructions.
metadata:
  author: andsangue
  version: "3.0"
---

## Context Load

Before doing any other work, read these files silently:

- `source/identity/AGENTS.md` — authoritative list of CV tracks and file paths; derive all track options from its CV Tracks table
- `source/identity/SOUL.md`
- `source/identity/IDENTITY.md`
- `source/memory/MEMORY.md`
- `source/memory/*` (all files indexed in MEMORY.md)


## Workflow

1. **Ask for inputs** — Ask the user two things in a single message:
   - Which CV track to modify: present the tracks listed in the AGENTS.md CV Tracks table (track name, file path, and use case). Let the user pick.
   - The job description (ask them to paste it)
   Wait for the user's reply before proceeding.
2. Read the selected CV and `source/soft-skills/soft_skills.md` (skip silently if the file does not exist)
3. Understand the job (parse job description for keywords, requirements, nice-to-haves)
4. Map experience to requirements (what matches directly, what needs expansion, what's missing)
5. Optimize with guardrails (expand real experience, match keywords, reframe soft skills)
6. Check boundaries (what NOT to change, what NOT to fabricate)
7. Validate (interview defensibility test on every modified claim)
8. Proofread (spelling, consistency, metric accuracy, no overselling)
9. Deliver output (updated CV + summary of changes + gap flags)


## Source Files

- **source/identity/**: Authentic voice, values, boundaries. Always follow SOUL.md tone — never adopt the job description's corporate language.
- **source/**: Comprehensive experience data, legacy CVs, and reference documents. Single source of truth for what the candidate has actually done.
- **source/soft-skills/soft_skills.md**: Cross-track soft skills and cross-cutting strengths. Read when the JD emphasizes collaboration, team dynamics, UI/UX partnership, or leadership signals.


## ATS Optimization

Using the base CV, optimize for a job aiming for a high ATS score — keeping the facts and surfacing what is present in source but not explicitly stated in the CV.

### Use Cases

- **Expanding brief mentions:** CV has brief or missing information due to length constraints, but the JD requires detail. Extend using source/. Example: JD has a 'Nice to have' for AI — source explains academic experience with deep learning and language models.
- **Surfacing secondary technologies:** CV is optimized for one stack, but source contains other relevant technologies. Surface when relevant as 'nice to have.'
- **Keyword matching:** CV uses abbreviated or internal terms — JD uses full names or alternate terminology. Swap to match the JD's terminology.
- **Soft skill reframing:** Reframe to match the JD's language while keeping authentic meaning. Example: "Conveying complex issues at different abstraction levels" → "Communicating complex technical concepts to diverse audiences, from engineers to C-level executives."

### Guardrails

- Always label context when expanding skills: production experience vs. academic/research. Never present academic work as production skills.
- Match the JD's title ONLY if experience supports it. Never inflate to match a posting.
- Do NOT modify or remove candidate differentiators called out in SOUL.md or IDENTITY.md — they are key signals for the roles the candidate is targeting.
- **Missing experience:** If the JD requires something not in source, do not fabricate it. Skip silently, strengthen adjacent skills, and flag critical gaps to the user.


## Guardrails & Boundaries

"Help the user be honest about their experience, position them for roles they can actually get and succeed in, and show them the path to their aspirational level."

### The Core Method

- Discover everything (CVs, personality tests, detailed Q&A in source/)
- Assess honestly (real level vs. target level)
- Optimize storytelling using SOUL.md style — not the JD's style
- Identify overselling (red flags, interview tests)
- Rewrite with honesty
- Validate (defensibility check, personality data)
- Keep ideas simple. No over-explanation. No jargon. No excessive adjectives.
- Do not make structural changes to the CV only to optimize for ATS.

### The Core Warning

"Better to target one level lower and succeed than target too high and fail. Real achievements are usually impressive enough."

### Do NOT

- Add technologies not used in production (move to Academic/Research if relevant)
- Change "coordinated" to "managed" or "led" to inflate leadership scope
- Add metrics that weren't measured
- Remove the candidate's positioning statement (the opening 'Seeking...' line or equivalent opener defined in the CV)
- Claim formal mentoring, hiring, or people management unless sourced
- Fabricate experience to fill gaps
- Adopt the JD's corporate tone over the candidate's authentic voice


## File Management

- Edit the CV file for the track the user selected in step 1. File paths come from the AGENTS.md CV Tracks table — do not assume any path.
- Do not create per-company tailored files unless explicitly requested. Changes are tracked via git.


## Style & Formatting

### Markdown Rules
- `#` for Name, `##` for Major Sections, `###` for Companies/Roles
- `-` for bullet points
- `**` for key metrics, technologies, and achievements
- Ensure all links (GitHub, LinkedIn, Email) are functional

### Content Goals
- Prioritize tangible results (e.g., "99.5% uptime", "reduced deployment time by 60%")
- Ensure domain-relevant technical keywords from the candidate's expertise (per SOUL.md) are surfaced when the JD calls for them


## Proofread

- Spelling/Grammar (language per IDENTITY.md)
- Consistency in dates and formatting
- Seniority of language used
- Verify all metrics match source documents
- No claim contradicts source/
- Academic experience remains labeled as academic
- The candidate's positioning statement still fits the target job


## Validation

After optimization, review each modified bullet. For every changed claim: "Could the candidate discuss this for 10 minutes in an interview?" If not, revert.


## Output

1. Edit the CV in place (per File Management)
2. Write the report to **`source/tracks/<track>/output.md`** (overwrite on every run). Summarize in chat.
3. Save the job offer to **`source/tracks/<track>/<Company>_<Role>.md`** (verbatim, no edits).

Report must include:
1. **Target Role** — Company, role title, work model
2. **Requirement Mapping** — Table of every JD requirement mapped to its CV status
3. **Changes Made** — Each change with exact text and reason
4. **Gap Flags** — Honest assessment of uncovered requirements with risk rating
5. **Validation** — Confirm all modified claims pass the 10-minute defensibility test

Format rules for `source/<track>/output.md`:
- Header: `# tailorCV Output`
- Second line: `> This file is overwritten on each /tailor-cv run.`
- `##` for each section
- Tables for Requirement Mapping and Gap Flags
- SOUL.md tone — direct, no fluff
