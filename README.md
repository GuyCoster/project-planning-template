# Project Plan

> **Using this template:** replace the title above with your project's name, rewrite the line below to say what the project is, then delete this block and start Step 1.

Planning repository for *[project name]*. No code lives here — this repo works through the design of the project before anything gets built, following [Tech With Tim's 9-step planning framework](https://www.youtube.com/watch?v=AGWyx96lP8U).

The work is done conversationally with Claude Code acting as a planning mentor; `CLAUDE.md` holds its instructions. Each step is worked through in discussion and written to a numbered markdown file as it goes.

## The 9 steps
1. Start from your goal — why, who for, what makes it valuable
2. User capabilities & features
3. Data models
4. User flow & UI mapping
5. System architecture & core logic
6. Scope & MVP definition
7. Presentation layer
8. Tech stack selection
9. The development process

Technology choices are deliberately deferred until Step 8, so the stack is chosen to fit the project rather than the other way around.

## Files
| File | Purpose |
|---|---|
| `CLAUDE.md` | Instructions for the planning assistant |
| `00_progress-tracker.md` | Status of all 9 steps — start here |
| `00_project-overview.md` | Condensed summary of everything settled so far |
| `00_step-guide.md` | Key questions, exit criteria and traps per step |
| `00_decisions.md` | Decision log, including rejected alternatives |
| `01_…` – `09_…` | Output of each step |

`CLAUDE.md` and the `00_*` files are project-agnostic — they're the reusable part. Only this README and the numbered step files describe a specific project.

## Working on this
Open the repo with Claude Code and say which step you're picking up, or just start — it reads the tracker first and continues from the next incomplete step. A step usually takes several exchanges; it's marked `Final` only once its exit criteria in the step guide are met. Work happens on `main`, and files are committed and pushed as they change.

## After planning
No code is added here while planning is under way. When Step 9 closes, you decide where the build lives — a separate build repo, or this one with the planning files moved into `docs/planning/`. Either way the documents the build needs are written fresh from this planning output rather than copied (see the handoff section of `00_step-guide.md`), and the planning files are then frozen as the record of what was decided and why.

## Reusing this setup
This repo is intended to be a GitHub **template repository** (Settings → *Template repository*). Each new project starts from **Use this template** → name it → open with Claude Code → Step 1. Don't fork it: GitHub allows only one fork of a repo per account, so a fork works once and blocks every project after it.

Template repos don't sync, so if you improve `CLAUDE.md` or the step guide during a project, copy that change back here yourself.
