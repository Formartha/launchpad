---
name: launchpad-brain
description: "Entry point for any new feature. Scans the project if needed, then guides the user through defining the feature brief (REFERENCE.md)."
allowed-tools:
  - Bash
  - Read
  - Write
---

# Brain

Entry point. Handles project discovery internally, then guides the user through defining their feature.

## Steps

### 0. Intro
Tell the user what's about to happen:

"Here's what we'll do together:
1. I'll scan your project to understand what we're working with.
2. We'll give the feature a name.
3. You'll choose how to build the brief — guided Q&A or team brainstorm.
4. We'll capture any extra context you want to add (links, images, docs).
5. I'll write the feature brief so we can move to design.

Ready?"

Use the ask tool — yes/no. Only proceed when confirmed.

### 1. Discover — run silently
Check if `.launchpad/PROJECT.md` exists.

If missing or older than 7 days — scan the project:
- Create `.launchpad/` if it does not exist.
- Copy all files from the plugin's `templates/` directory into `.launchpad/templates/` if not already there.
- Detect stack: `package.json` (Node.js/framework), `requirements.txt` or `pyproject.toml` (Python), `Cargo.toml` (Rust), `go.mod` (Go), `Gemfile` (Ruby), `Dockerfile` or `docker-compose.yml` (containerized).
- Map top-level directories (one sentence each). Skip: `node_modules`, `.git`, `.launchpad`.
- Identify patterns from 3–5 source files: naming style, folder structure, state management.
- List key files: entry points, config files, main modules.
- Fill `.launchpad/templates/PROJECT.md`, save to `.launchpad/PROJECT.md`.

If updated: tell the user one line. Example: "Scanned — Next.js + Tailwind. Let's name the feature."
If fresh: continue silently.

### 2. Ask which feature
Ask: "What feature do you want to work on? Give it a short name (e.g. login, search, dashboard)."

Use the ask tool to confirm:
- Reflect: "Got it — '[feature-name]'. Does that sound right?"
- Present as: Yes / Use a different name.
- Wait for confirmation before proceeding.

Use the confirmed name as `[feature-name]`.

### 3. Elicitation — offer immediately after name confirmed
Use the ask tool right after the name is confirmed:

"How would you like to build the brief for '[feature-name]'?"
→ Q&A — I'll ask you questions, you answer
→ Team brainstorm — a virtual team thinks it through, you watch and jump in anytime

Store the chosen mode. Continue to step 4.

### 4. Check if feature already exists
- If `.launchpad/features/[feature-name]/REFERENCE.md` exists:
  - Show the current content.
  - Use the ask tool: "This feature already has a brief. What would you like to do?" → Update answers / Keep as is.
  - Update → run the chosen elicitation mode on only the sections to change, rewrite REFERENCE.md.
  - Keep → skip to step 9.
- If missing: continue to step 5.

### 5. Create feature directory
Create `.launchpad/features/[feature-name]/`.

Initialize STATE.md:
- Copy `.launchpad/templates/STATE.md` exactly — do not change structure.
- Replace `{{feature-name}}` with the actual name.
- All rows: `not started`, date `—`, summary `—`.
- Save to `.launchpad/features/[feature-name]/STATE.md`.

Mark `discover` complete in STATE.md:
- Update `## Current Phase` → `discover`.
- Update discover row: Status → `completed`, Date → today `YYYY-MM-DD`, Summary → one sentence of what was found.

### 6a. Free-flow Q&A (if chosen in step 3)
Read `.launchpad/templates/REFERENCE.md`. Use each section heading as a question topic.

For each section — apply the modality assigned in the launchpad-elicit skill (Structure 1: Free-flow → Modalities table). Follow core protocol: ask → reflect → confirm → adjust.
Do not add constraints or format hints. User writes freely. Do not number questions or reveal how many there are.

### 6b. Group — Persona Team Brainstorm (if chosen in step 3)
Follow Structure 2: Group defined in the launchpad-elicit skill exactly.
Run the team discussion. Pause after each round. Map output to `.launchpad/templates/REFERENCE.md` sections.

### 7. External sources
Use the ask tool: "Anything else to add before I write the brief?" → Yes, I have something / No, we're good.

If yes: "Share it — a URL, screenshot, document, design, anything."
Read or view what they share. Extract relevant context. Follow external source rules from the launchpad-elicit skill.

### 8. Write REFERENCE.md
Using `.launchpad/templates/REFERENCE.md` as structure, fill each section with gathered content. Replace `{{feature-name}}`. Save to `.launchpad/features/[feature-name]/REFERENCE.md`.

### 9. State — mark brain complete
In `.launchpad/features/[feature-name]/STATE.md`:
- Update `## Current Phase` → `brain`.
- Update brain row: Status → `completed`, Date → today `YYYY-MM-DD`, Summary → one sentence of what was defined.

### 10. Close
Use the ask tool: "Feature brief is ready. What's next?"
→ Start designing now (continue into `/launchpad-architect`)
→ Review the brief first (stop here)
