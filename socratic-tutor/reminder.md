# Reminders

Track reminder state throughout the session as one of: **unset**, **set**, or
**opted out**. This state must be preserved in "save state" and restored by
"resume from:".

## When to prompt

- At **Session start (Step 5)**, right after presenting the initial skill map.
- During **"show progress"**, if reminder state is `unset`.
- Always frame reminder prompts as optional and easy to skip. Never block the tutoring
  flow waiting for reminder details if the user wants to jump straight into learning.

## Opt-out rule

If the user explicitly asks to skip/forget reminders or tells you not to ask again
(e.g., "forget reminders", "don't ask me about reminders", "no reminders"), set
reminder state to **opted out** and do not prompt for reminders again — not at session
start, not on "show progress" — unless the user explicitly asks to be reminded or runs
the "remind" command.

## Setup execution

When the user wants to set a reminder (one-time or recurring):

1. Ask for any missing details: one-time vs. recurring frequency, date/day(s), time,
   and timezone.
2. Use available **Calendar tools** to create the study event (one-time or recurring),
   enabling email notifications/alerts on the event if supported.
3. Use available **Email tools** to send/configure the reminder email. If native
   recurring email scheduling is unsupported, send an immediate confirmation/summary
   email and rely on the recurring calendar event's email notifications — let the user
   know briefly.
4. Once configured, update reminder state to **set**.

## Teardown on course completion

This is **automatic** — triggered by a passing final assessment, not by any user
command. Do not wait for the user to ask.

When the user passes the final assessment and the course is marked complete:

1. If reminder state is **set**, attempt to delete or cancel the recurring study event
   using available **Calendar tools**.
2. Notify the user that their study reminder has been automatically cancelled now that
   they've reached mastery — keep it brief and celebratory, not clinical.
3. If a confirmation/summary email was sent during setup, send a short
   **completion email** via Email tools noting that the course is done and the
   reminder has been cancelled.
4. If Calendar or Email tools are unavailable, inform the user that they should
   manually cancel the reminder they set up earlier.
5. Update reminder state to **completed** (distinct from `opted out` — signals the
   reminder was intentionally closed out after mastery, not suppressed mid-session).
6. Do not attempt teardown if reminder state is `unset` or `opted out`.
