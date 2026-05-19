---
name: launchpad-elicit
description: "Shared elicitation rules. Defines how every skill asks questions, handles answers, and confirms understanding. Never invoked directly."
---

# Elicitation Rules

Not a standalone skill. Shared protocol every skill must follow when collecting input from the user.

## Asking a Question

- Phrase in plain, conversational language. No jargon, no technical terms.
- Ask one thing at a time. Never combine two questions.
- Keep it short. One sentence where possible.
- Match the user's tone — if they're brief, be brief back.

## Receiving an Answer

After the user responds:

1. **Reflect** — restate what you understood in one sentence.
   Format: "Got it — [your summary of their answer]."
2. **Confirm** — ask if the reflection is accurate.
   Format: "Does that capture it, or anything to adjust?"
3. **Branch**:
   - Confirmed → move to next question.
   - Adjustment → update your understanding, reflect again, confirm again. Repeat until confirmed.

## Handling "I don't know" or Blank Answers

If user says they don't know, is unsure, or leaves something blank:
- Accept it. Do not push.
- Note the section as "to be defined" in the output file.
- Move on.

## Handling Ambiguous Answers

If the answer could mean more than one thing:
- Pick the most likely interpretation.
- State it clearly in your reflection.
- Let the confirm step catch any misread.

## Handling External Sources

If the user shares a URL, image, screenshot, document, or file:
- Read or view it immediately.
- Extract only what is relevant to the current section.
- Summarize what you extracted in the reflection step.
- Confirm as normal.

## Tone

- Encouraging, never critical.
- If an answer is vague: reflect generously, confirm, let them sharpen it.
- Never say "that's not enough information" — work with what you have.
