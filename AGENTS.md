# Agent workflow

## Session start

Read these files in order:

1. `spec/sessions/README.md`: the sessions routing file.
2. The highest-numbered `spec/sessions/session-XX.md` file: the current numbered session file. Treat it as active unless it contains an explicit end marker such as `Session ended` or `Today's work is done`.
3. `spec/sessions/HANDOFF.md`: read this handoff file if it contains an active handoff.
4. `spec/technical-context.md`: the short project fact file.
5. `spec/identity/README.md`: read this identity routing file if it exists.
6. `spec/identity/project-dna.md`: read this project identity file if it exists.
7. `spec/identity/brand-voice.md` and `spec/identity/TONE.md`: read each file if it exists when writing interface copy or other saved content that depends on product identity.

If no numbered session file exists, create `spec/sessions/session-01.md` from the session template when real work begins.

Do not ask whether to use identity. If `spec/identity/` does not exist, continue without mentioning it. If an identity file still contains template placeholders, treat it as unfilled and do not use those placeholders as project facts.

## First startup

If `spec/technical-context.md` still contains placeholders, determine which case applies.

For a new project with no application code or project manifest:

1. Ask what the user wants to build and which constraints are fixed.
2. Use the `grilling` skill to settle product, stack, and architecture choices that must be decided before code.
3. Do not create application code until the user approves those choices.
4. Fill `spec/technical-context.md` after the stack is approved.

For an existing codebase:

1. Read only the root README, project manifests, lockfiles, relevant configuration, top-level source directories, and application entry points.
2. Fill `spec/technical-context.md` with verified facts.
3. Do not change application code during startup unless the user asks.
4. Stop discovery when the six fields in `spec/technical-context.md` are clear.

Do not scan dependency directories, generated files, build output, or version-control history during startup. Update `spec/technical-context.md` when one of its facts changes. Do not copy project facts into `AGENTS.md` or `.claude/CLAUDE.md`.

## Current documentation

Before writing or changing code that depends on a programming language, runtime, framework, library, SDK, API, CLI, or cloud service:

1. Confirm the installed version from project files, or the intended version from the user's approved plan.
2. Fetch current authoritative documentation for that version and the exact topic involved. Use Context7 when available; otherwise use the official documentation source.
3. For an existing codebase, match the installed version. For a new project, use the approved latest stable version.
4. Do not rely on model memory for API names, configuration, defaults, deprecations, or version behavior.
5. If current matching documentation cannot be reached, report that before writing code that depends on it.

Keep documentation lookup narrow. Do not fetch external documentation for local logic, writing, or refactoring that does not depend on an external contract.

## Engineering rules

- Use installed specialist skills only when the confirmed stack and current task match them. Do not load specialist skills during session startup.
- New feature: use the `grilling` skill before code. Ask only about unresolved behavior or consequential choices.
- Architecture or system design: use the `codebase-design` skill.
- Broad structural refactor: use the `improve-codebase-architecture` skill.
- Read existing exports, callers, related tests, and shared utilities before adding code.
- Prefer the smallest change that fits the current structure. Do not add a dependency or abstraction for hypothetical future use.
- Match existing conventions. If a convention causes a concrete problem, explain it instead of silently creating another pattern.
- Push back when a spec is unclear, incomplete, unworkable, or conflicts with the project's goals and constraints. Explain the problem, propose a workable option, and get confirmation before coding. Do not agree blindly.
- Run the project's configured format, lint, type, test, and build checks that apply to the change.
- State exactly what ran, what passed, and what was skipped. Do not claim completion when a required check failed or did not run.
- Analyze time and space complexity only for nontrivial algorithms or loops where it can affect the design.

## Testing

- Put assertions inside test cases, not setup or grouping blocks.
- Use the test tool's native asynchronous style. Do not mix callback completion with promises or async functions.
- Do not commit focused, disabled, or skipped tests unless the user explicitly accepts and documents the reason.
- Keep test suites shallow enough to make setup, behavior, and failures easy to trace.

## What automated checks cannot prove

Review these directly instead of assuming a passing tool proves them:

1. Business and domain logic
2. Clear and accurate naming
3. Architecture and data flow
4. Boundary conditions and failure cases
5. Accessibility, performance, and usability for user-facing work
6. Useful comments and documentation where the code alone is not clear

## Security

- Treat external input as untrusted and validate it at the system boundary.
- Do not execute untrusted text as code or inject raw content without validation and sanitization.
- Use safe platform APIs instead of building commands, queries, markup, links, paths, or stored values from untrusted strings.
- Do not expose secrets or sensitive values in code, logs, errors, tests, or documentation.
- Preserve authentication, authorization, privacy, and access checks when changing protected behavior.

## Interface and experience

Apply this section only to user-facing interface work.

- Communicate the purpose and primary action within 2 to 3 seconds of view.
- Use progressive disclosure. Do not show every detail at once.
- Make the interface usable without separate instructions.
- Fix shared UI problems in the shared source that owns them, such as the design system, theme, shared UI module, or global styles. Do not hide a shared cause with one-off page overrides, inline styles, or local patches.
- For nested rounded surfaces, set the outer radius to the inner radius plus the padding between them.
- Animate state changes, navigation transitions, action feedback, and loading states.
- Do not animate form submission while awaiting a response, destructive confirmations, or repeated micro-interactions after first use.

## Written content

When writing or editing interface copy, documentation, README files, Markdown, specs, guides, or other saved content, invoke the `unslop` skill.

Do not invoke `unslop` for chat replies, status updates, or other conversation unless the user explicitly asks.

## Session continuity

Use the `handoff` skill when work pauses and another session needs to continue it.

Run the `wrap-up` skill at the end of a work session. Record verified facts only.
