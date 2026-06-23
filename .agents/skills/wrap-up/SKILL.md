---
name: wrap-up
description: End-of-session log for numbered session files in spec/sessions/. Use the session template, append to the latest open session, and verify all file paths.
---

# Wrap Up

Run at the end of every work session or before context gets compacted.

1. Use numbered session files in `spec/sessions/`: `session-01.md`, `session-02.md`, and so on.
2. Find the highest existing session number.
   - If there is no session file yet: create `session-01.md` from `spec/sessions/templates/SESSION_TEMPLATE.md`.
   - If the latest session is still open: append to that file.
   - If the latest session is clearly ended: create the next numbered file from `spec/sessions/templates/SESSION_TEMPLATE.md`.
3. Treat the latest session as ended only when the note already includes an explicit end marker such as `Session ended`, `Today's work is done`, `Start a new session note next time`, or equivalent wording that unambiguously closes the session.
4. Treat user instructions such as `start a new session note`, `new session`, `session ended`, or `today's work is done` as a signal to close the current session and create the next numbered file on the next wrap-up.
5. When appending to an open session, update only the verified sections. Do not create duplicate headers.
6. When creating a new session file, keep the filename numbering zero-padded to two digits and continue the sequence from the latest existing file.
7. Write only what is true and verified. One line per entry. No in-progress noise.
8. Decisions: log only irreversible or architectural choices.
9. Blockers: number them. Strike through resolved blockers. Do not add timestamps or dates.
10. Verify every file path or line number cited actually exists before writing.
11. Confirm: "Session logged."
