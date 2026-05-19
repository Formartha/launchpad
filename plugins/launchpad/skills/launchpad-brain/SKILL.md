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

After scanning (whether new or fresh): follow On Skill End rules in `skills/launchpad-state/SKILL.md` to mark `discover` complete in STATE.md. Do this before asking the feature name — discover must be recorded first.

### 2. Ask which feature
Ask: "What feature do you want to work on? Give it a short name (e.g. login, search, dashboard)."

Wait for the answer. Follow the elicitation confirm loop in `skills/launchpad-elicit/SKILL.md`:
- Reflect: "Got it — '[feature-name]'. Does that sound right, or want a different name?"
- Wait for confirmation before doing anything else.

Use the confirmed name as `[feature-name]`.

### 3. Check if feature already exists
- If `.launchpad/features/[feature-name]/REFERENCE.md` exists:
  - Show the current content.
  - Ask: "This feature already has a brief. Want to update any answers?"
  - Yes → go through only the questions to change, then rewrite REFERENCE.md.
  - No → skip to State step.
- If missing: continue to step 4.

### 4. Create feature directory
Ask: "Ready to start building the brief for '[feature-name]'? I'll create a folder and we'll go through the brief."

- Yes → create `.launchpad/features/[feature-name]/`, initialize STATE.md following `skills/launchpad-state/SKILL.md` → "Initializing STATE.md".
- No → "No problem. Come back when you're ready." Stop.

### 5. Elicitation mode
Ask: "How would you like to work through this? I can brainstorm it with you — thinking out loud together, one question at a time — or you can just describe the feature however you like and I'll take it from there."

- Brainstorm / guided → continue to step 6a.
- Free-form / describe it myself → continue to step 6b.

### 6a. Guided Q&A
Open `templates/REFERENCE.md`. Read every section heading.

For each section — use the heading as the topic, ask it conversationally. Follow the elicitation protocol in `skills/launchpad-elicit/SKILL.md`.
Do not add constraints, hints, or format guidance. User writes freely. Do not number questions or reveal how many there are.

### 6b. Free-form
Ask: "Tell me about '[feature-name]' in your own words — whatever comes to mind."
Wait for the response. Accept everything. Do not redirect or prompt for more structure.
Then map what was said onto the sections in `templates/REFERENCE.md` as best you can. Leave sections blank if not covered.

### 6. External sources
Ask: "Before we wrap up — is there anything else you'd like to add? A website, a screenshot, a document, a design, anything at all."

Follow the external source rules in `skills/launchpad-elicit/SKILL.md` for anything shared.

### 7. Write REFERENCE.md
Using `templates/REFERENCE.md` as structure, fill each section with the user's answers and any external context gathered. Replace `{{feature-name}}`. Save to `.launchpad/features/[feature-name]/REFERENCE.md`.

### 8. State — end
Follow On Skill End rules in `skills/launchpad-state/SKILL.md`. Mark `brain` complete in STATE.md.

### 9. Close
"Your feature brief is ready. Want me to start designing the architecture now, or would you prefer to review it first?"

- Yes / now → continue directly into the `/launchpad-architect` skill steps without waiting for a command.
- No / later → "Take your time. Run `/launchpad-architect` when you're ready."
