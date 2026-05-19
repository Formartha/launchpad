---
name: launchpad-architect
description: "Designs the technical approach for a feature. Reads the feature brief, proposes an implementation plan, writes FEATURE.md."
---

# Architect

Read the feature brief, design a concrete implementation plan, propose it to the user, adjust based on feedback, then write FEATURE.md.

## Steps

### 1. Ask which feature
Ask: "Which feature are we designing?" Wait for the answer. Use that as `[feature-name]`.

### 2. State — start
Follow On Skill Start rules in `skills/launchpad-state/SKILL.md`. Verify `brain` phase is complete.
If not: stop and tell the user what to run first.

### 3. Read context silently
- `.launchpad/PROJECT.md`
- `.launchpad/features/[feature-name]/REFERENCE.md`

### 4. Propose approach
"Here's how I'd build [feature-name]:" — short summary, 3–5 sentences. Cover:
- What approach you'll take
- What files will be created or changed
- Any dependencies or tools needed

Follow the elicitation confirm loop in `skills/launchpad-elicit/SKILL.md` — reflect the approach, confirm, adjust until agreed.

### 5. Adjust if needed
If the user redirects: update approach, reflect again, confirm. Follow `skills/launchpad-elicit/SKILL.md` throughout.

### 6. Write FEATURE.md
Open `templates/FEATURE.md`. Fill in:
- **Approach**: the agreed paragraph
- **Flow**: plain-text arrow diagram, user perspective. Use `→ ↓ ↘ ↙` and short labels. No jargon — a non-developer must follow it. Show branching paths (e.g. success vs. error).
- **Files**: each file to create or modify, one per line, with a short note
- **Steps**: numbered implementation steps, concrete and specific
- **Test Scenarios**: one line per scenario that verifies the feature works

Replace `{{feature-name}}`. Save to `.launchpad/features/[feature-name]/FEATURE.md`.

### 7. State — end
Follow On Skill End rules in `skills/launchpad-state/SKILL.md`. Mark `architect` complete in STATE.md.

### 8. Close
"Architecture is ready. Want me to start building it now, or would you prefer to review first?"

- Yes / now → continue directly into the `/launchpad-implement` skill steps.
- No / later → "Run `/launchpad-implement` when you're ready."
