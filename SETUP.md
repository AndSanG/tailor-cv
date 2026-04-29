# Adding tailor-cv to a project

## 1. Add the submodule

From your project root:

```bash
git submodule add git@github.com:AndSanG/tailor-cv.git .agents/skills/tailor-cv
git commit -m "add tailor-cv skill"
```

> If cloning a project that already has this submodule:
> ```bash
> git clone --recurse-submodules <your-repo-url>
> # or, if already cloned:
> git submodule update --init
> ```

## 2. Scaffold the project structure

Copy the template into your project root and fill in the placeholders:

```bash
cp -r .agents/skills/tailor-cv/template/. .
```

See `example/` for a fully filled-in reference.

## 3. Fill in the required files

| File | What to put in it |
|---|---|
| `source/identity/IDENTITY.md` | Name, role, handle, location, language |
| `source/identity/SOUL.md` | Voice, tone, expertise, boundaries |
| `source/identity/AGENTS.md` | CV tracks table — name, file path, use case |
| `source/memory/MEMORY.md` | Empty index to start; add entries as memories accumulate |

See `INSTALL.md` for the full file contract per file.

## 4. Add your CV files

Create one folder per track under `source/tracks/`, matching the paths in your `AGENTS.md` tracks table:

```
source/tracks/
  ios/
    Candidate_iCV.md
  web-hybrid/
    Candidate_rrnCV.md
```

## 5. Register the skill in Claude Code

Add to `.claude/settings.json` in your project:

```json
{
  "skills": [".agents/skills/tailor-cv/SKILL.md"]
}
```

Or add to `~/.claude/settings.json` to use across all projects.

## 6. Verify

Before the first run, confirm:

- [ ] `source/identity/AGENTS.md` has a `## CV Tracks` table
- [ ] `source/identity/SOUL.md` has tone and boundary rules
- [ ] `source/identity/IDENTITY.md` has name and language
- [ ] `source/memory/MEMORY.md` exists
- [ ] All CV files listed in the tracks table exist at their paths

Then run `/tailor-cv` in Claude Code.

## Keeping the skill up to date

```bash
# Pull latest skill updates
git submodule update --remote .agents/skills/tailor-cv
git commit -m "update tailor-cv"
```
