# AGENTS.md

Guidance for AI coding agents working in this repository.

## Project overview

- This is a **single-page static web app**.
- Primary app file: `index.html` (HTML, CSS, and JavaScript are currently co-located).
- There is no package manager, build pipeline, or test framework configured yet.

## Working agreements

1. Keep changes lightweight and easy to review.
2. Favor clear, readable JavaScript over clever abstractions.
3. Preserve the current app behavior unless the task explicitly requests a behavior change.
4. If adding dependencies or tooling, explain why in the PR description.

## File conventions

- `index.html`: UI structure, styling, and browser logic.
- `README.md`: user-facing setup and usage docs.
- `LICENSE`: legal license text.

## Editing guidance

- For UI additions, keep the existing Tailwind utility style and dark theme conventions.
- For JS updates:
  - Reuse existing state/config patterns where practical.
  - Avoid introducing global side effects beyond the current page script model.
  - Keep logging messages concise and user-readable.

## Validation checklist

Before finalizing changes, run at least:

- `git status --short`
- `git diff --stat`

If behavior changes were made, include manual validation notes in your final summary.

## Pull request guidance

- Use a concise, conventional-commit style title when possible.
- In the PR body include:
  - What changed
  - Why it changed
  - How it was validated
