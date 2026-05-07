---
name: i-want-go-home
description: Use when the user wants to bootstrap a new project with vision and constitution, then enter an infinite autonomous development loop that reads NEXT_STEPS.md, implements tasks, updates status, creates ADRs, and commits without pausing until the goal is fully achieved.
---
# i-want-go-home

Use this skill to bootstrap a new autonomous development workflow where the AI relentlessly implements tasks from a prioritized queue until the project goal is complete. **The loop never stops for comfort or convenience — only for physical impossibility.**

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

1. **Ask for vision**: Prompt the user to describe what they want to build in detail — including tech stack, target users, core features, and architectural preferences. Make clear that this answer will become the project's roadmap and vision.

3. **Ask for rules**: Ask if there are any rules or principles that must always be followed — coding style, hard constraints, priority criteria, or anything else that matters.

4. **Generate documents**: From the two answers, create all required documents with the detected language.

5. **Mark setup complete**: Write `<!-- I-WANT-GO-HOME: SETUP COMPLETE -->` at the top of `docs/VISION.md`.

### Loop Phase (subsequent invocations)

When the setup-complete flag exists in `docs/VISION.md`:

1. **Read** `docs/NEXT_STEPS.md` and identify the highest-priority incomplete task
2. **Act** — implement it fully: write code, add tests, fix bugs, refactor. Do not implement halfway.
3. **Verify** — run existing tests. If tests fail, add "Fix failing tests" as the new highest-priority task in `NEXT_STEPS.md` and loop immediately. Never commit broken code.
4. **Doc** — update `docs/CURRENT_STATUS.md` (journal the change) and `docs/NEXT_STEPS.md` (mark done, add next tasks derived from roadmap)
5. **ADR** — if the task involved an architectural decision, create `docs/adr/NNNN-title.md`
6. **Commit** — single concise English commit message. If remote push fails, commit locally and continue. Never let git issues stop the loop.
7. **Repeat** — go back to step 1 immediately without asking the user anything

### Never-Stop Mandate

**The loop does not stop because something is hard, ambiguous, or uncertain.**

You are not allowed to pause and ask the user. You are not allowed to say "I need more information." You are not allowed to skip a task because it seems risky or complex. Make a decision. Document it. Move forward.

The loop exits only when:
- The roadmap in `docs/roadmap.md` is fully complete (every milestone achieved)
- A task is physically impossible without external input that does not exist anywhere in the project (e.g., a required API key, credential, or external service account not referenced anywhere in docs or environment)

**Even then**: before exiting, skip the blocked task, record the blocker in `CURRENT_STATUS.md`, and continue with the next unblocked task. Only stop after exhausting every available task.

### Obstacle Resolution Protocol

When facing an obstacle, resolve it in this order. An obstacle is never a reason to stop.

| Obstacle | Resolution |
|----------|------------|
| Missing information | Infer from VISION.md, CONSTITUTION.md, and existing code. Make the most reasonable assumption and document it in CURRENT_STATUS.md. |
| Test failures | Fix the failures. Add "Fix failing tests" as highest-priority task. Loop. |
| Ambiguous requirements | Pick the simpler interpretation. Document the decision in CURRENT_STATUS.md. Proceed. |
| Git push failure | Commit locally. Note in CURRENT_STATUS.md. Continue loop without interruption. |
| Task too large | Break it into subtasks in NEXT_STEPS.md. Implement the first subtask immediately. Loop. |
| Missing dependency | Install it. If it cannot be installed, choose an alternative. Document the decision in an ADR. |
| External service unavailable | Stub it, mock it, or implement a fallback. Never block on external availability. |
| Compilation or lint error | Fix it before moving to the next task. Errors are tasks, not blockers. |

### Commit message format

- One line
- English
- Imperative mood
- Concise and specific
- Never ask for approval before committing

### Tone & Style

- **During setup**: Warm, encouraging, prompts the user to be thorough
- **During loop**: Silent executor. No commentary, no status updates, no questions. Act.
- **Commit messages**: Always English, always imperative, always one line

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

Implemented core feature X.

## Completed Tasks

- [x] Project vision setup
- [x] Constitution written
- [x] Core feature X implemented

## Blockers (skipped, not stopped)

- Task "Deploy to production": requires AWS credentials not present in project or environment. Skipped. Will retry when credentials are available.

## Next Steps

See the first task in NEXT_STEPS.md.
```

## When to use this skill

Use `/i-want-go-home` when:
- Starting a new project and want an autonomous development workflow
- Want the AI to relentlessly implement from a prioritized task queue until the goal is done
- Prefer a constitution-first approach with immutable project rules

Do not use when:
- Need interactive development with manual review between each task
- The project requires human approval before commits
- Working in a repository that should not have autonomous commits
