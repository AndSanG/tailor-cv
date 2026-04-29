# tailor-cv

A Claude Code skill that optimizes a candidate's CV for a specific job description using ATS keyword matching, honest experience framing, and voice guardrails defined in a `SOUL.md` file.

## What it does

1. Reads your project's identity and memory files at session start
2. Asks which CV track to tailor and prompts for the job description
3. Maps JD requirements to your real experience
4. Optimizes for ATS keywords without fabricating or inflating claims
5. Validates every changed bullet passes a 10-minute interview defensibility test
6. Delivers the edited CV, a requirement mapping table, and gap flags

## Install

```bash
git submodule add git@github.com:AndSanG/tailor-cv.git .agents/skills/tailor-cv
git commit -m "add tailor-cv skill"
```

Scaffold the required project structure from the included template:

```bash
cp -r .agents/skills/tailor-cv/template/. .
```

Register in `.claude/settings.json`:

```json
{
  "skills": [".agents/skills/tailor-cv/SKILL.md"]
}
```

Full setup instructions → [`INSTALL.md`](INSTALL.md)

## Required project structure

```
source/
  identity/
    SOUL.md        ← voice, tone, content boundaries
    IDENTITY.md    ← name, role, language
    AGENTS.md      ← CV tracks table (skill entry point)
  memory/
    MEMORY.md      ← memory index
  soft-skills/     ← optional
  tracks/
    <track>/
      <cv>.md      ← CV file, path defined in AGENTS.md
```

## Reference

| File | Purpose |
|---|---|
| [`SKILL.md`](SKILL.md) | Skill definition loaded by Claude Code |
| [`INSTALL.md`](INSTALL.md) | File contracts and verification checklist |
| [`template/`](template/) | Blank project scaffold |
| [`example/`](example/) | Filled-in reference (John Appleseed) |

## Usage

```
/tailor-cv
```

## Keeping up to date

```bash
git submodule update --remote .agents/skills/tailor-cv
git commit -m "update tailor-cv"
```
