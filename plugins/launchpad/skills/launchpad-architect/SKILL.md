---
name: launchpad-architect
description: "Designs the technical approach for a feature. Reads the feature brief, elicits technical constraints, proposes an implementation plan, writes FEATURE.md."
when_to_use: "Use after /launchpad-brain has written REFERENCE.md and the user is ready to decide how to build the feature."
allowed-tools:
  - Read
  - Write
---

# Architect

Technical focus only. Read the brief, understand constraints, propose a concrete implementation plan. Not a product conversation — this is about how to build it.

## Steps

### 1. Ask which feature
Ask: "Which feature are we designing?" Wait for the answer. Use that as `[feature-name]`.

### 2. State — start
Read `.launchpad/features/[feature-name]/STATE.md`. Verify `brain` phase is complete.
If not: stop. Tell the user to run `/launchpad-brain` first.

### 3. Read context silently
- `.launchpad/PROJECT.md`
- `.launchpad/features/[feature-name]/REFERENCE.md`

### 4. Elicitation mode
Use the ask tool:

"How would you like to work through the architecture for '[feature-name]'?"
→ Quick — I'll propose an approach, you confirm or adjust
→ Options — I'll show 2–3 approaches with trade-offs, you pick one
→ Q&A — I'll ask a few technical questions first, then propose

- Quick → step 5a
- Options → step 5b
- Q&A → step 5c

### 5a. Quick
Propose one concrete approach in 3–5 sentences. Cover: overall approach, files to create/modify, key dependencies.
Reflect, confirm, adjust until agreed. Then → step 6.

### 5b. Options
Present 2–3 distinct architectural approaches. For each:
- Name it (one word or short phrase)
- Describe it in 2 sentences
- One trade-off (what you gain, what you give up)

Use the ask tool: "Which direction fits best?"
User picks → confirm → adjust if needed → step 6.

### 5c. Technical Q&A
Ask targeted technical questions one at a time:
- Any constraints on stack, libraries, or file structure?
- Performance or scale requirements?
- Does anything in the existing codebase need to be preserved or avoided?
- Any hard deadlines or complexity limits?

After each answer: reflect, confirm. Once all answered → propose one approach → confirm → step 6.

### 6. Write FEATURE.md
Using `.launchpad/templates/FEATURE.md` as structure, fill in:
- **Approach**: the agreed paragraph
- **Flow**: plain-text arrow diagram, user perspective. Use `→ ↓ ↘ ↙` and short labels. No jargon — a non-developer must follow it. Show branching paths (e.g. success vs. error).
- **Files**: each file to create or modify, one per line, with a short note
- **Steps**: numbered implementation steps, concrete and specific
- **Test Scenarios**: one line per scenario that verifies the feature works

Replace `{{feature-name}}`. Save to `.launchpad/features/[feature-name]/FEATURE.md`.

### 7. State — mark architect complete
In `.launchpad/features/[feature-name]/STATE.md`:
- Update `## Current Phase` → `architect`.
- Update architect row: Status → `completed`, Date → today `YYYY-MM-DD`, Summary → one sentence of the chosen approach.

### 8. Close
Use the ask tool: "Architecture is ready. What's next?"
→ Start building now (continue into `/launchpad-implement`)
→ Review the architecture first (stop here)
