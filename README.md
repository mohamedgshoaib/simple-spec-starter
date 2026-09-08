# simple-spec-starter

A small starter for spec-driven work with AI agents.

It keeps the session workflow, optional project identity, and agent rules in clear places. Use the workflow by itself, or add only the parts your project needs.

## The core workflow

The required part of this repo is the `spec/sessions/` directory.

- `spec/sessions/README.md` is the sessions routing file.
- `spec/sessions/session-XX.md` is a numbered session file. Replace `XX` with the session number.
- `spec/sessions/HANDOFF.md` is the handoff file for the next agent.
- `handoff` is a skill for writing the handoff file.
- `wrap-up` is a skill for recording verified end-of-session facts.
- `grilling` is a skill for testing a plan before new feature work starts.
- `unslop` is a skill for interface copy, documentation, README files, Markdown, and other saved content. It does not apply to chat replies unless you invoke it.

These files and skills define the core workflow. The other included skills are project-specific additions.

## Start here

For a new project, tell your agent:

> Start this spec for a new project: [one sentence about what you want to build]. Help me define it before writing code.

For an existing codebase, tell your agent:

> Start the spec workflow for this existing codebase. Learn only what you need about the current project, then begin the first session without changing application code.

That is the full setup prompt. The agent instructions own the rest of the startup flow.

## Identity files

`spec/identity/` holds product facts, audience details, positioning, brand voice, and wording rules. Keep it when the project needs that context. Remove it when it does not.

Agents will not ask whether to use identity. If the directory exists, they read it. If it does not exist, they continue without mentioning it. Unfilled template text is never treated as a project fact.

Identity files are not design-system or implementation rules.

## Technical context

`spec/technical-context.md` is a short project fact file that agents read at the start of each session. The agent fills it during the first startup and updates it only when one of its facts changes.

It records one project sentence, whether code already exists, the main stack names, the main code paths, normal checks, and constraints. It does not copy dependency lists, exact versions, every project script, directory trees, or framework documentation.

Project facts stay in `spec/technical-context.md`. Agents do not copy them into `AGENTS.md` or `.claude/CLAUDE.md`.

## Reading order

At the start of a session, an agent should read these files in order:

1. `AGENTS.md` or `.claude/CLAUDE.md`: the agent instruction file.
2. `spec/sessions/README.md`: the sessions routing file.
3. The highest-numbered `spec/sessions/session-XX.md` file: the current numbered session file. Treat it as active unless it contains an explicit end marker such as `Session ended` or `Today's work is done`.
4. `spec/sessions/HANDOFF.md`: the handoff file, if it exists and contains an active handoff.
5. `spec/technical-context.md`: the short technical context file.
6. `spec/identity/README.md`: the identity routing file, if it exists. If it does not exist, continue without mentioning it.
7. `spec/identity/project-dna.md`: the project identity file, if it exists. If it does not exist, continue.
8. `spec/identity/brand-voice.md` and `spec/identity/TONE.md`: read each file if it exists when writing interface copy or other saved content that depends on product identity. If a file does not exist, continue without it.

The session workflow comes first. Technical context keeps discovery short. Identity files add product and brand context when they exist.

## Skills are a menu

The `.agents/skills/` and `.claude/skills/` directories contain local skills. Each skill is independent. Keep the skills that match the project and remove the ones that do not.

For example:

- `vercel-react-best-practices` is a React and Next.js performance skill.
- `no-use-effect` is a React-specific skill.
- `make-interfaces-feel-better` is a UI design and interaction skill.
- `typescript-expert` is a TypeScript and JavaScript skill.
- `write-project-readme` is a README research and writing skill.
- `codebase-design` is a module and architecture skill.
- `commit-message` is a commit message writing skill.

If you use both `.agents/skills/` and `.claude/skills/`, remove unused skills from both directories. Before removing a skill, check `AGENTS.md` and `.claude/CLAUDE.md`. If an instruction names a skill, keep that skill for the work covered by the instruction or update the instruction too.

## When to use this

Use this starter when work will span more than one session, involve more than one agent, or need product decisions to stay available after the chat ends.

Skip it for a throwaway script or a project that already has a workflow for session context and handoffs.

This starter is small on purpose. Keep the workflow. Add identity files and specialist skills only when they help.
