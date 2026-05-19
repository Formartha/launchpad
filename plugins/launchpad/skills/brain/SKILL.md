---
name: brain
description: "Entry point for any new feature. Scans the project if needed, then guides the user through a short Q&A to define the feature brief (REFERENCE.md)."
---

# Brain

The entry point. Run this first. It handles project discovery internally, then guides the user through defining their feature.

---

## Steps

### 1. Discover — run internally, silently
Check if `.launchpad/PROJECT.md` exists.

If it does not exist, or is older than 7 days — scan the project now before asking the user anything:
- Create `.launchpad/` if it does not exist.
- Detect the tech stack by looking for: `package.json` (Node.js/framework), `requirements.txt` or `pyproject.toml` (Python), `Cargo.toml` (Rust), `go.mod` (Go), `Gemfile` (Ruby), `Dockerfile` or `docker-compose.yml` (containerized).
- Map top-level directories (one sentence each). Skip: `node_modules`, `.git`, `.launchpad`.
- Identify patterns from 3–5 source files: naming style, folder structure, state management.
- List key files: entry points, config files, main modules.
- Open `templates/PROJECT.md`, fill each section, save to `.launchpad/PROJECT.md`.

If PROJECT.md was just created or updated: tell the user in one line what was found before continuing.
Example: "Scanned the project — found a Next.js app with Tailwind. Let's define your feature."

If PROJECT.md already exists and is fresh: continue silently.

---

### 2. Ask which feature
Ask: "What feature do you want to work on? Give it a short name (e.g. login, search, dashboard)."

Wait for the answer. Use that as `[feature-name]` for the rest of this skill.

---

### 3. Check if feature already exists
- If `.launchpad/features/[feature-name]/REFERENCE.md` exists:
  - Show the current content.
  - Ask: "This feature already has a brief. Want to update any of these answers?"
  - If yes: go through only the questions the user wants to change, then rewrite REFERENCE.md.
  - If no: skip to Orchestrator step.
- If it does not exist: continue to step 4.

---

### 4. Create feature directory
Create `.launchpad/features/[feature-name]/` if it does not exist.

Initialize STATE.md by following the rules in `skills/orchestrator/SKILL.md` → "Initializing STATE.md".

---

### 5. Ask questions — one per template section
Open `templates/REFERENCE.md`. Read every section heading.

For each section — ask the user about it, one at a time. Wait for the answer before moving to the next.
Phrase each question in plain, conversational language based on the section heading.
Do not number the questions. Do not tell the user how many there are.

---

### 6. Write REFERENCE.md
Using `templates/REFERENCE.md` as the structure, fill in each section with the user's answers. Replace `{{feature-name}}` with the actual name. Save to `.launchpad/features/[feature-name]/REFERENCE.md`.

---

### 7. Orchestrator — end
Follow the On Skill End rules in `skills/orchestrator/SKILL.md`. Mark `brain` as completed in STATE.md.

---

### 8. Close
Tell the user: "Got it. Your feature brief is ready. Run `/architect` when you want to design how it works."
