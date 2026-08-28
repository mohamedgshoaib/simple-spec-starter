# simple-spec-starter

A small starter for spec-driven development with AI agents.

It keeps product decisions, working context, and session notes in separate places so you can return later or hand the work to another agent.

## what this is

This starter gives you a small set of folders and files:

- `spec/identity/` for durable product truth
- `spec/sessions/` for short-lived working state
- `.agents/skills/` and `.claude/skills/` for local skills you want agents to use
- `AGENTS.md` and `.claude/CLAUDE.md` for repo behavior rules

That is the whole setup. There is no heavy framework, large planning system, or process for its own sake.

## how to use it

Copy the contents of this repo into the root of your existing project or a new project.

Then:

1. Fill `spec/identity/project-dna.md`
2. Fill `spec/identity/brand-voice.md`
3. Fill `spec/identity/TONE.md`
4. Keep `AGENTS.md` at the repo root and `.claude/CLAUDE.md` at the `.claude` directory root
5. Start `spec/sessions/session-01.md` from the template when real work begins
6. Keep `HANDOFF.md` empty or set to `No active handoff.` until a handoff is needed

Product truth lives in `identity`, active work lives in `sessions`, and agent behavior lives in the root instructions.

## why work this way

Projects often lose time when context gets muddy. Product ideas shift, old decisions disappear into chat history, and each new session starts by explaining the same things again.

Spec-driven development helps by separating three kinds of truth:

- Long-term truth: what the product is, who it serves, and what it should never become
- Session truth: what is finished, what is blocked, and which decisions are locked
- Agent rules: how work should be done in this repo

This gives the agent fewer gaps to fill and helps it stay aligned with the product.

## a normal work session

The flow is:

1. You open the repo and the agent reads `spec/identity/` first.
2. It reads the latest open session in `spec/sessions/`.
3. You say: "Add onboarding for first-time users."
4. The agent checks whether this is a new feature. If it is, the agent writes the spec before coding.
5. During the work, the session file records only verified outcomes such as "onboarding entry point added," "empty state copy approved," and "analytics event still blocked by missing event name."
6. If you stop mid-session, `HANDOFF.md` tells the next agent what is in scope and what comes next.

The next session can start with the current facts instead of reconstructing the past.

## two skills that matter most

- `handoff` writes a compact continuation note to `spec/sessions/HANDOFF.md` so a fresh agent can continue without replaying the whole chat.
- `wrap-up` updates the numbered session log with verified facts only so the repo records what happened.

Use `handoff` when work is paused and another session will pick it up. Use `wrap-up` at the end of a work session or before context gets compacted.

## why these starter skills exist

- `codebase-design` gives a shared vocabulary for interfaces, module depth, and testability.
- `commit-message` writes a commit message that is factual, compact, and non-persuasive.
- `deslop` cleans AI-shaped code that does not match the branch or codebase.
- `grilling` sharpens a feature or design before code starts.
- `handoff` preserves only the next agent's continuation context.
- `improve-codebase-architecture` finds architectural friction and turns it into concrete refactor candidates.
- `make-interfaces-feel-better` gives design principles for polished interfaces.
- `no-use-effect` enforces a stricter React posture and replaces lazy effect usage with better patterns.
- `typescript-expert` is the fallback specialist for hard TypeScript and JavaScript problems.
- `unslop` cleans AI-shaped writing so text sounds normal.
- `vercel-react-best-practices` keeps React and Next.js work aligned with strong performance defaults.
- `wrap-up` keeps session logs factual, compact, and usable.
- `write-project-readme` writes a project README that is factual and reflects the project's current state.

## when to use this

Use this starter when:

- you work with AI agents regularly
- the project will span more than a few sessions
- product direction matters as much as code output
- you want continuity without adding process for its own sake

## when not to use this

Skip it when:

- you are making a throwaway script
- the project is tiny and will be finished in one sitting
- nobody needs handoff, continuity, or product-level thinking
- a full PRD system already exists and this would duplicate it

## final note

This starter is intentionally small. If a file does not make future work clearer or easier to resume, it probably does not belong here.
