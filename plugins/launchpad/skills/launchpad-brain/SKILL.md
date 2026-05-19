---
name: launchpad-brain
description: "Entry point for any new feature. Scans the project if needed, then guides the user through defining the feature brief (REFERENCE.md)."
---

# Brain

Entry point. Handles project discovery internally, then guides the user through defining their feature.

## Steps

### 0. Intro
Before doing anything else, tell the user what's about to happen in plain language:

"Here's what we'll do together:
1. I'll scan your project to understand what we're working with.
2. We'll give the feature a name.
3. You'll choose how to build the brief — guided brainstorm or describe it yourself.
4. We'll capture any extra context you want to add (links, images, docs).
5. I'll write the feature brief so we can move to design.

Ready?"

Use the ask tool to present this as a yes/no choice. Only proceed when the user confirms.

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
Example: "Scanned — Next.js + Tailwind. Let's name the feature."
If fresh: continue silently.

After scanning: follow On Skill End rules in `skills/launchpad-state/SKILL.md` to mark `discover` complete in STATE.md.

### 2. Ask which feature
Ask: "What feature do you want to work on? Give it a short name (e.g. login, search, dashboard)."

Wait for the answer. Use the ask tool to confirm:
- Reflect: "Got it — '[feature-name]'. Does that sound right?"
- Present as yes / use a different name.
- Wait for confirmation before doing anything else.

Use the confirmed name as `[feature-name]`.

### 3. Check if feature already exists
- If `.launchpad/features/[feature-name]/REFERENCE.md` exists:
  - Show the current content.
  - Use the ask tool: "This feature already has a brief. What would you like to do?" → Update answers / Keep as is.
  - Update → go through only the changed questions, rewrite REFERENCE.md.
  - Keep → skip to State step.
- If missing: continue to step 4.

### 4. Create feature directory
Use the ask tool: "Ready to start the brief for '[feature-name]'?" → Yes / Not yet.

- Yes → create `.launchpad/features/[feature-name]/`, initialize STATE.md following `skills/launchpad-state/SKILL.md` → "Initializing STATE.md".
- Not yet → "No problem. Come back when you're ready." Stop.

### 5. Elicitation mode
Use the ask tool to present the choice:

"How would you like to build the brief?"
→ Brainstorm with me (guided, one question at a time)
→ Describe it yourself (free-form, I'll structure it)

- Brainstorm → continue to step 6a.
- Describe it yourself → continue to step 6b.

### 6a. Guided Q&A
Open `templates/REFERENCE.md`. Read every section heading.

For each section:
- Look up the assigned modality in `skills/launchpad-elicit/SKILL.md` → "Modality Assignment per REFERENCE.md Section".
- Apply that modality. Follow the core protocol (reflect, confirm, adjust) throughout.
- Do not add constraints or format hints. User writes freely.
- Do not number questions or reveal how many there are.

### 6b. Free-form
Ask: "Tell me about '[feature-name]' in your own words — whatever comes to mind."
Wait. Accept everything. Map what was said onto sections in `templates/REFERENCE.md`. Leave blanks where not covered.

### 7. External sources
Use the ask tool: "Anything else to add before I write the brief?" → Yes, I have something / No, we're good.

If yes: "Share it — a URL, screenshot, document, design, anything." Follow external source rules in `skills/launchpad-elicit/SKILL.md`.

### 8. Write REFERENCE.md
Fill `templates/REFERENCE.md` with all gathered content. Replace `{{feature-name}}`. Save to `.launchpad/features/[feature-name]/REFERENCE.md`.

### 9. State — end
Follow On Skill End rules in `skills/launchpad-state/SKILL.md`. Mark `brain` complete in STATE.md.

### 10. Close
Use the ask tool: "Feature brief is ready. What's next?"
→ Start designing now (continue into `/launchpad-architect`)
→ Review the brief first (stop here)
