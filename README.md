# Launchpad

ASDLC workflow for non-developers. Guided conversations — no prompts to write, no commands to memorize.

## Install

Two steps — run these in your terminal:

```bash
claude plugin marketplace add Formartha/launchpad
claude plugin install --scope user launchpad@launchpad
```

Then restart Claude Code. Type `/brain` to start.

## How it works

Each feature moves through 4 phases. Every phase is a guided conversation — the skill asks, you answer.

```
/brain      start here → scans project + defines feature → REFERENCE.md
/architect  design a solution                             → FEATURE.md
/implement  build it                                     → code in your project
/test       verify it works + archive when done          → tests
```

## Usage

**Start anything:**
```
/brain
```
Brain handles everything first — scans your project, then asks what you want to build.

**Continue where you left off:**
Run the same skill again — it picks up from the current state.

**Missing a step?**
Each skill checks what's been done. If something is missing, it tells you exactly what to run first.

## What gets created

```
.launchpad/
├── PROJECT.md                  project knowledge base (written by brain)
├── features/
│   └── [feature-name]/
│       ├── STATE.md            current phase + history (orchestrator only)
│       ├── REFERENCE.md        what to build (from your answers)
│       └── FEATURE.md          how to build it (from architect)
└── completed/
    └── [feature-name]/         archived features (not scanned)
```

## Skills

| Skill | What it does |
|---|---|
| `/brain` | Entry point. Scans project, asks 5 questions, writes REFERENCE.md |
| `/architect` | Proposes a design, writes FEATURE.md |
| `/implement` | Builds the feature step by step |
| `/test` | Tests all scenarios, archives when done |
