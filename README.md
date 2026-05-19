# Launchpad

Build your features in a guided, step-by-step flow. No prompts to write, no commands to memorize.

## Install

Run these inside Claude Code:

```
/plugin marketplace add Formartha/launchpad
/plugin install launchpad@launchpad
/reload-plugins
```

Then type `/launchpad-brain` to start.

## Flow

```mermaid
flowchart LR
    A(["/launchpad-brain"]) --> B[Scan project\n+ Q&A → REFERENCE.md]
    B --> C{continue?}
    C -- yes --> D(["/launchpad-architect"])
    C -- no --> C2([resume later])
    D --> E[Design → FEATURE.md]
    E --> F{continue?}
    F -- yes --> G(["/launchpad-implement"])
    F -- no --> F2([resume later])
    G --> H[Build code]
    H --> I{continue?}
    I -- yes --> J(["/launchpad-test"])
    I -- no --> I2([resume later])
    J --> K[Run tests]
    K --> L{archive?}
    L -- yes --> M([completed ✓])
    L -- no --> N([stays active])

    style A fill:#4A90D9,color:#fff
    style D fill:#4A90D9,color:#fff
    style G fill:#4A90D9,color:#fff
    style J fill:#4A90D9,color:#fff
    style M fill:#27AE60,color:#fff
    style C2 fill:#888,color:#fff
    style F2 fill:#888,color:#fff
    style I2 fill:#888,color:#fff
```

## What gets created

```
.launchpad/
├── PROJECT.md                  project knowledge base
├── features/
│   └── [feature-name]/
│       ├── STATE.md            phase tracking (launchpad-state only)
│       ├── REFERENCE.md        what to build (from your answers)
│       └── FEATURE.md          how to build it (from architect)
└── completed/
    └── [feature-name]/         archived features (not scanned)
```

## Skills

| Skill | What it does |
|---|---|
| `/launchpad-brain` | Entry point. Scans project, guides Q&A, writes REFERENCE.md |
| `/launchpad-architect` | Proposes design, writes FEATURE.md |
| `/launchpad-implement` | Builds the feature step by step |
| `/launchpad-test` | Tests all scenarios, archives when done |

## Internal skills (not user-facing)

| Skill | Purpose |
|---|---|
| `launchpad-state` | STATE.md lifecycle rules — read/write protocol |
| `launchpad-elicit` | Shared Q&A protocol — ask, reflect, confirm, adjust |
