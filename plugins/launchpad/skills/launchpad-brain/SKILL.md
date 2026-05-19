---
name: launchpad-brain
description: "Entry point for any new feature. Scans the project if needed, then guides the user through Q&A to define the feature brief (REFERENCE.md)."
---

# Brain

Entry point. Handles project discovery internally, then guides the user through defining their feature.

## Steps

### 1. Discover — run silently
Check if `.launchpad/PROJECT.md` exists.

If missing or older than 7 days — scan the project before asking anything:
- Create `.launchpad/` if it does not exist.
- Detect stack: `package.json` (Node.js/framework), `requirements.txt` or `pyproject.toml` (Python), `Cargo.toml` (Rust), `go.mod` (Go), `Gemfile` (Ruby), `Dockerfile` or `docker-compose.yml` (containerized).
- Map top-level directories (one sentence each). Skip: `node_modules`, `.git`, `.launchpad`.
- Identify patterns from 3–5 source files: naming style, folder structure, state management.
- List key files: entry points, config files, main modules.
- Fill `templates/PROJECT.md`, save to `.launchpad/PROJECT.md`.

If updated: tell the user in one line what was found.
Example: "Scanned the project — found a Next.js app with Tailwind. Let's define your feature."
If fresh: continue silently.

### 2. Ask which feature
Ask: "What feature do you want to work on? Give it a short name (e.g. login, search, dashboard)."

Wait for the answer. Use that as `[feature-name]`.

### 3. Check if feature already exists
- If `.launchpad/features/[feature-name]/REFERENCE.md` exists:
  - Show the current content.
  - Ask: "This feature already has a brief. Want to update any answers?"
  - Yes → go through only the questions to change, then rewrite REFERENCE.md.
  - No → skip to Orchestrator step.
- If missing: continue to step 4.

### 4. Create feature directory
Create `.launchpad/features/[feature-name]/` if it does not exist.
Initialize STATE.md by following `skills/launchpad-orchestrator/SKILL.md` → "Initializing STATE.md".

### 5. Ask questions — one per template section
Open `templates/REFERENCE.md`. Read every section heading.
For each section — ask the user about it, one at a time. Wait for the answer before moving to the next.
Phrase each question in plain, conversational language. Do not number them or reveal how many there are.

### 6. Write REFERENCE.md
Using `templates/REFERENCE.md` as structure, fill each section with the user's answers. Replace `{{feature-name}}`. Save to `.launchpad/features/[feature-name]/REFERENCE.md`.

### 7. Orchestrator — end
Follow On Skill End rules in `skills/launchpad-orchestrator/SKILL.md`. Mark `brain` complete in STATE.md.

### 8. Close
"Your feature brief is ready. Run `/launchpad-architect` when you want to design how it works."
