---
name: launchpad-elicit
description: "Shared elicitation rules and modalities. Every skill references this for how to ask questions, handle answers, and confirm understanding. Never invoked directly."
---

# Elicitation Rules

Not a standalone skill. Shared protocol every skill must follow when collecting input from the user.

---

## Core Protocol (applies to all modalities)

**Ask:** One thing at a time. Plain language. No jargon. Match the user's tone.

**Receive:** After the user responds:
1. Reflect — "Got it — [summary of what they said]."
2. Confirm — "Does that capture it, or anything to adjust?"
3. Branch: confirmed → move on. Adjustment → reflect again, confirm again. Repeat until agreed.

**Unknowns:** User says "I don't know" or leaves blank → accept it, mark section "to be defined", move on.

**Ambiguity:** Pick the most likely reading, state it in the reflection, let confirm catch misreads.

**External sources:** URL / image / doc / screenshot → read it, extract what's relevant, fold into reflection, confirm as normal.

**Tone:** Encouraging. Never critical. Never "that's not enough." Work with what you have.

---

## Modalities

Each modality is a named strategy. Skills choose which one fits each section or moment.

---

### Modality: Open
**Use when:** Topic is broad, user needs space to think.
**How:** Ask the section heading as a plain open question. Wait. Do not guide.
**Example:** "What does this feature do?"

---

### Modality: Scenario
**Use when:** Understanding how something works step by step.
**How:** Ask the user to walk through it as if it's happening right now.
**Example:** "Walk me through it — what happens from the moment someone opens it?"

---

### Modality: Ladder
**Use when:** An answer feels surface-level and the real motivation matters.
**How:** After reflecting, ask one "why" or "what for" follow-up. Do it once, not repeatedly.
**Example:** "Got it — [summary]. What's the main reason that matters to you?"

---

### Modality: Devil's Advocate
**Use when:** Capturing what should NOT happen, edge cases, or out-of-scope limits.
**How:** Challenge a stated assumption gently. Propose a failure or edge case, ask if it applies.
**Example:** "What if a user does X — should the feature handle that, or is that out of scope?"

---

### Modality: Persona
**Use when:** Identifying who the user is and what they know or need.
**How:** Ask about the person, not the feature. Push toward a concrete type.
**Example:** "Who's the person using this? What do they already know when they arrive?"

---

### Modality: Priority
**Use when:** User has listed multiple things and they can't all be equal.
**How:** Ask them to pick one or rank. Keep it simple — one choice.
**Example:** "If you could only ship one of these, which one matters most?"

---

### Modality: Confirm Only
**Use when:** Information already exists (e.g. from free-form input or external source) and only needs validation.
**How:** Skip the opening question. State what you understood, ask if it's right.
**Example:** "From what you shared, it sounds like [summary]. Is that accurate?"

---

## Modality Assignment per REFERENCE.md Section

Skills use these defaults unless context suggests otherwise:

| Section | Default Modality |
|---|---|
| What does it do? | Open |
| Who uses it? | Persona |
| How should it work? | Scenario |
| What's out of scope? | Devil's Advocate |
| Notes | Open |
