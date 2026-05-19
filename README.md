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
flowchart TD
    A(["/launchpad-brain"]) --> B[Scan project\nwrite PROJECT.md]
    B --> C[Ask: what feature?]
    C --> D[Q&A per REFERENCE.md template\nreflect · confirm · adjust]
    D --> E[External sources?\nURL / image / doc]
    E --> F[Write REFERENCE.md]
    F --> G{Continue to\narchitect now?}
    G -- yes --> H(["/launchpad-architect"])
    G -- no --> WAIT1([Wait — run /launchpad-architect when ready])

    H --> I[Read PROJECT.md + REFERENCE.md]
    I --> J[Propose approach\nreflect · confirm · adjust]
    J --> K[Write FEATURE.md\nApproach · Flow · Files · Steps · Tests]
    K --> L{Continue to\nbuild now?}
    L -- yes --> M(["/launchpad-implement"])
    L -- no --> WAIT2([Wait — run /launchpad-implement when ready])

    M --> N[Show Steps list\nconfirm or adjust]
    N --> O[Build step by step\nnarrate each step]
    O --> P{Continue to\ntest now?}
    P -- yes --> Q(["/launchpad-test"])
    P -- no --> WAIT3([Wait — run /launchpad-test when ready])

    Q --> R[Run test scenarios]
    R --> S{All pass?}
    S -- yes --> T{Archive feature?}
    S -- no --> U[Fix or note each failure]
    U --> T
    T -- yes --> V[Move to .launchpad/completed/]
    T -- no --> WAIT4([Feature stays active])

    style A fill:#4A90D9,color:#fff
    style H fill:#4A90D9,color:#fff
    style M fill:#4A90D9,color:#fff
    style Q fill:#4A90D9,color:#fff
    style V fill:#27AE60,color:#fff
    style WAIT1 fill:#888,color:#fff
    style WAIT2 fill:#888,color:#fff
    style WAIT3 fill:#888,color:#fff
    style WAIT4 fill:#888,color:#fff
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
