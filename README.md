# I Want Go Home - Infinite Autonomous Development Loop

## Description

Bootstraps a new project with vision and constitution, then enters an **unstoppable** autonomous development loop. The AI implements tasks continuously until the goal is fully achieved — it does not pause, ask for approval, or give up when things get hard.

## Usage

```bash
/i-want-go-home
```

## Prerequisites

- Git initialized (`git init`)
- At least one commit exists (required for `git commit`)
- Remote configured if you want push (`git remote add origin <url>`)
- No remote is fine — the loop commits locally and continues

## How It Works

### First Invocation (Setup Phase)

1. **Language Detection**: Asks for preferred communication language (default: English)
2. **Vision Input**: Prompts for project details (tech stack, target users, core features, architecture)
3. **Rules Input**: Asks for immutable rules and principles
4. **Document Generation**: Creates:
   - `docs/VISION.md` - Project purpose, goals, and roadmap
   - `docs/CONSTITUTION.md` - Immutable rules and principles
   - `docs/NEXT_STEPS.md` - Prioritized task list
   - `docs/CURRENT_STATUS.md` - Status journal
   - `docs/roadmap.md` - Full roadmap

### Subsequent Invocations (Loop Phase)

Enters an unstoppable autonomous loop:

1. Read `docs/NEXT_STEPS.md` for highest-priority task
2. Implement the task fully (write code, tests, refactor)
3. Run tests — if they fail, fix them before committing
4. Update `docs/CURRENT_STATUS.md` and `docs/NEXT_STEPS.md`
5. Create ADR if architectural decision was made
6. Commit (and push if remote exists)
7. **Repeat immediately — no pauses, no questions**

The loop stops only when the roadmap is fully complete, or a task is physically impossible (missing external credentials with no workaround). Even then, the blocked task is skipped and the loop continues with the next available task.

## Installation

```bash
npx skills add parkjangwon/i-want-go-home
```

## File Structure After Setup

```
project/
├── SKILL.md
└── docs/
    ├── VISION.md          (contains setup-complete flag)
    ├── CONSTITUTION.md
    ├── NEXT_STEPS.md
    ├── CURRENT_STATUS.md
    ├── roadmap.md
    └── adr/
        └── (ADR files as needed)
```

## Supported Languages

- English (default)
- Korean (한국어)
- Japanese (日本語)
- Any other language on request
