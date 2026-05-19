---
name: launchpad-brain
description: "Entry point. Scans project if needed, guides user through Q&A to define feature brief (REFERENCE.md)."
---

# Brain

Entry point. Handles discovery internally, then guides user through feature definition.

## Steps

### 1. Discover — silent
Check `.launchpad/PROJECT.md` exists.

Missing or older than 7 days — scan project silently:
- Create `.launchpad/` if missing.
- Detect stack: `package.json` (Node.js), `requirements.txt`/`pyproject.toml` (Python), `Cargo.toml` (Rust), `go.mod` (Go), `Gemfile` (Ruby), `Dockerfile`/`docker-compose.yml` (containerized).
- Map top-level dirs (one line each). Skip: `node_modules`, `.git`, `.launchpad`.
- Identify patterns from 3–5 source files: naming, folder structure, state management.
- List key files: entry points, config, main modules.
- Fill `templates/PROJECT.md`, save to `.launchpad/PROJECT.md`.

If updated: one line to user. Example: "Scanned — Next.js + Tailwind. Let's define your feature."
If fresh: continue silently.

### 2. Ask feature name
"What feature do you want to work on? Short name (e.g. login, search, dashboard)."

Wait. Use answer as `[feature-name]`.

### 3. Check existing
- `.launchpad/features/[feature-name]/REFERENCE.md` exists:
  - Show content. Ask: "Already have a brief. Update any answers?"
  - Yes → update changed questions only, rewrite REFERENCE.md.
  - No → skip to Orchestrator step.
- Missing → continue to step 4.

### 4. Create dir
Create `.launchpad/features/[feature-name]/` if missing.
Init STATE.md → follow `skills/launchpad-orchestrator/SKILL.md` → "Initializing STATE.md".

### 5. Ask questions
Open `templates/REFERENCE.md`. Read section headings.
One question per section. Wait for answer before next.
Plain conversational phrasing. No numbering. No count.

### 6. Write REFERENCE.md
Fill `templates/REFERENCE.md` with answers. Replace `{{feature-name}}`. Save to `.launchpad/features/[feature-name]/REFERENCE.md`.

### 7. Orchestrator — end
Follow On Skill End in `skills/launchpad-orchestrator/SKILL.md`. Mark `brain` complete in STATE.md.

### 8. Close
"Feature brief ready. Run `/launchpad-architect` to design it."
