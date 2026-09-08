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
- `unslop` is a skill for cleaning up project-facing writing.

These files and skills define the core workflow. The other included skills are project-specific additions.

## Choose your setup

### Workflow only

Use this setup if you want the session and agent workflow without the identity layer.

Keep `spec/sessions/`, the agent instruction files, and the `handoff`, `wrap-up`, `grilling`, and `unslop` skills. You do not need `spec/identity/`. Do not copy it, or remove it after copying the starter.

Nothing in the sessions workflow depends on the identity files.

### Workflow with identity

Use `spec/identity/` when you are:

- building a website or product from scratch and need to define its identity
- working on an existing website and need to document or reshape its identity

The identity files hold product facts, audience details, positioning, brand voice, and wording rules.

They are not a design system and do not replace implementation rules.

If `spec/identity/` exists, read `spec/identity/README.md` first. Then read the identity files that apply to the work.

## How to use it

1. Copy the starter files into the root of an existing project or a new project.
2. Keep the core session workflow.
3. Keep `spec/identity/` only if the project needs product or brand identity guidance.
4. Keep the specialist skills that match the project and remove the rest.
5. Start a numbered session when real work begins.
6. Use `handoff` when work pauses and `wrap-up` when the session ends.

## Reading order

At the start of a session, an agent should read these files in order:

1. `AGENTS.md` or `.claude/CLAUDE.md`: the agent instruction file.
2. `spec/sessions/README.md`: the sessions routing file.
3. The highest-numbered `spec/sessions/session-XX.md` file: the current numbered session file. Treat it as active unless it contains an explicit end marker such as `Session ended` or `Today's work is done`.
4. `spec/sessions/HANDOFF.md`: the handoff file, if it exists and contains an active handoff.
5. `spec/identity/README.md`: the identity routing file, if it exists. If it does not exist, continue.
6. `spec/identity/project-dna.md`: the project identity file, if it exists. If it does not exist, continue.
7. `spec/identity/brand-voice.md` and `spec/identity/TONE.md`: read each file if it exists when writing product copy or other identity-sensitive content. If a file does not exist, continue without it.

The session workflow comes first. Identity files add product and brand context when the project needs them.

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
