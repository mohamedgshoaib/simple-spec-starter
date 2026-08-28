---
name: handoff
description: Compact the current conversation into a handoff document, or clear it when the user asks to clean up, clean, clear, reset, or empty the handoff.
argument-hint: "What will the next session be used for?"
disable-model-invocation: true
---

Read `spec/sessions/templates/HANDOFF_TEMPLATE.md` before writing.
Follow the template structure exactly unless a section is genuinely not applicable.
Keep the handoff compact, factual, and non-persuasive.

If the user asks to clean up, clean, clear, reset, empty, or use similar wording to remove the handoff, replace the entire contents of `spec/sessions/HANDOFF.md` with exactly `No active handoff.` Do not delete `HANDOFF.md`.

Write a handoff to `spec/sessions/HANDOFF.md` summarising the current conversation so a fresh agent can continue the work, conversation will be compacted.

Include a "suggested skills" section in the document, which suggests skills that the agent should invoke, and include the current scope of work and what's next, and what principles or workflows are established with the user in current conversation that should carry forward.

Do not duplicate content already captured in other artifacts (CLAUDE.md, AGENTS.md), only reference and guide the agent on where to look, do not bloat the agent's context window.

Redact any sensitive information, such as API keys, passwords, or personally identifiable information.

If the user passed arguments, treat them as a description of what the next session will focus on and tailor accordingly.
