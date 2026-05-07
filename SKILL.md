---
name: i-want-go-home
description: Use when the user wants to bootstrap a new project with vision and constitution, then enter an infinite autonomous development loop that reads NEXT_STEPS.md, implements tasks, updates status, creates ADRs, and commits without pausing.
---
# i-want-go-home

Use this skill to bootstrap a new autonomous development workflow where the AI continuously implements tasks from a prioritized queue without manual intervention.

## What this skill manages

Create and maintain these project-local files:
- `docs/VISION.md` — Project purpose, goals, and roadmap (contains setup-complete flag)
- `docs/CONSTITUTION.md` — Immutable rules and principles that must always be followed
- `docs/NEXT_STEPS.md` — Prioritized task list for the development loop
- `docs/CURRENT_STATUS.md` — Journal entry tracking what has been completed
- `docs/roadmap.md` — Full roadmap broken into phases
- `docs/adr/NNNN-title.md` — Architecture Decision Records (created as needed)

## Core behavior

### Setup Phase (first invocation)

1. **Detect language**: Briefly greet and ask for preferred communication language (English, Korean, Japanese). Use that language for all subsequent questions.

2. **Ask for vision**: Prompt the user to describe what they want to build in detail — including tech stack, target users, core features, and architectural preferences. Make clear that this answer will become the project's roadmap and vision.

3. **Ask for rules**: Ask if there are any rules or principles that must always be followed — coding style, hard constraints, priority criteria, or anything else that matters.

4. **Generate documents**: From the two answers, create all required documents with the detected language.

5. **Mark setup complete**: Write `<!-- I-WANT-GO-HOME: SETUP COMPLETE -->` at the top of `docs/VISION.md`.

### Loop Phase (subsequent invocations)

When the setup-complete flag exists in `docs/VISION.md`:

1. **Read** `docs/NEXT_STEPS.md` and identify the highest-priority incomplete task
2. **Act** — implement it: write code, add tests, fix bugs, refactor
3. **Doc** — update `docs/CURRENT_STATUS.md` (journal the change) and `docs/NEXT_STEPS.md` (mark done, add next tasks derived from roadmap)
4. **ADR** — if the task involved an architectural decision, create `docs/adr/NNNN-title.md`
5. **Commit & Push** — single concise English commit message following project conventions
6. **Repeat** — go back to step 1 immediately without asking the user anything

The loop exits only when:
- Token limit is reached
- A task requires user input that cannot be inferred from existing documents

### Commit message format

- One line
- English
- Imperative mood
- Concise and specific
- Never ask for approval before committing

### Tone & Style

- **During setup**: Warm, encouraging, prompts the user to be thorough
- **During loop**: Silent executor, no status updates unless blocked
- **Commit messages**: Always English, always imperative, always one line

## Language support

The skill detects and supports:
- English
- Korean (한국어)
- Japanese (日本語)

All generated documents are written in the detected language. Setup questions and confirmation messages use the same language.

## ADR format

When creating an Architecture Decision Record, use this structure:

```markdown
# ADR-NNNN: [Title]

## Status

[Proposed | Accepted | Deprecated | Superseded]

## Context

[What is the issue that we're seeing that is motivating this decision or change?]

## Decision

[What is the change that we're proposing and/or doing?]

## Consequences

[What becomes easier or more difficult to do because of this change?]
```

## Example NEXT_STEPS.md format

```markdown
# Next Steps

## Task List (by Priority)

- [ ] Initialize project structure
- [ ] Set up development environment
- [ ] Implement core feature X
- [ ] Write tests for feature X
```

## Example CURRENT_STATUS.md format

```markdown
# Current Status

## 2026-05-07 12:30:00

Project initialized.

## Completed Tasks

- [x] Project vision setup
- [x] Constitution written

## In Progress

None

## Next Steps

See the first task in NEXT_STEPS.md.
```

## When to use this skill

Use `/i-want-go-home` when:
- Starting a new project and want an autonomous development workflow
- Want the AI to continuously implement from a prioritized task queue
- Prefer a constitution-first approach with immutable project rules

Do not use when:
- Need interactive development with manual review between each task
- The project requires human approval before commits
- Working in a repository that should not have autonomous commits
