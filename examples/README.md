# About `settings-allowlist.json`

This is **optional**. It stops Claude asking "Allow?" every time a scheduled task reads your email or updates your planner. Clicking **Always allow** on each prompt does the same thing, one tool at a time, and is the easiest option.

## The connector IDs are different for everyone

`<GMAIL_ID>` and `<CALENDAR_ID>` are placeholders. Each person's Gmail and Google Calendar connectors get their own long ID, for example `mcp__1a2b3c4d-....__search_threads`. Copying someone else's file won't work.

The easy way: run `/household-assistant:setup`. It finds your IDs and fills them in for you, and it asks before changing your settings.

To do it by hand: after you've clicked "Always allow" once for a Gmail tool, open `~/.claude/settings.json` and you'll see the full name, starting `mcp__` and ending `__search_threads` or similar. The part in the middle is your ID.

## What's in it, and what to leave out

- **Reading** files in `~/.claude/scheduled-tasks/`, searching and reading email, listing calendars: safe to allow.
- **Editing** files in `~/.claude/scheduled-tasks/`: lets the tasks update their own state file and playbook.
- `ArtifactData`: lets the tasks read and update your family planner.
- `create_draft` / `update_draft`: drafts only; nothing goes out.
- `create_event` / `update_event`: adds or changes events. The task prompts only allow this on your personal calendar, never the work one.
- `send_message` and `reply`: **these send real email.** The task prompts only send to you, or under the standing approvals you chose, or after you've approved a draft. If you'd like Claude to ask you every single time something is sent, delete these two lines. We recommend that for your first few weeks.

Nothing here allows deleting email, trashing messages, deleting events or forwarding mail.

## Where it goes

Merge the `allow` list into `~/.claude/settings.json` (Windows: `%USERPROFILE%\.claude\settings.json`). Keep anything already in that file.
