# I Want Go Home - Infinite Development Loop Skill

## Description

Bootstraps a new project with vision and constitution, then enters an infinite autonomous development loop.

## Usage

```bash
/i-want-go-home
```

## How It Works

### First Invocation (Setup Phase)

1. **Language Detection**: Asks for preferred communication language
2. **Vision Input**: Prompts for project details (tech stack, target users, core features, architecture)
3. **Rules Input**: Asks for immutable rules and principles
4. **Document Generation**: Creates:
   - `docs/VISION.md` - Project purpose, goals, and roadmap
   - `docs/CONSTITUTION.md` - Immutable rules and principles
   - `docs/NEXT_STEPS.md` - Prioritized task list
   - `docs/CURRENT_STATUS.md` - Status journal
   - `docs/roadmap.md` - Full roadmap

### Subsequent Invocations (Loop Phase)

Enters infinite autonomous loop:

1. Read `docs/NEXT_STEPS.md` for highest-priority task
2. Implement the task (write code, tests, refactor)
3. Update `docs/CURRENT_STATUS.md` and `docs/NEXT_STEPS.md`
4. Create ADR if architectural decision needed
5. Commit and push with English imperative message
6. Repeat immediately

## Installation

Deploy `skill.sh` to your skills.sh environment.

## File Structure After Setup

```
project/
├── docs/
│   ├── VISION.md          (contains setup-complete flag)
│   ├── CONSTITUTION.md
│   ├── NEXT_STEPS.md
│   ├── CURRENT_STATUS.md
│   ├── roadmap.md
│   └── adr/
│       └── (ADR files as needed)
└── skill.sh
```

## Supported Languages

- English
- Korean (한국어)
- Japanese (日本語)
