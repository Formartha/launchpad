---
name: launchpad-architect
description: "Designs technical approach for a feature. Reads feature brief, proposes implementation plan, writes FEATURE.md."
---

# Architect

Read feature brief, design implementation plan, propose to user, adjust, write FEATURE.md.

## Steps

### 1. Ask feature name
"Which feature are we designing?" Wait. Use as `[feature-name]`.

### 2. Orchestrator — start
Follow On Skill Start in `skills/launchpad-orchestrator/SKILL.md`. Verify `brain` complete.
Blocked → tell user what to run first.

### 3. Read context silently
- `.launchpad/PROJECT.md`
- `.launchpad/features/[feature-name]/REFERENCE.md`

### 4. Propose approach
"Here's how I'd build [feature-name]:" — 3–5 sentences max. Cover: approach, files affected, dependencies.
"Does this make sense, or change anything?"

### 5. Adjust
User redirects → update, confirm again. Repeat until yes.

### 6. Write FEATURE.md
Fill `templates/FEATURE.md`:
- **Approach**: agreed paragraph
- **Flow**: plain-text arrow diagram, user perspective. Arrows: `→ ↓ ↘ ↙`. No jargon. Show branches (success/error).
- **Files**: one per line, short note
- **Steps**: numbered, concrete
- **Test Scenarios**: one line per scenario

Replace `{{feature-name}}`. Save to `.launchpad/features/[feature-name]/FEATURE.md`.

### 7. Orchestrator — end
Follow On Skill End in `skills/launchpad-orchestrator/SKILL.md`. Mark `architect` complete.

### 8. Close
"Architecture ready. Run `/launchpad-implement` to start building."
