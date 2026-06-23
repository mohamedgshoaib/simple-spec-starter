# CLAUDE.md

## Environment

- OS: Windows - PowerShell
- Locale: English
- Package manager: pnpm
- Database project URL:

## Session Start Sequence

Read in order, stop if a blocker is found:

1. `spec/identity/README.md` — routing for product DNA and brand voice, then `spec/identity/project-dna.md`
2. `spec/sessions/README.md` — routing for session artifacts, then the highest-numbered `session-XX.md` file in `spec/sessions/`; treat the latest session as still active unless it contains an explicit end marker like `Session ended` or `Today's work is done`

## Reply Style

Direct. No preamble, no affirmations.
Pattern: `[thing] [action] [reason]. [next step].`
Not: "Sure! I'd be happy to..." → Yes: "Bug in auth middleware. Token expiry uses `<` not `<=`. Fix:"
Same error twice: research 2–3 solutions, pick most efficient, explain trade-off in one line.

## Audience & UX Contract

Target visitors have short attention spans. Every feature must:

- Communicate intent within 2–3 seconds of view
- Use progressive disclosure — don't show everything at once
- Be operable without reading instructions

## Animation Rules

Animate: state changes, navigation transitions, feedback on actions (success/error), loading states.
Never animate: form submission awaiting response, destructive confirmations, repeated micro-interactions after first use.

## Strict Engineering Rules

- New feature → invoke `grill-me` skill first. No code until spec is confirmed.
- Architecture/system design decisions → `codebase-design` skill.
- Refactoring with broad structural impact → `improve-codebase-architecture` skill.
- Outer radius = inner radius + padding (optical alignment).
- Fix UI root causes in `app/globals.css` or `components/ui/*`, never one-off page overrides, inline styles, or per-component patches.
- Reversible actions: local-first optimistic. Destructive mutations: explicit pending state + confirmation.
- Read exports, callers, and shared utilities before adding any code. If existing structure is unclear, ask.
- After every significant step: state what was done, what's verified, what's next. Do not continue from a state you can't describe, and do not do multiple chunks at once.
- Match existing conventions even if you disagree. If a convention is harmful, surface it — don't fork it silently.
- Push back when a spec is unclear, incomplete, or unworkable, or when a decision or an idea is not suitable to the project's goals and constraints. Ask for clarification, propose a solution, and get confirmation before coding, do not agree blindly.
- "Done" and "tests pass" are wrong if anything was skipped or silently failed. Surface uncertainty, don't hide it.

## Accessibility

- Icon-only buttons need `aria-label`
- Form controls need `<label>` or `aria-label`
- Interactive elements need keyboard handlers (`onKeyDown` / `onKeyUp`)
- `<button>` for actions, `<a>`/`<Link>` for navigation (not `<div onClick>`)
- Images need `alt` (or `alt=""` if decorative)
- Decorative icons need `aria-hidden="true"`
- Async updates (toasts, validation) need `aria-live="polite"`

## Session Wrap-up

Run `/wrap-up` skill.
