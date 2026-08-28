---
name: wrap-up
description: Record verified end-of-session facts in numbered files under spec/sessions/. Use the session template, update the latest open session, and verify file paths.
---

# Wrap up

Run this at the end of a work session or before the conversation is compacted.

1. Use numbered session files in `spec/sessions/`, such as `session-01.md` and `session-02.md`.
2. Find the highest existing session number.
   - If there is no session file yet: create `session-01.md` from `spec/sessions/templates/SESSION_TEMPLATE.md`.
   - If the latest session is still open: append to that file.
   - If the latest session is clearly ended: create the next numbered file from `spec/sessions/templates/SESSION_TEMPLATE.md`.
3. Treat the latest session as ended only when its note has an explicit end marker, such as `Session ended`, `Today's work is done`, or `Start a new session note next time`.
4. Treat user instructions such as `start a new session note`, `new session`, `session ended`, or `today's work is done` as a signal to close the current session and create the next numbered file at the next wrap-up.
5. When appending to an open session, update only verified sections. Do not create duplicate headers.
6. When creating a new session file, use two-digit zero-padded numbering and continue from the highest existing number.
7. Record only true, verified facts. Use one line per entry. Do not include work in progress.
8. In Decisions, record only irreversible or architectural choices.
9. In Blockers, number active blockers, strike resolved blockers, and do not add timestamps or dates.
10. Verify every cited file path or line number before writing.
11. Confirm with: "Session logged."
