---
name: architect
description: "Designs the technical approach for a feature. Reads the feature brief and proposes an implementation plan. Writes FEATURE.md."
---

# Architect

Read the feature brief and design a concrete implementation plan. Propose it to the user, adjust based on feedback, then write FEATURE.md.

---

## Steps

### 1. Ask which feature
Ask: "Which feature are we designing?"

Wait for the answer. Use that as `[feature-name]`.

### 2. Orchestrator — start
Follow the On Skill Start rules in `skills/orchestrator/SKILL.md`. Verify `brain` phase is complete.
If not: stop and tell the user what to run first.

### 3. Read context silently
Read both files without mentioning it:
- `.launchpad/PROJECT.md`
- `.launchpad/features/[feature-name]/REFERENCE.md`

### 4. Propose approach
Tell the user: "Here's how I'd build [feature-name]:" then give a short summary (3–5 sentences max). Cover:
- What approach you'll take
- What files will be created or changed
- Any dependencies or tools needed

Ask: "Does this make sense, or do you want to change anything?"

### 5. Adjust if needed
If the user redirects: update your approach and confirm again. Repeat until they say yes.

### 6. Write FEATURE.md
Open `templates/FEATURE.md`. Fill in:
- **Approach**: the agreed approach paragraph
- **Flow**: a plain-text diagram showing how the feature works from the user's perspective. Use arrows (`→`, `↓`, `↘`, `↙`) and short labels. No technical jargon — a non-developer must be able to read it and understand exactly what happens at each step. Show branching paths (e.g. success vs. error).
- **Files**: each file to create or modify, one per line, with a short note
- **Steps**: numbered implementation steps, concrete and specific
- **Test Scenarios**: one line per scenario that verifies the feature works

Replace `{{feature-name}}`. Save to `.launchpad/features/[feature-name]/FEATURE.md`.

### 7. Orchestrator — end
Follow the On Skill End rules in `skills/orchestrator/SKILL.md`. Mark `architect` as completed in STATE.md.

### 8. Close
Tell the user: "Architecture is ready. Run `/launchpad:implement` when you want to start building."
