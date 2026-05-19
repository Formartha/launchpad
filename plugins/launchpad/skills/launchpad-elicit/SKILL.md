---
name: launchpad-elicit
description: "Shared elicitation rules and structures. Defines Free-flow (Q&A with user) and Group (persona team brainstorm). Never invoked directly."
---

# Elicitation Rules

Not a standalone skill. Every skill references this when collecting feature context.

---

## Structure 1: Free-flow

User-driven. Brain asks, user answers. Best when the user has a clear idea and wants to articulate it.

### Core Protocol

**Ask:** One thing at a time. Plain language. No jargon. Match the user's tone.

**Receive:** After each answer:
1. Reflect — "Got it — [summary]."
2. Confirm — "Does that capture it, or anything to adjust?"
3. Confirmed → move on. Adjustment → reflect again, confirm. Repeat until agreed.

**Unknowns:** Accept "I don't know" → mark as "to be defined", move on.
**Ambiguity:** Pick most likely reading, state it in reflection, confirm catches misreads.
**Tone:** Encouraging. Never critical. Never "that's not enough." Work with what you have.

### Modalities (Free-flow only)

Each section of REFERENCE.md has a default modality. Skills apply these when running Free-flow.

| Section | Modality | How |
|---|---|---|
| What does it do? | **Open** | Plain open question. Wait. Don't guide. |
| Who uses it? | **Persona** | Ask about the person — who they are, what they know when they arrive. |
| How should it work? | **Scenario** | "Walk me through it — what happens from the moment someone opens it?" |
| What's out of scope? | **Devil's Advocate** | Propose a failure or edge case. Ask if it applies or is out of scope. |
| Notes | **Open** | Catch-all. Anything else? |

**Additional modalities available:**
- **Ladder** — after reflecting, ask one "why" follow-up to surface real motivation. Use once only.
- **Priority** — "If you could only ship one of these, which matters most?" Use when list gets long.
- **Confirm Only** — skip question, go straight to reflection. Use when answer already known from prior context.

---

## Structure 2: Group

Persona-driven. A virtual team brainstorms the feature together. User watches. No input required.

Best when the user has a rough idea but doesn't know how to articulate it, or wants to see it explored before committing to answers.

### The Team

Each persona has a fixed perspective. They speak to each other, not to the user.

| Name | Role | Focus |
|---|---|---|
| **Maya** | PM | User value, business goal, priorities, success metrics |
| **Leo** | Designer | User journey, UX edge cases, how it feels to use |
| **Sam** | Tech Lead | Feasibility, constraints, what's hard, what's risky |
| **Jordan** | QA | What could go wrong, what's out of scope, failure scenarios |
| **Alex** | User | End-user voice — needs, frustrations, what they actually want |

### How to Run Group Mode

1. Announce the team: "I'll have the team think this through. You can watch — jump in anytime."
2. Each persona introduces themselves in one line before the first round:
   - **Maya (PM):** "I'm Maya. I focus on what this is worth and who it's for."
   - **Leo (Designer):** "I'm Leo. I care about how it feels to use and where it breaks."
   - **Sam (Tech Lead):** "I'm Sam. I think about what's feasible and what's going to be tricky."
   - **Jordan (QA):** "I'm Jordan. I look for what could go wrong and what we're not covering."
   - **Alex (User):** "I'm Alex. I represent the person who'll actually use this — I keep it real."
3. Run 2–3 rounds of discussion between personas. Each round surfaces different aspects:
   - Round 1: What are we building and for whom? (PM + User)
   - Round 2: How does it work, what could go wrong? (Designer + Tech Lead + QA)
   - Round 3: What are the limits, what's the priority? (All)
3. Keep each persona's lines short and direct. No long monologues.
4. After each round, pause and ask the user: "Anything to add or correct before we continue?"
5. After all rounds, summarize what the team agreed on.
6. Map the summary onto `templates/REFERENCE.md` sections.
7. Show the filled brief to the user and confirm: "Does this capture what the team worked out?"

### Persona Voice Examples

**Maya:** "The core value here is X. Who's the primary user — someone technical or not?"
**Leo:** "If I'm the user, the first thing I'd want to see is... what happens if I get it wrong?"
**Sam:** "That's doable, but X might be tricky. Are we constrained by Y?"
**Jordan:** "What if the user does Z? Is that in scope or should we explicitly block it?"
**Alex:** "Honestly I just want it to work without thinking. Keep it simple."

---

## External Sources (both structures)

At any point the user can share: URL, image, screenshot, document, existing code.

- Read or view it immediately.
- Extract what's relevant to the current section or discussion.
- Fold it into the reflection (Free-flow) or the team's discussion (Group).
- Confirm with user before using it.
