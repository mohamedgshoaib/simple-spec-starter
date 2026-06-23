# simple-spec-starter

A tiny starter for spec driven development with AI agents.

It keeps product thinking, working context, and session continuity clean enough that you can come back tomorrow, or hand the work to another agent, without losing the plot.

## what this is

This starter gives you a small structure:

- `spec/identity/` for durable product truth
- `spec/sessions/` for short lived working state
- `.agents/skills/` for local skills you want agents to use
- `AGENTS.md` and `CLAUDE.md` for repo behavior rules

That is it. No heavy framework. No giant planning system. No fake ceremony.

## how to use it

Copy the contents of this repo into the root of your existing project or a new project.

Then do this:

1. Fill `spec/identity/project-dna.md`
2. Fill `spec/identity/brand-voice.md`
3. Keep `AGENTS.md` and `CLAUDE.md` at the repo root
4. Start `spec/sessions/session-01.md` from the template when real work begins
5. Keep `HANDOFF.md` empty or set to `No active handoff.` until a handoff is actually needed

The point is simple: product truth lives in `identity`, active work lives in `sessions`, and agent behavior lives in the root instructions.

## why work this way

Most projects do not fail because people cannot code. They fail because context gets muddy. The product idea shifts, old decisions disappear into chat history, and every new session starts with re-explaining the same thing.

Spec driven development helps because it separates three kinds of truth:

- Long term truth: what the product is, who it serves, what it should never become
- Session truth: what was actually finished, what is blocked, what decision is locked
- Agent rules: how work should be done inside this repo

That makes AI more useful. It has less room to guess and a better chance of staying aligned with the product.

## a normal work session

Here is the flow:

1. You open the repo and the agent reads `spec/identity/` first.
2. It reads the latest open session in `spec/sessions/`.
3. You say: "Add onboarding for first time users."
4. The agent checks whether this is a new feature. If yes, it specs first before coding.
5. During the work, the session file records only verified outcomes such as "onboarding entry point added," "empty state copy approved," and "analytics event still blocked by missing event name."
6. If you stop mid stream, `HANDOFF.md` tells the next agent what is in scope and what comes next.

That means the next session does not start with "what were we doing again?"

## two skills that matter most

- `handoff` writes a compact continuation note into `spec/sessions/HANDOFF.md` so a fresh agent can continue without replaying the whole chat.
- `wrap-up` updates the numbered session log with verified facts only so the repo keeps a clean record of what actually happened.

Use `handoff` when work is paused and another session will pick it up. Use `wrap-up` at the end of a work session or before context gets compacted.

## why these starter skills exist

- `grill-me` sharpens a feature or design before code starts.
- `codebase-design` gives a shared vocabulary for seams, interfaces, depth, and testability.
- `improve-codebase-architecture` finds architectural friction and turns it into concrete refactor candidates.
- `handoff` preserves only the next agent's continuation context.
- `wrap-up` keeps session logs factual, compact, and usable.
- `deslop` cleans AI-shaped code that does not match the branch or codebase.
- `humanizer` cleans AI-shaped writing so docs and copy sound normal.
- `no-use-effect` enforces a stricter React posture and replaces lazy effect usage with better patterns.
- `typescript-expert` is the fallback specialist for hard TypeScript and JavaScript problems.
- `vercel-react-best-practices` keeps React and Next.js work aligned with strong performance defaults.

## when to use this

Use this starter when:

- you work with AI agents regularly
- the project will span more than a few sessions
- product direction matters as much as code output
- you want continuity without turning the repo into a process museum

## when not to use this

Skip it when:

- you are making a throwaway script
- the project is tiny and will be finished in one sitting
- nobody needs handoff, continuity, or product level thinking
- a full PRD system already exists and this would duplicate it

## final note

This starter is intentionally small. If a file does not make future work clearer or easier to resume, it probably does not belong here.
